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

> 左公因子是针对**同一个非终结符**的

<img src="README.assets/image-20220908145240981.png" alt="image-20220908145240981" style="zoom:67%;" />

> 本质x1是在**推迟决定**

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

每个非终结符对应一条产生式，选择产生式的逻辑直接写在了 

举例：

<img src="README.assets/image-20220922151033547.png" alt="image-20220922151033547" style="zoom:67%;" />

<img src="README.assets/image-20220922151043361.png" alt="image-20220922151043361" style="zoom:67%;" />

<img src="README.assets/image-20220922151053106.png" alt="image-20220922151053106" style="zoom:67%;" />

<img src="README.assets/image-20220922151101171.png" alt="image-20220922151101171" style="zoom:67%;" />

<img src="README.assets/image-20220922151109633.png" alt="image-20220922151109633" style="zoom:67%;" />

<img src="README.assets/image-20220922151118904.png" alt="image-20220922151118904" style="zoom:67%;" />

<img src="README.assets/image-20220922151127247.png" alt="image-20220922151127247" style="zoom:67%;" />

### 4 非递归的预测分析算法

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

### 0 补充

#### 0.1 系统框架与问题

<img src="README.assets/image-20221110092249791.png" alt="image-20221110092249791" style="zoom:67%;" />

<img src="README.assets/image-20221110092351208.png" alt="image-20221110092351208" style="zoom:67%;" />

-   输入缓冲
-   栈
-   表 
-   控制程序

找句型、句柄：

-   :star:（重要区别）：自底向上分析中，**栈+输入缓冲**中的内容是句型，栈中的只是句型的前缀

    >   如果是自顶向下的，只要栈中的就够了，就是句型

-   形成**句柄**时可以规约，句柄就是**产生式右部**

重要问题：

-   该移进还是该归约，归约的时候用哪个归约

    >   **表**可以告诉我们

    <img src="README.assets/image-20221110093025199.png" alt="image-20221110093025199" style="zoom:50%;" />

#### 0.2 两大类方法的思想

*优先法：*

>   优先级：**归约的优先级**

用优先级确定何时规约何时移进

优先级在归约中的作用：

-   我比你后归约（优先级比你低），我就要让你移入，
-   如果我们要同时归约（优先级相等），我还得让你移入才能归约
-   我比你先归约（优先级比低高），我就直接归约了
-   能归约的时候归约啥呢？就是从**大于**到**第一次**小于的地方（不包括第一次小于）

:star:核心问题：优先级的规定：

-   优先级一般只看距离栈顶最近的终结符，非终结符忽略
-   算符优先

---

*状态法：*

...

（已经总结）

#### 0.3 算符优先分析法

优先级的一般规定（注意，只规定终结符就够了）

![image-20221110094018066](README.assets/image-20221110094018066.png)

-   左右括号同时规约才对，所以相等
-   加法从左到右算就好了，不必两个加法同时，所以加法大于加法

---

*文法特征：*

<img src="README.assets/image-20221110094312049.png" alt="image-20221110094312049" style="zoom:67%;" />

-   没有**两个大写符号/非终结符相连**，这也叫**算符文法**

-   从文法中看到优先级：

    >   看不出优先级的就是二义性的，就是普通的算符文法；能看出来优先关系的，就是算符优先文法

    -   左右括号同时出现，优先级相等
    -   形成T才能归约E，而T是乘法的代表，E是加减的代表，所以乘法优先级高于加减

---

算符文法的定义：

<img src="README.assets/image-20221110094625235.png" alt="image-20221110094625235" style="zoom:67%;" />

算符优先文法的定义/优先级怎么看：

<img src="README.assets/image-20221110095951984.png" alt="image-20221110095951984" style="zoom:67%;" />

<img src="README.assets/image-20221110100325849.png" alt="image-20221110100325849" style="zoom:67%;" />

-   能推断出优先级，没矛盾的，就是**算符优先**的了，要在算符文法基础上

    >   对于不能通过产生式判断的算符文法，也可以强行规定优先级关系，使其成为算法优先文法

