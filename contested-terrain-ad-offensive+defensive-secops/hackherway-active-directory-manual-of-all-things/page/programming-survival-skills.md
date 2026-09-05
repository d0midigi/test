# Programming Survival Skills

Programming Survival Skills

Why study programming? Hackers should study programming and learn as much about the subject as possible to find vulnerabilities in programs and get them fixed before unethical hackers take advantage of them. It is very much a foot race: if vulnerability exists, who will find it first? The purpose of this chapter is to give you the survival skills necessary to understand upcoming chapters and later find the holes in software before the black hats do.

In this chapter, we cover the following topics:

* C programming language
* Computer memory
* Intel processors
* Assembly language basics
* Debugging with gdb
* Python survival skills

C Programming Language

The C programming language was developed in 1972 by Dennis Ritchie from AT\&T Bell Labs. The language was heavily used in Unix and is thereby ubiquitous. In fact, much of the staple networking programs and operating systems are based in C.

Basic C Language Constructs

Although each C program is unique, there are common structures that can be found in most programs. We’ll discuss these in subsequent sections.

main()

All C programs contain a **main()** structure (lowercase) that follows this format:

![A screen shot of a computer

Description automatically generated](<../.gitbook/assets/0 (64).png>)

The return value type and arguments are optional. If you use command-line arguments for **main(),** use the format:

![A black and white text

Description automatically generated with medium confidence](<../.gitbook/assets/1 (48).png>)

* The **argc** integer holds the number of arguments
* The **argv** array holds the input arguments (strings)
* The parentheses and brackets are mandatory
* White space between these elements does not matter
* The brackets are used to denote the beginning and end of a block of code

Although procedure and function calls are optional, the program would do nothing without them. _**Procedure statements**_ are simply a series of commands that perform operations on data or variables and normally end with a semicolon (;).

Functions

Functions are self-contained bundles of algorithms that can be called for execution by **main()** or other functions. Technically, the **main()** structure of each C program is also a function; however, most programs contain other functions. The format is as follows:

![A black background with text

Description automatically generated with medium confidence](<../.gitbook/assets/2 (41).png>)

The first line of a function is called the _**signature.**_ By looking at it, you can tell if the function returns a value after executing or requires arguments that will be used in processing the procedures of the function.

The call to the function looks like this:

![A black and white screen with white text

Description automatically generated](<../.gitbook/assets/3 (30).png>)

Again, notice the required semicolon at the end of the function call. In general, the semicolon is used on all stand-alone command lines (not bounded by brackets or parentheses).

Functions are used to modify the flow of a program. When a call to a function is made, the execution of the program temporarily jumps to the function. After execution of the called function has completed, the program continues executing on the line following the call.

Variables

_**Variables**_ are used in programs to store pieces of information that may change and may be used to dynamically influence the program. The table below shows some common types of variables:

| **Variable Type** | **Use**                                             | **Typical Size**                                                   |
| ----------------- | --------------------------------------------------- | ------------------------------------------------------------------ |
| int               | Stores signed integer values such as 314 or -314    | <p>4 bytes for 32bit machines</p><p>2 bytes for 16bit machines</p> |
| float             | Stores signed floating-point numbers such as -3.234 | 4 bytes                                                            |
| double            | Stores large floating-point numbers                 | 8 bytes                                                            |
| char              | Stores a single character such as “d”               | 1 byte                                                             |

When the program is compiled, most variables are preallocated memory of a fixed size according to system-specific definitions of size. The sizes in the above table are considered typical; there is no guarantee that you will get those exact sizes. It is left up to the hardware implmentaiton to define this size; however, the function **sizeof()** is used in C to ensure that the correct sizes are allocated by the compiler.

Variables are typically defined near the top of a block of code. As the compiler chews up the code and builds a symbol table, it must be aware of a variable before it is used in the code later. This formal declaration of variables is done in the following manner:

![](<../.gitbook/assets/4 (33).png>)

For example,

![A black rectangular object with a white letter

Description automatically generated](<../.gitbook/assets/5 (30).png>)

The integer is normally 4 bytes and is declared in memory with a name of a and an initial value of **0.**

Once declared, the assignment construct is used to change the value of a variable. For example, the statement:

![](<../.gitbook/assets/6 (32).png>)

X=x+1; is an assignment statement containing a variable **x** modified by the **+** operator. The new value is stored into the **x.** It is common to use the format:

![](<../.gitbook/assets/7 (29).png>)

The **destination** is the location in which the final outcome is stored.

printf

The C language comes with many useful constructs for free (bundled in the libc library). One of the most commonly constructs is the printf command, generally used to print output to the screen. There are two forms of the printf command:

![](<../.gitbook/assets/8 (24).png>)

The first format is straightforward and is used to display a simple tring to the screen. The second format allows for more flexibility through the use of a format string that can be composed of normal characters and special symbols that act as placeholders for the list of variables following the comma. Commonly used format symbols are listed and described in the below table.

