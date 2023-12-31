**M值工艺包中等待时间对A2D 4K打印机打印满版全颌面实心牙模精度的影响**

**现象：**

在A2D 4K 打印机上使用M值工艺包打印满版全颌面实心牙模（模型如下图）在一个像素误差范围内53.3um的精度大约在76%，精度不合格

![image-20220422094442584](E:\文档\GitHub\Notiz\M值工艺包中等待时间对A2D 4K打印机打印满版全颌面实心牙模精度的影响.assets\image-20220422094442584.png)

![image-20220422094154169](E:\文档\GitHub\Notiz\M值工艺包中等待时间对A2D 4K打印机打印满版全颌面实心牙模精度的影响.assets\image-20220422094154169.png)

在A2D 4K 打印机上使用现行工艺包`13_Model HP 2.0 UV Grey Solid_50_E&P`打印满版全颌面实心牙模在一个像素误差范围内53.3um的精度在81%，误差范围50um的精度是80%，精度合格

![image-20220422095038496](E:\文档\GitHub\Notiz\M值工艺包中等待时间对A2D 4K打印机打印满版全颌面实心牙模精度的影响.assets\image-20220422095038496.png)



**分析：**

精度体现在牙模外形尺寸的匹配程度上，而牙模外形尺寸的主要影响因素有：打印的树脂种类、打印缩放系数、打印曝光时间和打印过程中的运动速度等待时间等，经过对比分析，这两版打印的主要差别在于使用的工艺包不同，导致打印过程中的运动速度等待时间不同，从而影响精度。



**测试：**

更改M值工艺包中的等待时间，测试能否提高精度

- **确定牙模牙齿部分对应切片层数**

精度对比的主要部分是牙模牙齿部分，根据模型确定牙齿部分对应的切片文件层数

![image-20220413154901032](E:\文档\GitHub\Notiz\M值工艺包中等待时间对A2D 4K打印机打印满版全颌面实心牙模精度的影响.assets\image-20220413154901032.png)

17.562/0.05 = 351，因此确定牙齿部分的切片文件层数为351层之后



- **根据截面占比和M值分别确定模型每一层使用的对应的工艺包段**

**现行工艺包调用段：**

177-359层调用第3段，360-473层调用第2段，474-531调用第1段

**M值工艺包调用段：**

253-334层调用第12段，335-372层调用第11段，373-386层调用第10段，387-399层调用第9段，400-412层调用第8段，413-427层调用第7段，428-429层第6段，430-431层第5段，432-446层第4段，447-453层第3段， 454-463层第2段，464-531层第1段



- **将M值工艺包使用到牙齿部分层的工艺包段中的等待时间和现行工艺包对应一致**

 [只修改等待时间和既改等待时间又改运动参数对比.pdf](..\..\..\intersecting surface\4K测试使用M值工艺包\继续优化\只修改等待时间的工艺包\只修改等待时间和既改等待时间又改运动参数对比.pdf) 



- **打印测试查看逆扫精度**

53. 5um误差范围内的精度为88%

![image-20220414142012613](E:\文档\GitHub\Notiz\M值工艺包中等待时间对A2D 4K打印机打印满版全颌面实心牙模精度的影响.assets\image-20220414142012613.png)

50um误差范围内的精度为86%

![image-20220414141849078](E:\文档\GitHub\Notiz\M值工艺包中等待时间对A2D 4K打印机打印满版全颌面实心牙模精度的影响.assets\image-20220414141849078.png)

- **总结**

经过测试发现，打印过程中的运动参数等待时间会对模型的精度产生影响，打印的等待时间和精度呈现正相关，推测原因由于等待时间越长，成型平台和料盘之间的树脂排液越充分，排液充分后再进行曝光，模型的精度从而更高。

