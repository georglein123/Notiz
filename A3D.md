A3D

1.机台上日志信息保留一周，不用覆盖

2.协调机台案例打印测试

3.

日志查看

![image-20220517144829678](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20220517144829678.png)

传感器信息：

![image-20220530140649738](E:\文档\GitHub\Notiz\A3D.assets\image-20220530140649738.png)



A3D上打印出现的问题：

- 出现较小截面导致幅面内实体被淘汰出去后无实体时，此时M值赋为0，没有进入工艺包对应段；

![image-20220518100033416](E:\文档\GitHub\Notiz\A3D.assets\image-20220518100033416.png)



```c++
6: 2022-05-17 11:04:20.603 [Thread (pooled)] [printimg.cpp:816->void PrintImg::UpdatePeelParam(PrintContext&)][INFO] UpdatePeelParam [layer:] 302 area_percent 0.116877 Peel up params speed and dis: QVector(400, 400, 400, 6000, 6000) QVector(150, 300, 450, 2900, 2900)
	行 56881: 2022-05-17 11:04:24.209 [Thread (pooled)] [printimg.cpp:796->void PrintImg::UpdateWaitTime(PrintContext&)][INFO] UpdateWaitTime [layer:] 303 area_percent 0.100069 Wait time is 100
	行 56882: 2022-05-17 11:04:24.209 [Thread (pooled)] [printimg.cpp:816->void PrintImg::UpdatePeelParam(PrintContext&)][INFO] UpdatePeelParam [layer:] 303 area_percent 0.100069 Peel up params speed and dis: QVector(400, 400, 400, 6000, 6000) QVector(150, 300, 450, 2900, 2900)
	行 57257: 2022-05-17 11:04:27.727 [Thread (pooled)] [printimg.cpp:796->void PrintImg::UpdateWaitTime(PrintContext&)][INFO] UpdateWaitTime [layer:] 304 area_percent 0.0851515 Wait time is 100
	行 57258: 2022-05-17 11:04:27.728 [Thread (pooled)] [printimg.cpp:816->void PrintImg::UpdatePeelParam(PrintContext&)][INFO] UpdatePeelParam [layer:] 304 area_percent 0.0851515 Peel up params speed and dis: QVector(400, 400, 400, 6000, 6000) QVector(150, 300, 450, 2900, 2900)
        
        -----------
        
	行 57631: 2022-05-17 11:04:30.862 [Thread (pooled)] [printimg.cpp:796->void PrintImg::UpdateWaitTime(PrintContext&)][INFO] UpdateWaitTime [layer:] 305 area_percent 0 Wait time is 0
	行 57632: 2022-05-17 11:04:30.862 [Thread (pooled)] [printimg.cpp:816->void PrintImg::UpdatePeelParam(PrintContext&)][INFO] UpdatePeelParam [layer:] 305 area_percent 0 Peel up params speed and dis: QVector(400, 400, 400, 6000, 6000) QVector(150, 300, 450, 2900, 2900)
	行 58004: 2022-05-17 11:04:34.260 [Thread (pooled)] [printimg.cpp:796->void PrintImg::UpdateWaitTime(PrintContext&)][INFO] UpdateWaitTime [layer:] 306 area_percent 0 Wait time is 0
	行 58005: 2022-05-17 11:04:34.260 [Thread (pooled)] [printimg.cpp:816->void PrintImg::UpdatePeelParam(PrintContext&)][INFO] UpdatePeelParam [layer:] 306 area_percent 0 Peel up params speed and dis: QVector(400, 400, 400, 6000, 6000) QVector(150, 300, 450, 2900, 2900)
	行 58407: 2022-05-17 11:04:37.814 [Thread (pooled)] [printimg.cpp:796->void PrintImg::UpdateWaitTime(PrintContext&)][INFO] UpdateWaitTime [layer:] 307 area_percent 0 Wait time is 0
	行 58408: 2022-05-17 11:04:37.814 [Thread (pooled)] [printimg.cpp:816->void PrintImg::UpdatePeelParam(PrintContext&)][INFO] UpdatePeelParam [layer:] 307 area_percent 0 Peel up params speed and dis: QVector(400, 400, 400, 6000, 6000) QVector(150, 300, 450, 2900, 2900)
	行 58747: 2022-05-17 11:04:41.458 [Thread (pooled)] [printimg.cpp:796->void PrintImg::UpdateWaitTime(PrintContext&)][INFO] UpdateWaitTime [layer:] 308 area_percent 0 Wait time is 0
	行 58748: 2022-05-17 11:04:41.458 [Thread (pooled)] [printimg.cpp:816->void PrintImg::UpdatePeelParam(PrintContext&)][INFO] UpdatePeelParam [layer:] 308 area_percent 0 Peel up params speed and dis: QVector(400, 400, 400, 6000, 6000) QVector(150, 300, 450, 2900, 2900)
	行 59160: 2022-05-17 11:04:45.283 [Thread (pooled)] [printimg.cpp:796->void PrintImg::UpdateWaitTime(PrintContext&)][INFO] UpdateWaitTime [layer:] 309 area_percent 0 Wait time is 0
	行 59161: 2022-05-17 11:04:45.284 [Thread (pooled)] [printimg.cpp:816->void PrintImg::UpdatePeelParam(PrintContext&)][INFO] UpdatePeelParam [layer:] 309 area_percent 0 Peel up params speed and dis: QVector(400, 400, 400, 6000, 6000) QVector(150, 300, 450, 2900, 2900)
搜索 "CalculateMValue end value" （1个文件中匹配到527次，总计查找1次）
```

工艺包该段：

```c++
				"MLowerLimit": 0.0,
                "MUpperLimit": 8,
                "Number": 1,
                "WaitTime": 100,
                "Z_AxisUp": [
                    { "v": 400, "s": 150 },
                    { "v": 400, "s": 300 },
                    { "v": 400, "s": 450 },
                    { "v": 6000, "s": 2900 },
                    { "v": 6000, "s": 2900 }
                ],
                "Z_AxisDown": [
                    { "v": 6000, "s": -1850 },
                    { "v": 4000, "s": -2850 },
                    { "v": 4000, "s": -2850 },
                    { "v": 4000, "s": -2850 },
                    { "v": 4000, "s": -2850 }
                ]
            },
```

单独运行第305层图片

![S000305_P1](E:\文档\GitHub\Notiz\A3D.assets\S000305_P1.png)

```
[extractItemInfo]VALID_ITEM_EMPTY
[collectItemParams]EXTRACT_ITEM_INFO_FAILED
[compute]COLLECT_ITEM_PARAM_FAILED
[main]COMPUTE_ERROR
```

错误信息的原因：

```c++
// check num of valid items
    if (itemLabels.size() == 0)
    {
        COUT << "[" << __func__ << "]"
             << "VALID_ITEM_EMPTY" << ENDL;
        return VALID_ITEM_EMPTY;
    }
```

修改筛选截面的大小阈值由$3mm^2$变成 $1mm^2$

无报错

或者直接在幅面内没有实体时M值为0，软件已改为该方法。





- M值计算突变



```c++
行 22261: 2022-05-17 10:58:27.959 [Thread (pooled)] [printimg.cpp:816->void PrintImg::UpdatePeelParam(PrintContext&)][INFO] UpdatePeelParam [layer:] 220 area_percent 9.34369 Peel up params speed and dis: QVector(400, 400, 400, 6000, 6000) QVector(150, 300, 450, 2900, 2900)
	行 22701: 2022-05-17 10:58:32.446 [Thread (pooled)] [printimg.cpp:796->void PrintImg::UpdateWaitTime(PrintContext&)][INFO] UpdateWaitTime [layer:] 221 area_percent 6.67458 Wait time is 100
        
        
        “------------
        
	行 22702: 2022-05-17 10:58:32.446 [Thread (pooled)] [printimg.cpp:816->void PrintImg::UpdatePeelParam(PrintContext&)][INFO] UpdatePeelParam [layer:] 221 area_percent 6.67458 Peel up params speed and dis: QVector(400, 400, 400, 6000, 6000) QVector(150, 300, 450, 2900, 2900)
	行 23144: 2022-05-17 10:58:37.337 [Thread (pooled)] [printimg.cpp:796->void PrintImg::UpdateWaitTime(PrintContext&)][INFO] UpdateWaitTime [layer:] 222 area_percent 47.3785 Wait time is 4500
        --------------”
        
	行 23145: 2022-05-17 10:58:37.337 [Thread (pooled)] [printimg.cpp:816->void PrintImg::UpdatePeelParam(PrintContext&)][INFO] UpdatePeelParam [layer:] 222 area_percent 47.3785 Peel up params speed and dis: QVector(300, 300, 300, 6000, 6000) QVector(400, 700, 1100, 4900, 4900)
	行 23585: 2022-05-17 10:58:41.841 [Thread (pooled)] [printimg.cpp:796->void PrintImg::UpdateWaitTime(PrintContext&)][INFO] UpdateWaitTime [layer:] 223 area_percent 48.0436 Wait time is 4500
	行 23586: 2022-05-17 10:58:41.841 [Thread (pooled)] [printimg.cpp:816->void PrintImg::UpdatePeelParam(PrintContext&)][INFO] UpdatePeelParam [layer:] 223 area_percent 48.0436 Peel up params speed and dis: QVector(300, 300, 300, 6000, 6000) QVector(400, 700, 1100, 4900, 4900)
	行 24051: 2022-05-17 10:58:46.090 [Thread (pooled)] [printimg.cpp:796->void PrintImg::UpdateWaitTime(PrintContext&)][INFO] UpdateWaitTime [layer:] 224 area_percent 48.6036 Wait time is 4500
        
        
      “-------------  
	行 24052: 2022-05-17 10:58:46.090 [Thread (pooled)] [printimg.cpp:816->void PrintImg::UpdatePeelParam(PrintContext&)][INFO] UpdatePeelParam [layer:] 224 area_percent 48.6036 Peel up params speed and dis: QVector(300, 300, 300, 6000, 6000) QVector(400, 700, 1100, 4900, 4900)
	行 24520: 2022-05-17 10:58:50.653 [Thread (pooled)] [printimg.cpp:796->void PrintImg::UpdateWaitTime(PrintContext&)][INFO] UpdateWaitTime [layer:] 225 area_percent 4.89971 Wait time is 100
        ---------------”
        
	行 24521: 2022-05-17 10:58:50.653 [Thread (pooled)] [printimg.cpp:816->void PrintImg::UpdatePeelParam(PrintContext&)][INFO] UpdatePeelParam [layer:] 225 area_percent 4.89971 Peel up params speed and dis: QVector(400, 400, 400, 6000, 6000) QVector(150, 300, 450, 2900, 2900)
```

224层：进入路线2，类似多个小基牙情况，计算的M值偏大

![S000224_P1](E:\文档\GitHub\Notiz\A3D.assets\S000224_P1.png)

