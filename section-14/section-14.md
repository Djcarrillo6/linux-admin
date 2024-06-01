**Section 14: Challenges - Network Interfaces**
  ## How to solve these challenges:
  - To be consistent with the filenames and paths run the commands on Ubuntu
  - Write your solution in a terminal and test it.
  - If your solution is not correct, then try to understand the error messages, watch the video again, rewrite the solution, and test it again. Repeat this step until you get the correct solution.
  - Save the solution in a file for future reference or recap.
  - Do not solve these challenges on a remote machine to which you are connected with SSH.
  - Run the following commands only on a local machine.
  
  ### Challenge #1
    - List the IP address, the Default Gateway, the Mac Address and the DNS Servers.
    - Use both ifconfig and ip commands.
  
  
  ### Challenge #2
    - Using ifconfig, disable the Ethernet interface.
    - Using ip, enable the Ethernet interface.
    - Check its status both with ifconfig and ip.
  
  
  ### Challenge #3
    - Set a new temporary IP address using both ip and ifconfig.
  
  
  ### Challenge #4
    - Using ifconfig, set a secondary IP address on the Ethernet interface.
  
  
  ### Challenge #5
    - Change the MAC address to a random one.
  
  ## Copying Files Challenges
  ### Challenge #6
    - Start 2 Linux VMs with the network in bridged mode and check that they are reachable using ping.
  
  
  ### Challenge #7
    - Install OpenSSH on one Linux VM, check the service status, and then connect to it using the ssh client from the other Linux VM.
  
  
  ### Challenge #8
    - Secure the SSH Daemon:
    - Change the listening Port to 2266
    - Allow only a single non-privileged user to connect to the SSH server.
    - Disable root login entirely.
  
  
  ### Challenge #9
    - Create a directory and a file in the user’s home directory.
    - Using scp, copy both the file and the directory to the remote Linux VM where the SSH daemon is running.
  
  
  ### Challenge #10
    - Using scp, copy a file from the remote VM where the SSH daemon is running to the local machine, in the current directory.
  
  
  ### Challenge #11
    - Solve the last 2 challenges using rsync instead of scp.