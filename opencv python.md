opencv python

remap函数：`dst(x,y) =  src(map_y(x,y), map_x(x,y))`

例如：

```python
#mapx
# [[ 5.  6.]
#  [ 7. 10.]]
```

```python
#map_y
# [[0. 1.]
#  [2. 3.]]
```

```python
#src
#array([[230,  45, 153, 233, 172, 153,  46,  29],
#       [172, 209, 186,  30, 197,  30, 251, 200],
#       [175, 253, 207,  71, 252,  60, 155, 124],
#       [114, 154, 121, 153, 159, 224, 146,  61],
#       [  6, 251, 253, 123, 200, 230,  36,  85],
#       [ 10, 215,  38,   5, 119,  87,   8, 249],
#       [  2,   2, 242, 119, 114,  98, 182, 219],
#       [168,  91, 224,  73, 159,  55, 254, 214]], dtype=uint8)
```

例如假设此时待求dst位置`（x,y） = (0,0)`的值

`map_x(x,y) = map_x(0,0) = 5`；

`map_y(x,y) = map_y(0,0) = 0`

`dst(0,0) = src(map_y(x,y), map_x(x,y)) = src(0,5) = 153`

因为`map_y(x,y), map_x(x,y)`都是整数，所以不需要插值，如果`map_y(x,y), map_x(x,y)`超过了`src`的维度，则赋值为0。





```python
import numpy as np
import cv2
img = np.uint8(np.random.rand(8, 8)*255)
#array([[230,  45, 153, 233, 172, 153,  46,  29],
#       [172, 209, 186,  30, 197,  30, 251, 200],
#       [175, 253, 207,  71, 252,  60, 155, 124],
#       [114, 154, 121, 153, 159, 224, 146,  61],
#       [  6, 251, 253, 123, 200, 230,  36,  85],
#       [ 10, 215,  38,   5, 119,  87,   8, 249],
#       [  2,   2, 242, 119, 114,  98, 182, 219],
#       [168,  91, 224,  73, 159,  55, 254, 214]], dtype=uint8)

map_y = np.array([[0, 1], [2, 3]], dtype=np.float32)
#map_y
# [[0. 1.]
#  [2. 3.]]

map_x = np.array([[5, 6], [7, 10]], dtype=np.float32)
#mapx
# [[ 5.  6.]
#  [ 7. 10.]]

mapped_img = cv2.remap(img, map_x, map_y, cv2.INTER_LINEAR)
#array([[153, 251],
#       [124,   0]], dtype=uint8)

# dst(x,y) =  src(map_x(x,y),map_y(x,y))
```

 

No interpolation is happening here since my map coordinates are exact integers. Also I included an out-of-bounds index (`map_x[1, 1] = 10`, which is larger than the image width), and notice that it just gets assigned the value `0` when it's out-of-bounds.



`cv.addWeighted`

 OpenCV 库的 `cv.addWeighted` 函数，对两个输入图像进行加权求和，并输出叠加后的结果。

具体来说，该函数以如下形式调用：

```
dst = cv.addWeighted(src1, alpha, src2, beta, gamma)
```

其中，`src1` 和 `src2` 是两个要融合的输入图像。这里分别为 `calib_img` 和 `mesh_roi`。

`alpha` 是第一个输入图像 `src1` 的权重系数，用于调整其在融合结果中的贡献。如果想要 `src1` 图像完全显示（即只显示 `src1` 图像，不透明度为 1），则设置 `alpha=1`。

`beta` 是第二个输入图像 `src2` 的权重系数，用于调整其在融合结果中的贡献。如果想要 `src2` 图像完全显示，设置 `beta=1`。

`gamma` 是添加到每个加权和的可选标量值。通常情况下将其设置为 0 即可。可以使用该参数来调整亮度或比例关系。

因此，在给定代码中，调用了 `cv.addWeighted` 将 `calib_img` 和 `mesh_roi` 进行加权叠加融合，根据公式：

```
dst = alpha * calib_img + beta * mesh_roi + gamma
```

这里 `alpha=1`, `beta=1`, `gamma=1`。即融合结果为两幅图像相等权重的加和，如果两幅图像中有重叠部分，则会透明度混合。

最终得到融合后的图像，并赋值给变量 `dst`。