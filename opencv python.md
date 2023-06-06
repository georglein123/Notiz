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

此时`（x,y） = (0,0)`

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