```c++
T: 41556
S: 81399
delta: 168.265
M: 563.147
T: 41540
S: 81415.7
delta: 168.252
M: 562.918
T: 41536
S: 81415.7
delta: 168.264
M: 562.807
T: 41511
S: 81434.4
delta: 168.243
M: 562.449
T: 39136
S: 69442.7
delta: 147.772
M: 576.476
T: 39094
S: 69336.7
delta: 147.76
M: 575.552
T: 39093
S: 69442.7
delta: 147.821
M: 575.439
T: 39082
S: 69368.4
delta: 147.823
M: 575.115
T: 23505
S: 64462.5
delta: 142.638
M: 298.902
T: 23496
S: 64643.8
delta: 142.678
M: 298.807
T: 23485
S: 64548.3
delta: 142.626
M: 298.655
T: 23477
S: 64496.7
delta: 142.635
M: 298.46
[collectItemParams]WARNING: valid_items=12 < topN_items=50
[compute]top 5 m: 576.476
[compute]top 5 m: 575.552
[compute]top 5 m: 575.439
[compute]top 5 m: 575.115
[compute]top 5 m: 563.147
[compute]MThre: 286.573
[compute]greater than MThre m: 576.476
[compute]greater than MThre m: 575.552
[compute]greater than MThre m: 575.439
[compute]greater than MThre m: 575.115
[compute]greater than MThre m: 563.147
[compute]greater than MThre m: 562.918
[compute]greater than MThre m: 562.807
[compute]greater than MThre m: 562.449
[compute]greater than MThre m: 298.902
[compute]greater than MThre m: 298.807
[compute]greater than MThre m: 298.655
[compute]greater than MThre m: 298.46
[compute]nums of M > M_thre : 12
[compute]nums of valid items : 12,  80% of the valid items : 9.6
[compute]nums of M > M_thre  >  80% of the valid items  
[compute]ENTER INTO CASE2
T: 416511
S: 2.91761e+06
delta: 651.895
M: 5703.77
concat_M: 5703.77, M_hat: 10805.1
[main]S000224_P1.png, final_M(without unit)=8254.45, final_M(with unit)=23.6263
[main]well done!
```



225层：进入路线1，多个实体，计算的M值偏小

![S000225_P1](E:\文档\GitHub\Notiz\A3D.assets\S000225_P1.png)

```c++
T: 42119
S: 81276.6
delta: 167.561
M: 575.607
T: 42118
S: 81240.1
delta: 167.554
M: 575.569
T: 42103
S: 81278.4
delta: 167.573
M: 575.277
T: 42087
S: 81220.4
delta: 167.525
M: 575.081
T: 39868
S: 69296.7
delta: 147.314
M: 592.527
T: 39863
S: 69299.9
delta: 147.309
M: 592.451
T: 39850
S: 69244.1
delta: 147.366
M: 591.887
T: 39838
S: 69264.9
delta: 147.345
M: 591.762
T: 23211
S: 63916.7
delta: 142.298
M: 294.213
T: 23202
S: 64011
delta: 142.397
M: 293.928
T: 23195
S: 63887.4
delta: 142.376
M: 293.76
T: 23191
S: 63814.1
delta: 142.319
M: 293.753
[collectItemParams]WARNING: valid_items=12 < topN_items=50
[compute]top 5 m: 592.527
[compute]top 5 m: 592.451
[compute]top 5 m: 591.887
[compute]top 5 m: 591.762
[compute]top 5 m: 575.607
[compute]MThre: 294.423
[compute]greater than MThre m: 592.527
[compute]greater than MThre m: 592.451
[compute]greater than MThre m: 591.887
[compute]greater than MThre m: 591.762
[compute]greater than MThre m: 575.607
[compute]greater than MThre m: 575.569
[compute]greater than MThre m: 575.277
[compute]greater than MThre m: 575.081
[compute]smaller than MThre m: 294.213
[compute]smaller than MThre m: 293.928
[compute]smaller than MThre m: 293.76
[compute]smaller than MThre m: 293.753
[compute]nums of M > M_thre : 8
[compute]nums of valid items : 12,  80% of the valid items : 9.6
[compute]nums of M > M_thre  <=  80% of the valid items  
[compute]ENTER INTO CASE1
delta 6=147.309
delta 3=167.573
delta 3_6=454.933
delta 6_3=447.865
X6=0.575225
X3=0.518009
delta 6=147.309
delta 9=142.298
delta 9_6=473.503
delta 6_9=475.033
X6=0.575225
X9=0.363144
delta 7=147.366
delta 10=142.397
delta 10_7=473.567
delta 7_10=475.085
X7=0.5755
X10=0.362469
delta 2=167.554
delta 9=142.298
delta 9_2=492.42
delta 2_9=500.303
X2=0.518439
X9=0.363144
delta 4=167.525
delta 10=142.397
delta 10_4=492.382
delta 4_10=500.227
X4=0.518182
X10=0.362469
[compute]area5:T5=39868, rectangle5:S5=69296.7, T5/S5:X5=0.575323, discrete:delta5=147.314, M5=592.527, 
[compute]T1=42119, S1=81276.6, X1=0.518218, delta1=167.561,  delta5=147.314,  delta1_5=xxx, delta5_1=xxx, M1=575.607, K1_5=0, 
[compute]T2=42118, S2=81240.1, X2=0.518439, delta2=167.554,  delta5=147.314,  delta2_5=xxx, delta5_2=xxx, M2=575.569, K2_5=0, 
[compute]T3=42103, S3=81278.4, X3=0.518009, delta3=167.573,  delta5=147.314,  delta3_5=xxx, delta5_3=xxx, M3=575.277, K3_5=0, 
[compute]T4=42087, S4=81220.4, X4=0.518182, delta4=167.525,  delta5=147.314,  delta4_5=xxx, delta5_4=xxx, M4=575.081, K4_5=0, 
[compute]T6=39863, S6=69299.9, X6=0.575225, delta6=147.309,  delta5=147.314,  delta6_5=xxx, delta5_6=xxx, M6=592.451, K6_5=0, 
[compute]T7=39850, S7=69244.1, X7=0.5755, delta7=147.366,  delta5=147.314,  delta7_5=xxx, delta5_7=xxx, M7=591.887, K7_5=0, 
[compute]T8=39838, S8=69264.9, X8=0.575155, delta8=147.345,  delta5=147.314,  delta8_5=xxx, delta5_8=xxx, M8=591.762, K8_5=0, 
[compute]T9=23211, S9=63916.7, X9=0.363144, delta9=142.298,  delta5=147.314,  delta9_5=xxx, delta5_9=xxx, M9=294.213, K9_5=0, 
[compute]T10=23202, S10=64011, X10=0.362469, delta10=142.397,  delta5=147.314,  delta10_5=xxx, delta5_10=xxx, M10=293.928, K10_5=0, 
[compute]area6:T6=39863, rectangle6:S6=69299.9, T6/S6:X6=0.575225, discrete:delta6=147.309, M6=592.451, 
[compute]T1=42119, S1=81276.6, X1=0.518218, delta1=167.561,  delta6=147.309,  delta1_6=xxx, delta6_1=xxx, M1=575.607, K1_6=0, 
[compute]T2=42118, S2=81240.1, X2=0.518439, delta2=167.554,  delta6=147.309,  delta2_6=xxx, delta6_2=xxx, M2=575.569, K2_6=0, 
[compute]T3=42103, S3=81278.4, X3=0.518009, delta3=167.573,  delta6=147.309,  delta3_6=xxx, delta6_3=xxx, M3=575.277, K3_6=0.319584, 
[compute]T4=42087, S4=81220.4, X4=0.518182, delta4=167.525,  delta6=147.309,  delta4_6=xxx, delta6_4=xxx, M4=575.081, K4_6=0, 
[compute]T5=39868, S5=69296.7, X5=0.575323, delta5=147.314,  delta6=147.309,  delta5_6=xxx, delta6_5=xxx, M5=592.527, K5_6=0, 
[compute]T7=39850, S7=69244.1, X7=0.5755, delta7=147.366,  delta6=147.309,  delta7_6=xxx, delta6_7=xxx, M7=591.887, K7_6=0, 
[compute]T8=39838, S8=69264.9, X8=0.575155, delta8=147.345,  delta6=147.309,  delta8_6=xxx, delta6_8=xxx, M8=591.762, K8_6=0, 
[compute]T9=23211, S9=63916.7, X9=0.363144, delta9=142.298,  delta6=147.309,  delta9_6=xxx, delta6_9=xxx, M9=294.213, K9_6=0.195134, 
[compute]T10=23202, S10=64011, X10=0.362469, delta10=142.397,  delta6=147.309,  delta10_6=xxx, delta6_10=xxx, M10=293.928, K10_6=0, 
[compute]area7:T7=39850, rectangle7:S7=69244.1, T7/S7:X7=0.5755, discrete:delta7=147.366, M7=591.887, 
[compute]T1=42119, S1=81276.6, X1=0.518218, delta1=167.561,  delta7=147.366,  delta1_7=xxx, delta7_1=xxx, M1=575.607, K1_7=0, 
[compute]T2=42118, S2=81240.1, X2=0.518439, delta2=167.554,  delta7=147.366,  delta2_7=xxx, delta7_2=xxx, M2=575.569, K2_7=0, 
[compute]T3=42103, S3=81278.4, X3=0.518009, delta3=167.573,  delta7=147.366,  delta3_7=xxx, delta7_3=xxx, M3=575.277, K3_7=0, 
[compute]T4=42087, S4=81220.4, X4=0.518182, delta4=167.525,  delta7=147.366,  delta4_7=xxx, delta7_4=xxx, M4=575.081, K4_7=0, 
[compute]T5=39868, S5=69296.7, X5=0.575323, delta5=147.314,  delta7=147.366,  delta5_7=xxx, delta7_5=xxx, M5=592.527, K5_7=0, 
[compute]T6=39863, S6=69299.9, X6=0.575225, delta6=147.309,  delta7=147.366,  delta6_7=xxx, delta7_6=xxx, M6=592.451, K6_7=0, 
[compute]T8=39838, S8=69264.9, X8=0.575155, delta8=147.345,  delta7=147.366,  delta8_7=xxx, delta7_8=xxx, M8=591.762, K8_7=0, 
[compute]T9=23211, S9=63916.7, X9=0.363144, delta9=142.298,  delta7=147.366,  delta9_7=xxx, delta7_9=xxx, M9=294.213, K9_7=0, 
[compute]T10=23202, S10=64011, X10=0.362469, delta10=142.397,  delta7=147.366,  delta10_7=xxx, delta7_10=xxx, M10=293.928, K10_7=0.195104, 
[compute]area8:T8=39838, rectangle8:S8=69264.9, T8/S8:X8=0.575155, discrete:delta8=147.345, M8=591.762, 
[compute]T1=42119, S1=81276.6, X1=0.518218, delta1=167.561,  delta8=147.345,  delta1_8=xxx, delta8_1=xxx, M1=575.607, K1_8=0, 
[compute]T2=42118, S2=81240.1, X2=0.518439, delta2=167.554,  delta8=147.345,  delta2_8=xxx, delta8_2=xxx, M2=575.569, K2_8=0, 
[compute]T3=42103, S3=81278.4, X3=0.518009, delta3=167.573,  delta8=147.345,  delta3_8=xxx, delta8_3=xxx, M3=575.277, K3_8=0, 
[compute]T4=42087, S4=81220.4, X4=0.518182, delta4=167.525,  delta8=147.345,  delta4_8=xxx, delta8_4=xxx, M4=575.081, K4_8=0, 
[compute]T5=39868, S5=69296.7, X5=0.575323, delta5=147.314,  delta8=147.345,  delta5_8=xxx, delta8_5=xxx, M5=592.527, K5_8=0, 
[compute]T6=39863, S6=69299.9, X6=0.575225, delta6=147.309,  delta8=147.345,  delta6_8=xxx, delta8_6=xxx, M6=592.451, K6_8=0, 
[compute]T7=39850, S7=69244.1, X7=0.5755, delta7=147.366,  delta8=147.345,  delta7_8=xxx, delta8_7=xxx, M7=591.887, K7_8=0, 
[compute]T9=23211, S9=63916.7, X9=0.363144, delta9=142.298,  delta8=147.345,  delta9_8=xxx, delta8_9=xxx, M9=294.213, K9_8=0, 
[compute]T10=23202, S10=64011, X10=0.362469, delta10=142.397,  delta8=147.345,  delta10_8=xxx, delta8_10=xxx, M10=293.928, K10_8=0, 
[compute]area1:T1=42119, rectangle1:S1=81276.6, T1/S1:X1=0.518218, discrete:delta1=167.561, M1=575.607, 
[compute]T2=42118, S2=81240.1, X2=0.518439, delta2=167.554,  delta1=167.561,  delta2_1=xxx, delta1_2=xxx, M2=575.569, K2_1=0, 
[compute]T3=42103, S3=81278.4, X3=0.518009, delta3=167.573,  delta1=167.561,  delta3_1=xxx, delta1_3=xxx, M3=575.277, K3_1=0, 
[compute]T4=42087, S4=81220.4, X4=0.518182, delta4=167.525,  delta1=167.561,  delta4_1=xxx, delta1_4=xxx, M4=575.081, K4_1=0, 
[compute]T5=39868, S5=69296.7, X5=0.575323, delta5=147.314,  delta1=167.561,  delta5_1=xxx, delta1_5=xxx, M5=592.527, K5_1=0, 
[compute]T6=39863, S6=69299.9, X6=0.575225, delta6=147.309,  delta1=167.561,  delta6_1=xxx, delta1_6=xxx, M6=592.451, K6_1=0, 
[compute]T7=39850, S7=69244.1, X7=0.5755, delta7=147.366,  delta1=167.561,  delta7_1=xxx, delta1_7=xxx, M7=591.887, K7_1=0, 
[compute]T8=39838, S8=69264.9, X8=0.575155, delta8=147.345,  delta1=167.561,  delta8_1=xxx, delta1_8=xxx, M8=591.762, K8_1=0, 
[compute]T9=23211, S9=63916.7, X9=0.363144, delta9=142.298,  delta1=167.561,  delta9_1=xxx, delta1_9=xxx, M9=294.213, K9_1=0, 
[compute]T10=23202, S10=64011, X10=0.362469, delta10=142.397,  delta1=167.561,  delta10_1=xxx, delta1_10=xxx, M10=293.928, K10_1=0, 
[main]S000225_P1.png, final_M(without unit)=833.711, final_M(with unit)=2.38629
[main]well done!
```