| **Format Symbol** | **Meaning**              | **Example**               |
| ----------------- | ------------------------ | ------------------------- |
|                   | Carriage return/new line | printf(“test\n”);         |
| %d                | Decimal value            | printf(“test %d”, 123);   |
| %s                | String value             | printf(“test %s”, 123”);  |
| %x                | Hex value                | printf(“test %x”, 0x123); |

These format symbols may be combined in any order to produce the desired output. Except for the  symbol, the number of variables/values needs to match the number of symbols in the format string; otherwise, problems will arise, as described in our discussion of format string exploits.

Scanf

The **scanf** command complements the **printf** command is generally used to get input from the user. The format is as follows:

![](<../.gitbook/assets/9 (23).png>)

The format string contains format symbols such as those shown for **printf** in the above table. For example, the following code will read an integer from the user and store it into the variable called **number:**

![](<../.gitbook/assets/10 (21).png>)

The **&** symbol means we are storing the value into the memory location pointed to by **number**; that will make more sense when we talk about “Pointers” later in this section. For now, realize that you must use the **&** symbol before any variable name with **scanf.** The command is smart enough to change types on-the-fly, so if you were to enter a character in the previous command prompt, the command would convert the character into the decimal (ASCII) value automatically. Bounds checking is not done in regard to string size, however, which may lead to problems.

Strcpy/strncpy

The **strcpy** command is probably the most dangerous command used in C. The format of the command is:

![A black box with white text

Description automatically generated](<../.gitbook/assets/11 (18).png>)

The purpose of the command is to copy each character in the source string (a series of characters ending with a null character **\0**) into the destination string. This is particularly dangerous because there is no checking of the source’s size before it is copied over to the destination. In reality, we are talking about overwriting memory locations here. Suffice to say it, when the source is larger than the space allocated for the destination, bad things happen (buffer overflows). A much safer command is the **strncpy** command. The format of that command is:

![](<../.gitbook/assets/12 (23).png>)

The _**width**_ field is used to ensure that only a certain number of characters are copied from the source string to the destination string, allowing for greater control by the programmer.

for and while Loops

FYI – FOR YOUR INFORMATION

| <img src="../.gitbook/assets/13 (19).png" alt="Exclamation mark with solid fill" data-size="original"> | **CAUTION** Using unbounded functions like **strncpy** is unsafe; however, most programming courses do not cover the dangers posed by these functions. In fact, if programmers would simply use the safer alternatives – for example, **strncpy** – then the entire class of buffer overflow attacks would be less prevalent. Obviously, programmers continue to use these dangerous functions since buffer overflows are the most common attack vector. That said, even bounded functions can suffer from incorrect width calculations. |
| ------------------------------------------------------------------------------------------------------ | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |

Loops are used in programming languages to iterate through a series of commands multiple times. The two common types are **for** and **while** loops.

**for** loops start counting at a beginning value, test the value for some condition, execute the statement, and increment the value for the next iteration. The format is as follows:

![A screen shot of a computer program

Description automatically generated](<../.gitbook/assets/14 (18).png>)

Therefore, a **for** loop like:

![A black rectangular object with a white letter

Description automatically generated](<../.gitbook/assets/15 (19).png>)

will print the numbers 0 to 9 on the same line (since  is not used), like this: 0123456789.

With **for** loops, the condition is checked prior to the iteration of the statements in the loop, so it is possible that even the first iteration will not be executed. When the condition is not met, the flow of the program continues after the loop.

FYI – FOR YOUR INFORMATION

It is important to note the use of the less-than operator (<) in place of the less-than-or-equal-to operator (<=), which allows the loop to proceed one more time until i=10. This is an important concept that can lead to off-by-one errors. Also, note the count started with 0. This is common in C and worth getting used to.

The while loop is used to iterate though a series of statements until a condition is met. The format is as follows:

![](<../.gitbook/assets/16 (20).png>)

Loops may also be nested within each other.

If/else

The if/else construct is used to execute a series of statements if a certain condition is met; otherwise, the optional else block of statements is executed. If there is not else block of statements, the flow of the program will continue after the end of the closing if block bracket (}). The format is as follows:

![A screen shot of a computer

Description automatically generated](<../.gitbook/assets/17 (18).png>)

The braces may be omitted for single statements.

Comments

To assist in the readability and sharing of source code, programmers include comments in the code. There are two ways to place commends in code: **//**, or **/\*** and **\*/**. The **//** indicates that any characters on the rest of that line are to be treated as comments and not acted on by the computer when the program executes. The **/\*** and **\*/** pair starts and stops a block of comments that may span multiple lines. The **/\*** is used to start the comment, and the \*/ is used to indicate the end of the comment block.

Sample Program

You are now ready to review your first program. We will start by showing the program with // commands included, and will follow up with a discussion of the program:

![A screen shot of a computer program

Description automatically generated](<../.gitbook/assets/18 (18).png>)

This very simple program prints “Hello haxor” to the screen using the **printf** function, included in the stdio.h library.

Now for one that’s a little more complex:
