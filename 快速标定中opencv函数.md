快速标定中opencv函数

```
import cv2 as cv
import numpy as np

# 加载图像
img = cv.imread('image.jpg')

# 将其转换为灰度
gray = cv.cvtColor(img, cv.COLOR_BGR2GRAY)

# 计算直方图
hist = cv.calcHist([gray], [0], None, [256], [0,256])

```

- 第一个参数是要计算直方图的图像列表。在这种情况下，我们只计算一个图像的直方图，所以我们将它作为一个元素的列表传递。
- 第二个参数是要计算直方图的通道列表。如果图像是灰度的，只有一个通道（0），但如果图像是彩色的，可能有三个通道（0，1，2分别代表B，G，R）。
- 第三个参数是掩码。如果提供了掩码，直方图将只计算掩码像素。`None`表示没有掩码。
- 第四个参数是直方图大小或者说是区间数。在这种情况下，是[256]，这意味着每个通道我们将有256个区间。
- 第五个参数是像素值的范围，通常对于8位图像来说是[0,256]。

这将返回一个256x1的numpy数组（直方图），其中每个值对应于该值的像素在图像中出现的次数。



但如果你想从不同的数字开始计数，你可以向`enumerate`提供一个可选的第二个参数。例如，`enumerate(list1, 1)`将从1开始计数。



三次样条插值

[样条插值(Spline Interpolation)-云社区-华为云 (huaweicloud.com)](https://bbs.huaweicloud.com/blogs/264151)