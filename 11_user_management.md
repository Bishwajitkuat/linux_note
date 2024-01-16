There are several kind of users in linux system

## Root user

- has heighest priveleges
- it has user ID: 0
- there can only be one root user per system

## Regualar users

- has limited previleges
- regular users can get temporary acces to root user through `sudo` command

## Service users

- has previlege for specific tasks
- this allows us to safely ren a webserver, database etc.

## Groups

- all users have a primary group
- each user can be assigned to zero to many additional groups

## `/etc/passwd`

- contains basic user account info such as
  - username
  - groupname
  - user ID (UID)
  - group ID (GID)
  - user description : it's optional, all uer might not have it
  - home directory
  - default shell

![user management](resources/imgs/user_mng1.png)

## `/etc/shadow`

- it stores encrypted user passwords and passwod againg info
- it also stores additional info such as date of last password changes, expiry datest etc.
- readable only by root users or with `sudo` privilege

## `/etc/group`

- contains info about the groups and their members
- readable by all users

![user management](resources/imgs/user_mng2.png)

## `useradd`

- we can add user with `useradd` command
  syntax

`useradd [options] [user name]`

options

- `-m` : create home directory, regular user might need a home dir, service user will not need on
- `-d` : to set custom home directory
- `-s` : to specify default shell, by defaul bash is default shell
- `-g` : by default a new group will be created with the same name as the username. with `-g` options we can specify primary group name for the user.
- `-G` : to add user to a secondary groups

![user management](resources/imgs/user_mng4.png)
a user is created with `test_user` name and home directory and existance of home dir, defauls CLI, groups tested

## `passwd`

- we can add or update password of current user. We can change other user's password if the current user have privileges

syntax

`passwd [options] [user name]`

options

- `-S` : Display password status
- `-d` : Delete password
- `-n` : set minimum password age in days
- `-x` : set maximum password age in days
- `-l` : to lock user account
- `-u` : to unlock user account

![user management](resources/imgs/user_mng3.png)

- `test_user`'s password status is checked and it is locked (L)
- setting password for test_user with sudo privilege
- checking password staus again, now it is active
- log in as test_user

## `usermod`

- with the usermod command, we can modify another user's details

syntax

`usermod [options] [user name]`

options

- `-c` : to change user description (eg. full name)
- `-s` : to change default shell
- `-d` : to change home directory, installed software might not work
- `-l` : to change username
- `-g` : to change primary group
- `-G` : to change secondary group
- `-aG` : to add secondary group

![user management](resources/imgs/user_mng5.png)

- test_user's description added and default shell has been changed
- test_user is added to sudo secondary group

## `userdel`

- we can also delete an existing user

syntax

`userdel [option] [user name]`

options

- `-r` : to remove the home directory and mails
- `-f` : force remove of home dir and mails even if the user is logged in

![user management](resources/imgs/user_mng_userdel1.png)

- user, user group and home directory is being deleted

## Groups in linux

- helps to organize users with similar access rights
- simplify permission management
- enhance collaboration and resource sharing
- controlling access to files and directories
- strengthen system security
- each user has a primary, and zero to many secondary groups
  - ### Primary group
    - stored in `/etc/passwd` file
    - default ownership for newly created files
  - ### Secondary group
    - multiple memberships are llowed in secondary group
    - stored in `/etc/group`
    - this allows us to give this user fine grained access rights to our system

## `groups`

- to see all the existing groups

syntax

`groups [user name]`

- if we do not pass any user name, then all grous of current user will be returns
- we can pass multiple user name as arguments

### Some importang froups in linux systems

- `root` : the superuser group with administrative privileges which have complete control over the system
- `sudo` : members can use sudo (administrative privileges) temporarily
- `adm` : allows members to read log files
- `lp` : members may manage printers and print queues
- `www-data` : users have access to web server processes and gives access to web content
- `plugdev` : allows this user to manage pluggable devices (eg, usb sticks, external HDD etc)

## `usermod` : we can use this command also to modify or to add user group

`usermod [options] [user name]`

- `-g` : to change primary group
- `-G` : to change secondary group
- `-aG` : to add secondary group

```shell
groups
sudo usermod -aG adm,www-data,lp bisso
groups bisso
```

![user management](resources/imgs/user_mng_usermod1.png)

## `adduser` : to add a user to a group

`adduser [user name] [group name]`

## `deluser` : to remove a user from a group

`deluser [user name] [group name]`

```shell
sudo adduser bisso plugdev
# adding bisso to plugdev
groups bisso
# checking whether the  group is added
sudo deluser bisso plugdev
# removing bisso from plugdev
groups bisso
# checking whether the group is removed
```

![user management](resources/imgs/user_mng_add_del_user1.png)

## `groupadd` : to create a custom group

`groupadd [options] [group name]`

- `-g` : to set a custom GID, but the GID has to be unique (not in use)

## `groupmod` : to modify a group

`groupmod [options] [group name]`

- `-n` : change group name
- `-g` : change GID

![user management](resources/imgs/user_mng_groupmod1.png)

## `groupdel` : to delete a group

`groupdel [group name]`

- however it can not delete any primary group
- primary group is essential for the user, so it can not be deleted withou deleting the user

## `su` : switch user

- to switch user
- if we do not

`su [user name]`

```shell
su root
# if we do not pass any username, it will be switch to root user
su
```

## `sudo` : superuser do

`sudo [options] [command]`

- `-k` : by default, terminal remember passwords for 15 min, -k option forget it
- `-s` : starts new shell with elevated privilege
- `-u [user name]` : to do something on behave of the other user without their password. eg. sudo -u das -s will run a CLI for das user.
- it gives temporary root privileges to other users.
- the user needed to be in sudo grop inoder to use sudo command

## `visudo`

- if we want to edit any sensative file in linux system we should use visudo command
- `visudo` will create a temporary file when we are editing
- if we made any mistack, we will have chance to correct it, because it will shows the syntax errors when we save out the file
-

```shell
sudo visudo /etc/sudoer
```

## `/etc/sudoers`

- contains a configaration for sudo users
- privileges for root user in `/etc/sudoers` file
- ` root    ALL=(ALL:ALL) ALL`

  - `root` : indicates user name, in this case it's root
  - `ALL` : indicates host name (machine name)
  - `(ALL:ALL)`
    - first `ALL` : the users to which this user sudo into, here, root user can sudo into all user
    - second `ALL` : the groups to which this user sudo into, here, root user can sudo into all groups
  - last `ALL` : it allows to run any command as root

- privileges for sudo group in `/etc/sudoers` file
- `%sudo   ALL=(ALL:ALL) ALL`

  - it same as root user but, group name is indicated by `%`. If there is `%` sign before a name, it indicates that it is a group

- at the end of the file the is : `@includedir /etc/sudoers.d`, means any file inside this directory will be imported to this fiel
- so if we want add our custom configaration, it is best practive to create a file inside this dir and add configaration into it.

```shell
sudo touch /etc/sudoers.d/das
sudo visudo /etc/sudoers.d/das
# adding the following content to the file
das ALL= /usr/bin/apt
# clt+o and clt+x to save and out
su das
# das as a sudo user only have acces to apt command, it do not have access to other command which needs sudo privilege
```

![user management](resources/imgs/user_mng_sudoers1.png)
