---
# Documentation: https://wowchemy.com/docs/managing-content/

title: "C语言字符串IO"
subtitle: ""
summary: " "
authors: [Rui Ying]
tags: [C]
categories: [C]
date: 2018-12-03T11:17:41Z
lastmod: 2018-12-03T11:17:41Z
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
## 1. 字符串输入

C语言本质上也是一种面向用户的程序，所以必须把尽可能多的细节告诉它。

例如，在处理字符串输入的时候，我们必须先告诉它需要多少空间。所以，下面这种情况就是错误的。

```c
char *name;
scanf("%s", name);
```

### 1.1 gets()函数

gets()的用法非常简单

```c
char words[SIZE];
get(words);
```

像上面的两段式就能实现读取输入：先指定大小，再获取输入。**gets()会读取整行然后丢弃\n换行符，并且在字符串末尾添加\0空字符**。

但是**gets()已经被废除**， 因为它有致命的缺陷，就是他无法检查数组是否装得下输入行。如果输入字符串过长，那么会导致缓冲区溢出，造成安全问题。

### 1.2 fgets()函数

 fgets()函数被用来替代gets，但是它的参数有3个。

```c
fgets( string, SIZE, stdin)
```

3个参数分别为字符串变量，字符串容量大小，标准输入的意思。

与之对应的，是fputs函数

``` c
fputs(string, stdout)
```

参数和上面类似，stdout代表标准输出。

fgets与gets的区别有主要几点：

* fgets限制读入字符数，读入size - 1的字符（最后一个为\0），或者到遇到第一个换行符为止
* fgets会存储换行符，gets会丢弃换行符

同样地，puts函数也会在末尾添加一个换行符（换行符真的是C语言最繁琐的地方之一）。

当你想用fgets()舍弃换行符的时候，可以采取

```c
while (words[i] != '\n')
 i++;
words[i] = '\0'; //用空字符替代换行符
//或者丢弃换行符后面的字符
/*
while (getchar() != '\n')
 continue;
*/
```

## 2. 字符串输出

### 2.1 puts()函数

puts函数很常用，但是要知道它的几个特性

* puts会在末尾添加换行符
* puts必须要看到 \0才知道停止

### 2.2 fputs()函数

与puts不同，fputs不会在输出末尾添加换行符。

### 2.3 printf()函数

无需多言，可以格式化不同的数据类型，也不会自作主张添加换行符。

## 3. 总结

| 换行处理 | 输入    | 输出            |
| -------- | ------- | --------------- |
| 丢弃     | gets()  | fputs, printf() |
| 保留     | fgets() | puts            |

## 4. 参考资料

[1] C Primer Plus