-   只有有可能**相邻**的符号之间才有必要规定优先级，才有可能在分析过程中产生优先级的比较，不然的话就报错

    >   :star:相邻的概念：直接相连，中间只隔一个非终结符

-   通过产生式就能看出来，要先规约谁，需要先规约谁。如果优先级不能这样确定，就不是算符优先文法

---

算符优先矩阵：

>   优先关系确定的原则：
>
>   ![image-20221110100506002](README.assets/image-20221110100506002.png)

-   为了方便计算，定义两类集合：

    ![image-20221110100526766](README.assets/image-20221110100526766.png)

-   规则：

    <img src="README.assets/image-20221110100651944.png" alt="image-20221110100651944" style="zoom:67%;" />

    -   这里的最后两条规则，实际上看的时候，就顺着B往下推就好了，接着看B推出的东西有没有那种两两相邻的，有就加入集合中

-   填写矩阵：

    -   矩阵默认情况是，左边竖着的代表栈内符号，上边横着的代表输入缓冲中的符号
    -   看所有产生式的右部，两个**两个符号滑动窗口**看，找到的符号之间的关系就写入矩阵中，都分析完了，找不到的就说明没有这种情况，出现冲突了就说明这不是算符优先

    <img src="README.assets/image-20221110105344775.png" alt="image-20221110105344775" style="zoom:67%;" />

---

*其他问题：*

-   有时会遇到需要归约但没有产生式可用的情况，这是因为没有规定非终结符的优先级关系，这个时候卡个bug，找形式相同的产生式归约即可

-   “句柄”问题，算符优先文法找不到真正的句柄（最左直接短语），而是**最左素短语**

    <img src="README.assets/image-20221110105930174.png" alt="image-20221110105930174" style="zoom:80%;" />

-   素短语的计算：素短语不能含有更小的素短语

    <img src="README.assets/image-20221110111313290.png" alt="image-20221110111313290" style="zoom:67%;" />

    1.   素短语首先是短语，所以需要先计算短语
    2.   然后按定义去排除

    <img src="README.assets/image-20221110111338099.png" alt="image-20221110111338099" style="zoom:67%;" /><img src="README.assets/image-20221110111344194.png" alt="image-20221110111344194" style="zoom:67%;" />

    <img src="README.assets/image-20221110111541041.png" alt="image-20221110111541041" style="zoom:67%;" /><img src="README.assets/image-20221110111547493.png" alt="image-20221110111547493" style="zoom:67%;" />

-   优先函数：节省算符优先矩阵的存储空间

    <img src="README.assets/image-20221110112419623.png" alt="image-20221110112419623" style="zoom:67%;" />

    <img src="README.assets/image-20221110112429936.png" alt="image-20221110112429936" style="zoom:50%;" />

    -   构造方法：用偏序关系构造DAG，计算拓扑排序，并基于拓扑排序构造优先函数

        <img src="README.assets/image-20221110112817005.png" alt="image-20221110112817005" style="zoom:67%;" />

---

*算符优先分析算法：*

<img src="README.assets/image-20221110111843083.png" alt="image-20221110111843083" style="zoom:67%;" />

1.   找要比较优先级的双方
2.   根据优先级大小判断该移进还是归约
     -   移进很简单
     -   归约就要找往下找第一个小于的地方，然后归约

---

*总结*：

<img src="README.assets/image-20221110113019478.png" alt="image-20221110113019478" style="zoom:67%;" />

#### 0.4 规范句型活前缀

规范句型活前缀：当分析栈中形成句柄后，分析栈中的所有内容就是活前缀了



### 1 概述

#### 1.1 移入-归约分析简介

<img src="README.assets/image-20220924211403301.png" alt="image-20220924211403301" style="zoom:67%;" />

