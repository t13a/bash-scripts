# Bash Scripts

My Bash script collection.

## Scripts

### `decisiontab`

A [dicision table](https://en.wikipedia.org/wiki/Decision_table) implementation. This contains functions that helps to improve the readability of complex `if` statements.

Example:

```sh
$ cat << EOF > ./get-status.sh
> #!/usrbin/env bash
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
