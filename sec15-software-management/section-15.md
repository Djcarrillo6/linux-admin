# Linux Administration: The Complete Linux Bootcamp For 2024
### Date: 5/31/2024

## Section 15: Linux Software Management

## Software Management Commands (dpkg and apt):
  ### DPKG:
  ##### Getting info about a deb file
  - dpkg --info google-chrome-stable_current_amd64.deb
  
  ##### Installing an application from a deb file
  - sudo dpkg -i google-chrome-stable_current_amd64.deb
  
  ##### List all installed programs
  - dpkg --get-selections
  - dpkg-query -l
  
  ##### Filtering the output
  - dpkg-query -l | grep ssh
  
  ##### Listing all files of an installed package
  - dpkg-query -l | grep ssh
  - dpkg -L openssh-server
  
  ##### Finding to which package a file belongs 
  - which ls
  - dpkg -S /bin/ls
      coreutils: /bin/cp
  
  ##### Removing a package
  - sudo dpkg -r google-chrome-stable
  
  ##### Purging a package
  - sudo dpkg -P google-chrome-stable
  
  ### APT:
  #### Updating the package index (doesn't install/uninstall/update any package)
  - sudo apt update
  
  #### Installing or updating a package named apache2
  - sudo apt install apache2
  
  #### Listing all upgradable packages
  - sudo apt list --upgradable
  
  #### Upgrading all applications
  - sudo apt full-upgrade
  - sudo apt full-upgrade -y        # => assume yes to any prompt (useful in scripts)
  
  #### Removing a package
  - sudo apt remove apache2
  
  #### Removing a package and its configurations
  - sudo apt purge apache2
  
  #### Removing dependencies that are not needed anymore
  - sudo apt autoremove
  
  #### Removing the saved deb files from the cache directory (var/cache/apt/archives)
  - sudo apt clean
  
  #### Listing all available packages
  - sudo apt list
  - sudo apt list | wc -l
  
  #### Searching for a package
  - sudo apt list | grep nginx
  
  #### Showing information about a package
  - sudo apt show nginx
  
  #### Listing all installed packages
  - sudo apt list --installed