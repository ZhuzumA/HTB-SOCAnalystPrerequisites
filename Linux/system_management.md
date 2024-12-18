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

## Backup and Restore
When backing up data on an Ubuntu system, I can utilize tools such as:
- Rsync
- Deja Dup
- Duplicity
Rsync is an open-source tool that allows us to quickly and securely back up files and folders to a remote location. It is particularly useful for transferring large amounts of data over the network, as it only transmits the changed parts of a file. It can also be used to create backups locally or on remote servers. If we need to back up large amounts of data over the network, Rsync might be the better option.

Duplicity is another graphical backup tool for Ubuntu that provides users with comprehensive data protection and secure backups. It also uses Rsync as a backend and additionally offers the possibility to encrypt backup copies and store them on remote storage media, such as FTP servers, or cloud storage services, such as Amazon S3.

Deja Dup is a graphical backup tool for Ubuntu that simplifies the backup process, allowing us to quickly and easily back up our data. It provides a user-friendly interface to create backup copies of data on local or remote storage media. It uses Rsync as a backend and also supports data encryption.

In order to ensure the security and integrity of backups, we should take steps to encrypt their backups. Encrypting backups ensures that sensitive data is protected from unauthorized access. Alternatively, we can encrypt backups on Ubuntu systems by utilizing tools such as GnuPG, eCryptfs, and LUKS.

In order to install Rsync on Ubuntu, we can use the apt package manager:
`sudo apt install rsync -y`

To backup an entire directory using rsync, we can use the following command:
`rsync -av /path/to/mydirectory user@backup_server:/path/to/backup/directory`

This command will copy the entire directory `/path/to/mydirectory` to a remote host `backup_server`, to the directory `/path/to/backup/directory`. The option archive `-a` is used to preserve the original file attributes, such as permissions, timestamps, etc., and using the `verbose -v` option provides a detailed output of the progress of the `rsync` operation.

We can also add additional options to customize the backup process, such as using compression and incremental backups:
`rsync -avz --backup --backup-dir=/path/to/backup/folder --delete /path/to/mydirectory user@backup_server:/path/to/backup/directory`

With this, we back up the `mydirectory` to the remote `backup_server`, preserving the original file attributes, timestamps, and permissions, and enabled compression `-z` for faster transfers. The `--backup` option creates incremental backups in the directory `/path/to/backup/folder`, and the `--delete` option removes files from the remote host that is no longer present in the source directory.

To restore the directory from the backup server to the local directory:
`rsync -av user@remote_host:/path/to/backup/directory /path/to/mydirectory`

# Encrypted Rsync
To ensure the security of our rsync file transfer between our local host and our backup server, we can combine the use of SSH and other security measures. By using SSH, we are able to encrypt our data as it is being transferred, making it much more difficult for any unauthorized individual to access it. 
## **##File System Management**

---

File system management on Linux is a complex process that involves organizing and maintaining the data stored on a disk or other storage device. Linux is a powerful operating system that supports a wide range of file systems, including `ext2`, `ext3`, `ext4`, `XFS`, `btrfs`, `NTFS`, and more.

The Linux file system is based on the Unix file system, which is a hierarchical structure that is composed of various components. At the top of this structure is the inode table, the basis for the entire file system. The inode table is a table of information associated with each file and directory on a Linux system. Inodes contain metadata about the file or directory, such as its permissions, size, type, owner, and so on. The inode table is like a database of information about every file and directory on a Linux system, allowing the operating system to quickly access and manage files. Files can be stored in the Linux file system in one of two ways:

- Regular files
- Directories

Regular files are the most common type of file, and they are stored in the root directory of the file system. Directories are used to store collections of files. When a file is stored in a directory, the directory is known as the parent directory for the files. In addition to regular files and directories, Linux also supports symbolic links, which are references to other files or directories. Symbolic links can be used to quickly access files that are located in different parts of the file system.

Disk management on Linux involves managing physical storage devices, including hard drives, solid-state drives, and removable storage devices. The main tool for disk management on Linux is the `fdisk`, which allows us to create, delete, and manage partitions on a drive. It can also display information about the partition table, including the size and type of each partition.

