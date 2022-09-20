# 词法分析

## 正则表达式

引例：

<img src="README.assets/image-20220907164908405.png" alt="image-20220907164908405" style="zoom:67%;" />

---

### 1 定义

<img src="README.assets/image-20220907165006688.png" alt="image-20220907165006688" style="zoom:67%;" />

> 应用举例：
>
> <img src="README.assets/image-20220907165118634.png" alt="image-20220907165118634" style="zoom:50%;" />
>
> <img src="README.assets/image-20220907165352713.png" alt="image-20220907165352713" style="zoom:67%;" />

### 2 正则语言

<img src="README.assets/image-20220907165418806.png" alt="image-20220907165418806" style="zoom:67%;" />

### 3 RE的代数定律

<img src="README.assets/image-20220907165549503.png" alt="image-20220907165549503" style="zoom:67%;" />

### 4 正则表达式与正则文法

<img src="README.assets/image-20220907165643167.png" alt="image-20220907165643167" style="zoom:67%;" />

## 正则定义

> 给一些 RE 命名 ，并在之后的 RE 中像使用 字母表中的符号一样使用这些名字

<img src="README.assets/image-20220907182206069.png" alt="image-20220907182206069" style="zoom:67%;" />

> 举例：
>
> <img src="README.assets/image-20220907182309807.png" alt="image-20220907182309807" style="zoom:67%;" />
>
> <img src="README.assets/image-20220907182508854.png" alt="image-20220907182508854" style="zoom:67%;" />

## 有穷自动机

### 1 有穷自动机简介

<img src="README.assets/image-20220907182648482.png" alt="image-20220907182648482" style="zoom:67%;" />

> 举例：
>
> <img src="README.assets/image-20220907183000926.png" alt="image-20220907183000926" style="zoom:67%;" />

### 2 FA模型与转换图

<img src="README.assets/image-20220907183030837.png" alt="image-20220907183030837" style="zoom:67%;" />

<img src="README.assets/image-20220907183109072.png" alt="image-20220907183109072" style="zoom:67%;" />

### 3 FA定义（接收）的语言

<img src="README.assets/image-20220907183137095.png" alt="image-20220907183137095" style="zoom:67%;" />

> <img src="README.assets/image-20220907183144770.png" alt="image-20220907183144770" style="zoom:60%;" />

### 4 最长子串匹配原则

<img src="README.assets/image-20220907190204790.png" alt="image-20220907190204790" style="zoom:67%;" />

## DFA与NFA

<img src="README.assets/image-20220907190643811.png" alt="image-20220907190643811" style="zoom:67%;" />

### 1 DFA

<img src="README.assets/image-20220907190728352.png" alt="image-20220907190728352" style="zoom:67%;" />

> <img src="README.assets/image-20220907190911170.png" alt="image-20220907190911170" style="zoom:67%;" />

### 2 NFA

<img src="README.assets/image-20220907190938084.png" alt="image-20220907190938084" style="zoom:67%;" />

> <img src="README.assets/image-20220907191016416.png" alt="image-20220907191016416" style="zoom:67%;" />

### 3 DFA与NFA的等价性

<img src="README.assets/image-20220907191032375.png" alt="image-20220907191032375" style="zoom:67%;" />

> <img src="README.assets/image-20220907191041705.png" alt="image-20220907191041705" style="zoom:67%;" />

### 4 $\epsilon$-NFA

<img src="README.assets/image-20220907191323660.png" alt="image-20220907191323660" style="zoom:67%;" />

> <img src="README.assets/image-20220907191331018.png" alt="image-20220907191331018" style="zoom:67%;" />

### 5 DFA算法的实现

> 从计算机实现的角度讲，DFA比NFA更容易实现

<img src="README.assets/image-20220907191808757.png" alt="image-20220907191808757" style="zoom:67%;" />

## 从RE到DFA

总体的思路：RE$\rarr$NFA$\rarr$DFA

<img src="README.assets/image-20220907191907729.png" alt="image-20220907191907729" style="zoom:67%;" />

### 1 RE$\rarr$NFA

> 总体思路：==分解、递归==

递归基础：

<img src="README.assets/image-20220907192008657.png" alt="image-20220907192008657" style="zoom:67%;" />

<img src="README.assets/image-20220907192015549.png" alt="image-20220907192015549" style="zoom:67%;" />

> 举例：分解（递归）
>
> <img src="README.assets/image-20220907192243396.png" alt="image-20220907192243396" style="zoom:67%;" />

### 2 NFA$\rarr$DFA

> 总体思路：==转换表==

<img src="README.assets/image-20220907192759283.png" alt="image-20220907192759283" style="zoom:67%;" />

下面这个例子是带有$\epsilon$的，在输入字符的前后都可以添加若干个$\epsilon$以跳转到所有可能的状态，其实就是$\epsilon$-闭包

> 所以初始状态直接是{A,B,C}

<img src="README.assets/image-20220907193703375.png" alt="image-20220907193703375" style="zoom:67%;" />

---

相关算法：子集构造法

> 因为NFA中的每个状态是其要转换成的DFA的某个状态的子集

<img src="README.assets/image-20220907194327589.png" alt="image-20220907194327589" style="zoom:67%;" />

> 算法中的空闭包函数：
>
> <img src="README.assets/image-20220907194341384.png" alt="image-20220907194341384" style="zoom:67%;" />

## 识别单词的DFA

### 1 识别标识符的DFA

<img src="README.assets/image-20220907194536884.png" alt="image-20220907194536884" style="zoom:67%;" />

### 2 识别无符号数的DFA

<img src="README.assets/image-20220907194559152.png" alt="image-20220907194559152" style="zoom:67%;" />

<img src="README.assets/image-20220907194648539.png" alt="image-20220907194648539" style="zoom:80%;" />

### 3 识别各进制无符号整数的DFA

<img src="README.assets/image-20220907195503760.png" alt="image-20220907195503760" style="zoom:67%;" />

### 4 识别注释的DFA

<img src="README.assets/image-20220907195658091.png" alt="image-20220907195658091" style="zoom:67%;" />

### 3 识别各类单词的DFA

<img src="README.assets/image-20220907195901330.png" alt="image-20220907195901330" style="zoom:67%;" />

## 词法分析阶段的错误处理

### 1 错误类型与检测

<img src="README.assets/image-20220907200205569.png" alt="image-20220907200205569" style="zoom:67%;" />

<img src="README.assets/image-20220907200222849.png" alt="image-20220907200222849" style="zoom:80%;" />

> 这里可能有点问题，就算是终止状态也应该报错	

### 2 错误处理程序

<img src="README.assets/image-20220907200453951.png" alt="image-20220907200453951" style="zoom:67%;" />

### 3 错误恢复

<img src="README.assets/image-20220907200602095.png" alt="image-20220907200602095" style="zoom:67%;" />

> :star:错误处理这里有些不明白，需要进一步补充理解