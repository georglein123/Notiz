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





出错：

- 现象：打印出的一版四个寄存牙模，每一个寄存牙模在模型中间部分很薄，紧贴成型平台，无法用铲刀铲下，只能用美工刀刮下，而寄存牙模周围较厚，可以用铲刀铲下
- 分析原因：层无法剥离
- 解决办法：修改工艺包参数，将截面识别每一段中的位移距离增大，使成型平台移动足够距离



- 现象：屏幕弹出“剥离失败”信息
- 分析原因：剥离失败的原因有
  - 剥离时的拉力过大
  - 剥离时的时间过长
  - 整段行程运行时间过长
- 解决办法：
  - 修改工艺包参数，尤其需关注截面占比每段中的关于剥离段的速度、行程参数设置





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











