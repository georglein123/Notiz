PS软件中读取要获取的某个区域范围，比如矩形范围，左上角点像素坐标在PS软件中读取（x1，y1），右下角点像素坐标（x2，y2）（这些像素点还是落在边界的待取区域上，而不是旁边）

代取区域：

![image-20220419111235374](E:\文档\GitHub\Notiz\从PS中读取范围到pythonCV中处理.assets\image-20220419111235374.png)

代取区域左上角：（96，107）

![image-20220419111000101](E:\文档\GitHub\Notiz\从PS中读取范围到pythonCV中处理.assets\image-20220419111000101.png)

待取区域右下角：（102，113）

![image-20220419111052110](E:\文档\GitHub\Notiz\从PS中读取范围到pythonCV中处理.assets\image-20220419111052110.png)

对应到python CV中编程获取矩阵的范围是[y1:y2+1, x1: x2+1, :]，即[107:114, 96:103, :]



从PS读取像素点坐标方法：

打开ps软件，在“窗口”选项中选择“信息”，即可查看某个像素的灰度值，同时可以查看某个像素的坐标

![image-20220105185851166](E:\文档\GitHub\Notiz\从PS中读取范围到pythonCV中处理.assets\image-20220105185851166.png)

![image-20220105185920028](E:\文档\GitHub\Notiz\从PS中读取范围到pythonCV中处理.assets\image-20220105185920028.png)