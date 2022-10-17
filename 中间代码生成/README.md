# 中间代码生成

>   各类语句的翻译，声明、赋值、控制、过程调用......

## 1 声明语句的翻译

主要任务：

<img src="README.assets/image-20221017162224521.png" alt="image-20221017162224521" style="zoom:67%;" />

### 1.1 类型表达式 Type Expressions

#### 1.1.1 基本类型

<img src="README.assets/image-20221017160700101.png" alt="image-20221017160700101" style="zoom:67%;" />

#### 1.1.2 类型名

<img src="README.assets/image-20221017160805187.png" alt="image-20221017160805187" style="zoom:67%;" />

#### 1.1.3 类型构造符

<u>数组构造符`array`</u>

<img src="README.assets/image-20221017160908702.png" alt="image-20221017160908702" style="zoom:67%;" />

---

<u>指针构造符`pointer`</u>

<img src="README.assets/image-20221017161504706.png" alt="image-20221017161504706" style="zoom:67%;" />

---

<u>笛卡尔乘积构造符$\times$</u>

<img src="README.assets/image-20221017161538624.png" alt="image-20221017161538624" style="zoom:67%;" />

---

<u>函数构造符$\rarr$</u>

<img src="README.assets/image-20221017161610610.png" alt="image-20221017161610610" style="zoom:67%;" />

-   $T_i$相当于参数
-   $R$相当于返回值

---

<u>记录构造符`record`</u>

<img src="README.assets/image-20221017161839758.png" alt="image-20221017161839758" style="zoom:67%;" />

-   n个字段，每个字段的名字、标识符是$N_i$，每个字段的类型是$T_i$

#### 1.1.4 类型表达式的绑定

举例：

<img src="README.assets/image-20221017162129785.png" alt="image-20221017162129785" style="zoom:67%;" />

### 1.2 局部变量的存储分配

<img src="README.assets/image-20221017162343027.png" alt="image-20221017162343027" style="zoom:67%;" />

-   由类型表达式得知类型宽度
-   根据宽度分配相对地址
-   还要管理符号表

---

文法举例：

<img src="README.assets/image-20221017162741469.png" alt="image-20221017162741469" style="zoom:67%;" />

-   需要收集类型、宽度，因而定义这样的属性

    <img src="README.assets/image-20221017162826562.png" alt="image-20221017162826562" style="zoom:67%;" />

-   特殊的变量：

    <img src="README.assets/image-20221017163007939.png" alt="image-20221017163007939" style="zoom:67%;" />

    -   `offset`有初始值，这里为0
    -   `t, w`的作用在下面的例子中介绍

-   副作用`enter`：每当识别出一个声明后，就创建一条记录

    <img src="README.assets/image-20221017163212402.png" alt="image-20221017163212402" style="zoom:67%;" />

    >   建立记录后`offset`就要后移了

---

文法识别过程举例：

<img src="README.assets/image-20221017164518160.png" alt="image-20221017164518160" style="zoom:67%;" />

>   当然，首先要验证，相同左部相同的产生式的SELECT集互不相交

基本类型举例：

1.   从开始符号推导，动作符在栈顶，执行动作，`offset`设置为0，动作出栈

     <img src="README.assets/image-20221017164432735.png" alt="image-20221017164432735" style="zoom:67%;" /><img src="README.assets/image-20221017164530336.png" alt="image-20221017164530336" style="zoom:67%;" />

2.   根据输入推导D

     <img src="README.assets/image-20221017164713600.png" alt="image-20221017164713600" style="zoom:67%;" /><img src="README.assets/image-20221017164730748.png" alt="image-20221017164730748" style="zoom:67%;" />

3.   根据输入推导T

     <img src="README.assets/image-20221017164713600.png" alt="image-20221017164713600" style="zoom:67%;" /><img src="README.assets/image-20221017164758861.png" alt="image-20221017164758861" style="zoom:67%;" />

4.   根据输入推导B，可以读取输入并出栈`real`

     <img src="README.assets/image-20221017164713600.png" alt="image-20221017164713600" style="zoom:67%;" /><img src="README.assets/image-20221017164850291.png" alt="image-20221017164850291" style="zoom:67%;" />

5.   执行语义动作a，计算B的综合属性

     <img src="README.assets/image-20221017165004527.png" alt="image-20221017165004527" style="zoom:67%;" /><img src="README.assets/image-20221017165028373.png" alt="image-20221017165028373" style="zoom:67%;" />

6.   执行语义动作a，给t和w赋值，其实是在传递值

     <img src="README.assets/image-20221017165004527.png" alt="image-20221017165004527" style="zoom:67%;" /><img src="README.assets/image-20221017165137392.png" alt="image-20221017165137392" style="zoom:67%;" />