Each logical partition or drive needs to be assigned to a specific directory on Linux. This process is called mounting. Mounting involves attaching a drive to a specific directory, making it accessible to the file system hierarchy. Once a drive is mounted, it can be accessed and manipulated just like any other directory on the system. The `mount` tool is used to mount file systems on Linux, and the `/etc/fstab` file is used to define the default file systems that are mounted at boot time.

##Containerization 

Containerization is a process of packaging and running applications in isolated environments, such as a container, virtual machine, or serverless environment. Technologies like Docker, Docker Compose, and Linux Containers make this process possible in Linux systems. These technologies allow users to create, deploy, and manage applications quickly, securely, and efficiently. With these tools, users can configure their applications in various ways, allowing them to tailor the application to their needs. Additionally, containers are incredibly lightweight, perfect for running multiple applications simultaneously and providing scalability and portability. Containerization is a great way to ensure that applications are managed and deployed efficiently and securely.

#Docker 

Docker is an open-source platform for automating the deployment of applications as self-contained units called containers. It uses a layered filesystem and resource isolation features to provide flexibility and portability. Additionally, it provides a robust set of tools for creating, deploying, and managing applications, which helps streamline the containerization process.

```bash
#!/bin/bash# Preparation
sudo apt update -y
sudo apt install ca-certificates curl gnupg lsb-release -y
sudo mkdir -m 0755 -p /etc/apt/keyrings
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /etc/apt/keyrings/docker.gpg
echo "deb [arch=$(dpkg --print-architecture) signed-by=/etc/apt/keyrings/docker.gpg] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable" | sudo tee /etc/apt/sources.list.d/docker.list > /dev/null

# Install Docker Engine
sudo apt update -y
sudo apt install docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin -y

# Add user htb-student to the Docker group
sudo usermod -aG docker htb-student
echo '[!] You need to log out and log back in for the group changes to take effect.'

# Test Docker installation
docker run hello-world
```

|Command|Description|

|—-|—-|

|docker ps|list all running containers|

|docker stop|Stop a running container|

|docker start|Start a stopped container|

|docker restart|Restart a running container|

|docker rm|Remove a container|

|docker rmi|Remove a docker image|

|docker logs|View the log of a container|

#Linux containers

Linux Containers (`LXC`) is a virtualization technology that allows multiple isolated Linux systems to run on a single host. It uses resource isolation features, such as `cgroups` and `namespaces`, to provide a lightweight virtualization solution. LXC also provides a rich set of tools and APIs for managing and configuring containers, contributing to its popularity as a containerization technology. By combining the advantages of LXC with the power of Docker, users can achieve a fully-fledged containerization experience in Linux systems.

Both LXC and Docker are containerization technologies that allow for applications to be packaged and run in isolated environments. However, there are some differences between the two that can be distinguished based on the following categories:

- Approach
- Image building
- Portability
- Easy of use
- Security

LXC is a lightweight virtualization technology that uses resource isolation features of the Linux kernel to provide an isolated environment for applications.

### **Managing LXC Containers**

When working with LXC containers, several tasks are involved in managing them. These tasks include creating new containers, configuring their settings, starting and stopping them as necessary, and monitoring their performance.

| **Command** | **Description** |
| --- | --- |
| `lxc-ls` | List all existing containers |
| `lxc-stop -n <container>` | Stop a running container. |
| `lxc-start -n <container>` | Start a stopped container. |
| `lxc-restart -n <container>` | Restart a running container. |
| `lxc-config -n <container name> -s storage` | Manage container storage |
| `lxc-config -n <container name> -s network` | Manage container network settings |
| `lxc-config -n <container name> -s security` | Manage container security settings |
| `lxc-attach -n <container>` | Connect to a container. |
| `lxc-attach -n <container> -f /path/to/share` | Connect to a container and share a specific directory or file. |

It is important to configure LXC container security to prevent unauthorized access or malicious activities inside the container. This can be achieved by implementing several security measures, such as:

- Restricting access to the container
- Limiting resources
- Isolating the container from the host
- Enforcing mandatory access control
- Keeping the container up to date

## **Network Configuration**

Network access control is another critical component of network configuration. Different NAC technologies available:

- Discretionary access control (DAC)
- Mandatory access control (MAC)
- Role-based access control (RBAC)

