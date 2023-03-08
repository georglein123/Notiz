CSP设备自动校准新方案验证测试操作流程

准备：

1. 电脑
2. 软件： xftp，xshell
3. 键盘
4. 网线

#### 一、 CSP设备上位机软件导入

1. 命令行杀死上位机

2. 进入app路径

   ![image-20230306200301299](E:/文档/GitHub/Notiz/自动均匀性校准优化.assets/image-20230306200301299.png)

   

3. 备份现行的release文件夹

   ![image-20230306200522025](E:/文档/GitHub/Notiz/自动均匀性校准优化.assets/image-20230306200522025.png)

   

4. 复制新版上位机软件指定文件到release，从而替换对应文件夹

5. 

   ![image-20230306200802670](E:/文档/GitHub/Notiz/自动均匀性校准优化.assets/image-20230306200802670.png)

   

6. 回到app路径上

![image-20230306201111116](E:/文档/GitHub/Notiz/自动均匀性校准优化.assets/image-20230306201111116.png)



#### 二、自动校准配置文件、20点光斑图导入

配置文件导入

![image-20230306201726894](E:/文档/GitHub/Notiz/自动均匀性校准优化.assets/image-20230306201726894.png)

第20点光斑图导入

![image-20230306201943964](E:/文档/GitHub/Notiz/自动均匀性校准优化.assets/image-20230306201943964.png)

#### 三、自动均匀性校准

1. 清洁料盘及相机模组镜头

2. 放好背光膜，插入相机模组

3. 进入高级设置，点击自动光机校准

   ![image-20221202115859841](E:/文档/GitHub/Notiz/自动均匀性校准优化.assets/image-20221202115859841.png)

   

   2. 依次进入下一步

      ![image-20221202120047656](E:/文档/GitHub/Notiz/自动均匀性校准优化.assets/image-20221202120047656.png)

      

   3. 完成自动校准后，进入mainwindow界面，进行复检

#### 四、复检

1. 复检光强设定在21W±0.2W（注意：不同光度计会有偏差，0.2W左右，同一个操作人员使用同一个光度计）

   ![image-20221202120649178](E:/文档/GitHub/Notiz/自动均匀性校准优化.assets/image-20221202120649178.png)

2. 开启均匀性检测

   ![image-20221202120809963](E:/文档/GitHub/Notiz/自动均匀性校准优化.assets/image-20221202120809963.png)



3. 导出测试结果到Downloads文件夹中

   ![image-20221202121258182](E:/文档/GitHub/Notiz/自动均匀性校准优化.assets/image-20221202121258182.png)



1. 注意光机防尘盖是否打开
2. 光路是否清洁（相机镜头、透明玻璃、料盘）
3. 检查mainWindow界面程序版本



#### 五、复原csp设备

1. 杀死前后端

2. 进入app路径

   ![image-20230306203134606](E:/文档/GitHub/Notiz/自动均匀性校准优化.assets/image-20230306203134606.png)

3. 在app路径下，删除release文件夹

   ![image-20230306203523328](E:/文档/GitHub/Notiz/自动均匀性校准优化.assets/image-20230306203523328.png)

4. 将release_orig改为release

   ![image-20230306203902484](E:/文档/GitHub/Notiz/自动均匀性校准优化.assets/image-20230306203902484.png)

5. 进入 .heygears/configs 中

6.  autograycalib.json删除

   ![image-20230306204246785](E:/文档/GitHub/Notiz/自动均匀性校准优化.assets/image-20230306204246785.png)

7. 将Downloads中的文件全部删除

