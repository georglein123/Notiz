

日志信息输出需求

- 当前图片层数
- 图片中实体数量
- 实体截面占比（`Section10`不用输出，其他类型需输出）
- 截面类型
- M值（`SectionLittle`还要输出待加权计算的另外两个M值）

如：

- 图片类型为`Section type: Section10`待输出的信息：

```c++
layer: 100; item amount: 8; section type: Section10; M value : 100;
```

- 图片类型为`Section type: SectionMedium`待输出的信息：

```c++
layer: 100; item amount: 15; area percent: 50%; section type: SectionMedium; M value : 100;
```

- 图片类型为`Section type: SectionLittle`待输出的信息：（该类型将待加权计算的两种M值分别输出）

```c++
layer: 100; item amount: 30; area percent: 30%; section type : SectionLittle; M value: 160, including Msum : 160, Mtotal : 160;
```

