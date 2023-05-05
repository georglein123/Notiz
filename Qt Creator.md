Qt Creator

Qt中每一个类都有一个与其同名的头文件

快速查看帮助：将鼠标指针放到一个类名或函数上，则出现一个提示框显示其简单介绍，按下F1键就可以在编辑器右边快速打开其帮助文档。



### 2.3.1 使用全自动ui界面



![image-20230504202209955](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20230504202209955.png)



![image-20230504202431201](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20230504202431201.png)



![image-20230504202342147](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20230504202342147.png)



![image-20230504202026005](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20230504202026005.png)



完成后文件形式：

![img_v2_429d8fb1-4d25-4f1d-8e8d-38bf6efd767g](C:\Users\Administrator\AppData\Roaming\LarkShell-ka-samhzo3j\sdk_storage\5287ca566b5f1745722e44551afcb588\resources\images\img_v2_429d8fb1-4d25-4f1d-8e8d-38bf6efd767g.jpg)

工程名称是创建工程时设定的名称

头文件和源文件的名称是创建工程时设定的类名

![image-20230504202740357](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20230504202740357.png)















### 2.3.2 使用半自动ui界面

新建空项目

![image-20230504162213534](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20230504162213534.png)



在空项目中添加cpp文件

![image-20230504162900361](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20230504162900361.png)



在空项目中添加ui文件

![image-20230504163004451](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20230504163004451.png)

![image-20230504163050348](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20230504163050348.png)

![image-20230504163122562](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20230504163122562.png)

![image-20230504163149097](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20230504163149097.png)

添加ui文件后并进行界面设计，然后点击左下角锤子图标进行build，会在当前项目文件夹下生成debug文件夹，该文件夹内含有该ui的头文件

之后在main文件中添加该头文件即可，例如：`#include "ui_dialog.h"`

### 2.3.3 不使用ui界面

1. 新建一个空工程
2. 加入类

![image-20230504173031622](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20230504173031622.png)

![image-20230504173237875](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20230504173237875.png)

生成的头文件

![image-20230504174010470](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20230504174010470.png)

生成的源文件

![image-20230504174207771](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20230504174207771.png)

3. 加入main文件

![image-20230504174709774](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20230504174709774.png)

3. 





# 第3章 窗口部件

## 3.1 基础窗口部件QWidget

### 3.1.1 窗口、子部件以及窗口类型

```c++
#include<QtWidgets>

int  main(int argc, char *argv[])
{
    QApplication a(argc, argv);
    
    //新建QWidget类对象，默认parent参赛为0,所以是个窗口
    QWidget *widget = new QWidget();
    
    //设置窗口标题
    widget->setWindowTitle(QObject::tr("i am widget"));
    
    //新建QLabel对象，默认parent参数为0,所以是个窗口
    QLabel *label = new QLabel();

    label->setWindowTitle(QObject::tr("i am label"));
    
    //设置要显示的信息
    label->setText(QObject::tr("label: i am window"));
    
    //label2指定了父窗口为widget，所以不是窗口
    QLabel * label2 = new QLabel(widget);
    
    label2->setText(QObject::tr("label2: i am sub widget of widget"));
    
    //改变部件大小
    label2->resize(250,20);
    
    //在屏幕上显示出来
    label->show();

    widget->show();

    int ret = a.exec();
    
    //释放空间
    delete label;
    delete widget;
    return ret;

}

```

窗口部件（widget）简称部件

Qt中把没有嵌入到其他部件中的部件称为窗口，一般窗口都有边框和标题栏

QMainWindow和大量的QDialog子类是最一般的窗口类型

窗口就是没有父部件的部件，所以又称为顶级部件，与其相对的是非窗口部件，又称子部件，在Qt中大部分部件被用作子部件，嵌入在别的窗口中。





## 调试输出信息

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



### 3.2.2 多窗口切换

使用全自动ui界面创建完成工程后

进入design页面，拖入指定的部件，然后右击，选择go to slot

![image-20230504203414077](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20230504203414077.png)



![image-20230504203537146](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20230504203537146.png)

点击OK后

自动在类的头文件中添加槽函数声明

![image-20230504203800920](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20230504203800920.png)

以及在类的源文件中自动添加功能函数

![image-20230504203859730](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20230504203859730.png)



```c++
// 由字符on_发射信号的部件对象名_信号名组成
void MyWidget::on_showChildButton_clicked()
{
    QDialog * dialog = new QDialog(this);
    QLabel *label = new QLabel(dialog);
    label->setText("hello world");
    dialog->show();
}
```



### 3.2.3 标准对话框

#### **颜色对话框**

```c++
void helloDialog::on_pushButton_3_clicked()
{
    //获取指定颜色对话框部件
    //getColor(设置初始颜色、指定父窗口和设置对话框标题)
    QColor color = QColorDialog::getColor(Qt::red, this, tr("color dialog"));
    qDebug() << "color: " << color;
}
```



#### **文件对话框**

```c++
void helloDialog::on_pushButton_4_clicked()
{
    //选择文件或文件夹对话框
    //getOpenFileName(指定父窗口、设置对话框标题、指定默认打开的目录路经、设置文件类型过滤器)
    QString fileName = QFileDialog::getOpenFileName(this, tr("file dialog"), "D: ", tr("images(* png * jpg)"));
    qDebug() << "fileName: " << fileName;
}

```

