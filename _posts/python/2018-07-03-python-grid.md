---
layout: blog
istop: false
background-image: http://www.cbdio.com/image/attachement/jpg/site2/20170810/f04da2247c301af63d0815.jpg
title: python-grid
date: 2018-07-03 01:14:31 +0800
category: tools
tags: 
- python
- grid
keywords: python
description: script by python
---

[On python, how to generate an array of coordinates between two points](https://gis.stackexchange.com/questions/167453/on-python-how-to-generate-an-array-of-coordinates-between-two-points)


[Create a polygon grid using with Geopandas](https://gis.stackexchange.com/questions/269243/create-a-polygon-grid-using-with-geopandas)

[Find index location of a lat/lon point on a raster grid in ArcPy](https://gis.stackexchange.com/questions/76781/find-index-location-of-a-lat-lon-point-on-a-raster-grid-in-arcpy)

[Get-grid-points-from-matplotlib](https://stackoverflow.com/questions/29493591/get-grid-points-from-matplotlib)


#
[Finding correct X Y values from two pairs of X Y map coordinates?](https://gis.stackexchange.com/questions/262503/finding-correct-x-y-values-from-two-pairs-of-x-y-map-coordinates)

```python
lat = 41.050
lon = -125.685
wind_lats = dataset.variables['lat'][:]
wind_lons = dataset.variables['lon'][:]
lat_idx = np.abs(wind_lats - lat).argmin()
lon_idx = np.abs(wind_lons - lon).argmin()
lat_idx = np.unravel_index(lat_idx, wind_lats.shape)
lon_idx = np.unravel_index(lon_idx, wind_lons.shape)
wind_lat_y = lat_idx[0]
wind_lat_x = lat_idx[1]
wind_lon_y = lon_idx[0]
wind_lon_x = lon_idx[1]

```
