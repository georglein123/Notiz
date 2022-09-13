chairside pro全流程数据获取





chairside pro全流程数据获取

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





一个excel下，根据过程若干个sheet，如下所示

![image-20220727132735564](E:\文档\GitHub\Notiz\chairside pro全流程数据获取.assets\image-20220727132735564.png)



**母光源**

首先4K母光源上获取数据

确认该路径下tmp文件夹已清空

![image-20220727131738245](E:\文档\GitHub\Notiz\chairside pro全流程数据获取.assets\image-20220727131738245.png)



开始相机模组自校准，并记录开始时间线，等待结束完成后，传输tmp文件夹，获取I——P——G数据关系，tmp文件夹内容如下所示

![image-20220727132002239](E:\文档\GitHub\Notiz\chairside pro全流程数据获取.assets\image-20220727132002239.png)

放入python脚本，处理信息

![image-20220727132027047](E:\文档\GitHub\Notiz\chairside pro全流程数据获取.assets\image-20220727132027047.png)

将生成的excel文件内容复制到指定sheet中



![image-20220727132051923](E:\文档\GitHub\Notiz\chairside pro全流程数据获取.assets\image-20220727132051923.png)

同时查看日志信息，查询关键字

4K母光源上日志查看路径`/home/heygears/.heygears/logs`，进入指定日期的文件夹中，找到backend日志，搜素关键字`WriterEEPROM QJsonObject` 下的`100_1500`参数，定位到自校准的时间线附近，获取此时的系数，为4K母光源的G——P拟合关系（G为自变量），日志信息如下所示

```
2022-07-26 13:19:44.721 [DEBUG] WriterEEPROM QJsonObject({"100_1500":[-6.454869890148984e-06,0.004198838025331497,-0.5713498592376709,32.304725646972656]
```

完成后，清空tmp文件夹即可，不要删除tmp文件夹





**记录时间线：**

在excel中类似增加sheet记录时间线



![image-20220727115037294](E:\文档\GitHub\Notiz\chairside pro全流程数据获取.assets\image-20220727115037294.png)





**首次自动均匀性校准**

首先机台设置tmp路径，获取I——P关系

设置路径：`/home/heygears/app/release/`

![image-20220727131738245](E:\文档\GitHub\Notiz\chairside pro全流程数据获取.assets\image-20220727131738245.png)

设置完成后，按流程操作自动均匀性校准，并记录时间线，等待结束后也记录时间线

**处理数据：**

首次自动均匀性校准完成后将tmp文件夹传输出来，内容如下所示

![image-20220727131424825](E:\文档\GitHub\Notiz\chairside pro全流程数据获取.assets\image-20220727131424825.png)

将python脚本放入文件夹，获取对应I——P关系

![image-20220727131446473](E:\文档\GitHub\Notiz\chairside pro全流程数据获取.assets\image-20220727131446473.png)



将数据复制粘贴到对应sheet中

![image-20220727115644780](E:\文档\GitHub\Notiz\chairside pro全流程数据获取.assets\image-20220727115644780.png)



**自动mask手动PI**

开始时在`时间线`sheet中记录开始时间线，等待结束后也记录时间线

按照时间线获取此时的日志（日志开始时间可以为开始时间线的前4分钟，日志时间可以为结束时间线的后1分钟），复制然后新建文件以类似日期动作如`20220726 19.00开始自动mask手动PI`的形式命名另存为txt文件

日志查看路径`/home/heygears/.heygears/logs`

![image-20220728200127364](E:\文档\GitHub\Notiz\chairside pro全流程数据获取.assets\image-20220728200127364.png)

![image-20220728200210686](E:\文档\GitHub\Notiz\chairside pro全流程数据获取.assets\image-20220728200210686.png)

该路径下进入到按日期命名的对应文件夹

使用关键字`OnFitGG`查询，获得如下结果

