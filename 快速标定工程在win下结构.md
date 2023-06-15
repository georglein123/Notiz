快速标定工程在win下结构

![image-20230605152746644](快速标定工程在win下结构.assets/image-20230605152746644.png)

`modules`文件夹下放置各个功能模块，其中`modules.pro`类似于cmake文件，将各个目录组织起来

![image-20230608161752029](快速标定工程在win下结构.assets/image-20230608161752029.png)

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