> 举例：
>
> <img src="README.assets/image-20220924211637159.png" alt="image-20220924211637159" style="zoom:67%;" />
>
> 句柄形成后立即归约，所以每一步归约都是**最左归约**；
>
> 根据之前学过的知识知道，每次使用产生式进行**最右推导**，得到的符号串都是一个句型，称之为“**最右句型**”或“**规范句型**”，所以反过来，最左归约在即将使用产生式之前也应该是一个**规范句型**，表现在上图中，就是蓝色区间的每一部分，**栈内符号和剩余输入**拼接成一个**规范句型**

#### 1.2 移入-归约分析的工作过程

<img src="README.assets/image-20220924212445577.png" alt="image-20220924212445577" style="zoom:67%;" />

<img src="README.assets/image-20220924212505009.png" alt="image-20220924212505009" style="zoom:67%;" />

#### 1.3 移入-归约分析中的关键问题

> 举例发现问题：
>
> <img src="README.assets/image-20220924212901401.png" alt="image-20220924212901401" style="zoom:60%;" />
>
> <img src="README.assets/image-20220924212919155.png" alt="image-20220924212919155" style="zoom:67%;" />
>
> 产生式的右部不一定是**<u>当前句型</u>**的直接短语，而每次其实是要选**<u>当前句型</u>**的**最左直接短语**来归约的，所以不能看到某个产生式的右部出现了就直接用，而是在使用之前对比所有可用的产生式右部，看哪个是**最左直接短语**。
>
> > 比如上图中画红线的那一行，是即将归约前的一行，它是句型$var<IDS>,i_B:real$，这个句型的最左直接短语应该是$<IDS>,i_B$而不是$i_B$

给出句柄的严谨定义：**当前句型的最左直接短语**

> 当前句型对应了一棵**当前的语法分析树**（是在动态变化的），从而有着当前的短语和当前的直接短语

> **<u>如何正确的识别句柄</u>**？这就是接下来要探讨的问题，也是**<u>自底向上分析的关键问题</u>**

### 2 LR分析法

#### 2.1 概述与基本原理

<img src="README.assets/image-20220924214050768.png" alt="image-20220924214050768" style="zoom:67%;" />

<img src="README.assets/image-20220924214842670.png" alt="image-20220924214842670" style="zoom:67%;" />

- 移进状态：圆点后面是终结符
- 待约状态：圆点后面是非终结符
- 归约状态：圆点后面没有符号

#### 2.2 结构与工作过程

<img src="README.assets/image-20220924214931344.png" alt="image-20220924214931344" style="zoom:67%;" />

> 注意左边有一个与符号栈平行的**状态栈**

LR分析表：

<img src="README.assets/image-20220924215137823.png" alt="image-20220924215137823" style="zoom:67%;" />

- 在有输入时，就要根据当前状态和**输入符号**使用$s_n$，注意是输入符号而不是栈顶符号

- 使用$r_n$进行归约时，也要跟着**弹出状态**，并且紧跟着规约之后，栈顶是非终结符，要进行一次***GOTO***状态转移，再根据新状态和**输入符号**进行***ACTION***

  > 这样的操作本质是为了**<u>保证符号栈和状态栈平行</u>**，平行之后才能ACTION

- 如果输入符号只剩结束符$\$$了，就一直把$\$$当成输入

> 分析表的应用举例：
>
> <img src="README.assets/image-20220924215330984.png" alt="image-20220924215330984" style="zoom:67%;" />
>
> <img src="README.assets/image-20220924220423671.png" alt="image-20220924220423671" style="zoom:45%;" />
>
> <img src="README.assets/image-20220924215527308.png" alt="image-20220924215527308" style="zoom:67%;" />
>
> <img src="README.assets/image-20220924215647663.png" alt="image-20220924215647663" style="zoom:67%;" />
>
> <img src="README.assets/image-20220924215736031.png" alt="image-20220924215736031" style="zoom:67%;" />
>
> <img src="README.assets/image-20220924215804658.png" alt="image-20220924215804658" style="zoom:67%;" />
>
> <img src="README.assets/image-20220924221326209.png" alt="image-20220924221326209" style="zoom:67%;" />
>
> <img src="README.assets/image-20220924221558018.png" alt="image-20220924221558018" style="zoom:60%;" />
>
> <img src="README.assets/image-20220924221905720.png" alt="image-20220924221905720" style="zoom:67%;" />
>
> <img src="README.assets/image-20220924221920008.png" alt="image-20220924221920008" style="zoom:67%;" />
>
> <img src="README.assets/image-20220924222007358.png" alt="image-20220924222007358" style="zoom:60%;" />
>
> <img src="README.assets/image-20220924222035327.png" alt="image-20220924222035327" style="zoom:67%;" />

