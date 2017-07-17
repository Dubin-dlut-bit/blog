## 2017.7.12 初步研究Procise工程的代码

关于QT相关书籍的推荐：

- [网址1](http://bbs.csdn.net/topics/391893955)
- [网址2](http://blog.csdn.net/waangyan/article/details/53173204)

关于Msvcr120.dll的问题：
[What is the Msvcr120.dll](https://www.quora.com/What-is-the-Msvcr120-dll-and-how-to-fix-it)

对于QT事件、信号的问题：

- [QT事件机制概览](http://blog.csdn.net/unclerunning/article/details/70226794#消息循环)
- [QT中信号与事件的小结](http://blog.csdn.net/andy_93/article/details/52670839)
- [Qt Main-Gui and other thread + events loops](https://stackoverflow.com/questions/16812602/qt-main-gui-and-other-thread-events-loops)

- [QT事件机制简析](http://qimo601.iteye.com/blog/1407911)

基础概念：

- [关于同步和异步](http://www.cnblogs.com/pinksnow520/p/3966462.html)，知乎上也有不错的[回答](https://www.zhihu.com/question/19732473)

> 小结：对于QT在GUI中的线程分配原理不甚了解，导致在研究代码时没有条理，没有找准主线程。需要对于**QT的事件处理机制、线程使用机制和Window的相关知识**的了解和掌握。

---
## 2017.7.13 初步研究Procise工程的代码

在Procise工程启动时，首先调用QSplashScreen类显示启动画面（图标与版本），然后调用自定义的MainWindow类显示主窗口。

在整个Procise工程中，比较重要的几个自定义类：
- `MainWindow : QMainWindow`
- `MainApp : QApplication`
- Project
- Gui
- ...

首先展开对于基础QT类的研究：
- QMainWindow
- QApplication

### QApplication类

一篇给新手介绍QApplication类的[博客](http://mobile.51cto.com/symbian-269525.htm)

[Qt 类简介之 Qt QApplication 类](http://blog.csdn.net/syp35/article/details/51383594)

官方网站介绍[Detailed Description](http://doc.qt.io/qt-5/qapplication.html#details)

> The QApplication class manages the GUI application's control flow and main settings.

QApplication类的主要作用是管理GUI应用的控制流程和主要设置。

QApplication specializes QGuiApplication with some functionality needed for QWidget-based applications. It handles widget specific initialization, finalization.

For any GUI application using Qt, there is precisely one QApplication object, no matter whether the application has 0, 1, 2 or more windows at any given time. For non-QWidget based Qt applications, use QGuiApplication instead, as it does not depend on the QtWidgets library.

Some GUI applications provide a special batch mode ie. provide command line arguments for executing tasks without manual intervention. In such non-GUI mode, it is often sufficient to instantiate a plain QCoreApplication to avoid unnecessarily initializing resources needed for a graphical user interface. The following example shows how to dynamically create an appropriate type of application instance:

---

对于Procise工程的整体流程，包括线程的分配、各个线程所实现的功能，需要有一定的分析和了解。

### 一些关于线程基础知识

[pthread_create()函数的使用](http://www.cnblogs.com/wainiwann/p/3550748.html)

---

涉及到了一种后端开发的脚本语言Tcl:

- 相应的基础教程[下载](http://bbs.eetop.cn/thread-394656-1-1.html)

- Tcl脚本语言的[学习笔记博客](http://blog.sina.com.cn/s/blog_6840802c0100k1ny.html)

- Procise工程中看到的`Tcl_Main()`函数的[官方介绍](http://tmml.sourceforge.net/doc/tcl/Tcl_Main.html)，主要是为相应的Shell应用开发提供了方便：

``` cpp
Tcl_Main(argc, argv, appInitProc)
// 其中appInitProc是一个类似于函数指针的变量，为相应应用的初始化提供了方便，能够实现类似于对初始化程序（函数）的调用
// Procise工程中调用的初始化函数为TclInitProcForQT（需要GUI时）
```

---
## 2017.7.14 继续研究Procise工程代码

一个不错的[QT入门博客系列](http://blog.51cto.com/zt/20)
