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