工作过程总结：

<img src="README.assets/image-20220924222225585.png" alt="image-20220924222225585" style="zoom:67%;" />

<img src="README.assets/image-20220924222304378.png" alt="image-20220924222304378" style="zoom:67%;" />

<img src="README.assets/image-20220924222312834.png" alt="image-20220924222312834" style="zoom:67%;" />

LR分析算法：

<img src="README.assets/image-20220924222510343.png" alt="image-20220924222510343" style="zoom:67%;" />

> 有了分析表之后，LR分析算法十分简单
>
> <img src="README.assets/image-20220924222524769.png" alt="image-20220924222524769" style="zoom:67%;" />
>
> 接下来的重点就是**分析表**了！

### 3 LR(0)分析法

#### 3.1 概念

项目：项目描述了句柄识别的状态

<img src="README.assets/image-20220924223855627.png" alt="image-20220924223855627" style="zoom:67%;" />

增广文法：增广文法让分析器**只有一个接受状态**

<img src="README.assets/image-20220924224058611.png" alt="image-20220924224058611" style="zoom:67%;" />

> 举例：文法中的项目
>
> <img src="README.assets/image-20220924224418464.png" alt="image-20220924224418464" style="zoom:67%;" />
>
> 还有许多**移进项目**和**待约项目**没有标明

后继项目：

<img src="README.assets/image-20220924224503158.png" alt="image-20220924224503158" style="zoom:67%;" />

项目的等价性：

> 举例：
>
> <img src="README.assets/image-20220924224733695.png" alt="image-20220924224733695" style="zoom:67%;" />
>
> 一个**项目的$\cdot$后面紧跟着非终结符**时，就存在**等价项目**，可以理解成“在等待xxx，而xxx能推导出xxx，所以其实就是在等待xxx**最左边的符号**”，等价项目具有传递性，直到$\cdot$后面变成终结符或者空

<img src="README.assets/image-20220924225217398.png" alt="image-20220924225217398" style="zoom:67%;" />

#### 3.2 自动机与分析表构造思想

<u>LR(0)自动机构造举例</u>：

1. 用开始符号产生式的初始项目**项目集闭包**生成**初始状态**

2. 用初始状态中的每个项目结合它**“等待”的符号**得到每个**后继项目**，再用每个后继项目**项目集闭包**生成**状态**

   > 一个项目可以出现在多个状态中

3. 遍历每个状态中的每个项目，不断得到后继项目的项目集闭包并生成新状态，直到新状态中所有项目都是**归约项目**（已经存在的状态之间是可能互相转换的）

<img src="README.assets/image-20220924230210713.png" alt="image-20220924230210713" style="zoom:67%;" />

<u>通过状态机构造分析表举例</u>：

- 边上是非终结符的，对应GOTO表；边上是终结符的，对应ACTION表

- 一行一行填表

- **接收项目**是单独在一个状态里，对应**接收状态**，在表中与结束符$\$$形成表项$acc$

- **待约**状态对应的表项都是$s_n$，**归约**状态对应的表项都是$r_n$，而且能归约的时候不管遇到什么输入都会执行归约的ACTION

  <img src="README.assets/image-20220926133436126.png" alt="image-20220926133436126" style="zoom:67%;" />

#### 3.4 自动机与分析表构造算法

<u>项目集闭包</u>：

<img src="README.assets/image-20220926133055881.png" alt="image-20220926133055881" style="zoom:67%;" />

