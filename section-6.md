# Linux Administration: The Complete Linux Bootcamp For 2024
### Date: 5/29/2024

## Section 6: The Linux File System

### Viewing files (cat, less, more, head, tail, watch):
#### displaying the contents of a file
- `cat filename`

#### displaying more files
- `cat filename1 filename2`

#### displaying the line numbers
- `can -n filename`

#### concatenating 2 files
- `cat filename1 filename2 > filename3`

#### viewing a file using less
- `less filename`

#### less shortcuts:
- `h`         => getting help
- `q`         => quit
- `enter`     => show next line
- `space`     => show next screen
- `/string`   => search forward for a string
- `?string`   => search backwards for a string
- `n / N`    => next/previous appearance

#### showing the last 10 lines of a file
  - `tail filename`

#### showing the last 15 lines of a file
- `tail -n 15 filename`

#### showing the last lines of a file starting with line no. 5
  - `tail -n +5 filename`

#### showing the last 10 lines of the file in real-time
  - `tail -f filename`

#### showing the first 10 lines of a file
  - `head filename`

#### showing the first 15 lines of a file
  - `head -n 15 filename`

#### running repeatedly a command with refresh of 3 seconds
  - `watch -n 3 ls -l`


### Working with files and directory (touch, mkdir, cp, mv, rm, shred):
#### creating a new file or updating the timestamps if the file already exists
  - `touch filename`

#### creating a new directory
  - `mkdir dir1`

#### creating a directory and its parents as well
  - `mkdir -p mydir1/mydir2/mydir3`

### The cp command
#### copying file1 to file2 in the current directory
  - `cp file1 file2`

#### copying file1 to dir1 as another name (file2)
  - `cp file1 dir1/file2`

#### copying a file prompting the user if it overwrites the destination
  - `cp -i file1 file2`

#### preserving the file permissions, group and ownership when copying
  - `cp -p file1 file2`

#### being verbose
  - `cp -v file1 file2`

#### recursively copying dir1 to dir2 in the current directory
  - `cp -r dir1 dir2/`

#### copy more source files and directories to a destination directory
  - `cp -r file1 file2 dir1 dir2 destination_directory/`


### The mv command:
#### renaming file1 to file2
  - `mv file1 file2`

#### moving file1 to dir1 
  - `mv file1 dir1/`

#### moving a file prompting the user if it overwrites the destination file
  - `mv -i file1 dir1/`

#### preventing a existing file from being overwritten
  - `mv -n file1 dir1/`

#### moving only if the source file is newer than the destination file or when the destination file is missing
  - `mv -u file1 dir1/`

#### moving file1 to dir1 as file2
  - `mv file1 dir1/file2`

#### moving more source files and directories to a destination directory
  - `mv file1 file2 dir1/ dir2/ destination_directory/`


### The rm command:
#### removing a file
  - `rm file1`

#### being verbose when removing a file
  - `rm -v file1`

#### removing a directory
  - `rm -r dir1/`

#### removing a directory without prompting
  - `rm -rf dir1/`

#### removing a file and a directory prompting the user for confirmation
  - `rm -ri fil1 dir1/`

#### secure removal of a file (verbose with 100 rounds of overwriting)
  - `shred -vu -n 100 file1`


### Piping and Command Redirection
  - Every Linux command or profram has 3 data streams connected to it:
    1. STDIN(0) - Standard Input
    2. STDOUT(1) - Standard Output
    3. STDERR(2) - Standard Error
  
  * Possible Flows:
    STDIN(0) -> COMMAND -> STDOUT(1)
              **OR**
    STDIN(0) -> COMMAND -> STDOUT(3)
  
  ### Piping Examples:
    - `ls -lSh /etc/ | head`            # see the first 10 files by size
    - `ps -ef | grep sshd`              # checking if sshd is running
    - `ps aux --sort=-%mem | head -n 3`  # showing the first 3 process by memory consumption
  
  ### Command Redirection Examples:
    #### output redirection
      - `ps aux > running_processes.txt`
      - `who -H > loggedin_users.txt`
    
    #### appending to a file
      - `id >> loggedin_users.txt`
    
    #### output and error redirection
      - `tail -n 10 /var/log/*.log > output.txt 2> errors.txt`
    
    #### redirecting both the output and errors to the same file
      - `tail -n 2 /etc/passwd /etc/shadow > output_errors.txt 2>&1`
      
      #### piping and redirection
      - `cat -n /var/log/auth.log | grep -ai "authentication failure" | wc -l`
      - `cat -n /var/log/auth.log | grep -ai "authentication failure" > auth.txt`


### Searching for text patterns (grep):
  grep [OPTIONS] pattern file:
  
  Options:
  `-n`          # => print line number
  `-i`          # => case insensitive
  `-v`         # inverse the match
  `-w`          # search for whole words
  `-a`          # search in binary files
  `-R`          # search in directory recursively
  `-c`          # display only the no. of matches
  `-C n`        # display a context (n lines before and after the match)
  
  # printing ASCII chars from a binary file
  - `strings binary_file`


### VIM
Modes of operation: Command, Insert, and Last Line Modes.
VIM Config File: ~/.vimrc

#### Entering the Insert Mode from the Command Mode
  - `i`  => insert before the cursor
  - `I`  => insert at the beginning of the line
  - `a`  => insert after the cursor
  - `A`  => insert at the end of the line
  - `o`  => insert on the next line

#### Entering the Last Line Mode from the Command Mode
  - `:`
#### Returning to Command Mode from Insert or Last Line Mode 
  - `ESC`
#### Shortcuts in Last Line Mode
  - `w!`  => write/save the file
  - `q!`  => quit the file without saving
  - `wq!` => save/write and quit
  - `e!`  => undo to the last saved version of the file
  - `set nu` => set line numbers
  - `set nonu`  => unset line numbers
  - `syntax on|off`
  - `%s/search_string/replace_string/g`

#### Shortcuts in Command Mode
  - `x`   => remove char under the cursor
  - `dd`  => cut the current line
  - `5dd` => cut 5 lines
  - `ZZ`  => save and quit
  - `u`   => undo
  - `G`   => move to the end of file
  - `$`   => move to the end of line
  - `0` or `^`  => move to the beginning of file
  - `:n` (Ex :10) => move to line n
  - `Shift+v`     => select the current line
  - `y`           => yank/copy to clipboard
  - `p`           => paste after the cursor
  - `P`           => paste before the cursor
  - `/string`     => search for string forward
  - `?string `    => search for string backward
  - `n`           => next occurrence
  - `N`           => previous occurrence
  
  # Opening more files in stacked windows
    - `vim -o file1 file2`
  
  # Opening more files and highlighting the differences
    - `vim -d file1 file2`
    - `Ctrl+w` => move between files


### The Inode Structure:
- Each file on the disk has a data structure called `index node` or `inode` associated with it. The inode contains information such as the file name, permissions, size, etc.
- It actually contains all file information except the file contents and the name.
- Each `inode` is uniquely identifiable by an integer number called `inode number`(`ls -i`)