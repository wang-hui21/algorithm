# 队列
### 基本介绍
队列：是一个**有序列表**，可以用**数组**或**链表**实现。
特点：遵循**先入先出**原则。既：先存入的数据先取出。

示意图：
![img.png](../../../img/img.png)
中图：存入数据

右图：取出数据，从队首取
## 数组模拟队列
队列本身是**有序列表**，使用数组结构来存储队列的数据，则如前面基本介绍中的示意图一样。

声明 4 个变量：

* arr：用来存储数据的数组
* maxSize：该队列的最大容量
* front：队首下标，随着数据输出而改变
* rear：队尾下标，随着数据输入而改变

队列中常用操作分析，以 add，把数据存入队列为例，思路分析：

1. 将尾指针往后移：rear + 1，前提是当 front == rear 时，队列是空的
2. 若尾指针 rear < maxSize -1：
* 则将数据存入 rear 所指的数组元素中，
* 否则无法存入数据。rear = maxSize -1 表示队列满了

以上思路是一个最基本的实现（不是完美的，看完代码就明白了）。代码实现如下：

[代码](queue.java)

以上代码中实现了一个**一次性队列（不能复用）**，因为当队列满了之后，再添加就加不进去了，获取数据也不能清空原队列中的数据。

优化方向：将这个数组改进位一个环形队列

### 思路分析
front：含义调整

表示：队列的第一个元素，也就是说 arr[front] 就是队列的第一个元素

初始值：0

rear：含义调整

表示：队列的最后一个元素的下一个位置

初始值：0

这个很重要，是一个小算法，能更方便的实现我们的环形队列。

队列 满 计算公式：(rear + 1) % maxSize == front

队列 空 计算公式：rear == front

队列中 有效元素个数 计算公式：(rear + maxSize - front) % maxSize

为了能更清晰这个算法，下面画图来演示队列中元素个数，关键变量的值
![img.png](../../../img/queue.png)

该算法取巧的地方在于 rear 的位置，注意看上图，rear 所在的位置 永远是空的，实现环形队列的算法也有多种，这里空出来一个位置，是这里算法的核心。

[代码](reQueue.java)