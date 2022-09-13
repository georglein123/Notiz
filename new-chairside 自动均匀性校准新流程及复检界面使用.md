chairside 自动均匀性校准新流程及复检界面使用

[TOC]

#### 〇、开始前必须核查项

1. **相机模组校准高度是否已设置**

​	查看方式：命令行输入`heygears@heygears:~$ cat /usr/local/ultracore/.env`

​	查看该文件中是否有关键字`CALIB_FALL`参数并进行了配置

![image-20220715145932254](E:\文档\GitHub\Notiz\new-chairside 自动均匀性校准新流程及复检界面使用.assets\image-20220715145932254.png)

​	 如若未配置，则配置后再进行后续步骤



2. **是否已设置使用自动均匀性校准结果**

   查看方式：命令行输入`heygears@heygears:~$ cat /usr/local/ultracore/.env`

   查看该文件中关键字`USE_AUTO_CALIBS` 是否配置为 `USE_AUTO_CALIBS=1`

![image-20220715150119721](E:\文档\GitHub\Notiz\new-chairside 自动均匀性校准新流程及复检界面使用.assets\image-20220715150119721.png)

​	若未配置该参数，则自行增加该参数并配置，操作方法如下：

​	2.1 命令行输入：`heygears@heygears:~$ sudo vim /usr/local/ultracore/.env`

![image-20220715150516836](E:\文档\GitHub\Notiz\new-chairside 自动均匀性校准新流程及复检界面使用.assets\image-20220715150516836.png)

​	2.2 接着键盘点击按键`I`，进入编辑模式，移动光标至末行，输入`USE_AUTO_CALIBS=1`

​	2.3 然后键盘点击按键`ESC`，退出编辑模式

​	2.4 接着英文输入法下输入`:wq`，即可自动退出

​	2.5最后重启打印机即可

​	**注意：**

​	配置`USE_AUTO_CALIBS=1`，并重启机器后

​	若接着做自动均匀性校准流程，那么使用的是自动均匀性校准结果，若做手动均匀性校准流程，则使用的是手动均匀性校准结果。

​	若只使用手动均匀性校准结果，则删除`USE_AUTO_CALIBS`字段



3.**`/home/heygears/.clinic`路径下是否无 `autograycalib.json`文件**

​	进入该路径`/home/heygears/.clinic`，查看是否有`autograycalib.json`文件，若有，则删除，若无则无需操作。

​	查看方式：

​	3.1 命令行输入`heygears@heygears:~$ cd .clinic`

​	3.2 命令行输入`ls -a`，查看当前路径下的所有文件

​	3.3 若存在`autograycalib.json`文件，则命令行输入`rm autograycalib.json`，删除该文件

​	3.4 命令行输入`ls -a`，检查是否已删除该文件

​	3.5 命令行输入`sudo reboot`，重启打印机并复核是否文件删除成功

​	3.6 再次进入该路径`heygears@heygears:~$ cd .clinic`

​	3.7 命令行输入`ls -a`，查看当前路径下的所有文件

​	3.8 若不存在`autograycalib.json`文件，则已删除成功





**以上核查没有问题后才可进入以下步骤：**

开启打印机后

#### 一、安装相机模组

#### 二、放入新的背光膜（一次性，不可重复使用）

1. 按照下图图示，找到背光膜正确的一面，并撕开背光膜（注意：勿触摸背光膜的中间部分）

![image-20220715131656974](E:\文档\GitHub\Notiz\new-chairside 自动均匀性校准新流程及复检界面使用.assets\image-20220715131656974.png)



2. 并将此面朝上，放入打印机料盘中（膜的左上缺角部分对应料盘左上角），如下图所示

![image-20220715132741355](E:\文档\GitHub\Notiz\new-chairside 自动均匀性校准新流程及复检界面使用.assets\image-20220715132741355.png)



3. 关闭打印机舱门

#### 三、关闭`相机SN校验`（每次重启后`相机SN校验`都会开启，需要手动关闭）

1. 点击`运维设置`

![image-20220715092159247](E:\文档\GitHub\Notiz\new-chairside 自动均匀性校准新流程及复检界面使用.assets\image-20220715092159247.png)



