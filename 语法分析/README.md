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

#### 1.6 串首终结符集

<img src="README.assets/image-20220908151502035.png" alt="image-20220908151502035" style="zoom:80%;" />

<img src="README.assets/image-20220908151508201.png" alt="image-20220908151508201" style="zoom:80%;" />

<img src="README.assets/image-20220908151517715.png" alt="image-20220908151517715" style="zoom:80%;" />

#### 1.7 LL(1)文法

<img src="README.assets/image-20220908152044010.png" alt="image-20220908152044010" style="zoom:80%;" />

<img src="README.assets/image-20220908152053249.png" alt="image-20220908152053249" style="zoom:80%;" />

> <img src="README.assets/image-20220908152108491.png" alt="image-20220908152108491" style="zoom:80%;" />

### 2 FIRST集、FOLLOW集、SELECT集的计算

#### 2.1 文法符号的FIRST集

FIRST集的定义：

<img src="README.assets/image-20220922140624568.png" alt="image-20220922140624568" style="zoom:67%;" />

> 举例：
>
> <img src="README.assets/image-20220922140642461.png" alt="image-20220922140642461" style="zoom:67%;" />

算法：

<img src="README.assets/image-20220922140825904.png" alt="image-20220922140825904" style="zoom:67%;" />

#### 2.2 符号串的FIRST集

算法：

<img src="README.assets/image-20220922140904721.png" alt="image-20220922140904721" style="zoom:60%;" />

#### 2.3 非终结符的FOLLOW集

定义：

<img src="README.assets/image-20220922140942695.png" alt="image-20220922140942695" style="zoom:67%;" />

> 举例：
>
> <img src="README.assets/image-20220922141404125.png" alt="image-20220922141404125" style="zoom:67%;" />
>
> 从中可以看出，一个非终结符的FOLLOW集可能依赖于另一个非终结符的FOLLOW集，所以要进行多轮计算，直到某一轮计算中，FOLLOW集不再更新

算法：

<img src="README.assets/image-20220922141735766.png" alt="image-20220922141735766" style="zoom:67%;" />

#### 2.4 由FIRST集和FOLLOW集计算SELECT集

<img src="README.assets/image-20220922142506197.png" alt="image-20220922142506197" style="zoom:67%;" />

- 同一非终结符各个**产生式**的**可选集**互不相交

LL(1)文法可以构造预测分析表：

<img src="README.assets/image-20220922142620654.png" alt="image-20220922142620654" style="zoom:67%;" />

### 3 递归的预测分析算法

<img src="README.assets/image-20220922151018261.png" alt="image-20220922151018261" style="zoom:67%;" />

举例：

<img src="README.assets/image-20220922151033547.png" alt="image-20220922151033547" style="zoom:67%;" />

<img src="README.assets/image-20220922151043361.png" alt="image-20220922151043361" style="zoom:67%;" />

<img src="README.assets/image-20220922151053106.png" alt="image-20220922151053106" style="zoom:67%;" />

<img src="README.assets/image-20220922151101171.png" alt="image-20220922151101171" style="zoom:67%;" />

<img src="README.assets/image-20220922151109633.png" alt="image-20220922151109633" style="zoom:67%;" />

<img src="README.assets/image-20220922151118904.png" alt="image-20220922151118904" style="zoom:67%;" />

<img src="README.assets/image-20220922151127247.png" alt="image-20220922151127247" style="zoom:67%;" />

### 4 递归的预测分析算法

<img src="README.assets/image-20220922152309569.png" alt="image-20220922152309569" style="zoom:67%;" />

> 下推自动机相当于给有穷自动机增加了记忆功能。图中的例子L，有穷自动机是无法识别的，因为n没有限制，可以”无穷“个，这是矛盾的

举例：

> 初始时栈底为语言结束符，栈顶为文法开始符号

- 对比输入指针符号与栈顶符号
  - 若栈顶符号为终结符
    - 二者相等，弹栈，输入指针后移
    - 二者不相等，报错
  - 若栈顶符号为非终结符，则根据SELECT集选择产生式，根据产生式弹栈并入栈

<img src="README.assets/image-20220922153334605.png" alt="image-20220922153334605" style="zoom:67%;" />

<img src="README.assets/image-20220922153457331.png" alt="image-20220922153457331" style="zoom:67%;" />

> <img src="README.assets/image-20220922153533394.png" alt="image-20220922153533394" style="zoom:67%;" />

### 5 错误处理

#### 5.1 错误检测

<img src="README.assets/image-20220922162839893.png" alt="image-20220922162839893" style="zoom:67%;" />

#### 5.2 错误恢复

<img src="README.assets/image-20220922163108565.png" alt="image-20220922163108565" style="zoom:67%;" />

> 意思就是，出错的时候，可以直接把输入符号扔掉，直到不出错，但这样扔有点太笨了，如果这个输入符在当前非终结符的后继符号集中，可以考虑把当前非终结符扔掉，这样也可以继续往下识别

举例：

- 同步词法单元的设置：

  <img src="README.assets/image-20220922163237356.png" alt="image-20220922163237356" style="zoom:67%;" />

- <img src="README.assets/image-20220922163426663.png" alt="image-20220922163426663" style="zoom:67%;" />

- 分析表如何工作：

  <img src="README.assets/image-20220922163841834.png" alt="image-20220922163841834" style="zoom:67%;" />



### 6 总结

<img src="README.assets/image-20220922153916865.png" alt="image-20220922153916865" style="zoom:67%;" />

## 自底向上分析



