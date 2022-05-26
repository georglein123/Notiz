M值工艺包中等待时间和下降时间关系对打印件表面质量影响的测试验证

总方案：选取标准模型圆柱，使用M值工艺包中的某段工艺参数进行打印测试，为了充分论证，分成两个方案，方案A：延长工艺包中某段的总时间，将增加的时间分别分配到等待时间和下降时间中，对比两者的打印件观察表面质量；方案B：不改变工艺包中某段的总时间，只是调节等待时间和下降时间，改变两者的占比，对比两者的打印件观察表面质量。

**模型选择**

分析发现90-160段的M值出现层数最多（使用4k满版全颌面牙模分析）

![image-20220415150717670](E:\文档\GitHub\Notiz\M值工艺包中下降段时间与等待段时间关系分析.assets\image-20220415150717670.png)

使用M=120的圆盘（半径38mm），h=6mm（底板h=1mm），打印观察表面质量（这样只用集中观察1段就可以推断时间的影响）

模型：半径38mm，高度6mm的圆柱

![S000001_P1](E:\文档\GitHub\Notiz\M值工艺包中下降段时间与等待段时间关系分析.assets\S000001_P1.png)

模型使用M值计算软件计算后为118

M值工艺包第13段参数

```c++
{
                "MLowerLimit": 90,
                "MUpperLimit": 160,
                "Number": 13,
                "WaitTime": 9500,
                "Z_AxisUp": [
                    { "v": 300, "s": 1600 },
                    { "v": 300, "s": 2400 },
                    { "v": 300, "s": 3600 },
                    { "v": 6000, "s": 12900 },
                    { "v": 6000, "s": 12900 }
                ],
                "Z_AxisDown": [
                    { "v": 6000, "s": -12000 },
                    { "v": 500, "s": -12850 },
                    { "v": 500, "s": -12850 },
                    { "v": 500, "s": -12850 },
                    { "v": 500, "s": -12850 }
                ]
            },
```

整个工艺包中的时间占比

目前最终使用的M值工艺包（骏哥改）每段时间：

考虑快速剥离策略（每段number中第1段就成功剥离）：

