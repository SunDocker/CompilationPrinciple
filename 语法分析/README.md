# 语法分析

## 自顶向下分析

### 1 概述

<img src="README.assets/image-20220908141623679.png" alt="image-20220908141623679" style="zoom:80%;" />

<img src="README.assets/image-20220908141631147.png" alt="image-20220908141631147" style="zoom:80%;" />

- 怎么选择？下面就会讲几种选择方式

> 举例：
>
> <img src="README.assets/image-20220908141643671.png" alt="image-20220908141643671" style="zoom:77%;" />

#### 1.1 最左推导与最右推导

<img src="README.assets/image-20220908141944994.png" alt="image-20220908141944994" style="zoom:70%;" />

<img src="README.assets/image-20220908142021905.png" alt="image-20220908142021905" style="zoom:67%;" />

![image-20220908142052894](README.assets/image-20220908142052894.png)

<img src="README.assets/image-20220908142157346.png" alt="image-20220908142157346" style="zoom:80%;" />

> 最左推导和最右推导具有唯一性

> 举例：
>
> <img src="README.assets/image-20220908142821779.png" alt="image-20220908142821779" style="zoom:67%;" />
>
> 按照上述规则分析，可以成功分析且分析结束后叶节点自左向右刚好构造输入串

#### 1.2 计算机实现自顶向下分析

<img src="README.assets/image-20220908143315191.png" alt="image-20220908143315191" style="zoom:67%;" />

需要回溯的分析器称为不确定的分析器，如果能预测出正确的产生式就是预测分析

#### 1.3 预测分析简介

<img src="README.assets/image-20220908143430427.png" alt="image-20220908143430427" style="zoom:67%;" />

### 2 文法转换

> 并不是所有文法都直接适用于自顶向下的分析，文法转换就是要改造这些文法以使其适合自顶向下的分析

#### 2.1 回溯问题与左递归

<img src="README.assets/image-20220908143734599.png" alt="image-20220908143734599" style="zoom:67%;" />

<img src="README.assets/image-20220908144123829.png" alt="image-20220908144123829" style="zoom:67%;" />

#### 2.2 消除直接左递归

<img src="README.assets/image-20220908144315447.png" alt="image-20220908144315447" style="zoom:77%;" />

> 举例：
>
> <img src="README.assets/image-20220908144505197.png" alt="image-20220908144505197" style="zoom:80%;" />

<img src="README.assets/image-20220908144707787.png" alt="image-20220908144707787" style="zoom:67%;" />

- 根据是否会导致左递归，把产生式分为两类，对这两类分别进行处理即可

> <img src="README.assets/image-20220908144716005.png" alt="image-20220908144716005" style="zoom:67%;" />

#### 2.3 消除间接左递归

<img src="README.assets/image-20220908144829450.png" alt="image-20220908144829450" style="zoom:67%;" />

- 只是多了一个代入的步骤

#### 2.4 消除左递归算法

<img src="README.assets/image-20220908145050277.png" alt="image-20220908145050277" style="zoom:67%;" />

> 循环推导就是A推着推着又回到A了

#### 2.5 提取左公因子

<img src="README.assets/image-20220908145240981.png" alt="image-20220908145240981" style="zoom:67%;" />

> 本质是在**推迟决定**

#### 2.6 提取左公因子算法

<img src="README.assets/image-20220908145302788.png" alt="image-20220908145302788" style="zoom:67%;" />

## 预测分析

### 1 LL(1)文法

> 什么样的文法才能使用预测分析呢？才能不用回溯呢？

> 根据自己想要的目标，设想出一个一定能满足目标的最方便的文法，但这个文法限制太多了，可以在同样满足目标的前提下，尝试一点一点放宽这个限制，提出新的文法

#### 1.1 S_文法

<img src="README.assets/image-20220908145609458.png" alt="image-20220908145609458" style="zoom:67%;" />

<img src="README.assets/image-20220908145620387.png" alt="image-20220908145620387" style="zoom:80%;" />

> 由此观之，候选式指的是**右部**

> <img src="README.assets/image-20220908145627510.png" alt="image-20220908145627510" style="zoom:80%;" />

#### 1.2 空产生式的使用

<img src="README.assets/image-20220908150030515.png" alt="image-20220908150030515" style="zoom:67%;" />

- 什么是A的后面？从分析树的角度看，就是当前分析树的**右紧邻兄弟节点**，看这个节点能不能推出输入符（或者这个节点直接就是输入符了）

#### 1.3 非终结符的后继符号集

<img src="README.assets/image-20220908150646669.png" alt="image-20220908150646669" style="zoom:77%;" />

<img src="README.assets/image-20220908150658255.png" alt="image-20220908150658255" style="zoom:67%;" />

> <img src="README.assets/image-20220908150715047.png" alt="image-20220908150715047" style="zoom:67%;" />

#### 1.4 产生式的可选集

<img src="README.assets/image-20220908150804663.png" alt="image-20220908150804663" style="zoom:80%;" />

#### 1.5 q_文法

<img src="README.assets/image-20220908151118249.png" alt="image-20220908151118249" style="zoom:80%;" />

> 这里说成“相同左部”，其实和S_文法那里说的“同一非终结符”是一样的约束前提

#### 1.6 串首终结符集

<img src="README.assets/image-20220908151502035.png" alt="image-20220908151502035" style="zoom:80%;" />

<img src="README.assets/image-20220908151508201.png" alt="image-20220908151508201" style="zoom:80%;" />

<img src="README.assets/image-20220908151517715.png" alt="image-20220908151517715" style="zoom:80%;" />

> 什么时候能用$A\rarr\alpha$来推导？用了它之后能在最左边产生输入符，也就是输入符在$\alpha$的串首终结符集中

#### 1.7 LL(1)文法

<img src="README.assets/image-20220908152044010.png" alt="image-20220908152044010" style="zoom:80%;" />

> 所谓任意两个，就是对所有相同左部产生式的约束；总之就是让能推导出的所有句型的首终结符都不相同；下面那两条的意思就是**可选集互不相交**，只不过当出现了推导出空的情况时，可以将“可选集互不相交”化简成这个样子

<img src="README.assets/image-20220908152053249.png" alt="image-20220908152053249" style="zoom:80%;" />

> <img src="README.assets/image-20220908152108491.png" alt="image-20220908152108491" style="zoom:80%;" />

### 2 FIRST集和FOLLOW集的计算





## 自底向上分析



