# go1

## Introduction to Go 1

Go version 1, Go 1 for short, defines a language and a set of core libraries that provide a stable foundation for creating reliable products, projects, and publications.

The driving motivation for Go 1 is stability for its users. People should be able to write Go programs and expect that they will continue to compile and run without change, on a time scale of years, including in production environments such as Google App Engine. Similarly, people should be able to write books about Go, be able to say which version of Go the book is describing, and have that version number still be meaningful much later.

Code that compiles in Go 1 should, with few exceptions, continue to compile and run throughout the lifetime of that version, even as we issue updates and bug fixes such as Go version 1.1, 1.2, and so on. Other than critical fixes, changes made to the language and library for subsequent releases of Go 1 may add functionality but will not break existing Go 1 programs. [The Go 1 compatibility document](/broken/pages/fb79d03442bc82eb9c0cda5e01877c7e5973517d) explains the compatibility guidelines in more detail.

Go 1 is a representation of Go as it used today, not a wholesale rethinking of the language. We avoided designing new features and instead focused on cleaning up problems and inconsistencies and improving portability. There are a number changes to the Go language and packages that we had considered for some time and prototyped but not released primarily because they are significant and backwards-incompatible. Go 1 was an opportunity to get them out, which is helpful for the long term, but also means that Go 1 introduces incompatibilities for old programs. Fortunately, the `go` `fix` tool can automate much of the work needed to bring programs up to the Go 1 standard.

This document outlines the major changes in Go 1 that will affect programmers updating existing code; its reference point is the prior release, r60 (tagged as r60.3). It also explains how to update code from r60 to run under Go 1.

## Changes to the language

### Append

The `append` predeclared variadic function makes it easy to grow a slice by adding elements to the end. A common use is to add bytes to the end of a byte slice when generating output. However, `append` did not provide a way to append a string to a `[]byte`, which is another common case.

```go
greeting := []byte{}
greeting = append(greeting, []byte("hello ")...)
```

By analogy with the similar property of `copy`, Go 1 permits a string to be appended (byte-wise) directly to a byte slice, reducing the friction between strings and byte slices. The conversion is no longer necessary:

```go
greeting = append(greeting, "world"...)
```

Updating: This is a new feature, so existing code needs no changes.

### Close

The `close` predeclared function provides a mechanism for a sender to signal that no more values will be sent. It is important to the implementation of `for` `range` loops over channels and is helpful in other situations. Partly by design and partly because of race conditions that can occur otherwise, it is intended for use only by the goroutine sending on the channel, not by the goroutine receiving data. However, before Go 1 there was no compile-time checking that `close` was being used correctly.

To close this gap, at least in part, Go 1 disallows `close` on receive-only channels. Attempting to close such a channel is a compile-time error.

```go
var c chan int
var csend chan<- int = c
var crecv <-chan int = c

close(c)      // legal
close(csend)  // legal
close(crecv)  // illegal
```

Updating: Existing code that attempts to close a receive-only channel was erroneous even before Go 1 and should be fixed. The compiler will now reject such code.

### Composite literals

In Go 1, a composite literal of array, slice, or map type can elide the type specification for the elements' initializers if they are of pointer type. All four of the initializations in this example are legal; the last one was illegal before Go 1.

```go
type Date struct {
    month string
    day   int
}

// Struct values, fully qualified; always legal.
holiday1 := []Date{
    Date{"Feb", 14},
    Date{"Nov", 11},
    Date{"Dec", 25},
}

// Struct values, type name elided; always legal.
holiday2 := []Date{
    {"Feb", 14},
    {"Nov", 11},
    {"Dec", 25},
}

// Pointers, fully qualified, always legal.
holiday3 := []*Date{
    &Date{"Feb", 14},
    &Date{"Nov", 11},
    &Date{"Dec", 25},
}

// Pointers, type name elided; legal in Go 1.
holiday4 := []*Date{
    {"Feb", 14},
    {"Nov", 11},
    {"Dec", 25},
}
```

Updating: This change has no effect on existing code, but the command `gofmt -s` applied to existing source will, among other things, elide explicit element types wherever permitted.

### Goroutines during init

The old language defined that `go` statements executed during initialization created goroutines but that they did not begin to run until initialization of the entire program was complete. This introduced clumsiness in many places and, in effect, limited the utility of the `init` construct: if it was possible for another package to use the library during initialization, the library was forced to avoid goroutines. This design was done for reasons of simplicity and safety but, as our confidence in the language grew, it seemed unnecessary. Running goroutines during initialization is no more complex or unsafe than running them during normal execution.

In Go 1, code that uses goroutines can be called from `init` routines and global initialization expressions without introducing a deadlock.

```go
var PackageGlobal int

func init() {
    c := make(chan int)
    go initializationFunction(c)
    PackageGlobal = <-c
}
```

Updating: This is a new feature, so existing code needs no changes, although it's possible that code that depends on goroutines not starting before `main` will break. There was no such code in the standard repository.

### The rune type

The language spec allows the `int` type to be 32 or 64 bits wide, but current implementations set `int` to 32 bits even on 64-bit platforms. It would be preferable to have `int` be 64 bits on 64-bit platforms. (There are important consequences for indexing large slices.) However, this change would waste space when processing Unicode characters with the old language because the `int` type was also used to hold Unicode code points: each code point would waste an extra 32 bits of storage if `int` grew from 32 bits to 64.

To make changing to 64-bit `int` feasible, Go 1 introduces a new basic type, `rune`, to represent individual Unicode code points. It is an alias for `int32`, analogous to `byte` as an alias for `uint8`.

Character literals such as `'a'`, `'語'`, and `'\u0345'` now have default type `rune`, analogous to `1.0` having default type `float64`. A variable initialized to a character constant will therefore have type `rune` unless otherwise specified.

Libraries have been updated to use `rune` rather than `int` when appropriate. For instance, the functions `unicode.ToLower` and relatives now take and return a `rune`.

```go
delta := 'δ' // delta has type rune.
var DELTA rune
DELTA = unicode.ToUpper(delta)
epsilon := unicode.ToLower(DELTA + 1)
if epsilon != 'δ'+1 {
    log.Fatal("inconsistent casing for Greek")
}
```

Updating: Most source code will be unaffected by this because the type inference from `:=` initializers introduces the new type silently, and it propagates from there. Some code may get type errors that a trivial conversion will resolve.

### The error type

Go 1 introduces a new built-in type, `error`, which has the following definition:

```go
type error interface {
    Error() string
}
```

Since the consequences of this type are all in the package library, it is discussed below in the errors package section.

### Deleting from maps

In the old language, to delete the entry with key `k` from map `m`, one wrote the statement:

```go
m[k] = value, false
```

This syntax was a peculiar special case, the only two-to-one assignment. It required passing a value (usually ignored) that is evaluated but discarded, plus a boolean that was nearly always the constant `false`. It did the job but was odd and a point of contention.

In Go 1, that syntax has gone; instead there is a new built-in function, `delete`. The call

```go
delete(m, k)
```

