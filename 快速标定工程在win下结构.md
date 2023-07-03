快速标定工程在win下结构

![image-20230605152746644](快速标定工程在win下结构.assets/image-20230605152746644.png)

`modules`文件夹下放置各个功能模块，其中`modules.pro`类似于cmake文件，将各个目录组织起来

![image-20230608161752029](快速标定工程在win下结构.assets/image-20230608161752029.png)

sdk文件夹确定了整体通讯框架，invoke，publish函数等的使用

在文件目录中的文件结构

![image-20230608161907402](快速标定工程在win下结构.assets/image-20230608161907402.png)

在Qt的.pro文件中，TEMPLATE指定了项目类型。在这个例子中，TEMPLATE的值是subdirs，表示该.pro文件是一个包含多个子目录的项目。

```
TEMPLATE = subdirs
SUBDIRS += \
    subdir1 \
    subdir2 \
    subdir3

```



其中某个模块的结构

![image-20230608163635382](快速标定工程在win下结构.assets/image-20230608163635382.png)



在文件目录中的文件结构

![image-20230608163721773](快速标定工程在win下结构.assets/image-20230608163721773.png)



```
SOURCES += \
    *.cpp \

HEADERS += \
    *.h \

QT += widgets

include(../global.pri)
include(../../3rd/opencv/opencv.pri)
```

SOURCES变量：包含所有用于构建项目的源代码文件（.cpp文件），通过使用通配符*.cpp，可以将当前目录下的所有.cpp文件添加到SOURCES变量中。

HEADERS变量：包含所有用于构建项目的头文件（.h文件），通过使用通配符*.h，可以将当前目录下的所有.h文件添加到HEADERS变量中。

QT变量：表示该项目需要使用哪些Qt模块。在这个例子中，该项目需要使用Qt Widgets模块。

include指令被用来包含其他文件。在这个例子中，global.pri和opencv.pri文件被包含到该.pro文件中，它们定义了一些全局变量和与OpenCV相关的变量。

反斜杠`\`是换行符，表示下一行是续行，在语法上仍然是同一个变量



被include进来的文件自动列出来了

![image-20230608163839217](快速标定工程在win下结构.assets/image-20230608163839217.png)







已modules中的projector为例



![image-20230629121204610](快速标定工程在win下结构.assets/image-20230629121204610.png)

![image-20230629121248940](快速标定工程在win下结构.assets/image-20230629121248940.png)

从message通道获取消息后，使用调用函数处理消息



`E:\quickCalib\src\sdk\ultrabus\object.cpp`

invoke：同步处理，发送一个消息，必须要有回应



![image-20230629135018477](快速标定工程在win下结构.assets/image-20230629135018477.png)

addinvoketion：处理从topic通道获得的内容，进行处理，然后返回消息

![image-20230629135101497](快速标定工程在win下结构.assets/image-20230629135101497.png)



publish：异步处理，发布一个消息，不需要回应

![image-20230629135324982](快速标定工程在win下结构.assets/image-20230629135324982.png)

addsubscription：处理从topic通道获取的内容，进行处理，发布消息者不需要等待返回

![image-20230629135359702](快速标定工程在win下结构.assets/image-20230629135359702.png)



init函数中只适合去定义建立各种联系

例如：

`ControlNode::Init()`

![image-20230629142643076](快速标定工程在win下结构.assets/image-20230629142643076.png)

run函数中才会执行订阅消息等操作

![image-20230629142659889](快速标定工程在win下结构.assets/image-20230629142659889.png)





invoke同步处理的使用方式：

1. 建立请求（将话题内容通过话题通道传递给处理函数，并等待处理结果）

![image-20230629140104301](快速标定工程在win下结构.assets/image-20230629140104301.png)

```
Invoke(Topics::Calibration, QVariant::fromValue(req))
```

`Topics::Calibration`：话题通道

`QVariant::fromValue(req)`：传递的内容，该内容的类型是QVariant泛型，可以储存任意类型，使用QVariant::fromValue函数将自己定义的类型变成QVariant类型。

注意：该函数的返回类型是`CalibRes`，所以return的返回结果类型也必须是`CalibRes`，

`Invoke(Topics::Calibration, QVariant::fromValue(req)).value<CalibRes>()`中，

`Invoke(Topics::Calibration, QVariant::fromValue(req))`等待的返回结果类型是QVariant泛型，然后使用`.value`变成`CalibRes`类型，`<CalibRes>`也表示该类型为`CalibRes`类型。

2. 建立联系（建立处理函数，谁来处理请求，将话题通道内的话题内容给处理函数处理）

![image-20230629140030277](快速标定工程在win下结构.assets/image-20230629140030277.png)

3. 处理请求（处理函数将话题通道内的话题内容进行处理，处理函数的参数就是话题内容）

![image-20230629135957377](快速标定工程在win下结构.assets/image-20230629135957377.png)

`msg.data.value<CalibParam>()`：

`<CalibParam>`表示`msg.data.value<CalibParam>()`是`CalibParam`类型，

