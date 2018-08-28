---
layout: blog
book: true
istop: true
title: "Python Wind"
background-image: http://nbviewer.jupyter.org/github/jtpio/p5-jupyter-notebook/blob/master/img/python_viz_landscape.png
date:  2018-06-23 10:13:56
category: research
tags:
- research
- wind
- python
---

# python画风垂直切变填色图

```python
# -*- coding: utf-8 -*-
from mpl_toolkits.basemap import Basemap
import numpy as np
#from matplotlib import cm
import matplotlib.pyplot as plt
from matplotlib import colors
from netCDF4 import Dataset
import scipy.ndimage

xmin=40
xm=57
xmax=73
ymin=24
ymax=37
ny=13
nx=33
st=0
mt=48
et=97
nt=96
#读取数据计算垂直风切变
a=Dataset("D:\\cygwin\\cygdrive\\dachuang\\uv2.5.nc","r")
z1=0
z2=1
uwnd=a.variables['u']
uwnd1=uwnd[:,z1,:,:]
uwnd2=uwnd[:,z2,:,:]
vwnd=a.variables['v']
vwnd1=vwnd[:,z1,:,:]
vwnd2=vwnd[:,z2,:,:]

#计算垂直风切变
vsheer=np.sqrt((uwnd2-uwnd1)*(uwnd2-uwnd1)+(vwnd2-vwnd1)*(vwnd2-vwnd1))

vsheer1=vsheer[st:mt,:,:]
vsheer1=np.mean(vsheer1,axis=0)
vsheer2=vsheer[mt:et,:,:]
vsheer2=np.mean(vsheer2,axis=0)
vsheer3=(vsheer2-vsheer1)
vsheer3[vsheer3>=3]=0
vsheer3[vsheer3<=-2]=0
vsheer3=scipy.ndimage.gaussian_filter(vsheer3,1)

bidate=a.variables['time']
blat=a.variables['latitude'][:]
blon=a.variables['longitude'][:]
blons,blats=np.meshgrid(blon,blat)

ax=plt.subplot(1,1,1)
# setup mercator map projection.
m = Basemap(llcrnrlon=100.,llcrnrlat=0.,urcrnrlon=180.,urcrnrlat=30.,\
            rsphere=(6378137.00,6356752.3142),\
            resolution='l',projection='merc',\
            lat_0=15.,lon_0=140.,lat_ts=20.)
m.drawcoastlines(linewidth=0.3)
#m.fillcontinents(color='linen')

blonm,blatm=m(blons,blats)

#调色
#'#2F4F4F','#008080','#008B8B','#40E0D0','#00FFFF','#7FFFD4','#F0FFFF',
#'#F0FFFF','#FFFF00','#FFA500','#FF8C00','#FF4500','#FF0000'
#'#9400D3','#0000FF','#4169E1','#00BFFF',
cdict=['#008080','#40E0D0','#00FFFF','#FFFFFF',\
'#F0FFFF','#FFFF00','#FFA500','#FF8C00']
my_cmap=colors.ListedColormap(cdict,'indexed')
#cm.register_cmap(name ='dbzcmap',data = cdict,lut = 128)
# 注意：cpool中有15个颜色，但是只使用了10个，其余的会被忽略
# 具体可查阅matplotlib官方文档中对ListedColormap的说明

#lev=np.linspace(np.min(sst3),np.max(sst3),50)
#bounds=np.linspace(-3.2,2.4, 8, endpoint=True)
norm=colors.Normalize(vmin=-2.0,vmax=3)
cf=m.contourf(blonm,blatm,vsheer3,cmap=plt.cm.RdBu_r,norm=norm)
cb=m.colorbar(cf,"bottom",size="10%",pad=0.3,alpha=1,norm=norm)
#,ticks=bounds,boundaries=bounds)
#cb.set_ticks(np.arange(-1.2,2.8,0.4)) 
#cb.set_ticklabels(np.arange(-1.2,2.8,0.4))
#cbar = pyplot.colorbar(pp, orientation='vertical', ticks=np.arange(cbar_min, cbar_max+cbar_step, cbar_step), format=cbar_num_format)
m.drawparallels(np.arange(0,40,10),labels=[1,0,0,0],fontsize=10,linewidth=0.0,)
# draw meridians
m.drawmeridians(np.arange(100,220,20),labels=[0,0,0,1],fontsize=10,linewidth=0.0)
ax.set_title('Vms',loc='left')
plt.show()
```