- 打印全幅面底板进入路线1无法退出：

![S000014_P1](E:\文档\GitHub\Notiz\A3D.assets\S000014_P1.png)

```
T: 2.58914e+06
S: 4.0606e+06
delta: 827.196
M: 54287.2
[collectItemParams]WARNING: valid_items=1 < topN_items=50
[compute]top 5 m: 54287.2
[compute]MThre: 5428.72
[compute]greater than MThre m: 54287.2
[compute]valid items nums: 1
[compute]M > M_thre nums: 1
[compute]ENTER INTO CASE1
terminate called after throwing an instance of 'std::out_of_range'
  what():  vector::_M_range_check: __n (which is 1) >= this->size() (which is 1)
已放弃 (核心已转储)
```

只有一个实体时，不会计算相对离散度等信息，所以需要设置只有1个实体的情况

 

4个满版全颌面实心牙模打印时间约3h30min

检查M值准确进入每个对应M值区间，执行对应的工艺参数

```c++
行 7528: 2022-05-30,18-00-27 546065194816  UpdateWaitTime [layer:] 1 area_percent 139.32115173339844 Wait time is 9500 
	行 7529: 2022-05-30,18-00-27 546065194816  UpdatePeelParam [layer:] 1 area_percent 139.32115173339844 Peel up params speed and dis: Vector{ 300 300 300 6000 6000 } Vector{ 1600 2400 3600 12900 12900 } 
	行 7530: 2022-05-30,18-00-27 546065194816  UpdatePeelParam [layer:] 1 Peel down params speed and dis: Vector{ 6000 500 500 500 500 } Vector{ -12000 -12850 -12850 -12850 -12850 } 
	行 7538: 2022-05-30,18-00-28 546065194816  UpdateWaitTime [layer:] 2 area_percent 139.32769775390625 Wait time is 9500 
	行 7539: 2022-05-30,18-00-28 546065194816  UpdatePeelParam [layer:] 2 area_percent 139.32769775390625 Peel up params speed and dis: Vector{ 300 300 300 6000 6000 } Vector{ 1600 2400 3600 12900 12900 } 
	行 7540: 2022-05-30,18-00-28 546065194816  UpdatePeelParam [layer:] 2 Peel down params speed and dis: Vector{ 6000 500 500 500 500 } Vector{ -12000 -12850 -12850 -12850 -12850 } 
	行 7548: 2022-05-30,18-00-29 546065194816  UpdateWaitTime [layer:] 3 area_percent 139.32313537597656 Wait time is 9500 
	行 7549: 2022-05-30,18-00-29 546065194816  UpdatePeelParam [layer:] 3 area_percent 139.32313537597656 Peel up params speed and dis: Vector{ 300 300 300 6000 6000 } Vector{ 1600 2400 3600 12900 12900 } 
	行 7550: 2022-05-30,18-00-29 546065194816  UpdatePeelParam [layer:] 3 Peel down params speed and dis: Vector{ 6000 500 500 500 500 } Vector{ -12000 -12850 -12850 -12850 -12850 } 
	行 7558: 2022-05-30,18-00-29 546065194816  UpdateWaitTime [layer:] 4 area_percent 139.35064697265625 Wait time is 9500 
	行 7559: 2022-05-30,18-00-29 546065194816  UpdatePeelParam [layer:] 4 area_percent 139.35064697265625 Peel up params speed and dis: Vector{ 300 300 300 6000 6000 } Vector{ 1600 2400 3600 12900 12900 } 
	行 7560: 2022-05-30,18-00-29 546065194816  UpdatePeelParam [layer:] 4 Peel down params speed and dis: Vector{ 6000 500 500 500 500 } Vector{ -12000 -12850 -12850 -12850 -12850 } 
```

```c++
行 13307: 2022-05-30,21-24-40 546065194816  UpdateWaitTime [layer:] 529 area_percent 0 Wait time is 100 
	行 13308: 2022-05-30,21-24-40 546065194816  UpdatePeelParam [layer:] 529 area_percent 0 Peel up params speed and dis: Vector{ 400 400 400 6000 6000 } Vector{ 150 300 450 2900 2900 } 
	行 13309: 2022-05-30,21-24-40 546065194816  UpdatePeelParam [layer:] 529 Peel down params speed and dis: Vector{ 6000 4000 4000 4000 4000 } Vector{ -1850 -2850 -2850 -2850 -2850 } 
	行 13318: 2022-05-30,21-24-43 546065194816  UpdateWaitTime [layer:] 530 area_percent 0 Wait time is 100 
	行 13319: 2022-05-30,21-24-43 546065194816  UpdatePeelParam [layer:] 530 area_percent 0 Peel up params speed and dis: Vector{ 400 400 400 6000 6000 } Vector{ 150 300 450 2900 2900 } 
	行 13320: 2022-05-30,21-24-43 546065194816  UpdatePeelParam [layer:] 530 Peel down params speed and dis: Vector{ 6000 4000 4000 4000 4000 } Vector{ -1850 -2850 -2850 -2850 -2850 } 
	行 13329: 2022-05-30,21-24-47 546065194816  UpdateWaitTime [layer:] 531 area_percent 0 Wait time is 100 
	行 13330: 2022-05-30,21-24-47 546065194816  UpdatePeelParam [layer:] 531 area_percent 0 Peel up params speed and dis: Vector{ 400 400 400 6000 6000 } Vector{ 150 300 450 2900 2900 } 
	行 13331: 2022-05-30,21-24-47 546065194816  UpdatePeelParam [layer:] 531 Peel down params speed and dis: Vector{ 6000 4000 4000 4000 4000 } Vector{ -1850 -2850 -2850 -2850 -2850 } 
```



时间精度增加

area_percent 换成M值 M value:

![image-20220601091951748](E:\文档\GitHub\Notiz\A3D.assets\image-20220601091951748.png)



```
[2022-05-24 17:00:51.070] [TRACE] 	 |--- temp: 23.15
[2022-05-24 17:00:51.072] [TRACE] PublishMsgProcess 675 msgkey: "1002"
[2022-05-24 17:00:53.854] [TRACE] - 94 - [wait][time] 30000 [wait][offset time] 0
[2022-05-24 17:00:53.854] [TRACE]  ====== Begin Read Model  95 `th Loop ====== 
[2022-05-24 17:00:53.854] [DEBUG] ReadModel 291
[2022-05-24 17:00:53.854] [DEBUG] [ "圆柱46高6M值.ult" ] layer done
[2022-05-24 17:00:53.854] [DEBUG] the buffer is not Empty
[2022-05-24 17:00:53.854] [DEBUG] [ "圆柱46高6M值.ult" ] step: PrintCtrl::PrintStep(Preprocessing)
[2022-05-24 17:00:53.854] [DEBUG] Read Model Parser Finished!
[2022-05-24 17:00:53.854] [DEBUG] 