will delete the map entry retrieved by the expression `m[k]`. There is no return value. Deleting a non-existent entry is a no-op.

Updating: Running `go fix` will convert expressions of the form `m[k] = value, false` into `delete(m, k)` when it is clear that the ignored value can be safely discarded from the program and `false` refers to the predefined boolean constant. The fix tool will flag other uses of the syntax for inspection by the programmer.

### Iterating in maps

The old language specification did not define the order of iteration for maps, and in practice it differed across hardware platforms. This caused tests that iterated over maps to be fragile and non-portable, with the unpleasant property that a test might always pass on one machine but break on another.

In Go 1, the order in which elements are visited when iterating over a map using a `for` `range` statement is defined to be unpredictable, even if the same loop is run multiple times with the same map. Code should not assume that the elements are visited in any particular order.

This change means that code that depends on iteration order is very likely to break early and be fixed long before it becomes a problem. Just as important, it allows the map implementation to ensure better map balancing even when programs are using range loops to select an element from a map.

```go
m := map[string]int{"Sunday": 0, "Monday": 1}
for name, value := range m {
    // This loop should not assume Sunday will be visited first.
    f(name, value)
}
```

Updating: This is one change where tools cannot help. Most existing code will be unaffected, but some programs may break or misbehave; we recommend manual checking of all range statements over maps to verify they do not depend on iteration order. There were a few such examples in the standard repository; they have been fixed. Note that it was already incorrect to depend on the iteration order, which was unspecified. This change codifies the unpredictability.

### Multiple assignment

The language specification has long guaranteed that in assignments the right-hand-side expressions are all evaluated before any left-hand-side expressions are assigned. To guarantee predictable behavior, Go 1 refines the specification further.

If the left-hand side of the assignment statement contains expressions that require evaluation, such as function calls or array indexing operations, these will all be done using the usual left-to-right rule before any variables are assigned their value. Once everything is evaluated, the actual assignments proceed in left-to-right order.

These examples illustrate the behavior.

```go
sa := []int{1, 2, 3}
i := 0
i, sa[i] = 1, 2 // sets i = 1, sa[0] = 2

sb := []int{1, 2, 3}
j := 0
sb[j], j = 2, 1 // sets sb[0] = 2, j = 1

sc := []int{1, 2, 3}
sc[0], sc[0] = 1, 2 // sets sc[0] = 1, then sc[0] = 2 (so sc[0] = 2 at end)
```

Updating: This is one change where tools cannot help, but breakage is unlikely. No code in the standard repository was broken by this change, and code that depended on the previous unspecified behavior was already incorrect.

### Returns and shadowed variables

A common mistake is to use `return` (without arguments) after an assignment to a variable that has the same name as a result variable but is not the same variable. This situation is called shadowing: the result variable has been shadowed by another variable with the same name declared in an inner scope.

