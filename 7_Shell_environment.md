# Shell environment

- The shell environment is a collection of settings, variables, aliases, and configurations
- It defines the context in which our programs are run

## Shell

- Outer layer of the operating system
- It takes commands from the user and translates them into a form that the kernel can understand
- It can also display the result of those commands to the user
- in general, everything that allows the outer world to access the operating system
- The graphical user interface is also a shell

However,

- Often, shell refers to the command line interface (CLI) of an operaing system.

## CLI

- A text-based interface that allows users to interact with systems by typing commands
- Linux shell refers to the CLI/terminal/console

## Environment variables

- the variables used to store configuration information and settings
- they influence the shell and program behavior
- The convention, env variables are written in uppercase letters
- Envs are not a Bash feature
- Env feature is provided by the operating system, so these variable are accessable by all programs
- Envs are automatically available for all programs that we lunch
- Envs are often used to pass configuration data to programs
- If you run your own application, you might also consider passing in the configuration as envs.

## `evn`

- returns all the environment variables.

```shell
env
```

## get a single env

`echo "${variable name}"`
or
`echo "$variable_name"`

```shell
echo "${PATH}"
echo "${USER}"
```

## HOME

- returns home directory of the current user.

```shell
echo "${HOME}"
```

## PWD

- returns current working directory

```shell
echo "${PWD}"
```

## OLDPWD

- last working directory befor the current one

```shell
echo "${OLDPWD}"
#or
cd "${OLDPWD}"
```

## USER

- returns user name

```shell
echo "${USER}"
```

## `export` : command to create or update envs

`export [VAR_NAME]='value preferably inside single quote'`

```shell
export HOME_COUNTRY='Finland'
echo "${HOME_COUNTRY}"
#output
Finland
# updating the last env
export HOME_COUNTRY='Bangladesh'
echo "${HOME_COUNTRY}"
#output
Bangladesh
```

## `unset` : command to remove envs

`unset [VAR_NAME]`

```shell
unset HOME_COUNTRY
echo "${HOME_COUNTRY}"
```

## PATH§

- The env var PATH is one of the most important variables in our shell
- stores a list of directores and each directory contains executable commands or programs such as echo, ls pwd etc.
- multiple directories separated by colons(`:`)
- for multiple directories PATH, order matters because directories are searched from left to right

## why do we need multiple paths

- Filesystem Hierarchy Standard: Unified standard of where to place files
- Single-user mode: A special way to lunch Linux for repairing a broken system

## Different paths:

- `/bin` : Essentail binaries, that need to be always available
- `/sbin` : Essentail binaries, that are usually executed as root, and need to be always available
- `/usr/bin` : Non-essential binaries, for all users. Could be shared with other computers
- `/usr/sbin` : Non-essential biraries, usually executed as root. Could be shared with other computers.
- `/usr/local/bin`: Specific to this host.Non-essential binaries.
- `/usr/local/sbin`: Specific to this host. Non-essential binaries, usually executed as root.

## Modifying PATH variable

- Sometimes, we want to modify the PATH variable because
  - we have a separate directory in which we want to install executable files on our system

## Appending new path

```shell
PATH="${PATH}:/new/path"
```

- new path will be append to the existing path

## `which` : to get the path of the command or program

`which [command or program]`

```shell
which ls
# output: /usr/bin/ls
which echo
# output: /usr/bin/echo
which cat
# output: /usr/bin/cat
which docker
# output: /usr/local/bin/docker
```

### Best practices regarding PATH

- Keeping system dirs at the beginning
- Place user-specific dirs after system dirs
- Avoid unnecessary duplication of dirs
- Minimizing the numbers of dirs to improve search efficiency
- Regularly review and clean up the PATH

## Creating a program called "my_program"

- adding the dir which containes the binary to the PATH

```shell
PATH="${PATH}:/media/bisso/Documents/linux_command_notes/exercises/bin"
```

- creating the binary file and make it executable

```shell
touch my_program
chmod +x my_program
```

- adding content to the binary file

