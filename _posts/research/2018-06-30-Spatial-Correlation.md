---
layout: blog
tools: true
istop: false
title: "Spatial Correlation"
background-image: 
date:  2018-06-26 10:13:56
category: research
tags:
- research
- correlation
- satellite
- web
---

# 相关研究

<a href="http://www.mdpi.com/2072-4292/8/11/914" title="Remote Sens. 2016, 8(11), 914; https://doi.org/10.3390/rs8110914">Spatial Correlation of Satellite-Derived PM2.5 with Hospital Admissions for Respiratory Diseases</a>  
![pic1](https://res.mdpi.com/def50200f7749950b21ad6cc54fef4e183a79ddfb032995b741860b42be54676a6d12c484d25dfe71f756fb7cd53a63143f542c7019977fec6df8f45541b35563b45b8a57beba310a0d58575be086624c7f9d6ef2b15f61b3b8c6f242d4b834d4ade6ce9d77fbbc34ead511fb19e006fa4ed3c7d5abff61575c70d9bdab67bc0d3a722c45c225d5b732121552cad0272b5cb78ca95027e458d311b43999f39ddcceacd23e0ef8d3dc1393ffb8aa7eead7e)

<a href="https://link.springer.com/chapter/10.1007/978-3-642-31137-6_39" title="Using Spatial Autocorrelation Techniques and Multi-temporal Satellite Data for Analyzing Urban Sprawl">Analyzing Urban Sprawl</a>

<a href="https://www.hydrol-earth-syst-sci.net/21/5987/2017/hess-21-5987-2017.pdf" title="Spatial pattern evaluation of a calibrated national hydrological model – a remote-sensing-based diagnostic approach">Spatial pattern evaluation</a>

# 讨论
<a href="https://www.researchgate.net/post/How_to_correlate_two_different_types_of_satellite_data_in_Erdas_or_ArcGIS" title="researchgate">How_to_correlate_two_different_types_of_satellite_data_in_Erdas_or_ArcGIS</a>

      Do you want to correlate pixel to pixel everyday? It is better if you could extract time series for selected pixel or location for both satellite products and do the correlation analysis. Some discussions are ++[here](http://gis.stackexchange.com/questions/91988/how-to-do-spatial-correlation-between-two-variables-on-arcgis-10-1)++

# 技术贴
[用geoda软件进行空间自相关分析示例](https://www.cnblogs.com/wicked-fly/p/6225002.html)
[空间自相关 (Global Morans I)](http://desktop.arcgis.com/zh-cn/arcmap/latest/tools/spatial-statistics-toolbox/spatial-autocorrelation.htm#S_GUID-275B0AA5-59CC-4A88-B84E-8E9F89F2C457)

[空间统计笔记之一(基础知识)](https://www.cnblogs.com/gisangela/archive/2012/10/22/2734176.html)

**[earthdatascience](https://www.earthdatascience.org/tutorials/)**

# 工具

> [GeoDa](https://spatial.uchicago.edu/software)
> [GeoDaSpace](https://geodacenter.github.io/GeoDaSpace/)
> [spvcm](https://github.com/ljwolf/spvcm/blob/master/spvcm/examples/using_the_sampler.ipynb)
> [CrimeStat](https://www.icpsr.umich.edu/CrimeStat/)

## R 语言

[Spatial-correlation-between-rasters Statnmap](https://statnmap.com/2018-01-27-spatial-correlation-between-rasters/)

[spatialEco](https://www.rdocumentation.org/packages/spatialEco/versions/1.1-0/topics/rasterCorrelation)

[Satellite Image Time Series Analysis](https://github.com/e-sensing/sits)

## Python 
[SPAtial EFficiency (SPAEF) – a new metric for pattern comparison](http://space.geus.dk/tools_products/index.html)
[github](https://github.com/cuneyd/spaef/tree/v1.0)

[Intro to Spatial Data Analysis in Python](https://2015.foss4g-na.org/sites/default/files/slides/Intro%20to%20Spatial%20Data%20Analysis%20in%20Python%20-%20FOSS4G%20NA%202015.pdf)
### PySal
[Moran’s I measures of spatial autocorrelation](http://pysal.readthedocs.io/en/latest/library/esda/moran.html) PySAL 

[How do I compute interactive spatial autocorrelation (Moran I) using PySAL?](https://stackoverflow.com/questions/45839957/python-how-do-i-compute-interactive-spatial-autocorrelation-moran-i-using-py)

[Geographic Data Science with PySAL and the pydata stack](http://darribas.org/gds_scipy16/)

[Exploratory Spatial Data Analysis -- ipynb](https://github.com/pysal/notebooks/blob/master/notebooks/PySAL_esda.ipynb)

### Scipy

[scipy.spatial.distance.correlation](https://docs.scipy.org/doc/scipy-0.14.0/reference/generated/scipy.spatial.distance.correlation.html)

#  Reprojection 

[MRT Modis Reprojection Toolbox](https://lpdaac.usgs.gov/tools/modis_reprojection_tool). It is a dos/unix based software which can be used in batch mode, which is a great assist while working with so many datasets. In MRT you can extract data in terms of bands (I guess you will need only NDVI and QA, so bands 1 and 12 respectively) as well as, spatial extend (if your area of interest is smaller than a MODIS tile). Data can be exported into several formats so you can go for one that suits you the most. Next, you can import these data to any other software, layerstack them into one-file time series and perform all desired analyses. 
[BfastSpatial package for R](https://dutri001.github.io/bfastSpatial/) which offers MODIS pre-processing functions which can be handy together with the MODIS or MODISTools package in R.

# Distance correlation

[Distance correlation with p-value](https://gist.github.com/wladston/c931b1495184fbb99bec)

# other question?

[How can I make linear regression across multiple raster layers?](https://www.researchgate.net/post/How_can_I_make_linear_regression_across_multiple_raster_layers)
[How to statistically compare two maps](https://www.researchgate.net/post/How_to_statistically_compare_two_maps)

[Introduction to spatial regression in Python](https://www.earthdatascience.org/tutorials/intro-to-spatial-regression/)