7.   根据输入推导C

     <img src="README.assets/image-20221017165004527.png" alt="image-20221017165004527" style="zoom:67%;" /><img src="README.assets/image-20221017165241376.png" alt="image-20221017165241376" style="zoom:67%;" />

8.   执行语义动作a，给C的综合属性赋值，其实是通过t和w保存的值来完成的，对应着之前说的传递

     <img src="README.assets/image-20221017165004527.png" alt="image-20221017165004527" style="zoom:67%;" /><img src="README.assets/image-20221017165951801.png" alt="image-20221017165951801" style="zoom:67%;" />

9.   执行语义动作a，计算T的综合属性

     <img src="README.assets/image-20221017165004527.png" alt="image-20221017165004527" style="zoom:67%;" /><img src="README.assets/image-20221017170053046.png" alt="image-20221017170053046" style="zoom:67%;" />

10.   `id ;`匹配输入，出栈

11.   执行语义动作a，在符号表中建立记录

      <img src="README.assets/image-20221017170223755.png" alt="image-20221017170223755" style="zoom:67%;" /><img src="README.assets/image-20221017170317467.png" alt="image-20221017170317467" style="zoom:67%;" />

12.   根据输入推导D

      <img src="README.assets/image-20221017170223755.png" alt="image-20221017170223755" style="zoom:67%;" /><img src="README.assets/image-20221017170402924.png" alt="image-20221017170402924" style="zoom:67%;" />

13.   根据输入推导T

      <img src="README.assets/image-20221017170223755.png" alt="image-20221017170223755" style="zoom:67%;" /><img src="README.assets/image-20221017170458205.png" alt="image-20221017170458205" style="zoom:67%;" />

14.   根据输入推导B

      <img src="README.assets/image-20221017170223755.png" alt="image-20221017170223755" style="zoom:67%;" /><img src="README.assets/image-20221017170530358.png" alt="image-20221017170530358" style="zoom:67%;" />

15.   匹配`int`

      <img src="README.assets/image-20221017170633563.png" alt="image-20221017170633563" style="zoom:67%;" />

16.   执行语义动作a，计算B的综合属性

      <img src="README.assets/image-20221017170633563.png" alt="image-20221017170633563" style="zoom:67%;" /><img src="README.assets/image-20221017170747782.png" alt="image-20221017170747782" style="zoom:67%;" />

17.   执行语义动作a，给t和w赋值，其实是在传递值

      <img src="README.assets/image-20221017170633563.png" alt="image-20221017170633563" style="zoom:67%;" /><img src="README.assets/image-20221017170838828.png" alt="image-20221017170838828" style="zoom:67%;" />

18.   根据输入推导C、执行动作传递值给C的综合属性

      <img src="README.assets/image-20221017170633563.png" alt="image-20221017170633563" style="zoom:67%;" /><img src="README.assets/image-20221017170928358.png" alt="image-20221017170928358" style="zoom:67%;" />

19.   `id ;`匹配输入，出栈

      <img src="README.assets/image-20221017171117428.png" alt="image-20221017171117428" style="zoom:67%;" />

20.   执行语义动作，在符号表中建立记录，结束

      <img src="README.assets/image-20221017171203717.png" alt="image-20221017171203717" style="zoom:67%;" />

<img src="README.assets/image-20221017171238695.png" alt="image-20221017171238695" style="zoom:67%;" />

---

数组类型举例：

<img src="README.assets/image-20221017172004259.png" alt="image-20221017172004259" style="zoom:67%;" />

-   主要关注数组类型的形成和宽度的计算
-   体会t和w在传递类型和宽度中的作用

## 2 简单赋值语句的翻译

主要任务：

<img src="README.assets/image-20221017173257482.png" alt="image-20221017173257482" style="zoom:67%;" />

-   表达式的值需要通过三地址码计算

<img src="README.assets/image-20221017173307598.png" alt="image-20221017173307598" style="zoom:70%;" />

三地址码举例：

<img src="README.assets/image-20221017173355562.png" alt="image-20221017173355562" style="zoom:67%;" />

### 2.1 赋值语句的SDT

<img src="README.assets/image-20221017173557747.png" alt="image-20221017173557747" style="zoom:67%;" />

-   `code`用于记录三地址码，`addr`用于记录表达式值的存放地址

-   表达式值的存放地址往往就是符号表中记录的地址，通过`lookup`就可以获得

-   不涉及计算的产生式三地址码属性`code`为空即可

-   涉及到计算，有新值产生，就需要`newtemp`存放值，同时要生成三地址码，拼接`code`

    >   `||`代表连接运算