2. 连续点击`运维设置`5次后，输入动态密码，点击`完成`

![image-20220712173953522](E:\文档\GitHub\Notiz\new-chairside 自动均匀性校准新流程及复检界面使用.assets\image-20220712173953522.png)



3. 进入如下界面，点击`开发者选项`

![image-20220712174027875](E:\文档\GitHub\Notiz\new-chairside 自动均匀性校准新流程及复检界面使用.assets\image-20220712174027875.png)



4. 保证`相机SN校验`选项未选中，即为关闭`相机SN校验`（该功能为了保证同一台打印机配置同一块模组，避免混用，现处于自动均匀性校准模块测试阶段，不需要该功能）

![image-20220712174130856](E:\文档\GitHub\Notiz\new-chairside 自动均匀性校准新流程及复检界面使用.assets\image-20220712174130856.png)



#### 四、自动均匀性校准

1. 在打印机操作界面，点击`光机校准`

![image-20220712174257225](E:\文档\GitHub\Notiz\new-chairside 自动均匀性校准新流程及复检界面使用.assets\image-20220712174257225.png)



2. 按界面提示点击`下一步`

![image-20220715091653465](E:\文档\GitHub\Notiz\new-chairside 自动均匀性校准新流程及复检界面使用.assets\image-20220715091653465.png)



（若出现如下问题提示界面，则表示未关闭`相机SN校验`，关闭方法见前文）

![image-20220715091752128](E:\文档\GitHub\Notiz\new-chairside 自动均匀性校准新流程及复检界面使用.assets\image-20220715091752128.png)



3. 关闭`相机SN校验`后，则出现以下提示界面，`安装光机校准镜头` 正常，点击`下一步`

![image-20220715092707572](E:\文档\GitHub\Notiz\new-chairside 自动均匀性校准新流程及复检界面使用.assets\image-20220715092707572.png)



4. 继续点击`下一步`

![image-20220715092821562](E:\文档\GitHub\Notiz\new-chairside 自动均匀性校准新流程及复检界面使用.assets\image-20220715092821562.png)



5. 接着点击`开始校准`，即可进入自动均匀性校准过程

![image-20220715092906841](E:\文档\GitHub\Notiz\new-chairside 自动均匀性校准新流程及复检界面使用.assets\image-20220715092906841.png)



自动均匀性校准过程开始

![image-20220715092959850](E:\文档\GitHub\Notiz\new-chairside 自动均匀性校准新流程及复检界面使用.assets\image-20220715092959850.png)



等待自动均匀性校准完成（完成后会生成一张新的mask，覆盖文件夹中存在的mask，在这个过程中，会捕获电流I和灰度G的关系）

（自动均匀性校准完成后会在以下路径中生成自动均匀性校准的的mask）![image-20220712135332543](E:\文档\GitHub\Notiz\new-chairside 自动均匀性校准新流程及复检界面使用.assets\image-20220712135332543.png)



#### 五、获取自动Mask的PI

1. 在打印机上插上键盘，在键盘上同时按下`Alt`和`Tab`键，选择`Form`调试界面，出现以下界面，选择`自动校准调试`选项卡，并点击`开始自动Mask的PI`

![image-20220714211238579](E:\文档\GitHub\Notiz\new-chairside 自动均匀性校准新流程及复检界面使用.assets\image-20220714211238579.png)



2. 此时出现提示信息，料盘中也会出现圆斑图，将光度计插入打印机，并按照圆斑图的位置对准，放置在料盘上，放置好之后再点击 `OK`

![image-20220715093704737](E:\文档\GitHub\Notiz\new-chairside 自动均匀性校准新流程及复检界面使用.assets\image-20220715093704737.png)



3. 点击 `OK`后，将开始捕获指定电流下的光强值，`当前能量列表` 栏中不断更新数值，即为`当前电流列表`中电流对应的光强值

![image-20220715094540013](E:\文档\GitHub\Notiz\new-chairside 自动均匀性校准新流程及复检界面使用.assets\image-20220715094540013.png)

（`自动Mask的PI`的记录数据放置路径）

