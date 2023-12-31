目前M值问题汇总

1.图层间M值突变：两张相似图层计算出的M值差异很大，导致打印横纹出现；

2.工艺包开发等待时间选取：打印高M值的测试圆柱，若要打印出表面质量好效果，需要长时间的剥离和等待时间，会严重影响打印效率；

3.牙模精度和工艺包等待时间平衡：工艺包提速过快，牙模精度偏低，适当加长工艺包的等待时间可提高牙模精度；

4.底板层剥离失败：由于底板层的剥离算法计算后的首段剥离行程与工艺包内第二段的行程会冲突，导致打印第一层时报错“剥离失败”；

5.底板段的表面质量：相对于同M值得实体段质量要好，可能与轮廓分离策略有关；

6.打印剥离力变大而出现打印横纹：在M值工艺包提速下打印剥离力会高于现行工艺包，在长期打印对平台锁紧结构有更高的要求，若平台有松动，牙模打印容易出现横纹，在4K打印机上有明显感受；

7.倒杯口效应：由于M值工艺包与现行工艺包均无法识别出带有倒杯口效应的牙模，但M值工艺包的打印速度更快一些和等待时间更短一些，会更容易出现或加重异常纹理；

8.代型台阶面的剥离力突变：有几层出现剥离力突然变大；



解决办法：

1.图层间M值突变：两张相似图层计算出的M值差异很大，导致打印横纹出现；

**M值计算路线优化，采取新的M值判断路线方案，目前已完成优化，无非正常突变问题**

2.工艺包开发等待时间选取：打印高M值的测试圆柱，若要打印出表面质量好效果，需要长时间的剥离和等待时间，会严重影响打印效率；

**在不同应用类型上做确定，在不同应用上开发M值工艺包时，M值的分段选择；可以是平均分段，效率最高，但是如果对最花时间的段进行划分开发，对节约时间最好**

3.牙模精度和工艺包等待时间平衡：工艺包提速过快，牙模精度偏低，适当加长工艺包的等待时间可提高牙模精度；

**增加等待时间或调节缩放系数**

4.底板层剥离失败：由于底板层的剥离算法计算后的首段剥离行程与工艺包内第二段的行程会冲突，导致打印第一层时报错“剥离失败”；

**目前底板运动方案：直接计算当前层M值，进入对应区间，但是要将前4段的剥离行程增加，具体为：工艺包每一大段分为上剥离和下剥离，其中上剥离有5个小段，前3段为慢速剥离过程，增加工艺包第3段的行程**



**正在开发新的底板策略，预计下周完成**

5.底板段的表面质量：相对于同M值的实体段质量要好，可能与轮廓分离策略有关；

**轮廓分离策略会使表面质量变差**

6.打印剥离力变大而出现打印横纹：在M值工艺包提速下打印剥离力会高于现行工艺包，在长期打印对平台锁紧结构有更高的要求，若平台有松动，牙模打印容易出现横纹，在4K打印机上有明显感受；

7.倒杯口效应：由于M值工艺包与现行工艺包均无法识别出带有倒杯口效应的牙模，但M值工艺包的打印速度更快一些和等待时间更短一些，会更容易出现或加重异常纹理；

**截面识别策略无法处理倒杯口效应，只能按照现行工艺包增加等待时间处理**

8.代型台阶面的剥离力突变：有几层出现剥离力突然变大；

**台阶面识别策略正在开发中，下一阶段导入**

