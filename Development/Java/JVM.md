# JVM相关

# 读《深入理解JAVA虚拟机－JVM高级特性与最佳实践》

## 第二章 自动内存管理机制

问题：
1. 运行时数据区域分为哪些部分，每部分都包含哪些数据，为什么要这么分？
2. 什么情况下会引起内存溢出？如何避免？

1. 对于第一个问题，运行时数据区域可以分为两部分，一个是常量部分，一个是变量部分，常量部分分为方法区，主要存储类的加载信息、常量和静态变量，我们常听的常量池就是在方法区中的一部分；变量部分分为栈区、堆区和程序计数器，栈区又分为虚拟机栈和本地方法栈

