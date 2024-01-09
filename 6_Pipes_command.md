## Pipe "|"

- Pipe is a mechanism that passes the output of one command an input to another command
- Thus, you can chain multiple commands togather and build more complex functionalities

`ysntax`

```shell
[command 1] | [command 2] | [command 3]
```

- output of command 1 will be used as argument for command 2 and output of command 2 will be used as argument for command 3.

```shell
ls -lah | wc -lwc > out.txt; cat out.txt
```

## `tee`

- With the combination of a `pipe` and the `tee` command you can create a stdout and redirect output into a file at the same time
  `systax`
  `[command 1] | tee [options] [file path]`

```shell
ls -lah | tee out.txt
```

- with the `tee` command, the output of `ls` command is rederected to `out.txt` as well as stdout is available in console which can be used as argument for other command. eg

```shell
ls -lah | tee out.txt | wc -lwc
```

- now, output of `ls` is rederected to `out.txt` file and `tee` command passing that output as argument to the `wc` command.
- finally, output of `ls` command is stored in `out.txt` and out put of `wc` command produce the final stdout in the terminal.

- `-a` : by default `tee` overwrite file content, but we can append with `-a` tag

```shell
echo 'Hello from tee command' | tee -a out.txt | wc -lwc; cat out.txt
```

## `sort`

`[command 1] | sort [options]`
`sort [options] [file path]`

- sort the contents in a file or stdin in a alphabetical order
- `-r` : sort in reverse alphabetical order
- `-n` : sort number in accending order
- `-u` : only returns uniq entires
- `-c` : check whether the content in a file are sorted and find unsorted elements
- `-k [column number]` : sort data on the basis of column number (starts from 1 not 0)

```shell
ls | tee out.txt | sort -r
sort -u out.txt
```

- stdout sorted in reverse order

```shell
ls -lah | tee out.txt | sort -k 5
```

- sorted stdout on be basis of column 5 which actually file size.

## `uniq`

`sort [options] [file path] | uniq [options]`

```shell
echo 'Bisso' >> names.txt; echo 'John' >> names.txt; echo 'Bisso' >> names.txt;  echo 'Mike' >> names.txt;echo 'Rokey' >> names.txt; echo 'John' >> names.txt;
```

- remove duplicate entires form stdout
- `uniq` command is always used after sorting because `uniq` only remove duplicate entires if they are placed next to each other. If they are different places uniq can not remove them.
- `-d` : returns only duplicate entries

```shell
sort names.txt | uniq
```

- returns only uniq entries in the stdout

```shell
sort names.txt | uniq -d
```

- returns only duplicate entries

## `grep`

- `grep` is used to filter data by `pattern` from stdin or file

`syntex : source is file`

`grep -F [pattern] [file path]`

```shell
grep -F Bisso names.txt
```

`syntex: source is stdin`

`[comand] | grep -F [pattern]`

```shell
cat names.txt| grep -F Bisso
```

```shell
ip addr show | grep -F 'inet'
```

## `tr` : translate

- translate/change charecter(s) from stdin and returns stdout.

`syntax`

`[command] | tr [options] [current charecter/range] [replacement charecter/range]`

```shell
echo 'Bisso Das' | tr s x
```

- replace all `s` with `x`

```shell
echo 'Bisso Das' | tr a-z A-Z
```

- replace any small letters with capital laters.

- `-d [cahrecter]` : delete the cherecters from stdin

```shell
# deletes all s
echo 'Bisso Das' | tr -d s
# deletes white spaces
echo 'Bisso Das' | tr -d ' '
```

## `rev` : reverse charectes

```shell
echo 'Bisso Das' | rev
```

- return charecters in reverse order.

## `cut` : programe which extract stdin or data from file depending on option and parameter is given

`[comand] | cut [option]`

- `-b [range]` : extract bytes on the baisis of range given

```shell
# retruns first 4 bytes
echo 'Hello!' | cut -b 1-4
# returns 3rd to the last bytes
echo 'Hello!' | cut -b 3-
# returns bytes till 3rd
echo 'Hello!' | cut -b -3
```

- `-c [range]` : extract charecters on the baisis of range given

```shell
# retruns first 4 cherectars
echo 'Hello!' | cut -c 1-4
# returns 3rd to the last cherectars
echo 'Hello!' | cut -c 3-
# returns cherectars till 3rd
echo 'Hello!' | cut -c -3
```

- `-d [delimiter] -f [field or feild range]` : each line in stdin or file will be separated into fields by `delimiter (eg, space, tab, "," ";" etc)`. The filed number or range given into the `-f` options will be filter out into terminal.

```shell
# line is seperated into fields on the basis of a white space, then 2nd field is filtered out
uptime | cut -d ` ` -f 2
# fields are seperated by ',' and first filed is filtered
echo 'Bangladesh,Dhaka' | cut -d ',' -f 1
```

## `sed` : replace, edite charecter,partern or words from stdin or files.

```shell
# 'world' word will be replace with 'bash' world and g stands for all occurances.
echo 'Hello world! It is a nice world!' | tee hello.txt | sed 's/world/bash/g'
# all the occurance of 'world' will be with '***' from hello.txt files
sed 's/world/***/g' hello.txt
```

## Server log analysis exercises

- how many downloads
- how many uniq downloads

download the exercise file

```shell
curl -O https://downloads.codingcoursestv.eu/055%20-%20bash/log/access.log
```

To have a look at the file

```shell
less ./access.log
```

Total downloads

```shell
grep -F .zip ./access.log | wc -l
```

- returns 4061, means 4061 downloads

uniqe downloads

```shell
grep -F .zip ./access.log | cut -d ' ' -f 7 | sort -u | wc -l
# or
grep -F .zip ./access.log | cut -d ' ' -f 7 | sort| uniq | wc -l
```

- returns 27, means 27 uniqe downloads
