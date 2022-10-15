# 语法制导翻译

## 概述

### 1 什么是语法制导翻译

<img src="README.assets/image-20221015110755705.png" alt="image-20221015110755705" style="zoom:67%;" />

### 2 基本思想

表示语义信息：

<img src="README.assets/image-20221015110927823.png" alt="image-20221015110927823" style="zoom:67%;" />

- 类型
- 值
- 地址
- …

计算**语义属性**：

<img src="README.assets/image-20221015111128096.png" alt="image-20221015111128096" style="zoom:67%;" />

### 3 两个概念

<img src="README.assets/image-20221015111231482.png" alt="image-20221015111231482" style="zoom:67%;" />

- SDD：

  - 对CFG的推广

    <img src="README.assets/image-20221015112410074.png" alt="image-20221015112410074" style="zoom:67%;" />

    > <img src="README.assets/image-20221015112555915.png" alt="image-20221015112555915" style="zoom:67%;" />
    >
    > 举例：
    >
    > <img src="README.assets/image-20221015112657790.png" alt="image-20221015112657790" style="zoom:67%;" />

- SDT：

  <img src="README.assets/image-20221015112931145.png" alt="image-20221015112931145" style="zoom:67%;" />

  > 举例：
  >
  > <img src="README.assets/image-20221015112952494.png" alt="image-20221015112952494" style="zoom:67%;" />

对比SDD与SDT：

<img src="README.assets/image-20221015113058972.png" alt="image-20221015113058972" style="zoom:67%;" />

## 语法制导定义

> <img src="README.assets/image-20221015143518917.png" alt="image-20221015143518917" style="zoom:67%;" />

### 1 文法符号的属性

<img src="README.assets/image-20221015143540034.png" alt="image-20221015143540034" style="zoom:67%;" />

*综合属性：*

- 非终结符的综合属性：

  <img src="README.assets/image-20221015143607657.png" alt="image-20221015143607657" style="zoom:67%;" />

  > <img src="README.assets/image-20221015143713279.png" alt="image-20221015143713279" style="zoom:67%;" />

- 终结符的综合属性：

  <img src="README.assets/image-20221015143720210.png" alt="image-20221015143720210" style="zoom:67%;" />

  > 由词法分析器提供

---

*继承属性：*

- 非终结符的继承属性：

  <img src="README.assets/image-20221015143902398.png" alt="image-20221015143902398" style="zoom:67%;" />

  > <img src="README.assets/image-20221015143916555.png" alt="image-20221015143916555" style="zoom:67%;" />

- 终结符没有继承属性：

  <img src="README.assets/image-20221015143941698.png" alt="image-20221015143941698" style="zoom:67%;" />

---

*举例：*

- 带有综合属性的SDD

  <img src="README.assets/image-20221015144407117.png" alt="image-20221015144407117" style="zoom:67%;" />

  > 有时语义规则的目的是产生**副作用**，比如打印语句，语义规则会写成**过程调用**的形式，可以看成是在定义产生式左部的虚综合属性，因为用到了子结点的属性值；
  >
  > `digit.lexval`是词法分析器提供的词法值

  <img src="README.assets/image-20221015144652338.png" alt="image-20221015144652338" style="zoom:67%;" />

- 带有继承属性L.in的SDD

  <img src="README.assets/image-20221015144919760.png" alt="image-20221015144919760" style="zoom:67%;" />

  > 这里T的属性还是综合属性，L的属性是**继承属性**；
  >
  > `id.lexeme`是词法分析器提供的词法值，表示构成id的字符序列；
  >
  > 副作用`addtype`的功能是在符号表中为`id.lexeme`创建一条**记录**，并将其**类型**设置为`L.inh`，也可以看成虚综合属性

  <img src="README.assets/image-20221015145329074.png" alt="image-20221015145329074" style="zoom:67%;" />

### 2 属性文法

<img src="README.assets/image-20221015145449575.png" alt="image-20221015145449575" style="zoom:67%;" />

> 举例：
>
> <img src="README.assets/image-20221015145457815.png" alt="image-20221015145457815" style="zoom:67%;" />

### 3 SDD的求值顺序

> <img src="README.assets/image-20221015145739860.png" alt="image-20221015145739860" style="zoom:67%;" />

<img src="README.assets/image-20221015145757602.png" alt="image-20221015145757602" style="zoom:80%;" />

顺序的重点在于**依赖关系**

---

*依赖图：*

<img src="README.assets/image-20221015145953330.png" alt="image-20221015145953330" style="zoom:67%;" />

> 举例：
>
> <img src="README.assets/image-20221015150045477.png" alt="image-20221015150045477" style="zoom:67%;" />
>
> - 继承属性在左边，综合属性在右边
> - 虚结点：之前据说的虚综合属性，图中的由自身属性和子id结点共同定义

- 根据依赖图计算属性：拓扑排序

  <img src="README.assets/image-20221015150438082.png" alt="image-20221015150438082" style="zoom:67%;" />

  > 举例：
  >
  > <img src="README.assets/image-20221015150612260.png" alt="image-20221015150612260" style="zoom:67%;" />

- 综合属性与继承属性的求值顺序规律：

  <img src="README.assets/image-20221015150743683.png" alt="image-20221015150743683" style="zoom:67%;" />

  > 举例：
  >
  > <img src="README.assets/image-20221015150838386.png" alt="image-20221015150838386" style="zoom:67%;" /><img src="README.assets/image-20221015150851132.png" alt="image-20221015150851132" style="zoom:67%;" />
  >
  > 如果图中没有**环**，那么至少存在一个**拓扑排序**

### 4 SDD的属性定义

<img src="README.assets/image-20221015151200291.png" alt="image-20221015151200291" style="zoom:60%;" />

<img src="README.assets/image-20221015151214198.png" alt="image-20221015151214198" style="zoom:67%;" />

<img src="README.assets/image-20221015151228600.png" alt="image-20221015151228600" style="zoom:67%;" />















