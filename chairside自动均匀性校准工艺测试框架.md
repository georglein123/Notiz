框架

- 设备：3台A2D，HP 2.0

- 项目：
  1. 测量光强（极差）
  2. 标牙逆扫
  3. 幅面一致性（圆形件）
  4. 分割代型
  5. 种植模型

​		

1. 测量光强：

   1. 3种光斑图：40个圆形光斑，方形光斑，偏移圆形光斑，120x90 px方格光斑图

   *：LED光强校准

2. 标牙逆扫

3. 幅面一致性

   1. 圆斑光强结果标准
   2. 2个料盘2号和3号打印3次测量

4. 分割代型

5. 种植模型



## chairside自动均匀性校准工艺测试



### 光强检测：

目的：检测自动均匀性校准模块的优劣并和手动校准对比

圆形光斑（数量6x4）、120x90 px方形光斑

V1.0

初始机器——圆斑检测光强——手动校准（LED校准）——圆形光斑、120x90 px方形光斑——删除手动校准的mask——自动均匀性校准（手动LED校准）——圆形光斑、120x90 px方形光斑

流程：

1. 打开chairside上位机，插入光度计，点击“均匀性校准”，读取各个点光强（6x4），并在电脑excel上记录各点光强
2. 重新返回到“均匀性校准”，调节各个点的灰度，进行光强校准
3. 完成之后，点击“LED校准”，将幅面光强拉到21W
4. 再次返回“均匀性校准”，投出圆形光斑，读取各个点光强，并在电脑excel上记录各点光强
5. 投方形光斑，读取各个点光强，并在电脑excel记录各点光强

   - chairside 120x90 px方形光斑图制作
   - ~~电脑投图~~还是上位机投图：
      - **电脑投图的话**上位机校准后的mask不能被应用？
        - 将手动校准的灰度文件拷贝出来，在opencv中划分成对应区域，区域内填充对应灰度值，即为手动校准的mask，然后再和要测试的图进行与运算
      - 手动校准的mask拷出电脑应用于方形光斑
      - ~~上位机投图的话如何将图导入到上位机中并应用手动均匀性校准后的mask~~
      - ~~外部图导入上位机如何操作~~

6. 移走手动均匀性校准的mask（复制下来，留在后面打印圆环件时使用），使chairside重新回到幅面光强不均匀的状态

    - 删除方法（请教肖工）
    - ~~是否增加重新投图圆形光斑，记录光强检测验证是否幅面不均匀状态~~（可以检测几个点粗略验证一下）
7. 插上自动均匀性校准模块，运行自动均匀性校准算法，获得mask，处理后投黑斑图，读取光强并在电脑excel上记录（自动均匀性校准使用介绍或人员配合）

    - 获得的mask在chairside外部
    - mask与圆斑图进行与运算，使得圆斑中心位置获得对应mask的值
       - 处理之后的圆斑图使用**~~电脑投图~~**还是上位机投图？
         - 上位机连接优盘指定投图（省略导出上位机手动校准的mask并作用于方形图操作）
         - 自动均匀性校准获取的mask如何保存到chairside中并运用在之后的打印测试中
         - ~~可以使用电脑投图检测，但是使用上位机投图检测更具有一致性与稳定性~~
           - 使用电脑投图需先设置电流使得光度计读数接近打印光强21W
    - 自动均匀性校准获取的mask应用到chairside上并进行“LED校准”（光强提升到21W）的流程和软件组细化，这会在打印测试件时需要使用到

8. 利用步骤7中同一张mask处理后投120x90 px方形光斑，读取光强并在电脑excel上记录

    - 处理方式类似步骤7
9. 处理数据
    - 数据结果呈现参考《自动均匀性校准测试报告20210729-2》对应部分

**沟通：**

幅面均匀后检测投图：圆斑图、方形图

- 出：手动均匀校准的mask拷出，（然后作用于方形图：与运算）
  - mask数据形式，如何作用于方形图上
  - 删除这张mask是否要放什么文件代替？
  - 拷贝到电脑里复制一份，之后打印圆环件需要使用
