---
layout: blog
tools: true
istop: false
title: "Python Satellite"
background-image: https://www.onlinebooksreview.com/uploads/blog_images/2017/11/08_Top+5+Libraries+for+Data+Science+in+Python.jpg
date:  2018-06-28 20:13:56
category: tools
tags:
- tools
- quickhtml
- python
- satellite
---


# 图片处理

## [cartopy](https://scitools.org.uk/cartopy/docs/latest/matplotlib/advanced_plotting.html?highlight=text)

```python
import os
import matplotlib.pyplot as plt

from cartopy import config
import cartopy.crs as ccrs


fig = plt.figure(figsize=(8, 12))

# get the path of the file. It can be found in the repo data directory.
fname = os.path.join(config["repo_data_dir"],
                     'raster', 'sample', 'Miriam.A2012270.2050.2km.jpg'
                     )
img_extent = (-120.67660000000001, -106.32104523100001, 13.2301484511245, 30.766899999999502)
img = plt.imread(fname)

ax = plt.axes(projection=ccrs.PlateCarree())
plt.title('Hurricane Miriam from the Aqua/MODIS satellite\n'
          '2012 09/26/2012 20:50 UTC')

# set a margin around the data
ax.set_xmargin(0.05)
ax.set_ymargin(0.10)

# add the image. Because this image was a tif, the "origin" of the image is in the
# upper left corner
ax.imshow(img, origin='upper', extent=img_extent, transform=ccrs.PlateCarree())
ax.coastlines(resolution='50m', color='black', linewidth=1)

# mark a known place to help us geo-locate ourselves
ax.plot(-117.1625, 32.715, 'bo', markersize=7, transform=ccrs.Geodetic())
ax.text(-117, 33, 'San Diego', transform=ccrs.Geodetic())

plt.show()
```
![pic1](https://scitools.org.uk/cartopy/docs/latest/_images/advanced_plotting-3.png)

[Web Map Tile Service time dimension demonstration](https://scitools.org.uk/cartopy/docs/latest/gallery/wmts_time.html?highlight=text)
![pic2](https://scitools.org.uk/cartopy/docs/latest/_images/sphx_glr_wmts_time_001.png)


