Qt Creator

Qt中每一个类都有一个与其同名的头文件

快速查看帮助：将鼠标指针放到一个类名或函数上，则出现一个提示框显示其简单介绍，按下F1键就可以在编辑器右边快速打开其帮助文档。



# 第3章 窗口部件

## 3.1 调试输出信息

qDebug

1. 使用qDebug函数，不需要添加头文件`#include<QDebug>`

```c++
qDebug("x: %d",x);
qDebug("y: &d", y);
```

2. 使用输出流

使用输出流的方式一次输出多个值，他们的类型可以不同，该种方法必须添加头文件

```c++
qDebug() << "geometry: " << geometry << "frame: " << frame;
```

还可以使用`Qt::endl`换行

```c++
qDebug()<<"pos:" << widget.pos() << Qt::endl <<"rect: " << widget.rect() << Qt::endl << "size: " << widget.size() << Qt::endl <<
        "width: " << widget.width() << Qt::endl << "height: " << widget.height();
```



## 3.2 对话框QDialog

### 3.2.1 模态和非模态对话框

QDialog类是所有对话框窗口类的基类

模态（modal）、非模态（modeless）按照运行对话框时是否还可以和该程序的其他窗口进行交互；

模态对话框：在没有关闭它之前，不能再与同一个应用程序的其他窗口进行交互，比如新建项目时弹出的对话框；

操作方式：

1. 需要调用它的`exec()`函数；
2. 在其前面使用`setModal()`函数

```
QDialog * dialog = 
```

非模态对话框：既可以与它交互，也可以与同一程序中的其他窗口交互

操作方式：使用`new`操作来创建，然后使用`show()`函数显示

