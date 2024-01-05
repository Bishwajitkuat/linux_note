## Bash Terminal

```bash
bash
```

- If ther terminal in other shell, it will return into `bash` shell.

```bash
echo "${BASH_VERSION}"
```

- return the current `bash` version
- Note: "" can not be replaced by ''. It has to be "".

## Echo

```bash
echo 'argument as text'
```

- return argument text into the terminal.

`-n` option:

- by default text will returned and a line break is added in the termilan. `-n` option in `echo` will remove the line break.

```bash
echo -n 'argument as text'
```

`-e` option: by default any special charecter in artument text will not regarded as special charecter. We can add `-e` option to `echo` command to read spcial charecter in argument text.

```bash
echo  'I am Bisso\nI live in Finland.'
```

- the text will return in one line. The line break charecter (`\n`) will not be read by `echo`.

```bash
echo -e 'I am Bisso\nI live in Finland.'
```

- because of `-e` option, a line break will be introduced in place of `\n`

## pwd : present working directory

```bash
pwd
```

- returns current working directory.

## cd : change directory

```bash
cd dir_name/absolute_path
```

- takes one argument: either directory name which has to be in current `pwd`, if not, we can pass absolute path of the directory.

```bash
cd /
```

- change directory to `root` directory

```bash
cd ~
```

- change directory to `home` directory

```bash
cd ..
```

- navigate to parent directory.

```bash
cd ../..
```

- navigate to two lavel up

## ls

`ls [options] [path]`

```bash
ls
```

- returns list of files and directories in the current directory.
- we can pass relative or obsolute path of a directory, if we are not in the directory which items want to be listed.

`options:`

- `-a` : list all file and folder including hidden onces.
- `-l` : present the return value in table formate, with detail information.
- `-r` : present the list in reverse order
- `-t` : sort by mofification time, newest first.
- `--color` :

## Absolute paths

- it's start with a "/"
- it's define the complete path to the file from root directory
- if we provide absolute path, current working directory is irrelavent.

## Relative paths

- are being resolved according to our current working directory
- it can be starts with "."

## Multiple Commands with ";"

- we can run multiple commands separated by ";", the commands will be executed one after another.

```bash
echo 'Hello world'; echo 'Hello from bash terminal'
```

```bash
cd /; ls -lah
```

## `--help` option

- `--help` option after a command, returns help page for that command

```bash
ls --help
pwd --help
```

## `man` command

- `man` command takes argument (another command) which help page want to see.

```bash
man ls
man pwd
```
