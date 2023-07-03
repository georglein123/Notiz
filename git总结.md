git总结

查看远端的更新

git fetch origin

查看有哪些更改

git diff origin/master

确认可以即可合并

*git merge origin/master* 



工作区workspace:

stage暂存区：

repository本地仓库：

remote远端仓库：

![image-20230703180447952](D:/文档/GitHub/Notiz/git使用.assets/image-20230703180447952.png)

![image-20230703183425821](D:/文档/GitHub/Notiz/git使用.assets/image-20230703183425821.png)

文件的三种状态：

untracked：未跟踪状态，此文件在文件夹中，在工作区

- （前进）staged：通过git add命令状态变为staged，将文件放入暂存区
- （后退）无法后退

modified：已修改状态（将本地仓库中的文件修改后即为该状态），仅仅是修改，没有进行其他操作，存放在暂存区，状态为modified。

- （前进）staged：通过git add 将状态变为staged
- （后退）unmodify：通过git checkout，即从本地仓库中取出文件，覆盖当前修改，丢弃修改，回到unmodify状态，或者通过git restore丢弃修改。

staged：暂存状态，存放在暂存区，状态为staged。

- （前进）unmodify：通过git commit，将文件放入本地仓库
- （后退）modified：通过git reset HEAD filename，取消暂存，变成modified
- （后退两步）untracked：通过git rm --cached filename，将文件放入工作区，状态变成untracked，不删除本地文件，只删除git记录，并且不要git记录
  - git rm filename， 既删除本地文件，也删除git记录。

unmodify：未修改状态，文件在本地仓库，状态为unmodify（本地仓库）

- （前进）：通过修改，状态变为modified，文件进入在暂存区；
- （后退）：通过git rm --cached filename， 将文件放入工作区，状态变成untracked。

![image-20230703184028205](D:/文档/GitHub/Notiz/git使用.assets/image-20230703184028205.png)

本地仓库的代码修改完成后，想查看修改了哪些地方

`git diff`：此命令比较的是工作区中当前文件和暂存区域快照之间的差异。 也就是修改之后还没有暂存起来的变化内容