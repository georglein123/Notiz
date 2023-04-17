CS和CSP日志中自动均匀性校准的关键字查看

CS——日志中关键字查看：

1. 设备端：

   1. 自动均匀性校准：

      - 离散数据：电流I（手动校准中的电流列表中的电流）、灰度avgGrey、newGrey、 LookUpPower
        - 日志关键字`CollectPI`
      - 拟合结果：LookUpPower和电流I
        - 日志关键字`多项式系数:  QVector`

   2. 自动mask手动PI：

      - 离散数据：设备端电流I，光强P

        `OnFitGG P-I`

      - 离散数据：设备端光强，设备端灰度、母光源光强，母光源灰度

        - `manPower_avgGray`
  - `4[k|K]Power_avgGray`
    
- 拟合结果：设备端电流I、光强P
      
  `PG_coeff =  QVector`
      
  `PG4K_coeff =  QVector`
  
- G-G的拟合结果
      
        - 拟合结果
  
  - `GG_coeffs std::vector`

**母光源的GP函数无法在cs的日志中查看**



1. 4K母光源：

   - **离散数据：电流I，光强P，灰度G**

   查看方式：4K母光源的控制机台`/home/heygears/app/release`的该路径下新建`tmp`文件夹，模组跑的图片就会存入其中，图片命名方式即为`电流I-光强P-灰度G`

   

   4K母光源上日志查看路径

   `/home/heygears/.heygears/logs/220726`

   `2022-07-26 13:19:44.721 [DEBUG] WriterEEPROM QJsonObject({"100_1500":[-6.454869890148984e-06,0.004198838025331497,-0.5713498592376709,32.304725646972656]`

   

   CSP设备——

   设备端：

   1. 自动均匀性校准：

      - 离散数据：电流I（此处电流I的值和 `自动mask手动PI` 中的电流值相同）、灰度avgGrey、newGrey、 LookUpPower
        - 日志关键字`CollectPI`
      - 拟合结果：LookUpPower和电流I
        - 日志关键字``InsertCoeffs Success to Insercoeffs: QVector``

   2. 自动mask手动PI：

      - 离散数据：设备端电流I，光强P

        `CreatePI 995 P-I`

      - 离散数据：设备端光强P，灰度G，母光源光强P，灰度G

        - `CreatePI 995 P-I`
        - `CreatePI 998 P-I`（CreatePI 998 P-I= 14.08 100）
   
      - 拟合结果：设备端电流I、光强P
   
        `PG_coeff =  QVector`
   
        `PG4K_coeff =  QVector`
   
      - 离散数据：光强列表下设备端灰度、母光源灰度
   
        - `manPower_avgGray`
        - `4[k|K]Power_avgGray`
   
      - G-G的拟合结果
   
        - 拟合结果
        - `GG_coeffs std::vector`
   
   3. 4K母光源的GP拟合函数可以在日志中查看
   
   2022-08-05 16:20:05.022 [DEBUG] CvtGrayToPower 792 `fn_coeffs`= (QVariant(double, -6.89945e-06), QVariant(double, 0.00441767), QVariant(double, -0.604259), QVariant(double, 33.9182))



重启后日志中会读取gg参数：`Run 138 key_GG_coeffs`

cs :  `gg_coeffs_list`——重启后无法看到，必须做一次自动均匀性校准才能看到