```c++
number 1
t_up1 : (150-0)/400 = 0.38
t_up_remain : (2900-150)/6000 = 0.46
sum of the up time:  0.84
t_down1 : (1850 - 0)/6000 = 0.31
t_down2 : (2850 - 1850)/4000 = 0.25
t_down3 : (2850 - 2850)/4000 = 0.0
t_down4 : (2850 - 2850)/4000 = 0.0
t_down5 : (2850 - 2850)/4000 = 0.0
sum of the down time: 0.56
waittime : 0.1
sum of the time: 0.84+0.56+0.1 =  1.5
waittime percent: 6.67%

number 2
t_up1 : (150-0)/400 = 0.38
t_up_remain : (2900-150)/6000 = 0.46
sum of the up time:  0.84
t_down1 : (1850 - 0)/6000 = 0.31
t_down2 : (2850 - 1850)/4000 = 0.25
t_down3 : (2850 - 2850)/4000 = 0.0
t_down4 : (2850 - 2850)/4000 = 0.0
t_down5 : (2850 - 2850)/4000 = 0.0
sum of the down time: 0.56
waittime : 0.2
sum of the time: 0.84+0.56+0.2 =  1.6
waittime percent: 12.50%

number 3
t_up1 : (170-0)/400 = 0.42
t_up_remain : (3900-170)/6000 = 0.62
sum of the up time:  1.04
t_down1 : (2850 - 0)/6000 = 0.47
t_down2 : (3850 - 2850)/4000 = 0.25
t_down3 : (3850 - 3850)/4000 = 0.0
t_down4 : (3850 - 3850)/4000 = 0.0
t_down5 : (3850 - 3850)/4000 = 0.0
sum of the down time: 0.72
waittime : 0.3
sum of the time: 1.04+0.72+0.3 =  2.06
waittime percent: 14.56%

number 4
t_up1 : (170-0)/400 = 0.42
t_up_remain : (3900-170)/6000 = 0.62
sum of the up time:  1.04
t_down1 : (2850 - 0)/6000 = 0.47
t_down2 : (3850 - 2850)/4000 = 0.25
t_down3 : (3850 - 3850)/4000 = 0.0
t_down4 : (3850 - 3850)/2000 = 0.0
t_down5 : (3850 - 3850)/2000 = 0.0
sum of the down time: 0.72
waittime : 0.4
sum of the time: 1.04+0.72+0.4 =  2.16
waittime percent: 18.52%

number 5
t_up1 : (200-0)/300 = 0.67
t_up_remain : (4900-200)/6000 = 0.78
sum of the up time:  1.45
t_down1 : (2850 - 0)/6000 = 0.47
t_down2 : (4850 - 2850)/4000 = 0.5
t_down3 : (4850 - 4850)/4000 = 0.0
t_down4 : (4850 - 4850)/4000 = 0.0
t_down5 : (4850 - 4850)/4000 = 0.0
sum of the down time: 0.97
waittime : 0.5
sum of the time: 1.45+0.97+0.5 =  2.92
waittime percent: 17.12%

number 6
t_up1 : (200-0)/300 = 0.67
t_up_remain : (4900-200)/6000 = 0.78
sum of the up time:  1.45
t_down1 : (2850 - 0)/6000 = 0.47
t_down2 : (4850 - 2850)/4000 = 0.5
t_down3 : (4850 - 4850)/4000 = 0.0
t_down4 : (4850 - 4850)/4000 = 0.0
t_down5 : (4850 - 4850)/4000 = 0.0
sum of the down time: 0.97
waittime : 0.6
sum of the time: 1.45+0.97+0.6 =  3.02
waittime percent: 19.87%

number 7
t_up1 : (300-0)/300 = 1.0
t_up_remain : (4900-300)/6000 = 0.77
sum of the up time:  1.77
t_down1 : (2850 - 0)/6000 = 0.47
t_down2 : (4850 - 2850)/4000 = 0.5
t_down3 : (4850 - 4850)/4000 = 0.0
t_down4 : (4850 - 4850)/4000 = 0.0
t_down5 : (4850 - 4850)/4000 = 0.0
sum of the down time: 0.97
waittime : 0.6
sum of the time: 1.77+0.97+0.6 =  3.34
waittime percent: 17.96%

number 8
t_up1 : (400-0)/300 = 1.33
t_up_remain : (4900-400)/6000 = 0.75
sum of the up time:  2.08
t_down1 : (2850 - 0)/6000 = 0.47
t_down2 : (3850 - 2850)/4000 = 0.25
t_down3 : (4850 - 3850)/2000 = 0.5
t_down4 : (4850 - 4850)/2000 = 0.0
t_down5 : (4850 - 4850)/2000 = 0.0
sum of the down time: 1.22
waittime : 1.8
sum of the time: 2.08+1.22+1.8 =  5.1
waittime percent: 35.29%

number 9
t_up1 : (400-0)/300 = 1.33
t_up_remain : (4900-400)/6000 = 0.75
sum of the up time:  2.08
t_down1 : (2850 - 0)/6000 = 0.47
t_down2 : (3850 - 2850)/4000 = 0.25
t_down3 : (4850 - 3850)/2000 = 0.5
t_down4 : (4850 - 4850)/2000 = 0.0
t_down5 : (4850 - 4850)/2000 = 0.0
sum of the down time: 1.22
waittime : 2.6
sum of the time: 2.08+1.22+2.6 =  5.9
waittime percent: 44.07%

number 10
t_up1 : (400-0)/300 = 1.33
t_up_remain : (4900-400)/6000 = 0.75
sum of the up time:  2.08
t_down1 : (2850 - 0)/6000 = 0.47
t_down2 : (3850 - 2850)/4000 = 0.25
t_down3 : (4850 - 3850)/2000 = 0.5
t_down4 : (4850 - 4850)/2000 = 0.0
t_down5 : (4850 - 4850)/2000 = 0.0
sum of the down time: 1.22
waittime : 3.0
sum of the time: 2.08+1.22+3.0 =  6.3
waittime percent: 47.62%

number 11
t_up1 : (400-0)/300 = 1.33
t_up_remain : (4900-400)/6000 = 0.75
sum of the up time:  2.08
t_down1 : (2850 - 0)/6000 = 0.47
t_down2 : (3850 - 2850)/4000 = 0.25
t_down3 : (4850 - 3850)/2000 = 0.5
t_down4 : (4850 - 4850)/2000 = 0.0
t_down5 : (4850 - 4850)/2000 = 0.0
sum of the down time: 1.22
waittime : 4.5
sum of the time: 2.08+1.22+4.5 =  7.8
waittime percent: 57.69%

number 12
t_up1 : (800-0)/300 = 2.67
t_up_remain : (4900-800)/6000 = 0.68
sum of the up time:  3.35
t_down1 : (2850 - 0)/6000 = 0.47
t_down2 : (3850 - 2850)/4000 = 0.25
t_down3 : (4850 - 3850)/2000 = 0.5
t_down4 : (4850 - 4850)/2000 = 0.0
t_down5 : (4850 - 4850)/2000 = 0.0
sum of the down time: 1.22
waittime : 7.2
sum of the time: 3.35+1.22+7.2 =  11.77
waittime percent: 61.17%

number 13
t_up1 : (1600-0)/300 = 5.33
t_up_remain : (12900-1600)/6000 = 1.88
sum of the up time:  7.21
t_down1 : (12000 - 0)/6000 = 2.0
t_down2 : (12850 - 12000)/500 = 1.7
t_down3 : (12850 - 12850)/500 = 0.0
t_down4 : (12850 - 12850)/500 = 0.0
t_down5 : (12850 - 12850)/500 = 0.0
sum of the down time: 3.7
waittime : 9.5
sum of the time: 7.21+3.7+9.5 =  20.41
waittime percent: 46.55%

number 14
t_up1 : (1600-0)/300 = 5.33
t_up_remain : (18900-1600)/10000 = 1.73
sum of the up time:  7.06
t_down1 : (18000 - 0)/10000 = 1.8
t_down2 : (18850 - 18000)/500 = 1.7
t_down3 : (18850 - 18850)/500 = 0.0
t_down4 : (18850 - 18850)/500 = 0.0
t_down5 : (18850 - 18850)/500 = 0.0
sum of the down time: 3.5
waittime : 12.1
sum of the time: 7.06+3.5+12.1 =  22.66
waittime percent: 53.40%

number 15
t_up1 : (1600-0)/200 = 8.0
t_up_remain : (18900-1600)/10000 = 1.73
sum of the up time:  9.73
t_down1 : (18000 - 0)/10000 = 1.8
t_down2 : (18850 - 18000)/500 = 1.7
t_down3 : (18850 - 18850)/500 = 0.0
t_down4 : (18850 - 18850)/500 = 0.0
t_down5 : (18850 - 18850)/500 = 0.0
sum of the down time: 3.5
waittime : 16.0
sum of the time: 9.73+3.5+16.0 =  29.23
waittime percent: 54.74%
```



