## 1. 通过打印日志的方式调试release版本的代码

这里调用的是std标准库中的方法：

```cpp
std::ofstream logfiles;
// 分别表示输出模式和在末尾添加模式
logfiles.open("log.txt", std::ofstream::out | std::ofstream::app)
logfiles << "Text and Variables" << std::endl;
logfiles.close();
```

这样能做到对于`log.txt`日志文件的末尾写入，方便调试。

其他方案，如[通过`printf`的方式](http://blog.csdn.net/a651588/article/details/51790821)。

## 2. 关于程序在debug下运行正常，在release下运行出问题

很大可能是因为有**没有初始化的变量**。对于debug模式下未初始化的变量系统会自动赋初值，但是release模式下并不会。其他情况可以参见参考资料。

### 参考资料：

- empty now.

关于[如何在release模式下启动debug中可以使用的相关功能](https://msdn.microsoft.com/en-us/library/fsk896zz.aspx)，然而我照着设置了一下，仍然无法在release模式下进行单步调试，也无法在断点的位置进行停顿。

## 3. 