<img src="README.assets/image-20220926133109207.png" alt="image-20220926133109207" style="zoom:67%;" />

<u>后继项目集闭包</u>：

<img src="README.assets/image-20220926133301575.png" alt="image-20220926133301575" style="zoom:60%;" />

<u>构造LR(0)自动机的状态集</u>：

<img src="README.assets/image-20220926134322599.png" alt="image-20220926134322599" style="zoom:67%;" />

<u>LR(0)分析表构造算法</u>：

<img src="README.assets/image-20220926134533579.png" alt="image-20220926134533579" style="zoom:67%;" />

<u>LR(0)自动机的形式化定义</u>：

<img src="README.assets/image-20220926135222817.png" alt="image-20220926135222817" style="zoom:67%;" />

- LR(0)自动机的**冲突**问题：

  - 移进/归约冲突：

  <img src="README.assets/image-20220926135729793.png" alt="image-20220926135729793" style="zoom:57%;" />

  <img src="README.assets/image-20220926135748648.png" alt="image-20220926135748648" style="zoom:50%;" />

  - 归约/归约冲突：

    <img src="README.assets/image-20220926135915707.png" alt="image-20220926135915707" style="zoom:67%;" />

    <img src="README.assets/image-20220926135909484.png" alt="image-20220926135909484" style="zoom:67%;" /><img src="README.assets/image-20220926135849706.png" alt="image-20220926135849706" style="zoom:67%;" />

如果LR(0)分析表中没有语法分析动作**冲突**，那么给定的文法就称为**<u>LR(0)文法</u>**

不是所有CFG都能用LR(0)方法进行分析，也就是说，**<u>CFG不总是LR(0)文法</u>**

> 如何解决冲突？SLR和LR(1)会给我们答案

### 4 SLR分析

> LR(0)分析为啥会有问题？因为没考虑**上下文环境**，没有向前查看符号
>
> <img src="README.assets/image-20220927092352589.png" alt="image-20220927092352589" style="zoom:67%;" />
>
> 如果能看看**FOLLOW集**，就会发现E后面不可能接*号，所以把T归约成E就是不对的。
>
> 这正是SLR分析的思想

#### 4.1 基本思想

<img src="README.assets/image-20220927092614379.png" alt="image-20220927092614379" style="zoom:67%;" />

- 所以其实要看的就是两种东西，对于移进/待约项目，看**圆点右侧的符号**；对于归约项目，看**左部FOLLOW集**

- 要保证**两两不相交**，这样选择就是唯一的；当然，如果不能保证两两不相交，那就还是有冲突，这种冲突会在下一小节解决

- 只向下查看一个符号就可以判断怎么做，也叫SLR(1)

  > S：Simple，只通过FOLLOW集化解冲突（之后会遇到需要更复杂方法才能化简的冲突）；
  >
  > LR(1)可简称为LR，所以叫SLR

> 举例1：
>
> LR(0)：
>
> <img src="README.assets/image-20220926135748648.png" alt="image-20220926135748648" style="zoom:50%;" />
>
> SLR：
>
> <img src="README.assets/image-20220927092956258.png" alt="image-20220927092956258" style="zoom:67%;" />
>
> - 在SLR分析表中，发现对于归约状态（含有归约项目的），并不全都是r了，而是只有在遇到FOLLOW集中元素时才归约

> 举例2：归约/归约冲突
>
> <img src="README.assets/image-20220927093328723.png" alt="image-20220927093328723" style="zoom:67%;" />

#### 4.2 SLR分析表构造算法

> 与LR(0)类似，不同之处在于对归约项目的处理，其他的都没变（CLOSURE、GOTO、项目集之类的算法还没变）
>
> LR(0)的分析表构造算法：
>
> <img src="README.assets/image-20220926134533579.png" alt="image-20220926134533579" style="zoom:67%;" />

<img src="README.assets/image-20220927093817378.png" alt="image-20220927093817378" style="zoom:80%;" />

