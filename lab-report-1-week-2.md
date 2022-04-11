![Image](https://github.com/Rudra17381/cse15l-lab-reports/blob/c723367ad687ae38a6f2d41ed92e1bda7d0d5d97/95ADA822-49E8-4BD5-A135-7C4889196355.jpeg)

# Lab Report Week 1

## Installing Visual Studio Code
---

#### Downloading VS Code
First we need to download visual studio code from the link given below.
> [Download Visual Studio Code](https://code.visualstudio.com)

It should look something like this:
![img](dndd)

#### Installing VS Code
Double click the downloaded file and follow the instructions to install visual studio code on your local computer

## Remotely Connecting
---

Often in real life situations be it normal jobs, businesses or scientific research, anything relating to IT will have you log into a remote server or computer to do your work. This may be due to security reasons, having to work with files that couldn't fit on local machines or simply local machines not having enough computing power to process the work you are trying to do. Due to this reason it is a good idea for organizations to have remote servers which can be powerful, have a large memory storage and be secure which allows all of its employees to be able to work with the same computing power and storage. In UCSD as well we have remote servers and IT services where we can log in and do our work. Often, CSE courses will have their work on these course specific servers and accounts. This course, CSE 15L is one such example where we need to be able to log into the remote server. 

Follow these steps to remotely connect to the server

1. **Install Open SSH if you are on a windows computer from the link below**
> [Open SSH](https://docs.microsoft.com/en-us/windows-server/administration/openssh/openssh_install_firstuse)
2. **Look up your course specific account from the link below**
> [UC San Diego Educational Technology Services](https://sdacs.ucsd.edu/~icc/index.php)
3. **Connecting to remote host**
    * Open the terminal in VS Code.
    * Type in the following command: ```ssh cs15lsp22zz@ieng6.ucsd.edu```  
    ```ssh``` here is the secure protocol that allows us to connect to the remote server.  
    ```cse15lsp22zz``` here is the user
        * ```cse15l``` is the course name 
        * ```sp22``` is the quarter (spring quarter 2022)
        * ```zz``` is your course specific account name
    ```ieng6.ucsd.edu``` is the host name where we will be connecting to.
    * Connecting to it the first time you should see the following message  
    ![img](difnidnf)
    * Your client PC is now connected to a host UCSD server computer.

## Trying Some Commands
---

There are many easy to learn commands that can help you navigate the host computer and use it as if its your own computer. These are command line commands so they are slightly different that the GUI interface of your computer that you may be used to but it should not be too difficult to pick up.
Note that these commands can be used on your own local computer as well.

#### Some Example Commands:
* ```cd```: This command helps you change the current directory that you are in.
* ```ls```: This command lists out all the files in the current directory.
* ```pwd```: This command prints out the whole path from the root directory to the current directory.
* ```mkdir```: This command creates a new empty directory with the name you give it.
* ```cp```: This command is used to copy files, groups of files or directories.
* ```-l```: This is sorta like a modifier, with ```ls``` it lists out all files and directories in long format.
* ```-a```: This is sorta like a modifier, with ```ls``` it lists out all files and directories wether they are hidden or not.
* ```-t```: This is sorta like a modifier, with ```ls``` it lists out all the files sorted by the time of last modification.

#### Try running some useful commands and seeing their output (Taken from Lab1):
* ```cd ~```: Should change your current directory to home directory.
* ```cd "child directory"```: Should change your current directory to one of its children.
* ```ls -lat```: Should list out all the files in the current directory in long format regardless of wether they are hidden or not. These files should be sorted by the date they were last modified. Notice how ```-lat``` is a combination of ```-l``` ```-a``` and ```-t```.
* ```ls /home/linux/ieng6/cs15lsp22/cs15lsp22abc``` where ```abc``` is your course specific account: This should display all the files in this current directory.
* ```cp /home/linux/ieng6/cs15lsp22/public/hello.txt ~/```: Should copy the file on location 1 (in this case ```hello.txt```) to location 2 (in this case the root directory.)
* ```cat /home/linux/ieng6/cs15lsp22/public/hello.txt```: Should print out the contents of ```hello.txt```.

**Press ```Ctrl + D``` or Run the ```exit``` command to exit the terminal.**

## Moving Files with ```scp```
---

One usual sitaution you might run into while working on a remote server is needing to move or copy files form the remote host to the local client computer. There may be many reasons for this: 
* Wanting to work offline, while on a bus or at home with unstable internet connection
* Having key files that may disrupt the server if there are any errors (in this case running them on a virtual machine or on a local client computer before pushing it to the remote server may be ideal to spot out errors and prevent it from causing collateral damage)
* Simply wanting faster read and write times for smaller files or datasets while testing multiple different AI models or programs (uploading or downloading files for each test is slow as the speed can be max a few hundered megabytes meanwhile the SSD on your local client PC has often read and write speeds of several gigabytes)

Whatever the reason may be, it is important to learn how to move files over ```ssh``` using ```scp```.






 




