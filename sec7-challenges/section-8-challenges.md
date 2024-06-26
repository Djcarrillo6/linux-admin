# Linux Administration: The Complete Linux Bootcamp For 2024
### Date: 5/29/2024

## Section 8 - User Account Management Exercises

### Challenges - User Account Management


### How to solve these challenges:
  - To be consistent with the filenames and paths run the commands on Ubuntu
  - Write your solution in a terminal and test it.
  - If your solution is not correct, then try to understand the error messages, watch the video again, rewrite the solution, and test it again. Repeat this step until you get the correct solution.
  - Save the solution in a file for future reference or recap.
  
  #### Challenge #1
    - Create a new user using the useradd command with no other options. Check if the home directory of the user was created as well.
    - Set a password for the user.
    - Log in as the new user (in a terminal or GUI).
  
  #### Challenge #2
    - Create a new user using the useradd specifying the following: the home directory (which will be created as well), the Bash shell, and a comment.
    - Set a password for the user.
    - Create a new group using the groupadd command and then add the user to the newly created group.
    - Check the groups to which the user belongs.
  
  #### Challenge #3
    - Try to execute a command as root (like say sudo cat /etc/shadow or sudo ls -l /root). Run the command as the user you created at the previous challenge. Notice what will happen.
    - Make this user an admin one and rerun the command as root.
  
  #### Challenge #4
    - Create 2 new groups and add the user from the previous challenge to those groups without taking it out of the groups it already belongs to.
  
  #### Challenge #5
    - Remove the groups and the users (including their home directory) created in the previous challenges.
  
  #### Challenge #6
    - Understand the concept of salt used in Linux passwords. Create 2 new users and set the same password for both of them. Check that the save password in /etc/shadow is different for each user.