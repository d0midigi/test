# Attachments: LNK Files

LNK files, also known as Windows shortcuts, are commonly used in Windows operating systems to create quick links or references to original files, folders, or applications. These shortcuts provide a convenient way for users to access specific files or programs without having to navigate through multiple directories.

When a user creates a shortcut in Windows, an LNK file is generated that contains information about the target file's location, filename, and program association. Additionally, LNK files may also store information about the icon that represents the shortcut, any optional shortcut keys, and other attributes that define how the shortcut behaves.

The presence of an LNK file is indicated by a small curved arrow overlay in the bottom-left corner of the shortcut icon. This visual cue helps users distinguish between regular files and shortcuts on their desktop or in file directories.

Overall, LNK files play a crucial role in enhancing user productivity and efficiency by providing quick access to frequently used files or applications in the Windows environment. Understanding how LNK files work and how to use them effectively can help users streamline their workflow and access important resources faster.

<figure><img src="../../../../../.gitbook/assets/image (58).png" alt=""><figcaption></figcaption></figure>

Let's check the properties on the Icon:

<figure><img src="../../../../../.gitbook/assets/image (59).png" alt=""><figcaption></figcaption></figure>

If you change the path of the original file that a Windows shortcut (LNK file) is pointing to, the shortcut may no longer work as intended. When you create a shortcut, the LNK file contains the full path to the original file or program it is linked to. If you move or rename the original file, the shortcut will no longer be able to find it and may display an error message or fail to open the target file or program.

Changing the path of the original file may also result in the shortcut icon displaying differently or not displaying at all, as the shortcut cannot locate the file it is linked to. In some cases, the shortcut icon may revert to a default icon or display a blank or generic icon instead of the custom icon associated with the original file.

<figure><img src="../../../../../.gitbook/assets/image (60).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../../../../.gitbook/assets/image (61).png" alt=""><figcaption></figcaption></figure>

To resolve this issue and restore the functionality of the shortcut, you can update the path of the LNK file to point to the correct location of the original file or program. Right-click on the shortcut, select Properties, and then update the Target field with the new path to the file or program. This will ensure that the shortcut points to the correct location and functions properly.

It is important to keep track of any changes to the paths of files and programs that your shortcuts are linked to, as this can help prevent issues with broken shortcuts and ensure that your desktop or files remain organized and accessible.<br>

If you want to confuse or trick a user by changing the path of a Windows shortcut, you can modify the properties of the shortcut to point to a different location or program. By changing the target path of the shortcut, you can make it appear as though it is linked to a different file or program than the user expects.

To do this, follow these steps:

1. Right-click on the shortcut icon that you want to modify.
2. Select Properties from the context menu.
3. In the Properties window, go to the Shortcut tab.
4. In the Target field, edit the path to point to a different file or program. You can specify any valid path or program executable on your machine.
5. Click Apply and then OK to save the changes.

After making these modifications, when the user clicks on the shortcut, it will open the program or file specified in the new path you set, potentially leading to confusion or a surprise result for the user.

<figure><img src="../../../../../.gitbook/assets/image (62).png" alt=""><figcaption></figcaption></figure>

If you modify the properties of a Windows shortcut to point to a different file or program, such as a text file in this case, the shortcut will launch the specified file or program when you execute it.

To create a shortcut that points to a specific text file and executes it when clicked, follow these steps:

1. Right-click on an empty area of your desktop or in the desired folder.
2. Select New > Shortcut from the context menu.
3. In the Create Shortcut wizard, click Browse to select the text file you want to execute.
4. Once you have selected the text file, click Next.
5. Enter a name for the shortcut or leave the default name, then click Finish.
6. Right-click on the newly created shortcut and select Properties.
7. In the Properties window, go to the Shortcut tab.
8. In the Target field, make sure the path to the text file is specified correctly.
9. If needed, you can also adjust other properties such as the Start in directory or Shortcut key.
10. Click Apply and then OK to save the changes.

When you double-click on the modified shortcut, it should open and execute the specified text file using the default text editor associated with .txt files on your system. This allows you to create a shortcut that directly opens a specific text file when clicked, providing quick access to the content of the file.

Always ensure that the file you are pointing the shortcut to is safe and does not contain harmful content, especially if you plan to share the shortcut with others.

<figure><img src="../../../../../.gitbook/assets/image.gif" alt=""><figcaption></figcaption></figure>

Creating a shortcut that points to a text file and using it as a means to execute code or a payload can be a method of social engineering or tricking a user into running malicious commands. By disguising the shortcut as a harmless text file, the user may be more likely to interact with it, unknowingly triggering the execution of malicious code.

To execute code or a payload using a text file shortcut, you can modify the Target field of the shortcut properties to point to a script or command that will run when the shortcut is opened. This can include PowerShell scripts, batch files, or other executable commands.