Monitoring network traffic is also an essential part of network configuration. Therefore, we should know how to configure network monitoring and logging and be able to analyze network traffic for security purposes. Tools such as syslog, rsyslog, ss, lsof, and the ELK stack can be used to monitor network traffic and identify security issues.

### Configuring Network Interfaces

When working with Ubuntu, you can configure local network interfaces using the `ifconfig` or the `ip` command. These powerful commands allow us to view and configure our system's network interfaces.

One way to obtain information regarding network interfaces, such as IP addresses, netmasks, and status, is by using the `ifconfig` command. By executing this command, we can view the available network interfaces and their respective attributes in a clear and organized manner. This information can be particularly useful when troubleshooting network connectivity issues or setting up a new network configuration. It should be noted that the `ifconfig` command has been deprecated in newer versions of Linux and replaced by the `ip` command, which offers more advanced features. Nevertheless, the `ifconfig` command is still widely used in many Linux distributions and continues to be a reliable tool for network management.

**Activate Network Interface**

```bash
sudo ifconfig eth0 up     
sudo ip link set eth0 up
```

One way to allocate an IP address to a network interface is by utilizing the `ifconfig` command. We must specify the interface's name and IP address as arguments to do this. This is a crucial step in setting up a network connection

`sudo ipconfig eth0 192.168.1.2`

To set the netmask for a network interface:

`sudo ipconfig eth0 netmask 255.255.255.0`

When we want to set the default gateway for a network interface, we can use the `route` command with the `add` option. By setting the default gateway, we are designating the IP address of the router that will be used to send traffic to destinations outside the local network:

`sudo route add default gw 192.168.1.1 eth0`

When configuring a network interface, it is often necessary to set Domain Name System (`DNS`) servers to ensure proper network functionality. Setting up DNS can be achieved by updating the `/etc/resolv.conf` file with the appropriate DNS server information. The `/etc/resolv.conf` file is a plain text file containing the system's DNS information. It is important to note that any changes made to this file will only apply to the current session and must be updated if the system is restarted or the network configuration is changed.

`sudo vim /etc/resolv.conf`

After completing the necessary modifications to the network configuration, it is essential to ensure that these changes are saved to persist across reboots. This can be achieved by editing the `/etc/network/interfaces` file, which defines network interfaces for Linux-based operating systems. Thus, it is vital to save any changes made to this file to avoid any potential issues with network connectivity:

`sudo vim /etc/network/interfaces`

This will open the `interfaces` file in the vim editor. We can add the network configuration settings to the file like this:

![An example to add information to the interfaces]()

By setting the `eth0` network interface to use a static IP address of `192.168.1.2`, with a netmask of `255.255.255.0` and a default gateway of `192.168.1.1`, we can ensure that your network connection remains stable and reliable. Additionally, by specifying DNS servers of `8.8.8.8` and `8.8.4.4`, we can ensure that our computer can easily access the internet and resolve domain names. Once we have made these changes to the configuration file, saving the file and exiting the editor is important. After that, we must restart the networking service to apply the changes:

`sudo systemctl restart networking`

Various tools can help us identify and resolve issues regarding network troubleshooting on Linux systems. Some of the most commonly used tools include:

1. Ping
2. Traceroute
3. Netstat
4. Tcpdump
5. Wireshark
6. Nmap

The most common network issues we will encounter during our penetration tests include the following:

