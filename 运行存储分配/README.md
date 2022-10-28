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

>   下面会解释这个特点

### 2 活动树