[2022-05-24 17:00:53.854] [DEBUG] --------
[2022-05-24 17:00:53.854] [DEBUG] - 95 - [exposure][begin]
[2022-05-24 17:00:53.854] [DEBUG] =================================== loop  104
[2022-05-24 17:00:53.855] [DEBUG] [ "圆柱46高6M值.ult" ] layer start: 95 / 120
[2022-05-24 17:00:53.855] [DEBUG] 进入这里-正常取图 105
[2022-05-24 17:00:53.855] [TRACE] [ProjectCtrl] OnExposure
[2022-05-24 17:00:53.855] [DEBUG] [ "圆柱46高6M值.ult" ] step: PrintCtrl::PrintStep(Exposuring)
[2022-05-24 17:00:53.855] [TRACE] Discard Led Eff:  "LE_UNCOVERED"
[2022-05-24 17:00:53.855] [TRACE] previewImg show time is  0
[2022-05-24 17:00:53.855] [DEBUG] Start Image Process,Layer:  105 step: 10
[2022-05-24 17:00:53.856] [DEBUG] handle base and get ELayerImgType_Object
[2022-05-24 17:00:53.856] [TRACE] ULT: other Layer
[2022-05-24 17:00:53.857] [DEBUG] src_mat fixed ... 1
[2022-05-24 17:00:53.857] [DEBUG] src_mat fixed ... 0 "/tmp/.A2DTemp/S000105_P1.png"
[2022-05-24 17:00:53.875] [TRACE] PublishMsgProcess 675 msgkey: "1006"
[2022-05-24 17:00:53.894] [TRACE] [ProjectCtrl] the current is: 281
[2022-05-24 17:00:53.896] [TRACE] [Projector] LedOn
[2022-05-24 17:00:53.896] [TRACE] [Ddp442x] setLedOnOff
[2022-05-24 17:00:53.896] [TRACE] [Ddp442xApi] GpioOpen
[2022-05-24 17:00:53.897] [TRACE] [Ddp442xApi] OpenWithRetry interfacenum: 2 , pre2retry: 3
[2022-05-24 17:00:53.898] [TRACE] SetLedOnOff
[2022-05-24 17:00:53.900] [TRACE] [ProjectorInterface] open_led success
[2022-05-24 17:00:53.901] [DEBUG] [Projector] LedOn result: no support
[2022-05-24 17:00:53.902] [TRACE] [ProjectCtrl] OnExposure preset time: 1500
[2022-05-24 17:00:53.902] [DEBUG] bObjImg  true
[2022-05-24 17:00:53.902] [DEBUG] wearhole scale  false
[2022-05-24 17:00:53.918] [DEBUG] IsRemap 60 校准是否打开 true
[2022-05-24 17:00:54.062] [DEBUG] ZoomIn Success to transform the image: 3854 2168 1.0036 1.0036
[2022-05-24 17:00:54.063] [DEBUG] ShapeAdjust completed ... src_mat rows,cols 2160 3840
[2022-05-24 17:00:54.188] [DEBUG] IsRemap 60 校准是否打开 true
[2022-05-24 17:00:54.356] [DEBUG] ZoomIn Success to transform the image: 3854 2168 1.0036 1.0036
[2022-05-24 17:00:54.372] [DEBUG] IsRemap 60 校准是否打开 true
[2022-05-24 17:00:54.538] [DEBUG] ZoomIn Success to transform the image: 3854 2168 1.0036 1.0036
[2022-05-24 17:00:54.538] [DEBUG] GetDemixMat Demix after and before image: "/tmp/.A2DTemp/S000115_P1.png" "/tmp/.A2DTemp/S000095_P1.png" 105
[2022-05-24 17:00:54.784] [DEBUG] NotBaseLayer and DoDemix.
[2022-05-24 17:00:55.316] [DEBUG] num of context.exposure is : 3
[2022-05-24 17:00:55.316] [DEBUG] 第 105 张图片的曝光的时间为:
[2022-05-24 17:00:55.317] [DEBUG] UpdateExposeParam 0:obj,1:contour,2:fill,3:support,4:preview layer of context: 105 layer of theory: 105 Type: 1 Energy: 21 ExposeTime: 0
[2022-05-24 17:00:55.317] [DEBUG] 第 105 张图片的曝光的时间为:
[2022-05-24 17:00:55.317] [DEBUG] UpdateExposeParam 0:obj,1:contour,2:fill,3:support,4:preview layer of context: 105 layer of theory: 105 Type: 2 Energy: 21 ExposeTime: 1500
[2022-05-24 17:00:55.317] [DEBUG] 第 105 张图片的曝光的时间为:
[2022-05-24 17:00:55.317] [DEBUG] UpdateExposeParam 0:obj,1:contour,2:fill,3:support,4:preview layer of context: 105 layer of theory: 105 Type: 4 Energy: 0 ExposeTime: 0
[2022-05-24 17:00:55.317] [DEBUG] 第  105 张图片的上升距离为:isAdaptive= false 的工艺包数据：= 18900 true QVector(1600, 2400, 3600, 6900, 18900) 173.572
[2022-05-24 17:00:55.318] [DEBUG] 第  105 层下降距离为:isAdaptive= false 的工艺包数据：= -18850
[2022-05-24 17:00:55.318] [DEBUG] layers  105 's energy is:  21
[2022-05-24 17:00:55.318] [DEBUG] layers  105 's current is:  281
[2022-05-24 17:00:55.318] [DEBUG] layers  105 's energy is:  21
[2022-05-24 17:00:55.319] [DEBUG] layers  105 's current is:  281
[2022-05-24 17:00:55.319] [DEBUG] layers  105 's energy is:  0
[2022-05-24 17:00:55.319] [DEBUG] layers  105 's current is:  80
[2022-05-24 17:00:55.320] [DEBUG] context enqueue  i : 104 context object layer : 105 context show layer is  105 

