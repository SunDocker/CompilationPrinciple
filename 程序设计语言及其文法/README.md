# 语言及其文法

## 基本概念

### 1 字母表及其运算

#### 1.1 字母表的概念

<img src="README.assets/image-20220902135103538.png" alt="image-20220902135103538" style="zoom:67%;" />

#### 1.2 乘积

<img src="README.assets/image-20220902135132768.png" alt="image-20220902135132768" style="zoom:67%;" />

#### 1.3 幂运算

<img src="README.assets/image-20220902135206084.png" alt="image-20220902135206084" style="zoom:67%;" />

#### 1.4 正闭包

<img src="README.assets/image-20220902135231066.png" alt="image-20220902135231066" style="zoom:67%;" />

#### 1.5 克林闭包

<img src="README.assets/image-20220902135309641.png" alt="image-20220902135309641" style="zoom:67%;" />

### 2 串及其运算

#### 2.1 串的概念

<img src="README.assets/image-20220902135345365.png" alt="image-20220902135345365" style="zoom:67%;" />

#### 2.2 连接和前后缀

<img src="README.assets/image-20220902135816252.png" alt="image-20220902135816252" style="zoom:67%;" />

#### 2.3 幂

<img src="README.assets/image-20220902135848222.png" alt="image-20220902135848222" style="zoom:67%;" />



## 文法的定义

> <img src="README.assets/image-20220902141610335.png" alt="image-20220902141610335" style="zoom:67%;" />

### 1 文法的形式化定义

#### 1.1 终结符

<img src="README.assets/image-20220902141650729.png" alt="image-20220902141650729" style="zoom:67%;" />

#### 1.2 非终结符

<img src="README.assets/image-20220902143041645.png" alt="image-20220902143041645" style="zoom:80%;" />

> <img src="README.assets/image-20220902143056149.png" alt="image-20220902143056149" style="zoom:80%;" />

#### 1.4 产生式

<img src="README.assets/image-20220902143134719.png" alt="image-20220902143134719" style="zoom:67%;" />

> <img src="README.assets/image-20220902143147530.png" alt="image-20220902143147530" style="zoom:67%;" />

#### 1.5 开始符号

<img src="README.assets/image-20220902143206746.png" alt="image-20220902143206746" style="zoom:80%;" />

> <img src="README.assets/image-20220902143246923.png" alt="image-20220902143246923" style="zoom:67%;" />

### 2 产生式的简写

<img src="README.assets/image-20220902143335398.png" alt="image-20220902143335398" style="zoom:80%;" />

> <img src="README.assets/image-20220902143346532.png" alt="image-20220902143346532" style="zoom:80%;" />

### 3 符号约定

终结符：

<img src="README.assets/image-20220902150841308.png" alt="image-20220902150841308" style="zoom:77%;" />

<img src="README.assets/image-20220902150952204.png" alt="image-20220902150952204" style="zoom:67%;" />

非终结符：

<img src="README.assets/image-20220902150859349.png" alt="image-20220902150859349" style="zoom:67%;" />

文法符号：

<img src="README.assets/image-20220902151304539.png" alt="image-20220902151304539" style="zoom:80%;" />

<img src="README.assets/image-20220902151318801.png" alt="image-20220902151318801" style="zoom:80%;" />

> <img src="README.assets/image-20220902152046489.png" alt="image-20220902152046489" style="zoom:80%;" />

## 语言的定义

> <img src="README.assets/image-20220902152920448.png" alt="image-20220902152920448" style="zoom:67%;" />

### 1 推导和归约

#### 1.1 推导

<img src="README.assets/image-20220902153011693.png" alt="image-20220902153011693" style="zoom:67%;" />

<img src="README.assets/image-20220902153028541.png" alt="image-20220902153028541" style="zoom:80%;" />

> <img src="README.assets/image-20220902153038714.png" alt="image-20220902153038714" style="zoom:67%;" />

#### 1.2 归约

<img src="README.assets/image-20220902153155305.png" alt="image-20220902153155305" style="zoom:67%;" />

> 回答前面的问题：
>
> <img src="README.assets/image-20220902153304034.png" alt="image-20220902153304034" style="zoom:67%;" />

### 2 句型和句子

<img src="README.assets/image-20220902153336910.png" alt="image-20220902153336910" style="zoom:80%;" />

<img src="README.assets/image-20220902153346189.png" alt="image-20220902153346189" style="zoom:80%;" />

> <img src="README.assets/image-20220902154054078.png" alt="image-20220902154054078" style="zoom:67%;" />

### 3 语言的形式化定义

<img src="README.assets/image-20220902154119493.png" alt="image-20220902154119493" style="zoom:67%;" />

> 文法解决了无穷语言的有穷表示问题

> 语言举例：
>
> <img src="README.assets/image-20220902154312219.png" alt="image-20220902154312219" style="zoom:67%;" />

### 4 语言上的运算

<img src="README.assets/image-20220902154355577.png" alt="image-20220902154355577" style="zoom:67%;" />

> <img src="README.assets/image-20220902154405005.png" alt="image-20220902154405005" style="zoom:80%;" />

## 文法的分类

### 0型文法

<img src="README.assets/image-20220902221231069.png" alt="image-20220902221231069" style="zoom:67%;" />

### 1型文法

<img src="README.assets/image-20220902221344606.png" alt="image-20220902221344606" style="zoom:67%;" />

> <img src="README.assets/image-20220902221353418.png" alt="image-20220902221353418" style="zoom:80%;" />
>
> 都要求$\alpha$中至少包含一个非终结符

### 2型文法

<img src="README.assets/image-20220902225359083.png" alt="image-20220902225359083" style="zoom:80%;" />

> <img src="README.assets/image-20220902225408580.png" alt="image-20220902225408580" style="zoom:80%;" />

<img src="README.assets/image-20220902225419823.png" alt="image-20220902225419823" style="zoom:67%;" />

### 3型文法

<img src="README.assets/image-20220902230545125.png" alt="image-20220902230545125" style="zoom:67%;" />

> <img src="README.assets/image-20220902230620818.png" alt="image-20220902230620818" style="zoom:67%;" />
>
> 用两种文法生成的标识符，当然还可以写一个左线性文法

<img src="README.assets/image-20220902230939396.png" alt="image-20220902230939396" style="zoom:67%;" />

### 四种文法之间的关系

<img src="README.assets/image-20220902230958751.png" alt="image-20220902230958751" style="zoom:67%;" />

