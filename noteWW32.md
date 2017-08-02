## 2017.7.31 学习Model-view架构

> Model/View is a technology used to separate data from views in widgets that handle data sets. 

Model-View技术用于将部件中的数据从试图中分离出来，便于处理数据。

该技术主要针对的几种数据存储格式：表格、列表和树结构。

---
## 2017.8.1 学习Model-View架构（针对QT自带的例子）

### 2.1 A Read Only Table

- 对于View控件来讲，不需要设定具体的数据内容，只需要指定View的类型

- 对于Model部分，需要定义View的具体参数，如QAbstractTableModel，需要定义表格的行数rowCount()和列数columnCount()，然后填入相应索引下的数据data()

### 2.2 Extending the Read Only Example with Roles

- 在Model部分，通过data()中的role来实现不同的显示方式，嵌入各种格式 enum Qt::ItemDataRole

### 2.3 A Clock inside a Table Cell

- 在不设定任何给View的更新信号的情况下，View对于model提供的数据的更新仅当鼠标在View中进行悬停或单双击操作时

- 通过设定Timer的溢出信号，使View对model的数据进行定期更新，实现Table中的Clock

### 2.4 Setting up Headers for Columns and Rows

- 类似于data()，表格的标签信息（表头）也可以用headerData()进行设定

### 2.5 The Minimal Editing Example

- 最简单的可编辑表格例子，关键函数setData()，对role进行Qt::EditRole的判断，修改相应索引下的Model数据值

> The dataChanged() signal should be emitted if the data was successfully set.

- <font color = red>Qt中的一条说明：</font>setData()完成时应该发射dataChanged()信号，通知View数据改变；然而感觉示例中发射的editCompleted信号并不是dataChanged()信号，**注释掉对于显示结果似乎也没有影响？**

- <font color = yellow>Qt::ItemFlags</font> 示例中重写了flags函数，对每个index的数据都加入了可写属性。关于flags的[官方文档](http://doc.qt.io/qt-5/qabstractitemmodel.html#flags)，可以用于调整单元格的属性。

> If editing one cell modifies more data than the data in that particular cell, the model must emit a `dataChanged()` signal in order for the data that has been changed to be read.

如果更改一个单元格使得其他单元格的数据也被更改，那么model需要发送dataChanged()信号通知更改？？？

在实现过程中涉及到了[信号与槽的参数传递](http://blog.csdn.net/lyc_daniel/article/details/12047819)，关于信号与槽的[一些知识](http://blog.csdn.net/u012964993/article/details/30454923)。

---
## 2017.8.2 学习Model-View 针对Qt自带示例

### 3.1 TreeView

- QTreeView提供了树状数据结构的显示。

- 在Model部分，使用的是QStandardItemModel，通过invisibleRootItem()方法提供树状结构的root结点，在此结点上通过QList数据结构扩展树状结构。

- <font color = red>显示效果：</font>在显示中，第一列按照树状结构进行显示，二、三列按照表格方式对齐显示。

涉及到的方法：（具体内容查Documentation）
- 涉及到的QList类的方法first()：指向QList中的第一个成员。
- 涉及到的QStandardItem的方法appendRow()：添加一行

### 3.2  Working with Selections


### [QSortFilterProxyModel简介及小例](http://blog.csdn.net/u010002704/article/details/41246929)