![image-20220715094215116](E:\文档\GitHub\Notiz\new-chairside 自动均匀性校准新流程及复检界面使用.assets\image-20220715094215116.png)



5. `自动Mask的PI`过程完成后，弹出如下提示窗口，点击`OK`

![image-20220715094659205](E:\文档\GitHub\Notiz\new-chairside 自动均匀性校准新流程及复检界面使用.assets\image-20220715094659205.png)



（若出现以下问题 `拟合KB失败`，此时需要做一次自动均匀性校准后，再进行`开始自动Mask的PI`）

![image-20220715095047510](E:\文档\GitHub\Notiz\new-chairside 自动均匀性校准新流程及复检界面使用.assets\image-20220715095047510.png)



6. 弹出`拟合KB成功`提示框后，获取自动Mask的PI的过程即完成



#### 六、二次自动均匀性校准

获取自动Mask的PI的过程完成后，需要再做一次自动均匀性校准，应用拟合KB结果（自动均匀性校准过程见前文）。



#### 七、复检

以上所有步骤按流程完成后，即可进行复检

1. **复检界面说明：**

`自动Mask`：调用的mask为自动均匀性校准生成的mask

`手动Mask`：请勿选择该选项！（该项表示调用的mask为手动均匀性校准生成的mask，而系统中并没有手动mask的PI，无法对比光强，所以勿选择）

`无Mask`：不调用mask

![image-20220721145944770](E:\文档\GitHub\Notiz\new-chairside 自动均匀性校准新流程及复检界面使用.assets\image-20220721145944770.png)

`设置能量（自动拟合）`：通过自动光强校准算法拟合出来的光强

`设置能量（手动拟合）`：通过自动mask的PI采集到的数据计算出来的光强

2. **复检界面使用测试步骤：**

   **检测光强：**

   ① 将chairside第3行3列的圆斑图拷贝到优盘中，插入打印机

   ② 选中模式`自动Mask`（默认只允许使用该种模式），点击`选择图片`，选中第①步中的图片进行指定投图

   ③ 选择图片完成后，接着点击`LED ON`

​	   ④ 然后在`设置能量(自动拟合)`或`设置能量（手动拟合）`右边的输入框中输入理想光强数值

​       ⑤ 之后点击`设置能量(自动拟合)`或`设置能量（手动拟合）`选项，即可查看通过算法拟合出来的光强或通过自动mask的PI采集到的数据			计算出来的光强。

​	   ⑥ 记录数据

![image-20220721160859139](E:\文档\GitHub\Notiz\new-chairside 自动均匀性校准新流程及复检界面使用.assets\image-20220721160859139.png)

​		**检测均匀性：**

​		① 点击`开启均匀检测`，料盘中出现圆斑图

![image-20220721150438292](E:\文档\GitHub\Notiz\new-chairside 自动均匀性校准新流程及复检界面使用.assets\image-20220721150438292.png)

​	  ② 将光度计放置在圆斑图上，记录此时的光强，并依次点击后一个，依次记录

​	  ③ 记录数据，并分析极差（幅面内最大光强减去最小光强）



#### 八、备注

1. **更改G-G的拟合方式（1次多项式拟合或2次多项式拟合）**

若需要更改G-G拟合的方式，如1次或2次多项式拟合，则进入到以下路径，打开`autograycalib.json`文件

![image-20220715101133324](E:\文档\GitHub\Notiz\new-chairside 自动均匀性校准新流程及复检界面使用.assets\image-20220715101133324.png)

如下图所示，参数`"gg_degrees"`配置的数值即代表1次多项式拟合或2次多项式拟合

![image-20220715134033793](E:\文档\GitHub\Notiz\new-chairside 自动均匀性校准新流程及复检界面使用.assets\image-20220715134033793.png)

修改后保存，必须重启打印机才能生效。



2. **chairside自动均匀性校准高度设置**

   2.1 插入相机模组

   2.2 进入打印机指定路径的配置文件，进入方法如下：

   ​	2.2.1命令行输入：`heygears@heygears:~$ sudo vim /usr/local/ultracore/.env`

![image-20220713110904261](E:\文档\GitHub\Notiz\new-chairside 自动均匀性校准新流程及复检界面使用.assets\image-20220713110904261.png)

