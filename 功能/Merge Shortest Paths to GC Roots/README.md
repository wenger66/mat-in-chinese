## Merge Shortest Paths to GC Roots

找到从GC Root到当前选择的，或者当前查询对象的最短路径

如下图，根节点是GC Root，每个GC Root都会显示类型，例如System Class、Thread等，一直显示到当前选择节点

![Merge Shortest Paths to GC Roots](./1.png)

不太清楚这个功能的使用场景