该段上升、下降及等待时间

```c++
number13

t_up1 : (1600-0)/300 = 5.33
t_up_remain : (12900-1600)/6000 = 1.88
sum of the up time:  7.21
t_down1 : (12000 - 0)/6000 = 2.0
t_down2 : (12850 - 12000)/500 = 1.7
t_down3 : (12850 - 12850)/500 = 0.0
t_down4 : (12850 - 12850)/500 = 0.0
t_down5 : (12850 - 12850)/500 = 0.0
sum of the down time: 3.7
waittime : 9.5
sum of the time: 7.21+3.7+9.5 =  20.41
waittime percent: 46.55%
```

**对照组：**

使用该段工艺参数的打印件表面质量：

![image-20220418172335170](E:\文档\GitHub\Notiz\M值工艺包中下降段时间与等待段时间关系分析.assets\image-20220418172335170.png)

**方案A：延长工艺包13段的总时间，将增加的时间分别分配到等待时间和下降时间中，对比两者观察表面质量**

**实验组A.1：**

将13段的等待时间由9.5s增加20.5s后到30s，其他不变

![image-20220418172819387](E:\文档\GitHub\Notiz\M值工艺包中下降段时间与等待段时间关系分析.assets\image-20220418172819387.png)

该段工艺包参数：

