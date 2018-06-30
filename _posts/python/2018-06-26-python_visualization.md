---
layout: blog
book: true
istop: true
title: "Python Visualization"
background-image: http://nbviewer.jupyter.org/github/jtpio/p5-jupyter-notebook/blob/master/img/python_viz_landscape.png
date:  2018-06-23 10:13:56
category: research
tags:
- research
- quickhtml
- python
---

python可视化库可以大致分为几类：
![picture](http://nbviewer.jupyter.org/github/jtpio/p5-jupyter-notebook/blob/master/img/python_viz_landscape.png)

> 基于matplotlib的可视化库
> 基于JS的可视化库
> 基于上述两者或其他组合功能的库

**[more detail](https://speakerdeck.com/jakevdp/pythons-visualization-landscape-pycon-2017?slide=36)**

[Overview of Python Visualization Tools](http://pbpython.com/visualization-tools-1.html)

----
# 速查
[python-graph-gallery](https://python-graph-gallery.com/)
![picture](https://python-graph-gallery.com/wp-content/uploads/Logo_PGG_full-3.jpg)

[unidata](http://unidata.github.io/python-gallery/examples/index.html) [Examples of GEMPAK Analysis and Display Capabilities](https://www.unidata.ucar.edu/software/gempak/examples/)

[国内首款-数据可视化参考手册：专业绘图必备](https://zhuanlan.zhihu.com/p/31210682)

[Visualising CMIP data](https://data-lessons.github.io/python-aos-lesson/02-visualisation/index.html)

[oceanpython](https://oceanpython.org/)
![pic2](https://oceanpython.files.wordpress.com/2013/03/glider_movie2.gif)

[domain](https://erikwk.wordpress.com/2011/03/31/plot-wrf-domains-in-google-earth/) : plot-wrf-domains-in-google-earth

[PyEarthScience](https://github.com/KMFleischer/PyEarthScience)

[earthpy](http://earthpy.org/category/data-processing.html)  [seaborn](http://earthpy.org/seaborn_library.html) [PyNGL](http://earthpy.org/komod-mitplot-drawmap.html) [CATEGORY](http://earthpy.org/category/visualization.html) [Basemap](http://earthpy.org/earthpy-basemap-amazon.html)

----
# 总结

## A-D

[altair](https://github.com/altair-viz/altair) : Declarative statistical visualization library for Python

**[Basemap](https://basemaptutorial.readthedocs.io/en/latest/index.html#)**

[Bokeh](http://bokeh.pydata.org/en/latest/) is an interactive visualization library that targets modern web browsers for presentation.一个用于做浏览器端交互可视化的库，实现分析师与数据的交互。[^Interactive] [ipynb](http://nbviewer.jupyter.org/github/bokeh/bokeh-notebooks/blob/master/index.ipynb)

[bqplot](https://github.com/bloomberg/bqplot) is a Grammar of Graphics-based interactive plotting framework for the Jupyter notebook

[cartopy](https://scitools.org.uk/cartopy/docs/latest/)
[cartopy-tutorial](https://github.com/nawendt/cartopy-tutorial) [jupyter](http://nbviewer.jupyter.org/gist/pelson) [climate06](python绘制地图的利器Cartopy使用说明)

[ccplot](http://ccplot.org/): CloudSat, CALIPSO and Aqua MODIS products[^SAT]

[CDAT](https://cdat.llnl.gov/) is a powerful and complete front-end to a rich set of visual-data exploration and analysis capabilities well suited for data analysis problems.[^3D]

[cis](http://cis.readthedocs.io/en/stable/gallery.html) : modis [^SAT] 

[CHIMPLOT](http://www.lmd.polytechnique.fr/chimplot/) [^MODEL]

[D3Py](https://github.com/mikedewar/d3py) :a plottling library for python, based on D3

[datamaps](http://datamaps.github.io/) : Customizable SVG map visualizations for the web in a single Javascript file using D3.js [^MAP]

## E-H

[Echarts](http://echarts.baidu.com/index.html) : BaiDu [^Interactive]

[folium](https://github.com/python-visualization/folium) [ipynb](http://nbviewer.jupyter.org/github/python-visualization/folium/tree/master/examples/) [ipynb2](https://nbviewer.jupyter.org/github/vincentropy/python_cartography_tutorial/tree/master/)[^MAP] 

[Geoplotlib](https://github.com/andrea-cuttone/geoplotlib) is a python toolbox for visualizing geographical data and making maps[^MAP]

[ggplot](http://ggplot.yhathq.com/)

[gmap](https://jupyter-gmaps.readthedocs.io/en/stable/) : is a plugin for Jupyter for embedding Google Maps in your notebooks. It is designed as a data visualization tool.[^MAP]

[gmtpython](https://www.gmtpython.xyz/latest/)

[gmplot](https://github.com/vgm64/gmplot)Plotting data on google maps, the easy (stupid) way.[^MAP]

[geopandas](http://geopandas.readthedocs.io/en/latest/) [^MAP]

[Highcharts](https://www.highcharts.com/) makes it easy for developers to set up interactive charts in their web pages [^Interactive]
## I-L

[igraph](http://igraph.org/python/)

**[iris](https://scitools.org.uk/iris/docs/latest/gallery.html)**

## M-O

[Mayavi](http://docs.enthought.com/mayavi/mayavi/) : 3D scientific data visualization and plotting in Python[^3D]

[matplot官方教學](https://matplotlib.org/tutorials/introductory/pyplot.html#sphx-glr-tutorials-introductory-pyplot-py)

[mapbox](https://www.mapbox.com/)[^MAP]

[Metpy](https://unidata.github.io/MetPy/latest/)[^MODEL]

**[MkMov](http://christopherbull.com.au/mkmov/index.html)** : make a **movie** from a NetCDF file or stitch together a series of *.png files. [^MODEL]

[mplleaflet](https://github.com/jwass/mplleaflet) [^MAP] **[SHOW](http://htmlpreview.github.io/?https://github.com/jwass/mplleaflet/master/examples/readme_example.html)**

*[networkx](https://networkx.github.io/)*

## P

[plotly官方教学](https://plot.ly/python/getting-started/)[^Interactive] [ipynb](http://nbviewer.jupyter.org/github/plotly/python-user-guide/blob/master/Index.ipynb)

[pyecharts](http://pyecharts.org/#/)是基于百度echarts的一个开源项目，也是我目前接触到的最容易实现交互可视化的工具，相比bokeh和plotly，pyecharts的语法更简单，实现效果更佳出众。

[pygal](http://pygal.org/en/stable/) : sexy python charting

*[pyqtgraph](http://www.pyqtgraph.org/)*

[paraview](https://www.paraview.org/) [pv_atmos for paraview](https://github.com/mjucker/pv_atmos)       [Cloud-resolving simulation over Germany using ICON HighRes](https://vimeo.com/156297434)

**[PyNGL](http://www.pyngl.ucar.edu/)** NCL [^MODEL]

**[PyNCplot](http://www.xn--llusfb-5va.cat/python/PyNCplot/)** for WRF trajectory [^MODEL]

**[PyWPS](http://birdhouse-workshop.readthedocs.io/en/latest/pywps/intro.html)** is a WPS implementation written in the Python language. The current version is 4.0.0.

[pyWRF](https://github.com/xigrug/pyWRF)is designed to read, process, and plot data from the Weather Research and Forecasting model. [^MODEL]

**[PyGEOMET](https://github.com/pygeomet/PyGEOMET)** : Python GUI of Earth Observations and Model Evaluation Toolkit like ncview

## Q-S

**[seaborn官方教学](http://seaborn.pydata.org/tutorial.html)**
**[SatPy](http://satpy.readthedocs.io/en/latest/overview.html)**

## T-V

*[VisPy](http://vispy.org/)* is a high-performance interactive 2D/3D data visualization library leveraging the computational power of modern Graphics Processing Units (GPUs) through the OpenGL library to display very large datasets.

*[vincent](https://github.com/wrobstory/vincent)* no more updates

*[VPython](http://www.glowscript.org/#/user/GlowScriptDemos/folder/Examples/): Easy-to-use 3-D visualization and animation environment*[^3D]

[Vapor-python](https://www.vapor.ucar.edu/docs/vapor-gui-general-guide/vapor-python-modules) [guide](https://test7.vapor.cms.ucar.edu/sites/default/files/VaporPythonGuide.pdf)[^3D]

## W-Z

**[WRF-Python](http://wrf-python.readthedocs.io/en/latest/plot.html)** [^MODEL]
**[Xarray](http://xarray.pydata.org/en/stable/plotting.html#maps)** [^MODEL]
----
# others

* [Igor](http://www.wavemetrics.com/)

* [Originlab](https://www.originlab.com/)

* [R ggplot2](https://ggplot2.tidyverse.org/)

[常用绘图、图片处理、截图工具](https://mp.weixin.qq.com/s?__biz=MzI5MzQzMjU4Mw==&mid=2247485324&idx=1&sn=2adf5b7136206aa409abcd39da084b0a&chksm=ec737be4db04f2f22dde63518803d8c663c2535033a685305b1d6ae1ad3aab93b10db9dbbdf0&scene=21#wechat_redirect)

# Color
[ColormapTransformations](http://scipy-cookbook.readthedocs.io/items/Matplotlib_ColormapTransformations.html)
----
[^MAP]: **地图可视化**
[^Interactive]: **交互式**
[^3D]: **3D**
[^SAT]: **SATELLITE**
[^MODEL]: **MODEL 模式**
