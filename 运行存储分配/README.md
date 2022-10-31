# 运行存储分配

## 运行存储分配概述

### 1 运行存储分配策略

<img src="README.assets/image-20221028161116528.png" alt="image-20221028161116528" style="zoom:67%;" />

静态存储分配：

<img src="README.assets/image-20221028161156010.png" alt="image-20221028161156010" style="zoom:67%;" />

动态存储分配：

<img src="README.assets/image-20221028161202291.png" alt="image-20221028161202291" style="zoom:67%;" />

### 2 运行时内存划分

运行时内存的划分：

<img src="README.assets/image-20221028161421859.png" alt="image-20221028161421859" style="zoom:67%;" />

活动记录的概念：

<img src="README.assets/image-20221028161643317.png" alt="image-20221028161643317" style="zoom:60%;" />

活动记录的一般形式：

<img src="README.assets/image-20221028161911839.png" alt="image-20221028161911839" style="zoom:67%;" />

>   临时变量对应于**中间代码生成**时需要的**临时变量**

## 静态存储分配

### 1 过程的静态存储分配

规则：

<img src="README.assets/image-20221028162350798.png" alt="image-20221028162350798" style="zoom:67%;" />

限制：

<img src="README.assets/image-20221028162448470.png" alt="image-20221028162448470" style="zoom:67%;" />

-   如果是递归调用的，无法确定该过程有多少个**活跃的活动记录**，也无法为这些活动记录分配地址空间
-   总得来说，就是**没有运行时的存储分配机制**

### 2 顺序分配法

>   <img src="README.assets/image-20221028162719080.png" alt="image-20221028162719080" style="zoom:67%;" />

<img src="README.assets/image-20221028162942336.png" alt="image-20221028162942336" style="zoom:67%;" />

>   这里其实也不是严格按执行顺序分配，主要理解“静态”和“互不相交”即可；
>
>   可以使用**覆盖**技术减少空间的使用，也就是接下来讲的**层次分配法**

### 3 层次分配法

<img src="README.assets/image-20221028164110018.png" alt="image-20221028164110018" style="zoom:67%;" />

-   没有**递归调用**，这个过程调用图中不会出现**环**
-   可以**从下至上**分配，同层可以互相“覆盖”；上层从子过程的中的最“高”地址开始分配

层次分配算法：



-   过程调用关系矩阵：

    <img src="README.assets/image-20221028164325326.png" alt="image-20221028164325326" style="zoom:67%;" />

    <img src="README.assets/image-20221028164358846.png" alt="image-20221028164358846" style="zoom:67%;" /><img src="README.assets/image-20221028164335599.png" alt="image-20221028164335599" style="zoom:50%;" />

-   内存量矩阵

    <img src="README.assets/image-20221028164343052.png" alt="image-20221028164343052" style="zoom:67%;" />

-   算法流程：

    <img src="README.assets/image-20221028164520185.png" alt="image-20221028164520185" style="zoom:67%;" />

    <img src="README.assets/image-20221028164529062.png" alt="image-20221028164529062" style="zoom:67%;" />

## 栈式存储分配

### 1 概念

<img src="README.assets/image-20221028164710015.png" alt="image-20221028164710015" style="zoom:67%;" />

优点：

<img src="README.assets/image-20221028164900515.png" alt="image-20221028164900515" style="zoom:67%;" />

>   后面讲到非局部变量时会解释这个特点

### 2 活动树

<img src="README.assets/image-20221030143259558.png" alt="image-20221030143259558" style="zoom:67%;" />

举例：快排的活动树

<img src="README.assets/image-20221030143610501.png" alt="image-20221030143610501" style="zoom:67%;" />

> 用首字母代表活动

### 3 控制栈

举例：快排活动出入栈

<img src="README.assets/image-20221030143915914.png" alt="image-20221030143915914" style="zoom:60%;" />

- 当一个过程是递归的时候，常常会有该过程的多个活动记录同时出现在栈中

**活动树和栈**的关系：

<img src="README.assets/image-20221030143955278.png" alt="image-20221030143955278" style="zoom:67%;" />

### 4 设计活动记录的原则

<img src="README.assets/image-20221030144203521.png" alt="image-20221030144203521" style="zoom:67%;" />

## 调用序列与返回序列

### 1 概念

<img src="README.assets/image-20221030144609279.png" alt="image-20221030144609279" style="zoom:67%;" />

### 2 工作流程

<img src="README.assets/image-20221030144951073.png" alt="image-20221030144951073" style="zoom:67%;" />

注意topsp的位置，是在局部数据上，而不是真的栈顶

- 组成部分
- 存参数的
- 存返回地址的
- 存top-sp的
- …

<img src="README.assets/image-20221030145401777.png" alt="image-20221030145401777" style="zoom:67%;" />

- 返回值
- 存topsp的
- 返回地址的
- …

### 3 任务划分

<img src="README.assets/image-20221030145543137.png" alt="image-20221030145543137" style="zoom:67%;" />

调用者：