​			2.2.2 接着键盘点击按键`I`，进入编辑模式，移动光标至末行，输入`RESET_FALL=0`

​			2.2.3 然后键盘点击按键`ESC`，退出编辑模式

​			2.2.4 接着英文输入法下输入`:wq`，即可自动退出

​			2.2.5最后重启打印机即可

​		2.3 重启机器后，主轴回到零位（上限位光电传感器的位置），放入高脚千分尺（适配chairside：高度`160mm`——相机模组镜片至料			  盘的高度，镜片周围旁的模组壳体至料盘高度`158.8mm`），不需放入背光膜，若此时千分尺已被压产生示数，则主轴零位设置有			  问题（可能上挡片安装有问题），需联系机械结构同事

​		2.4 进入`平台校准`界面（`平台校准`界面进入步骤如下），选择合适的主轴点动位移设置，点击移动按钮，当千分尺被压范围在		       			  `0.5±0.3mm`时，停止主轴移动，记录主轴下降距离

​			  `平台校准`界面进入步骤：

![image-20220720181236884](E:\文档\GitHub\Notiz\new-chairside 自动均匀性校准新流程及复检界面使用.assets\image-20220720181236884.png)



![image-20220720181302625](E:\文档\GitHub\Notiz\new-chairside 自动均匀性校准新流程及复检界面使用.assets\image-20220720181302625.png)



![image-20220720181336489](E:\文档\GitHub\Notiz\new-chairside 自动均匀性校准新流程及复检界面使用.assets\image-20220720181336489.png)



![image-20220720181533820](E:\文档\GitHub\Notiz\new-chairside 自动均匀性校准新流程及复检界面使用.assets\image-20220720181533820.png)



​		2.5 再次进入步骤2.2，打开打印机指定路径配置文件，将`RESET_FALL=0`删除，并将`CALIB_FALL`参数配置为刚才记录的主轴下降距			   离（同时将`CALIB_FALL`参数和打印机设备编号、相机模组编号一一对应备份记录在数据表中）

​		2.6 重启打印机，复核是否修改成功

​				复核项：

​				2.6.1 观察重启后的打印机主轴停止位置，若此时主轴未停在上限位光电门处，表示`RESET_FALL=0`删除成功

​    		    2.6.2 关闭`相机SN校验`，并进入`自动均匀性校准`步骤（`相机SN校验`及`自动均匀性校准`操作步骤见前文），当自动均匀性校准进度为						`0%`时，关机，沿着相机模组镜头镜片周围旁的模组壳体（勿接触镜片）四周移动一圈，是否偏差在允许范围`±0.3mm`内，						如果偏差在该范围内，则高度调节设置过程成功，否则，需重新调节并设置。



3. **无法显示如下的`Form`调试界面**

   若打印机上插上键盘，在键盘上同时按下`Alt`和`Tab`键，没有显示如下的`Form`调试界面

![image-20220714163638785](E:\文档\GitHub\Notiz\new-chairside 自动均匀性校准新流程及复检界面使用.assets\image-20220714163638785.png)

若没有Form调试界面，则可能该测试插件被放入到了黑名单blacklist中

放出来的方法：

进入到该路径下：

`heygears@heygears:~$ sudo vim ultracore/bin/plugin/.blacklist`

![image-20220721114328866](E:\文档\GitHub\Notiz\new-chairside 自动均匀性校准新流程及复检界面使用.assets\image-20220721114328866.png)

接着键盘点击按键`I`，进入编辑模式，移动光标至在`ultracore_test`前，加上`#`，即可注释掉该项内容

然后键盘点击按键`ESC`，退出编辑模式

接着英文输入法下输入`:wq`，即可自动退出

然后输入`heygears@heygears:~$ cat ultracore/bin/plugin/.blacklist`，查看是否更改成功

最后重启打印机即可

![image-20220714193919987](E:\文档\GitHub\Notiz\new-chairside 自动均匀性校准新流程及复检界面使用.assets\image-20220714193919987.png)

4. 出现以下错误时，表示未配置环境`USE_AUTO_CALIBS=1`

