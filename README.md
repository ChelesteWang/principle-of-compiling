# 编译原理期末复习

- - [第一章 概述][link 1]
  - - [1 一个典型的编译系统通常由哪些部分组成][1]
    - [2 编译程序前端包括……阶段？每部分的功能？][2]
  - [第二章][link 2]
  - - [1 基本概念][1 1]
    - [2 文法的二义性][2 1]
  - [第三章 词法分析][link 3]
  - [第四章 自顶向下语法分析法 \`推导\`][link 4]
  - - [1 文法的改写 LL(1)文法][1 _ ll_1]
    - [2 LL(1)文法的判定][2 ll_1]
    - [3 FIRST 集合 FOLLOW 集合][3 first_ follow]
    - [4 LL(1)预测分析表的构造][4 ll_1]
    - [5 对输入串的分析过程][5]
  - [第五章 自底向上优先分析 \`归约\`][link 5]
  - - [1 边移进边归约（可归约串）][1 2]
    - [2 规范归约][2 2]
    - [3 算法优先分析法：终结符号对的关系 \`大题\`][3 _]
  - [第八章 静态语义分析和中间代码生成][link 6]
  - - [1 中间代码形式][1 3]
    - [2 简单赋值语句的翻译][2 3]
    - [3 布尔表达式到四元式的翻译（求值/作为优化措施） \`大题\`][3 _ 1]

## 第一章 概述

### 1 一个典型的编译系统通常由哪些部分组成

![在这里插入图片描述](https://img-blog.csdnimg.cn/20200826173617960.png#pic_center)

### 2 编译程序前端包括……阶段？每部分的功能？

词法分析 ：从左到右一个字符一个字符地读入源程序，对构成源程序的字符流进行扫码和分解，从而识别出一个个单词  
语法分析 ：在词法分析基础上，将单词符号串转化为语法单位（语法范畴） （短语 子句 句子 程序段 程序），并确定整个输入串是否构成语法上正确的程序  
语义分析 ：对语法分析识别出各类语法范畴，分析其含义，并进行初步翻译（产生中间代码）  
中间代码生成：编译程序将源程序变成一个内部表示形式  
代码优化 ：对于代码（主要是中间代码）进行加工变换，以期能够产生更为高效（省时间和空间）的目标代码  
目标代码生成： 将中间代码变换成特定机器上的低级语言代码  
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200826174628364.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L2hlenVpaml1ZGV4aWFvYmFp,size_16,color_FFFFFF,t_70#pic_center)

## 第二章

### 1 基本概念

`语言`：  
语法：对语言结构的定义(是一组规则，定义符号如何排列，排列与符 号含义无关）  
语义：描述语言的含义（研究语法的含义）  
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200902165507667.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L2hlenVpaml1ZGV4aWFvYmFp,size_16,color_FFFFFF,t_70#pic_center)

句型  
句子  
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200902165304289.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L2hlenVpaml1ZGV4aWFvYmFp,size_16,color_FFFFFF,t_70#pic_center)

文法的组成 文法 G 定义为四元组（VN，VT，P，S）  
![在这里插入图片描述](https://img-blog.csdnimg.cn/2020090216485444.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L2hlenVpaml1ZGV4aWFvYmFp,size_16,color_FFFFFF,t_70#pic_center)

文法的类型  
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200826210957839.png#pic_center)  
文法：语言的形式化描述方法，是阐述语法的一个工具  
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200902165034202.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L2hlenVpaml1ZGV4aWFvYmFp,size_16,color_FFFFFF,t_70#pic_center)

![在这里插入图片描述](https://img-blog.csdnimg.cn/20200902165018733.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L2hlenVpaml1ZGV4aWFvYmFp,size_16,color_FFFFFF,t_70#pic_center)

直接推导  
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200902165108986.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L2hlenVpaml1ZGV4aWFvYmFp,size_16,color_FFFFFF,t_70#pic_center)  
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200902165137355.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L2hlenVpaml1ZGV4aWFvYmFp,size_16,color_FFFFFF,t_70#pic_center)  
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200902165218560.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L2hlenVpaml1ZGV4aWFvYmFp,size_16,color_FFFFFF,t_70#pic_center)

多步推导  
最左推导  
最右推导（规范推导）  
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200902165644895.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L2hlenVpaml1ZGV4aWFvYmFp,size_16,color_FFFFFF,t_70#pic_center)  
语法树  
子树：任一结点及其全部后继  
直接子树（树高为 1）：一子树根只有直接后继  
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200902165857243.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L2hlenVpaml1ZGV4aWFvYmFp,size_16,color_FFFFFF,t_70#pic_center)  
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200902165911260.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L2hlenVpaml1ZGV4aWFvYmFp,size_16,color_FFFFFF,t_70#pic_center)

![在这里插入图片描述](https://img-blog.csdnimg.cn/20200902165815595.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L2hlenVpaml1ZGV4aWFvYmFp,size_16,color_FFFFFF,t_70#pic_center)

### 2 文法的二义性

L(G)的某个子句不只一个最左/最右推导  
如果一个文法存在某个句子对应两棵不同的语法树，则说这个文法是二义的  
若一个文法中存在某个句子，它有两个不同的最左（最右）推导，则这个文法是二义的  
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200826205818570.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L2hlenVpaml1ZGV4aWFvYmFp,size_16,color_FFFFFF,t_70#pic_center)  
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200826205843244.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L2hlenVpaml1ZGV4aWFvYmFp,size_16,color_FFFFFF,t_70#pic_center)  
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200826210023652.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L2hlenVpaml1ZGV4aWFvYmFp,size_16,color_FFFFFF,t_70#pic_center)

## 第三章 词法分析

词法分析的任务：识别单词  
(输出形式) 词法分析器的输出结果：单词种别和属性二元组

## 第四章 自顶向下语法分析法 `推导`

语法分析的任务：识别句子 根据产生式识别输入串是否为一个句子  
自顶向下语法分析受上下文无关文法影响

自上而下语法分析器，从文法的开始符号出发，反复使用文法的产生式，建立与输入符号串匹配最左推导

### 1 文法的改写 LL(1)文法

左递归的消除 转换为右递归（消除循环）

![在这里插入图片描述](https://img-blog.csdnimg.cn/2020090217361823.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L2hlenVpaml1ZGV4aWFvYmFp,size_16,color_FFFFFF,t_70#pic_center)  
\#1 消除直接左递归

![在这里插入图片描述](https://img-blog.csdnimg.cn/20200902173723199.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L2hlenVpaml1ZGV4aWFvYmFp,size_16,color_FFFFFF,t_70#pic_center)  
\#2 消除间接做左递归（代入法）  
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200902173921481.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L2hlenVpaml1ZGV4aWFvYmFp,size_16,color_FFFFFF,t_70#pic_center)  
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200902182803315.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L2hlenVpaml1ZGV4aWFvYmFp,size_16,color_FFFFFF,t_70#pic_center)

提取公共左因子  
消去回溯  
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200902174243417.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L2hlenVpaml1ZGV4aWFvYmFp,size_16,color_FFFFFF,t_70#pic_center)

### 2 LL(1)文法的判定

![在这里插入图片描述](https://img-blog.csdnimg.cn/20200902174423648.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L2hlenVpaml1ZGV4aWFvYmFp,size_16,color_FFFFFF,t_70#pic_center)  
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200902174432475.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L2hlenVpaml1ZGV4aWFvYmFp,size_16,color_FFFFFF,t_70#pic_center)

![在这里插入图片描述](https://img-blog.csdnimg.cn/20200902174403323.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L2hlenVpaml1ZGV4aWFvYmFp,size_16,color_FFFFFF,t_70#pic_center)

![在这里插入图片描述](https://img-blog.csdnimg.cn/20200902174330393.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L2hlenVpaml1ZGV4aWFvYmFp,size_16,color_FFFFFF,t_70#pic_center)

### 3 FIRST 集合 FOLLOW 集合

![在这里插入图片描述](https://img-blog.csdnimg.cn/20200826221837281.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L2hlenVpaml1ZGV4aWFvYmFp,size_16,color_FFFFFF,t_70#pic_center)  
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200826221805240.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L2hlenVpaml1ZGV4aWFvYmFp,size_16,color_FFFFFF,t_70#pic_center)

### 4 LL(1)预测分析表的构造

![在这里插入图片描述](https://img-blog.csdnimg.cn/20200902174552902.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L2hlenVpaml1ZGV4aWFvYmFp,size_16,color_FFFFFF,t_70#pic_center)

### 5 对输入串的分析过程

例题  
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200902175223794.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L2hlenVpaml1ZGV4aWFvYmFp,size_16,color_FFFFFF,t_70#pic_center)  
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200902175312295.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L2hlenVpaml1ZGV4aWFvYmFp,size_16,color_FFFFFF,t_70#pic_center)  
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200902175330729.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L2hlenVpaml1ZGV4aWFvYmFp,size_16,color_FFFFFF,t_70#pic_center)

## 第五章 自底向上优先分析 `归约`

从输入串开始，逐步进行“归约”，直至归约到文法的开始符号

### 1 边移进边归约（可归约串）

各种不同的自下而上分析法的一个共同特点是“边输入单词符号（移进符号栈），边规约”

### 2 规范归约

短语:每颗子树的叶子  
直接短语：每颗直接子树的叶子  
句柄：某句型的最左直接短语（即规范分析中最先被归约的子串）  
规范（最右）推导  
规范归约（最左归约）  
最右推导的逆过程  
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200902210348659.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L2hlenVpaml1ZGV4aWFvYmFp,size_16,color_FFFFFF,t_70#pic_center)

![在这里插入图片描述](https://img-blog.csdnimg.cn/20200902210316954.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L2hlenVpaml1ZGV4aWFvYmFp,size_16,color_FFFFFF,t_70#pic_center)  
素短语：至少包含一个终结符且不包含更小素短语的短句  
最左素短语

### 3 算法优先分析法：终结符号对的关系 `大题`

FIRSTVT LASTVT 集合的构造  
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200902210438951.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L2hlenVpaml1ZGV4aWFvYmFp,size_16,color_FFFFFF,t_70#pic_center)

构造算法优先关系表  
判断算法优先文法  
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200826214429943.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L2hlenVpaml1ZGV4aWFvYmFp,size_16,color_FFFFFF,t_70#pic_center)  
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200902210617235.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L2hlenVpaml1ZGV4aWFvYmFp,size_16,color_FFFFFF,t_70#pic_center)

## 第八章 静态语义分析和中间代码生成

### 1 中间代码形式

逆波兰式  
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200902210703460.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L2hlenVpaml1ZGV4aWFvYmFp,size_16,color_FFFFFF,t_70#pic_center)  
![在这里插入图片描述](https://img-blog.csdnimg.cn/2020090221071326.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L2hlenVpaml1ZGV4aWFvYmFp,size_16,color_FFFFFF,t_70#pic_center)  
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200902210727974.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L2hlenVpaml1ZGV4aWFvYmFp,size_16,color_FFFFFF,t_70#pic_center)

三元式  
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200902210746740.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L2hlenVpaml1ZGV4aWFvYmFp,size_16,color_FFFFFF,t_70#pic_center)  
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200902210759134.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L2hlenVpaml1ZGV4aWFvYmFp,size_16,color_FFFFFF,t_70#pic_center)

四元式（三地址代码）  
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200902210818315.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L2hlenVpaml1ZGV4aWFvYmFp,size_16,color_FFFFFF,t_70#pic_center)  
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200902210828512.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L2hlenVpaml1ZGV4aWFvYmFp,size_16,color_FFFFFF,t_70#pic_center)  
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200902210835976.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L2hlenVpaml1ZGV4aWFvYmFp,size_16,color_FFFFFF,t_70#pic_center)

### 2 简单赋值语句的翻译

理解语法制导翻译的方法

### 3 布尔表达式到四元式的翻译（求值/作为优化措施） `大题`

![在这里插入图片描述](https://img-blog.csdnimg.cn/20200902210907906.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L2hlenVpaml1ZGV4aWFvYmFp,size_16,color_FFFFFF,t_70#pic_center)  
1️⃣ 求值 E1 rop E2 4 条语句  
2️⃣ 采用优化措施  
困难：转移的目标在对它的应用之后才出现  
解决方法：拉链-返填法

[link 1]: #__2
[1]: #1__3
[2]: #2__5
[link 2]: #_14
[1 1]: #1__15
[2 1]: #2__52
[link 3]: #__61
[link 4]: #___65
[1 _ ll_1]: #1__LL1_70
[2 ll_1]: #2_LL1_86
[3 first_ follow]: #3_FIRST_FOLLOW_94
[4 ll_1]: #4_LL1_98
[5]: #5__100
[link 5]: #___108
[1 2]: #1__110
[2 2]: #2__112
[3 _]: #3___124
[link 6]: #__134
[1 3]: #1__135
[2 3]: #2__150
[3 _ 1]: #3___153
