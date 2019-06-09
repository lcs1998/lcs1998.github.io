---

layout:     post
title:      Number()、parseInt()与parseFloat()解析
subtitle:   js学习笔记（1）
date:       2019-05-21
author:     Jacob
header-img: img/post-bg-ios9-web.jpeg
catalog: true
tags:

    - JavaScript
    - 内置函数
---

# Number() 与 parseInt()解析

> 在 Python 中，将字符串转为整型变量的函数是 ```int()``` ，直接使用 ```int("123")```就可以得到 `123`的输出结果，这样可以比较快速的得到我们想要的结果，在 js 中将 string 类型 转为 number 类型的函数有三种， `Number()`、 `parseInt()` 和 `parseFloat()`。
>
> Number()可以用于任何数据类型，而另外两个则专门用于把字符串转换为数值，这三个函数对于同样的输入会有不一样的结果。

## 1.Number()

Number() 的转换规则如下：

+ 对于Boolean值，真返回 1，假返回 0

+ 如果是Number型数值，则输入与输出一致

+ 如果是 null 型，则会返回 0

+ 如果是 undefined ，则会返回 NaN（Not a Number）

+ 如果是字符串，则会满足一下规则：

  + 如果字符串中只包含数字（包括正负号的情况），则会将其转换为十进制数值，运行示例如下：

    ![1560098180459](https://github.com/lcs1998/lcs1998.github.io/blob/master/img/1560098180459.png?raw=true)

  + 如果字符串中包含浮点格式，则会输出浮点数

    ![1560098232457](https://github.com/lcs1998/lcs1998.github.io/blob/master/img/1560098232457.png?raw=true)

  + 如果字符串中包含有效的十六进制数值，则会输出相应的十进制数值

    ![1560098317302](https://github.com/lcs1998/lcs1998.github.io/blob/master/img/1560098317302.png?raw=true)

  + 如果字符串是空的，则将其转换为0

    ![1560098356513](https://github.com/lcs1998/lcs1998.github.io/blob/master/img/1560098356513.png?raw=true)

  + 除上述格式外，全部转为NaN

    ![1560098415580](https://github.com/lcs1998/lcs1998.github.io/blob/master/img/1560098415580.png?raw=true)

## 2.parseInt()

由于NUmber()函数在转换字符串时比较复杂，因此我们平时最常使用的还是 `parseInt()`函数。它会忽略字符串前面的空格，直到找到一个**非空格**字符串，如果第一个字符串**不为数字或者正负号**，则会返回**NaN**。如果第一个是数字字符或者正负号，会接着向下扫描，知道完成所有字符或者遇到一个**非数字字符**。

![1560098814334](https://github.com/lcs1998/lcs1998.github.io/blob/master/img/1560098814334.png?raw=true)

在**ECMAScript 5 JavaScript**引擎中，parseInt()已经**不具有解析八进制值**的能力，所以上述

```javascript
parseInt("070")
```

会输出 70

在 `parseInt()`可以指定第二个参数为进制数，如下所示：

![1560099051278](https://github.com/lcs1998/lcs1998.github.io/blob/master/img/1560099051278.png?raw=true)

## 3.parseFloat()

关于使用方法如下所示：

![1560099214446](https://github.com/lcs1998/lcs1998.github.io/blob/master/img/1560099214446.png?raw=true)

