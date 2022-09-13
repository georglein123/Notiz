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