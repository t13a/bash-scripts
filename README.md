# Bash Scripts

My Bash script collection.

## Scripts

### `decisiontab`

A [dicision table](https://en.wikipedia.org/wiki/Decision_table) implementation. This contains functions that helps to improve the readability of complex `if` statements.

Example:

```sh
$ cat << EOF > ./get-status.sh
> #!/usr/bin/env bash
>
> source ./decisiontab
>
> # this is real code not document
> decision_init LIVE  INIT  READY TERM
> decision_rule yes   no    -     -       echo not-initialized
> decision_rule yes   yes   no    no      echo not-ready
> decision_rule yes   yes   yes   no      echo ready
> decision_rule yes   -     -     yes     echo terminating
> decision_rule no    -     -     yes     echo terminated
> decision_rule -     -     -     -       echo invalid
> decision_make
EOF
$ env LIVE=yes INIT=yes READY=yes TERM=no bash ./get-status.sh
> ready
```

### `echo-with-color`

A fancy `echo` command wrapper. 16 colors defined by [ANSI escape code](https://en.wikipedia.org/wiki/ANSI_escape_code#3/4_bit) are available.

Example:

```
$ ./echo-with-color -R hello -Y world -G with -C 3/4 -B bit -M color
> hello world with 3/4 bit color # shown in each color
```

### `file-output`

A little flexible file output command. You can specify whether to append or replace, overwrite or not overwrite, etc. Also this outputs short and meaningful information.

Example:

```sh
$ echo 'input' | ./file-output output.txt
> output.txt: file created
$ echo 'input' | ./file-output output.txt # no overwrite, and returns non-zero exit status
> output.txt: already exists
$ echo 'input' | ./file-output -n output.txt # no overwrite, but returns exit status of zero
> output.txt: already exists, but ignored
$ echo 'input' | ./file-output -f output.txt # overwrite, but not changed
> output.txt: OK
$ echo 'other input' | ./file-output -f output.txt # overwrite, and changed
> output.txt: changed
```
