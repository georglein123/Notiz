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



## shell命令

类Unix shell，例如 Bash 或 ZSH， `echo $SHELL`命令可以查看您的 shell 是否满足要求

### 单个程序

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



文件目录浏览

```c++
missing:~$ pwd
/home/missing
missing:~$ cd /home
missing:/home$ pwd
/home
missing:/home$ cd ..
missing:/$ pwd
/
missing:/$ cd ./home
missing:/home$ pwd
/home
missing:/home$ cd missing
missing:~$ pwd
/home/missing
missing:~$ ../../bin/echo hello
hello
```

配置 shell 提示符来显示各种有用的信息



查询程序的参数、输入输出的信息`man`

```shell
missing:~$ man ls
```

```c++
missing:~$ ls -l /home
drwxr-xr-x 1 missing  users  4096 Jun 15  2019 missing
```

更加详细地列出目录下文件或文件夹的信息

本行第一个字符 `d` 表示 `missing` 是一个目录

接下来的九个字符，每三个字符构成一组。 （`rwx`）. 它们分别代表了文件所有者（`missing`），用户组（`users`） 以及其他所有人具有的权限

其中 `-` 表示该用户不具备相应的权限

为了进入某个文件夹，用户需要具备该文件夹以及其父文件夹的“搜索”权限（以“可执行”：`x`）权限表示

为了列出它的包含的内容，用户必须对该文件夹具备读权限（`r`）



### shebang





### 程序间

在 shell 中，程序（此时就是一个命令，例如echo，cat等等）有两个主要的“流”：

- 输入流
- 输出流

当程序尝试读取信息时，它们会从输入流中进行读取，当程序打印信息时，它们会将信息输出到输出流中

通常，一个程序的输入输出流都是您的终端。也就是，您的键盘作为输入，显示器作为输出。 但是，我们也可以重定向这些流！

流重定向：

最简单的重定向是 `< file` 和 `> file`。这两个命令可以将程序的输入输出流分别重定向到文件

```c++
missing:~$ echo hello > hello.txt
missing:~$ cat hello.txt
hello
missing:~$ cat < hello.txt
hello
missing:~$ cat < hello.txt > hello2.txt
missing:~$ cat hello2.txt
hello
```

使用 `>>` 来向一个文件追加内容。

```
missing:~$ cat < hello.txt >> hello2.txt
```

在hello2.txt的文件中追加内容，不会覆盖原内容



使用管道（ *pipes* ），我们能够更好的利用文件重定向。 `|` 操作符允许我们将一个程序的输出和另外一个程序的输入连接起来

```
missing:~$ ls -l / 
```



### 根用户（root user）

 通常在我们并不会以根用户的身份直接登录系统，因为这样可能会因为某些错误的操作而破坏系统。 取而代之的是我们会在需要的时候使用 `sudo` 命令





## Shell 脚本

创建脚本文件

`xxx.sh`

执行：

命令行：`. xxx.sh`



 bash 脚本

赋值：`foo=bar`

访问变量中存储的数值：`$foo`

注：`foo = bar` （使用空格隔开）是不能正确工作的，因为解释器会调用程序`foo` 并将 `=` 和 `bar`作为参数，shell脚本中使用空格会起到分割参数的作用

Bash中的字符串通过`'` 和 `"`分隔符来定义：

- 以`'`定义的字符串为原义字符串，其中的变量不会被转义，

- 而 `"`定义的字符串会将变量值进行替换。

```shell
foo=bar
echo "$foo"
# 打印 bar
echo '$foo'
# 打印 $foo
```



`bash`也支持`if`, `case`, `while` 和 `for` 这些控制流关键字，支持函数，它可以接受参数并基于参数进行操作

```shell
mcd () {
    mkdir -p "$1"
    cd "$1"
}
```

与其他脚本语言不同的是，bash使用了很多特殊的变量来表示参数、错误代码和相关变量。下面是列举来其中一些变量

- `$0` - 脚本名
- `$1` 到 `$9` - 脚本的参数。 `$1` 是第一个参数，依此类推。
- `$@` - 所有参数
- `$#` - 参数个数
- `$?` - 前一个命令的返回值
- `$$` - 当前脚本的进程识别码
- `!!` - 完整的上一条命令，包括参数。常见应用：当你因为权限不足执行命令失败时，可以使用 `sudo !!`再尝试一次。
- `$_` - 上一条命令的最后一个参数。如果你正在使用的是交互式 shell，你可以通过按下 `Esc` 之后键入 . 来获取这个值。

```shell
mcd () {
    mkdir -p "$1"
    cd "$1"
}

mcd "$@"

```



`mcd "$@"` 这句代码用于在脚本中调用 `mcd` 函数，并将脚本接收到的所有参数（如果有的话）传递给该函数。

### 各组成部分的解释

- `mcd`：这是你定义的函数名。
- `"$@"`：这是一个特殊的Shell变量，用于表示所有传递给脚本或函数的参数。每个参数都作为独立的字符串处理。

### 为什么使用 "$@" 而不是其他？

