# Quick and Dirty Linus OS

Quick & Dirty: Linux Operating System

Because hacking takes place within a terminal, shell, or command-line interface, you should have at least a familiarity with a few of its basics, particularly when it pertains to security issues.

| MAC Times                                                                        |                                   |
| -------------------------------------------------------------------------------- | --------------------------------- |
| Modify                                                                           | Modify the contents of the file   |
| Access                                                                           | When the files were last accessed |
| Change                                                                           | Metadata change                   |
| <p>Use the<br>touch -mac<br>filename command to update all at the same time.</p> |                                   |

| Linux Filesystem |                                                          |
| ---------------- | -------------------------------------------------------- |
| /                | Root of the file system                                  |
| /var             | Variable data and log files are located here             |
| /bin             | <p>Binaries</p><p>Commands for users</p>                 |
| /sbin            | <p>System binaries</p><p>Commands for administration</p> |
| /root            | Home directory for the root user                         |
| /home            | Directory for all home folders for non-privileged users  |
| /boot            | Stores the Linux kernel image and other boot files       |
| /proc            | Direct access to the Linux kernel                        |
| /dev             | Direct access to hardware storage devices                |
| /mnt             | Place to mount devices onto user mode filesystems        |

| User and Group Permissions Example                       |      |
| -------------------------------------------------------- | ---- |
| <p>User can RWX</p><p>Group can R</p><p>Others can R</p> | 764  |
| <p>User can RW</p><p>Group can R</p><p>Others can R</p>  | 644  |
| <p>SUID bit set</p><p>User and Group can RWX</p>         | 4770 |
| <p>SUID and GUID bit set</p><p>All Users can RWX</p>     | 6777 |

| Identifying Users and Processes |                       |
| ------------------------------- | --------------------- |
| 1                               | INIT process ID       |
| 0                               | Root UID, GID         |
| 1-9999                          | Accounts for services |
| Above 1000                      | All other users       |

| Permissions |          |           |            |
| ----------- | -------- | --------- | ---------- |
| Perm. IDs   | **User** | **Group** | **Others** |
| R           | 400      | 040       | 004        |
| W           | 200      | 020       | 002        |
| X           | 100      | 010       | 001        |
| SUID        | 4000     |           |            |
| SGID        |          | 2000      |            |
