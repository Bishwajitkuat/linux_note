## User Management

- In linux there are three types of users

### System accounts

- These are responsible for running background tasks on the system, such as webserver, database
- These accounts does not have a home directory

### Regular users

- They have access to their own files and directories
- They cannot perform administrative tasks or access other user's files without permission

### Superuser (root user)

- The root user has unrestricted access to the entire system including files belongs to regular users
- Can install add or remove users, and grant or remove privilege to other users.
- Can change configuration of the system

### `sudo` (super user do)

- Elevating privileges to root user for the current user
- we use `sudo` command before the command

```bash
ls -lah /root
# permission denied for the regular user
sudo ls -lah /root
# this will grant access to /root directory to the regular user
```

### grant `sudo` privilege to regular user

```bash
# changed to root user
su -
# adding using to sudo group
adduser user_name sudo
```

### Package management

- Most linux distributions offer a centralized way to install sowtware
- Package management is slightly different for each distribution
- On Debian based distributions (Ubuntu, debian), the package manager is `apt`

#### `apt`

- `apt` needs `sudo` privilege

```shell
sudo apt update
```

- refresh the list of avialabe packages
- we should run this before running any command with `apt`

```shell
sudo apt upgrade
```

- existing packages will be upgraded which might need to install some additional dependencies.

```shell
sudo apt full-upgrade
# or
sudo apt dist-upgrade
```

- runs a large upgrade of our system
- removes unused packages

```shell
sudo apt autoremove
```

- removes unused packages

```shell
# to install a package
# sudo apt install package_name
sudo apt install cowsay
# to remove a package
# sudo apt remove package_name
sudo apt remove cowsay
```

Another package manage for debian familly is `apt-get` which can be used instead of `apt`. However, `apt-get upgrade` does not install additional packages.

#### `dnf`

- package manager for RHEL related distributions such as CentOS
- commands are here as `root` user

```shell
dnf upgrade
# or
dnf update
```

- update package list and upgrades the system

```shell
dnf install package_name
dnf remove package_name
```

```shell
dnf update
dnf install epel-release
dnf update
# fully enabling all the epel-release packages
crb enable
dnf update
```

- allows additional pacakges to install like cowsay
- `yum` used to be package manager but command still works

### Running `bash` in MacOs

- install home brew in mac.

```shell
brew update
brew install bash
brew upgrade
bash
echo "${BASH_VERSION}"
```