- 变成了只对于左部FOLLOW集中的符号采取归约动作
- 如果给定文法的**SLR分析表**中不存在有冲突的动作，那么该文法称为**SLR文法**

#### 4.3 SLR中的冲突

<img src="README.assets/image-20220927094323320.png" alt="image-20220927094323320" style="zoom:67%;" />

怎么看的冲突？就是看那两部分，**圆点右**和**左部FOLLOW**

### 5 LR(1)分析

> SLR分析的问题：
>
> <img src="README.assets/image-20220927094552942.png" alt="image-20220927094552942" style="zoom:67%;" />
>
> 也就是说，**不在左部FOLLOW集中肯定不能用它归约**，但在左部FOLLOW集中不一定就非要用它归约

#### 5.1 基本思想

<img src="README.assets/image-20220927111450307.png" alt="image-20220927111450307" style="zoom:67%;" />

- 在特定的情况下，A后面能接的东西虽然都在FOLLOW集中，但都是子集，而且是有所不同的，这受到**A进一步会被规约成的符号**的影响，A**进一步会被规约成的符号**<u>右边能接的东</u>西，与A**的FOLLOW集**的交集，才是真正能规约的输入符号集

  > 这是因为每次都是最左规约，输入符号虽然现在在FOLLOW集中，但还可能被进一步规约，这个FOLLOW集就变了
  >
  > 目前留有的疑问：
  >
  > - A进一步会被规约成的符号：目前不确定是什么
  > - A进一步会被规约成的符号右边能接的东西：可能是FOLLOW集，也可能是所在右部的下一个符号

- 所以，SLR用FOLLOW集，显然是扩大了范围。重点是找到**特定位置的特定后继符**

<u>**规范LR(1)项目**</u>：

> 在构造项目时就已经考虑到了特定位置的特定后继符问题

<img src="README.assets/image-20220927112737727.png" alt="image-20220927112737727" style="zoom:70%;" />

- 注意重点，是当前状态能跟在A后面的，也就是当前状态能跟在**<u>产生式左部符号后面</u>**的

  > SLR中只有一个带圆点的产生式，根据FOLLOW集判断用不用它(归约项目)；现在直接根据输入符，把能用它的情况分成了多个项目，每个项目对应一个输入符，可以证明，展望符一定在左部FOLLOW集中，但左部FOLLOW集中的不都是展望符；当然有时候，产生式和圆点位置相同，但展望符不同的多个，也会写在一起成这样：$A\rarr\alpha\beta, a/b/c...$

  > LR(1)规范项目中，逗号左边的可称为第一分量，逗号右边的可称为第二分量

- LR(1) 中的1指的是项目的**第二个分量**的长度

  > 可以是k，但对于大多数语言，1就够了

- <img src="README.assets/image-20220927112835287.png" alt="image-20220927112835287" style="zoom:80%;" />

  > 就是说，对于移入项目和待约项目，展望符没用，但为了定义的完整，把它定义出来了

- <img src="README.assets/image-20220927112952619.png" alt="image-20220927112952619" style="zoom:67%;" />

  > 对于归约项目，展望符是有意义的

  - 这样的a的集合总是FOLLOW(A)的子集，而且它通常是一个真子集

<u>**等价LR(1)项目**</u>：（展望符怎么求）

<img src="README.assets/image-20220927134322164.png" alt="image-20220927134322164" style="zoom:67%;" />

- 首先得出项目的**等价项目**，然后看展望符，就分两种情况了，这要看等价项目左部在原项目中右边的符号(串)$\beta$

  - $\beta$能推出空，则直接继承

    > 因为此时可以跟在B后面的就是可以跟在A后面的

  - $\beta$不能推出空，则是其FIRST集，对于FIRST集中的每一个元素，都作为一次展望符，生成一个项目

- 从求解展望符的角度看，最初的项目就是初始项目，展望符为结束符$\$$

#### 5.2 LR(1)自动机与分析表

<img src="README.assets/image-20220927134611720.png" alt="image-20220927134611720" style="zoom:80%;" />

