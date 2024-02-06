# Basic Linux Commands

## Navigation

```Bash
# Print Working Directory
pwd
```
```Bash
#List
ls 
#List long
ls -l
#List Long / All
ls -la
```
``` Bash
#Change Directory
cd 
#Shortcut to home
cd ~
#Current directory
cd .
#Parent directory
cd ..
```

## Man pages
Manual pages gives description of command and how to use

```Bash
man 

#Search for command
man -k
#Search for term
man /term
#Show next page
n
```
```Output example```
```Bash
MAN(1)                                                       Manual pager utils                                                       MAN(1)

NAME
       man - an interface to the system reference manuals

SYNOPSIS
       man [man options] [[section] page ...] ...
       man -k [apropos options] regexp ...
       man -K [man options] [section] term ...
       man -f [whatis options] page ...
       man -l [man options] file ...
       man -w|-W [man options] page ...

DESCRIPTION
       man  is the system's manual pager.  Each page argument given to man is normally the name of a program, utility or function.  The man‐
       ual page associated with each of these arguments is then found and displayed.  A section, if provided, will direct man to  look  only
       in  that  section of the manual.  The default action is to search in all of the available sections following a pre-defined order (see
       DEFAULTS), and to show only the first page found, even if page exists in several sections.
```
## File Directory
```Bash
#Make Directory
mkdir
#Remove Directory
rmdir
#Make Blank File
touch
#Copy file or directory
#Example: cp ./source_file ./destination_file
cp
#Move file or directory
#Example: mv ./source_file ./destination_directory
mv
#Remove file
rm
```

## Permissions

### File Permission Example
-rw-r--r-- 1 dialtone dialtone    0 Feb  6 10:51 example

|File Type|Permissions|Number of hard links|Owners|File Size|Last Modified (Date,Time)| File Name|
|----|---|----|-----|----|---|---|
|-|rw-r--r--| 1 |dialtone dialtone|    0| Feb  6 10:51 |example|
### File Permissions

|Permission Type|Symbol|If a file has this permission, you can|if a directory has this permission, you can|
|--------------|-----------|-----------|----------------|
| READ | r | Open and view file contents | read direcory contents |
|WRITE | w | Edit, delete or rename file | Edit, delete, or rename files within the directory|
|EXECUTE|x | Execute the file | Enter the directory; without x, the directory's r and w permissions are useless|
|NONE| - | Do nothing | Do nothing |


### Placements
|P1 | P2 | P3 | P4 | P5 | P6 | P7 | P8 | P9 | P10
|---|---|---|---|---|---|---|---|---|---|
|-|r|w|-|r|-|-|r|-|-|  
|d|r|w|x|r|-|x|-|-|-|  
 
### Placement explained

| Position   | Definition of position  | Permission |
|------------|-------------------------|------------|
| Position 1 | (-) File (D) /Directory | File type
| Position 2 | Read (r)|User/Owner of the file or directory
| Position 3 | Write (w)|User/Owner of the file or directory
| Position 4 | Execute (x)|User/Owner of the file or directory 
| Position 5 | Read (r)|Group of the file or directory
| Position 6 | Write (w)|Group of the file or directory
| Position 7 | Execute (x)|Group of the file or directory 
| Position 8 | Read (r)|Other of the file or directory
| Position 9 | Write (w)|Other of the file or directory
| Position 10 | Execute (x)|Other of the file or directory 
 
 ## Binary Permissions
 Made of 3 octets [1 = on for permission 0 = off for permission]

 |File Type position| Binary 4 | Binary 2 | Binary 1 | Definition |
 |----|----|----|----|----|
 |----| 0 | 0 | 0 | No permissions
 |----| 0 | 0 | 1 | Execute only
 |----| 0 | 1 | 0 | Write Only
 |----| 0 | 1 | 1 | Write / Execute
 |----| 1 | 0 | 0 | Read Only 
 |----| 1 | 0 | 1 | Read / Execute
 |----| 1 | 1 | 0 | Read / Write
 |----| 1 | 1 | 1 | Read / Write / Execute

## Permission Related Commands
Change permissions of file or directory
```BASH 
chmod # Change file by permission or by bits
```
chmod has 3 permission arguements that can be accepted (Who: U(u)ser,G(g)roup,O(o)ther,A(a)ll, Grant/Revoke, Which r,w,x)
```Example```
```bash
-rw-r--r-- 1 user group    0 Feb  6 10:51 example #(original)
chmod u -r example
---------- 1 user group    0 Feb  6 10:51 example #(altered)

#or

-rw-r--r-- 1 user group    0 Feb  6 10:51 example #(original)
chmod 751 example
-rwxr-x--x 1 dialtone dialtone    0 Feb  6 10:51 example #(altered)
```