[2022-05-24 17:00:55.403] [TRACE] [ProjectCtrl] [exposure][time]: 1546
[2022-05-24 17:00:55.403] [TRACE] [Projector] LedOff
[2022-05-24 17:00:55.404] [TRACE] [Ddp442x] setLedOnOff
[2022-05-24 17:00:55.404] [TRACE] [Ddp442xApi] GpioOpen
[2022-05-24 17:00:55.404] [TRACE] [Ddp442xApi] OpenWithRetry interfacenum: 2 , pre2retry: 3
[2022-05-24 17:00:55.404] [TRACE] SetLedOnOff
[2022-05-24 17:00:55.404] [TRACE] [ProjectorInterface] close_led success
[2022-05-24 17:00:55.404] [DEBUG] [Projector] LedOff result: no support
[2022-05-24 17:00:55.450] [TRACE] OnEnviromentCheck 57 data: QMap(("Projector", QVariant(bool, true))("Screen", QVariant(bool, true)))
[2022-05-24 17:00:55.451] [TRACE] - 95 - [exposure][time] 1595 [exposure][offset time] 95
[2022-05-24 17:00:55.451] [DEBUG] begin SyncPeel
[2022-05-24 17:00:55.453] [DEBUG] [ "圆柱46高6M值.ult" ] step: PrintCtrl::PrintStep(Peeling)
[2022-05-24 17:00:55.453] [TRACE] command: "ac100118ff00000400000001d227acdc"
[2022-05-24 17:00:55.489] [DEBUG] NotifyComm 通訊返回 "ac100118ff00000400000001d227acdc"
[2022-05-24 17:00:55.530] [TRACE] Slave State change:  "ES-0 OPR-0 OPL-0 NP-1 ZT-0 ZB-0 ZS-0 ZR-0 ZZ-1 ZP-1 CAU-1 CAL-0 CGU-1 CGD-0 TL-1 CAE-0 ZAE-0 SP-1 ST-0 HES-1"  | F- "-30.80"
[2022-05-24 17:00:55.729] [TRACE] Slave State change:  "ES-0 OPR-0 OPL-0 NP-0 ZT-0 ZB-0 ZS-0 ZR-0 ZZ-1 ZP-1 CAU-1 CAL-0 CGU-1 CGD-0 TL-1 CAE-0 ZAE-0 SP-1 ST-0 HES-1"  | F- "-9.60"
[2022-05-24 17:00:56.072] [WARN] QModbusDevice::Error(TimeoutError) "Response timeout."
[2022-05-24 17:01:01.068] [TRACE] slave:
[2022-05-24 17:01:01.070] [TRACE] 	 |--- plateform: 1
[2022-05-24 17:01:01.071] [TRACE] 	 |--- force: 2.9
[2022-05-24 17:01:01.071] [TRACE] 	 |--- temp: 24.38
[2022-05-24 17:01:01.071] [TRACE] 	 |--- humidity: 62.39
[2022-05-24 17:01:01.071] [TRACE] heaint:
[2022-05-24 17:01:01.071] [TRACE] 	 |--- temp: 22.91
[2022-05-24 17:01:01.087] [TRACE] PublishMsgProcess 675 msgkey: "1002"
[2022-05-24 17:01:08.071] [WARN] QModbusDevice::Error(TimeoutError) "Response timeout."
[2022-05-24 17:01:08.129] [TRACE] Slave State change:  "ES-0 OPR-0 OPL-0 NP-0 ZT-0 ZB-0 ZS-1 ZR-0 ZZ-1 ZP-1 CAU-1 CAL-0 CGU-1 CGD-0 TL-1 CAE-0 ZAE-0 SP-1 ST-0 HES-1"  | F- "1.40"
[2022-05-24 17:01:08.229] [TRACE] Slave State change:  "ES-0 OPR-0 OPL-0 NP-0 ZT-0 ZB-0 ZS-0 ZR-0 ZZ-1 ZP-1 CAU-1 CAL-0 CGU-1 CGD-0 TL-1 CAE-0 ZAE-0 SP-1 ST-0 HES-1"  | F- "1.50"
[2022-05-24 17:01:09.382] [TRACE] exe result: "ZAXIS->SEGMENTED_MOTION" "COMMAND_SUCCESS"
[2022-05-24 17:01:09.383] [DEBUG] end SyncPeel
[2022-05-24 17:01:09.383] [TRACE] Escape 0 1376520
[2022-05-24 17:01:09.384] [DEBUG] begin SyncPeel
[2022-05-24 17:01:09.384] [TRACE] command: "ac100118ff00000400000002d367acdc"
[2022-05-24 17:01:09.403] [DEBUG] discard slave return result 
[2022-05-24 17:01:09.421] [DEBUG] discard slave return result 
[2022-05-24 17:01:09.440] [TRACE] Slave State change:  "ES-0 OPR-0 OPL-0 NP-0 ZT-0 ZB-0 ZS-1 ZR-0 ZZ-1 ZP-0 CAU-1 CAL-0 CGU-1 CGD-0 TL-1 CAE-0 ZAE-0 SP-1 ST-0 HES-1"  | F- "0.10"
[2022-05-24 17:01:09.458] [DEBUG] NotifyComm 通訊返回 "ac100118ff00000400000002d367acdc"
[2022-05-24 17:01:09.529] [TRACE] Slave State change:  "ES-0 OPR-0 OPL-0 NP-0 ZT-0 ZB-0 ZS-0 ZR-0 ZZ-1 ZP-1 CAU-1 CAL-0 CGU-1 CGD-0 TL-1 CAE-0 ZAE-0 SP-1 ST-0 HES-1"  | F- "0.20"
[2022-05-24 17:01:11.069] [TRACE] slave:
[2022-05-24 17:01:11.069] [TRACE] 	 |--- force: -1
[2022-05-24 17:01:11.105] [TRACE] PublishMsgProcess 675 msgkey: "1002"
[2022-05-24 17:01:11.229] [TRACE] Slave State change:  "ES-0 OPR-0 OPL-0 NP-1 ZT-0 ZB-0 ZS-0 ZR-0 ZZ-1 ZP-1 CAU-1 CAL-0 CGU-1 CGD-0 TL-1 CAE-0 ZAE-0 SP-1 ST-0 HES-1"  | F- "-25.10"
[2022-05-24 17:01:12.272] [TRACE] exe result: "ZAXIS->SEGMENTED_MOTION" "COMMAND_SUCCESS"
[2022-05-24 17:01:12.273] [DEBUG] end SyncPeel
[2022-05-24 17:01:12.274] [TRACE] Escape 0 1376520
[2022-05-24 17:01:12.274] [TRACE] [PrintCtrl] peel up: Curlayer: 95 Number: "14"
[2022-05-24 17:01:12.275] [TRACE] [PrintCtrl] speed[0]: 300, distance[0]: 1600
[2022-05-24 17:01:12.275] [TRACE] [PrintCtrl] speed[1]: 300, distance[1]: 2400
[2022-05-24 17:01:12.275] [TRACE] [PrintCtrl] speed[2]: 300, distance[2]: 3600
[2022-05-24 17:01:12.275] [TRACE] [PrintCtrl] speed[3]: 6000, distance[3]: 6900
[2022-05-24 17:01:12.275] [TRACE] [PrintCtrl] speed[4]: 10000, distance[4]: 18900
[2022-05-24 17:01:12.275] [TRACE] [PrintCtrl] peel down: Curlayer: 95 Number: "14"
[2022-05-24 17:01:12.276] [TRACE] [PrintCtrl] speed[0]: 10000, distance[0]: -18000
[2022-05-24 17:01:12.276] [TRACE] [PrintCtrl] speed[1]: 500, distance[1]: -18850
[2022-05-24 17:01:12.276] [TRACE] [PrintCtrl] speed[2]: 500, distance[2]: -18850
[2022-05-24 17:01:12.276] [TRACE] [PrintCtrl] speed[3]: 500, distance[3]: -18850
[2022-05-24 17:01:12.276] [TRACE] [PrintCtrl] speed[4]: 500, distance[4]: -18850
[2022-05-24 17:01:12.276] [TRACE] - 95 - [peel][time] 16824 [peel][offset time] -425
[2022-05-24 17:01:12.277] [DEBUG] [ "圆柱46高6M值.ult" ] step: PrintCtrl::PrintStep(Waiting)
[2022-05-24 17:01:12.336] [TRACE] Slave State change:  "ES-0 OPR-0 OPL-0 NP-1 ZT-0 ZB-0 ZS-1 ZR-0 ZZ-1 ZP-0 CAU-1 CAL-0 CGU-1 CGD-0 TL-1 CAE-0 ZAE-0 SP-1 ST-0 HES-1"  | F- "-107.60"
[2022-05-24 17:01:20.069] [WARN] QModbusDevice::Error(TimeoutError) "Response timeout."
[2022-05-24 17:01:21.068] [TRACE] slave:
[2022-05-24 17:01:21.069] [TRACE] 	 |--- plateform: -1
[2022-05-24 17:01:21.069] [TRACE] 	 |--- force: -50.8
[2022-05-24 17:01:21.069] [TRACE] 	 |--- temp: 24.3
[2022-05-24 17:01:21.069] [TRACE] 	 |--- humidity: 62.44
[2022-05-24 17:01:21.120] [TRACE] PublishMsgProcess 675 msgkey: "1002"
[2022-05-24 17:01:31.069] [TRACE] slave:
[2022-05-24 17:01:31.069] [TRACE] 	 |--- force: -39.7
[2022-05-24 17:01:31.069] [TRACE] 	 |--- temp: 24.32
[2022-05-24 17:01:31.069] [TRACE] 	 |--- humidity: 62.27
[2022-05-24 17:01:31.069] [TRACE] heaint:
[2022-05-24 17:01:31.069] [TRACE] 	 |--- temp: 22.59
[2022-05-24 17:01:31.130] [TRACE] PublishMsgProcess 675 msgkey: "1002"
[2022-05-24 17:01:32.071] [WARN] QModbusDevice::Error(TimeoutError) "Response timeout."
[2022-05-24 17:01:41.069] [TRACE] slave:
[2022-05-24 17:01:41.069] [TRACE] 	 |--- force: -31.4
[2022-05-24 17:01:41.069] [TRACE] 	 |--- temp: 24.42
[2022-05-24 17:01:41.069] [TRACE] 	 |--- humidity: 62.34
[2022-05-24 17:01:41.069] [TRACE] heaint:
[2022-05-24 17:01:41.069] [TRACE] 	 |--- temp: 23.23
[2022-05-24 17:01:41.143] [TRACE] PublishMsgProcess 675 msgkey: "1002"
[2022-05-24 17:01:42.069] [TRACE] [Hg_DailyRollingAppender] clearBeforeDays The logs generated before the specified date are cleared -  QDate("2021-11-25") log type: "print"
[2022-05-24 17:01:42.070] [TRACE] [Hg_DailyRollingAppender] clearBeforeDays The logs generated before the specified date are cleared -  QDate("2022-04-24") log type: "hive"
[2022-05-24 17:01:42.079] [TRACE] [Hg_DailyRollingAppender] clearBeforeDays The logs generated before the specified date are cleared -  QDate("2022-04-24") log type: "backend"
[2022-05-24 17:01:42.274] [TRACE] - 95 - [wait][time] 30000 [wait][offset time] 0
[2022-05-24 17:01:42.274] [TRACE]  ====== Begin Read Model  96 `th Loop ====== 
[2022-05-24 17:01:42.274] [DEBUG] [ "圆柱46高6M值.ult" ] layer done
[2022-05-24 17:01:42.274] [DEBUG] ReadModel 291
[2022-05-24 17:01:42.274] [TRACE] UpdateTimecost >>>  115300 1200 -3172  remain layers:  25
[2022-05-24 17:01:42.274] [DEBUG] the buffer is not Empty
[2022-05-24 17:01:42.274] [DEBUG] [ "圆柱46高6M值.ult" ] step: PrintCtrl::PrintStep(Preprocessing)
[2022-05-24 17:01:42.274] [DEBUG] Read Model Parser Finished!
[2022-05-24 17:01:42.274] [DEBUG] 





[2022-05-24 17:01:42.274] [DEBUG] --------
[2022-05-24 17:01:42.274] [DEBUG] - 96 - [exposure][begin]
[2022-05-24 17:01:42.275] [DEBUG] =================================== loop  105
[2022-05-24 17:01:42.275] [DEBUG] [ "圆柱46高6M值.ult" ] layer start: 96 / 120
[2022-05-24 17:01:42.275] [DEBUG] 进入这里-正常取图 106
[2022-05-24 17:01:42.275] [TRACE] [ProjectCtrl] OnExposure
[2022-05-24 17:01:42.275] [DEBUG] [ "圆柱46高6M值.ult" ] step: PrintCtrl::PrintStep(Exposuring)
[2022-05-24 17:01:42.275] [TRACE] previewImg show time is  0
[2022-05-24 17:01:42.275] [DEBUG] Start Image Process,Layer:  106 step: 10
[2022-05-24 17:01:42.277] [DEBUG] handle base and get ELayerImgType_Object
[2022-05-24 17:01:42.277] [TRACE] ULT: other Layer
[2022-05-24 17:01:42.281] [TRACE] Discard Led Eff:  "LE_UNCOVERED"
[2022-05-24 17:01:42.281] [DEBUG] src_mat fixed ... 1
[2022-05-24 17:01:42.281] [DEBUG] src_mat fixed ... 0 "/tmp/.A2DTemp/S000106_P1.png"
[2022-05-24 17:01:42.314] [TRACE] [ProjectCtrl] the current is: 281
[2022-05-24 17:01:42.316] [TRACE] [Projector] LedOn
[2022-05-24 17:01:42.317] [TRACE] [Ddp442x] setLedOnOff
[2022-05-24 17:01:42.319] [TRACE] [Ddp442xApi] GpioOpen
[2022-05-24 17:01:42.320] [TRACE] [Ddp442xApi] OpenWithRetry interfacenum: 2 , pre2retry: 3
[2022-05-24 17:01:42.320] [TRACE] SetLedOnOff
[2022-05-24 17:01:42.322] [TRACE] [ProjectorInterface] open_led success
```



A3D日志信息

```
2022-05-30,21-18-03 546065194816  UpdateWaitTime [layer:] 440 area_percent 10.33032512664795 Wait time is 300 
2022-05-30,21-18-03 546065194816  UpdatePeelParam [layer:] 440 area_percent 10.33032512664795 Peel up params speed and dis: Vector{ 400 400 400 6000 6000 } Vector{ 170 350 500 3900 3900 } 
2022-05-30,21-18-03 546065194816  UpdatePeelParam [layer:] 440 Peel down params speed and dis: Vector{ 6000 4000 4000 4000 4000 } Vector{ -2850 -3850 -3850 -3850 -3850 } 
2022-05-30,21-18-08 544252897280  当前图层 410 等待时间 600 



2022-05-30,21-18-08 546065194816  当前图层 441 曝光参数来自于标准 
2022-05-30,21-18-08 546065194816  当前图层 441 曝光参数来自于标准 
2022-05-30,21-18-08 546065194816  当前图层 441 曝光参数来自于标准 
2022-05-30,21-18-09 546065194816  当前图层 441 曝光参数来自于标准 
2022-05-30,21-18-09 546065194816  当前图层 441 曝光参数来自于标准 
2022-05-30,21-18-09 546065194816  UpdateExposeParam 0:obj,1:contour,2:fill,3:support,4:preview 当前图层 441 Type: 0 Energy: 21 ExposeTime: 1250 
2022-05-30,21-18-09 546065194816  UpdateExposeParam 0:obj,1:contour,2:fill,3:support,4:preview 当前图层 441 Type: 4 Energy: 0 ExposeTime: 0 
2022-05-30,21-18-09 546065194816  UpdateWaitTime [layer:] 441 area_percent 10.256172180175781 Wait time is 300 
2022-05-30,21-18-09 546065194816  UpdatePeelParam [layer:] 441 area_percent 10.256172180175781 Peel up params speed and dis: Vector{ 400 400 400 6000 6000 } Vector{ 170 350 500 3900 3900 } 
2022-05-30,21-18-09 546065194816  UpdatePeelParam [layer:] 441 Peel down params speed and dis: Vector{ 6000 4000 4000 4000 4000 } Vector{ -2850 -3850 -3850 -3850 -3850 } 



2022-05-30,21-18-13 544252897280  当前图层 411 等待时间 600 
2022-05-30,21-18-14 546065194816  当前图层 442 曝光参数来自于标准 
2022-05-30,21-18-14 546065194816  当前图层 442 曝光参数来自于标准 
2022-05-30,21-18-14 546065194816  当前图层 442 曝光参数来自于标准 
2022-05-30,21-18-15 546065194816  当前图层 442 曝光参数来自于标准 
2022-05-30,21-18-15 546065194816  当前图层 442 曝光参数来自于标准 
2022-05-30,21-18-15 546065194816  UpdateExposeParam 0:obj,1:contour,2:fill,3:support,4:preview 当前图层 442 Type: 0 Energy: 21 ExposeTime: 1250 
2022-05-30,21-18-15 546065194816  UpdateExposeParam 0:obj,1:contour,2:fill,3:support,4:preview 当前图层 442 Type: 4 Energy: 0 ExposeTime: 0 
2022-05-30,21-18-15 546065194816  UpdateWaitTime [layer:] 442 area_percent 10.2808837890625 Wait time is 300 
2022-05-30,21-18-15 546065194816  UpdatePeelParam [layer:] 442 area_percent 10.2808837890625 Peel up params speed and dis: Vector{ 400 400 400 6000 6000 } Vector{ 170 350 500 3900 3900 } 
2022-05-30,21-18-15 546065194816  UpdatePeelParam [layer:] 442 Peel down params speed and dis: Vector{ 6000 4000 4000 4000 4000 } Vector{ -2850 -3850 -3850 -3850 -3850 } 
2022-05-30,21-18-19 544252897280  当前图层 412 等待时间 600 
2022-05-30,21-18-20 546065194816  当前图层 443 曝光参数来自于标准 
2022-05-30,21-18-20 546065194816  当前图层 443 曝光参数来自于标准 
2022-05-30,21-18-20 546065194816  当前图层 443 曝光参数来自于标准 
2022-05-30,21-18-21 546065194816  当前图层 443 曝光参数来自于标准 
2022-05-30,21-18-21 546065194816  当前图层 443 曝光参数来自于标准 
2022-05-30,21-18-21 546065194816  UpdateExposeParam 0:obj,1:contour,2:fill,3:support,4:preview 当前图层 443 Type: 0 Energy: 21 ExposeTime: 1250 
2022-05-30,21-18-21 546065194816  UpdateExposeParam 0:obj,1:contour,2:fill,3:support,4:preview 当前图层 443 Type: 4 Energy: 0 ExposeTime: 0 
2022-05-30,21-18-21 546065194816  UpdateWaitTime [layer:] 443 area_percent 10.087335586547852 Wait time is 300 
2022-05-30,21-18-21 546065194816  UpdatePeelParam [layer:] 443 area_percent 10.087335586547852 Peel up params speed and dis: Vector{ 400 400 400 6000 6000 } Vector{ 170 350 500 3900 3900 } 
2022-05-30,21-18-21 546065194816  UpdatePeelParam [layer:] 443 Peel down params speed and dis: Vector{ 6000 4000 4000 4000 4000 } Vector{ -2850 -3850 -3850 -3850 -3850 } 
2022-05-30,21-18-25 544252897280  当前图层 413 等待时间 600 
```



