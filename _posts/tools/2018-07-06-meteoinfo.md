---
layout: blog
tools: true
title: "METEOINFO"
background-image: http://www.meteothinker.com/_static/logo.jpg
date:  2018-06-22 10:13:56
category: tools
tags:
- tools
- quickhtml
- NCL
- plot
---

**[METEOINFO](http://www.meteothinker.com/)** 官网


----

# **[脚本汇总贴](http://bbs.06climate.com/forum.php?mod=viewthread&tid=36151&extra=page%3D1)**

## 使用到的

[MeteoInfoLab脚本示例：绘制雷达反射率图](http://bbs.06climate.com/forum.php?mod=viewthread&tid=59768&extra=page%3D1)

[利用MeteoInfo中TrajStat插件做条件轨迹聚类分析](http://bbs.06climate.com/forum.php?mod=viewthread&tid=37332&extra=page%3D1)

[MeteoInfo脚本示例：移动轨迹](http://bbs.06climate.com/forum.php?mod=viewthread&tid=31797&extra=&page=1)

[MeteoInfo脚本教程（十四）：轨迹数据](http://bbs.06climate.com/forum.php?mod=viewthread&tid=31437&extra=page%3D2)
## 未解决问题

[求助hysplit中 聚类分析后比湿是如何得到的](http://bbs.06climate.com/forum.php?mod=viewthread&tid=24760&extra=page%3D1&page=1)

## 待学习

[trajstat做PSCF分析时按步骤操作遇到这个问题](http://bbs.06climate.com/forum.php?mod=viewthread&tid=61535&extra=page%3D2)
[PSCF Analysis](http://www.meteothinker.com/docs/trajstat/pscf.html)

[TrajStat做出的PSCF网格图形转成渐变色 ](http://bbs.06climate.com/forum.php?mod=viewthread&tid=31305&extra=page%3D1)

# metetoinfo 1.5

3D stem plot:
```python
z = linspace(0, 1, 100)
x = z * np.sin(20 * z)
y = z * np.cos(20 * z)
c = x + y

#Plot
ax = axes3d()
points, stemlines = ax.stem(x, y, z, c=c, edge=False, samestemcolor=True)
colorbar(stemlines,shrink=0.8)
title('Point 3D plot example')
```
![3dplot](http://www.meteothinker.com/_images/stem3_1.png)
![traj_plot](https://raw.githubusercontent.com/xigrug/xigrug.github.io/master/picture/traj_multi_color_plot.png)

## text
plotutil.py
![text_plot](https://raw.githubusercontent.com/xigrug/xigrug.github.io/master/picture/meteoinfo-text.png)
