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

  - 程序片段放在右部，但具体不一定放在哪个位置

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


- 带有继承属性L.in的`SDD`

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

#### 4.1 S-属性定义

<img src="README.assets/image-20221015152700079.png" alt="image-20221015152700079" style="zoom:67%;" />

- <img src="README.assets/image-20221015152741428.png" alt="image-20221015152741428" style="zoom:67%;" />

> 举例：
>
> <img src="README.assets/image-20221015152731343.png" alt="image-20221015152731343" style="zoom:67%;" />

#### 4.2 L-属性定义

<img src="README.assets/image-20221015152828196.png" alt="image-20221015152828196" style="zoom:67%;" />

<img src="README.assets/image-20221015152955548.png" alt="image-20221015152955548" style="zoom:67%;" />

- 子结点不能依赖父结点的**综合属性**，不然可以造成循环依赖
- <img src="README.assets/image-20221015153003317.png" alt="image-20221015153003317" style="zoom:67%;" />

> 举例：
>
> <img src="README.assets/image-20221015153246116.png" alt="image-20221015153246116" style="zoom:60%;" />
>
> <img src="README.assets/image-20221015153533519.png" alt="image-20221015153533519" style="zoom:67%;" />

## 语法制导翻译方案

<img src="README.assets/image-20221015153641980.png" alt="image-20221015153641980" style="zoom:67%;" />

> <img src="README.assets/image-20221015153650024.png" alt="image-20221015153650024" style="zoom:67%;" />

<img src="README.assets/image-20221015153720708.png" alt="image-20221015153720708" style="zoom:67%;" />

### 1 将S-SDD转换为SDT/S-SDD的自底向上翻译

<img src="README.assets/image-20221015153931875.png" alt="image-20221015153931875" style="zoom:67%;" />

- 综合属性要在子结点分析完后才能计算，所以**计算综合属性的语义动作/程序片段**要放在产生式的**最右边**

> <img src="README.assets/image-20221015153939546.png" alt="image-20221015153939546" style="zoom:67%;" />

在LR过程中实现SDT，也就是==**规约**时执行语义动作==，**<u>在规约时计算属性值</u>**：

<img src="README.assets/image-20221015154533127.png" alt="image-20221015154533127" style="zoom:67%;" />

> 举例：
>
> <img src="README.assets/image-20221015154557628.png" alt="image-20221015154557628" style="zoom:67%;" />

---

*扩展LR语法分析栈：*

<img src="README.assets/image-20221015154807058.png" alt="image-20221015154807058" style="zoom:67%;" />

- 属性值要么是**<u>语义分析器规定的</u>**某些终结符的值，要么是**<u>在规约时计算</u>**出来的

- 如果属性值的大小没有限制，或者数量过多没有限制，最好使用**指针**

- **语义动作与栈操作**的对应关系举例：

  <img src="README.assets/image-20221015155156738.png" alt="image-20221015155156738" style="zoom:67%;" />

举例：

<img src="README.assets/image-20221015155244306.png" alt="image-20221015155244306" style="zoom:67%;" />

> 没有语义动作意思其实是**属性值不变**

<img src="README.assets/image-20221015155400195.png" alt="image-20221015155400195" style="zoom:67%;" />

<img src="README.assets/image-20221015155406952.png" alt="image-20221015155406952" style="zoom:67%;" />

<img src="README.assets/image-20221015155415701.png" alt="image-20221015155415701" style="zoom:67%;" /><img src="README.assets/image-20221015155857954.png" alt="image-20221015155857954" style="zoom:67%;" /><img src="README.assets/image-20221015160354257.png" alt="image-20221015160354257" style="zoom:67%;" /><img src="README.assets/image-20221015160710425.png" alt="image-20221015160710425" style="zoom:67%;" /><img src="README.assets/image-20221015160718315.png" alt="image-20221015160718315" style="zoom:67%;" />

<img src="README.assets/image-20221015160931981.png" alt="image-20221015160931981" style="zoom:67%;" /><img src="README.assets/image-20221015160944539.png" alt="image-20221015160944539" style="zoom:67%;" /><img src="README.assets/image-20221015161137145.png" alt="image-20221015161137145" style="zoom:67%;" /><img src="README.assets/image-20221015161159438.png" alt="image-20221015161159438" style="zoom:67%;" /><img src="README.assets/image-20221015161242498.png" alt="image-20221015161242498" style="zoom:67%;" />