1. 初始项目$I_0$

   <img src="README.assets/image-20220927135710338.png" alt="image-20220927135710338" style="zoom:67%;" />

   - 第二项和第三项由第一项等价出来，使用的是1)和2)产生式；由于第一项S后面没有符号，所以第二、三项继承其展望符
   - 第四项和第五项由第二项等价出来，L后面跟着终结符=，其FIRST集就是{=}，所以展望符是=
   - 第六项由第三项等价出来，由于第三项R后面没有符号，所以继承展望符
   - 其他同理，直到生成的都是移进项目，不再能推出等价项目

2. $GOTO(I_0, S)$

   ![image-20220927142249268](README.assets/image-20220927142249268.png)

   - 只有归约项目，不能等价

3. $GOTO(I_0, L)$

   <img src="README.assets/image-20220927142256235.png" alt="image-20220927142256235" style="zoom:80%;" />

   - 只有移进项目，不能等价

4. $GOTO(I_0,R)$

5. $GOTO(I_0,*)$

   <img src="README.assets/image-20220927142402868.png" alt="image-20220927142402868" style="zoom:80%;" />

6. …同理，要注意的是，展望符不同，即使产生式和圆点位置相同，也是不同的项目

<img src="README.assets/image-20220927143920131.png" alt="image-20220927143920131" style="zoom:80%;" />

<u>**LR(1)分析表**</u>：

- 对于不涉及规约项目的状态，处理方法与LR(0)相同

- 对于涉及规约项目的状态，只有ACTION列(输入符号)是其**展望符**时才能规约

  > 之前构造SLR的时候，是遇到左部FOLLOW集中的符号都能规约

<img src="README.assets/image-20220927144421053.png" alt="image-20220927144421053" style="zoom:67%;" />

<img src="README.assets/image-20220927145007836.png" alt="image-20220927145007836" style="zoom:80%;" />

> <img src="README.assets/image-20220927145018694.png" alt="image-20220927145018694" style="zoom:67%;" />
>
> 可以看到，LR(1)对SLR的状态进行了分裂（当然LR(0)的自动机也长这样）
>
> 如果除展望符外，两个LR(1)项目集是相同的，则称这两个LR(1)项目集是**同心**的
>
> > 把同心的项目都合并了，就得到LR(0)项目集了，所以这里的”心“指的就是LR(0)

#### 5.3 自动机与分析表构造算法

> 因为展望符的加入而有所修改，主要修改的对象就是展望符相关的东西，和归约项目的处理

闭包的修改：

<img src="README.assets/image-20220927145355912.png" alt="image-20220927145355912" style="zoom:67%;" />

GOTO的修改：

<img src="README.assets/image-20220927145441744.png" alt="image-20220927145441744" style="zoom:67%;" />

项集族的修改：

<img src="README.assets/image-20220927145602986.png" alt="image-20220927145602986" style="zoom:67%;" />

LR(1)自动机定义的修改：

<img src="README.assets/image-20220927145719273.png" alt="image-20220927145719273" style="zoom:67%;" />

LR分析表构造算法的修改：

<img src="README.assets/image-20220927150208767.png" alt="image-20220927150208767" style="zoom:67%;" />

### 6 LALR分析法

> LR(1)分析确实解决了几乎所有冲突，但状态太多了，想让它少点，LALR就是这个目的，合并一些动作不冲突的状态
>
> <img src="README.assets/image-20220927151044777.png" alt="image-20220927151044777" style="zoom:67%;" />
>
> 直观上理解，画出的这些状态都可以参与合并

#### 6.1 基本思想

<img src="README.assets/image-20220927151252537.png" alt="image-20220927151252537" style="zoom:67%;" />

合并哪些项目？合并只保留第一分量时(重复的只留一个)，完全相同的项目集，这样的项目集也叫m同心项目集，也就是对应LR(0)项目集相同。这其实就是在合并**展望符集合**

> 合并后的展望符集合仍为FOLLOW集的子集

#### 6.2 自动机和状态表

<img src="README.assets/image-20220927151509830.png" alt="image-20220927151509830" style="zoom:67%;" />

