# Linux Administration: The Complete Linux Bootcamp For 2024
### Date: 5/29/2024

## Section 9 - Linux File Permissions


### File Permissions:
  - File permissions (file modes) specifcy who can access, change or execute a file on a Linux system.
  - It ensures that only authorized users and processes can access files and directories.
  - Each file or directory has an owner and a group. By default, the owner is the user who creates the file and the group is the primary group of the user who creates the file.
  - The ownership of a file or a directory can be changed only by root using the `chown` and `chgrp` commands.
  - For each file the permissions are assigned to three different categories of users:
    1. The file owner
    2. The group owner
    3. Other (anyone else or the outside world)
  
  - `ls -l /etc/passwd` -> `-rw-r--r-- 1 root 2972 May 29 18:14 /etc/passwd`:
    - The first character `-` defines the file type
    - The 9 characters that follow the first are the file permissions & a hyphen implies an absence of a file permission.
      - The first trio of this 9 define the owner permissions
      - The second trio of this 9 define the group permissions
      - The third trio of this 9 define the everyone else's permissions
  
  ### Octal (Numeric) Notation Of File Permissions:
    - Linux file permissions are representated in either a symbolic link or an octal notation.
    - See `./resources/octal-notation.pdf` for more details
  
  ### Changing File Permissions (chmod):
    - `chmod` is the command used to change the permissions of a file or a directory using either the symbolic link or octal notation.
    - Only the root, or the file's owner, can change the file's permissions.
  
  ### Changing File Ownership (chown, chgrp):
  See `./resources/chown-and-chgrp.pdf` for more details
  
  
  #### Special Permissions - SUID (Set User ID):
    - Besides, `r`, `w`, and `x` for the owner, group and others respectively, there are 3 extra special permissions for each file or directory: `SUID` or `Set User ID`, `SGID` or `Set Group ID`, and `Sticky` or `Sticky Bit`.
    - These special permissions are for a file or directory overall, not just for a user category.
    - **When an executeable file with SUID is executed then the resulting process will have the permissions of the owner of the command, not the permissions of the user who executed the command.**
    
    * Setting SUID:
     - Absolute Mode: `chmod 4XXX file`
     - Relative Mode: `chmod u+s file`
      
      [RUN]: `ls -l /usr/bin/passwd` -> `-rwsr-xr-x 1 root root 4775 May 29 18:14 /usr/bin/passwd`
  
  * For Details On SUID: [here](./resources/SUID.pdf)
  * For Details on SGID: `./resources/SGID.pdf`
  * For Detrails on Stick Bit: `./resources/sticky-bit.pdf`
  
  #### The `usmak` Command:
    - On Linux all files and directories are created with a default set of permissions. The `umask` utility allows you to view or set the base or the default permissions for a newly created file or directory.
      - The default permission for files is `0666` which means `readable, writable, and executable`
      - The default for directories is `0777` which means `readable, writable, and executable`, and `sticky bit`
  
  #### Understanding File Attributes:
    - The attributes define the properties of a file or a directory.
    - Linux allows for ACL(s) (Access Control Lists) to be associated with files.
    - Each file attribute can have one of two states: `set` or `cleared`.
    - The attributes are considered distinct from other metadata such as file system permissions, owner, group, and size.
    
    * The `lsattr` Command:
      - The `lsattr` command displays the attributes of a file or directory. 
      - Each attribute will have either a `-` or a `[CHARACTER]` depending on whether the attribute is set or cleared:
        - `e`: This means extend format and it indicates that the file is using extends for mapping the blocks on disk.
        - To see the rest of the options, use the `man lsattr` command.
    
    * The `chattr` Command:
      - The `chattr` command is used to change the attributes of a file or a directory.
      - To see the rest of the options, use the `man chattr` command.
  
  
  ### File Permissions Commands:
    #### LEGEND
    `u` = User
    `g` = Group
    `o` = Others/World
    `a` = all
    
    `r` = Read
    `w` = write
    `x` = execute
    `-` = no access
    
    ##### Displaying the permissions (ls and stat)
      - `ls -l /etc/passwd`
        
        Example Output of `ls -l /etc/passwd`:
          -rw-r--r-- 1 root root 2871 aug 22 14:43 /etc/passwd
      
      - `stat /etc/shadow`
        Example Outputof `stat /etc/shadow`:
              File: /etc/shadow
              Size: 1721      	Blocks: 8          IO Block: 4096   regular file
              Device: 805h/2053d	Inode: 524451      Links: 1
              Access: (0640/-rw-r-----)  Uid: (    0/    root)   Gid: (   42/  shadow)
              Access: 2020-08-24 11:31:49.506277118 +0300
              Modify: 2020-08-22 14:43:36.326651384 +0300
              Change: 2020-08-22 14:43:36.342652202 +0300
              Birth: -
    
    ##### Changing the permissions using the relative (symbolic) mode:
      - `chmod u+r filename`
      - `chmod u+r,g-wx,o-rwx filename`
      - `chmod ug+rwx,o-wx filename`
      - `chmod ugo+x filename`
      - `chmod a+r,a-wx filename`
    
    ##### Changing the permissions using the absolute (octal) mode:
      PERMISSIONS      EXAMPLE
      u   g   o
      rwx rwx rwx     chmod 777 filename
      rwx rwx r-x     chmod 775 filename
      rwx r-x r-x     chmod 755 filename
      rwx r-x ---     chmod 750 filename
      rw- rw- r--     chmod 664 filename
      rw- r-- r--     chmod 644 filename
      rw- r-- ---     chmod 640 filename
    
    ##### setting the permissions as of a reference file
      - `chmod --reference=file1 file2`
    
    ##### Changing permissions recursively
      - `chmod -R u+rw,o-rwx filename`
    
    #### SUID (Set User ID):
      ##### Displaying the SUID permission:
      - `ls -l /usr/bin/umount` 
      
      Example Output of `ls -l /usr/bin/umount`:
        -rwsr-xr-x 1 root root 39144 apr  2 18:29 /usr/bin/umount
      
      - `stat /usr/bin/umount`
      
      Example Output of `stat /usr/bin/umount`:
          File: /usr/bin/umount
          Size: 39144     	Blocks: 80         IO Block: 4096   regular file
          Device: 805h/2053d	Inode: 918756      Links: 1
          Access: (4755/-rwsr-xr-x)  Uid: (    0/    root)   Gid: (    0/    root)
          Access: 2020-08-22 14:35:46.763999798 +0300
          Modify: 2020-04-02 18:29:40.000000000 +0300
          Change: 2020-06-30 18:27:32.851134521 +0300
          Birth: -
      
      # Setting SUID
        - `chmod u+s executable_file`
        - `chmod 4XXX executable_file`      # => Ex: chmod 4755 script.sh
      
      
      #### SGID (Set Group ID):
        ##### Displaying the SGID permission
        - `ls -ld projects/`
        
        Example Output of `ls -ld projects/`:
        drwxr-s--- 2 student student 4096 aug 25 11:02 projects/
        
        - `stat projects/`
        
        Example Output of `stat projects/`:
            File: projects/
            Size: 4096      	Blocks: 8          IO Block: 4096   directory
            Device: 805h/2053d	Inode: 266193      Links: 2
            Access: (2750/drwxr-s---)  Uid: ( 1001/ student)   Gid: ( 1002/ student)
            Access: 2020-08-25 11:02:15.013355559 +0300
            Modify: 2020-08-25 11:02:15.013355559 +0300
            Change: 2020-08-25 11:02:19.157290764 +0300
            Birth: -
        
        ##### setting SGID
          - `chmod 2750 projects/`
          - `chmod g+s projects/`
    
    
    ## The Sticky Bit
      - The stick bit is used to allow a file to be executed with only the owner's permission.
      ##### Displaying the sticky bit permission
      - `ls -ld /tmp/`
      
      Example Output of `ls -ld /tmp/`:
        drwxrwxrwt 20 root root 4096 aug 25 10:49 /tmp/
      
      - `stat /tmp/`
      
      Example Output of `stat /tmp/`:
        File: /tmp/
        Size: 4096      	Blocks: 8          IO Block: 4096   directory
        Device: 805h/2053d	Inode: 786434      Links: 20
        Access: (1777/drwxrwxrwt)  Uid: (    0/    root)   Gid: (    0/    root)
        Access: 2020-08-22 14:46:03.259455125 +0300
        Modify: 2020-08-25 10:49:53.756211470 +0300
        Change: 2020-08-25 10:49:53.756211470 +0300
        Birth: -
      
      ##### Setting the sticky bit
      - `mkdir temp`
      - `chmod 1777 temp/`
      - `chmod o+t temp/`
      - `ls -ld temp/`
      
      Example Output of `ls -ld temp/`:
        drwxrwxrwt 2 student student 4096 aug 25 11:04 temp/
    
    
    #### UMASK:
      ##### Displaying the UMASK
      - `umask` 
      
      ##### Setting a new umask value
      - umask new_value     # => Ex: umask 0022
      
      #### Changing File Ownership (root only):
        ##### Changing the owner
        - `chown new_owner file/directory`      # => Ex: sudo chown john a.txt
        
        ##### Changing the group owner
        - `chgrp new_group file/directory`
        
        ##### Changing both the owner and the group owner
        - `chown new_owner:new_group file/directory`
        
        ##### Changing recursively the owner or the group owner
        - `chown -R new-owner file/directory`
        
        ##### displaying the file attributes
        - `lsattr filename`
        
        ##### Changing the file attributes
        - `chattr +-attribute filename`     # => Ex: sudo chattr +i report.txt