<img src="README.assets/image-20221015161257002.png" alt="image-20221015161257002" style="zoom:67%;" />

### 2 将L-SDD转换为SDT

<img src="README.assets/image-20221015161413025.png" alt="image-20221015161413025" style="zoom:67%;" />

<img src="README.assets/image-20221015161420177.png" alt="image-20221015161420177" style="zoom:67%;" />

- ==继承属性会在即将出现时进行计算==，因为这个继承属性要么依赖父结点的继承属性，要么依赖左边符号的属性值，或者依赖于自己的属性

> 举例：
>
> <img src="README.assets/image-20221015161629207.png" alt="image-20221015161629207" style="zoom:67%;" />

<img src="README.assets/image-20221015161922492.png" alt="image-20221015161922492" style="zoom:67%;" />

> <img src="README.assets/image-20221015162341765.png" alt="image-20221015162341765" style="zoom:67%;" />

<img src="README.assets/image-20221015162411249.png" alt="image-20221015162411249" style="zoom:67%;" />

后面就会介绍这些内容

### 3 在非递归的预测分析过程中进行翻译(L-SDD)

*扩展语法分析栈：*

<img src="README.assets/image-20221015163009194.png" alt="image-20221015163009194" style="zoom:67%;" />

- 继承属性在即将出现时计算，存放在**与A平行的记录**中

- 综合属性在子结点分析完后计算，要**新增一条综合记录**存放

  > A对应的综合记录就在与A平行的记录之下

- 还要增加一种**动作记录**，指向要执行的动作

---

*举例：*

<img src="README.assets/image-20221015163548253.png" alt="image-20221015163548253" style="zoom:67%;" />

- 先将语义动作起别名

  <img src="README.assets/image-20221015163634232.png" alt="image-20221015163634232" style="zoom:67%;" />

  - 这可以看成特殊的CFG，新增了一种符号，叫**动作符号**

<img src="README.assets/image-20221015163845375.png" alt="image-20221015163845375" style="zoom:67%;" />

<img src="README.assets/image-20221015163910114.png" alt="image-20221015163910114" style="zoom:80%;" />

1. T出栈，但Tsyn不能出栈（因为还没算出来），对应**产生式右部**进栈，对应的**综合记录和动作记录**也入栈

   <img src="README.assets/image-20221015164128639.png" alt="image-20221015164128639" style="zoom:67%;" />

2. F出栈，同样方式入栈

3. digit遇到输入符，正常出栈并消耗输入，同时需要将综合属性值copy到后面的动作a~6~中

   <img src="README.assets/image-20221015164636279.png" alt="image-20221015164636279" style="zoom:67%;" />

4. digit出栈后，栈顶为动作记录，直接执行计算综合记录属性值，存放到后面的Fsyn综合记录中即可

   > 之前F出栈的时候，Fsyn没出，而Fsyn又刚好在F下，所以这时会刚好在a~6~下

   <img src="README.assets/image-20221015164936610.png" alt="image-20221015164936610" style="zoom:67%;" />

5. Fsyn出栈之前要将**综合属性值传递**给后面的动作，后面计算时会用到

   <img src="README.assets/image-20221015165018855.png" alt="image-20221015165018855" style="zoom:67%;" />

6. a~1~正常进行计算，T’也可以按照产生式出栈，同时要传递综合属性值给动作a3

   <img src="README.assets/image-20221015165308374.png" alt="image-20221015165308374" style="zoom:67%;" />

   <img src="README.assets/image-20221015165422784.png" alt="image-20221015165422784" style="zoom:67%;" />

7. *匹配，F推导，同样的出栈，传递属性值，计算属性值

   <img src="README.assets/image-20221015165610554.png" alt="image-20221015165610554" style="zoom:67%;" />

   <img src="README.assets/image-20221015165733564.png" alt="image-20221015165733564" style="zoom:70%;" />

8. T’推导，传递，计算，copy，出栈

   <img src="README.assets/image-20221015165841506.png" alt="image-20221015165841506" style="zoom:67%;" />

   <img src="README.assets/image-20221015165909248.png" alt="image-20221015165909248" style="zoom:67%;" />

   <img src="README.assets/image-20221015165920163.png" alt="image-20221015165920163" style="zoom:67%;" />

总结传递属性值问题：

<img src="README.assets/image-20221015170817534.png" alt="image-20221015170817534" style="zoom:67%;" />

> 属性值的处理其实就是语义动作的处理，因为**属性值问题已经解耦交给语义动作**了

