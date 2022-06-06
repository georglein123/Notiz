电脑连接打印机后台

将打印机用网线连接起来

打开打印机的网络设置，点击“静态IP”，获取打印机的IP地址

主机：输入打印机的IP地址

![image-20220407161842460](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20220407161842460.png)

点击“用户身份验证”，输入用户名：heygears，密码：heygears，然后点击连接，即可连接打印机

![image-20220407162044406](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20220407162044406.png)

然后点击菜单栏中的绿色图标，即可进入打印机后台文件系统

![image-20220407162255718](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20220407162255718.png)

然后进入下图中所示的文件路径，即可进入到日志中

![image-20220407162417435](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20220407162417435.png)



A2D日志相关信息阅读：

```cassandra
[2022-05-31 14:54:13.856] [DEBUG] [ "m108.ult" ] step: PrintCtrl::PrintStep(Preprocessing)
[2022-05-31 14:54:13.856] [DEBUG] the buffer is not Empty
[2022-05-31 14:54:13.856] [DEBUG] Read Model Parser Finished!
[2022-05-31 14:54:13.856] [DEBUG] - 28 - [exposure][begin]
[2022-05-31 14:54:13.856] [DEBUG] --------
[2022-05-31 14:54:13.856] [TRACE] [ProjectCtrl] OnExposure
[2022-05-31 14:54:13.856] [DEBUG] [ "m108.ult" ] layer start: 28 / 30
[2022-05-31 14:54:13.856] [TRACE] previewImg show time is  0
[2022-05-31 14:54:13.857] [DEBUG] [ "m108.ult" ] step: PrintCtrl::PrintStep(Exposuring)
[2022-05-31 14:54:13.857] [TRACE] Discard Led Eff:  "LE_UNCOVERED"
[2022-05-31 14:54:13.862] [TRACE] PublishMsgProcess 675 msgkey: "1006"
[2022-05-31 14:54:13.880] [TRACE] [ProjectCtrl] the current is: 309
[2022-05-31 14:54:13.880] [TRACE] [Projector] LedOn
[2022-05-31 14:54:13.881] [TRACE] [Ddp442x] setLedOnOff
[2022-05-31 14:54:13.881] [TRACE] [Ddp442xApi] GpioOpen
[2022-05-31 14:54:13.881] [TRACE] [Ddp442xApi] OpenWithRetry interfacenum: 2 , pre2retry: 3
[2022-05-31 14:54:13.882] [TRACE] SetLedOnOff
[2022-05-31 14:54:13.884] [TRACE] [ProjectorInterface] open_led success
[2022-05-31 14:54:13.885] [DEBUG] [Projector] LedOn result: no support
[2022-05-31 14:54:13.885] [TRACE] [ProjectCtrl] OnExposure preset time: 1500
[2022-05-31 14:54:15.386] [TRACE] [ProjectCtrl] [exposure][time]: 1528
[2022-05-31 14:54:15.387] [TRACE] [Projector] LedOff
[2022-05-31 14:54:15.387] [TRACE] [Ddp442x] setLedOnOff
[2022-05-31 14:54:15.388] [TRACE] [Ddp442xApi] GpioOpen
[2022-05-31 14:54:15.389] [TRACE] [Ddp442xApi] OpenWithRetry interfacenum: 2 , pre2retry: 3
[2022-05-31 14:54:15.390] [TRACE] SetLedOnOff
[2022-05-31 14:54:15.390] [TRACE] [ProjectorInterface] close_led success
[2022-05-31 14:54:15.392] [DEBUG] [Projector] LedOff result: no support
[2022-05-31 14:54:15.429] [TRACE] OnEnviromentCheck 57 data: QMap(("Projector", QVariant(bool, true))("Screen", QVariant(bool, true)))
[2022-05-31 14:54:15.429] [TRACE] - 28 - [exposure][time] 1573 [exposure][offset time] 73
[2022-05-31 14:54:15.429] [DEBUG] begin SyncPeel
[2022-05-31 14:54:15.429] [DEBUG] [ "m108.ult" ] step: PrintCtrl::PrintStep(Peeling)
[2022-05-31 14:54:15.429] [TRACE] command: "ac100118ff00000400000001d227acdc"
[2022-05-31 14:54:15.465] [DEBUG] NotifyComm 通訊返回 "ac100118ff00000400000001d227acdc"
[2022-05-31 14:54:15.536] [TRACE] Slave State change:  "ES-0 OPR-0 OPL-0 NP-1 ZT-0 ZB-0 ZS-0 ZR-0 ZZ-1 ZP-1 CAU-1 CAL-0 CGU-1 CGD-0 TL-1 CAE-0 ZAE-0 SP-1 ST-1 HES-1"  | F- "-93.30"
[2022-05-31 14:54:16.136] [TRACE] Slave State change:  "ES-0 OPR-0 OPL-0 NP-0 ZT-0 ZB-0 ZS-0 ZR-0 ZZ-1 ZP-1 CAU-1 CAL-0 CGU-1 CGD-0 TL-1 CAE-0 ZAE-0 SP-1 ST-1 HES-1"  | F- "1.20"
[2022-05-31 14:54:20.531] [TRACE] slave:
[2022-05-31 14:54:20.531] [TRACE] 	 |--- plateform: 1
[2022-05-31 14:54:20.532] [TRACE] 	 |--- force: 0.6
[2022-05-31 14:54:20.532] [TRACE] heaint:
[2022-05-31 14:54:20.533] [TRACE] 	 |--- temp: 23.56
[2022-05-31 14:54:20.573] [TRACE] PublishMsgProcess 675 msgkey: "1002"
[2022-05-31 14:54:29.117] [TRACE] exe result: "ZAXIS->SEGMENTED_MOTION" "COMMAND_SUCCESS"
[2022-05-31 14:54:29.118] [DEBUG] end SyncPeel
[2022-05-31 14:54:29.118] [TRACE] Escape 0 1376520
[2022-05-31 14:54:29.118] [DEBUG] begin SyncPeel
[2022-05-31 14:54:29.119] [TRACE] command: "ac100118ff00000400000002d367acdc"
[2022-05-31 14:54:29.137] [DEBUG] discard slave return result 
[2022-05-31 14:54:29.156] [DEBUG] discard slave return result 
[2022-05-31 14:54:29.174] [TRACE] Slave State change:  "ES-0 OPR-0 OPL-0 NP-0 ZT-0 ZB-0 ZS-1 ZR-0 ZZ-1 ZP-0 CAU-1 CAL-0 CGU-1 CGD-0 TL-1 CAE-0 ZAE-0 SP-1 ST-1 HES-1"  | F- "0.10"
[2022-05-31 14:54:29.192] [DEBUG] NotifyComm 通訊返回 "ac100118ff00000400000002d367acdc"
[2022-05-31 14:54:29.236] [TRACE] Slave State change:  "ES-0 OPR-0 OPL-0 NP-0 ZT-0 ZB-0 ZS-0 ZR-0 ZZ-1 ZP-1 CAU-1 CAL-0 CGU-1 CGD-0 TL-1 CAE-0 ZAE-0 SP-1 ST-1 HES-1"  | F- "0.00"
[2022-05-31 14:54:30.532] [TRACE] slave:
[2022-05-31 14:54:30.533] [TRACE] 	 |--- force: -0.1
[2022-05-31 14:54:30.533] [TRACE] 	 |--- temp: 24.64
[2022-05-31 14:54:30.534] [TRACE] 	 |--- humidity: 59.57
[2022-05-31 14:54:30.534] [TRACE] heaint:
[2022-05-31 14:54:30.535] [TRACE] 	 |--- temp: 23.88
[2022-05-31 14:54:30.588] [TRACE] PublishMsgProcess 675 msgkey: "1002"
[2022-05-31 14:54:30.936] [TRACE] Slave State change:  "ES-0 OPR-0 OPL-0 NP-1 ZT-0 ZB-0 ZS-0 ZR-0 ZZ-1 ZP-1 CAU-1 CAL-0 CGU-1 CGD-0 TL-1 CAE-0 ZAE-0 SP-1 ST-1 HES-1"  | F- "-18.00"
[2022-05-31 14:54:32.667] [TRACE] exe result: "ZAXIS->SEGMENTED_MOTION" "COMMAND_SUCCESS"
[2022-05-31 14:54:32.668] [DEBUG] end SyncPeel
[2022-05-31 14:54:32.669] [TRACE] Escape 0 1376520
[2022-05-31 14:54:32.670] [TRACE] [PrintCtrl] peel up: Curlayer: 28 Number: "13"
[2022-05-31 14:54:32.671] [TRACE] [PrintCtrl] speed[0]: 300, distance[0]: 1600
[2022-05-31 14:54:32.671] [TRACE] [PrintCtrl] speed[1]: 300, distance[1]: 2400
[2022-05-31 14:54:32.672] [TRACE] [PrintCtrl] speed[2]: 300, distance[2]: 3600
[2022-05-31 14:54:32.673] [TRACE] [PrintCtrl] speed[3]: 6000, distance[3]: 12900
[2022-05-31 14:54:32.673] [TRACE] [PrintCtrl] speed[4]: 6000, distance[4]: 12900
[2022-05-31 14:54:32.674] [TRACE] [PrintCtrl] peel down: Curlayer: 28 Number: "13"
[2022-05-31 14:54:32.675] [TRACE] [PrintCtrl] speed[0]: 6000, distance[0]: -12000
[2022-05-31 14:54:32.675] [TRACE] [PrintCtrl] speed[1]: 500, distance[1]: -12850
[2022-05-31 14:54:32.676] [TRACE] [PrintCtrl] speed[2]: 500, distance[2]: -12850
[2022-05-31 14:54:32.676] [TRACE] [PrintCtrl] speed[3]: 500, distance[3]: -12850
[2022-05-31 14:54:32.677] [TRACE] [PrintCtrl] speed[4]: 500, distance[4]: -12850
[2022-05-31 14:54:32.677] [TRACE] - 28 - [peel][time] 17241 [peel][offset time] -8
[2022-05-31 14:54:32.678] [DEBUG] [ "m108.ult" ] step: PrintCtrl::PrintStep(Waiting)
[2022-05-31 14:54:32.736] [TRACE] Slave State change:  "ES-0 OPR-0 OPL-0 NP-1 ZT-0 ZB-0 ZS-1 ZR-0 ZZ-1 ZP-0 CAU-1 CAL-0 CGU-1 CGD-0 TL-1 CAE-0 ZAE-0 SP-1 ST-1 HES-1"  | F- "-106.50"
[2022-05-31 14:54:40.532] [TRACE] slave:
[2022-05-31 14:54:40.532] [TRACE] 	 |--- plateform: -1
[2022-05-31 14:54:40.533] [TRACE] 	 |--- force: -93.4
[2022-05-31 14:54:40.533] [TRACE] 	 |--- temp: 24.79
[2022-05-31 14:54:40.534] [TRACE] 	 |--- humidity: 59.65
[2022-05-31 14:54:40.535] [TRACE] heaint:
[2022-05-31 14:54:40.535] [TRACE] 	 |--- temp: 22.99
[2022-05-31 14:54:40.600] [TRACE] PublishMsgProcess 675 msgkey: "1002"
[2022-05-31 14:54:42.170] [TRACE] - 28 - [wait][time] 9500 [wait][offset time] 0
[2022-05-31 14:54:42.170] [TRACE]  ====== Begin Read Model  29 `th Loop ====== 
[2022-05-31 14:54:42.170] [DEBUG] [ "m108.ult" ] layer done
[2022-05-31 14:54:42.170] [DEBUG] ReadModel 291
[2022-05-31 14:54:42.170] [DEBUG] the buffer is not Empty
[2022-05-31 14:54:42.170] [DEBUG] [ "m108.ult" ] step: PrintCtrl::PrintStep(Preprocessing)
[2022-05-31 14:54:42.170] [DEBUG] Read Model Parser Finished!
[2022-05-31 14:54:42.170] [DEBUG] --------
[2022-05-31 14:54:42.170] [DEBUG] - 29 - [exposure][begin]
[2022-05-31 14:54:42.170] [DEBUG] [ "m108.ult" ] layer start: 29 / 30
[2022-05-31 14:54:42.170] [TRACE] [ProjectCtrl] OnExposure
[2022-05-31 14:54:42.171] [TRACE] Discard Led Eff:  "LE_UNCOVERED"
[2022-05-31 14:54:42.171] [TRACE] previewImg show time is  0
[2022-05-31 14:54:42.171] [DEBUG] [ "m108.ult" ] step: PrintCtrl::PrintStep(Exposuring)
[2022-05-31 14:54:42.193] [TRACE] [ProjectCtrl] the current is: 309
[2022-05-31 14:54:42.193] [TRACE] [Projector] LedOn
[2022-05-31 14:54:42.193] [TRACE] [Ddp442x] setLedOnOff
[2022-05-31 14:54:42.193] [TRACE] [Ddp442xApi] GpioOpen
[2022-05-31 14:54:42.194] [TRACE] [Ddp442xApi] OpenWithRetry interfacenum: 2 , pre2retry: 3
[2022-05-31 14:54:42.194] [TRACE] SetLedOnOff
[2022-05-31 14:54:42.194] [TRACE] [ProjectorInterface] open_led success
[2022-05-31 14:54:42.194] [DEBUG] [Projector] LedOn result: no support
[2022-05-31 14:54:42.194] [TRACE] [ProjectCtrl] OnExposure preset time: 1500
[2022-05-31 14:54:42.203] [TRACE] PublishMsgProcess 675 msgkey: "1006"
[2022-05-31 14:54:43.695] [TRACE] [ProjectCtrl] [exposure][time]: 1524
[2022-05-31 14:54:43.695] [TRACE] [Projector] LedOff
[2022-05-31 14:54:43.696] [TRACE] [Ddp442x] setLedOnOff
```

