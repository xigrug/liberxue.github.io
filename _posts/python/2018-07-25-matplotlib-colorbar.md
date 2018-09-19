---
layout: blog
book: true
title: "Matplotlib colorbar"
background-image: https://matplotlib.org/_static/logo2.png 
date:  2018-07-25 17:00:00
category: python
tags:
- matplotlib
- python
- color
---
[matplotlib colorbar placement and size](https://stackoverflow.com/questions/16702479/matplotlib-colorbar-placement-and-size)

|[Property](https://matplotlib.org/api/colorbar_api.html) |Description |
| --------   | :-----  | 
|orientation |	vertical or horizontal|
|fraction|	0.15; fraction of original axes to use for colorbar|
|pad|	0.05 if vertical, 0.15 if horizontal; fraction of original axes between colorbar and new image axes|
|shrink|	1.0; fraction by which to multiply the size of the colorbar|
|aspect|	20; ratio of long to short dimensions|
|anchor|	(0.0, 0.5) if vertical; (0.5, 1.0) if horizontal; the anchor point of the colorbar axes|
|panchor|	(1.0, 0.5) if vertical; (0.5, 0.0) if horizontal; the anchor point of the colorbar parent axes. If False, the parent axes’ anchor will be unchanged|

[Python Matplotlib: Change Colorbar Tick Width [duplicate]](https://stackoverflow.com/questions/19549243/python-matplotlib-change-colorbar-tick-width)
![pic1](https://i.imgur.com/kFOnkED.png)

[Set Matplotlib colorbar size to match graph](https://stackoverflow.com/questions/18195758/set-matplotlib-colorbar-size-to-match-graph)
```python
plt.colorbar(im,fraction=0.046, pad=0.04)
```

[matplotlib contour plot with lognorm - colorbar levels](https://stackoverflow.com/questions/17951672/matplotlib-contour-plot-with-lognorm-colorbar-levels)
```python
import matplotlib.pyplot as plt
import numpy as np
from matplotlib.colors import LogNorm
delta = 0.025

x = y = np.arange(0, 3.01, delta)
X, Y = np.meshgrid(x, y)
Z1 = plt.mlab.bivariate_normal(X, Y, 1.0, 1.0, 0.0, 0.0)
Z2 = plt.mlab.bivariate_normal(X, Y, 1.5, 0.5, 1, 1)
Z = 10 * (Z1* Z2)

fig=plt.figure()
ax1 = fig.add_subplot(111)
lvls = np.logspace(-4,0,20)
CF = ax1.contourf(X,Y,Z,
         norm = LogNorm(),
         levels = lvls
        )
CS = ax1.contour(X,Y,Z,
         norm = LogNorm(),
         colors = 'k',
         levels = lvls
        )
cbar = plt.colorbar(CF, ticks=lvls, format='%.4f')
plt.show()
```
![](https://i.stack.imgur.com/WJJcd.png)
