# Linux Administration: The Complete Linux Bootcamp For 2024
### Date: 5/31/2024

## Section 17: System Administration

### Task Automation & Scheduling with Cron:
  - Cron runs as a daemon process and is used to automate repetitive tasks.
  - The files that contains the jobs for a given user is called the `crontab` file.
  - In Ubuntu, the `crontab` file is located in `/var/spool/cron/crontabs`.
    - *The exact location of these files is Linux distro specific.*
  - `crontab` is a command used to manage the cron files and depending on the context of either user or system, the file can be located at:
    - User: `/usr/bin/crontab`
    - System: `/etc/crontab`
  
  #### User Cron Jobs
    - Each user has their own `crontab` file which contains a cron table that is used by the Linux system to manage schedule jobs.
  
  ### Cron Commands:
    ## Task Scheduling using `cron`
      ##### editing the current user’s crontab file 
      - crontab -e
      
      ##### listing the current user’s crontab file 
      - crontab -l
      
      ##### removing the current user’s crontab file 
      - crontab -r
      
      ## COMMON EXAMPLES ##
      ##### run every minute
      `* * * * * /path_to_task_to_run.sh`
      
      ##### run every hour at minute 15
      `15 * * * * /path_to_task_to_run.sh`
      
      ##### run every day at 6:30 PM
      `30 18 * * * /path_to_task_to_run.sh`
      
      ##### run every Monday at 10:03 PM
      `3 22 * * 1 /path_to_task_to_run.sh`
      
      ##### run on the 1st of every Month at 6:10 AM
      `10 6 1 * * /path_to_task_to_run.sh`
      
      ##### run every hour at minute 1, 20 and 35
      `1,20,35 * * * * /path_to_task_to_run.sh`
      
      ##### run every two hour at minute 10
      `10 */2 * * * /path_to_task_to_run.sh`
      
      ##### run once a year on the 1st of January at midnight
      `@yearly /path_to_task_to_run.sh`
      
      ##### run once a month at midnight on the first day of the month
      `@monthly /path_to_task_to_run.sh`
      
      ##### run once a week at midnight on Sunday
      `@weekly  /path_to_task_to_run.sh`
      
      ##### once an hour at the beginning of the hour
      `@hourly /path_to_task_to_run.sh`
      
      ##### run at boot time
      `@reboot /path_to_task_to_run.sh`
      
      All scripts in following directories will run as root at that interval:
      - /etc/cron.hourly
      - /etc/cron.daily  
      - /etc/cron.hourly  
      - /etc/cron.monthly
      - /etc/cron.weekly
  
  ### Anacron Commands:
    - Unlike `cron`, `anacron` does not expect the system to be online 24/7 but rather for windows that more align with desktop operating systems.
    - `anacron` is not a daemon process and it is not supposed to be run as root.
  
  
  ### Getting System Hardware Information:
    - The `lwhw` command is used to get system hardware information.
    - The `lscpu` command is used to get CPU information.
    - The `lspci` command is used to get PCI information.
    - The `dmidecode` command is used to get device information.
    - The `hdparam` command is used to get disk information.
    
    ### Commands:
      ##### Displaying full hardware information
      - `lshw`
      - `lshw -short`     // => short format
      - l`shw -json`      // => json format
      - `lshw -html`      // => html format
      - `inxi -Fx`
      
      ##### Displaying info about the CPU
        - `lscpu`
        - `lshw -C cpu`
        - `lscpu -J`  // => json format
      
      ##### Displaying info about the installed RAM memory
        - `dmidecode -t memory` 
        - `dmidecode -t memory | grep -i size`
        - `dmidecode -t memory | grep -i max`
      
      ##### Displaying info about free/used memory
        - `free -m`
      
      ##### Getting info about pci buses and about the devices connected to them
        - `lspci`
        - `lspci | grep -i wireless`
        - `lspci | grep -i vga`
      
      ##### Getting info about USB controllers and about devices connected
        - `lsusb`
        - `lsusb -v`
      
      ##### Getting info about hard disks
        - `lshw -short -C disk`
        - `fdisk -l`
        - `fdisk -l /dev/sda`
        - `lsblk`
        - `hdparm -i /dev/sda`
        - `hdparm -I /dev/sda`
      
      ##### Benchmarking disk read performance
        - `hdparm -tT --direct /dev/sda`
      
      ##### Getting info about WiFi cards and networks
        - `lshw -C network`
        - `iw list`
        - `iwconfig`
        - `iwlist wlo1 scan`
      
      ##### Getting hardware information from the /proc virtual fs
        - `cat /proc/cpuinfo`
        - `/proc/partitions`
        - `cat /proc/meminfo`
        - `cat /proc/version`
        - `uname -r`    // => kernel version
        - `uname -a`
        
        - `acpi -bi`    # battery information
        - `acpi -V`
      
      #### Working directly with device files (dd)
        ##### Backing up the MBR (the first sector of /dev/sda)
        - `dd if=/dev/sda of=~/mbr.dat bs=512 count=1`
        
        ##### Restoring the MBR
        - `dd if=~/mbr.dat of=/dev/sda bs=512 count=1`
        
        ##### Cloning a partition (sda1 to sdb2)
        - `dd if=/dev/sda1 of=/dev/sdb2 bs=4M status=progress`
  
  
  ### Systemd:
    - The name comes from System Management Daemon, and it is a Linux initialization system & service manager with many components such as on demand service, logging, boot mamanagement, timer, etc.
    - Systemd is the Ubuntu initialization system during the boot and startup process.
    - The Linux boot process has the following phases:
      1. The system powers up
      2. The boot loader loads the kernel
      3. The kernel loads the initial RAM disk
      4. The initial RAM disk loads the system drives and looks for the root file system
      5. Once the kernel is setup, it begin the systemd initialization process
         1. The systemd daemon is started with PID 1, then takes over to mount the host file systems & start servicecs
    - Unlike it's predesessor `init` system, `systemd` can run processes in parallel.
    - When running `ps -ef | less`, `systemd` will show as `init` for backward compatibility.
   
   #### Service Management (systemd, systemctl):
    - The `systemctl` command is used to manage services.
  
  #### Commands:
    ## Service Management using systemd and systemctl
      ##### Showing info about the boot process
      - `systemd-analyze`
      - `systemd-analyze blame`
      
      ##### Listing all active units systemd knows about
      - `systemctl list-units`
      - `systemctl list-units | grep ssh`
      
      ##### Checking the status of a service
      - `sudo systemctl status nginx.service`
      
      ##### Stopping a service
      - `sudo systemctl stop nginx`
      
      ##### Starting a service
      - `sudo systemctl start nginx`
      
      ##### Restarting a service
      - `sudo systemctl restart nginx`
      
      ##### Reloading the configuration of a service
      - `sudo systemctl reload nginx`
      - `sudo systemctl reload-or-restart nginx`
      
      ##### Enabling to start at boot time
      - `sudo systemctl enable nginx`
      
      ##### Disabling at boot time
      - `sudo systemctl disable nginx`
      
      ##### Checking if it starts automatically at boot time
      - `sudo systemctl is-enabled nginx`
      
      ##### masking a service (stopping and disabling it)
      - `sudo systemctl mask nginx`
      
      ##### Unmasking a service
      - `sudo systemctl unmask nginx`