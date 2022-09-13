chairside全流程数据获取

数据组织形式：

新文件夹下：

**母光源**

​	**1. 图片数据**

​	**2. 日志信息**

**设备端 三个过程**

​	**首次自动均匀性校准：**

​		**3. 图片数据**

​		**4. 日志信息**

​	**自动mask手动PI：**

​		**5. 日志信息**

​	**再次自动均匀性校准：**

​		**6.图片数据**

​		**7. 日志信息**

**8. excel汇总数据**



![image-20220727134509718](E:\文档\GitHub\Notiz\chairside全流程数据获取.assets\image-20220727134509718.png)

一个excel下，根据过程若干个sheet，如下所示

![image-20220727132735564](E:\文档\GitHub\Notiz\chairside全流程数据获取.assets\image-20220727132735564.png)



**母光源**

首先4K母光源上获取数据

确认该路径下tmp文件夹已清空

![image-20220727131738245](E:\文档\GitHub\Notiz\chairside全流程数据获取.assets\image-20220727131738245.png)



开始相机模组自校准，并记录开始时间线，等待结束完成后，传输tmp文件夹，获取I——P——G数据关系，tmp文件夹内容如下所示

![image-20220727132002239](E:\文档\GitHub\Notiz\chairside全流程数据获取.assets\image-20220727132002239.png)

放入python脚本，处理信息

![image-20220727132027047](E:\文档\GitHub\Notiz\chairside全流程数据获取.assets\image-20220727132027047.png)

将生成的excel文件内容复制到指定sheet中



![image-20220727132051923](E:\文档\GitHub\Notiz\chairside全流程数据获取.assets\image-20220727132051923.png)

同时查看日志信息，查询关键字

4K母光源上日志查看路径`/home/heygears/.heygears/logs`，进入指定日期的文件夹中，找到backend日志，搜素关键字`WriterEEPROM QJsonObject` 下的`100_1500`参数，定位到自校准的时间线附近，获取此时的系数，为4K母光源的G——P拟合关系（G为自变量），日志信息如下所示

```
2022-07-26 13:19:44.721 [DEBUG] WriterEEPROM QJsonObject({"100_1500":[-6.454869890148984e-06,0.004198838025331497,-0.5713498592376709,32.304725646972656]
```

完成后，清空tmp文件夹即可，不要删除tmp文件夹





**记录时间线：**

在excel中类似增加sheet记录时间线



![image-20220727115037294](E:\文档\GitHub\Notiz\chairside全流程数据获取.assets\image-20220727115037294.png)





**首次自动均匀性校准**

首先机台设置tmp路径，获取I——P关系

设置路径：`/home/heygears/ultracore/bin`

![image-20220727115201978](E:\文档\GitHub\Notiz\chairside全流程数据获取.assets\image-20220727115201978.png)

设置完成后，按流程操作自动均匀性校准，并记录时间线，等待结束后也记录时间线

**处理数据：**

首次自动均匀性校准完成后将tmp文件夹传输出来，内容如下所示

![image-20220727131424825](E:\文档\GitHub\Notiz\chairside全流程数据获取.assets\image-20220727131424825.png)

将python脚本放入文件夹，获取对应I——P关系

![image-20220727131446473](E:\文档\GitHub\Notiz\chairside全流程数据获取.assets\image-20220727131446473.png)



将数据复制粘贴到对应sheet中

![image-20220727115644780](E:\文档\GitHub\Notiz\chairside全流程数据获取.assets\image-20220727115644780.png)



**自动mask手动PI**

开始时在`时间线`sheet中记录开始时间线，等待结束后也记录时间线

按照时间线获取此时的日志（日志开始时间可以为开始时间线的前4分钟，日志时间可以为结束时间线的后1分钟），复制然后新建文件以类似日期动作如`20220726 19.00开始自动mask手动PI`的形式命名另存为txt文件

日志查看路径`/home/heygears/ultracore/log`，如下图所示

![image-20220727152306452](E:\文档\GitHub\Notiz\chairside全流程数据获取.assets\image-20220727152306452.png)

该路径下进入到按日期命名的对应文件夹，若查找之前日期的日志，则进入的`archive`文件夹，找到指定日期的压缩文件

使用关键字`OnFitGG`查询，获得如下结果

