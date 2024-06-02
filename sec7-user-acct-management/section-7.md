# Linux Administration: The Complete Linux Bootcamp For 2024
### Date: 5/29/2024

## Section 7 - User Account Management
- There are two types of groups that a user can belong to:
  1. `Primary Group`: the id is stored in `etc/passwd` and the group name in `/etc/group`. This group is assigned to the files that are created by the user.
     - A user can only belong to one primary group. 
  2. `Secondary Group`: stored in `etc/group`.
- In Linux, a file is owned by both the user and the group that user belongs to.
- In the following line from `/etc/passwd: student:x:1001:1002::/home/student:/bin/bash`:
  - 1001 is the UID(user ID) and 1002 is the primary GID(group ID).
  - The primary group is `student` and the secondary group is `users`.
  - The `x` is the permission bits.

### Account Management
#### IMPORTANT FILES
##### `/etc/passwd` # => users and info: username:x:uid:gid:comment:home_directory:login_shell
##### `/etc/shadow` # => users' passwords
##### `/etc/group` # => groups

#### Creating a user account
useradd [OPTIONS] username
#### OPTIONS:
##### `-m` => create home directory
##### `-d` directory => specify another home directory
##### `-c` "comment"
##### `-s` shell
##### `-G` => specify the secondary groups (must exist)
##### `-g` => specify the primary group (must exist)
##### `-G` => Adds user to secondary groups

Example:
  - `useradd -m -d /home/john -c "C++ Developer" -s /bin/bash -G sudo,adm,mail john`

##### changing a user account
`usermod [OPTIONS]` username # => uses the same options as useradd

Example:
  - `usermod -aG developers,managers john # => adding the user to two secondary groups`

##### deleting a user account
  - `userdel -r username` # => `-r` removes user's home directory as well

##### creating a group
  - `groupadd group_name`

##### deleting a group
  - `groupdel group_name`

##### displaying all groups
  - `cat /etc/groups`

##### displaying the groups a user belongs to
  - `groups`

#### creating admin users
##### add the user to sudo group in Ubuntu and wheel group in CentOS
  - `usermod -aG sudo john`


#### Monitoring Users
  - `who -H` # => displays logged in users
  - `id` # => displays the current user and its groups
  - `whoami` # => displays EUID

##### listing who’s logged in and what’s their current process.
  - `w`
  - `uptime`

##### printing information about the logins and logouts of the users
  - `last`
  - `last -u username`