---
layout: blog
book: true
title: "Python Visualization BUG"
background-image: http://nbviewer.jupyter.org/github/jtpio/p5-jupyter-notebook/blob/master/img/python_viz_landscape.png
date:  2018-07-07 17:03:56
category: research
tags:
- research
- quickhtml
- python
---
遇到的错误总结

Basemap 的坐标设置起点并不是坐标原点

m = Basemap(width=8000000,height=7000000,
            resolution='l',projection='aea',\
            lat_1=0.,lat_2=40,lon_0=110,lat_0=20)

mmb = m.pcolormesh(gx, gy, img1, cmap=cmap, norm=norm)