```c++
{
                "MLowerLimit": 90,
                "MUpperLimit": 160,
                "Number": 13,
                "WaitTime": 30000,
                "Z_AxisUp": [
                    { "v": 300, "s": 1600 },
                    { "v": 300, "s": 2400 },
                    { "v": 300, "s": 3600 },
                    { "v": 6000, "s": 12900 },
                    { "v": 6000, "s": 12900 }
                ],
                "Z_AxisDown": [
                    { "v": 6000, "s": -12000 },
                    { "v": 500, "s": -12850 },
                    { "v": 500, "s": -12850 },
                    { "v": 500, "s": -12850 },
                    { "v": 500, "s": -12850 }
                ]
            },
```



打印结果：（左边为实验组A.1，右边为对照组）

![image-20220424155815448](E:\文档\GitHub\Notiz\M值工艺包中下降段时间与等待段时间关系分析.assets\image-20220424155815448.png)



结果：表面质量变好



**实验组A.2：**

将13段的下降速度降低从而将下降时间由3.7s增加20.5s后到24.21s，其他不变

![image-20220418181001040](E:\文档\GitHub\Notiz\M值工艺包中下降段时间与等待段时间关系分析.assets\image-20220418181001040.png)

修改后工艺包的该段：

```c++
{
                "MLowerLimit": 90,
                "MUpperLimit": 160,
                "Number": 13,
                "WaitTime": 9500,
                "Z_AxisUp": [
                    { "v": 300, "s": 1600 },
                    { "v": 300, "s": 2400 },
                    { "v": 300, "s": 3600 },
                    { "v": 6000, "s": 12900 },
                    { "v": 6000, "s": 12900 }
                ],
                "Z_AxisDown": [
                    { "v": 600, "s": -12000 },
                    { "v": 202, "s": -12850 },
                    { "v": 500, "s": -12850 },
                    { "v": 500, "s": -12850 },
                    { "v": 500, "s": -12850 }
                ]
            },
```

打印结果：（左边为实验组A.2，右边为对照组）

![image-20220424155952859](E:\文档\GitHub\Notiz\M值工艺包中下降段时间与等待段时间关系分析.assets\image-20220424155952859.png)



结果：表面质量并无明显好转，甚至更差



**方案B：不改变工艺包第13段的总时间，只是调节等待时间和下降时间，改变两者的占比，观察两者打印件的表面质量**

**实验组B.1：**

修改了第13段工艺包下降段速度和等待时间，使下降时间由之前的3.7s增加到8.7s，等待时间由之前的9.5s减小到4.5s，总时间不变

![image-20220415152534222](E:\文档\GitHub\Notiz\M值工艺包中下降段时间与等待段时间关系分析.assets\image-20220415152534222.png)



修改后的工艺包第13段工艺参数

