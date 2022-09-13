chairside 自动均匀性校准新流程及复检界面使用

**前提条件：**

（若打印机中无自动均匀性校准生成的mask

查看路径：`/home/heygears/ultracore/bin`，

![image-20220713094845049](E:\文档\GitHub\Notiz\chairside 自动均匀性校准新流程及复检界面使用.assets\image-20220713094845049.png)

则需先运行自动均匀性校准生成一张mask

步骤：

安装相机模组，并放入新的背光膜（一次性，不可重复使用），并进入`开发者模式`，关闭`相机SN校验`（该功能为了保证同一台打印机配置同一块模组，避免混用，现在测试阶段，不需要该功能）

操作方法：连续点击`运维设置`5次后，输入密码，点击`完成`

![image-20220712173953522](E:\文档\GitHub\Notiz\chairside 自动均匀性校准.assets\image-20220712173953522.png)



点击`开发者选项`

![image-20220712174027875](E:\文档\GitHub\Notiz\chairside 自动均匀性校准.assets\image-20220712174027875.png)



关闭`相机SN校验`

![image-20220712174130856](E:\文档\GitHub\Notiz\chairside 自动均匀性校准.assets\image-20220712174130856.png)



返回打印机操作界面，点击`光机校准`

![image-20220712174257225](E:\文档\GitHub\Notiz\chairside 自动均匀性校准.assets\image-20220712174257225.png)



等待自动均匀性校准完成（此时会生成一张新的mask）

（自动均匀性校准完成后会在以下路径中生成自动均匀性校准的的mask）![image-20220712135332543](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20220712135332543.png)



）



若打印机有自动均匀性校准后生成的mask

打开该操作界面，点击`自动校准调试`选项卡，并点击`开始自动Mask的PI`

![image-20220712163235338](E:\文档\GitHub\Notiz\chairside 自动均匀性校准.assets\image-20220712163235338.png)



按照提示信息将光度计插入打印机并按照投图放置在料盘上，放好后再点击 `OK`

![image-20220712164738387](E:\文档\GitHub\Notiz\chairside 自动均匀性校准.assets\image-20220712164738387.png)



（`自动mask手动PI`的记录数据放置路径）

![image-20220712135555640](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20220712135555640.png)



PI曲线记录完成后，弹出提示窗口，点击`OK`

![image-20220712164552293](E:\文档\GitHub\Notiz\chairside 自动均匀性校准.assets\image-20220712164552293.png)



勿关机（若关机，则必须再做一次`开始自动Mask的PI`）

安装相机模组，并放入新的背光膜（一次性，不可重复使用），并进入`开发者模式`，关闭`相机SN校验`（该功能为了保证同一台打印机配置同一块模组，避免混用）

操作方法：连续点击`运维设置`5次后，输入密码，点击`完成`

![image-20220712173953522](E:\文档\GitHub\Notiz\chairside 自动均匀性校准.assets\image-20220712173953522.png)



点击`开发者选项`

![image-20220712174027875](E:\文档\GitHub\Notiz\chairside 自动均匀性校准.assets\image-20220712174027875.png)



关闭`相机SN校验`

![image-20220712174130856](E:\文档\GitHub\Notiz\chairside 自动均匀性校准.assets\image-20220712174130856.png)



返回打印机操作界面，点击`光机校准`

![image-20220712174257225](E:\文档\GitHub\Notiz\chairside 自动均匀性校准.assets\image-20220712174257225.png)



等待自动均匀性校准完成（此时会生成一张新的mask，之后投圆斑图等会调用该mask），即可进行复检

（自动均匀性校准完成后会在以下路径中生成自动均匀性校准的的mask）![image-20220712135332543](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20220712135332543.png)





复检界面使用：

`自动校准模式`：调用的mask为自动均匀性校准生成的mask

`手动校准模式`：调用的mask为手动均匀性校准生成的mask

`裸光机模式`：不调用mask

测试步骤：

选中指定模式，点击`选择图片`进行指定投图，选择图片完成后，接着点击`LED ON`，然后在设置能量框或设置电流框中输入对应数值，然后点击`设置电流`或`设置能量`（必须先LED ON 之后再点击设置能量，），即可查看`当前功率`或`当前电流`。

![image-20220712174845276](E:\文档\GitHub\Notiz\chairside 自动均匀性校准.assets\image-20220712174845276.png)





算法相关配置参数文件

![image-20220713101801062](E:\文档\GitHub\Notiz\chairside 自动均匀性校准新流程及复检界面使用.assets\image-20220713101801062.png)





chairside自动均匀性校准高度设置

进入指定路径的高度修改配置文件

![image-20220713110904261](E:\文档\GitHub\Notiz\chairside 自动均匀性校准新流程及复检界面使用.assets\image-20220713110904261.png)

首先设置`RESET_FALL=0`，



将`RESET_FALL=0`注释，并把`CALIB_FALL`参数配置















































退出文件，然后操作打印机使主轴点动运动到指定高度治具千分尺产生示数的位置，并根据点动次数计算运动距离

然后再打开该文件，将`RESET_FALL=0`注释，并把`CALIB_FALL`参数配置为计算得到的运动距离

最后做自动均匀性校准测试，观察是否运动距离准确。







![image-20220713163004608](E:\文档\GitHub\Notiz\chairside 自动均匀性校准新流程及复检界面使用.assets\image-20220713163004608.png)



















![image-20220714163638785](E:\文档\GitHub\Notiz\chairside 自动均匀性校准新流程及复检界面使用.assets\image-20220714163638785.png)