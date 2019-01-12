# 基本概念

## 堆转储

堆转储是Java进程在某个特定时间的内存快照。根据包含的信息不同，有很多种格式，但是基本上都会包括Java对象、Java类的信息。
正常情况下，在堆转储之前会触发一次Full GC。

Memory Analyzer工具内能使用HPROF二进制堆转储文件，OpenJ9的系统转储文件，OpenJ9的PHD堆转储文件。

堆转储信息中通常包括：

* 所有对象，包括对象的类、属性、值、引用
* 所有类，包括类的类加载器、名称、父类、静态属性
* GCRoots，虚拟机可达的对象
* 线程堆栈和本地变量，快照时的线程调用栈，每个栈帧本地对象的信息

堆转储并不包含所有信息，例如对象的创建者和创建位置。

## Shallow heap vs Retained heap

Shallow heap 和 Retained heap 的含义都是指的实例，而不是类

浅堆(Shallow heap)：指一个对象本身占用的内存，包括每个引用占用32位或者64位（根据操作系统架构的不同）的内存，每个整型占用4个字节的内存，
每个长整型占用8个字节的内存等等

保留集合(Retained set):当对象X被回收时，所有可以被回收的对象，一起组成了X的Retained set

保留堆(Retained heap):对象X的保留集合中的所有对象的本身大小总和，就是X的保留堆大小。也可以这样理解：为对象X保留的堆空间

简而言之，一个对象的浅堆指的是本身占用的堆内存空间，一个对象的保留堆指的是当这个对象被回收后，所有可以连带被回收对象总共占用的堆内存空间

领头集合的保留集合（The retained set for a leading set ）：领头集合的所有对象都被回收时，保留集合的所有对象将被释放。

这个概念主要用来针对被多个引用的对象。如下图，只有G被回收，H由于仍被F引用，并不属于G的保留集合;
同理，只有F被回收，H由于仍被G引用，也不属于F的保留集合。所以只有G、F都被回收，H才可以被回收，所以G、F就称为
领头集合，这个领头集合的保留集合就包含了H

![Example object graph](./1.png)

最小保留堆大小(The Minimum Retained Size): 是一种对于保留堆大小的估计值，这种算法比精确求出保留堆大小快很多，它只依赖检查集合？中对象的数量，
并不考虑堆转储中对象的数量。

## [Dominator Tree](https://help.eclipse.org/2018-12/index.jsp?topic=/org.eclipse.mat.ui.help/welcome.html)

## [Garbage Collection Roots](https://help.eclipse.org/2018-12/index.jsp?topic=/org.eclipse.mat.ui.help/welcome.html)