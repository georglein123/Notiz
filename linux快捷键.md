linux快捷键

Alt + F1打开命令行，也可以打开文件管理器Windows + E 再按F4

CS杀死上位机

- sudo killall ultracore-bootloader  杀掉上位机

CSP杀死上位机：分别执行

- sudo killall backend
-  sudo killall frontend

CSP新版软件更新方法

- 先备份现行的release文件夹
- 杀死上位机，复制指定的文件夹到release，从而替换对应文件夹
- 重启设备



\##复制一个文件夹下的多个文件 如果我们想把文件夹file_a中的多个文件，如a，b，c复制到文件夹file_b中，该怎么办呢？

用最土的方法，cp file_a/a file_a/b file_a/c file_b，即可。我们可以看到我们把a，b，c文件的路径都写了一遍。 我们很容易想到能不能不用重复写相同的文件路径呢？答案是可以的，方法如下：

cp file_a/{a,b,c} file_b，即可。注意大括号中的文件是用逗号分开的。

大括号里面可以添加要复制的文件或者文件夹。



移动/重命名

mv 



复制

cp



删除

rm





