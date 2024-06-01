# Linux Administration: The Complete Linux Bootcamp For 2024
### Date: 5/29/2024

## Section 10: Challenges - File Permissions
How to solve these challenges:
  - To be consistent with the filenames and paths run the commands on Ubuntu
  - Write your solution in a terminal and test it.
  - If your solution is not correct, then try to understand the error messages, watch the video again, rewrite the solution, and test it again. Repeat this step until you get the correct solution.
  - Save the solution in a file for future reference or recap.



- Create a directory with a regular file in it. Work as a non-privileged user.


#### Challenge #1
- Display the permissions of ubuntu.txt
- Remove all permissions of others.


#### Challenge #2
- Remove the read permission of ubuntu.txt for the owner and check if the owner can read the file.


#### Challenge #3
- Using the octal notation, set the permissions of the directory to rwxrwx--- and of the file to rw-r-----


#### Challenge #4
- Set the permissions of the directory to 0667. Check if the user (owner) can list its contents, move to the directory and remove it.


#### Challenge #5
- Set the permissions of all the files in the user's home directory to 0640 and the permissions of all directories to 0750.


#### Challenge #6
- As a non-privileged user list the contents of /root using the ls command. See what will happen.
- As root set SUID to ls and list the contents of /root again as a non-privileged user.
- Check the SUID permission set on ls
- As root remove the SUID bit.


#### Challenge #7
- Set the directory permissions to 0777 and the file permissions to 0000. As another non-privileged user, try to remove the file.
- Create a new file in the directory and set its permissions to 0644.
- Set the Sticky Bit on the directory.
- As another non-privileged user, try to remove the file.


#### Challenge #8
- Change the owner and the group owner of all files in the current user home directory to the current user and its primary group.