A3D满版5个全颌面实心牙模

91-248层共158层打印时间突然增加，每层增加将近20s，增加总时间接近1h，

91层是M值从14段落到第13段

248层是M值第13段的最后一层

```c++
	行 525: 2022-06-01,18-25-41 545595235488  end print layer 87 cost time: 22.95s 
	行 531: 2022-06-01,18-26-05 545595235488  end print layer 88 cost time: 24.80s 
	行 537: 2022-06-01,18-26-30 545595235488  end print layer 89 cost time: 24.84s 
	行 543: 2022-06-01,18-26-53 545595235488  end print layer 90 cost time: 22.90s 
	
	------以下层91——248层时间发生突变
        
	行 549: 2022-06-01,18-27-38 545595235488  end print layer 91 cost time: 44.42s 
	行 555: 2022-06-01,18-28-22 545595235488  end print layer 92 cost time: 44.25s 
	行 561: 2022-06-01,18-29-03 545595235488  end print layer 93 cost time: 41.56s 
	行 567: 2022-06-01,18-29-45 545595235488  end print layer 94 cost time: 41.49s 
	行 573: 2022-06-01,18-30-26 545595235488  end print layer 95 cost time: 41.50s 
	行 579: 2022-06-01,18-31-08 545595235488  end print layer 96 cost time: 41.42s 
	行 585: 2022-06-01,18-31-49 545595235488  end print layer 97 cost time: 41.44s 
	行 591: 2022-06-01,18-32-31 545595235488  end print layer 98 cost time: 41.34s 
	行 597: 2022-06-01,18-33-15 545595235488  end print layer 99 cost time: 44.08s 
	行 603: 2022-06-01,18-33-56 545595235488  end print layer 100 cost time: 41.44s 
	行 609: 2022-06-01,18-34-38 545595235488  end print layer 101 cost time: 41.40s 
	行 615: 2022-06-01,18-35-19 545595235488  end print layer 102 cost time: 41.52s 
	行 621: 2022-06-01,18-36-00 545595235488  end print layer 103 cost time: 41.33s 
	行 627: 2022-06-01,18-36-42 545595235488  end print layer 104 cost time: 41.46s 
	行 633: 2022-06-01,18-37-23 545595235488  end print layer 105 cost time: 41.48s 
	行 639: 2022-06-01,18-38-05 545595235488  end print layer 106 cost time: 41.39s 
	行 645: 2022-06-01,18-38-46 545595235488  end print layer 107 cost time: 41.42s 
	行 651: 2022-06-01,18-39-30 545595235488  end print layer 108 cost time: 44.33s 
	行 657: 2022-06-01,18-40-18 545595235488  end print layer 109 cost time: 47.47s 
	行 663: 2022-06-01,18-41-02 545595235488  end print layer 110 cost time: 44.15s 
	行 669: 2022-06-01,18-41-44 545595235488  end print layer 111 cost time: 41.39s 
	行 675: 2022-06-01,18-42-28 545595235488  end print layer 112 cost time: 44.27s 
	行 681: 2022-06-01,18-43-09 545595235488  end print layer 113 cost time: 41.47s 
	行 687: 2022-06-01,18-43-51 545595235488  end print layer 114 cost time: 41.49s 
	行 693: 2022-06-01,18-44-32 545595235488  end print layer 115 cost time: 41.48s 
	行 699: 2022-06-01,18-45-14 545595235488  end print layer 116 cost time: 41.52s 
	行 705: 2022-06-01,18-45-58 545595235488  end print layer 117 cost time: 44.28s 
	行 711: 2022-06-01,18-46-45 545595235488  end print layer 118 cost time: 47.43s 
	行 717: 2022-06-01,18-47-33 545595235488  end print layer 119 cost time: 47.40s 
	行 723: 2022-06-01,18-48-14 545595235488  end print layer 120 cost time: 41.53s 
	行 729: 2022-06-01,18-48-59 545595235488  end print layer 121 cost time: 44.19s 
	行 735: 2022-06-01,18-49-40 545595235488  end print layer 122 cost time: 41.47s 
	行 741: 2022-06-01,18-50-21 545595235488  end print layer 123 cost time: 41.43s 
	行 747: 2022-06-01,18-51-03 545595235488  end print layer 124 cost time: 41.53s 
	行 753: 2022-06-01,18-51-44 545595235488  end print layer 125 cost time: 41.43s 
	行 759: 2022-06-01,18-52-26 545595235488  end print layer 126 cost time: 41.49s 
	行 765: 2022-06-01,18-53-07 545595235488  end print layer 127 cost time: 41.39s 
	行 771: 2022-06-01,18-53-52 545595235488  end print layer 128 cost time: 44.34s 
	行 777: 2022-06-01,18-54-33 545595235488  end print layer 129 cost time: 41.45s 
	行 783: 2022-06-01,18-55-15 545595235488  end print layer 130 cost time: 41.49s 
	行 789: 2022-06-01,18-56-02 545595235488  end print layer 131 cost time: 47.44s 
	行 795: 2022-06-01,18-56-46 545595235488  end print layer 132 cost time: 44.22s 
	行 801: 2022-06-01,18-57-34 545595235488  end print layer 133 cost time: 47.22s 
	行 807: 2022-06-01,18-58-15 545595235488  end print layer 134 cost time: 41.51s 
	行 813: 2022-06-01,18-58-59 545595235488  end print layer 135 cost time: 44.29s 
	行 819: 2022-06-01,18-59-44 545595235488  end print layer 136 cost time: 44.21s 
	行 825: 2022-06-01,19-00-25 545595235488  end print layer 137 cost time: 41.48s 
	行 831: 2022-06-01,19-01-09 545595235488  end print layer 138 cost time: 44.17s 
	行 837: 2022-06-01,19-01-51 545595235488  end print layer 139 cost time: 41.48s 
	行 843: 2022-06-01,19-02-35 545595235488  end print layer 140 cost time: 44.30s 
	行 849: 2022-06-01,19-03-19 545595235488  end print layer 141 cost time: 44.31s 
	行 855: 2022-06-01,19-04-01 545595235488  end print layer 142 cost time: 41.39s 
	行 861: 2022-06-01,19-04-45 545595235488  end print layer 143 cost time: 44.22s 
	行 867: 2022-06-01,19-05-29 545595235488  end print layer 144 cost time: 44.23s 
	行 873: 2022-06-01,19-06-13 545595235488  end print layer 145 cost time: 44.26s 
	行 879: 2022-06-01,19-06-58 545595235488  end print layer 146 cost time: 44.27s 
	行 885: 2022-06-01,19-07-45 545595235488  end print layer 147 cost time: 47.36s 
	行 891: 2022-06-01,19-08-32 545595235488  end print layer 148 cost time: 47.40s 
	行 897: 2022-06-01,19-09-14 545595235488  end print layer 149 cost time: 41.37s 
	行 903: 2022-06-01,19-09-58 545595235488  end print layer 150 cost time: 44.22s 
	行 909: 2022-06-01,19-10-39 545595235488  end print layer 151 cost time: 41.40s 
	行 915: 2022-06-01,19-11-27 545595235488  end print layer 152 cost time: 47.42s 
	行 921: 2022-06-01,19-12-14 545595235488  end print layer 153 cost time: 47.27s 
	行 927: 2022-06-01,19-12-58 545595235488  end print layer 154 cost time: 44.27s 
	行 933: 2022-06-01,19-13-46 545595235488  end print layer 155 cost time: 47.36s 
	行 939: 2022-06-01,19-14-30 545595235488  end print layer 156 cost time: 44.23s 
	行 945: 2022-06-01,19-15-11 545595235488  end print layer 157 cost time: 41.40s 
	行 951: 2022-06-01,19-15-56 545595235488  end print layer 158 cost time: 44.30s 
	行 957: 2022-06-01,19-16-43 545595235488  end print layer 159 cost time: 47.37s 
	行 963: 2022-06-01,19-17-27 545595235488  end print layer 160 cost time: 44.22s 
	行 969: 2022-06-01,19-18-11 545595235488  end print layer 161 cost time: 44.23s 
	行 975: 2022-06-01,19-18-56 545595235488  end print layer 162 cost time: 44.27s 
	行 981: 2022-06-01,19-19-40 545595235488  end print layer 163 cost time: 44.24s 
	行 987: 2022-06-01,19-20-21 545595235488  end print layer 164 cost time: 41.45s 
	行 993: 2022-06-01,19-21-06 545595235488  end print layer 165 cost time: 44.29s 
	行 999: 2022-06-01,19-21-47 545595235488  end print layer 166 cost time: 41.44s 
	行 1005: 2022-06-01,19-22-29 545595235488  end print layer 167 cost time: 41.41s 
	行 1011: 2022-06-01,19-23-16 545595235488  end print layer 168 cost time: 47.43s 
	行 1017: 2022-06-01,19-24-03 545595235488  end print layer 169 cost time: 47.45s 
	行 1023: 2022-06-01,19-24-51 545595235488  end print layer 170 cost time: 47.43s 
	行 1029: 2022-06-01,19-25-35 545595235488  end print layer 171 cost time: 44.26s 
	行 1035: 2022-06-01,19-26-17 545595235488  end print layer 172 cost time: 41.45s 
	行 1041: 2022-06-01,19-27-04 545595235488  end print layer 173 cost time: 47.28s 
	行 1047: 2022-06-01,19-27-45 545595235488  end print layer 174 cost time: 41.41s 
	行 1053: 2022-06-01,19-28-30 545595235488  end print layer 175 cost time: 44.27s 
	行 1059: 2022-06-01,19-29-14 545595235488  end print layer 176 cost time: 44.27s 
	行 1065: 2022-06-01,19-29-55 545595235488  end print layer 177 cost time: 41.39s 
	行 1071: 2022-06-01,19-30-37 545595235488  end print layer 178 cost time: 41.49s 
	行 1077: 2022-06-01,19-31-21 545595235488  end print layer 179 cost time: 44.33s 
	行 1083: 2022-06-01,19-32-03 545595235488  end print layer 180 cost time: 41.45s 
	行 1089: 2022-06-01,19-32-47 545595235488  end print layer 181 cost time: 44.27s 
	行 1095: 2022-06-01,19-33-28 545595235488  end print layer 182 cost time: 41.43s 
	行 1101: 2022-06-01,19-34-10 545595235488  end print layer 183 cost time: 41.37s 
	行 1107: 2022-06-01,19-34-57 545595235488  end print layer 184 cost time: 47.34s 
	行 1113: 2022-06-01,19-35-38 545595235488  end print layer 185 cost time: 41.46s 
	行 1119: 2022-06-01,19-36-26 545595235488  end print layer 186 cost time: 47.32s 
	行 1125: 2022-06-01,19-37-13 545595235488  end print layer 187 cost time: 47.35s 
	行 1131: 2022-06-01,19-37-55 545595235488  end print layer 188 cost time: 41.43s 
	行 1137: 2022-06-01,19-38-42 545595235488  end print layer 189 cost time: 47.44s 
	行 1143: 2022-06-01,19-39-26 545595235488  end print layer 190 cost time: 44.20s 
	行 1149: 2022-06-01,19-40-08 545595235488  end print layer 191 cost time: 41.52s 
	行 1155: 2022-06-01,19-40-49 545595235488  end print layer 192 cost time: 41.44s 
	行 1161: 2022-06-01,19-41-31 545595235488  end print layer 193 cost time: 41.44s 
	行 1167: 2022-06-01,19-42-15 545595235488  end print layer 194 cost time: 44.24s 
	行 1173: 2022-06-01,19-42-59 545595235488  end print layer 195 cost time: 44.26s 
	行 1179: 2022-06-01,19-43-46 545595235488  end print layer 196 cost time: 47.41s 
	行 1185: 2022-06-01,19-44-28 545595235488  end print layer 197 cost time: 41.49s 
	行 1191: 2022-06-01,19-45-15 545595235488  end print layer 198 cost time: 47.38s 
	行 1197: 2022-06-01,19-46-00 545595235488  end print layer 199 cost time: 44.29s 
	行 1203: 2022-06-01,19-46-44 545595235488  end print layer 200 cost time: 44.25s 
	行 1209: 2022-06-01,19-47-31 545595235488  end print layer 201 cost time: 47.36s 
	行 1215: 2022-06-01,19-48-19 545595235488  end print layer 202 cost time: 47.41s 
	行 1221: 2022-06-01,19-49-06 545595235488  end print layer 203 cost time: 47.39s 
	行 1227: 2022-06-01,19-49-50 545595235488  end print layer 204 cost time: 44.23s 
	行 1233: 2022-06-01,19-50-38 545595235488  end print layer 205 cost time: 47.40s 
	行 1239: 2022-06-01,19-51-25 545595235488  end print layer 206 cost time: 47.39s 
	行 1245: 2022-06-01,19-52-07 545595235488  end print layer 207 cost time: 41.44s 
	行 1251: 2022-06-01,19-52-54 545595235488  end print layer 208 cost time: 47.34s 
	行 1257: 2022-06-01,19-53-41 545595235488  end print layer 209 cost time: 47.18s 
	行 1263: 2022-06-01,19-54-28 545595235488  end print layer 210 cost time: 47.34s 
	行 1269: 2022-06-01,19-55-13 545595235488  end print layer 211 cost time: 44.30s 
	行 1275: 2022-06-01,19-55-54 545595235488  end print layer 212 cost time: 41.42s 
	行 1281: 2022-06-01,19-56-42 545595235488  end print layer 213 cost time: 47.42s 
	行 1287: 2022-06-01,19-57-23 545595235488  end print layer 214 cost time: 41.41s 
	行 1293: 2022-06-01,19-58-04 545595235488  end print layer 215 cost time: 41.38s 
	行 1299: 2022-06-01,19-58-48 545595235488  end print layer 216 cost time: 44.11s 
	行 1305: 2022-06-01,19-59-36 545595235488  end print layer 217 cost time: 47.42s 
	行 1311: 2022-06-01,20-00-20 545595235488  end print layer 218 cost time: 44.32s 
	行 1317: 2022-06-01,20-01-04 545595235488  end print layer 219 cost time: 44.28s 
	行 1323: 2022-06-01,20-01-52 545595235488  end print layer 220 cost time: 47.37s 
	行 1329: 2022-06-01,20-02-36 545595235488  end print layer 221 cost time: 44.26s 
	行 1335: 2022-06-01,20-03-20 545595235488  end print layer 222 cost time: 44.25s 
	行 1341: 2022-06-01,20-04-05 545595235488  end print layer 223 cost time: 44.26s 
	行 1347: 2022-06-01,20-04-49 545595235488  end print layer 224 cost time: 44.25s 
	行 1353: 2022-06-01,20-05-36 545595235488  end print layer 225 cost time: 47.36s 
	行 1359: 2022-06-01,20-06-24 545595235488  end print layer 226 cost time: 47.40s 
	行 1365: 2022-06-01,20-07-08 545595235488  end print layer 227 cost time: 44.26s 
	行 1371: 2022-06-01,20-07-55 545595235488  end print layer 228 cost time: 47.41s 
	行 1377: 2022-06-01,20-08-43 545595235488  end print layer 229 cost time: 47.45s 
	行 1383: 2022-06-01,20-09-24 545595235488  end print layer 230 cost time: 41.35s 
	行 1389: 2022-06-01,20-10-08 545595235488  end print layer 231 cost time: 44.24s 
	行 1395: 2022-06-01,20-10-50 545595235488  end print layer 232 cost time: 41.39s 
	行 1401: 2022-06-01,20-11-37 545595235488  end print layer 233 cost time: 47.42s 
	行 1407: 2022-06-01,20-12-25 545595235488  end print layer 234 cost time: 47.42s 
	行 1413: 2022-06-01,20-13-12 545595235488  end print layer 235 cost time: 47.38s 
	行 1419: 2022-06-01,20-13-59 545595235488  end print layer 236 cost time: 47.30s 
	行 1425: 2022-06-01,20-14-47 545595235488  end print layer 237 cost time: 47.33s 
	行 1431: 2022-06-01,20-15-34 545595235488  end print layer 238 cost time: 47.35s 
	行 1437: 2022-06-01,20-16-21 545595235488  end print layer 239 cost time: 47.31s 
	行 1443: 2022-06-01,20-17-09 545595235488  end print layer 240 cost time: 47.40s 
	行 1449: 2022-06-01,20-17-56 545595235488  end print layer 241 cost time: 47.35s 
	行 1455: 2022-06-01,20-18-43 545595235488  end print layer 242 cost time: 47.32s 
	行 1461: 2022-06-01,20-19-30 545595235488  end print layer 243 cost time: 47.18s 
	行 1467: 2022-06-01,20-20-18 545595235488  end print layer 244 cost time: 47.39s 
	行 1473: 2022-06-01,20-21-05 545595235488  end print layer 245 cost time: 47.42s 
	行 1479: 2022-06-01,20-21-47 545595235488  end print layer 246 cost time: 41.50s 
	行 1485: 2022-06-01,20-22-28 545595235488  end print layer 247 cost time: 41.47s 
	行 1491: 2022-06-01,20-23-10 545595235488  end print layer 248 cost time: 41.35s 
	
	----以上时间突变结束
	
	行 1497: 2022-06-01,20-23-22 545595235488  end print layer 249 cost time: 12.86s 
	行 1503: 2022-06-01,20-23-35 545595235488  end print layer 250 cost time: 12.62s 
```



