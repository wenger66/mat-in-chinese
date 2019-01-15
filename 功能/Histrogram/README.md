## 直方图(Histrogram)

MAT的直方图(Histogram)是从类的角度看内存占用情况，支配树(Dominator Tree)是从对象的角度看内存占用情况

直方图的主要作用是查看实例的个数，尤其是自己创建的类的实例个数

如下图，输入com.zte.ums.em.rm.*
![Histrogram](./1.png)

解释下每个字段
* Class Name:类名
* Objects:实例个数，准确值
* Shallow Heap:浅堆占用内存，[这里](../../概念/README.md)有详细介绍，准确值
* Retained Heap:初始为最小保留堆占用内存，保留堆占用内存大于等于该值。可以使用右键功能Calculate Precise Retained Size计算精确值
[这里](../../概念/README.md)有详细介绍

可以按任意列排序，常用排序是Objects和Retained Heap列