```
2022-07-26 19:02:22.880 [0x0000005586794d50] [graycalib.cpp:1099->QVariant GrayCalib::OnFitGG(const QVariant&)][DEBUG] OnFitGG P-I= 120 18.62
2022-07-26 19:02:22.881 [0x0000005586794d50] [graycalib.cpp:1099->QVariant GrayCalib::OnFitGG(const QVariant&)][DEBUG] OnFitGG P-I= 160 24.4599
2022-07-26 19:02:22.881 [0x0000005586794d50] [graycalib.cpp:1099->QVariant GrayCalib::OnFitGG(const QVariant&)][DEBUG] OnFitGG P-I= 130 20.12
2022-07-26 19:02:22.882 [0x0000005586794d50] [graycalib.cpp:1099->QVariant GrayCalib::OnFitGG(const QVariant&)][DEBUG] OnFitGG P-I= 200 30.06
2022-07-26 19:02:22.882 [0x0000005586794d50] [graycalib.cpp:1099->QVariant GrayCalib::OnFitGG(const QVariant&)][DEBUG] OnFitGG P-I= 100 15.59
2022-07-26 19:02:22.882 [0x0000005586794d50] [graycalib.cpp:1099->QVariant GrayCalib::OnFitGG(const QVariant&)][DEBUG] OnFitGG P-I= 170 25.9
2022-07-26 19:02:22.883 [0x0000005586794d50] [graycalib.cpp:1099->QVariant GrayCalib::OnFitGG(const QVariant&)][DEBUG] OnFitGG P-I= 240 35.43
2022-07-26 19:02:22.883 [0x0000005586794d50] [graycalib.cpp:1099->QVariant GrayCalib::OnFitGG(const QVariant&)][DEBUG] OnFitGG P-I= 140 21.58
2022-07-26 19:02:22.883 [0x0000005586794d50] [graycalib.cpp:1099->QVariant GrayCalib::OnFitGG(const QVariant&)][DEBUG] OnFitGG P-I= 110 17.11
2022-07-26 19:02:22.884 [0x0000005586794d50] [graycalib.cpp:1099->QVariant GrayCalib::OnFitGG(const QVariant&)][DEBUG] OnFitGG P-I= 280 40.89
2022-07-26 19:02:22.884 [0x0000005586794d50] [graycalib.cpp:1099->QVariant GrayCalib::OnFitGG(const QVariant&)][DEBUG] OnFitGG P-I= 180 27.32
2022-07-26 19:02:22.884 [0x0000005586794d50] [graycalib.cpp:1099->QVariant GrayCalib::OnFitGG(const QVariant&)][DEBUG] OnFitGG P-I= 150 22.99
2022-07-26 19:02:22.885 [0x0000005586794d50] [graycalib.cpp:1099->QVariant GrayCalib::OnFitGG(const QVariant&)][DEBUG] OnFitGG P-I= 145 22.32
2022-07-26 19:02:22.885 [0x0000005586794d50] [graycalib.cpp:1099->QVariant GrayCalib::OnFitGG(const QVariant&)][DEBUG] OnFitGG P-I= 220 32.79
2022-07-26 19:02:22.885 [0x0000005586794d50] [graycalib.cpp:1099->QVariant GrayCalib::OnFitGG(const QVariant&)][DEBUG] OnFitGG P-I= 190 28.7
2022-07-26 19:02:22.886 [0x0000005586794d50] [graycalib.cpp:1099->QVariant GrayCalib::OnFitGG(const QVariant&)][DEBUG] OnFitGG P-I= 260 38.22
2022-07-26 19:02:22.887 [0x0000005586794d50] [graycalib.cpp:1099->QVariant GrayCalib::OnFitGG(const QVariant&)][DEBUG] OnFitGG P-I= 91 14.18
2022-07-26 19:02:22.887 [0x0000005586794d50] [graycalib.cpp:1110->QVariant GrayCalib::OnFitGG(const QVariant&)][DEBUG] OnFitGG 1110 autoMask_manPI= QVector(2.70379e-07, -0.00020879, 0.188468, -1.44955)
```



将数据整理保存到excel对应sheet中

![image-20220727120750366](E:\文档\GitHub\Notiz\chairside全流程数据获取.assets\image-20220727120750366.png)



使用关键字`CollectPG`查询，结果如下

（CollectPG gamma_exp_manPower_avgGray （前一个数为P，后一个数为G）：设备端对应的 P——G值）

（CollectPG gamma_exp_4KPower_avgGray：4K母光源计算得到的对应的P——G值）

```
 CollectPG gamma_exp_manPower_avgGray= "100_1500" 15.5798 150.26 
 
 CollectPG gamma_exp_4KPower_avgGray= "100_1500" 19.3566 150.26 
 
 CollectPG gamma_exp_manPower_avgGray= "100_1500" 17.1155 156.74
 
 CollectPG gamma_exp_4kPower_avgGray= "100_1500" 21.0502 156.74
 .....
 
 PG_coeff =  QVector(0.000482093, -0.0853838, 6.74983, 64.0407)
 PG4K_coeff =  QVector(0.000901713, -0.102554, 6.82825, 49.9174)
```

设备端和4K母光源数据分别整理到excel对应sheet中，

![image-20220727121725025](E:\文档\GitHub\Notiz\chairside全流程数据获取.assets\image-20220727121725025.png)



![image-20220727122038062](E:\文档\GitHub\Notiz\chairside全流程数据获取.assets\image-20220727122038062.png)



查询关键字`FitGG`，如下所示

各个数字分别对应光强P、设备端G和4K母光源上的G，及最后一行的GG拟合系数

```
P_G_G4K =  10 , 123.483 , 108.846
P_G_G4K =  10.5 , 126.058 , 111.351
....
GG_coeffs std::vector(1.61487e-05, -0.00750795, 2.12236, -69.3293)
```

在excel中对应sheet整理数据

![image-20220727130814925](E:\文档\GitHub\Notiz\chairside全流程数据获取.assets\image-20220727130814925.png)

![image-20220727130854140](E:\文档\GitHub\Notiz\chairside全流程数据获取.assets\image-20220727130854140.png)



**再次自动均匀性校准**

将首次自动均匀性校准设置的tmp文件夹中的图片全部删除，保留空的tmp文件夹

设置完成后，按流程操作自动均匀性校准，并记录时间线，等待结束后也记录时间线

再次自动均匀性校准完成后将tmp文件夹传输出来，内容如下所示

![image-20220727131156193](E:\文档\GitHub\Notiz\chairside全流程数据获取.assets\image-20220727131156193.png)

将python脚本放入文件夹，获取对应I——P关系

![image-20220727131532801](E:\文档\GitHub\Notiz\chairside全流程数据获取.assets\image-20220727131532801.png)

将数据复制粘贴到对应sheet中

![image-20220727131627205](E:\文档\GitHub\Notiz\chairside全流程数据获取.assets\image-20220727131627205.png)



PI拟合的结果（P为自变量）查询关键字 `多项式系数:  QVector`

```
多项式系数:  QVector(0.0009, -0.0545, 8.0191, -17.0785)
```