```cassandra
-----89层具体打印信息
2022-06-01,18-26-05 545595235488  begin print layer 89 
2022-06-01,18-26-06 545595235488  begin Exposure layer 89 wait time: 1250 
2022-06-01,18-26-07 545595235488  end Exposure end  
2022-06-01,18-26-07 545595235488  begin peel layer 89 percent: 161.6649932861328 Number: 14 up dis: Vector{ 1600 2400 3600 6900 18900 } down dis: Vector{ -18000 -18850 -18850 -18850 -18850 } 
2022-06-01,18-26-18 545595235488  begin wait layer 89 percent: 161.6649932861328 Number: 14 wait time: 12100 
2022-06-01,18-26-30 545595235488  end print layer 89 cost time: 24.84s 

----90层
2022-06-01,18-26-30 545595235488  begin print layer 90 
2022-06-01,18-26-31 545595235488  begin Exposure layer 90 wait time: 1250 
2022-06-01,18-26-32 545595235488  end Exposure end  
2022-06-01,18-26-32 545595235488  begin peel layer 90 percent: 160.57208251953125 Number: 14 up dis: Vector{ 1600 2400 3600 6900 18900 } down dis: Vector{ -18000 -18850 -18850 -18850 -18850 } 
2022-06-01,18-26-41 545595235488  begin wait layer 90 percent: 160.57208251953125 Number: 14 wait time: 12100 
2022-06-01,18-26-53 545595235488  end print layer 90 cost time: 22.90s 

------91层
2022-06-01,18-26-53 545595235488  begin print layer 91 
2022-06-01,18-26-54 545595235488  begin Exposure layer 91 wait time: 1250 
2022-06-01,18-26-55 545595235488  end Exposure end  
2022-06-01,18-26-55 545595235488  begin peel layer 91 percent: 159.41864013671875 Number: 13 up dis: Vector{ 1600 2400 3600 12900 12900 } down dis: Vector{ -12000 -12850 -12850 -12850 -12850 } 
2022-06-01,18-27-28 545595235488  begin wait layer 91 percent: 159.41864013671875 Number: 13 wait time: 9500 
2022-06-01,18-27-38 545595235488  end print layer 91 cost time: 44.42s 
```



4K上第13段运行时间为