```c++
{
                "MLowerLimit": 90,
                "MUpperLimit": 160,
                "Number": 13,
                "WaitTime": 4500,
                "Z_AxisUp": [
                    { "v": 300, "s": 1600 },
                    { "v": 300, "s": 2400 },
                    { "v": 300, "s": 3600 },
                    { "v": 6000, "s": 12900 },
                    { "v": 6000, "s": 12900 }
                ],
                "Z_AxisDown": [
                    { "v": 1714, "s": -12000 },
                    { "v": 500, "s": -12850 },
                    { "v": 500, "s": -12850 },
                    { "v": 500, "s": -12850 },
                    { "v": 500, "s": -12850 }
                ]
            }
```



打印结果：（左边为实验组B.1，右边为对照组）

![image-20220424155226673](E:\文档\GitHub\Notiz\M值工艺包中下降段时间与等待段时间关系分析.assets\image-20220424155226673.png)



结果：表面质量和对照组对比，变差



**实验组B.2：**

将下降时间由3.7s缩短2s到1.7s，等待时间由9.5s延长2s到11.5s，总时间不变

![image-20220419131841681](E:\文档\GitHub\Notiz\M值工艺包中下降段时间与等待段时间关系分析.assets\image-20220419131841681.png)

该段工艺包参数：

```c++
{
                "MLowerLimit": 90,
                "MUpperLimit": 160,
                "Number": 13,
                "WaitTime": 11500,
                "Z_AxisUp": [
                    { "v": 300, "s": 1600 },
                    { "v": 300, "s": 2400 },
                    { "v": 300, "s": 3600 },
                    { "v": 6000, "s": 12900 },
                    { "v": 6000, "s": 12900 }
                ],
                "Z_AxisDown": [
                    { "v": 12000, "s": -12000 },
                    { "v": 1214, "s": -12850 },
                    { "v": 500, "s": -12850 },
                    { "v": 500, "s": -12850 },
                    { "v": 500, "s": -12850 }
                ]
            },
```

打印结果：（左边为实验组B.2，右边为对照组）

![image-20220424155446035](E:\文档\GitHub\Notiz\M值工艺包中下降段时间与等待段时间关系分析.assets\image-20220424155446035.png)

结果：打印件表面质量与对照组相比，相似

经过以上对比发现：等待时间对打印件的表面质量影响权重更高，推测原因可能在打印过程中，由于曝光前硅胶回弹导致树脂液体流动，需要等待时间来使树脂静止稳定，此时再曝光会对打印件表面质量更好。而即使降低下降速度还是会扰动树脂液体，从而导致降低下降速度对表面质量的改善并不明显。





选择更大截面测试

整个工艺包中的时间占比

目前最终使用的M值工艺包（骏哥改）每段时间：

考虑快速剥离策略（每段number中第1段就成功剥离）：

