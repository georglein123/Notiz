- 打印厚度测试
  - 在指定光强下（工艺包中指定的光强），曝光不同时间，获得使得固化厚度大于100mm的时间
    - 使用U盘指定投图，投均匀性校准中的第38张图，在上位机高级设置中设置曝光时间，用测厚仪测量固化厚度，用excel记录下来
- 修改工艺包参数
  - 将工艺包进行解密，然后修改，修改完成后再加密
    - 更改参数：曝光能量，曝光时间
    - 更改的全流程整理一下
  - 完成后的文件夹使用工艺包打包工具打包后才能导入机器中使用
- 将模型文件导入机器中进行打印
  - 模型文件的制作、切片



**LCD打印机配置文件中关于剥离时间和剥离力配置**

```c++
[photometer]
serialport=/dev/uart_pho
[network]
device=enp3s0
[interface]
ip=192.168.3.200
mask=255.255.255.0
gateway=192.168.3.1
[comm]
type=0
serialport=/dev/uart_main_slave
ip=127.0.0.1
port=9999
[cover_axis]
speed = 150
[z_axis]
speedcoeff=4
distancecoeff=4

reset_falldistance = 0

reset_speed1=9000
reset_speed2=1250
reset_timeout=60

zero_speed1=9000
zero_distance1=-165000
zero_speed2=2000
zero_distance2=-12000
zero_speed3=50
zero_residue_dis=100
zero_maxforce=35
zero_minforce=15
zero_delaytime=3000
zero_timeout=360
zero_protect_dis=300

zero_gingva_speed1=6500
zero_gingva_distance1=-136500
zero_gingva_speed2=500
zero_gingva_distance2=-12000
zero_gingva_speed3 = 25
zero_gingva_residue_dis = 30
zero_gingva_maxforce=30
zero_gingva_minforce=20
zero_gingva_delaytime=5000
zero_gingva_timeout=360
zero_gingva_protect_dis = 300

segment_timeout=20 #剥离时间阈值

#打印机复位时点动移动时的参数设置，防止打印机突然大幅移动
peel_speed1=250
peel_distance1=1200
peel_distance2=2000000
peel_timeout1=20
peel_timeout2=60

relative_speed=4000

[consttemp]
wavedistance=50
wavespeed =4000
enable = true

[systemparam]
pid_fast_temp1 = 700
pid_keep_temp1 = 400
pid_fast_temp2 = 200
pid_keep_temp2 = 250
pid_protect_temp = 1000

z_axis_factor = 4
z_max_step = 300000

force_factor = 4300
max_pressure = -150 #最大压力
max_pull = 800  #剥离最大拉力
max_protect_force = -200
platform_force = -5
zero_decel_force = -20

c_max_step =200000
c_decel_step = 54463
c_normal_speed = 5000
c_decel_speed = 1000
z_emerg_delay = 600
zero_force_err_times = 1

device_id	= 1


[lamp]
enable = true


[tray]
enable = false

```



**打印机软件系统查看工艺包及删除方法**

1. 进入文件系统`/home/heygears/.a2d/db`
2. 使用软件`DB Browser for SQLite` 软件打开`hg_techbag.db`
3. 点击“浏览数据”选项卡，在“表”的下拉列表中选择“pp”，即可查看该打印机中的工艺包
4. 更改完成后的文件保存后要将打印机断电并重启后生效





### 出错：

- 现象：打印出的一版四个寄存牙模，每一个寄存牙模在模型中间部分很薄，紧贴成型平台，无法用铲刀铲下，只能用美工刀刮下，而寄存牙模周围较厚，可以用铲刀铲下
- 分析原因：层无法剥离，由于料盘使用的是绷膜料盘，曝光时打印物体粘接在绷膜和成型平台中间，剥离时成型平台上移，也会拉动绷膜上移，成型平台上移距离太短就会导致无法剥离开
- 解决办法：修改工艺包参数，将截面识别每一大段Number中的位移距离增大，使成型平台移动足够距离
  - 注意：截面识别每一大段Number中有5段对应不同速度段，虽然把5段中最后一段的距离增大了，该Number段的总体位移增大了，但是无法判断绷膜料盘在该Number段的5个小段中哪段发生剥离的，假如在第3段速度中没有剥离而是在第4段速度中剥离，而第4段速度又突然增大，则易发生剥离异常。所以5段中前4段的速度值尽量平滑。




