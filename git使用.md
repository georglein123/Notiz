在VS Code中将使用git

代码提交

一、从远端下载代码仓库

1. 将远端代码仓库下载下来

![image-20230415002552485](/Users/junhuang/Library/Application Support/typora-user-images/image-20230415002552485.png)

2. 进入到下载下来的远端文件夹内，查看文件信息（必须有git文件夹才能查看git状态），及git状态

![image-20230415004412518](git使用.assets/image-20230415004412518.png)

3. 代码仓库中的文件修改后，查看修改的文件

![image-20230415005023909](git使用.assets/image-20230415005023909.png)

4. 代码仓库中新增文件

![image-20230415005413389](git使用.assets/image-20230415005413389.png)

5. 添加git变化

![image-20230415010022698](git使用.assets/image-20230415010022698.png)

6. 记录了变化之后可以提交了（交代what and why）

![image-20230415010837844](git使用.assets/image-20230415010837844.png)

7. 上传到远端（注意github分支名是main）

   origin是git的仓库，main是分支名

   ![image-20230415015614951](git使用.assets/image-20230415015614951.png)

上传成功后，GitHub上显示的信息

![image-20230415020001964](git使用.assets/image-20230415020001964.png)

二、本地代码仓库（此时无git）

1. 新建路径

![image-20230415020710183](git使用.assets/image-20230415020710183.png)

2. git初始化

![image-20230415091328009](git使用.assets/image-20230415091328009.png)

3. 查看文件的git状态

![image-20230415091603835](git使用.assets/image-20230415091603835.png)

4. 添加git变化

![image-20230415092107327](git使用.assets/image-20230415092107327.png)

5. 提交git变化

![image-20230415092351351](git使用.assets/image-20230415092351351.png)

6. 上传git变化（由于远端无此仓库，上传会出现错误，需要先在远端新建仓库）

![image-20230415092958809](git使用.assets/image-20230415092958809.png)

7. 在远端新建仓库

![image-20230416113122909](git使用.assets/image-20230416113122909.png)

8. 将远端仓库和本地仓库建立连接，并查看连接的远端仓库（）

```c++
git remote -v (小写v)
```

![image-20230416113603335](git使用.assets/image-20230416113603335.png)

![image-20230416113742383](git使用.assets/image-20230416113742383.png)

9. 上传到远端（显示出错）

![image-20230416120313081](git使用.assets/image-20230416120313081.png)

因为此时该本地仓库的分支名是master，不是main

见步骤3:

![image-20230416120540881](git使用.assets/image-20230416120540881.png)

10. 上传至远端分支master

![image-20230416120640807](git使用.assets/image-20230416120640807.png)

还可以：将当前分支强行命名为main分支

![image-20230417204318380](git使用.assets/image-20230417204318380.png)

![image-20230417205256113](git使用.assets/image-20230417205256113.png)



11. 远端显示

![image-20230416121658256](git使用.assets/image-20230416121658256.png)

分支

1. 查看当前路径的分支情况

![image-20230416124037360](git使用.assets/image-20230416124037360.png)

2. 创建新分支，并选择该分支

![image-20230416181615535](git使用.assets/image-20230416181615535.png)

3. 切换分支

![image-20230416182110697](git使用.assets/image-20230416182110697.png)

4. 切换分支

![image-20230416182557951](git使用.assets/image-20230416182557951.png)

5. 在该分支上修改路径中的文件

![image-20230416183218260](git使用.assets/image-20230416183218260.png)

6. 保存及提交变化记录

![image-20230416183450594](git使用.assets/image-20230416183450594.png)

7. 切换到另一分支main，main分支无修改

![image-20230416183900040](git使用.assets/image-20230416183900040.png)

8. 分支比较

![image-20230416185339002](git使用.assets/image-20230416185339002.png)



分支合并

将feature-readme-instructions分支合并到main分支之前

先将feature-readme-instructions分支上传到远端

![image-20230416202649329](git使用.assets/image-20230416202649329.png)

需要设置上游，再上传

![image-20230416204356500](git使用.assets/image-20230416204356500.png)



GitHub界面合并分支

1. 合并请求

![image-20230416205622928](git使用.assets/image-20230416205622928.png)

2. 创建合并

![image-20230416211142362](git使用.assets/image-20230416211142362.png)

3. 进行合并

![image-20230416211617193](git使用.assets/image-20230416211617193.png)

4. 确认合并

![image-20230416211729896](git使用.assets/image-20230416211729896.png)

合并结果

![image-20230416211855105](git使用.assets/image-20230416211855105.png)

合并分支到主分支main后拉到本地

1. 切换到主分支main

![image-20230416212316732](git使用.assets/image-20230416212316732.png)

2. 从远端拉到本地

![image-20230416212542465](git使用.assets/image-20230416212542465.png)

3. 从分支合并到主分支后，即可删除从分支

![image-20230416235059375](git使用.assets/image-20230416235059375.png)



冲突解决

1. 

![image-20230416235809324](git使用.assets/image-20230416235809324.png)

2. 

![image-20230417000546958](git使用.assets/image-20230417000546958.png)

3. 

![image-20230417001214811](git使用.assets/image-20230417001214811.png)

（这两分支都在本地的同一文件的同一位置做了修改，因此产生了冲突，必须提交修改后才能切换分支）

4. 

![image-20230417001622133](git使用.assets/image-20230417001622133.png)

5. 

![image-20230417001941485](git使用.assets/image-20230417001941485.png)

6. 

![image-20230417002448957](git使用.assets/image-20230417002448957.png)

7. 修改

![image-20230417003221321](git使用.assets/image-20230417003221321.png)

8. 

![image-20230417003858597](git使用.assets/image-20230417003858597.png)



撤销

1. 

![image-20230417004514305](git使用.assets/image-20230417004514305.png)

2. 

![image-20230417004724380](git使用.assets/image-20230417004724380.png)

3. 提交了变化记录

![image-20230417005021613](git使用.assets/image-20230417005021613.png)

4. 重置

HEAD：指代上一次提交的commit

1:表示commit的上一步

![image-20230417005224522](git使用.assets/image-20230417005224522.png)

![image-20230417005524409](git使用.assets/image-20230417005524409.png)

5. 

![image-20230417005948629](git使用.assets/image-20230417005948629.png)

![image-20230417010148566](git使用.assets/image-20230417010148566.png)

6. 

![image-20230417010621866](git使用.assets/image-20230417010621866.png) 



查看远端的更新

git fetch origin

查看有哪些更改

git diff origin/master

确认可以即可合并

*git merge origin/master* 

