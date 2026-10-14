# Windows Version and Configuration

### <mark style="color:yellow;">1.1</mark> System Information Commands

#### <mark style="color:yellow;">1.1</mark> Basic System Information

<mark style="color:yellow;">**Command:**</mark>

```css
systeminfo | findstr /B /C:"OS Name" /C:"OS Version"
```

This command retrieves essential information about the operating system by using the `systeminfo` utility, which outputs a summary of system configurations. The `findstr` command is then utilized to filter this output to only display lines that contain either "OS Name" or "OS Version." This allows you to quickly ascertain the specific version and name of the operating system currently running on the machine without having to sift through a plethora of information.

<mark style="color:yellow;">**Output:**</mark>

The result of this command will display the operating system's name along with its version number, enabling quick identification of the operating system you seek information about.

#### <mark style="color:yellow;">1.2</mark> Patch and Update Information

<mark style="color:yellow;">**Command:**</mark>

```
wmic qfe list
```

This command fetches details about all the installed Quick Fix Engineering (QFE) updates on the system. QFE updates are crucial for maintaining the operating system's security and functionality. Using `wmic`, the command provides a clear listing of installed updates, which is essential for you especially if you need to keep track of what updates have been applied to what systems.

<mark style="color:yellow;">**Output:**</mark>

The command returns a list of installed updates that provide key details such as update IDs, descriptions of the updates that have been applied, and their respective installation timestamps. This information is useful if you find yourself having to troubleshoot and ensure that system is up to date with everything.

#### <mark style="color:yellow;">1.3</mark> Architecture Information

<mark style="color:yellow;">**Command:**</mark>

```handlebars
wmic os get osarchitecture
```

This command retrieves the architecture of the currently running operating system, which indicates whether it is a 32-bit or 64-bit version. Knowing the architecture is vital for software installation and for ensuring compatibility with applications.

### <mark style="color:yellow;">2.</mark> Environment Variables

#### <mark style="color:yellow;">2.1</mark> List Environment Variables

**Commands:**

```
set
```

Or, using PowerShell:

```
Get-ChildItem Env:
```

Both commands are designed to list all environment variables defined within the operating system. What exactly are environment variables, you might be wondering.

<mark style="color:yellow;">**2.1.1**</mark>**&#x20;Environment Variables vs. Object-Oriented Output Explanation**

Environment variables are dynamic values that can affect the behavior of processes that run on the system. In other words, they are named values that hold system or application information (like `PATH`, `HOME`, `ENV`) that programs read to adjust their behaviors, settings, or access resources without changing the code. They act as a flexible configuration layer, so to speak. These layers allow applications to run on different systems (dev, prod) with different settings (languages, debug modes, file paths) just by changing these external values, making software more portable and way easier to manage.

The `set` command provides a view of these variables in a command prompt, while the PowerShell command does the same but with a focus on object-oriented output.

Now, you're probably wondering why have two commands that essentially do the same thing? Why not just have one that does it all?

The core difference is that environment variables are system-wide key-value pairs that are used for configurations, while object-oriented output involves accessing properties of data structures that are defined within a program's scope. The `set` command is relevant to environment variables (in some contexts), but not directly to object-oriented output.

<details>

<summary><mark style="color:yellow;">ELI5: Environment Variables &#x26; Object-Oriented Output</mark></summary>

Imagine your computer is a big toy box.

**Environment variables** are like permanent stickers you stick on the _outside_ of the toy box. Everyone in the whole room (your computer system) can read these stickers to now general rules, like "The rule is: always clean up your LEGOs first." Sometimes you use a special command, like `set`, to put these stickers on (in certain systems).

**Object-oriented output** is like the specific instructions printed _inside_ a tiny instructional manual that comes with one specific toy (an "object"). Only the person playing with _that specific toy_ at that moment can read those instructions. These rules are part of the toy itself, not the whole room.

So:

* **Environment Variables:** System-wide, like a general house rule sticker on the outside of a toy box.
* **Object-Oriented Output:** Program-specific, like an instruction manual that only comes with a toy inside the box.

The `set` command helps with the stickers (sometimes), but has nothing to do with reading the little instructions manuals inside the toys.

</details>

<mark style="color:yellow;">**Output:**</mark>

The output consists of variable names paired with their respective values. This information can provide you more insight into the configurations and settings that govern the behaviors of the system and applications running on it.

### 3. Drive Information

#### 3.1 Listing Logical Drives

**Command:**

```
wmic logicaldisk get caption
```

This command lists all logical drives recognized by the operating system, providing a convenient way to see all available storage locations on the system.