```c++
number 1
t_up1 : (150-0)/400 = 0.38
t_up_remain : (2900-150)/6000 = 0.46
sum of the up time:  0.84
t_down1 : (1850 - 0)/6000 = 0.31
t_down2 : (2850 - 1850)/4000 = 0.25
t_down3 : (2850 - 2850)/4000 = 0.0
t_down4 : (2850 - 2850)/4000 = 0.0
t_down5 : (2850 - 2850)/4000 = 0.0
sum of the down time: 0.56
waittime : 0.1
sum of the time: 0.84+0.56+0.1 =  1.5
waittime percent: 6.67%

number 2
t_up1 : (150-0)/400 = 0.38
t_up_remain : (2900-150)/6000 = 0.46
sum of the up time:  0.84
t_down1 : (1850 - 0)/6000 = 0.31
t_down2 : (2850 - 1850)/4000 = 0.25
t_down3 : (2850 - 2850)/4000 = 0.0
t_down4 : (2850 - 2850)/4000 = 0.0
t_down5 : (2850 - 2850)/4000 = 0.0
sum of the down time: 0.56
waittime : 0.2
sum of the time: 0.84+0.56+0.2 =  1.6
waittime percent: 12.50%

number 3
t_up1 : (170-0)/400 = 0.42
t_up_remain : (3900-170)/6000 = 0.62
sum of the up time:  1.04
t_down1 : (2850 - 0)/6000 = 0.47
t_down2 : (3850 - 2850)/4000 = 0.25
t_down3 : (3850 - 3850)/4000 = 0.0
t_down4 : (3850 - 3850)/4000 = 0.0
t_down5 : (3850 - 3850)/4000 = 0.0
sum of the down time: 0.72
waittime : 0.3
sum of the time: 1.04+0.72+0.3 =  2.06
waittime percent: 14.56%

number 4
t_up1 : (170-0)/400 = 0.42
t_up_remain : (3900-170)/6000 = 0.62
sum of the up time:  1.04
t_down1 : (2850 - 0)/6000 = 0.47
t_down2 : (3850 - 2850)/4000 = 0.25
t_down3 : (3850 - 3850)/4000 = 0.0
t_down4 : (3850 - 3850)/2000 = 0.0
t_down5 : (3850 - 3850)/2000 = 0.0
sum of the down time: 0.72
waittime : 0.4
sum of the time: 1.04+0.72+0.4 =  2.16
waittime percent: 18.52%

number 5
t_up1 : (200-0)/300 = 0.67
t_up_remain : (4900-200)/6000 = 0.78
sum of the up time:  1.45
t_down1 : (2850 - 0)/6000 = 0.47
t_down2 : (4850 - 2850)/4000 = 0.5
t_down3 : (4850 - 4850)/4000 = 0.0
t_down4 : (4850 - 4850)/4000 = 0.0
t_down5 : (4850 - 4850)/4000 = 0.0
sum of the down time: 0.97
waittime : 0.5
sum of the time: 1.45+0.97+0.5 =  2.92
waittime percent: 17.12%

number 6
t_up1 : (200-0)/300 = 0.67
t_up_remain : (4900-200)/6000 = 0.78
sum of the up time:  1.45
t_down1 : (2850 - 0)/6000 = 0.47
t_down2 : (4850 - 2850)/4000 = 0.5
t_down3 : (4850 - 4850)/4000 = 0.0
t_down4 : (4850 - 4850)/4000 = 0.0
t_down5 : (4850 - 4850)/4000 = 0.0
sum of the down time: 0.97
waittime : 0.6
sum of the time: 1.45+0.97+0.6 =  3.02
waittime percent: 19.87%

number 7
t_up1 : (300-0)/300 = 1.0
t_up_remain : (4900-300)/6000 = 0.77
sum of the up time:  1.77
t_down1 : (2850 - 0)/6000 = 0.47
t_down2 : (4850 - 2850)/4000 = 0.5
t_down3 : (4850 - 4850)/4000 = 0.0
t_down4 : (4850 - 4850)/4000 = 0.0
t_down5 : (4850 - 4850)/4000 = 0.0
sum of the down time: 0.97
waittime : 0.6
sum of the time: 1.77+0.97+0.6 =  3.34
waittime percent: 17.96%

number 8
t_up1 : (400-0)/300 = 1.33
t_up_remain : (4900-400)/6000 = 0.75
sum of the up time:  2.08
t_down1 : (2850 - 0)/6000 = 0.47
t_down2 : (3850 - 2850)/4000 = 0.25
t_down3 : (4850 - 3850)/2000 = 0.5
t_down4 : (4850 - 4850)/2000 = 0.0
t_down5 : (4850 - 4850)/2000 = 0.0
sum of the down time: 1.22
waittime : 1.8
sum of the time: 2.08+1.22+1.8 =  5.1
waittime percent: 35.29%

number 9
t_up1 : (400-0)/300 = 1.33
t_up_remain : (4900-400)/6000 = 0.75
sum of the up time:  2.08
t_down1 : (2850 - 0)/6000 = 0.47
t_down2 : (3850 - 2850)/4000 = 0.25
t_down3 : (4850 - 3850)/2000 = 0.5
t_down4 : (4850 - 4850)/2000 = 0.0
t_down5 : (4850 - 4850)/2000 = 0.0
sum of the down time: 1.22
waittime : 2.6
sum of the time: 2.08+1.22+2.6 =  5.9
waittime percent: 44.07%

number 10
t_up1 : (400-0)/300 = 1.33
t_up_remain : (4900-400)/6000 = 0.75
sum of the up time:  2.08
t_down1 : (2850 - 0)/6000 = 0.47
t_down2 : (3850 - 2850)/4000 = 0.25
t_down3 : (4850 - 3850)/2000 = 0.5
t_down4 : (4850 - 4850)/2000 = 0.0
t_down5 : (4850 - 4850)/2000 = 0.0
sum of the down time: 1.22
waittime : 3.0
sum of the time: 2.08+1.22+3.0 =  6.3
waittime percent: 47.62%

number 11
t_up1 : (400-0)/300 = 1.33
t_up_remain : (4900-400)/6000 = 0.75
sum of the up time:  2.08
t_down1 : (2850 - 0)/6000 = 0.47
t_down2 : (3850 - 2850)/4000 = 0.25
t_down3 : (4850 - 3850)/2000 = 0.5
t_down4 : (4850 - 4850)/2000 = 0.0
t_down5 : (4850 - 4850)/2000 = 0.0
sum of the down time: 1.22
waittime : 4.5
sum of the time: 2.08+1.22+4.5 =  7.8
waittime percent: 57.69%

number 12
t_up1 : (800-0)/300 = 2.67
t_up_remain : (4900-800)/6000 = 0.68
sum of the up time:  3.35
t_down1 : (2850 - 0)/6000 = 0.47
t_down2 : (3850 - 2850)/4000 = 0.25
t_down3 : (4850 - 3850)/2000 = 0.5
t_down4 : (4850 - 4850)/2000 = 0.0
t_down5 : (4850 - 4850)/2000 = 0.0
sum of the down time: 1.22
waittime : 7.2
sum of the time: 3.35+1.22+7.2 =  11.77
waittime percent: 61.17%

number 13
t_up1 : (1600-0)/300 = 5.33
t_up_remain : (12900-1600)/6000 = 1.88
sum of the up time:  7.21
t_down1 : (12000 - 0)/6000 = 2.0
t_down2 : (12850 - 12000)/500 = 1.7
t_down3 : (12850 - 12850)/500 = 0.0
t_down4 : (12850 - 12850)/500 = 0.0
t_down5 : (12850 - 12850)/500 = 0.0
sum of the down time: 3.7
waittime : 9.5
sum of the time: 7.21+3.7+9.5 =  20.41
waittime percent: 46.55%

number 14
t_up1 : (1600-0)/300 = 5.33
t_up_remain : (18900-1600)/10000 = 1.73
sum of the up time:  7.06
t_down1 : (18000 - 0)/10000 = 1.8
t_down2 : (18850 - 18000)/500 = 1.7
t_down3 : (18850 - 18850)/500 = 0.0
t_down4 : (18850 - 18850)/500 = 0.0
t_down5 : (18850 - 18850)/500 = 0.0
sum of the down time: 3.5
waittime : 12.1
sum of the time: 7.06+3.5+12.1 =  22.66
waittime percent: 53.40%

number 15
t_up1 : (1600-0)/200 = 8.0
t_up_remain : (18900-1600)/10000 = 1.73
sum of the up time:  9.73
t_down1 : (18000 - 0)/10000 = 1.8
t_down2 : (18850 - 18000)/500 = 1.7
t_down3 : (18850 - 18850)/500 = 0.0
t_down4 : (18850 - 18850)/500 = 0.0
t_down5 : (18850 - 18850)/500 = 0.0
sum of the down time: 3.5
waittime : 16.0
sum of the time: 9.73+3.5+16.0 =  29.23
waittime percent: 54.74%
```