```
2022-07-28 19:10:03.766 [DEBUG] CreatePI 995 P-I= 13.71 100
2022-07-28 19:10:03.767 [DEBUG] CreatePI 995 P-I= 15.08 110
2022-07-28 19:10:03.767 [DEBUG] CreatePI 995 P-I= 16.42 120
2022-07-28 19:10:03.768 [DEBUG] CreatePI 995 P-I= 17.73 130
2022-07-28 19:10:03.768 [DEBUG] CreatePI 995 P-I= 19.03 140
2022-07-28 19:10:03.769 [DEBUG] CreatePI 995 P-I= 20.3 150
2022-07-28 19:10:03.769 [DEBUG] CreatePI 995 P-I= 21.57 160
2022-07-28 19:10:03.769 [DEBUG] CreatePI 995 P-I= 22.84 170
2022-07-28 19:10:03.770 [DEBUG] CreatePI 995 P-I= 24.08 180
2022-07-28 19:10:03.770 [DEBUG] CreatePI 995 P-I= 25.32 190
2022-07-28 19:10:03.770 [DEBUG] CreatePI 995 P-I= 26.55 200
2022-07-28 19:10:03.771 [DEBUG] CreatePI 995 P-I= 29.01 220
2022-07-28 19:10:03.771 [DEBUG] CreatePI 995 P-I= 31.42 240
2022-07-28 19:10:03.772 [DEBUG] CreatePI 995 P-I= 33.79 260
2022-07-28 19:10:03.772 [DEBUG] CreatePI 995 P-I= 36.12 280
2022-07-28 19:10:03.772 [DEBUG] CreatePI 995 P-I= 38.42 300
2022-07-28 19:10:03.773 [DEBUG] CreatePI 995 P-I= 40.68 320
```



将数据整理保存到excel对应sheet中





使用关键字`CollectPG`查询，结果如下

（CollectPG gamma_exp_manPower_avgGray= "100_1500" 13.7408 108.22（前一个数为P，后一个数为G）：设备端对应的 P——G值）

（CollectPG gamma_exp_4KPower_avgGray= "100_1500" 15.0281 108.22：4K母光源计算得到的对应的P——G值）

```c++
2022-07-28 19:10:03.777 [DEBUG] CollectPG gamma_exp_manPower_avgGray= "100_1500" 13.7408 108.22
2022-07-28 19:10:03.777 [DEBUG] CvtGrayToPower 785 enter
2022-07-28 19:10:03.777 [DEBUG] CvtGrayToPower 787 fn_key= "100_1500"
2022-07-28 19:10:03.778 [DEBUG] CvtGrayToPower 788 avgGray= 108.22
2022-07-28 19:10:03.778 [DEBUG] CvtGrayToPower 792 fn_coeffs= (QVariant(double, 1.22133e-06), QVariant(double, 0.00130929), QVariant(double, -0.15091), QVariant(double, 14.4778))
2022-07-28 19:10:03.779 [DEBUG] CollectPG gamma_exp_4KPower_avgGray= "100_1500" 15.0281 108.22
2022-07-28 19:10:03.779 [WARN] AvgGrayWithRect 762 enter
2022-07-28 19:10:03.780 [WARN] AvgGrayWithRect avgGrey= 117.212
2022-07-28 19:10:03.780 [DEBUG] CollectPG gamma_exp_manPower_avgGray= "100_1500" 15.0766 117.212
2022-07-28 19:10:03.781 [DEBUG] CvtGrayToPower 785 enter
2022-07-28 19:10:03.781 [DEBUG] CvtGrayToPower 787 fn_key= "100_1500"
2022-07-28 19:10:03.781 [DEBUG] CvtGrayToPower 788 avgGray= 117.212
2022-07-28 19:10:03.782 [DEBUG] CvtGrayToPower 792 fn_coeffs= (QVariant(double, 1.22133e-06), QVariant(double, 0.00130929), QVariant(double, -0.15091), QVariant(double, 14.4778))
2022-07-28 19:10:03.782 [DEBUG] CollectPG gamma_exp_4kPower_avgGray= "100_1500" 16.744 117.212
2022-07-28 19:10:03.783 [WARN] AvgGrayWithRect 762 enter
2022-07-28 19:10:03.783 [WARN] AvgGrayWithRect avgGrey= 123.969
2022-07-28 19:10:03.784 [DEBUG] CollectPG gamma_exp_manPower_avgGray= "100_1500" 16.3999 123.969
2022-07-28 19:10:03.784 [DEBUG] CvtGrayToPower 785 enter
2022-07-28 19:10:03.784 [DEBUG] CvtGrayToPower 787 fn_key= "100_1500"
2022-07-28 19:10:03.785 [DEBUG] CvtGrayToPower 788 avgGray= 123.969
```





设备端和4K母光源数据分别整理到excel对应sheet中，

![image-20220727121725025](E:\文档\GitHub\Notiz\chairside pro全流程数据获取.assets\image-20220727121725025.png)



