linux操作命令



sed

Sed, short for Stream EDitor, is a command that is used to perform text transformations and manipulations on a file. Some of these transformations include searching and replacing text. With Linux sed command, you can manipulate and edit text files without even opening them. In this tutorial, you will learn how to manipulate text files using sed command.

`sed {OPTIONS} filename`

`sed 's/Linux/Unix/' linuxgeek.txt`

The `s` in the command is the replacement indicator.
The `/` are the delimiters
`Linux` is the search term
`unix` is the replacement term



sed -i

-i: overwrite，覆盖， this flag makes the edits "in place"

sed -e

-e: expression， add the script to the commands to be executed



## shell

shell 是一个编程环境，所以它具备变量、条件、循环和函数

您当前所在的位置是 `~` (表示 "home")

`$` 符号表示您现在的身份不是 root 用户

1. 输入 *命令* ，命令最终会被 shell 解析

```shell
missing:~$ date
```



2. 在执行命令的同时向程序传递 *参数* ：

`echo`：打印出传给echo的参数

```shell
missing:~$ echo hello
```



 shell 基于空格分割命令并进行解析，然后执行第一个单词代表的程序，并将后续的单词作为程序可以访问的参数。

如果您希望传递的参数中包含空格（例如一个名为 My Photos 的文件夹），您要么用使用单引号，双引号将其包裹起来，要么使用转义符号 `\` 进行处理（`My\ Photos`）

如果你要求 shell 执行某个指令，但是该指令并不是 shell 所了解的编程关键字，那么它会去咨询 *环境变量* `$PATH`，它会列出当 shell 接到某条指令时，进行程序搜索的路径：

*环境变量* `$PATH`，

```shell
missing:~$ echo $PATH
/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin
missing:~$ which echo
/bin/echo
missing:~$ /bin/echo $PATH
/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin
```

shell 了解到需要执行 `echo` 这个程序，随后它便会在 `$PATH` 中搜索由 `:` 所分割的一系列目录，基于名字搜索该程序



命令的具体路径

```shell
missing:~$ which echo
/bin/echo
```



直接指定需要执行的程序的路径来执行该程序

```shell
missing:~$ /bin/echo $PATH
/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin
```

```shell
missing:~$ /bin/echo hello
```



查询程序的参数、输入输出的信息`man`

```shell
missing:~$ man ls
```





## Shell 脚本

 bash 脚本

赋值：`foo=bar`

访问变量中存储的数值：`$foo`

注：`foo = bar` （使用空格隔开）是不能正确工作的，因为解释器会调用程序`foo` 并将 `=` 和 `bar`作为参数，shell脚本中使用空格会起到分割参数的作用

Bash中的字符串通过`'` 和 `"`分隔符来定义：

- 以`'`定义的字符串为原义字符串，其中的变量不会被转义，

- 而 `"`定义的字符串会将变量值进行替换。
