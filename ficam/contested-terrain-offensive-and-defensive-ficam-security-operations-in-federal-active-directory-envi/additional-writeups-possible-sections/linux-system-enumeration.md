# Linux System Enumeration

When performing System Enumeration during a security assessment or Linux administration task, your goal is to map out the environment. Here is a more structured and professional rewrite of your list, categorized by the type of information each command retrieves.

### 1. System Identification

These commands help you identify the hardware, OS version, and kernel details.

* `hostname`: Displays the name assigned to the target machine.
* `uname -a`: Prints detailed system information, including the kernel version and system architecture.
* `cat /proc/version`: Provides specific details about the kernel version and the compiler used to build it.
* `cat /etc/issue`: Shows the OS distribution and version; keep in mind this file is easily edited by administrators and may not always be accurate.
* `lscpu`: Lists comprehensive information about the CPU architecture (cores, threads, virtualization, etc.).

### 2. Process Monitoring

Understanding what is currently running is vital for identifying services, potential vulnerabilities, or misconfigurations.

* `ps`: Displays processes associated with the current user’s terminal session.
* `ps -A`: Provides a snapshot of every running process on the system.
* `ps axjf`: Visualizes the process tree, showing parent-child relationships between processes.
* `ps aux`: A comprehensive view of all processes:
  * `a`: All users.
  * `u`: Displays the user/owner of the process.
  * `x`: Includes processes not attached to a terminal.
* `ps aux | grep root`: Filters the process list to show only those running with root privileges.

### 3. Environment & Configuration

These commands reveal how the system is configured and what scheduled tasks are running.

* `env`: Lists all environment variables, which can reveal path configurations, user settings, or even sensitive API keys.
* `ls -la /etc/cron.daily/`: Lists all scripts scheduled to run daily. These are often targets for privilege escalation if permissions are weak.
* `cat /etc/crontab`: Displays the system-wide Crontab file, showing scheduled tasks and the users they run as.

#### Summary Table: Quick Reference

| **Category** | **Command**        | **Key Utility**               |
| ------------ | ------------------ | ----------------------------- |
| Identity     | `uname -a`         | Kernel & Arch info            |
| Hardware     | `lscpu`            | CPU specs                     |
| Processes    | `ps aux`           | Full process snapshot         |
| Automation   | `cat /etc/crontab` | Scheduled tasks (Persistence) |
| Variables    | `env`              | Session configuration         |
