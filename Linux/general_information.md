# Learning Dependecies

## 19th November 2024
Today, I learned about **Linux**, **Windows OS**, and **Virtual Private Server**. How to install them and make basic configurations. 


### Key Takeaways
- **Linux history**: At first was a personal project started in 1991 by a finnish student Linus Torvalds.
- **Linux distributions**: Available in over 600 distributions.
- **Linux Customization**: We can customize our promt by using special characters. 
- **System Information**: Learnt how to get system information using *uname* command.
- **Secure Shell**: used SSH with provided username and IP adress by HTB in Pwnbox.     

### Reflections
## General Information
Linux is generally considered more secure than other operating systems, and while it has many kernel vulnerabilities in the past, it is becoming less and less frequet. It is less susceptible to malware than Windows operating systems and is very frequently updated. Linux is also very stable and generally affords very high performance to end-user. 
**Linux follows five core principles**:
![FIVE Linux Principles and their Description](resources/five_principles.png)
**Linux Components**
![Seven Linux components and their description](resources/components.png)
**Linux Architecture**
The Linux operating system can be broken down into four layers:
![Hardware, Kernel, Shell, System Utility and their description](resources/Linux_architecture.png)
**File System Hierarchy**
The Linux operating system is structured in a tree-like hierarchy and is documented in the Filesystem Hierarchy Standard (FHS). Linux is structured with the following standard top-level directories:
![Linux file system](resources/file_system_hierarchy.png)
![All file systems and their definition](resources/file_system.png)

## Linux Distributions
The most popular and well-known distributions or an operating system based on the Linux kernel being Ubuntu, Debian, CENTOS, Fedora, OpenSUSE, elementary, Manjaro, Gentoo Linux, RedHat, Linux Mint.
For cyber security specialists, some of the most popular Linux distros are but are not limited to:
- ParrosOS on Ubuntu or Debian;
- Raspberry Pi OS on CentOS or BackBox;
- BlackArch on Pentoo;

## Linux Customization 
The promt can be customized using special characters and variables in the shell's configuration file (<span style="color: lightgreen;">.bashrc</span> for the Bash shell). Here are special characters:
![Special Characters for custom promts, like date, name of shell, current time, full path or hostname](resources/custom_promt.png)

## Getting Help
The first two ways where we can get help in Linux are *the man pages* and *the help functions*
Syntax of the man command:
![an example how to get help through man command](resources/man_command.png)
An example of help function:
![An example of getting help through the help function](resources/help_command.png)
`-h` is the short version of `--help` command
Another helpful tool that can be userful is <span style="color: lightgreen;">apropos</span>
![an example of apropos command](resources/apropos_command.png)

## Getting system Information
Running `uname` command will print information about the machine, like kernel name, hostname, the kernel release, kernel version, operating system. There are additional attributes that will print only specific information:
![Options to print certain system information](resources/uname_options.png)

## Secure Shell (SSH)
Secure protocol that allows clients to access and execute commands or actions on remote computers. 
Here is an example command how to connect to the targets:
![ssh command to connect to the target remotely](resources/ssh_login.png)
