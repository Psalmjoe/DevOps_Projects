# Linux Practice Project
## Introduction to Basic Linux Commands
Linux commands  are executed on Terminal by pressing Enter at the end of line. You can run commands to perform various tasks, from package installation to user management and file manipulation.

Here's what a Linux command's general syntax looks like

```CommandName [option(s)] [parameter(s)]``` 

## File Manipulation
### 1. Sudo command 
This is short for *superuser do*, sudo is one of the most popular basic Linux commands that lets you perform tasks that requires administrative or root permissions.

The general syntax is:

```sudo (command e.g apt upgrade) ```

For example:

```sudo apt upgrade```
![Alt text](<Images/Screenshot 2023-11-15 151413.png>)

### 2. pwd Command
The pwd command stands for *Print Working Directory*. It provides information about the current/present directory that is being worked in.

```pwd [option]```

It has two acceptable options:

*-L (logical) Use pwd from environment even if it contains symbolic links.*

*-P (physical) Avoid all symbolic links, and instead give you an absolute path.*

```pwd```

![Alt text](<Images/Screenshot 2023-11-15 153229.png>)

### 3. cd Command
The cd command in Linux stands for *Change Directory.* It is used to change the current directory of the terminal.

It uses the syntax below:

```cd CommandsLinux```

An example is shown below:

![Alt text](<Images/Screenshot 2023-11-15 154303.png>)

Here are some shortcuts to help navigate the cd command :

```cd ~ [username]``` goes to another user's home directory

```cd..``` moves one directory up

```cd -``` move to your previous directory.

### 4. ls Command

ls is a Linux shell command that lists directory contents of files and directories. It provides valuable information about files, directories, and their attributes. Running it without a flag or parameter will show the current working directory's content.
![Alt text](<Images/Screenshot 2023-11-15 154945.png>)


To see other directories' content, type ls followed by the desired path. For example, to view files in the Document folder, enter :

```ls Documents```

![Alt text](<Images/Screenshot 2023-11-15 155415.png>)

Here are some options you can use with the ls command

```ls -R``` lists all the files in the subdirectories

```ls -a``` shows hidden files in addition to the visible ones

```ls -lh``` shows the file sizes in easily readable format, such as MB, GB, and TB
![Alt text](<Images/Screenshot 2023-11-15 160213.png>)

### 5. cat Command
Cat(concatenate) command is very frequently used in Linux. It reads data from the file and gives its content as output. It helps us to create, view, and concatenate files. To run the cat command, type cat followed by the file name and extention. For instance;

```cat Learning-linux```
![Alt text](<Images/Screenshot 2023-11-15 163548.png>)


Here are other ways to use the cat command :

```cat filename1.txt filename2.txt > filename3.txt```
![Alt text](<Images/Screenshot 2023-11-15 163918.png>)

*Merges file1.txt and file2.txt and stores the output in file3.txt*

```tac file1.txt```

This command displays the content of a a file in reverse order.
![Alt text](<Images/Screenshot 2023-11-15 165221.png>)

### 6. cp Command
cp stands for a copy. This command is used to copy files or groups of files or directories. To copy files from the current directory to another directory, enter cp followed by the file name and the destination directory. For example;

```cp sample.md test-folder```
![Alt text](<Images/Screenshot 2023-11-15 170127.png>)

To copy the content of a file to a new file in the same directory, enter cp followed by the source and dsetination file as below :

```cp file.txt file2.txt```
![Alt text](<Images/Screenshot 2023-11-15 170628.png>)

To copy an entire directory, use the R flag as shown below

``` cp -R sample Devops_linux/```
![Alt text](<Images/Screenshot 2023-11-15 171809.png>)

### 7. mv Command
mv command is used to move and rename files and directories. To move a file, include destination path. For example

```mv sample test-folder```

![Alt text](<Images/Screenshot 2023-11-15 173357.png>)

mv can also be used to rename a file or folder. For example;

``` mv sample new-sample```

![Alt text](<Images/Screenshot 2023-11-15 173907.png>)

### 8. mkdir Command
mkdir command in Linux allows the user to create directories (also referred to as folders in some operating systems). This command can create multiple directories at once as well as set the permissions for the directories.

Here's the basic syntax

```mkdir [option] directory_name```

For example, to create a directly called music

```mkdir Music```
![Alt text](<Images/Screenshot 2023-11-15 175321.png>)

To make a new directory called song inside music, use the command :

```mkdir music/Songs```

![Alt text](<Images/Screenshot 2023-11-15 175759.png>)

### 9. rmdir Command
The rmdir command removes the directory, specified by the Directory parameter, from the system. The directory must be empty before you can remove it, and you must have write permission in its parent directory.

To remove and empty dirextory from its parent directory, use the below cammand :

```rmdir music/songs```
![Alt text](<Images/Screenshot 2023-11-15 180634.png>)

### 10. rm Command
The rm Command rm stands for remove, and it is used to remove files, directories, and links. By default, it does not remove directories. This command normally works silently and it should be used carefully, because once you delete a file in Linux the content cannot be recovered.

Syntax :

```rm filename```

Multiple files can be removed by running the below command :

```rm file1.txt file2.txt file3.txt```
![Alt text](<Images/Screenshot 2023-11-15 180957.png>)












