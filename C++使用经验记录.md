C++使用经验记录

### 头文件中定义了一个全局变量，就不要在源文件的某个函数中又定义一次，否则该变量会变成局部变量。

头文件

定义一个全局变量

![image-20230516121406650](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20230516121406650.png)

cpp文件

标注的那段话又会被定义一次，变成局部变量

![image-20230516121320930](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20230516121320930.png)