# Learning Dependecies

## 21st November 2024
Today, I learned about **Linux**, **Windows OS**, and **Virtual Private Server**. How to install them and make basic configurations. 


### Key Takeaways
- **Linux Navigation**: At first was a personal project started in 1991 by a finnish student Linus Torvalds.
- **Working with files and directories**: Available in over 600 distributions.
  

### Reflections
## Linux Navigation
Main commands to navigate in Linux:
- <span style="color:lightgreen"> *pwd*</span> - where am I;
- <span style="color:lightgreen"> *ls*</span> - to list all the contents inside a directory;
to display more information about directories and file I can use an option:
- <span style="color:lightgreen"> *ls -l*</span> - First, we see the total amount of blocks (1024-byte - 1 block) used by the files and directories listed in the current directory, also we see type and permissions, number of hard links to the file/directory, owner, group owner, size or number of blocks, date and time, and finally directory name.
- <span style="color:lightgreen"> *ls -la*</span> - to list all files of a directory, including hidden files that start with a dot at the beginning of its name. 
- <span style="color:lightgreen"> *cd*</span> - we can navigate to the directory and specify the path by adding the path to the specific directory, for instance: cd /dev/shm;
- <span style="color:lightgreen"> *cd -*</span> - to get back to the home directory;
- <span style="color:lightgreen"> *cd /dev/s [TAB x2]*</span> - if I type cd /dev/s and press *TAB* twice it will return all entries with the letter *s* in the directory of /dev/;
- <span style="color:lightgreen"> *cd ..*</span> - to jump to the parent directory, 1 level up in the directory hierarchy;
- <span style="color:lightgreen"> *touch*</span> - to create a file;
- <span style="color:lightgreen"> *mkdir*</span> - to create a directory;
- <span style="color:lightgreen"> *mkdir -p*</span> - to create parent directories;
- <span style="color:lightgreen"> *tree*</span> - to see the whole structure of directories;
- <span style="color:lightgreen"> *touch ./users/tom/readme.txt*</span> - create readme.txt inside tom dir, fram home directory;
- <span style="color:lightgreen"> *mv*</span> - move or rename files and dirs;
- <span style="color:lightgreen"> *rm*</span> - remove files;
- <span style="color:lightgreen"> *rm -r*</span> - remove not empty directory;
- <span style="color:lightgreen"> *rmdir*</span> - remove directory;
- <span style="color:lightgreen"> *nano*</span> file.txt - create text file in Nano editor;
- <span style="color:lightgreen"> *cat*</span> file.txt - to view the contents of the file;  
- <span style="color:lightgreen"> *which*</span> - to return the path to the file or link that should be executed;
- <span style="color:lightgreen"> *find*</span> - to find files and folders, I can use options to define search by parameters: 

![An example with multiple options](resources/find.png)
 
And here is an explonation of parameters:

![An detailed explanation of options](resources/find_parameters.png)


- <span style="color:lightgreen"> *locate*</span> - to return file or folders quicker through the system;
- <span style="color:lightgreen"> *find*</span> |wc -l - to count the total number of obtained results;  
- <span style="color:lightgreen"> *find*</span> 2> /dev/null - to redirect the resulting errors to the "null device", which discard all data;
- <span style="color:lightgreen"> *find*</span> 2> /dev/null > file.txt - to redirect standard result to file.txt without resulting errors;
- <span style="color:lightgreen"> *find*</span> 2> stderr.txt 1> stdout.txt - to direct STDOUT ot stdout file, and all resulting error files to STDERR;
- <span style="color:lightgreen"> *ls | grep*</span> ".txt" - in this case ls lists files, and its output is sent to `grep`, which filters for `.txt` files. 
- <span style="color:lightgreen"> *more*</span>
- <span style="color:lightgreen"> *less*</span>
- <span style="color:lightgreen"> *head*</span>
- <span style="color:lightgreen"> *tail*</span>
- <span style="color:lightgreen"> *sort*</span>
- <span style="color:lightgreen"> *grep -v*</span>
- <span style="color:lightgreen"> *cut*</span>
- <span style="color:lightgreen"> *tr*</span>
- <span style="color:lightgreen"> *column*</span>
- <span style="color:lightgreen"> *awk*</span>
- <span style="color:lightgreen"> *sed*</span>
- <span style="color:lightgreen"> *wc*</span>


**Practical Excersices** 
1. Used this command to resolve the problem: 
`find / -type f -name *.conf -size +25k -size -28k -newermt 2020-03-03 2>/dev/null` 
2. How many total packages are installed on the target system?
`dpkg -l | grep -c '^ii'`
3. How many files exist on the system that have the ".log" file extension?
`find / -type f -name *.log 2> /dev/null |wc -l`
