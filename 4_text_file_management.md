## `cat`

`cat [file path]`

- returns content of the file to the terminal

```shell
cat ./romeo.txt
```

## `head`

`head [options] [file_path]`

- if no options is given, first 10 lines of the file will be return
- `-n 15` : by `-n` option we can pass how many lines we want to see. `-n 15` option will retrun first 15 lines

```shell
head -n 15 ./romeo.txt
```

## `tail`

`tail [options] [file_path]`

- if no options is given, last 10 lines of the file will be return
- `-n 15` : by `-n` option we can pass how many lines we want to see. `-n 15` option will retrun last 15 lines

```shell
tail -n 15 ./romeo.txt
```

## `less`

`less ./romeo.txt`

- allows to read large files
- `arrow key` to navigate through lines
- `f` : key to next page
- `b` : key to previous page
- `50p` : to jump to 50%, we can use other parcentages
- `=` : to know the current position
- `-N` : show row numbers
- `/search_word` : search for the word in the forward direction
- `?search_word` : search for the word in the backward direction
- `q` : to quite

## `wc` : word count

`wc [options] [file path]`

- returns:
  - number of lines (-l)
  - number of words (-w)
  - number of bytes (-c)
- if we do not pass any option, wc will return number of lines, words and bytes in order.

```shell
wc ./romeo.txt
wc -l ./romeo.txt
wc -lwc ./romeo.txt
```

## `du` : disk usage

`du [options] [file/dir path]`

- returns size of the file or dir
- `-h` : display size in human readable formate
- if we do not pass any path ot file/dir, du will return size for current dir as well as all the child dir and files.

```shell
du -h
du -h ./romeo.txt
```

## nano : text editor

`nano [file path]`

- file will be open in nano text editor