1. **独立处理每个参数**：使用`"$@"`能确保每个参数都作为独立的字符串传递，即使参数包含空格或其他特殊字符也没有问题。

    例如，如果你运行 `./mcd.sh "new folder" "another folder"`，`$@` 就会是 `"new folder" "another folder"` 这两个独立的参数。

2. **引号的重要性**：引号（`"`）非常重要，因为它们确保即使参数中有空格或特殊字符，参数也会完整地传递。

### 在上下文中的应用

假设你有一个脚本文件（假设名为`mcd.sh`），其内容如下：

```bash
mcd () {
    mkdir -p "$1"
    cd "$1"
}

mcd "$@"
```

当你运行 `./mcd.sh MyFolder`，这里的 `"$@"` 会将 `MyFolder` 这一参数传递给 `mcd` 函数。然后 `mkdir -p "MyFolder"` 和 `cd "MyFolder"` 会被依次执行。

如果你运行 `./mcd.sh "New Folder"`（注意这里的空格），`"$@"` 会将 `New Folder` 作为一个整体（一个参数）传递给 `mcd` 函数，因此会创建一个名为 `New Folder` 的目录并进入该目录。

总体而言，`mcd "$@"` 是一种灵活和安全的方式，用于将所有脚本参数传递给 `mcd` 函数。



完整列表：