- 入：自动均匀性校准的mask拷入，（之后用于打印测试）
- 方形图制作



V1.1

初始机器——圆斑——手动均匀性校准——圆斑、120x90方形图——自动均匀性校准——圆斑、120x90方形图——处理数据

流程：

1. chairside插上光度计，点击“均匀性校准”，投圆斑图，记录各个点光强并拷贝下此时系统中的灰度文件（将灰度文件值都调节成255）（记录打印机原始幅面状态）
2. 回到“均匀性校准”，调节灰度值，使幅面光强均匀，完成后点击“LED校准”，将光强提升到21W（手动均匀性校准）
3. 继续回到“均匀性校准”，投圆斑图，记录各个点光强（记录手动均匀性校准后的幅面光强状态）
4. 插入优盘，点击“指定投图”，投120x90方形图（分辨率1920x1080），打开电脑上光度计读数软件读取光强，记录各个点光强（记录手动均匀性校准后的幅面更加细化的光强状态）
   - **指定投图是否已运用手动校准灰度文件？**——已使用

5. 移走手动均匀性校准的灰度文件，备着后面使用，导入在步骤1中拷贝的灰度文件（使幅面光强状态重新回到手动校准前的状态）
   - **灰度文件存放位置**

6. 插上自动均匀性校准模块，进行自动均匀性校准，**使自动均匀性校准产生的mask导入到上位机并应用于投图和打印**
7. （自动均匀性校准产生的mask作用于上位机之后）回到“均匀性校准”，投圆斑图，记录各个点光强
   - **输入：优盘指定投图的一张图片（圆斑图，120x90方形图，分辨率1920x1080）**
   - **输出：带有自动均匀性校准后灰度的图片**
   - **问题：自动均匀性校准后是否手动LED校准？**——手动LED校准光强提升到21w
   - 如果自动均匀性校准产生的mask暂时无法作用于上位机，可以先用电脑处理圆斑图和120x90方形图，再使用优盘“指定投图”

8. 插入优盘，使用“指定投图”，投120x90方形图，记录各个点光强
9. 处理数据



沟通：

- 手动校准的灰度文件在打印机中的位置
- 自动均匀性校准的mask如何作用于打印机
  - 需求：
    - 光强检测
      - 输入：优盘指定投图一张图片（120x90方形图）
      - 输出：带有自动均匀性校准后灰度的图片

    - 打印测试
      - 输入：导入到打印机中的切片模型
      - 输出：切片模型中每张切片被自动均匀性校准后灰度处理后打印










工具：

- 硬件：
  - 1台chairside打印机（工艺组现在项目所用，如需可随时联系）
  - 1台电脑
  - 1只光度计
  - 线缆：光机控制线，HDMI线
- 软件：
  - excel
  - 若电脑控制投图：光机控制软件（注意版本）
- 数据：
  - 方形光斑图（图片验证）
    - 方形为传统光度计的圆圈的内接矩形（尽量保证）
    - 更重要：方形图铺满整个分辨率幅面（分辨率能将方形对应的长边短边整除）







### 打印测试：

目的：在特定极差条件下的自动均匀性校准模块对打印件的影响

圆环件，~~分割代型~~，侧面质量

圆环件：~~手动均匀性校准~~（“光强检测”保存下来的mask存储到打印机中）——打印圆环件合格——删除手动校准的mask——自动均匀性校准——打印圆环件检测

流程：

1. ~~打开chairside上位机，插入光度计，点击“均匀性校准”，调节各点灰度，使幅面光强均匀，再进行“LED校准” 将幅面光强提升至21W~~使用“光强检测”中已经手动校准后拷贝下来的灰度文件，存放到打印机中
2. 在打印机中导入适配chairside机型的圆环件模型
3. 安装成型平台、料盘等，倒入树脂材料HP UV 2.0 Grey，选中模型进行打印
4. 打印完成后，进行标准清洗、后固化，使用2.5次元设备测量
5. 记录数据，并检验是否达到合格要求（要求？）
   - 数据结果呈现参考《自动均匀性校准测试报告20210729-2》对应部分