4K全颌面牙模中最大的M值为167（大M值的截面等待时间较长，才具有优化可行性）

![image-20220505095603088](E:\文档\GitHub\Notiz\M值工艺包中等待时间和下降时间关系对打印件表面质量影响的测试验证.assets\image-20220505095603088.png)

使用M=167的圆盘（半径？mm），h=6mm（底板h=1mm），打印观察表面质量（这样只用集中观察1段就可以推断时间的影响）

圆盘半径r为46mm，计算出来的M值173.39

![S000001_P1](E:\文档\GitHub\Notiz\M值工艺包中等待时间和下降时间关系对打印件表面质量影响的测试验证.assets\S000001_P1.png)

```c++
number 14
t_up1 : (1600-0)/300 = 5.33
t_up_remain : (18900-1600)/10000 = 1.73
sum of the up time:  7.06
t_down1 : (18000 - 0)/10000 = 1.8
t_down2 : (18850 - 18000)/500 = 1.7
t_down3 : (18850 - 18850)/500 = 0.0
t_down4 : (18850 - 18850)/500 = 0.0
t_down5 : (18850 - 18850)/500 = 0.0
sum of the down time: 3.5
waittime : 12.1
sum of the time: 7.06+3.5+12.1 =  22.66
waittime percent: 53.40%
```