![image-20220725143911128](E:\文档\GitHub\Notiz\new-chairside 自动均匀性校准新流程及复检界面使用.assets\image-20220725143911128.png)







光强拟合数据

`2022-07-14 17:35:26.757 [0x000000556d2b9e80] [graycalib.cpp:1120->QVariant GrayCalib::OnFitGG(const QVariant&)][DEBUG] OnFitGG 1120 autoMask_manPI= QVector(5.47859e-08, -8.85887e-05, 0.164264, -0.619612)`



日志中查找关键字`G_G4K`，数据即为设备灰度，4k的灰度数据

```
G_G4K =  88.9898 , 97.3977
```



G_G的拟合数据：`GG_coeffs= QVector(0.00697209, -0.769471, 120.708)`





chairside上自动均匀性校准模组拍摄图片储存方法：

在`/home/heygears/ultracore/bin`该路径下新建一个tmp文件夹，生成的图片即可储存在该文件夹下，要记得每次删除该文件夹







4K母光源的控制机台（chairside Pro）

`/home/heygears/app/release`

该路径下新建tmp文件夹，模组跑的图片就会存入其中



4K母光源的控制机台（chairside Pro）上日志查看路径`获取P=f(G)关系`

`/home/heygears/.heygears/logs/220726`

`2022-07-26 13:19:44.721 [DEBUG] WriterEEPROM QJsonObject({"100_1500":[-6.454869890148984e-06,0.004198838025331497,-0.5713498592376709,32.304725646972656]`



自动更改环境配置参数

- sed -ie 's/USE_AUTO_CALIBS=0/USE_AUTO_CALIBS=1/g' /usr/local/ultracore/.env



传统手动光度计均匀性校准及光强校准方式下数据存放：

手动mask下的手动PI数据存放位置

![image-20220721111312213](E:\文档\GitHub\Notiz\new-chairside 自动均匀性校准新流程及复检界面使用.assets\image-20220721111312213.png)

做打印之前查看日志确认调用的是自动的还是手动的结果



chairside更新bin文件夹

1. 暂停上下位机运行，才能替换bin文件：命令行输入`sudo killall ultracore-bootloader`

2. 进入到包含bin文件夹的目录下，命令行输入`heygears@heygears:~$ cd ultracore/ `

3. 改变bin文件夹的读写方式，命令行输入`sudo chmod -R 777 bin/ `

4. 即可用新的bin文件夹替换旧的bin文件夹





CS——日志中关键字查看：

1. 设备端：

   1. 自动均匀性校准：

      - 离散数据：电流I（此处电流I的值和 `自动mask手动PI` 中的电流值相同）、灰度avgGrey、newGrey、 LookUpPower
        - 日志关键字`CollectPI`
      - 拟合结果：LookUpPower和电流I
        - 日志关键字`多项式系数:  QVector`

   2. 自动mask手动PI：

      - 离散数据：设备端电流I，光强P

        `OnFitGG P-I`

      - 离散数据：设备端光强P，灰度G，母光源光强P，灰度G

        - `OnFitGG P-I`

      - 拟合结果：设备端电流I、光强P

        `PG_coeff =  QVector`

        `PG4K_coeff =  QVector`

      - 离散数据：光强列表下设备端灰度、母光源灰度

        - `manPower_avgGray`
        - `4[k|K]Power_avgGray`

      - G-G的拟合结果

        - 拟合结果
        - `GG_coeffs std::vector`


**母光源的GP函数无法在cs的日志中查看**



