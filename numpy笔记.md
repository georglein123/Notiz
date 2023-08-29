numpy笔记

根据x，y，组合成网格的每个点的坐标

```
corx, cory = np.meshgrid(np.array(x),np.array(y))
points = np.dstack([corx, cory])
```

例如：

```
import numpy as np
x = [1,3,5]
y = [2,4,6]

corx, cory = np.meshgrid(np.array(x),np.array(y))
points = np.dstack([corx, cory])
```

输出：

corx: x轴所有坐标

[[1 3 5]
 [1 3 5]
 [1 3 5]]

cory:y轴所有坐标

[[2 2 2]
 [4 4 4]
 [6 6 6]]

points:每个点对应的（x，y）

[[[1 2]
  [3 2]
  [5 2]]

 [[1 4]
  [3 4]
  [5 4]]

 [[1 6]
  [3 6]
  [5 6]]]

