# How to reproduce the problem

Sometimes I would like to build on binary only as the source code may contains
a lot of other similar code (for example a lot of driver share the same API).

This document describe how to reproduce the [issue](https://github.com/fcamel/gj/issues/11)

## compile a.c 

```
gcc -g a.c
```

## run `gj` on binary only

```
pandy@ubuntu:~/gj_test$ gj -I
> Index ELF binaries ...
('a.out', '') 2
Index [a.out] ...
nm: 'a.out': No such file
readelf: Error: 'a.out': No such file
Save the index to gj.index

> Done
```

Search the symbol, it complains `ID` not found.

```
pandy@ubuntu:~/gj_test$ gj -D foo
Database file "ID" is not found. Have you run "gj -i"?
```

## How to workaround

create an empty ID:

```
pandy@ubuntu:~/gj_test$ touch ID
```

This workaround  could work:

```
(1) 3:./a.c:foo

Select an action:
* Input number to select a file. Multiple choices are allowed (e.g., type "1-3, 5")
* Type ";" / "!;" to keep / remove statements.
* Type "." to switch between all matches and fold matches.
* Type STRING (regex) to filter filename. !STRING means exclude the matched filename:
* Type ~[PATTERN1 PATTERN2 ~PATTERN3 ...] to start over.
  Type only "~" to use the patterns from the command line.
* Type ENTER to exit.
>>

```