In functions with named return values, the Go 1 compilers disallow return statements without arguments if any of the named return values is shadowed at the point of the return statement. (It isn't part of the specification, because this is one area we are still exploring; the situation is analogous to the compilers rejecting functions that do not end with an explicit return statement.)

This function implicitly returns a shadowed return value and will be rejected by the compiler:

```go
func Bug() (i, j, k int) {
    for i = 0; i < 5; i++ {
        for j := 0; j < 5; j++ { // Redeclares j.
            k += i*j
            if k > 100 {
                return // Rejected: j is shadowed here.
            }
        }
    }
    return // OK: j is not shadowed here.
}
```

Updating: Code that shadows return values in this way will be rejected by the compiler and will need to be fixed by hand. The few cases that arose in the standard repository were mostly bugs.

### Copying structs with unexported fields

The old language did not allow a package to make a copy of a struct value containing unexported fields belonging to a different package. There was, however, a required exception for a method receiver; also, the implementations of `copy` and `append` have never honored the restriction.

Go 1 will allow packages to copy struct values containing unexported fields from other packages. Besides resolving the inconsistency, this change admits a new kind of API: a package can return an opaque value without resorting to a pointer or interface. The new implementations of `time.Time` and `reflect.Value` are examples of types taking advantage of this new property.

As an example, if package `p` includes the definitions:

```go
type Struct struct {
    Public int
    secret int
}

func NewStruct(a int) Struct { // Note: not a pointer.
    return Struct{a, f(a)}
}

func (s Struct) String() string {
    return fmt.Sprintf("{%d (secret %d)}", s.Public, s.secret)
}
```

a package that imports `p` can assign and copy values of type `p.Struct` at will. Behind the scenes the unexported fields will be assigned and copied just as if they were exported, but the client code will never be aware of them. The code

```go
import "p"

myStruct := p.NewStruct(23)
copyOfMyStruct := myStruct
fmt.Println(myStruct, copyOfMyStruct)
```

will show that the secret field of the struct has been copied to the new value.

Updating: This is a new feature, so existing code needs no changes.

### Equality

Before Go 1, the language did not define equality on struct and array values. This meant, among other things, that structs and arrays could not be used as map keys. On the other hand, Go did define equality on function and map values. Function equality was problematic in the presence of closures (when are two closures equal?) while map equality compared pointers, not the maps' content, which was usually not what the user would want.

Go 1 addressed these issues. First, structs and arrays can be compared for equality and inequality (`==` and `!=`), and therefore be used as map keys, provided they are composed from elements for which equality is also defined, using element-wise comparison.

```go
type Day struct {
    long  string
    short string
}

Christmas := Day{"Christmas", "XMas"}
Thanksgiving := Day{"Thanksgiving", "Turkey"}

holiday := map[Day]bool{
    Christmas:    true,
    Thanksgiving: true,
}

fmt.Printf("Christmas is a holiday: %t\n", holiday[Christmas])
```

Second, Go 1 removes the definition of equality for function values, except for comparison with `nil`. Finally, map equality is gone too, also except for comparison with `nil`.

Note that equality is still undefined for slices, for which the calculation is in general infeasible. Also note that the ordered comparison operators (`<` `<=` `>` `>=`) are still undefined for structs and arrays.

Updating: Struct and array equality is a new feature, so existing code needs no changes. Existing code that depends on function or map equality will be rejected by the compiler and will need to be fixed by hand. Few programs will be affected, but the fix may require some redesign.

## The package hierarchy

Go 1 addresses many deficiencies in the old standard library and cleans up a number of packages, making them more internally consistent and portable.

This section describes how the packages have been rearranged in Go 1. Some have moved, some have been renamed, some have been deleted. New packages are described in later sections.

### The package hierarchy

Go 1 has a rearranged package hierarchy that groups related items into subdirectories. For instance, `utf8` and `utf16` now occupy subdirectories of `unicode`. Also, [some packages](go1.md#subrepo) have moved into subrepositories of [`code.google.com/p/go`](http://code.google.com/p/go) while [others](go1.md#deleted) have been deleted outright.

| Old path          | New path            |
| ----------------- | ------------------- |
| asn1              | encoding/asn1       |
| csv               | encoding/csv        |
| gob               | encoding/gob        |
| json              | encoding/json       |
| xml               | encoding/xml        |
| exp/template/html | html/template       |
| big               | math/big            |
| cmath             | math/cmplx          |
| rand              | math/rand           |
| http              | net/http            |
| http/cgi          | net/http/cgi        |
| http/fcgi         | net/http/fcgi       |
| http/httptest     | net/http/httptest   |
| http/pprof        | net/http/pprof      |
| mail              | net/mail            |
| rpc               | net/rpc             |
| rpc/jsonrpc       | net/rpc/jsonrpc     |
| smtp              | net/smtp            |
| url               | net/url             |
| exec              | os/exec             |
| scanner           | text/scanner        |
| tabwriter         | text/tabwriter      |
| template          | text/template       |
| template/parse    | text/template/parse |
| utf8              | unicode/utf8        |
| utf16             | unicode/utf16       |

Note that the package names for the old `cmath` and `exp/template/html` packages have changed to `cmplx` and `template`.

Updating: Running `go fix` will update all imports and package renames for packages that remain inside the standard repository. Programs that import packages that are no longer in the standard repository will need to be edited by hand.

### The package tree exp

Because they are not standardized, the packages under the `exp` directory will not be available in the standard Go 1 release distributions, although they will be available in source code form in [the repository](http://code.google.com/p/go/) for developers who wish to use them.

Several packages have moved under `exp` at the time of Go 1's release:

* `ebnf`
* `html`†
* `go/types`

(†The `EscapeString` and `UnescapeString` types remain in package `html`.)

All these packages are available under the same names, with the prefix `exp/`: `exp/ebnf` etc.

Also, the `utf8.String` type has been moved to its own package, `exp/utf8string`.

Finally, the `gotype` command now resides in `exp/gotype`, while `ebnflint` is now in `exp/ebnflint`. If they are installed, they now reside in `$GOROOT/bin/tool`.

Updating: Code that uses packages in `exp` will need to be updated by hand, or else compiled from an installation that has `exp` available. The `go fix` tool or the compiler will complain about such uses.

### The package tree old

Because they are deprecated, the packages under the `old` directory will not be available in the standard Go 1 release distributions, although they will be available in source code form for developers who wish to use them.

The packages in their new locations are:

* `old/netchan`
* `old/regexp`
* `old/template`

Updating: Code that uses packages now in `old` will need to be updated by hand, or else compiled from an installation that has `old` available. The `go fix` tool will warn about such uses.

### Deleted packages

Go 1 deletes several packages outright:

* `container/vector`
* `exp/datafmt`
* `go/typechecker`
* `try`

and also the command `gotry`.

Updating: Code that uses `container/vector` should be updated to use slices directly. See [the Go Language Community Wiki](http://code.google.com/p/go-wiki/wiki/SliceTricks) for some suggestions. Code that uses the other packages (there should be almost zero) will need to be rethought.

### Packages moving to subrepositories

Go 1 has moved a number of packages into other repositories, usually sub-repositories of [the main Go repository](http://code.google.com/p/go/). This table lists the old and new import paths:

| Old                    | New                                         |
| ---------------------- | ------------------------------------------- |
| crypto/bcrypt          | code.google.com/p/go.crypto/bcrypt          |
| crypto/blowfish        | code.google.com/p/go.crypto/blowfish        |
| crypto/cast5           | code.google.com/p/go.crypto/cast5           |
| crypto/md4             | code.google.com/p/go.crypto/md4             |
| crypto/ocsp            | code.google.com/p/go.crypto/ocsp            |
| crypto/openpgp         | code.google.com/p/go.crypto/openpgp         |
| crypto/openpgp/armor   | code.google.com/p/go.crypto/openpgp/armor   |
| crypto/openpgp/elgamal | code.google.com/p/go.crypto/openpgp/elgamal |
| crypto/openpgp/errors  | code.google.com/p/go.crypto/openpgp/errors  |
| crypto/openpgp/packet  | code.google.com/p/go.crypto/openpgp/packet  |
| crypto/openpgp/s2k     | code.google.com/p/go.crypto/openpgp/s2k     |
| crypto/ripemd160       | code.google.com/p/go.crypto/ripemd160       |
| crypto/twofish         | code.google.com/p/go.crypto/twofish         |
| crypto/xtea            | code.google.com/p/go.crypto/xtea            |
| exp/ssh                | code.google.com/p/go.crypto/ssh             |
| image/bmp              | code.google.com/p/go.image/bmp              |
| image/tiff             | code.google.com/p/go.image/tiff             |
| net/dict               | code.google.com/p/go.net/dict               |
| net/websocket          | code.google.com/p/go.net/websocket          |
| exp/spdy               | code.google.com/p/go.net/spdy               |
| encoding/git85         | code.google.com/p/go.codereview/git85       |
| patch                  | code.google.com/p/go.codereview/patch       |
| exp/wingui             | code.google.com/p/gowingui                  |

Updating: Running `go fix` will update imports of these packages to use the new import paths. Installations that depend on these packages will need to install them using a `go get` command.

## Major changes to the library

This section describes significant changes to the core libraries, the ones that affect the most programs.

### The error type and errors package

The placement of `os.Error` in package `os` is mostly historical: errors first came up when implementing package `os`, and they seemed system-related at the time. Since then it has become clear that errors are more fundamental than the operating system. For example, it would be nice to use `Errors` in packages that `os` depends on, like `syscall`. Also, having `Error` in `os` introduces many dependencies on `os` that would otherwise not exist.

Go 1 solves these problems by introducing a built-in `error` interface type and a separate `errors` package (analogous to `bytes` and `strings`) that contains utility functions. It replaces `os.NewError` with [`errors.New`](file:///pkg/errors/#New), giving errors a more central place in the environment.

So the widely-used `String` method does not cause accidental satisfaction of the `error` interface, the `error` interface uses instead the name `Error` for that method:

```go
type error interface {
    Error() string
}
```

The `fmt` library automatically invokes `Error`, as it already does for `String`, for easy printing of error values.

```go
type SyntaxError struct {
    File    string
    Line    int
    Message string
}

func (se *SyntaxError) Error() string {
    return fmt.Sprintf("%s:%d: %s", se.File, se.Line, se.Message)
}
```

All standard packages have been updated to use the new interface; the old `os.Error` is gone.

A new package, [`errors`](file:///pkg/errors/), contains the function

```go
func New(text string) error
```

to turn a string into an error. It replaces the old `os.NewError`.

```go
var ErrSyntax = errors.New("syntax error")
```

Updating: Running `go fix` will update almost all code affected by the change. Code that defines error types with a `String` method will need to be updated by hand to rename the methods to `Error`.

### System call errors

The old `syscall` package, which predated `os.Error` (and just about everything else), returned errors as `int` values. In turn, the `os` package forwarded many of these errors, such as `EINVAL`, but using a different set of errors on each platform. This behavior was unpleasant and unportable.

In Go 1, the [`syscall`](file:///pkg/syscall/) package instead returns an `error` for system call errors. On Unix, the implementation is done by a [`syscall.Errno`](file:///pkg/syscall/#Errno) type that satisfies `error` and replaces the old `os.Errno`.

The changes affecting `os.EINVAL` and relatives are described elsewhere.

Updating: Running `go fix` will update almost all code affected by the change. Regardless, most code should use the `os` package rather than `syscall` and so will be unaffected.

### Time

Time is always a challenge to support well in a programming language. The old Go `time` package had `int64` units, no real type safety, and no distinction between absolute times and durations.

One of the most sweeping changes in the Go 1 library is therefore a complete redesign of the [`time`](file:///pkg/time/) package. Instead of an integer number of nanoseconds as an `int64`, and a separate `*time.Time` type to deal with human units such as hours and years, there are now two fundamental types: [`time.Time`](file:///pkg/time/#Time) (a value, so the `*` is gone), which represents a moment in time; and [`time.Duration`](file:///pkg/time/#Duration), which represents an interval. Both have nanosecond resolution. A `Time` can represent any time into the ancient past and remote future, while a `Duration` can span plus or minus only about 290 years. There are methods on these types, plus a number of helpful predefined constant durations such as `time.Second`.

Among the new methods are things like [`Time.Add`](file:///pkg/time/#Time.Add), which adds a `Duration` to a `Time`, and [`Time.Sub`](file:///pkg/time/#Time.Sub), which subtracts two `Times` to yield a `Duration`.

The most important semantic change is that the Unix epoch (Jan 1, 1970) is now relevant only for those functions and methods that mention Unix: [`time.Unix`](file:///pkg/time/#Unix) and the [`Unix`](file:///pkg/time/#Time.Unix) and [`UnixNano`](file:///pkg/time/#Time.UnixNano) methods of the `Time` type. In particular, [`time.Now`](file:///pkg/time/#Now) returns a `time.Time` value rather than, in the old API, an integer nanosecond count since the Unix epoch.

```go
// sleepUntil sleeps until the specified time. It returns immediately if it's too late.
func sleepUntil(wakeup time.Time) {
    now := time.Now() // A Time.
    if !wakeup.After(now) {
        return
    }
    delta := wakeup.Sub(now) // A Duration.
    fmt.Printf("Sleeping for %.3fs\n", delta.Seconds())
    time.Sleep(delta)
}
```

The new types, methods, and constants have been propagated through all the standard packages that use time, such as `os` and its representation of file time stamps.

Updating: The `go fix` tool will update many uses of the old `time` package to use the new types and methods, although it does not replace values such as `1e9` representing nanoseconds per second. Also, because of type changes in some of the values that arise, some of the expressions rewritten by the fix tool may require further hand editing; in such cases the rewrite will include the correct function or method for the old functionality, but may have the wrong type or require further analysis.

## Minor changes to the library

This section describes smaller changes, such as those to less commonly used packages or that affect few programs beyond the need to run `go fix`. This category includes packages that are new in Go 1. Collectively they improve portability, regularize behavior, and make the interfaces more modern and Go-like.

### The archive/zip package

In Go 1, [`*zip.Writer`](file:///pkg/archive/zip/#Writer) no longer has a `Write` method. Its presence was a mistake.

Updating: What little code is affected will be caught by the compiler and must be updated by hand.

### The bufio package

In Go 1, [`bufio.NewReaderSize`](file:///pkg/bufio/#NewReaderSize) and [`bufio.NewWriterSize`](file:///pkg/bufio/#NewWriterSize) functions no longer return an error for invalid sizes. If the argument size is too small or invalid, it is adjusted.

Updating: Running `go fix` will update calls that assign the error to \_. Calls that aren't fixed will be caught by the compiler and must be updated by hand.

### The compress/flate, compress/gzip and compress/zlib packages

In Go 1, the `NewWriterXxx` functions in [`compress/flate`](file:///pkg/compress/flate), [`compress/gzip`](file:///pkg/compress/gzip) and [`compress/zlib`](file:///pkg/compress/zlib) all return `(*Writer, error)` if they take a compression level, and `*Writer` otherwise. Package `gzip`'s `Compressor` and `Decompressor` types have been renamed to `Writer` and `Reader`. Package `flate`'s `WrongValueError` type has been removed.

Updating: Running `go fix` will update old names and calls that assign the error to \_. Calls that aren't fixed will be caught by the compiler and must be updated by hand.

### The crypto/aes and crypto/des packages

In Go 1, the `Reset` method has been removed. Go does not guarantee that memory is not copied and therefore this method was misleading.

The cipher-specific types `*aes.Cipher`, `*des.Cipher`, and `*des.TripleDESCipher` have been removed in favor of `cipher.Block`.

Updating: Remove the calls to Reset. Replace uses of the specific cipher types with cipher.Block.

### The crypto/elliptic package

In Go 1, [`elliptic.Curve`](file:///pkg/crypto/elliptic/#Curve) has been made an interface to permit alternative implementations. The curve parameters have been moved to the [`elliptic.CurveParams`](file:///pkg/crypto/elliptic/#CurveParams) structure.

Updating: Existing users of `*elliptic.Curve` will need to change to simply `elliptic.Curve`. Calls to `Marshal`, `Unmarshal` and `GenerateKey` are now functions in `crypto/elliptic` that take an `elliptic.Curve` as their first argument.

### The crypto/hmac package

In Go 1, the hash-specific functions, such as `hmac.NewMD5`, have been removed from `crypto/hmac`. Instead, `hmac.New` takes a function that returns a `hash.Hash`, such as `md5.New`.

Updating: Running `go fix` will perform the needed changes.

### The crypto/x509 package

In Go 1, the [`CreateCertificate`](file:///pkg/crypto/x509/#CreateCertificate) and [`CreateCRL`](file:///pkg/crypto/x509/#CreateCRL) functions in `crypto/x509` have been altered to take an `interface{}` where they previously took a `*rsa.PublicKey` or `*rsa.PrivateKey`. This will allow other public key algorithms to be implemented in the future.

Updating: No changes will be needed.

### The encoding/binary package

In Go 1, the `binary.TotalSize` function has been replaced by [`Size`](file:///pkg/encoding/binary/#Size), which takes an `interface{}` argument rather than a `reflect.Value`.

Updating: What little code is affected will be caught by the compiler and must be updated by hand.

### The encoding/xml package

In Go 1, the [`xml`](file:///pkg/encoding/xml/) package has been brought closer in design to the other marshaling packages such as [`encoding/gob`](file:///pkg/encoding/gob).

The old `Parser` type is renamed [`Decoder`](file:///pkg/encoding/xml/#Decoder) and has a new [`Decode`](file:///pkg/encoding/xml/#Decoder.Decode) method. An [`Encoder`](file:///pkg/encoding/xml/#Encoder) type was also introduced.

The functions [`Marshal`](file:///pkg/encoding/xml/#Marshal) and [`Unmarshal`](file:///pkg/encoding/xml/#Unmarshal) work with `[]byte` values now. To work with streams, use the new [`Encoder`](file:///pkg/encoding/xml/#Encoder) and [`Decoder`](file:///pkg/encoding/xml/#Decoder) types.

When marshaling or unmarshaling values, the format of supported flags in field tags has changed to be closer to the [`json`](file:///pkg/encoding/json) package (`\`xml:"name,flag"\``). The matching done between field tags, field names, and the XML attribute and element names is now case-sensitive. The` XMLName\` field tag, if present, must also match the name of the XML element being marshaled.

Updating: Running `go fix` will update most uses of the package except for some calls to `Unmarshal`. Special care must be taken with field tags, since the fix tool will not update them and if not fixed by hand they will misbehave silently in some cases. For example, the old `"attr"` is now written `",attr"` while plain `"attr"` remains valid but with a different meaning.

### The expvar package

In Go 1, the `RemoveAll` function has been removed. The `Iter` function and Iter method on `*Map` have been replaced by [`Do`](file:///pkg/expvar/#Do) and [`(*Map).Do`](file:///pkg/expvar/#Map.Do).

Updating: Most code using `expvar` will not need changing. The rare code that used `Iter` can be updated to pass a closure to `Do` to achieve the same effect.

### The flag package

In Go 1, the interface [`flag.Value`](file:///pkg/flag/#Value) has changed slightly. The `Set` method now returns an `error` instead of a `bool` to indicate success or failure.

There is also a new kind of flag, `Duration`, to support argument values specifying time intervals. Values for such flags must be given units, just as `time.Duration` formats them: `10s`, `1h30m`, etc.

```go
var timeout = flag.Duration("timeout", 30*time.Second, "how long to wait for completion")
```

Updating: Programs that implement their own flags will need minor manual fixes to update their `Set` methods. The `Duration` flag is new and affects no existing code.

### The go/\* packages

Several packages under `go` have slightly revised APIs.

A concrete `Mode` type was introduced for configuration mode flags in the packages [`go/scanner`](file:///pkg/go/scanner/), [`go/parser`](file:///pkg/go/parser/), [`go/printer`](file:///pkg/go/printer/), and [`go/doc`](file:///pkg/go/doc/).

The modes `AllowIllegalChars` and `InsertSemis` have been removed from the [`go/scanner`](file:///pkg/go/scanner/) package. They were mostly useful for scanning text other then Go source files. Instead, the [`text/scanner`](file:///pkg/text/scanner/) package should be used for that purpose.

The [`ErrorHandler`](file:///pkg/go/scanner/#ErrorHandler) provided to the scanner's [`Init`](file:///pkg/go/scanner/#Scanner.Init) method is now simply a function rather than an interface. The `ErrorVector` type has been removed in favor of the (existing) [`ErrorList`](file:///pkg/go/scanner/#ErrorList) type, and the `ErrorVector` methods have been migrated. Instead of embedding an `ErrorVector` in a client of the scanner, now a client should maintain an `ErrorList`.

The set of parse functions provided by the [`go/parser`](file:///pkg/go/parser/) package has been reduced to the primary parse function [`ParseFile`](file:///pkg/go/parser/#ParseFile), and a couple of convenience functions [`ParseDir`](file:///pkg/go/parser/#ParseDir) and [`ParseExpr`](file:///pkg/go/parser/#ParseExpr).

The [`go/printer`](file:///pkg/go/printer/) package supports an additional configuration mode [`SourcePos`](file:///pkg/go/printer/#Mode); if set, the printer will emit `//line` comments such that the generated output contains the original source code position information. The new type [`CommentedNode`](file:///pkg/go/printer/#CommentedNode) can be used to provide comments associated with an arbitrary [`ast.Node`](file:///pkg/go/ast/#Node) (until now only [`ast.File`](file:///pkg/go/ast/#File) carried comment information).

The type names of the [`go/doc`](file:///pkg/go/doc/) package have been streamlined by removing the `Doc` suffix: `PackageDoc` is now `Package`, `ValueDoc` is `Value`, etc. Also, all types now consistently have a `Name` field (or `Names`, in the case of type `Value`) and `Type.Factories` has become `Type.Funcs`. Instead of calling `doc.NewPackageDoc(pkg, importpath)`, documentation for a package is created with:

```go
doc.New(pkg, importpath, mode)
```

where the new `mode` parameter specifies the operation mode: if set to [`AllDecls`](file:///pkg/go/doc/#AllDecls), all declarations (not just exported ones) are considered. The function `NewFileDoc` was removed, and the function `CommentText` has become the method [`Text`](file:///pkg/go/ast/#Text) of [`ast.CommentGroup`](file:///pkg/go/ast/#CommentGroup).

In package [`go/token`](file:///pkg/go/token/), the [`token.FileSet`](file:///pkg/go/token/#FileSet) method `Files` (which originally returned a channel of `*token.File`s) has been replaced with the iterator [`Iterate`](file:///pkg/go/token/#FileSet.Iterate) that accepts a function argument instead.

In package [`go/build`](file:///pkg/go/build/), the API has been nearly completely replaced. The package still computes Go package information but it does not run the build: the `Cmd` and `Script` types are gone. (To build code, use the new [`go`](file:///cmd/go/) command instead.) The `DirInfo` type is now named [`Package`](file:///pkg/go/build/#Package). `FindTree` and `ScanDir` are replaced by [`Import`](file:///pkg/go/build/#Import) and [`ImportDir`](file:///pkg/go/build/#ImportDir).

Updating: Code that uses packages in `go` will have to be updated by hand; the compiler will reject incorrect uses. Templates used in conjunction with any of the `go/doc` types may need manual fixes; the renamed fields will lead to run-time errors.

### The hash package

In Go 1, the definition of [`hash.Hash`](file:///pkg/hash/#Hash) includes a new method, `BlockSize`. This new method is used primarily in the cryptographic libraries.

The `Sum` method of the [`hash.Hash`](file:///pkg/hash/#Hash) interface now takes a `[]byte` argument, to which the hash value will be appended. The previous behavior can be recreated by adding a `nil` argument to the call.

Updating: Existing implementations of `hash.Hash` will need to add a `BlockSize` method. Hashes that process the input one byte at a time can implement `BlockSize` to return 1. Running `go fix` will update calls to the `Sum` methods of the various implementations of `hash.Hash`.

### The http package

In Go 1 the [`http`](file:///pkg/net/http/) package is refactored, putting some of the utilities into a [`httputil`](file:///pkg/net/http/httputil/) subdirectory. These pieces are only rarely needed by HTTP clients. The affected items are:

* ClientConn
* DumpRequest
* DumpRequestOut
* DumpResponse
* NewChunkedReader
* NewChunkedWriter
* NewClientConn
* NewProxyClientConn
* NewServerConn
* NewSingleHostReverseProxy
* ReverseProxy
* ServerConn

The `Request.RawURL` field has been removed; it was a historical artifact.

The `Handle` and `HandleFunc` functions, and the similarly-named methods of `ServeMux`, now panic if an attempt is made to register the same pattern twice.

Updating: Running `go fix` will update the few programs that are affected except for uses of `RawURL`, which must be fixed by hand.

### The image package

The [`image`](file:///pkg/image/) package has had a number of minor changes, rearrangements and renamings.

Most of the color handling code has been moved into its own package, [`image/color`](file:///pkg/image/color/). For the elements that moved, a symmetry arises; for instance, each pixel of an [`image.RGBA`](file:///pkg/image/#RGBA) is a [`color.RGBA`](file:///pkg/image/color/#RGBA).

The old `image/ycbcr` package has been folded, with some renamings, into the [`image`](file:///pkg/image/) and [`image/color`](file:///pkg/image/color/) packages.

The old `image.ColorImage` type is still in the `image` package but has been renamed [`image.Uniform`](file:///pkg/image/#Uniform), while `image.Tiled` has been removed.

This table lists the renamings.

| Old                      | New                          |
| ------------------------ | ---------------------------- |
| image.Color              | color.Color                  |
| image.ColorModel         | color.Model                  |
| image.ColorModelFunc     | color.ModelFunc              |
| image.PalettedColorModel | color.Palette                |
| image.RGBAColor          | color.RGBA                   |
| image.RGBA64Color        | color.RGBA64                 |
| image.NRGBAColor         | color.NRGBA                  |
| image.NRGBA64Color       | color.NRGBA64                |
| image.AlphaColor         | color.Alpha                  |
| image.Alpha16Color       | color.Alpha16                |
| image.GrayColor          | color.Gray                   |
| image.Gray16Color        | color.Gray16                 |
| image.RGBAColorModel     | color.RGBAModel              |
| image.RGBA64ColorModel   | color.RGBA64Model            |
| image.NRGBAColorModel    | color.NRGBAModel             |
| image.NRGBA64ColorModel  | color.NRGBA64Model           |
| image.AlphaColorModel    | color.AlphaModel             |
| image.Alpha16ColorModel  | color.Alpha16Model           |
| image.GrayColorModel     | color.GrayModel              |
| image.Gray16ColorModel   | color.Gray16Model            |
| ycbcr.RGBToYCbCr         | color.RGBToYCbCr             |
| ycbcr.YCbCrToRGB         | color.YCbCrToRGB             |
| ycbcr.YCbCrColorModel    | color.YCbCrModel             |
| ycbcr.YCbCrColor         | color.YCbCr                  |
| ycbcr.YCbCr              | image.YCbCr                  |
| ycbcr.SubsampleRatio444  | image.YCbCrSubsampleRatio444 |
| ycbcr.SubsampleRatio422  | image.YCbCrSubsampleRatio422 |
| ycbcr.SubsampleRatio420  | image.YCbCrSubsampleRatio420 |
| image.ColorImage         | image.Uniform                |

The image package's `New` functions ([`NewRGBA`](file:///pkg/image/#NewRGBA), [`NewRGBA64`](file:///pkg/image/#NewRGBA64), etc.) take an [`image.Rectangle`](file:///pkg/image/#Rectangle) as an argument instead of four integers.

Finally, there are new predefined `color.Color` variables [`color.Black`](file:///pkg/image/color/#Black), [`color.White`](file:///pkg/image/color/#White), [`color.Opaque`](file:///pkg/image/color/#Opaque) and [`color.Transparent`](file:///pkg/image/color/#Transparent).

Updating: Running `go fix` will update almost all code affected by the change.

### The log/syslog package

In Go 1, the [`syslog.NewLogger`](file:///pkg/log/syslog/#NewLogger) function returns an error as well as a `log.Logger`.

Updating: What little code is affected will be caught by the compiler and must be updated by hand.

### The mime package

In Go 1, the [`FormatMediaType`](file:///pkg/mime/#FormatMediaType) function of the `mime` package has been simplified to make it consistent with [`ParseMediaType`](file:///pkg/mime/#ParseMediaType). It now takes `"text/html"` rather than `"text"` and `"html"`.

Updating: What little code is affected will be caught by the compiler and must be updated by hand.

### The net package

In Go 1, the various `SetTimeout`, `SetReadTimeout`, and `SetWriteTimeout` methods have been replaced with [`SetDeadline`](file:///pkg/net/#IPConn.SetDeadline), [`SetReadDeadline`](file:///pkg/net/#IPConn.SetReadDeadline), and [`SetWriteDeadline`](file:///pkg/net/#IPConn.SetWriteDeadline), respectively. Rather than taking a timeout value in nanoseconds that apply to any activity on the connection, the new methods set an absolute deadline (as a `time.Time` value) after which reads and writes will time out and no longer block.

There are also new functions [`net.DialTimeout`](file:///pkg/net/#DialTimeout) to simplify timing out dialing a network address and [`net.ListenMulticastUDP`](file:///pkg/net/#ListenMulticastUDP) to allow multicast UDP to listen concurrently across multiple listeners. The `net.ListenMulticastUDP` function replaces the old `JoinGroup` and `LeaveGroup` methods.

Updating: Code that uses the old methods will fail to compile and must be updated by hand. The semantic change makes it difficult for the fix tool to update automatically.

### The os package

The `Time` function has been removed; callers should use the [`Time`](file:///pkg/time/#Time) type from the `time` package.

The `Exec` function has been removed; callers should use `Exec` from the `syscall` package, where available.

The `ShellExpand` function has been renamed to [`ExpandEnv`](file:///pkg/os/#ExpandEnv).

The [`NewFile`](file:///pkg/os/#NewFile) function now takes a `uintptr` fd, instead of an `int`. The [`Fd`](file:///pkg/os/#File.Fd) method on files now also returns a `uintptr`.

There are no longer error constants such as `EINVAL` in the `os` package, since the set of values varied with the underlying operating system. There are new portable functions like [`IsPermission`](file:///pkg/os/#IsPermission) to test common error properties, plus a few new error values with more Go-like names, such as [`ErrPermission`](file:///pkg/os/#ErrPermission) and [`ErrNoEnv`](file:///pkg/os/#ErrNoEnv).

The `Getenverror` function has been removed. To distinguish between a non-existent environment variable and an empty string, use [`os.Environ`](file:///pkg/os/#Environ) or [`syscall.Getenv`](file:///pkg/syscall/#Getenv).

The [`Process.Wait`](file:///pkg/os/#Process.Wait) method has dropped its option argument and the associated constants are gone from the package. Also, the function `Wait` is gone; only the method of the `Process` type persists.

The `Waitmsg` type returned by [`Process.Wait`](file:///pkg/os/#Process.Wait) has been replaced with a more portable [`ProcessState`](file:///pkg/os/#ProcessState) type with accessor methods to recover information about the process. Because of changes to `Wait`, the `ProcessState` value always describes an exited process. Portability concerns simplified the interface in other ways, but the values returned by the [`ProcessState.Sys`](file:///pkg/os/#ProcessState.Sys) and [`ProcessState.SysUsage`](file:///pkg/os/#ProcessState.SysUsage) methods can be type-asserted to underlying system-specific data structures such as [`syscall.WaitStatus`](file:///pkg/syscall/#WaitStatus) and [`syscall.Rusage`](file:///pkg/syscall/#Rusage) on Unix.

Updating: Running `go fix` will drop a zero argument to `Process.Wait`. All other changes will be caught by the compiler and must be updated by hand.

#### The os.FileInfo type

Go 1 redefines the [`os.FileInfo`](file:///pkg/os/#FileInfo) type, changing it from a struct to an interface:

```go
type FileInfo interface {
    Name() string    // base name of the file
    Size() int64     // length in bytes
    Mode() FileMode  // file mode bits
    ModTime() time.Time // modification time
    IsDir() bool     // abbreviation for Mode().IsDir()
    Sys() interface{} // underlying data source (can return nil)
}
```

The file mode information has been moved into a subtype called [`os.FileMode`](file:///pkg/os/#FileMode), a simple integer type with `IsDir`, `Perm`, and `String` methods.

The system-specific details of file modes and properties such as (on Unix) i-number have been removed from `FileInfo` altogether. Instead, each operating system's `os` package provides an implementation of the `FileInfo` interface, which has a `Sys` method that returns the system-specific representation of file metadata. For instance, to discover the i-number of a file on a Unix system, unpack the `FileInfo` like this:

```go
fi, err := os.Stat("hello.go")
if err != nil {
    log.Fatal(err)
}
// Check that it's a Unix file.
unixStat, ok := fi.Sys().(*syscall.Stat_t)
if !ok {
    log.Fatal("hello.go: not a Unix file")
}
fmt.Printf("file i-number: %d\n", unixStat.Ino)
```

Assuming (which is unwise) that `"hello.go"` is a Unix file, the i-number expression could be contracted to:

```go
fi.Sys().(*syscall.Stat_t).Ino
```

The vast majority of uses of `FileInfo` need only the methods of the standard interface.

The `os` package no longer contains wrappers for the POSIX errors such as `ENOENT`. For the few programs that need to verify particular error conditions, there are now the boolean functions [`IsExist`](file:///pkg/os/#IsExist), [`IsNotExist`](file:///pkg/os/#IsNotExist) and [`IsPermission`](file:///pkg/os/#IsPermission).

```go
f, err := os.OpenFile(name, os.O_RDWR|os.O_CREATE|os.O_EXCL, 0600)
if os.IsExist(err) {
    log.Printf("%s already exists", name)
}
```

Updating: Running `go fix` will update code that uses the old equivalent of the current `os.FileInfo` and `os.FileMode` API. Code that needs system-specific file details will need to be updated by hand. Code that uses the old POSIX error values from the `os` package will fail to compile and will also need to be updated by hand.

### The os/signal package

The `os/signal` package in Go 1 replaces the `Incoming` function, which returned a channel that received all incoming signals, with the selective `Notify` function, which asks for delivery of specific signals on an existing channel.

Updating: Code must be updated by hand. A literal translation of

```go
c := signal.Incoming()
```

is

```go
c := make(chan os.Signal)
signal.Notify(c) // ask for all signals
```

but most code should list the specific signals it wants to handle instead:

```go
c := make(chan os.Signal)
signal.Notify(c, syscall.SIGHUP, syscall.SIGQUIT)
```

### The path/filepath package

In Go 1, the [`Walk`](file:///pkg/path/filepath/#Walk) function of the `path/filepath` package has been changed to take a function value of type [`WalkFunc`](file:///pkg/path/filepath/#WalkFunc) instead of a `Visitor` interface value. `WalkFunc` unifies the handling of both files and directories.

```go
type WalkFunc func(path string, info os.FileInfo, err error) error
```

The `WalkFunc` function will be called even for files or directories that could not be opened; in such cases the error argument will describe the failure. If a directory's contents are to be skipped, the function should return the value [`filepath.SkipDir`](file:///pkg/path/filepath/#variables)

```go
markFn := func(path string, info os.FileInfo, err error) error {
    if path == "pictures" {
        // Will skip walking of directory pictures and its contents.
        return filepath.SkipDir
    }
    if err != nil {
        return err
    }
    log.Println(path)
    return nil
}
err := filepath.Walk(".", markFn)
if err != nil {
    log.Fatal(err)
}
```

Updating: The change simplifies most code but has subtle consequences, so affected programs will need to be updated by hand. The compiler will catch code using the old interface.

### The regexp package

The [`regexp`](file:///pkg/regexp/) package has been rewritten. It has the same interface but the specification of the regular expressions it supports has changed from the old "egrep" form to that of [RE2](http://code.google.com/p/re2/).

Updating: Code that uses the package should have its regular expressions checked by hand.

### The runtime package

In Go 1, much of the API exported by package `runtime` has been removed in favor of functionality provided by other packages. Code using the `runtime.Type` interface or its specific concrete type implementations should now use package [`reflect`](file:///pkg/reflect/). Code using `runtime.Semacquire` or `runtime.Semrelease` should use channels or the abstractions in package [`sync`](file:///pkg/sync/). The `runtime.Alloc`, `runtime.Free`, and `runtime.Lookup` functions, an unsafe API created for debugging the memory allocator, have no replacement.

Before, `runtime.MemStats` was a global variable holding statistics about memory allocation, and calls to `runtime.UpdateMemStats` ensured that it was up to date. In Go 1, `runtime.MemStats` is a struct type, and code should use [`runtime.ReadMemStats`](file:///pkg/runtime/#ReadMemStats) to obtain the current statistics.

The package adds a new function, [`runtime.NumCPU`](file:///pkg/runtime/#NumCPU), that returns the number of CPUs available for parallel execution, as reported by the operating system kernel. Its value can inform the setting of `GOMAXPROCS`. The `runtime.Cgocalls` and `runtime.Goroutines` functions have been renamed to `runtime.NumCgoCall` and `runtime.NumGoroutine`.

Updating: Running `go fix` will update code for the function renamings. Other code will need to be updated by hand.

### The strconv package

In Go 1, the [`strconv`](file:///pkg/strconv/) package has been significantly reworked to make it more Go-like and less C-like, although `Atoi` lives on (it's similar to `int(ParseInt(x, 10, 0))`), as does `Itoa(x)` (`FormatInt(int64(x), 10)`). There are also new variants of some of the functions that append to byte slices rather than return strings, to allow control over allocation.

This table summarizes the renamings; see the [package documentation](file:///pkg/strconv/) for full details.

| Old call          | New call                          |
| ----------------- | --------------------------------- |
| Atob(x)           | ParseBool(x)                      |
| Atof32(x)         | ParseFloat(x, 32)§                |
| Atof64(x)         | ParseFloat(x, 64)                 |
| AtofN(x, n)       | ParseFloat(x, n)                  |
| Atoi(x)           | Atoi(x)                           |
| Atoi(x)           | ParseInt(x, 10, 0)§               |
| Atoi64(x)         | ParseInt(x, 10, 64)               |
| Atoui(x)          | ParseUint(x, 10, 0)§              |
| Atoui64(x)        | ParseUint(x, 10, 64)              |
| Btoi64(x, b)      | ParseInt(x, b, 64)                |
| Btoui64(x, b)     | ParseUint(x, b, 64)               |
| Btoa(x)           | FormatBool(x)                     |
| Ftoa32(x, f, p)   | FormatFloat(float64(x), f, p, 32) |
| Ftoa64(x, f, p)   | FormatFloat(x, f, p, 64)          |
| FtoaN(x, f, p, n) | FormatFloat(x, f, p, n)           |
| Itoa(x)           | Itoa(x)                           |
| Itoa(x)           | FormatInt(int64(x), 10)           |
| Itoa64(x)         | FormatInt(x, 10)                  |
| Itob(x, b)        | FormatInt(int64(x), b)            |
| Itob64(x, b)      | FormatInt(x, b)                   |
| Uitoa(x)          | FormatUint(uint64(x), 10)         |
| Uitoa64(x)        | FormatUint(x, 10)                 |
| Uitob(x, b)       | FormatUint(uint64(x), b)          |
| Uitob64(x, b)     | FormatUint(x, b)                  |

Updating: Running `go fix` will update almost all code affected by the change. § `Atoi` persists but `Atoui` and `Atof32` do not, so they may require a cast that must be added by hand; the `go fix` tool will warn about it.

### The template packages

The `template` and `exp/template/html` packages have moved to [`text/template`](file:///pkg/text/template/) and [`html/template`](file:///pkg/html/template/). More significant, the interface to these packages has been simplified. The template language is the same, but the concept of "template set" is gone and the functions and methods of the packages have changed accordingly, often by elimination.

Instead of sets, a `Template` object may contain multiple named template definitions, in effect constructing name spaces for template invocation. A template can invoke any other template associated with it, but only those templates associated with it. The simplest way to associate templates is to parse them together, something made easier with the new structure of the packages.

Updating: The imports will be updated by fix tool. Single-template uses will be otherwise be largely unaffected. Code that uses multiple templates in concert will need to be updated by hand. The [examples](file:///pkg/text/template/#examples) in the documentation for `text/template` can provide guidance.

### The testing package

The testing package has a type, `B`, passed as an argument to benchmark functions. In Go 1, `B` has new methods, analogous to those of `T`, enabling logging and failure reporting.

```go
func BenchmarkSprintf(b *testing.B) {
    // Verify correctness before running benchmark.
    b.StopTimer()
    got := fmt.Sprintf("%x", 23)
    const expect = "17"
    if expect != got {
        b.Fatalf("expected %q; got %q", expect, got)
    }
    b.StartTimer()
    for i := 0; i < b.N; i++ {
        fmt.Sprintf("%x", 23)
    }
}
```

Updating: Existing code is unaffected, although benchmarks that use `println` or `panic` should be updated to use the new methods.

### The testing/script package

The testing/script package has been deleted. It was a dreg.

Updating: No code is likely to be affected.

### The unsafe package

In Go 1, the functions `unsafe.Typeof`, `unsafe.Reflect`, `unsafe.Unreflect`, `unsafe.New`, and `unsafe.NewArray` have been removed; they duplicated safer functionality provided by package [`reflect`](file:///pkg/reflect/).

Updating: Code using these functions must be rewritten to use package [`reflect`](file:///pkg/reflect/). The changes to [encoding/gob](http://code.google.com/p/go/source/detail?r=2646dc956207) and the [protocol buffer library](http://code.google.com/p/goprotobuf/source/detail?r=5340ad310031) may be helpful as examples.

### The url package

In Go 1 several fields from the [`url.URL`](file:///pkg/net/url/#URL) type were removed or replaced.

The [`String`](file:///pkg/net/url/#URL.String) method now predictably rebuilds an encoded URL string using all of `URL`'s fields as necessary. The resulting string will also no longer have passwords escaped.

The `Raw` field has been removed. In most cases the `String` method may be used in its place.

The old `RawUserinfo` field is replaced by the `User` field, of type [`*net.Userinfo`](file:///pkg/net/url/#Userinfo). Values of this type may be created using the new [`net.User`](file:///pkg/net/url/#User) and [`net.UserPassword`](file:///pkg/net/url/#UserPassword) functions. The `EscapeUserinfo` and `UnescapeUserinfo` functions are also gone.

The `RawAuthority` field has been removed. The same information is available in the `Host` and `User` fields.

The `RawPath` field and the `EncodedPath` method have been removed. The path information in rooted URLs (with a slash following the schema) is now available only in decoded form in the `Path` field. Occasionally, the encoded data may be required to obtain information that was lost in the decoding process. These cases must be handled by accessing the data the URL was built from.

URLs with non-rooted paths, such as `"mailto:dev@golang.org?subject=Hi"`, are also handled differently. The `OpaquePath` boolean field has been removed and a new `Opaque` string field introduced to hold the encoded path for such URLs. In Go 1, the cited URL parses as:

```go
URL{
    Scheme:   "mailto",
    Opaque:   "dev@golang.org",
    RawQuery: "subject=Hi",
}
```

A new [`RequestURI`](file:///pkg/net/url/#URL.RequestURI) method was added to `URL`.

The `ParseWithReference` function has been renamed to `ParseWithFragment`.

Updating: Code that uses the old fields will fail to compile and must be updated by hand. The semantic changes make it difficult for the fix tool to update automatically.

## The go command

Go 1 introduces the [go command](file:///cmd/go/), a tool for fetching, building, and installing Go packages and commands. The `go` command does away with makefiles, instead using Go source code to find dependencies and determine build conditions. Most existing Go programs will no longer require makefiles to be built.

See [How to Write Go Code](file:///doc/code.html) for a primer on the `go` command and the [go command documentation](file:///cmd/go/) for the full details.

Updating: Projects that depend on the Go project's old makefile-based build infrastructure (`Make.pkg`, `Make.cmd`, and so on) should switch to using the `go` command for building Go code and, if necessary, rewrite their makefiles to perform any auxiliary build tasks.

## The cgo command

In Go 1, the [cgo command](file:///cmd/cgo) uses a different `_cgo_export.h` file, which is generated for packages containing `//export` lines. The `_cgo_export.h` file now begins with the C preamble comment, so that exported function definitions can use types defined there. This has the effect of compiling the preamble multiple times, so a package using `//export` must not put function definitions or variable initializations in the C preamble.

## Packaged releases

One of the most significant changes associated with Go 1 is the availability of prepackaged, downloadable distributions. They are available for many combinations of architecture and operating system (including Windows) and the list will grow. Installation details are described on the [Getting Started](file:///doc/install) page, while the distributions themselves are listed on the [downloads page](http://code.google.com/p/go/downloads/list).

Build version go1.0.1. A link [noted](http://code.google.com/policies.html#restrictions), and then, coming up on the very next line, we will find yet another link, link 3.0 if you will, after a few more words [link text](file:///LINK). [Terms of Service](file:///doc/tos.html) | [Privacy Policy](http://www.google.com/intl/en/privacy/privacy-policy.html)
