
* [安装DTFJ插件](./Installing%20IBM%20DTFJ%20feature/README.md)

* [直方图(Histrogram)](./Histrogram/README.md)

* [支配树(Dominator Tree)](./Dominator%20Tree/README.md)

* [线程分析(Analyzing Threads)](./Analyzing%20Threads/README.md)

* [类加载器分析(Analyze Class Loader)](./Analyze%20Class%20Loader/README.md)

* [对象可达路径(Path to GC Roots)](./Path%20to%20GC%20Roots/README.md)

* [对象可达最短路径(Merge Shortest Paths to GC Roots)/](./Merge%20Shortest%20Paths%20to%20GC%20Roots/README.md)

* [提取列表对象值(Extract List Values)](./Extract%20List%20Values/README.md)

* [不可达对象(Unreachable)](./Unreachable/README.md)


**所有功能其实就是配置不同的SQL查询语句**

**MAT中大部分功能都是围绕着路径，有的是从支配的角度，有的是从引用的角度

MAT中最常见的对象/类表格的Class Name列包含了大量的信息，这里介绍下，以下图为例

![Class Name](./1.png)

* cache: 变量名称，这个变量是一个CopyOnWriteArrayList的对象，参考代码段1
* array: 变量名称，CopyOnWriteArrayList的对象中的一个属性是array，这个变量是一个Object数组，参考代码段2
* \[0\]: 数组Index，这个对象是Object数组的第0个元素
* org.qimi.lab.cow.Element @ 0xc0021b40: 对象类和对象地址

对应如下的代码


        // 测试对象缓存列表
        private static List<Element> cache = new CopyOnWriteArrayList<Element>();
        
        /** The array, accessed only via getArray/setArray. */
        private transient volatile Object[] array;