- 现象：屏幕弹出“剥离失败”信息
- 分析原因：剥离失败的原因有
  - 剥离时的拉力过大
  - 剥离时的时间过长
  - 整段行程运行时间过长
- 解决办法：
  - 修改工艺包参数，尤其需关注截面占比每段中的关于剥离段的速度、行程参数设置
  - 将工艺包中截面占比的每段中的速度增大，使得剥离时间减小

错误信息

![image-20220113115455434](E:\文档\GitHub\Notiz\study model打印测试.assets\image-20220113115455434.png)

分析：

第60层P1

![第60层](E:\文档\GitHub\Notiz\study model打印测试.assets\S000060_P1.png)

第60层P2

![S000060_P2](E:\文档\GitHub\Notiz\study model打印测试.assets\S000060_P2.png)

第61层

![S000061_P1](E:\文档\GitHub\Notiz\study model打印测试.assets\S000061_P1.png)

第61层P2

![S000061_P2](E:\文档\GitHub\Notiz\study model打印测试.assets\S000061_P2.png)

日志信息

```c
[2022-01-13 10:24:11.532][INFO] layer: 60 begin
[2022-01-13 10:24:11.528][DEBUG] --------
[2022-01-13 10:24:11.539][INFO] Preprocessing
[2022-01-13 10:24:11.542][DEBUG] [ "LCD-925-寄存牙模-100um.ult" ] layer start: 60 / 442
[2022-01-13 10:24:11.543][DEBUG] handle base and get ELayerImgType_Object
[2022-01-13 10:24:11.548][WARN] SendSyncLocalMsg 436 disconnect ultranet, donot publish intermediate state!
[2022-01-13 10:24:11.543][INFO] Exposuring
[2022-01-13 10:24:11.548][DEBUG] [ "LCD-925-寄存牙模-100um.ult" ] step: PrintCtrl::Preprocessing
[2022-01-13 10:24:11.552][DEBUG] the current is:  1000
[2022-01-13 10:24:11.558][TRACE] ULT: other Layer
[2022-01-13 10:24:11.562][INFO] paint screen
[2022-01-13 10:24:11.564][DEBUG] [ "LCD-925-寄存牙模-100um.ult" ] step: PrintCtrl::Exposuring
[2022-01-13 10:24:11.566][TRACE] command: "ac102301ff00000101ac61acdc"
[2022-01-13 10:24:11.572][TRACE] enableSupportFixed
[2022-01-13 10:24:11.573][INFO] set current is ok
[2022-01-13 10:24:11.583][TRACE] exe result: "35->" "COMMAND_SUCCESS"
[2022-01-13 10:24:11.588][INFO] led on
[2022-01-13 10:24:12.092][DEBUG] src_mat fixed ... 2
[2022-01-13 10:24:12.097][DEBUG] src_mat fixed ... 0 "/tmp/.A2DTemp/S000065_P1.png"
[2022-01-13 10:24:12.271][TRACE] support_fixed: layerImgType 0
[2022-01-13 10:24:12.287][DEBUG] bObjImg  true
[2022-01-13 10:24:12.291][DEBUG] wearhole scale  false
[2022-01-13 10:24:12.472][DEBUG] ZoomIn Success to transform the image: 5789 3618 1.005 1.005
[2022-01-13 10:24:12.478][DEBUG] ShapeAdjust completed ...
[2022-01-13 10:24:12.762][DEBUG] LCDConversion 350 input projecotr type: "pj623" 3600 5760
[2022-01-13 10:24:12.775][DEBUG] LCDConversion 363 projecotr type: "pj623" 3600 5760
[2022-01-13 10:24:13.605][TRACE] operator() 78 auto close cover time out!
[2022-01-13 10:24:13.615][DEBUG] [frontmonitor] send autoclose cover notice
[2022-01-13 10:24:14.237][DEBUG] src_mat fixed ... 1 "/tmp/.A2DTemp/S000065_P2.png"
[2022-01-13 10:24:14.407][TRACE] support_fixed: layerImgType 1
[2022-01-13 10:24:14.413][DEBUG] bObjImg  false
[2022-01-13 10:24:14.564][DEBUG] ZoomIn Success to transform the image: 5789 3618 1.005 1.005
[2022-01-13 10:24:14.572][DEBUG] ShapeAdjust completed ...
[2022-01-13 10:24:14.874][DEBUG] LCDConversion 350 input projecotr type: "pj623" 3600 5760
[2022-01-13 10:24:14.880][DEBUG] LCDConversion 363 projecotr type: "pj623" 3600 5760
[2022-01-13 10:24:15.645][DEBUG] the current is:  1000
[2022-01-13 10:24:15.646][INFO] paint screen
[2022-01-13 10:24:15.654][INFO] set current is ok
[2022-01-13 10:24:16.220][DEBUG] elecon_flag  true 1000 100 65
[2022-01-13 10:24:16.239][TRACE] command: "ac102301ff000001006ca0acdc"
[2022-01-13 10:24:16.239][INFO] clear screen
[2022-01-13 10:24:16.249][TRACE] exe result: "35->" "COMMAND_SUCCESS"
[2022-01-13 10:24:16.254][DEBUG] begin SyncPeel
[2022-01-13 10:24:16.254][DEBUG] [ "LCD-925-寄存牙模-100um.ult" ] step: PrintCtrl::Peeling
[2022-01-13 10:24:16.254][INFO] led off
[2022-01-13 10:24:16.259][TRACE] command: "ac100118ff00000400000001d227acdc"
[2022-01-13 10:24:16.254][TRACE] OnEnviromentCheck 56 data: QMap(("Projector", QVariant(bool, true))("Screen", QVariant(bool, true)))
[2022-01-13 10:24:16.262][INFO] Peeling
[2022-01-13 10:24:16.266][INFO] peel up (speed) params: [300, 800, 4000, 4000, 4000], (distance)params: [5000, 8000, 10000, 10000, 10000]
[2022-01-13 10:24:16.270][INFO] peel down (speed) params: [4000, 1000, 1000, 1000, 1000], (distance)params: [-3000, -9900, -9900, -9900, -9900]
[2022-01-13 10:24:16.303][TRACE] Slave State change:  "ES-0 OPR-0 OPL-0 NP-0 ZT-0 ZB-0 ZS-0 ZR-0 ZZ-1 ZP-1 CAU-0 CAL-0 CGU-0 CGD-0 TL-1 CAE-0 ZAE-0 SP-1 TS-0 SP2-0 ST-0 PID-0"  | F- "0.62"  | lts- "1130"  | rts- "2326"  | lbs- "975"  | rbs- "1848"
[2022-01-13 10:24:32.953][TRACE] Slave Raw Log >>{  "segMove:num 1|f 0|s 20000"  }<<
[2022-01-13 10:24:34.232][TRACE] exe result: "ZAXIS->SEGMENTED_MOTION" "COMMAND_SUCCESS"
[2022-01-13 10:24:34.238][DEBUG] end SyncPeel
[2022-01-13 10:24:34.244][DEBUG] begin SyncPeel
[2022-01-13 10:24:34.248][TRACE] command: "ac100118ff00000400000002d367acdc"
[2022-01-13 10:24:41.924][TRACE] exe result: "ZAXIS->SEGMENTED_MOTION" "COMMAND_SUCCESS"
[2022-01-13 10:24:41.930][DEBUG] end SyncPeel
[2022-01-13 10:24:41.931][TRACE] Slave State change:  "ES-0 OPR-0 OPL-0 NP-0 ZT-0 ZB-0 ZS-1 ZR-0 ZZ-1 ZP-0 CAU-0 CAL-0 CGU-0 CGD-0 TL-1 CAE-0 ZAE-0 SP-1 TS-0 SP2-0 ST-0 PID-0"  | F- "-9.14"  | lts- "1136"  | rts- "2327"  | lbs- "975"  | rbs- "1846"
[2022-01-13 10:24:41.936][DEBUG] [ "LCD-925-寄存牙模-100um.ult" ] step: PrintCtrl::Waiting
[2022-01-13 10:24:41.937][INFO] Peeling result: COMMAND_SUCCESS
[2022-01-13 10:24:41.942][INFO] Waiting
[2022-01-13 10:24:41.946][INFO] wait 400ms
[2022-01-13 10:24:42.337][DEBUG] [ "LCD-925-寄存牙模-100um.ult" ] layer done
[2022-01-13 10:24:42.339][DEBUG] Start Image Process,Layer:  66
[2022-01-13 10:24:42.340][INFO] layer: 60 end
[2022-01-13 10:24:42.356][DEBUG] --------
[2022-01-13 10:24:42.363][DEBUG] handle base and get ELayerImgType_Object
```