1. 4K母光源：

   - **离散数据：电流I，光强P，灰度G**

   查看方式：4K母光源的控制机台`/home/heygears/app/release`的该路径下新建`tmp`文件夹，模组跑的图片就会存入其中，图片命名方式即为`电流I-光强P-灰度G`

   

   4K母光源上日志查看路径

   `/home/heygears/.heygears/logs/220726`

   `2022-07-26 13:19:44.721 [DEBUG] WriterEEPROM QJsonObject({"100_1500":[-6.454869890148984e-06,0.004198838025331497,-0.5713498592376709,32.304725646972656]`

   

   CSP设备——

   设备端：

   1. 自动均匀性校准：

      - 离散数据：电流I（此处电流I的值和 `自动mask手动PI` 中的电流值相同）、灰度avgGrey、newGrey、 LookUpPower
        - 日志关键字`CollectPI`
      - 拟合结果：LookUpPower和电流I
        - 日志关键字``InsertCoeffs Success to Insercoeffs: QVector``

   2. 自动mask手动PI：

      - 离散数据：设备端电流I，光强P

        `CreatePI 995 P-I`

      - 离散数据：设备端光强P，灰度G，母光源光强P，灰度G

        - `CreatePI 995 P-I`

      - 拟合结果：设备端电流I、光强P

        `PG_coeff =  QVector`

        `PG4K_coeff =  QVector`

      - 离散数据：光强列表下设备端灰度、母光源灰度

        - `manPower_avgGray`
        - `4[k|K]Power_avgGray`

      - G-G的拟合结果

        - 拟合结果
        - `GG_coeffs std::vector`

   3. 4K母光源的GP拟合函数可以在日志中查看

   2022-08-05 16:20:05.022 [DEBUG] CvtGrayToPower 792 `fn_coeffs`= (QVariant(double, -6.89945e-06), QVariant(double, 0.00441767), QVariant(double, -0.604259), QVariant(double, 33.9182))

   

   

**chairside文件路径：**

| 序号                                        | 文件名                     | 文件路径                     |
| ------------------------------------------- | -------------------------- | ---------------------------- |
| 1. 自动mask手动PI时采集的电流I和光强P离散值 | autoenergycalibparams.json | /home/heygears/.clinic       |
| 2. 手动均匀性校准及光强校准数据             | calibration.db             | /home/heygears/ultracore/.db |
| 3. 自动均匀性校准拟合的GG参数               | config.db                  | /home/heygears/ultracore/.db |

 





2. 手动自动均匀性校准及光强校准数据 `/home/heygears/ultracore/.db`

![image-20220815094620894](E:\文档\GitHub\Notiz\new-chairside 自动均匀性校准新流程及复检界面使用.assets\image-20220815094620894.png)



3. 自动均匀性校准拟合的GG参数 `/home/heygears/ultracore/.db`

![image-20220815095101609](E:\文档\GitHub\Notiz\new-chairside 自动均匀性校准新流程及复检界面使用.assets\image-20220815095101609.png)





**chairside pro文件路径：**

| 序号                                        | 文件名                     | 文件路径                         |
| ------------------------------------------- | -------------------------- | -------------------------------- |
| 1. 自动mask手动PI时采集的电流I和光强P离散值 | autoenergycalibparams.json | /home/heygears/.heygears/configs |
| 2. 手动均匀性校准及光强校准数据             | energycalibparams.json     | /home/heygears/.heygears/configs |
| 3. 自动均匀性校准拟合的GG参数               | hg_autocalib.db            | /home/heygears/.heygears/db      |

3. 自动均匀性校准拟合的GG参数 `/home/heygears/.heygears/db`

![image-20220815100241447](E:\文档\GitHub\Notiz\new-chairside 自动均匀性校准新流程及复检界面使用.assets\image-20220815100241447.png)





chairside Pro设备相机模组高度确定

查看slaveconfig.ini文件

![image-20220818131025099](E:\文档\GitHub\Notiz\new-chairside 自动均匀性校准新流程及复检界面使用.assets\image-20220818131025099.png)



DB数据库中无数据时无法更改，先插入数据，再改那个数据即可

`INSERT INTO autocalib_ggcoeffs VALUES (1, 1, 100);`



优盘路径

![image-20220822115316609](E:\文档\GitHub\Notiz\new-chairside 自动均匀性校准新流程及复检界面使用.assets\image-20220822115316609.png)



先获取db文件夹的读写权限

chairside pro更改db中的GG参数后，必须重启才能生效

重启后日志中会读取gg参数：`Run 138 key_GG_coeffs`

cs :  `gg_coeffs_list`——必须做了自动均匀性校准才会打印出该参数



Linux中拷贝文件

优盘路径：/mnt/HJ1131/heygears

sudo cp  待复制的文件  优盘路径