方案A

A.1：等待时间由12.1s增加17.9s变成30s



A.2:：更换下降速度，增加下降时间由3.5s增加17.9s到21.4s，

```c++
number 14
t_up1 : (1600-0)/300 = 5.33
t_up_remain : (18900-1600)/10000 = 1.73
sum of the up time:  7.06
t_down1 : (18000 - 0)/1000 = 18.0
t_down2 : (18850 - 18000)/250 = 3.4
t_down3 : (18850 - 18850)/500 = 0.0
t_down4 : (18850 - 18850)/500 = 0.0
t_down5 : (18850 - 18850)/500 = 0.0
sum of the down time: 21.4
waittime : 12.1
sum of the time: 7.06+21.4+12.1 =  40.56
waittime percent: 29.83%
```

**方案B：不改变工艺包第14段的总时间，只是调节等待时间和下降时间，改变两者的占比，观察两者打印件的表面质量**

**实验组B.1：**

修改了第14段工艺包下降段速度和等待时间，使下降时间由之前的3.5s增加5s到8.5s，等待时间由之前的12.1s减小5s到7.1s，总时间不变

```c++
number 14
t_up1 : (1600-0)/300 = 5.33
t_up_remain : (18900-1600)/10000 = 1.73
sum of the up time:  7.06
t_down1 : (18000 - 0)/10000 = 1.8
t_down2 : (18850 - 18000)/127 = 6.69
t_down3 : (18850 - 18850)/500 = 0.0
t_down4 : (18850 - 18850)/500 = 0.0
t_down5 : (18850 - 18850)/500 = 0.0
sum of the down time: 8.49
waittime : 7.1
sum of the time: 7.06+8.49+7.1 =  22.65
waittime percent: 31.35%
```



**实验组B.2：**

将下降时间由3.5s缩短2s到1.5s，等待时间由12.1s延长2s到14.1s，总时间不变

```c++
number 14
t_up1 : (1600-0)/300 = 5.33
t_up_remain : (18900-1600)/10000 = 1.73
sum of the up time:  7.06
t_down1 : (18000 - 0)/20000 = 0.9
t_down2 : (18850 - 18000)/1418 = 0.6
t_down3 : (18850 - 18850)/500 = 0.0
t_down4 : (18850 - 18850)/500 = 0.0
t_down5 : (18850 - 18850)/500 = 0.0
sum of the down time: 1.5
waittime : 14.1
sum of the time: 7.06+1.5+14.1 =  22.66
waittime percent: 62.22%
```



增加等待时间不容易掉板