第61层

```c
[2022-01-13 10:24:42.365][INFO] layer: 61 begin
[2022-01-13 10:24:42.371][DEBUG] [ "LCD-925-寄存牙模-100um.ult" ] layer start: 61 / 442
[2022-01-13 10:24:42.376][TRACE] ULT: other Layer
[2022-01-13 10:24:42.378][DEBUG] the current is:  1000
[2022-01-13 10:24:42.379][INFO] Preprocessing
[2022-01-13 10:24:42.383][DEBUG] [ "LCD-925-寄存牙模-100um.ult" ] step: PrintCtrl::Preprocessing
[2022-01-13 10:24:42.384][WARN] SendSyncLocalMsg 436 disconnect ultranet, donot publish intermediate state!
[2022-01-13 10:24:42.388][TRACE] enableSupportFixed
[2022-01-13 10:24:42.389][TRACE] command: "ac102301ff00000101ac61acdc"
[2022-01-13 10:24:42.393][DEBUG] [ "LCD-925-寄存牙模-100um.ult" ] step: PrintCtrl::Exposuring
[2022-01-13 10:24:42.390][INFO] Exposuring
[2022-01-13 10:24:42.407][TRACE] exe result: "35->" "COMMAND_SUCCESS"
[2022-01-13 10:24:42.409][INFO] paint screen
[2022-01-13 10:24:42.415][INFO] set current is ok
[2022-01-13 10:24:42.421][INFO] led on
[2022-01-13 10:24:42.916][DEBUG] src_mat fixed ... 2
[2022-01-13 10:24:42.930][DEBUG] src_mat fixed ... 0 "/tmp/.A2DTemp/S000066_P1.png"
[2022-01-13 10:24:43.083][TRACE] support_fixed: layerImgType 0
[2022-01-13 10:24:43.088][DEBUG] bObjImg  true
[2022-01-13 10:24:43.115][DEBUG] wearhole scale  false
[2022-01-13 10:24:43.312][DEBUG] ZoomIn Success to transform the image: 5789 3618 1.005 1.005
[2022-01-13 10:24:43.326][DEBUG] ShapeAdjust completed ...
[2022-01-13 10:24:43.618][DEBUG] LCDConversion 350 input projecotr type: "pj623" 3600 5760
[2022-01-13 10:24:43.624][DEBUG] LCDConversion 363 projecotr type: "pj623" 3600 5760
[2022-01-13 10:24:45.331][DEBUG] src_mat fixed ... 1 "/tmp/.A2DTemp/S000066_P2.png"
[2022-01-13 10:24:45.489][TRACE] support_fixed: layerImgType 1
[2022-01-13 10:24:45.503][DEBUG] bObjImg  false
[2022-01-13 10:24:45.731][DEBUG] ZoomIn Success to transform the image: 5789 3618 1.005 1.005
[2022-01-13 10:24:45.745][DEBUG] ShapeAdjust completed ...
[2022-01-13 10:24:45.943][DEBUG] LCDConversion 350 input projecotr type: "pj623" 3600 5760
[2022-01-13 10:24:45.957][DEBUG] LCDConversion 363 projecotr type: "pj623" 3600 5760
[2022-01-13 10:24:46.442][DEBUG] the current is:  1000
[2022-01-13 10:24:46.443][INFO] paint screen
[2022-01-13 10:24:46.452][INFO] set current is ok
[2022-01-13 10:24:47.061][TRACE] command: "ac102301ff000001006ca0acdc"
[2022-01-13 10:24:47.061][INFO] clear screen
[2022-01-13 10:24:47.071][TRACE] exe result: "35->" "COMMAND_SUCCESS"
[2022-01-13 10:24:47.077][DEBUG] begin SyncPeel
[2022-01-13 10:24:47.078][DEBUG] [ "LCD-925-寄存牙模-100um.ult" ] step: PrintCtrl::Peeling
[2022-01-13 10:24:47.078][INFO] led off
[2022-01-13 10:24:47.078][TRACE] OnEnviromentCheck 56 data: QMap(("Projector", QVariant(bool, true))("Screen", QVariant(bool, true)))
[2022-01-13 10:24:47.083][TRACE] command: "ac100118ff00000400000001d227acdc"
[2022-01-13 10:24:47.087][INFO] Peeling
[2022-01-13 10:24:47.091][INFO] peel up (speed) params: [300, 800, 4000, 4000, 4000], (distance)params: [5000, 8000, 10000, 10000, 10000]
[2022-01-13 10:24:47.095][INFO] peel down (speed) params: [4000, 1000, 1000, 1000, 1000], (distance)params: [-3000, -9900, -9900, -9900, -9900]
[2022-01-13 10:24:47.127][TRACE] Slave State change:  "ES-0 OPR-0 OPL-0 NP-0 ZT-0 ZB-0 ZS-0 ZR-0 ZZ-1 ZP-1 CAU-0 CAL-0 CGU-0 CGD-0 TL-1 CAE-0 ZAE-0 SP-1 TS-0 SP2-0 ST-0 PID-0"  | F- "0.55"  | lts- "1128"  | rts- "2321"  | lbs- "972"  | rbs- "1841"
[2022-01-13 10:24:47.455][DEBUG] elecon_flag  true 1000 100 66
[2022-01-13 10:25:07.105][TRACE] Tick overtime: "ZAXIS->SEGMENTED_MOTION"
[2022-01-13 10:25:07.105][DEBUG] end SyncPeel
[2022-01-13 10:25:07.113][ERROR] peel up failed!
[2022-01-13 10:25:07.114][TRACE] command: "ac102304ff0000010039a0acdc"
[2022-01-13 10:25:07.119][ERROR] Peeling result: COMMAND_TIMEOUT
[2022-01-13 10:25:07.125][TRACE] exe result: "35->" "COMMAND_SUCCESS"
[2022-01-13 10:25:07.130][DEBUG] [ModelParser] current buffer size 5
[2022-01-13 10:25:07.135][DEBUG] image process is broke off, model parser finished;
[2022-01-13 10:25:07.152][DEBUG] Close Model Parser Finished!
[2022-01-13 10:25:07.174][DEBUG] print process result: PrintCtrl::PeelError
[2022-01-13 10:25:07.178][ERROR] print error: PrintCtrl::PeelError
[2022-01-13 10:25:07.182][TRACE] 任务失败
[2022-01-13 10:25:08.341][TRACE] Slave State change:  "ES-0 OPR-0 OPL-0 NP-0 ZT-0 ZB-0 ZS-1 ZR-0 ZZ-1 ZP-0 CAU-0 CAL-0 CGU-0 CGD-0 TL-1 CAE-0 ZAE-0 SP-1 TS-0 SP2-0 ST-0 PID-0"  | F- "0.37"  | lts- "1087"  | rts- "2323"  | lbs- "1037"  | rbs- "1843"
[2022-01-13 10:25:13.772][DEBUG] AdjustPlatform "CoverAxisDownSlowly"
[2022-01-13 10:25:13.778][TRACE] command: "ac101101ff000004fffffc183901acdc"
[2022-01-13 10:25:13.881][WARN] "Start"  Fail 3
[2022-01-13 10:25:13.996][WARN] "Start"  Fail 2
[2022-01-13 10:25:14.115][WARN] "Start"  Fail 1
[2022-01-13 10:25:14.120][DEBUG] AdjustPlatform xxxxxxxxxxxxx : false
[2022-01-13 10:26:14.618][DEBUG] "eth0" --> State changed: "NetworkDeviceStatePrepare" : "NetworkDeviceStateReasonNone"
[2022-01-13 10:26:14.640][DEBUG] "eth0" --> State changed: "NetworkDeviceStateConfig" : "NetworkDeviceStateReasonNone"
[2022-01-13 10:26:14.672][DEBUG] "eth0" --> State changed: "NetworkDeviceStateFailed" : "NetworkDeviceStateReasonConfigFailed"
[2022-01-13 10:26:14.702][DEBUG] "eth0" --> State changed: "NetworkDeviceStateDisconnected" : "NetworkDeviceStateReasonNone"
[2022-01-13 10:26:14.729][WARN] "No such interface 'org.freedesktop.DBus.Properties' on object at path /org/freedesktop/NetworkManager/ActiveConnection/33"
[2022-01-13 10:26:14.735][DEBUG] "eth0" --> State changed: "NetworkDeviceStatePrepare" : "NetworkDeviceStateReasonNone"
[2022-01-13 10:26:14.742][DEBUG] "eth0" --> State changed: "NetworkDeviceStateConfig" : "NetworkDeviceStateReasonNone"
[2022-01-13 10:26:14.749][DEBUG] "eth0" --> State changed: "NetworkDeviceStateFailed" : "NetworkDeviceStateReasonConfigFailed"
[2022-01-13 10:26:14.755][DEBUG] "eth0" --> State changed: "NetworkDeviceStateDisconnected" : "NetworkDeviceStateReasonNone"
[2022-01-13 10:26:14.764][DEBUG] "eth0" --> State changed: "NetworkDeviceStatePrepare" : "NetworkDeviceStateReasonNone"
[2022-01-13 10:26:14.772][DEBUG] "eth0" --> State changed: "NetworkDeviceStateConfig" : "NetworkDeviceStateReasonNone"
[2022-01-13 10:26:14.786][DEBUG] "eth0" --> State changed: "NetworkDeviceStateFailed" : "NetworkDeviceStateReasonConfigFailed"
[2022-01-13 10:26:14.793][DEBUG] "eth0" --> State changed: "NetworkDeviceStateDisconnected" : "NetworkDeviceStateReasonNone"
[2022-01-13 10:26:14.800][DEBUG] "eth0" --> State changed: "NetworkDeviceStatePrepare" : "NetworkDeviceStateReasonNone"
[2022-01-13 10:26:14.807][DEBUG] "eth0" --> State changed: "NetworkDeviceStateConfig" : "NetworkDeviceStateReasonNone"
[2022-01-13 10:26:14.813][DEBUG] "eth0" --> State changed: "NetworkDeviceStateFailed" : "NetworkDeviceStateReasonConfigFailed"
[2022-01-13 10:26:14.819][DEBUG] "eth0" --> State changed: "NetworkDeviceStateDisconnected" : "NetworkDeviceStateReasonNone"
[2022-01-13 10:28:57.756][DEBUG] begin reposit| ResetProcess
[2022-01-13 10:28:57.779][INFO] Resetting
```



- 现象：打印件出现裂缝缺口

![image-20220119145525298](E:\文档\GitHub\Notiz\study model打印测试.assets\image-20220119145525298.png)

- 分析原因：
  - 推测：层与层之间粘接不牢固，导致打印脱离
    - 原因：曝光时间不够，固化程度不足
  - 推测：打印层剥离时，成型平台中间部分未与离型膜完全剥离开
    - 原因：绷膜料盘剥离时，在成型平台上升时一起上升，在成型平台的中间部分最难剥离
- 解决办法：
  - 修改工艺包中的曝光时间，增加曝光时间
  - 修改工艺包中的截面识别每一段Number中的总行程距离，增加行程距离，同时还要考虑到截面识别每一段Number中各个小段的速度不要突然增大
  - 





