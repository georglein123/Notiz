A3D

1.机台上日志信息保留一周，不用覆盖

2.协调机台案例打印测试

3.

日志查看

![image-20220517144829678](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20220517144829678.png)



A3D上打印出现的问题：

- 打印全幅面4个空心标牙，最后几层M值计算为0，但是等待时间也为0（应该会进入第1段M值为0的段，等待时间也有100us）

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
[compute]valid items nums: 12
[compute]M > M_thre nums: 12
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
[compute]valid items nums: 12
[compute]M > M_thre nums: 8
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

