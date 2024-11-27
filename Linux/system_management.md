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