**出栈时执行代码**的确定，也就是**传递属性值**问题：

<img src="README.assets/image-20221015190832259.png" alt="image-20221015190832259" style="zoom:67%;" />

<img src="README.assets/image-20221015191254057.png" alt="image-20221015191254057" style="zoom:67%;" />

<img src="README.assets/image-20221015191416181.png" alt="image-20221015191416181" style="zoom:67%;" />

<img src="README.assets/image-20221015191426999.png" alt="image-20221015191426999" style="zoom:67%;" />

- 注意这里位置的判断，也就是top的计算，产生式右部是**从右向左入栈**
- 同一个符号在不同的产生式中，执行代码也可能是不同的

### 4 在递归的预测分析过程中进行翻译(L-SDD)

将**非终结符对应的过程**扩展为函数，参数就是继承属性，返回值就是综合属性，同时**主函数**也要修改

<img src="README.assets/image-20221015192735708.png" alt="image-20221015192735708" style="zoom:67%;" />

<img src="README.assets/image-20221015192757488.png" alt="image-20221015192757488" style="zoom:67%;" />

<img src="README.assets/image-20221015193649899.png" alt="image-20221015193649899" style="zoom:67%;" />

主函数：

<img src="README.assets/image-20221015192826471.png" alt="image-20221015192826471" style="zoom:67%;" />

总结算法：

<img src="README.assets/image-20221015192911245.png" alt="image-20221015192911245" style="zoom:67%;" />

<img src="README.assets/image-20221015193411560.png" alt="image-20221015193411560" style="zoom:67%;" />

- 词法单元就是终结符+属性值

### 5 L-SDD的自底向上翻译

<img src="README.assets/image-20221016140033099.png" alt="image-20221016140033099" style="zoom:67%;" />

> S-属性定义语义动作都在右部最后，可以规约时执行，很适合自底向上。而L-属性定义的语义动作可以出现在右部中间，就需要**修改文法**才能制导翻译了

**标记非终结符**：

<img src="README.assets/image-20221016181236287.png" alt="image-20221016181236287" style="zoom:67%;" />

<img src="README.assets/image-20221016181248085.png" alt="image-20221016181248085" style="zoom:67%;" />

- 注意体会上图中的修改方式，`inh`对应到了`i`，再对应到`syn`
- <img src="README.assets/image-20221016181256123.png" alt="image-20221016181256123" style="zoom:80%;" />
- <u>可以证明</u>：**如果一个文法是LL的，那么标记非终结符可以插入到产生式的任何位置，并且得到的文法是LR文法**

<img src="README.assets/image-20221016181734750.png" alt="image-20221016181734750" style="zoom:80%;" />

<img src="README.assets/image-20221016181743775.png" alt="image-20221016181743775" style="zoom:80%;" />

<img src="README.assets/image-20221016182056488.png" alt="image-20221016182056488" style="zoom:67%;" /><img src="README.assets/image-20221016182105984.png" alt="image-20221016182105984" style="zoom:67%;" /><img src="README.assets/image-20221016182143836.png" alt="image-20221016182143836" style="zoom:67%;" /><img src="README.assets/image-20221016182254262.png" alt="image-20221016182254262" style="zoom:67%;" /><img src="README.assets/image-20221016182311935.png" alt="image-20221016182311935" style="zoom:67%;" />

<img src="README.assets/image-20221016183531903.png" alt="image-20221016183531903" style="zoom:70%;" />

- 这里很迷，就是`*FNT'`会被规约成`T'`，`T'`的继承属性其实就是`M`的`T'inh`，所以可以直接算出`N`
- `T'.inh`是由产生式中紧靠`T'`左侧的标记非终结符对应的动作计算的，所以综合属性值就在当前栈顶

<img src="README.assets/image-20221016184038910.png" alt="image-20221016184038910" style="zoom:67%;" /><img src="README.assets/image-20221016184056991.png" alt="image-20221016184056991" style="zoom:67%;" />

执行代码：

<img src="README.assets/image-20221016185430228.png" alt="image-20221016185430228" style="zoom:67%;" />

- M只出现在F的右侧，所以规约出M时F一定在栈顶，一定能计算M的属性值，不然就出错了，N相对于F也是如此
- N还需要T’的继承属性，T’的继承属性是M计算的，M一定会出现

> 讲得乱七八糟的

总结：

<img src="README.assets/image-20221016185612042.png" alt="image-20221016185612042" style="zoom:67%;" />