- 参数
- 控制链
- 保存的机器状态中的PC值（返回地址）
- 更新topsp
- （设置访问链）

被调用者：

- 返回值
- 其他机器状态
- 恢复topsp

### 4 变长数据的存储分配

<img src="README.assets/image-20221030150327840.png" alt="image-20221030150327840" style="zoom:67%;" />

动态数组举例：

<img src="README.assets/image-20221030150648369.png" alt="image-20221030150648369" style="zoom:67%;" />

- 变长数组虽然出现在栈中，但它们并不是活动记录的一部分。

  > **编译时能确定大小的才是活动记录中的部分**，比如那个数组指针。而变长数组是在运行时才分配的

## 非局部数据的访问

### 1 概念

<img src="README.assets/image-20221030161335641.png" alt="image-20221030161335641" style="zoom:67%;" />

过程嵌套举例：

<img src="README.assets/image-20221030161559720.png" alt="image-20221030161559720" style="zoom:67%;" />

不支持过程嵌套举例：

<img src="README.assets/image-20221030161625981.png" alt="image-20221030161625981" style="zoom:67%;" />

### 2 非局部数据的访问

不支持过程嵌套的：

<img src="README.assets/image-20221030161700420.png" alt="image-20221030161700420" style="zoom:67%;" />

#### 2.1 嵌套深度

支持过程嵌套的：

嵌套深度定义：

<img src="README.assets/image-20221030161813395.png" alt="image-20221030161813395" style="zoom:67%;" />

<img src="README.assets/image-20221030161846419.png" alt="image-20221030161846419" style="zoom:67%;" />

#### 2.2 访问链

<img src="README.assets/image-20221030162039458.png" alt="image-20221030162039458" style="zoom:67%;" />

访问链使用举例：沿着访问链访问外围数据

<img src="README.assets/image-20221030162305029.png" alt="image-20221030162305029" style="zoom:67%;" />

<img src="README.assets/image-20221030162339483.png" alt="image-20221030162339483" style="zoom:67%;" />

### 3 访问链的建立

<img src="README.assets/image-20221030163231739.png" alt="image-20221030163231739" style="zoom:67%;" />

> 注意，外层调用内层不能直接调内层的内层，因为看不到，只能调在自己内部定义的一级内层

- 外调内，复制外到内

<img src="README.assets/image-20221030163419369.png" alt="image-20221030163419369" style="zoom:67%;" />

- 同级调，访问相同直接复制

<img src="README.assets/image-20221030163805622.png" alt="image-20221030163805622" style="zoom:67%;" />

> 内调外是可以跨好多级的

- 内调外，访问最近公共祖先（不包括二者本身）

## 堆式存储分配

### 1 概念

<img src="README.assets/image-20221030183319388.png" alt="image-20221030183319388" style="zoom:67%;" />

<img src="README.assets/image-20221030183408175.png" alt="image-20221030183408175" style="zoom:67%;" />

### 2 分配与释放策略

<img src="README.assets/image-20221030183443555.png" alt="image-20221030183443555" style="zoom:67%;" />

<img src="README.assets/image-20221030183544893.png" alt="image-20221030183544893" style="zoom:67%;" />

<img src="README.assets/image-20221030183556982.png" alt="image-20221030183556982" style="zoom:67%;" />

### 3 堆式管理的条件

<img src="README.assets/image-20221030183621623.png" alt="image-20221030183621623" style="zoom:67%;" />

## 符号表

### 1 概述

<img src="README.assets/image-20221030183906565.png" alt="image-20221030183906565" style="zoom:67%;" />

- 记录标识符和标识符的属性信息

### 2 数据结构

<img src="README.assets/image-20221030184132535.png" alt="image-20221030184132535" style="zoom:67%;" />

### 3 访问与访问链

<img src="README.assets/image-20221030184519922.png" alt="image-20221030184519922" style="zoom:67%;" />

构造访问链的时候也需要用到符号表信息，创建新的活动记录时，先在调用者的符号表中找，如果在自己的符号表中找到了，就直接把新的活动记录的访问链设置为调用者，如果在自己的符号表找不到，则沿着访问链到新的符号表，直到某个符号表中有这个过程名，则把新活动记录的访问链设置为这个符号表对应的活动记录

<img src="README.assets/image-20221030184703867.png" alt="image-20221030184703867" style="zoom:67%;" />

### 4 符号表对标识符的处理

<img src="README.assets/image-20221030190104858.png" alt="image-20221030190104858" style="zoom:67%;" />

### 5 嵌套过程声明语句的SDT/符号表的建立

<img src="README.assets/image-20221030190251106.png" alt="image-20221030190251106" style="zoom:67%;" />

<img src="README.assets/image-20221030191115235.png" alt="image-20221030191115235" style="zoom:67%;" />

举例：

先写出了这个程序的概括版

<img src="README.assets/image-20221030191454722.png" alt="image-20221030191454722" style="zoom:67%;" />

举例：

（这段我没看，之后有空再说吧）

