---
# Documentation: https://wowchemy.com/docs/managing-content/

title: "C语言数组和指针"
subtitle: ""
summary: " "
authors: [Rui Ying]
tags: [C]
categories: [C]
date: 2018-12-02T21:31:14Z
lastmod: 2018-12-02T21:31:14Z
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
## 数组名是常量，指针是变量

C语言中，数组和指针经常被混淆。如下一个例子:

```C
char ar[] = "ABC";
   const char *pt[] = "ABC";
```

他们的共同点在于，都可以进行基本的数组表示。

```C
for (i = 0; i < 3; i++)
    putchar(ar[i]); //or putchar(pt[i]);

```

或者进行指针加法操作：

```C
for (i = 0; i < 3; i++)
    putchar(*(ar+1)); //or putchar(*(pt[i]));
```

其实数组名的本质在于，他是数组首元素的地址*常量*，也就是一串十六进制的数值。所以它可以通过指针加法来表示下N个元素。
而指针的本质在于，它是某个变量（这里是一个字符串）的地址，是一个*变量*，所以它不但可以进行上述操作，还可以进行*递增*操作，例如pt++，或者展开来pt = pt +１。数组不能这样操作是因为它是不可变的。你可以用ar + n来表示其他元素，但你不能用ar++这样的形式。

## 初始化数组是cp, 初始化指针是mv

同样是上面的例子，ar和pt都指向“ABC”这个字符串。但是，事实上，用printf(%p)就可以试出来，pt指针是和"ABC"的地址是一样的，ar数组是和"ABC"的地址是不一样的。因为初始化数组是将静态存储区的字符串拷贝到数组中，而初始化指针只是把字符串的地址传递给指针。所以，初始化数组是进行创建副本，而初始化指针只是告诉你一个地址，没有进行字符串的移动。
可以看出来，指针是相对灵活的。但是，在某些时候也会造成错误。例如如果在表示字符串时，如果没有用const表示常量，就可能会字符串的地址造成修改，进而影响整个字符串代码。所以最好用const限定字符串常量。

## 参考资料

[1] C Primer Plus第六版