6. 若未达到合格要求，则重新调试打印机，直至打印圆形件合格要求，合格后进行下一步
7. 删除手动均匀性校准的mask，导入在“光强检测”步骤1中储存的原始灰度文件，使chairside重新回到幅面光强不均匀的状态
   - 可以检测几个点粗略验证一下  ~~是否重新投图圆形光斑，记录光强检测验证是否幅面不均匀状态~~   
8. 插上自动均匀性校准模块，运行自动均匀性校准算法，获得mask应用到chairside上并进行“LED校准”（光强提升到21W）
   - ~~是否重新投图圆形光斑，记录光强验证自动均匀性校准发挥作用使幅面达到一致性~~
9. 再次打印圆环件模型，完成打印后进行标准清洗、后固化，使用2.5次元设备测量
10. 记录数据
    - 数据结果呈现参考《自动均匀性校准测试报告20210729-2》对应部分
11. 重复步骤9和步骤10进行多次打印测量，总计进行3次圆环件打印，并记录数据



V1.1

1. 使用“光强检测”中已经手动校准后拷贝下来的灰度文件，存放到打印机中
2. 在打印机中导入适配chairside机型的圆环件模型
3. 安装成型平台、料盘等，倒入树脂材料HP UV 2.0 Grey，选中模型进行打印
4. 打印完成后，进行标准清洗、后固化，使用2.5次元设备测量
5. 记录数据，并检验是否达到合格要求（**要求——1到1.2个像素**）
   - 数据结果呈现参考《自动均匀性校准测试报告20210729-2》对应部分
6. 若未达到合格要求，则重新调试打印机，直至打印圆形件合格要求，合格后进行下一步
7. 删除手动均匀性校准的mask，导入在“光强检测”步骤1中储存的原始灰度文件，使chairside重新回到幅面光强不均匀的状态
   - 可以检测几个点粗略验证一下
8. 插上自动均匀性校准模块，运行自动均匀性校准算法，获得mask应用到chairside上并进行“LED校准”（光强提升到21W）
9. 再次打印圆环件模型，完成打印后进行标准清洗、后固化，使用2.5次元设备测量
10. 记录数据
    - 数据结果呈现参考《自动均匀性校准测试报告20210729-2》对应部分
11. 重复步骤9和步骤10进行多次打印测量，总计进行3次圆环件打印，并记录数据







能否将圆环件打印放在光强检测中做？

将光强检测中的mask拷出来即可，不用再做手动光强校准



物料：

- ​	硬件
  - 适配chairside的圆环件模型
  - chairside成型平台、料盘
  - 树脂材料HP UV 2.0 Grey





侧面质量：自动均匀性校准之后打印观察，根据经验精度是符合的，意义不大

可做极端测试在侧面光强极差在2W的时候看打印件效果

目的：了解极差光强对侧面质量的影响

**和宇哥沟通侧面质量件模型**

模型：圆柱（表面残渣，或不均匀反光），应用（不太好观察得出来）：基托，较高，一直曝光，可以给残渣出现的机会更多

chairsdie上调节一个区域达到2W极差，在magics中将圆柱放在这个地方，实际打印时可能存在镜像问题，但是是可操作的

幅面内多做一些

最坏的情况可以判断，最好无法判断





分割代型打印不做

分割代型：在要求极高的案例下检测自动均匀性的效果，需要调试设备，测试所需时间待评估 

**能否和应用一起做，和宇哥沟通评估时间**

应用不做分割代型，预估时间2-3天

手动均匀性校准——测试并调整机台diff值——打印分割代型合格——删除手动均匀性校准的mask——自动均匀性校准——打印分割代型检测

- 测试并调整机台diff值是否同《自动均匀性校准测试报告20210729-2》一样，
  - 该步骤的细化



和徐工沟通后，自动均匀性校准的工艺测试报告最晚在18号之前出具

以上测试如需排除偶然性误差，可联系安排例如3台chairside打印机进行如上测试





自动均匀性校准模块如何知道自己校准均匀了（没有反馈）？有一天打印的用例不合格了如何判别是不是自动校准模块的锅？

场内大量测试