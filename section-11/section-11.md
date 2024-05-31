# Linux Administration: The Complete Linux Bootcamp For 2024
### Date: 5/29/2024

## Section 11 - Linux Process Managment

### Processes & The Linux Security Model:
  * See [PDF](.resources/linux-process-management.pdf) for more details.
  
  - Not all commands in Linux result in a dedicated process. There are two types of commands in Linux, commands that are executable files on the hard disk and commands that are shell built-ins.
  - The `type` command can be used to determine which of the two types of commands is being used.
    - `type rm` -> `rm is /usr/bin/rm`
    - `type cd` -> `cd is a shell builtin`
  - Only when running a command that is an executable file is a new process created, unlike when a shell built-in command is used in which case no new process is created.
  - Each process has: 
    - A process ID (PID) and *possibly* a parent process ID (PPID). The PPID is the PID of the parent process.
    - A User
    - A Group
    - Priority/Nice
  - The OS maintains a table that associates every process to the data necessary for it's execution.
  - When a process terminates it's execution the OS releases most of the resources and information associated with it.
    - A terminated process whose data has not been collected is called a zombie process.
  
  ### Whats The Difference Between A Process and A Thread?
    - Threads are processes that run in parallel with the OS. They are created when a process is created, and are terminated when the process terminates.
    - Multiple threads can exist in the same process and share the same resources.
    - Can be thought of as "sub processes" that run in the same memory context(process) and share the same resources.
    - "Task" is often a synonym for "process".
  
  ### Process Viewing Commands (ps, pstree, pgrep)
    #### Checking if a command is shell built-in or executable file
    - `type rm`        # => rm is /usr/bin/rm
    - `type cd`        # => cd is a shell built-in
    
    #### Displaying all processes started in the current terminal
      - `ps`
    
    #### Displaying all processes running in the system
      - `ps -ef` 
      - `ps aux`
      - `ps aux | less`       # => piping to less
    
    #### sorting by memory and piping to less
      - `ps aux --sort=%mem | less`
    
    #### ASCII art process tree
      - `ps -ef --forest`
    
    #### Displaying all processes of a specific user
      - `ps -f -u username`
    
    #### Checking if a process called sshd is running
      - `pgrep -l sshd`
      - `ps -ef | grep sshd`
    
    #### Displaying a hierarchical tree structure of all running processes
      - `pstree`
    
    #### Prevent merging identical branches
      - `pstree -c`
  
  ### Getting a Dynaic Real-Time View of the Running System (top, htop):
    - `top` returns a dynamic real-time view of the running system:
      - Updates every 3 seconds by default.
      - There are two areas of the output, (1) summary & (2) task/process table
      - `summary`:
        - Intuitive display of system resources
        - `top` - Displays the total time of the running system, total logged in users, avg load, etc.
        - `Tasks` - Displays the total number of tasks/processes and their states(running, sleeping, stopped, zombie)
        - `%Cpu(s)` - Displays the CPU usage based on the interval of last refresh
  
  ### Commands - top:
    #### starting top
      - `top`
    
    #### top shortcuts while it's running:
      - `h`       # => getting help
      - `space`   # => manual refresh
      - `d`       # => setting the refresh delay in seconds
      - `q`       # => quitting top
      - `u`       # => display processes of a user
      - `m`       # => changing the display for the memory
      - `1`       # => individual statistics for each CPU
      - `x/y`     # => highlighting the running process and the sorting column
      - `b`       # => toggle between bold and text highlighting
      - `<`       # => move the sorting column to the left
      - `>`       # => move the sorting column to the right
      - `F`       # => entering the Field Management screen 
      - `W`       # => saving top settings
    
    #### running top in batch mode (3 refreshes, 1 second delay)
      - `top -d 1 -n 3 -b > top_processes.txt`
  
  # Interactive process viewer (top alternative)
    - `sudo apt update && sudo apt install htop`    # => Installing htop
    - `htop`
  
  ### Signals and Killing Processes (kill, pkill, killall, pidof):
    - The `kill` command is most commonly used to kill a process.
    - It sends a signal to the process that defaults to `SIGTERM`.
    - There are many different signals that can be sent with the `kill` command, and they can be listed with `kill -l`.
    - A `signal` is an asynchronous signal that can be sent to a process.
    - To target a process, you must first determine the `PID` of the process.
      - A quick way to filters the list of running processes is to use the `pidof` command.
        - `pidof -s chrome` #=> returns all PID(s) that match the string "chrome"
    - To signal multuple process IDs as a group, use the `kill` command and pass the all capital letters of the signal or the number of the signal.
      - `kill -INT 15029 14977 16489 65989` or `kill -2 15029 14977 16489 65989`
  
  ### Foreground & Background Processes:
    - By default any process that is started from the terminal is run in the foreground.
    - To run a process in the background, use the `&` operator at the end of the command.
    - When starting a process in the background, it can be identified by a job ID.
    - When seeing a display of all processes in the background, use the job ID is usually in the bracket and the process ID is to the right of the bracket.
      - `sleep 20 &` -> `[1] 15766`
  
  ### Job Control:
    - The `jobs` command is used to display all the jobs that are currently running.
    - You can bring a background process to the foreground using the `fg` command.
    - You can push any foreground process to the background using the `bg` command.
    - A shortcut to kill a background process is the `Ctrl + Z` keys.
  
  ### Process Management Commands:
    #### Killing processes (kill, pkill, killall)
      ##### Listing all signals
      - `kill -l`
      
      ##### Sending a signal (default SIGTERM - 15) to a process by pid 
      - `kill pid`        # => Ex: - kill 12547
      
      ##### Sending a signal to more processes
      - `kill -SIGNAL pid1 pid2 pid3`
      
      ##### Sending a specific signal (SIGHUP - 1) to a process by pid
      - `kill -1 pid`
      - `kill -HUP pid`
      - `kill -SIGHUP pid`
      
      ##### Sending a signal (default SIGTERM - 15) to process by process name
      - `pkill process_name`          # => Ex: pkill sleep
      - `killall process_name`
      - `kill $(pidof process_name)`  # => Ex: kill -HUP $(pidof sshd)
      
      ##### Running a process in the background
      - `command &`   # => Ex: sleep 100 &
      
      ##### Showing running jobs
      - `jobs`
      
      ##### Stopping (pausing) the running process
      -` Ctrl + Z`
      
      ##### Resuming and bringing to the foreground a process by job_d
      - `fg %job_id`
      
      ##### Resuming in the background a process by job_d
      - `bg %job_id`
      
      ##### starting a process immune to SIGHUP
      - `nohup command` &     # => Ex: nohup wget http://site.com &