- `#!/usr/bin/env node`
- this line indicates that load node from /usr/bin/env and execute the following lines with node
- this line must be the first line
- `console.log("Hello from my program");`

- execute the program

```shell
my_program
```

example how to pass value of a ENV during running `my_program`

adding the ENV :

```shell
export MESSAGE='Hello! How are you doing?'
echo "${MESSAGE}"
# output: Hello! How are you doing?
```

adding the following line to `my_program`

`console.log(process.env.MESSAGE)`

executing the program

```shell
my_program
# output:
# Hello! How are you doing?
# Hello from my program
```

Passing custom `MESSAGE` value during calling the program

```shell
MESSAGE='Good morning!' my_program
# the program used the custom MESSAGE ENV instead of system provided one
# output:
# Good morning!
# Hello from my program
```

## `chsh` : change shell

`chsh -s "[shell path]"`

we can see all availabel sehll from `/etc/shells`

```shell
cat /etc/shells
```

see my current bash

```shell
echo "${SHELL}"
# output: /bin/bash
```

change my shell to `sh`

```shell
chsh -s "/bin/sh"
echo "${SHELL}"
# output after log out and log back
# /bin/sh
```

## Storing custom shell configarations

There are several options where can we save the configarations.

#### For interactive login shell

- ~/.bash_profile
- ~/.bash_login
- ~/.profile

#### For interactive non-login shell

- ~/.bashrc

## Interactive login shell

- we directl log into a computer for example tty-terminal on our machine or ssh from remote
- we need to log in to work in the system

## Interactive non-login shell

- The terminal on our desktop environment or the bash withing an existing terminal
- we do not need to login to used it

## Non-interactive non-login shell

- we run a .sh-script for example
- `bash script.sh` or
- `./script.sh`

## Non-interactive login shell

- very rare. One way would be, if we send a command with ssh to a remote server without starting a shell.
- `echo command | ssh server`

## Adding a env in .bashrc

- adding MY_SECRETE

```shell
nano ~/.bashrc
# adding env into the file
export MY_SECRETE='secrete'
echo "${MY_SECRETE}"
# output: secrete
```

- adding PATH for ./exercises/bin so that i can run my_program

```shell
nano ~/.bashrc
# adding the following line at the end
PATH="${PATH}:/media/bisso/Documents/linux_command_notes/exercises/bin"
# open a new CLI
echo "${PATH}"
# output: /usr/local/bin:/usr/bin:/bin:/usr/local/games:/usr/games:/media/bisso/Documents/linux_command_notes/exercises/bin
# now I can run my_program from any directory and any CLI
```

## `alias` : assign a name for a command

- `alias [alisa]='[command']`
- creates new alias, if already existed, overwrite that

```shell
alias gohome='cd ~'
pwd
# output: /media/bisso/Documents/linux_command_notes
gohome
pwd
# output: /home/bisso
```

- `alias`
- list all aliases in use

```shell
alias
# output
# alias gohome='cd ~'
# alias ls='ls --color=auto'
```

- `unalias [alias]`
- remove a alias

```shell
unalias gohome
```

### **_If we want to load the alias each time with new CLI, we need to add these alias to the .bashrc file_**

## `set`

- One way to change the behavior of the shell in the set command
- It provides pre-defined configuration options that we can use
- to enable a feature
- `set -[feature]`
- to disable a feature
- `set +[feature]`
- examples

```shell
set -x
```

- `-x` : xtrace: enables that each command that the shell executes will be printed
- allows better debug commands
- now you can see the detail execution fo all comand
- disable the feature `set +x`

```shell
set -t
```

- `-t`: exits the terminal upon reading and running one command.

## `shopt`

- we can configure the shell behaviour
- to enable a configuration option
- `shopt -s [optname]`
- to disable a configuration option
- `shopt -u [optname]`
- shopt configuratin options are specific to Bash
- examples

```shell
shopt -s autocd
```

- we can now navigate without writing cd , only path is succifient
- to disable `shopt -u autocd`

```shell
shopt -s cdspell
```

- if there is minor miss spelling in dir name, it will still navigate to that dir