```cassandra
[2022-05-31 14:53:40.617] [TRACE] PublishMsgProcess 675 msgkey: "1002"
[2022-05-31 14:53:45.457] [TRACE] - 26 - [wait][time] 9501 [wait][offset time] 1
[2022-05-31 14:53:45.457] [TRACE]  ====== Begin Read Model  27 `th Loop ====== 
[2022-05-31 14:53:45.457] [DEBUG] [ "m108.ult" ] layer done
[2022-05-31 14:53:45.457] [DEBUG] ReadModel 291
[2022-05-31 14:53:45.457] [DEBUG] the buffer is not Empty
[2022-05-31 14:53:45.458] [DEBUG] [ "m108.ult" ] step: PrintCtrl::PrintStep(Preprocessing)
[2022-05-31 14:53:45.458] [DEBUG] Read Model Parser Finished!

-------打印开始
[2022-05-31 14:53:45.458] [DEBUG] - 27 - [exposure][begin]
[2022-05-31 14:53:45.458] [DEBUG] --------
[2022-05-31 14:53:45.458] [DEBUG] [ "m108.ult" ] layer start: 27 / 30
[2022-05-31 14:53:45.458] [TRACE] [ProjectCtrl] OnExposure
[2022-05-31 14:53:45.459] [TRACE] previewImg show time is  0
[2022-05-31 14:53:45.459] [TRACE] Discard Led Eff:  "LE_UNCOVERED"
[2022-05-31 14:53:45.459] [DEBUG] [ "m108.ult" ] step: PrintCtrl::PrintStep(Exposuring)
[2022-05-31 14:53:45.491] [TRACE] [ProjectCtrl] the current is: 309
[2022-05-31 14:53:45.491] [TRACE] [Projector] LedOn
[2022-05-31 14:53:45.491] [TRACE] [Ddp442x] setLedOnOff
[2022-05-31 14:53:45.491] [TRACE] [Ddp442xApi] GpioOpen
[2022-05-31 14:53:45.491] [TRACE] [Ddp442xApi] OpenWithRetry interfacenum: 2 , pre2retry: 3
[2022-05-31 14:53:45.492] [TRACE] SetLedOnOff
[2022-05-31 14:53:45.492] [TRACE] [ProjectorInterface] open_led success
[2022-05-31 14:53:45.492] [DEBUG] [Projector] LedOn result: no support
[2022-05-31 14:53:45.492] [TRACE] [ProjectCtrl] OnExposure preset time: 1500
[2022-05-31 14:53:45.522] [TRACE] PublishMsgProcess 675 msgkey: "1006"
[2022-05-31 14:53:46.993] [TRACE] [ProjectCtrl] [exposure][time]: 1534
[2022-05-31 14:53:46.993] [TRACE] [Projector] LedOff
[2022-05-31 14:53:46.994] [TRACE] [Ddp442x] setLedOnOff
[2022-05-31 14:53:46.994] [TRACE] [Ddp442xApi] GpioOpen
[2022-05-31 14:53:46.994] [TRACE] [Ddp442xApi] OpenWithRetry interfacenum: 2 , pre2retry: 3
[2022-05-31 14:53:46.995] [TRACE] SetLedOnOff
[2022-05-31 14:53:46.995] [TRACE] [ProjectorInterface] close_led success
[2022-05-31 14:53:46.998] [DEBUG] [Projector] LedOff result: no support
[2022-05-31 14:53:47.042] [DEBUG] begin SyncPeel
[2022-05-31 14:53:47.042] [TRACE] OnEnviromentCheck 57 data: QMap(("Projector", QVariant(bool, true))("Screen", QVariant(bool, true)))
[2022-05-31 14:53:47.042] [TRACE] - 27 - [exposure][time] 1584 [exposure][offset time] 84
[2022-05-31 14:53:47.042] [TRACE] command: "ac100118ff00000400000001d227acdc"
[2022-05-31 14:53:47.042] [DEBUG] [ "m108.ult" ] step: PrintCtrl::PrintStep(Peeling)
[2022-05-31 14:53:47.078] [DEBUG] NotifyComm 通訊返回 "ac100118ff00000400000001d227acdc"
[2022-05-31 14:53:47.137] [TRACE] Slave State change:  "ES-0 OPR-0 OPL-0 NP-1 ZT-0 ZB-0 ZS-0 ZR-0 ZZ-1 ZP-1 CAU-1 CAL-0 CGU-1 CGD-0 TL-1 CAE-0 ZAE-0 SP-1 ST-1 HES-1"  | F- "-93.40"
[2022-05-31 14:53:47.836] [TRACE] Slave State change:  "ES-0 OPR-0 OPL-0 NP-0 ZT-0 ZB-0 ZS-0 ZR-0 ZZ-1 ZP-1 CAU-1 CAL-0 CGU-1 CGD-0 TL-1 CAE-0 ZAE-0 SP-1 ST-1 HES-1"  | F- "19.10"
[2022-05-31 14:53:50.532] [TRACE] slave:
[2022-05-31 14:53:50.532] [TRACE] 	 |--- plateform: 1
[2022-05-31 14:53:50.533] [TRACE] 	 |--- force: 3.7
[2022-05-31 14:53:50.533] [TRACE] 	 |--- temp: 24.68
[2022-05-31 14:53:50.534] [TRACE] 	 |--- humidity: 59.66
[2022-05-31 14:53:50.631] [TRACE] PublishMsgProcess 675 msgkey: "1002"
[2022-05-31 14:54:00.531] [TRACE] slave:
[2022-05-31 14:54:00.532] [TRACE] 	 |--- force: 0.7
[2022-05-31 14:54:00.533] [TRACE] 	 |--- temp: 24.73
[2022-05-31 14:54:00.534] [TRACE] 	 |--- humidity: 59.65
[2022-05-31 14:54:00.535] [TRACE] heaint:
[2022-05-31 14:54:00.536] [TRACE] 	 |--- temp: 24.77
[2022-05-31 14:54:00.547] [TRACE] PublishMsgProcess 675 msgkey: "1002"
[2022-05-31 14:54:00.792] [TRACE] exe result: "ZAXIS->SEGMENTED_MOTION" "COMMAND_SUCCESS"
[2022-05-31 14:54:00.792] [DEBUG] end SyncPeel
[2022-05-31 14:54:00.793] [TRACE] Escape 0 1376520
[2022-05-31 14:54:00.794] [DEBUG] begin SyncPeel
[2022-05-31 14:54:00.794] [TRACE] command: "ac100118ff00000400000002d367acdc"
[2022-05-31 14:54:00.803] [DEBUG] discard slave return result 
[2022-05-31 14:54:00.821] [DEBUG] discard slave return result 
[2022-05-31 14:54:00.849] [TRACE] Slave State change:  "ES-0 OPR-0 OPL-0 NP-0 ZT-0 ZB-0 ZS-1 ZR-0 ZZ-1 ZP-0 CAU-1 CAL-0 CGU-1 CGD-0 TL-1 CAE-0 ZAE-0 SP-1 ST-1 HES-1"  | F- "0.60"
[2022-05-31 14:54:00.869] [DEBUG] NotifyComm 通訊返回 "ac100118ff00000400000002d367acdc"
[2022-05-31 14:54:00.936] [TRACE] Slave State change:  "ES-0 OPR-0 OPL-0 NP-0 ZT-0 ZB-0 ZS-0 ZR-0 ZZ-1 ZP-1 CAU-1 CAL-0 CGU-1 CGD-0 TL-1 CAE-0 ZAE-0 SP-1 ST-1 HES-1"  | F- "0.00"
[2022-05-31 14:54:02.536] [TRACE] Slave State change:  "ES-0 OPR-0 OPL-0 NP-1 ZT-0 ZB-0 ZS-0 ZR-0 ZZ-1 ZP-1 CAU-1 CAL-0 CGU-1 CGD-0 TL-1 CAE-0 ZAE-0 SP-1 ST-1 HES-1"  | F- "-11.60"
[2022-05-31 14:54:04.355] [TRACE] exe result: "ZAXIS->SEGMENTED_MOTION" "COMMAND_SUCCESS"
[2022-05-31 14:54:04.356] [DEBUG] end SyncPeel
[2022-05-31 14:54:04.356] [TRACE] Escape 0 1376520
[2022-05-31 14:54:04.356] [TRACE] [PrintCtrl] peel up: Curlayer: 27 Number: "13"
[2022-05-31 14:54:04.357] [TRACE] [PrintCtrl] speed[0]: 300, distance[0]: 1600
[2022-05-31 14:54:04.357] [TRACE] [PrintCtrl] speed[1]: 300, distance[1]: 2400
[2022-05-31 14:54:04.357] [TRACE] [PrintCtrl] speed[2]: 300, distance[2]: 3600
[2022-05-31 14:54:04.357] [TRACE] [PrintCtrl] speed[3]: 6000, distance[3]: 12900
[2022-05-31 14:54:04.357] [TRACE] [PrintCtrl] speed[4]: 6000, distance[4]: 12900
[2022-05-31 14:54:04.358] [TRACE] [PrintCtrl] peel down: Curlayer: 27 Number: "13"
[2022-05-31 14:54:04.358] [TRACE] [PrintCtrl] speed[0]: 6000, distance[0]: -12000
[2022-05-31 14:54:04.358] [TRACE] [PrintCtrl] speed[1]: 500, distance[1]: -12850
[2022-05-31 14:54:04.358] [TRACE] [PrintCtrl] speed[2]: 500, distance[2]: -12850
[2022-05-31 14:54:04.358] [TRACE] [PrintCtrl] speed[3]: 500, distance[3]: -12850
[2022-05-31 14:54:04.358] [TRACE] [PrintCtrl] speed[4]: 500, distance[4]: -12850
[2022-05-31 14:54:04.359] [TRACE] - 27 - [peel][time] 17314 [peel][offset time] 65
[2022-05-31 14:54:04.359] [DEBUG] [ "m108.ult" ] step: PrintCtrl::PrintStep(Waiting)
[2022-05-31 14:54:04.436] [TRACE] Slave State change:  "ES-0 OPR-0 OPL-0 NP-1 ZT-0 ZB-0 ZS-1 ZR-0 ZZ-1 ZP-0 CAU-1 CAL-0 CGU-1 CGD-0 TL-1 CAE-0 ZAE-0 SP-1 ST-1 HES-1"  | F- "-101.50"
[2022-05-31 14:54:10.532] [TRACE] slave:
[2022-05-31 14:54:10.532] [TRACE] 	 |--- plateform: -1
[2022-05-31 14:54:10.533] [TRACE] 	 |--- force: -94
[2022-05-31 14:54:10.533] [TRACE] 	 |--- temp: 24.78
[2022-05-31 14:54:10.533] [TRACE] heaint:
[2022-05-31 14:54:10.533] [TRACE] 	 |--- temp: 23.88
[2022-05-31 14:54:10.559] [TRACE] PublishMsgProcess 675 msgkey: "1002"
[2022-05-31 14:54:13.856] [TRACE] - 27 - [wait][time] 9500 [wait][offset time] 0
[2022-05-31 14:54:13.856] [TRACE]  ====== Begin Read Model  28 `th Loop ====== 
[2022-05-31 14:54:13.856] [DEBUG] [ "m108.ult" ] layer done

------打印结束


[2022-05-31 14:54:13.856] [DEBUG] ReadModel 291
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
```

