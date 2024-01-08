## Writting output to a file

## `>` : redirection operator

`[out put] > [file path]`

- output will be over written into the file, any prvious info will be removed

```shell
echo 'Hello from terminal!' > ./hello.txt
ls -lah > ./ls.txt
```

## `>>` : redirection operator with append

`[out put] >> [file path]`

- output will be written at the end of the file, any prvious info will not deleted, rather added after the privious info.

```shell
echo 'Hello again from terminal!' >> ./hello.txt

```

## Standard streams

- by default, there are 3 communication channels for data:
  - `0` : standard input (from the keyboard): stdin
  - `1` : standard output (on the screeen): stdout
  - `2` : standard error output (on the screen): stderr

## `< or <<` : redirecting stdin

```shell
wc -l < out.txt
```

- here `stdin` of the out.txt file is redirected to `wc -l` command
- we can redirect the output of `wc -l` command into another file. eg

```shell
wc -l < out.txt >> out_1.txt
```

## `1> or 1>>` : redirecting stdout

it's adjuctly same as `> or >>`

## `2> or 2>>` : redirecting stderr

`[error output] 2> [file path]`

```shell
ls --lsfslkfj 2> ./error.txt
```

- redirect the error message into error.txt file

```shell
ls --lsfslkfj 2> /dev/null
```

- redirection error message to `/dev/null`, means the error will not appears in the terminal and System will remove the error message periodically.

## `> [output file] 2>&1` : redirecting stdout and stderr into same file

`[out put] > [output file path] 2>&1`

- out put will be redirected to same file
- `2>&1` : converting into `stderr` to `stdout`, so, technically what is written in files are all stdout
- order of potions is important, because first stdout redirects into file, then stderr converted into stdout redirectes into the same file, if `2>&1 is given first` and destination file does not exists yet, this will not work.

```shell
ls -lh ./ ./doesnotexist > out.txt 2>&1
```

## `>> [output file] 2>&1` : redirecting and appending stdout and stderr into same file

`[out put] >> [output file path] 2>&1`

- out put will be redirected and appended to same file
- `2>&1` : converting into `stderr` to `stdout`, so, technically what is written in files are all stdout
- order of potions is important, because first stdout redirects into file, then stderr converted into stdout redirectes into the same file, if `2>&1 is given first` and destination file does not exists yet, this will not work.

```shell
ls -lh ./ ./doesnotexist >> out.txt 2>&1
```
