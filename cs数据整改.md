CS数据整改

连接客户设备后，将对应数据放入指定文件夹

![image-20220919142507795](E:\文档\GitHub\Notiz\ChairSide已发货设备自动均匀性校准整改方案流程.assets\image-20220919142507795.png)

**获取近似自动光强P**

将calibration.db文件导出为csv文件

![image-20220919143055000](E:\文档\GitHub\Notiz\ChairSide已发货设备自动均匀性校准整改方案流程.assets\image-20220919143055000.png)

然后运行csv_gray_to_mask.py，生成文件mask_24.png

![image-20220919143008600](E:\文档\GitHub\Notiz\ChairSide已发货设备自动均匀性校准整改方案流程.assets\image-20220919143008600.png)

打开t_light_intensity_adjust.csv，将energy栏的数值乘1e-4，获得右边栏的能量值

![image-20220919143409189](E:\文档\GitHub\Notiz\ChairSide已发货设备自动均匀性校准整改方案流程.assets\image-20220919143409189.png)

然后将该栏数据放入手动mask手动PI模板中的Energy栏中

![image-20220919143549690](E:\文档\GitHub\Notiz\ChairSide已发货设备自动均匀性校准整改方案流程.assets\image-20220919143549690.png)

接着点击图表，查看图表数据框是否在所有数据范围中

![image-20220919144039567](E:\文档\GitHub\Notiz\ChairSide已发货设备自动均匀性校准整改方案流程.assets\image-20220919144039567.png)

并确定“输入左侧列表范围”中四个值分别对应左边列表的四个值，从而下方的系数和图表中的系数相同，从而生成手动光强P

![image-20220919150836944](E:\文档\GitHub\Notiz\ChairSide已发货设备自动均匀性校准整改方案流程.assets\image-20220919150836944.png)



然后使用cs_center_gray_capturing.py脚本获取自动校准生成的mask和手动的mask_24中心灰度值，然后复制进入表格对应位置的手动灰度和自动灰度，就可以获得最后一栏的近似自动光强P，将该近似自动光强P复制粘贴放入cs_发货整改excel中的自动mask手动PI：设备端I——P的光强P中

![image-20220921092707890](E:\文档\GitHub\Notiz\ChairSide已发货设备自动均匀性校准整改方案流程.assets\image-20220921092707890.png)



**获取设备端IG数据**

客户做完自动均匀性校准后，获取日志文件，然后使用cs_whole_process_data_collecting.py脚本运行，获取设备端IG数据，将灰度G数据复制粘贴放入cs_发货整改excel中的首次自校：设备端I——G的avgGray中

![image-20220921092941919](E:\文档\GitHub\Notiz\ChairSide已发货设备自动均匀性校准整改方案流程.assets\image-20220921092941919.png)



**cs_发货整改excel的使用及拟合参数序列化**

见word文件



**拟合参数写入config.db文件**

拟合参数写入config.db文件，同时确定其他参数如缩放系数是否正确，并将config.db先上传指Downloads路径下，然后使用命令行操作sudo cp /home/heygears/Downloads/config.db /home/heygears/ultracore/.db，最后在/home/heygears/ultracore/.db路径下打开config.db，查看是否是写入的正确参数



**复核拟合参数是否成功写入**

整改完成后客户会再做一次自动均匀性校准，打开日志文件，搜索关键字gg_coeffs_list，若参数和写入参数一致，则更改成功

