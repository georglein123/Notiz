CSP国外已发设备远程整改方法



**国外需远程整改CSP设备：**

![image-20220829095825538](E:\文档\GitHub\Notiz\CSP海外设备整改.assets\image-20220829095825538.png)





**技术支持：**

客户设备——客户电脑

客户电脑——场内电脑

**见刘静分享文档`CSP 远程校准返工用--第三方远程协助（及vpn海外配置）`**





**场内电脑（升级前获取数据）：**

连接客户电脑后，备份客户设备数据；

- 手动均匀性校准数据、PI数据——`energycalibparams.json`，路径`/home/heygears/.heygears/configs`![image-20220822093944643](E:\文档\GitHub\Notiz\CSP海外设备整改.assets\image-20220822093944643.png)
- 自动mask（出厂前做过，保留在路径下）——`mask.png`，路径 `/home/heygears/app/release`![image-20220822112027435](E:\文档\GitHub\Notiz\CSP海外设备整改.assets\image-20220822112027435.png)



**软件运维：**

已知`设备SN码`，在场内电脑操作期间下发软件 `新版`升级软件

- 客户设备：连接Cloud，即可升级



**场内电脑（更改GG参数及替换）：**

1. 客户进行首次自动均匀性校准（此过程同时查看sn是否能成功匹配，若无法匹配成功，修改`autograyclib.json`文件中SN参数后导入设备）（客户进行首次自动均匀性校准的时间由整改同事确定）

   - `autograyclib.json`文件路径 `/home/heygears/.heygears/configs`
   - 修改的SN参数：`"enable_matchSN": true` 设为 `False`

2. 进入指定路径下获取生成的自动mask

   - 自动mask（出厂前做过，保留在路径下）——`mask.png`，路径 `/home/heygears/app/release`![image-20220822112027435](E:\文档\GitHub\Notiz\CSP海外设备整改.assets\image-20220822112027435.png)

   - 日志，路径`/home/heygears/.heygears/logs`

     ![image-20220907101345437](E:\文档\GitHub\Notiz\CSP海外设备整改.assets\image-20220907101345437.png)

3. 在手动 `PI列表`中进行三次拟合，并将 `指定列表中的电流I` 复制进入，求得 `此指定电流列表下的光强P`；

4. 将 `自动mask`和手动 `mask_40`一起放入`pycharm`程序中，获取两者 `中心灰度值`；

5. 将灰度值记录到`手动mask手动PI列表`中，并近似出此时 `自动mask手动PI对应的光强列表`；

6. 使用日志提取IG数据，将 IG数据及相机模组 `母光源数据`复制到 `csp出货整改模板`，分析出合适的`GG参数`；

7. 更改 `hg_autocalib.db`模板文件，将修改好的 `db文件`覆盖原db文件，并使用md5比对确定原db文件已覆盖

   - db文件路径 `/home/heygears/.heygears/db`

   ![image-20220907102431600](E:\文档\GitHub\Notiz\CSP海外设备整改.assets\image-20220907102431600.png)

8. 更新覆盖 `autograyclib.json`文件

   - `autograyclib.json`文件路径 `/home/heygears/.heygears/configs`

   ![image-20220907102710600](E:\文档\GitHub\Notiz\CSP海外设备整改.assets\image-20220907102710600.png)

9. 将海外运维vpn文件放入指定路径

   - 文件路径：`/etc/openvpn/client`

10. 重启（保证还是正常连接），然后查看 `日志` 中`gg`参数确认是否修改成功

   - 日志，路径`/home/heygears/.heygears/logs`
   - 查询关键字 `key_GG_coeffs`

11. 请客户再做进行一次自动均匀性校准

12. 整改完成。



**风险点：**

1. 整改后客户打印机光强无法复核，若之后出现打印问题，如何快速解决；
   - 按照客诉问题流程处理
2. 适配设备的相机模组SN码有不匹配情况发生（通达客退设备有该情况）；
   - 临时更改配置文件，再做模组设备适配