- Network connectivity issues
- DNS resolution issues (it's always DNS)
- Packet loss
- Network performance issues

Each issue, along with common causes that may include misconfigured firewalls or routers, damaged network cables or connectors, incorrect network settings, hardware failure, incorrect DNS server settings, DNS server failure, misconfigured DNS records, network congestion, outdated network hardware, incorrectly configured network settings, unpatched software or firmware, and lack of proper security controls. 

## Remote desktop protocols in linux
Remote desktop protocols are used in Windows, Linux, and macOS to provide graphical remote access to a system. The administrators can utilize remote desktop protocols in many scenarios like troubleshooting, software or system upgrading, and remote systems administration. The administrator needs to connect to the remote system they will administer remotely, and therefore, they use the appropriate protocol accordingly. In addition, they can log in using different protocols if they want to install an application on their remote system. The most common protocols for this usage are RDP (Windows) and VNC (Linux).

The XServer is the user-side part of the `X Window System network protocol` (`X11` / `X`). The `X11` is a fixed system that consists of a collection of protocols and applications that allow us to call application windows on displays in a graphical user interface. The ports that are utilized for X server are typically located in the range of `TCP/6001-6009`, allowing communication between the client and server. When starting a new desktop session via X server the `TCP port 6000` would be opened for the first X display `:0`. This range of ports enables the server to perform its tasks such as hosting applications, as well as providing services to clients. 

X11's significant disadvantage is the unencrypted data transmission. However, this can be overcome by tunneling the SSH protocol.

For this, we have to allow X11 forwarding in the SSH configuration file (`/etc/ssh/sshd_config`) on the server that provides the application by changing this option to `yes`.

Remote desctop protocol in Linux: 

```
cat /etc/ssh/sshd_config | grep X11Forwarding
```

Start the application in our client:
`ssh -X htb-student@10.129.23.11 /usr/bin/firefox`

The `X Display Manager Control Protocol` (`XDMCP`) protocol is used by the `X Display Manager` for communication through UDP port 177 between X terminals and computers operating under Unix/Linux. It is used to manage remote X Window sessions on other machines and is often used by Linux system administrators to provide access to remote desktops. XDMCP is an insecure protocol and should not be used in any environment that requires high levels of security. 

`Virtual Network Computing` (`VNC`) is a remote desktop sharing system based on the RFB protocol that allows users to control a computer remotely. It allows a user to view and interact with a desktop environment remotely over a network connection. The user can control the remote computer as if sitting in front of it. This is also one of the most common protocols for remote graphical connections for Linux hosts.

VNC is generally considered to be secure. It uses encryption to ensure the data is safe while in transit and requires authentication before a user can gain access.

Traditionally, the VNC server listens on TCP port 5900. So it offers its `display 0` there. Other displays can be offered via additional ports, mostly `590[x]`, where `x` is the display number. Adding multiple connections would be assigned to a higher TCP port like 5901, 5902, 5903, etc.

For these VNC connections, many different tools are used. Among them are for example:

- [TigerVNC](https://tigervnc.org/)
- [TightVNC](https://www.tightvnc.com/)
- [RealVNC](https://www.realvnc.com/en/)
- [UltraVNC](https://uvnc.com/)

The most used tools for such kinds of connections are UltraVNC and RealVNC because of their encryption and higher security.

Linux Security 

All computer systems have an inherent risk of intrusion. Some present more of a risk than others, such as an internet-facing web server hosting multiple complex web applications. Linux systems are also less prone to viruses that affect Windows operating systems and do not present as large an attack surface as Active Directory domain-joined hosts. Regardless, it is essential to have certain fundamentals in place to secure any Linux system.

One of the Linux operating systems' most important security measures is keeping the OS and installed packages up to date. This can be achieved with a command such as:

`apt update && apt dist-upgrade`

Besides, there are different applications and services such as [Snort](https://www.snort.org/), [chkrootkit](http://www.chkrootkit.org/), [rkhunter](https://packages.debian.org/sid/rkhunter), [Lynis](https://cisofy.com/lynis/), and others that can contribute to Linux's security. In addition, some security settings should be made, such as:

- Removing or disabling all unnecessary services and software
- Removing all services that rely on unencrypted authentication mechanisms
- Ensure NTP is enabled and Syslog is running
- Ensure that each user has its own account
- Enforce the use of strong passwords
- Set up password aging and restrict the use of previous passwords
- Locking user accounts after login failures
- Disable all unwanted SUID/SGID binaries

TCP wrapper is a security mechanism used in Linux systems that allows the system administrator to control which services are allowed access to the system. It works by restricting access to certain services based on the hostname or IP address of the user requesting access. TCP wrappers use the following configuration files:

- `/etc/hosts.allow`
- `/etc/hosts.deny`

In short, the `/etc/hosts.allow` file specifies which services and hosts are allowed access to the system, whereas the `/etc/hosts.deny` file specifies which services and hosts are not allowed access. These files can be configured by adding specific rules to the files.