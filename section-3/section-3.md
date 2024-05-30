# The Linux Terminal

- The `Terminal Emulator` is a crucial part of any Linux system because it allows you to interact with the Linux system through a shell.
- A `shell` is a program that takes commands from the user and gives them to the operating system's kernel to execute. It's also called the command interpreter. The shell gets started when the user logs in or when a program starts.
- The `bash` shell is the default shell on most Linux distributions.


### The Linux Command Structure
- The Linux command structure is similar to that of the Windows command structure.
- The Linux command structure is as follows:
    - `command` `options` `arguments`
    - `ping -c 5 google.com`
        - `ping` is the command
        - `-c` is the option
        - `5` is an argument
        - `google.com` is an argument


### Getting Help, Man, Pages
- The `man` command(short for manual) is used to display the manual pages for other commands which has the documentation for the command.
- A `man` page has a specific structure and syntax that document how the program/command is designed to be used:

- In the abbreviated output of `man ls` below, the bracked `[]` indicates optional arguments, and the ellipsis `...` indicates that the preceding argument can be repeated.

```bash
    man ls
```

```bash
NAME 
        ls - list directory contents

SYNOPSIS
        ls [OPTION]... [FILE]...

DESCRIPTION
        List information about the FILEs (the current directory by default)
```

### The `type` Command
- The `type` command is used to find out the type of a command.
    - A command can be a shell built-in command, a shell function, a shell script, a binary executable, or a source code file.

##########################
#### Getting Help in Linux
##########################

# MAN Pages
`man command`     # => Ex: man ls

### The man page is displayed with the less command
#### SHORTCUTS:
`h`         => getting help
`q`         => quit
`enter`     => show next line
`space`     => show next screen
`/string`   => search forward for a string
`?string`   => search backwards for a string
`n / N`     => next/previous appearance

##### checking if a command is shell built-in or executable file
`type rm`        # => rm is /usr/bin/rm
`type cd`        # => cd is a shell builtin

##### getting help for shell built-in commands
`help command`    # => Ex: help cd
`command --help`  # => Ex: rm --help

##### searching for a command, feature or keyword in all man Pages
`man -k uname`
`man -k "copy files"`
`apropos passwd`


##########################
#### Keyboard Shortcuts
##########################
TAB  # autocompletes the command or the filename if its unique
TAB TAB (press twice)   # displays all commands or filenames that start with those letters

# clearing the terminal
`CTRL + L`

# closing the shell (exit)
`CTRL + D`

# cutting (removing) the current line 
`CTRL + U`

# moving the cursor to the start of the line
`CTRL + A`

# moving the cursor to the end of the line
`Ctrl + E`

# stopping the current command
`CTRL + C`

# sleeping a the running program
`CTRL + Z`

# opening a terminal 
`CTRL + ALT + T`


##########################
### Bash History
##########################
- The `history` command is used to display the history of commands that you have executed.
- The `.bash_hisory` file contains the history of commands that you have executed.
- The `HISTSIZE` variable is used to set the maximum number of commands that can be stored in the history.
- The `HISTFILESIZE` variable is used to set the maximum number of commands that can be stored in the history file.
- The `HISCONTROL` variable is used to set the maximum number of commands that can be stored in the history file.
    - `ignorespace` - ignore commands that start with a space
    - `ignoredups` - ignore commands that are duplicates of the previous command
    - **The default on Ubuntu is `ignoreboth` which is equivalent to `ignorespace:ignoredups`. If you place a signle ` ` before a command, then it will be ignored in the history.**


##### showing the history
`history`

##### removing a line (ex: 100) from the history
`history -d 100`

##### removing the entire history
`history -c`

##### printing the no. of commands saved in the history file (~/.bash_history)
`echo $HISTFILESIZE`

##### printing the no. of history commands saved in the memory
`echo $HISTSIZE`

##### rerunning the last command from the history
`!!`

##### running  a specific command from the history (ex: the 20th command)
`!20`

##### running the last nth (10th) command from the history
`!-10`

##### running the last command starting with abc 
`!abc`

##### printing the last command starting with abc 
`!abc:p`

##### reverse searching into the history
`CTRL + R`

##### recording the date and time of each command in the history
`HISTTIMEFORMAT="%d/%m/%y %T"`

##### making it persistent after reboot
`echo "HISTTIMEFORMAT=\"%d/%m/%y %T\"" >> ~/.bashrc`
##### or
`echo 'HISTTIMEFORMAT="%d/%m/%y %T"' >> ~/.bashrc`

## Root User vs Normal User

##########################
### Running commands as root (sudo, su)
##########################
#### running a command as root (only users that belong to sudo group [Ubuntu] or wheel [CentOS])
`sudo command`

#### becoming root temporarily in the terminal
`sudo su`      # => enter the user's password

#### setting the root password
`sudo passwd root`

#### changing a user's password
`passwd username`

##### Becoming root temporarily in the terminal
`su`     # => enter the root password

- The `root` user is the superuser. It has access to all the files and directories on the system.
- The `normal` user is a regular user. It has access to only the files and directories that are created by the user.
- **Generally it's reccomended to not use `root` for standard/ordinary tasks. When `root` privledges are needed, it's better to use `sudo` to run the command as `root` user.**
- To log into the `root` account: `sudo su` which will prompt for the password.
- In terminal syntax: `$` = root, `#` = normal user will be appended to the prefix of the command.

##### The `sudo` Crendetial Cache Management:
- When you log into the `root` account, the `sudo` credential cache is created for 5 minutes(on Ubunut). This means that you can run `sudo` commands without having to enter the password for 5 minutes.
- To invalidate the cache credentials and force you to enter the password for every `sudo` command, run: `sudo -k`
- To invalidate the cache credentials and force you to enter the password for every `sudo` command for 10 minutes, run: `sudo -k 10`

##### Setting A New Password For The Root Account
- To set a new password for the `root` account, run: `sudo passwd`


## The `/` Directory
- The `/` directory is the root directory of the system.
- The `/root` directory is the home directory of the `root` user.
- The `/home` directory is the home directory of the `normal` user.