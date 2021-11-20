---
# Documentation: https://wowchemy.com/docs/managing-content/

title: "C语言预处理"
subtitle: ""
summary: " "
authors: [Rui Ying]
tags: [C]
categories: [C]
date: 2018-12-06T12:02:48Z
lastmod: 2018-12-06T12:02:48Z
featured: false
draft: false

# Featured image
# To use, add an image named `featured.jpg/png` to your page's folder.
# Focal points: Smart, Center, TopLeft, Top, TopRight, Left, Right, BottomLeft, Bottom, BottomRight.
image:
  caption: ""
  focal_point: ""
  preview_only: false

# Projects (optional).
#   Associate this post with one or more of your projects.
#   Simply enter your project's folder or file name without extension.
#   E.g. `projects = ["internal-project"]` references `content/project/deep-learning/index.md`.
#   Otherwise, set `projects = []`.
projects: []
---
# C语言预处理

C的编译过程分为三步。以hello.c为例子，从源代码.c到可执行文件（如windows下的.exe）的过程是：

| 过程               | 名称     | GCC代码        | 作用                     |
| ------------------ | -------- | -------------- | ------------------------ |
| hello.c -> hello.i | 预处理   | gcc -E hello.c | 预处理头文件及宏         |
| hello.i -> hello.s | 编译     | gcc -S hello.i | 转为汇编代码             |
| hello.s -> hello.o | 汇编处理 | gcc -C hello.s | 转为机器码，生成目标文件 |
| hello.o -> hello   | 链接     | gcc  hello.o   | 生成可执行文件           |

C语言预处理是编译过程的第一步，将源文件.c处理为.i文件。其中预处理就包括对#define指令的翻译。

\#define语句不是专属于C语言的语句，它是一个宏。而宏是完全的*文本替换*。  
所以/#define不用分号结束语句，换行时要使用'/'。  
\#define宏因此也可以用作定义函数。所有参数和整体都要带括号，因为替换中可能会出现意外的运算顺序错误。  
\#运算符的作用是将变量转化为字符串。如`#x == "x"`。  
\#\#运算符就是一个黏合剂，如`x ## 2 == x2`  
预处理也会处理#include头文件，也就是插入一些.head文件。在\#include .h的时候常常可能造成重复声明，所以可以通过\#ifndef, \#define, \#endif 这3个语句来进行检验。