![image-20220727122038062](E:\文档\GitHub\Notiz\chairside pro全流程数据获取.assets\image-20220727122038062.png)



查询关键字`FitGG`，如下所示

各个数字分别对应光强P、设备端G和4K母光源上的G，及最后一行的GG拟合系数

```
2022-07-28 19:10:03.835 [DEBUG] FitGG 1094  P_G_G4K =  10 , 87.3716 , 80.9068
2022-07-28 19:10:03.835 [DEBUG] FitGG 1094  P_G_G4K =  10.5 , 90.6244 , 83.9618
2022-07-28 19:10:03.836 [DEBUG] FitGG 1094  P_G_G4K =  11 , 93.7929 , 86.9523
2022-07-28 19:10:03.836 [DEBUG] FitGG 1094  P_G_G4K =  11.5 , 96.879 , 89.8794
2022-07-28 19:10:03.836 [DEBUG] FitGG 1094  P_G_G4K =  12 , 99.8845 , 92.744
2022-07-28 19:10:03.836 [DEBUG] FitGG 1094  P_G_G4K =  12.5 , 102.811 , 95.5474
2022-07-28 19:10:03.836 [DEBUG] FitGG 1094  P_G_G4K =  13 , 105.661 , 98.2905
2022-07-28 19:10:03.836 [DEBUG] FitGG 1094  P_G_G4K =  13.5 , 108.436 , 100.974
2022-07-28 19:10:03.837 [DEBUG] FitGG 1094  P_G_G4K =  14 , 111.137 , 103.6
2022-07-28 19:10:03.837 [DEBUG] FitGG 1094  P_G_G4K =  14.5 , 113.767 , 106.169
2022-07-28 19:10:03.837 [DEBUG] FitGG 1094  P_G_G4K =  15 , 116.327 , 108.682
2022-07-28 19:10:03.837 [DEBUG] FitGG 1094  P_G_G4K =  15.5 , 118.82 , 111.14
2022-07-28 19:10:03.837 [DEBUG] FitGG 1094  P_G_G4K =  16 , 121.246 , 113.544
2022-07-28 19:10:03.838 [DEBUG] FitGG 1094  P_G_G4K =  16.5 , 123.608 , 115.895
2022-07-28 19:10:03.838 [DEBUG] FitGG 1094  P_G_G4K =  17 , 125.908 , 118.195
2022-07-28 19:10:03.838 [DEBUG] FitGG 1094  P_G_G4K =  17.5 , 128.148 , 120.444
2022-07-28 19:10:03.838 [DEBUG] FitGG 1094  P_G_G4K =  18 , 130.328 , 122.644
2022-07-28 19:10:03.839 [DEBUG] FitGG 1094  P_G_G4K =  18.5 , 132.452 , 124.795
```

GG拟合多项式系数及结果

```c++
2022-07-28 19:10:03.851 [DEBUG] FitGG 1100 valid_GG_degrees= 2
2022-07-28 19:10:03.851 [DEBUG] FitGG gamma_exp: "100_1500" GG_coeffs std::vector(-0.000909803, 1.25072, -23.6763)
```



在excel中对应sheet整理数据

![image-20220727130814925](E:\文档\GitHub\Notiz\chairside pro全流程数据获取.assets\image-20220727130814925.png)

![image-20220727130854140](E:\文档\GitHub\Notiz\chairside pro全流程数据获取.assets\image-20220727130854140.png)







**再次自动均匀性校准**

将首次自动均匀性校准设置的tmp文件夹中的图片全部删除，保留空的tmp文件夹

设置完成后，按流程操作自动均匀性校准，并记录时间线，等待结束后也记录时间线

再次自动均匀性校准完成后将tmp文件夹传输出来，内容如下所示

![image-20220727131156193](E:\文档\GitHub\Notiz\chairside pro全流程数据获取.assets\image-20220727131156193.png)

将python脚本放入文件夹，获取对应I——P关系

![image-20220727131532801](E:\文档\GitHub\Notiz\chairside pro全流程数据获取.assets\image-20220727131532801.png)

将数据复制粘贴到对应sheet中

![image-20220727131627205](E:\文档\GitHub\Notiz\chairside pro全流程数据获取.assets\image-20220727131627205.png)



PI拟合的结果（P为自变量）查询关键字 `多项式系数:  QVector`

```
多项式系数:  QVector(0.0009, -0.0545, 8.0191, -17.0785)
```

