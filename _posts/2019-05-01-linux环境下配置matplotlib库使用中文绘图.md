---

layout:     post
title:      Liunx环境下配置matplotlib库使用中文绘图
subtitle:   更新.....
date:       2019-05-01
author:     Lcs
header-img: img/post-bg-ios9-web.jpeg
catalog: true
tags:

    - Liunx
    - Python
    - matplotlib
---

# Liunx环境下配置matplotlib库使用中文绘图

最近在使用matplotlib库的过程中需要用到中文绘图，在网上找了好多种方法，最终用一种方法解决了，在此记录。

首先Linux是有自己的中文字体的，叫做"Droid Sans Fallback"，我们可以直接使用它作为全局字体。在python文件中新建一个文件设置字体

```python
def conf_zh(font_name):
    from pylab import mpl
    mpl.rcParams['font.sans-serif'] = [font_name]
    mpl.rcParams['axes.unicode_minus'] = False 
```

新建玩之后在主函数调用，调用方法如下：

```
if __name__ == "__main__":
    conf_zh("Droid Sans Fallback")
    t = arange(-5*pi, 5*pi, 0.001)
    y = sin(t)/t
    plt.plot(t, y)
    plt.title("你好")
    plt.show()
```

使用此方法可以调用中文字体进行绘图