<img src="README.assets/image-20220927151537863.png" alt="image-20220927151537863" style="zoom:80%;" />

> <img src="README.assets/image-20220927144421053.png" alt="image-20220927144421053" style="zoom:57%;" />

#### 6.3 合并同心项目集带来的问题

**<u>冲突问题</u>**：

- 按照之前的方法合并，就会出现这种**归约-归约冲突**，同一个输入符，不知道该用哪个产生式归约了，因为它们的**展望符**都相同

<img src="README.assets/image-20220927151953015.png" alt="image-20220927151953015" style="zoom:80%;" />

> 为啥不会造成移进-归约冲突？因为冲突的本质是展望符冲突，而移进时展望符没用
>
> > 合并之前已经没有移进-归约冲突了

**<u>推迟错误发现的问题</u>**：

- 合并同心项集后，虽然不产生冲突，但可能会**推迟错误的发现**

<img src="README.assets/image-20220927152758008.png" alt="image-20220927152758008" style="zoom:67%;" />

LALR分析法可能会作多余的**归约动作**，但绝不会作错误的**移进操作**

> LALR其实是在合并展望符集合，展望符与归约有关，与移进无关

#### 6.4 LALR的特点

形式上：

<img src="README.assets/image-20220927153032375.png" alt="image-20220927153032375" style="zoom:67%;" />

内容上：

<img src="README.assets/image-20220927153048770.png" alt="image-20220927153048770" style="zoom:67%;" />

分析能力上：

- 比LR(1)更晚发现错误
- 比SLR更细致地划分信息，延迟发现的错误其实是更少的

<img src="README.assets/image-20220927153115236.png" alt="image-20220927153115236" style="zoom:80%;" />

### 7 LR对二义性文法的分析与错误处理

#### 7.1 二义性文法的特点

<img src="README.assets/image-20221109220648911.png" alt="image-20221109220648911" style="zoom:67%;" />

>   LR的指的是LR(0)的

#### 7.2 LR中二义性的消除

例1：算术表达式文法

<img src="README.assets/image-20221109221046437.png" alt="image-20221109221046437" style="zoom:67%;" />

使用优先级和结合性解决二义性

-   对于7：如果是乘号就移进（因为乘法优先级更高），如果是加号就要归约（因为加法是左结合的）
-   对于8：一定归约，因为乘法优先级高

<img src="README.assets/image-20221109221106020.png" alt="image-20221109221106020" style="zoom:67%;" />



例2：if语句文法

<img src="README.assets/image-20221109221158182.png" alt="image-20221109221158182" style="zoom:67%;" />

（正则定义）

<img src="README.assets/image-20221109221220613.png" alt="image-20221109221220613" style="zoom:67%;" />

-   通过引入**就近匹配原则**消除二义性

<img src="README.assets/image-20221109221409621.png" alt="image-20221109221409621" style="zoom:67%;" />

#### 7.3 二义性文法的使用

<img src="README.assets/image-20221109221429806.png" alt="image-20221109221429806" style="zoom:67%;" />

#### 7.4 语法错误的检测

<img src="README.assets/image-20221109221503894.png" alt="image-20221109221503894" style="zoom:67%;" />

#### 7.5 错误恢复策略

<img src="README.assets/image-20221109221523737.png" alt="image-20221109221523737" style="zoom:67%;" />

<img src="README.assets/image-20221109221945381.png" alt="image-20221109221945381" style="zoom:67%;" />

-   没听懂，需要补充



<img src="README.assets/image-20221109221958954.png" alt="image-20221109221958954" style="zoom:67%;" />



举例：

<img src="README.assets/image-20221109222403169.png" alt="image-20221109222403169" style="zoom:67%;" />

<img src="README.assets/image-20221109222421420.png" alt="image-20221109222421420" style="zoom:67%;" />

-   思想就是计算出**缺什么**，然后假设不缺，移入到对应状态，再继续分析
-   如果归约状态下出错了可以直接规约