[Special Characters (tldp.org)](https://tldp.org/LDP/abs/html/special-chars.html)



直接输出

命令通常使用 `STDOUT`来返回输出值，使用`STDERR` 来返回错误及错误码，便于脚本以更加友好的方式报告错误。

返回码或退出状态是脚本/命令之间交流执行状态的方式。返回值0表示正常执行，其他所有非0的返回值都表示有错误发生。

退出码可以搭配 `&&`（与操作符）和 `||`（或操作符）使用，用来进行条件判断，决定是否执行其他程序。

同一行的多个命令可以用`;`分隔

程序 `true` 的返回码永远是`0`，`false` 的返回码永远是`1`

```shell
false || echo "Oops, fail"
# Oops, fail

true || echo "Will not be printed"
#

true && echo "Things went well"
# Things went well

false && echo "Will not be printed"
#

false ; echo "This will always run"
# This will always run
```



以变量的形式获取一个命令的输出

通过 *命令替换*（*command substitution*）实现

例如，如果执行 `for file in $(ls)` ，shell首先将调用`ls` ，然后遍历得到的这些返回值

当您通过 `$( CMD )` 这样的方式来执行`CMD` 这个命令时，它的输出结果会替换掉 `$( CMD )`



冷门的类似特性是 *进程替换*（*process substitution*）

 `<( CMD )` 会执行 `CMD` 并将结果输出到一个临时文件中，并将 `<( CMD )` 替换成临时文件名。这在我们希望返回值通过文件而不是STDIN传递时很有用。例如， `diff <(ls foo) <(ls bar)` 会显示文件夹 `foo` 和 `bar` 中文件的区别。

```shell
#!/bin/bash

echo "Starting program at $(date)" # date会被替换成日期和时间

echo "Running program $0 with $# arguments with pid $$"

for file in "$@"; do
    grep foobar "$file" > /dev/null 2> /dev/null
    # 如果模式没有找到，则grep退出状态为 1
    # 我们将标准输出流和标准错误流重定向到Null，因为我们并不关心这些信息
    if [[ $? -ne 0 ]]; then
        echo "File $file does not have any foobar, adding one"
        echo "# foobar" >> "$file"
    fi
done
```

在条件语句中，我们比较 `$?` 是否等于0。 Bash实现了许多类似的比较操作，您可以查看 [`test 手册`](https://man7.org/linux/man-pages/man1/test.1.html)。 在bash中进行比较时，尽量使用双方括号 `[[ ]]` 而不是单方括号 `[ ]`，这样会降低犯错的几率



注意，脚本并不一定只有用 bash 写才能在终端里调用。比如说，这是一段 Python 脚本，作用是将输入的参数倒序输出：

```python
#!/usr/local/bin/python
import sys
for arg in reversed(sys.argv[1:]):
    print(arg)
```



### Shebang

内核知道去用 python 解释器而不是 shell 命令来运行这段脚本，是因为脚本的开头第一行的 [shebang](https://en.wikipedia.org/wiki/Shebang_(Unix))。

在 `shebang` 行中使用 [`env`](https://man7.org/linux/man-pages/man1/env.1.html) 命令是一种好的实践，它会利用环境变量中的程序来解析该脚本，这样就提高来您的脚本的可移植性。`env` 会利用我们第一节讲座中介绍过的`PATH` 环境变量来进行定位。 例如，使用了`env`的shebang看上去时这样的`#!/usr/bin/env python`。



`#!/bin/bash` 是一个称为“shebang”（也称为“hashbang”或“pound-bang”）的特殊标记，它位于脚本文件的第一行。这一行指示操作系统应该使用哪个解释器来运行脚本的剩余部分。在这个特定的例子中，它指定了脚本应由 `/bin/bash` 解释器（也就是Bash shell）来执行。

### 组成部分解释

- `#!`：这是shebang的起始符号，用于标识接下来的路径是解释器的路径。
- `/bin/bash`：这是解释器的绝对路径，用于执行脚本。在这个例子中，解释器是Bash shell，通常位于`/bin/`目录下。

### 如何工作？

当你通过如下方式运行脚本：

```bash
./my_script.sh
```

操作系统会查看脚本的第一行。如果它看到了一个shebang（`#!`），它就会知道需要使用shebang后指定的解释器来运行这个脚本。因此，在这个例子中，它会使用`/bin/bash`来执行脚本中的命令。

### 注意事项

- Shebang 必须出现在脚本文件的第一行。
- Shebang 行后面不能有空格。
- 解释器路径必须是绝对路径，不能是相对路径。

如果你的系统中Bash的路径不是`/bin/bash`，或者你想使用其他的shell或解释器（如`/bin/sh`、`/usr/bin/python`等），你需要相应地修改shebang。

例如，如果你想使用Python解释器运行脚本，shebang应该改为：

```bash
#!/usr/bin/python
```

这样，操作系统就会知道使用`/usr/bin/python`来执行脚本。



当执行脚本时，我们经常需要提供形式类似的参数

bash使我们可以轻松的实现这一操作，它可以基于文件扩展名展开表达式。这一技术被称为shell的 *通配*（*globbing*）

- 通配符 - 当你想要利用通配符进行匹配时，你可以分别使用 `?` 和 `*` 来匹配一个或任意个字符。例如，对于文件`foo`, `foo1`, `foo2`, `foo10` 和 `bar`, `rm foo?`这条命令会删除`foo1` 和 `foo2` ，而`rm foo*` 则会删除除了`bar`之外的所有文件。
- 花括号`{}` - 当你有一系列的指令，其中包含一段公共子串时，可以用花括号来自动展开这些命令。这在批量移动或转换文件时非常方便。

```shell
convert image.{png,jpg}
# 会展开为
convert image.png image.jpg

cp /path/to/project/{foo,bar,baz}.sh /newpath
# 会展开为
cp /path/to/project/foo.sh /path/to/project/bar.sh /path/to/project/baz.sh /newpath

# 也可以结合通配使用
mv *{.py,.sh} folder
# 会移动所有 *.py 和 *.sh 文件

mkdir foo bar

# 下面命令会创建foo/a, foo/b, ... foo/h, bar/a, bar/b, ... bar/h这些文件
touch {foo,bar}/{a..h}
touch foo/x bar/y
# 比较文件夹 foo 和 bar 中包含文件的不同
diff <(ls foo) <(ls bar)
# 输出
# < x
# ---
# > y
```



函数与shell

shell函数和脚本有如下一些不同点：

- 函数只能与shell使用相同的语言，脚本可以使用任意语言。因此在脚本中包含 `shebang` 是很重要的。
- 函数仅在定义时被加载，脚本会在每次被执行时加载。这让函数的加载比脚本略快一些，但每次修改函数定义，都要重新加载一次。
- 函数会在当前的shell环境中执行，脚本会在单独的进程中执行。因此，函数可以对环境变量进行更改，比如改变当前工作目录，脚本则不行。脚本需要使用 [`export`](https://man7.org/linux/man-pages/man1/export.1p.html) 将环境变量导出，并将值传递给环境变量。
- 与其他程序语言一样，函数可以提高代码模块性、代码复用性并创建清晰性的结构。shell脚本中往往也会包含它们自己的函数定义。



查找文件及代码

`grep`

在Linux文件系统中查找名为 `foo` 的目录，通常使用 `find` 命令。与在根目录下查找类似，但由于你现在是要在整个文件系统中查找，所以具体的命令会有所不同。这里有几种方法：

### 1. 在整个文件系统中查找

```bash
sudo find / -type d -name "foo" 2>/dev/null
```

这个命令会在整个文件系统中搜索，从根目录 `/` 开始。

### 2. 在特定目录下开始搜索

如果你有一个更加具体的起始目录，比如你想从 `/home` 开始搜索，那么你可以这样做：

```bash
sudo find /home -type d -name "foo" 2>/dev/null
```

### 命令解释

- `sudo`：使用管理员权限执行命令，因为某些目录可能需要这样的权限。
- `find`：是用于查找文件和目录的命令。
- `/` 或 `/home`：这是搜索的起始目录。
- `-type d`：这个选项告诉 `find` 命令只查找目录。
- `-name "foo"`：这表示你只对名为 "foo" 的目录感兴趣。
- `2>/dev/null`：这会把所有错误信息（大多是权限不足的错误）重定向到 `/dev/null`，意即忽略这些错误。

### 注意事项

- 运行这个命令可能需要一些时间，特别是如果你从根目录 `/` 开始搜索的话。
- `2>/dev/null` 是可选的，但它可以帮助你过滤掉不必要的错误信息。

运行这些命令后，所有名为 `foo` 的目录路径都会在命令行输出中列出。如果没有找到任何这样的目录，那么命令将不会有任何输出。
