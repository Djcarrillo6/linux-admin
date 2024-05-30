# Linux Administration: The Complete Linux Bootcamp For 2024
### Date: 3/27/2024

## Section 5: The Linux File System

### 5.24 - Intro to The Linux File System
- In a Linux file system, everything is a file. If something is not a file, then it's a process.
- `FHS` - The File System Hierarchy Standard:
  - `/` - The root directory
  - `bin` - The binary directory containes binaries or user executable files which are available to all users.
  - `boot` - The boot directory contains the files required for starting the system.
  - `dev` - The device directory contains device files.
  - `etc` - The system configuration directory contains most, if not all system – wide configuration files.
  - `home` - The home directory is where you will find your users home directories. Under this directory, there is another directory for each user, if that particular user has a home directory.
  - `lib` - The library directory contains shared library files used by different applications.
  - `media` - The media directory is used for external storage, will be automatically mounted.
  - `mnt` - The mount directory is list "media", but is not very often used these days. Used to be the directory for CD-ROM and floppy disks.
  - `opt` - The optional directory
  - `proc` - The process directory is a virtual directory that contains process information about your computer hardware, such as information about your CPU, RAM memory, and other hardware.
  - `run` - The runtime directory runs temporarily in RAM and 
  - `sbin` - The system binary directory contains applications that only the superuser(hence the initial s) will need.
  - `srv` - The server directory contains server-specific files and directories.
  - `sys` - The system directory
  - `tmp` - The temporary directory cotains temporary files usually stored by applications that are running.
  - `usr` - The user directory contains user-specific files and directories.
    - `/bin` - The binary directory
    - `/include` - The include directory
    - `/lib` - The library directory
    - `local` - The local directory
    - `sbin` - The system binary directory
    - `/src` - The source code directory
  - `var` - The variable directory usually contains variable-length files such as logs which are used by multiple applications.
    - `/cache` - The cache directory
    - `/lib` - The library directory
    - `/log` - The log directory
    - `/mail` - The mail directory
    - `/spool` - The spool directory
    - `/tmp` - The temporary directory

- `~` is always the home directory of the current user.
- On both `Ubuntu` & `CentOS` `/bin` & `/sbin` are simlinks to `/usr/bin` & `/usr/sbin` respectively.

##########################
## Linux Paths
##########################

`.`       # => the current working directory
`..`      # => the parent directory
`~`    # => the user's home directory

`cd`      # => changing the current directory to user's home directory
`cd ~`    # => changing the current directory to user's home directory
`cd - `   # => changing the current directory to the last directory
`cd /path_to_dir`    # => changing the current directory to path_to_dir 
`pwd`     # => printing the current working directory

## Installing tree
`sudo apt install tree`

`tree directory/`     # => Ex: tree .
`tree -d .`           # => prints only directories
`tree -f .`          # => prints absolute paths


### The `ls` Command Implementation Details
##########################

#### The ls Command

#### ls [OPTIONS] [FILES]

##########################

#### Listing the current directory

#### ~ => user's home directory

#### . => current directory

#### .. => parent directory

`ls`

`ls .`



#### Listing More Directories

`ls ~ /var /`


#### -l => Long Listing

`ls -l ~`


#### -a => Listing all files and directories including hidden ones

`ls -la ~`


#### -1 => Listing on a single column

`ls -1 /etc`


#### -d => Displaying information about the directory, not about its contents

`ls -ld /etc`


#### -h => Displaying the size in human readable format

`ls -h /etc`


#### -S => Displaying sorting by size

`ls -Sh /var/log`


#### Note: ls does not display the size of a directory and all its contents. Use `du` instead

`du -sh ~`


#### -X => Displaying sorting by extension

`ls -lX /etc`


#### --hide => Hiding some files

`ls --hide=*.log /var/log`


#### -R => Displaying a directory recursively

`ls -lR ~`


#### -i => Displaying the inode number

`ls -li /etc`


## Understanding File Timestamps: atime, mtime, ctime(stat, touch, date)
- Every file on Linux has three timestamps: atime, mtime, and ctime
- Each timestamp is an integer representing the number of seconds since the Unix Epoch (1970-01-01 00:00:00 UTC)
- The `atime` is the time of last access
- The `mtime` is the time of last modification
- The `ctime` is the time of last status change


### Running `ls -l`:
- This command will list the file type and permissions for each file in the current directory
  - The first character `-` represents the file type
  - The first character `d` represents the directory type
  - The first character `l` represents the symbolic link type
  - The first character `c` represents the character device type
  - The first character `b` represents the block device type
  - The first character `s` represents the socket type
  - The first character `p` represents the named pipe type



### File Timestamps and Date Commands:
##########################
  #### displaying atime:
  - `ls -lu`
  
  #### displaying mtime
  - `ls -l`
  - `ls -lt`
  
  #### displaying ctime
  - `ls -lc`
  
  #### displaying all timestamps
  - `stat file.txt`
  
  #### displaying the full timestamp
  - `ls -l --full-time /etc/`
  
  #### creating an empty file if it does not exist, update the timestamps if the file exists
  - `touch file.txt`
  
  #### changing only the access time to current time
  - `touch -a file`
  
  #### changing only the modification time to current time
  - `touch -m file`
  
  #### changing the modification time to a specific date and time
  - `touch -m -t 201812301530.45 a.txt`
  
  #### changing both atime and mtime to a specific date and time
  - `touch -d "2010-10-31 15:45:30" a.txt`
  
  #### changing the timestamp of a.txt to those of b.txt
  - `touch a.txt -r b.txt`
  
  #### displaying the date and time
  - `date`
  
  #### showing this month's calendar
  - `cal`
  
  #### showing the calendar of a specific year
  - `cal 2021`
  
  #### showing the calendar of a specific month and year
  - `cal 7 2021`
  
  #### showing the calendar of previous, current and next month
  - `cal -3`
  
  #### setting the date and time
  - `date --set="2 OCT 2020 18:00:00"`
  
  #### displaying the modification time and sorting the output by name.
  - `ls -l`
  
  #### displaying the output sorted by modification time, newest files first
  - `ls -lt`
  
  #### displaying and sorting by atime
  - `ls -ltu`
  
  #### reversing the sorting order
  - `ls -ltu --reverse`