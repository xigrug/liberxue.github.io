---
layout: blog
book: true
istop: true
title: "Python Moviepy"
background-image: http://nbviewer.jupyter.org/github/jtpio/p5-jupyter-notebook/blob/master/img/python_viz_landscape.png
date:  2018-08-05 10:13:56
category: research
tags:
- research
- movie
- python
---

# [用Python和MoviePy将数据动态可视化](http://python.jobbole.com/81185/)

## 用Matplotlib的动画
2D/3D绘图库Matplotlib已经有了动画模块，但我发现moviepy可以做出更轻量级，质量更好的视频，却达到了两倍的速度（不知道为什么？在这里看到更多细节）。这里有个如何使用matplotlib和moviepy的例子

```python
import matplotlib.pyplot as plt
import numpy as np
from moviepy.video.io.bindings import mplfig_to_npimage
import moviepy.editor as mpy
 
# DRAW A FIGURE WITH MATPLOTLIB
 
duration = 2
 
fig_mpl, ax = plt.subplots(1,figsize=(5,3), facecolor='white')
xx = np.linspace(-2,2,200) # the x vector
zz = lambda d: np.sinc(xx**2)+np.sin(xx+d) # the (changing) z vector
ax.set_title("Elevation in y=0")
ax.set_ylim(-1.5,2.5)
line, = ax.plot(xx, zz(0), lw=3)
 
# ANIMATE WITH MOVIEPY (UPDATE THE CURVE FOR EACH t). MAKE A GIF.
 
def make_frame_mpl(t):
    line.set_ydata( zz(2*np.pi*t/duration))  # <= Update the curve
    return mplfig_to_npimage(fig_mpl) # RGB image of the figure
 
animation =mpy.VideoClip(make_frame_mpl, duration=duration)
animation.write_gif("sinc_mpl.gif", fps=20)
```

![1](http://ww2.sinaimg.cn/mw690/6941baebgw1eq9lywi411g20b406o40z.gif)
