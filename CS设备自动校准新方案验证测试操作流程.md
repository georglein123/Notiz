CS设备自动校准新方案验证测试操作流程

准备：

1. 电脑
2. 软件： xftp，xshell
3. 键盘
4. 网线

#### 一、 CS设备上位机软件导入

1. 进入后台命令行，杀掉前端和后端

   `sudo killall ultracore-bootloader`

2. 更改ultracore文件夹的读写权限

   用户目录（`/home/heygears/`）下执行：`sudo chmod 777 ultracore -R`

3. 备份bin文件，后期复原时直接使用该备份bin文件

   进入到ultracore路径下， 将bin文件夹命名为bin_orig，并新建一个bin文件夹

   `cd ultracore`

   `mv bin bin_orig`

   `mkdir bin`

4. 将解压后的文件夹内文件传输到bin文件夹内

   ![img](CS设备自动校准新方案验证测试操作流程.assets/lQDPJwjd8nzTHVxrzQJssCs5ztls3rqEA7Hq1xvATgA_620_107.jpg_620x10000q90.jpg)

5. 重启

#### 二、自动校准配置文件、第10点光斑图导入

配置文件导入

第10点光斑图导入

#### 三、自动均匀性校准

1. 清洁料盘及相机模组镜头
2. 放好背光膜，插入相机模组
3. 自动光机校准


#### 四、复检

1. 复检光强设定在21W±0.2W（注意：不同光度计会有偏差，0.2W左右，同一个操作人员使用同一个光度计）

2. 开启均匀性检测


3. 导出测试结果到Downloads文件夹中


注意：

1. 注意光机防尘盖是否打开
2. 光路是否清洁（相机镜头、透明玻璃、料盘）

#### 五、复原cs设备

1. 杀死前后端

2. 进入到ultracore路径下， 删除bin文件，将bin_orig更名为bin

   `cd ultracore`

   `sudo rm -r bin`

   `mv bin_orig bin`

3. autograycalib.json删除

4. 将Downloads中的文件全部删除

5. 重启

