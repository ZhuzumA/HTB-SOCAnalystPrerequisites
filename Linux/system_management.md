# Learning Dependecies

## 27th November 2024
I learned about **Linux Navigation**, ****, and **Virtual Private Server**. How to install them and make basic configurations. 


### Key Takeaways
- **User Management**: 
- **Package Management**: 
- **Service and Process Management**:
- **Task Scheduling**:
- **File Descriptions and Redirections**:
- **Filter Contents**:
- **Regular Expressions**:
- **Permission Managment**:

### Reflections
## User Management
Here is a list that will help to better understand and deal with user management:
![Command on user management and their defenition](/Linux/resources/user_management.png)

## Package management
Packages are archives that contain binaries of software, configuration files, information about dependencies and keep track of updates and upgrades. The features that most package management systems provide are:

- Package downloading
- Dependency resolution
- A standard binary package format
- Common installation and configuration locations
- Additional system-related configuration and functionality
- Quality control

The package management software retrieves the necessary changes for system installation from the package itself and then implements these changes to install the package successfully. If the package management software recognizes that additional packages are required for the proper functioning of the package that has not yet been installed, a dependency is included and either warns the administrator or tries to reload the missing software from a repository, for example, and install it in advance.

If an installed software has been deleted, the package management system then retakes the package's information, modifies it based on its configuration, and deletes files. There are different package management programs that we can use for this. Here is a list of examples of such programs:
![Here is a list of different package management programs](/Linux/resources/package_management.png)

## Service and Process Management
In general, there are two types of services: internal, the relevant services that are required at system startup, which for example, perform hardware-related tasks, and services that are installed by the user, which usually include all server services. Such services run in the background without any user interaction. These are also called `daemons` and are identified by the letter `'d'` at the end of the program name, for example, `sshd` or `systemd`.

There are three possibilities to run several commands, one after the other. These are separated by:

- Semicolon `;`
- Double ampersand characters `&&`
- Pipes `|`
The difference between them lies in the previous processes' treatment and depends on whether the previous process was completed successfully or with errors. The semicolon `;` is a command separator and executes the commands by ignoring previous commands' results and errors.
However, it looks different if we use the double AND characters `&&` to run the commands one after the other. If there is an error in one of the commands, the following ones will not be executed anymore, and the whole process will be stopped.
Pipes `|` depend not only on the correct and error-free operation of the previous processes but also on the previous processes' results.

*The problem*: Use the "systemctl" command to list all units of services and submit the unit name with the description "Load AppArmor profiles managed internally by snapd" as the answer. 
*Solution*: 
`systemctl list-units --type=service | grep "Load AppArmor profiles managed internally by snapd"`


## Task Scheduling
Task scheduling is a feature in Linux systems that allows users to schedule and automate tasks. It allows administrators and users to run tasks at a specific time or within specific frequencies without having to start them manually. It can be used in Linux systems such as Ubuntu, Redhat Linux, and Solaris to manage a variety of tasks. Examples include automatically updating software, running scripts, cleaning databases, and automating backups. This also allows users to schedule regular and repetitive tasks to ensure they are run regularly. In addition, alerts can be set up to display when certain events occur or to contact administrators or users. 
`Systemd` is a service used in Linux systems such as Ubuntu, Redhat Linux, and Solaris to start processes and scripts at a specific time. With it, we can set up processes and scripts to run at a specific time or time interval and can also specify specific events and triggers that will trigger a specific task. To do this, we need to take some steps and precautions before our scripts or processes are automatically executed by the system.
1. Create a timer
2. Create a service
3. Activate the timer

`Cron` is another tool that can be used in Linux systems to schedule and automate processes. It allows users and administrators to execute tasks at a specific time or within specific intervals. For the above examples, we can also use Cron to automate the same tasks. We just need to create a script and then tell the cron daemon to call it at a specific time.

With Cron, we can automate the same tasks, but the process for setting up the Cron daemon is a little different than Systemd. To set up the cron daemon, we need to store the tasks in a file called `crontab` and then tell the daemon when to run the tasks. Then we can schedule and automate the tasks by configuring the cron daemon accordingly. The structure of Cron consists of the following components:
![The structure of crone their definition and an example](/Linux/resources/task_cron.png)

The "System Update" should be executed once every sixth hour. This is indicated by the entry `0 */6` in the hour column. The task is executed by the script `update_software.sh`, whose path is given in the last column.

The task `execute scripts` is to be executed every first day of the month at midnight. This is indicated by the entries `0` and `0` in the minute and hour columns and `1` in the days-of-the-month column. The task is executed by the `run_scripts.sh` script, whose path is given in the last column.

The third task, `Cleanup DB`, is to be executed every Sunday at midnight. This is specified by the entries `0` and `0` in the minute and hour columns and `0` in the days-of-the-week column. The task is executed by the `clean_database.sh` script, whose path is given in the last column.

The fourth task, backups, is to be executed every Sunday at midnight. This is indicated by the entries `0` and `0` in the minute and hour columns and `7` in the days-of-the-week column. The task is executed by the `backup.sh script`, whose path is given in the last column.

*The problem*: What is the Type of the service of the "dconf.service"?
*Solution*: 
1. `sudo find / -name 'dconf.service' | grep 'dconf'`
2. `cat /usr/lib/systemd/user/dconf.service`

