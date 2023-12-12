# Configuring Linux File Permissions
<h2>Description</h2>
In this project, I practiced the principle of least privilege by using bash commands on Linux to change file permissions. I investigated the directory to identify misconfigured permissions.  

<h2>Check file and directory details (examples highlighted in yellow!)</h2>
To start my investigation, I used the “pwd” command to see my current directory.

<br>I used the “ls” command to view the current folders and files discovered “projects”

After that, I navigated to the “projects” folder by using the “cd projects” command. <br>The "cd" command is used when you want to change the directory. Add "cd" and then add your argument, which is the "name" of the directory. 

I typed the” ls -l” command to view the files and folder permissions of files and folders in the "projects" folder. <br>

I typed in the “ls -la” command to view the permissions for hidden files and folders, then I discovered a hidden file called “.project_x.txt” Having "." in front of the file indicates that the file is hidden.

<img src="https://imgur.com/ERqgvsL.png" height="80%" width="80%"/>

<h2>Change file permissions  (examples highlighted in yellow!)</h2>
The project_k.txt file was misconfigured for “other” 

project_k.txt reads “-rw-rw-rw-” <br>

Here is how to read these permissions:<Br>
| Letter | Description |
|----------|----------|
| r = Read: for files & folders |This is the ability to read the file contents; for directories, this is the ability to read all contents in the directory including both files and subdirectories |
| w = Write: for files & folders | This is the ability to make modifications on the file contents; for directories, this is the ability to create new files in the directory |
| e = Execute: for files & folders | This is the ability to execute the file if it’s a program; for directories, this is the ability to enter the directory and access its files|

| Owner Type | Description |
|----------|----------|
| USER | The owner of the file |
| GROUP | A group that the owner is part of |
| OTHER | All other users on the system


| Character | Example | Meaning |
|:---|  :--- |  :--- |
| 1st   | **d**rwxrwxrwx   | File Type <br> **d** for directory <br> **-** for a regular file    |
||| **USER (2nd to 4th character)**|
| 2nd    | d**r**wxrwxrwx   | Read Permissions for the user <br> **r** if the user has Read permissions <br> **-** if the user lacks Read permissions|
| 3rd    | dr**w**xrwxrwx    | Write Permissions for the user <br> **w** if the user has Write permissions<br> **-** if the user lacks Write permissions  |
| 4th    | drw**x**rwxrwx    | Execute Permissions for the user <br> **r** if the user has Execute permissions <br> **-** if the user lacks Execute permissions    |
||| **GROUP (5th to 7th character)**|
| 5th    | drwx**r**wxrwx    | Read Permissions for the group <br> **r** if the group has Read permissions <br> **-** if the group lacks Read permissions    |
| 6th    | drwxr**w**xrwx    | Write Permissions for the group <br> **r** if the group has Write permissions <br> **-** if the group lacks Write permissions    |
| 7th    | drwxrw**x**rwx    |Execute Permissions for the group <br> **r** if the group has Execute permissions <br> **-** if the group lacks Execute permissions    |
|||**OTHER (8th to 10th character)**|
| 8th    | drwxrwx**r**wx    | Read Permissions for the other <br> **r** if the other has Read permissions <br> **-** if the other lacks Read permissions    |
| 9th    | drwxrwxr**w**x    | Write Permissions for the other <br> **r** if the other has Write permissions <br> **-** if the other Write permissions    |
| 10th    | drwxrwxrw**x**    | Execute Permissions for the other <br> **r** if the other has Execute permissions <br> **-** if the other lacks Execute permissions    |

<br> From the tables “-rw-rw-rw-” means that User, Group, and Other have "rw-" permissions, this tells us that each group has read and write with no execute permissions because of the "-" symbol at the end. All other users on the system "Other" should not have write permissions.

<img src="https://imgur.com/9Rbi2DX.png" height="80%" width="80%"/>

I typed "chmod o-w project_k.txt" to remove write permissions from “other”.

**The chmod command is used to modify or change permissions and it requires two arguments:** 
<Br>The first argument indicates how to change permissions. 
<br>The second argument indicates the file or directory you want to change permissions for.

<br> In the command "chmod **o-w** project_k.txt" 

<br>The first argument is "o-w", "o" means other, "-" means to remove, we use "+" for adding permissions. "w" means write which means I want to remove write permissions to the "other" group.

<br> The second argument is the file I want to change the permissions for, which is "project_k.txt.

<br>After I typed this command. It now reads” -rw-rw-r--”. Write permissions are now removed from "other".

<img src="https://imgur.com/uYSFSho.png" height="80%" width="80%"/>

project_m.txt file permission for the "research_team" group had read permissions when they shouldn't have.

<img src="https://imgur.com/OABjUW3.png" height="80%" width="80%"/>

I typed “chmod g-r project_m.txt” to remove read permissions from the "research_team" group. 
The first argument is "g-r" which means remove "read" permissions from "group". Remember "g = group" and "-" means remove, and "r" means read.
<br>It now reads “-rw------” so the "research_team" group has no access at all.

<img src="https://imgur.com/erY1xu1.png" height="80%" width="80%"/>

<h2>Change file permissions on a hidden file  (examples highlighted in yellow!)</h2>
Remember hidden files have "." in front of file names.
<br>The user “researcher2” and group “research_team” have incorrect permissions for the hidden file ".project_x.txt"
<br>The current permission reads “-rw--w-----” This indicates that the user has read and write permissions while the group has write permissions.
<br>Both the users and the group should only have read permissions and no write permissions. 
<br>So now I need to remove the write permissions for both the user and the group while adding read permissions to the group. 
<img src="https://imgur.com/DuRIUBr.png" height="80%" width="80%"/>

To change to  the correct permissions I typed “chmod u-w, g-w, g+r .project_x.txt” 
The first argument removes write permissions from the "users" and "group", and also adds read permission, hence the "+" sign in the command.
<br>It now reads “-r-r-----” Only the user and group can read this hidden file now.

<img src="https://imgur.com/uAtCW4R.png" height="80%" width="80%"/>

<h2>Change directory permissions  (examples highlighted in yellow!)</h2>
The “research_team” group has access to the “drafts’” folder when they shouldn't have.
</br>“ Drwx--x---” means research_team has executable permissions, therefore they have access.

<img src="https://imgur.com/FEGsjbv.png" height="80%" width="80%"/>

I typed” chmod g-x drafts” to remove access to drafts from the group “research_team” 
<br> "g" means group, "-" means to remove, "x" means execute permissions. 
<br>It now reads “drwx------” research_team has no permissions or access to the folder now.
Only the user has read, write, and execute permissions.
<img src="https://imgur.com/7FE73do.png" height="80%" width="80%"/>


<h2>Summary</h2>
In conclusion, I identified regular files and hidden files that had misconfigured permissions and was able to change these permissions back to a secure configuration, therefore increasing this fictional company's security posture.