## Network Services
Secure Shell (SSH) is a network protocol that allows the secure transmission of data and commands over a network. It is widely used to securely manage remote systems and securely access remote systems to execute commands or transfer files. In order to connect to our or a remote Linux host via SSH, a corresponding SSH server must be available and running.

The most commonly used SSH server is the OpenSSH server. OpenSSH is a free and open-source implementation of the Secure Shell (SSH) protocol that allows the secure transmission of data and commands over a network.

Administrators use OpenSSH to securely manage remote systems by establishing an encrypted connection to a remote host. With OpenSSH, administrators can execute commands on remote systems, securely transfer files, and establish a secure remote connection without the transmission of data and commands being intercepted by third parties.

To install OpenSSH:
```sudo apt install openssh-server -y```

To check if the server  is running, I use the following command:
```systemctl status ssh```

SSH - Logging In:
```ssh username@IP_adress```

OpenSSH can be configured and customized by editing the file `/etc/ssh/sshd_config` with a text editor. Here we can adjust settings such as the maximum number of concurrent connections, the use of passwords or keys for logins, host key checking, and more. However, it is important for us to note that changes to the OpenSSH configuration file must be done carefully.

*Network File System (NFS)* is a network protocol that allows us to store and manage files on remote systems as if they were stored on the local system. It enables easy and efficient management of files across networks. For example, administrators use NFS to store and manage files centrally (for Linux and Windows systems) to enable easy collaboration and management of data. For Linux, there are several NFS servers, including NFS-UTILS (*Ubuntu*), NFS-Ganesha (*Solaris*), and OpenNFS (*Redhat Linux*).

Install NFS:
```sudo apt install nfs-kernel-server -y```

To check if the server is running:
```systemctl statu nfs-kernel-server```

We can configure NFS via the configuration file `/etc/exports`. This file specifies which directories should be shared and the access rights for users and systems. It is also possible to configure settings such as the transfer speed and the use of encryption. NFS access rights determine which users and systems can access the shared directories and what actions they can perform. Here are some important access rights that can be configured in NFS:

|Permissions|Description|
|-----------|-----------|
|`rw`|Gives users and systems read and write permissions to the shared directory.|
|`ro`|Gives users and systems read-only access to the shared directory.|
|`no_root_squash`|Prevents the root user on the client from being restricted to the rights of a normal user.|
|`root_squash`|Restricts the rights of the root user on the client to the rights of a normal user.|
|`sync`|Synchronizes the transfer of data to ensure that changes are only transferred after they have been saved on the file system.|
|`async`|Transfers data asynchronously, which makes the transfer faster, but may cause inconsistencies in the file system if changes have not been fully committed.|

A *web server* is a type of software that provides data and documents or other applications and functions over the Internet. They use the Hypertext Transfer Protocol (HTTP) to send data to clients such as web browsers and receive requests from those clients. These are then rendered in the form of Hypertext Markup Language (HTML) in the client's browser. This type of communication allows the client to create dynamic web pages that respond to the client's requests.
Apache web server has a variety of features that allow us to host a secure and efficient web application. Moreover, we can also configure logging to get information about the traffic on our server, which helps us analyze attacks. We can install Apache using the following command:
`sudo apt install apache2 -y`
For Apache2, to specify which folders can be accessed, we can edit the file `/etc/apache2/apache2.conf` with a text editor. This file contains the global settings. We can change the settings to specify which directories can be accessed and what actions can be performed on those directories.

Virtual Private Network (VPN) is a technology that allows us to connect securely to another network as if we were directly in it. This is done by creating an encrypted tunnel connection between the client and the server, which means that all data transmitted over this connection is encrypted. Some of the most popular VPN servers for Linux servers are OpenVPN, L2TP/IPsec, PPTP, SSTP, and SoftEther. OpenVPN is a popular open-source VPN server available for various operating systems, including Ubuntu, Solaris, and Redhat Linux. 
OpenVPN provides us with a variety of features, including encryption, tunneling, traffic shaping, network routing, and the ability to adapt to dynamically changing networks. We can install the server and client with the following command:
`sudo apt install openvpn -y`

OpenVPN can be customized and configured by editing the configuration file `/etc/openvpn/server.conf`. This file contains the settings for the OpenVPN server. We can change the settings to configure certain features such as encryption, tunneling, traffic shaping, etc.

If we want to connect to an OpenVPN server, we can use the `.ovpn` file we received from the server and save it on our system. We can do this with the following command on the command line:
`sudo openvpn --config internal.ovpn`

`cURL` is a tool that allows us to transfer files from the shell over protocols like `HTTP`, `HTTPS`, `FTP`, `SFTP`, `FTPS`, or `SCP`. This tool gives us the possibility to control and test websites remotely. Besides the remote servers' content, we can also view individual requests to look at the client's and server's communication. Usually, `cURL` is already installed on most Linux systems. This is another critical reason to familiarize ourselves with this tool, as it can make some processes much easier later on.

An alternative to curl is the tool wget. With this tool, we can download files from FTP or HTTP servers directly from the terminal, and it serves as a good download manager. If we use wget in the same way, the difference to curl is that the website content is downloaded and stored locally, as shown in the following example:
![wget command and its output](/Linux/resources/wget.png)