---
layout: blog
book: true
title: "Python FLEXPART"
background-image: http://bbs.06climate.com/forum.php?mod=attachment&aid=NTA0MzB8MjYzNGVkZGZ8MTUzMjM5OTQzMXw2MjUxfDQyNzQz&noupdate=yes 
date:  2018-07-07 17:03:56
category: research
tags:
- tools
- python
- flexpart
---

This programme was written by Lintao Li around 2014-8-20, for analyzing the out put of FLEXPART

Li, L., A. Dolman, and Z. Xu, 2015: Atmospheric moisture sources, paths, and the 
quantitative importance to the Eastern Asian Monsoon region. J. Hydrometeor. 
doi:10.1175/JHM-D-15-0082.1

[聚类轨迹图](http://bbs.06climate.com/forum.php?mod=viewthread&tid=42743&extra=&page=1)

```python
import matplotlib
import matplotlib.lines as mlines
matplotlib.use('Agg')
import numpy as np
from mpl_toolkits.basemap import Basemap, cm
import matplotlib.pyplot as plt
import FortFlex as ff
import pflexible as pf
import os
import cPickle as pickle  #1000 times faster than pickle!
import matplotlib.gridspec as gridspec
n=8000
print 'data reading'
data_file=os.path.join('/home/lintaoli/dealwith-output', '200901-pick-1000')
f=open(data_file, 'r+b', True)
y=pickle.load(f)
lon = y['longitude']
lat = y['latitude']
print 'data reading finished'
plt.figure(figsize=(30, 30))

width = 15000000; height=8000000; lon_0 = 62; lat_0 = 40
m = Basemap(width=width,height=height,projection='aeqd',lat_0=lat_0,lon_0=lon_0)
s=m.readshapefile('/home/lintaoli/try/bou2_4m/bou2_4l', 'provinces')
for j in  xrange(n):
  xi, yi = m(lon[:, j], lat[:, j])
  im1 = m.plot(xi, yi, color='lightgray', alpha=0.06) #we can specify the color degree of trajectories by adjusting the value of q


m.drawcoastlines(linewidth=0.5)
m.drawcountries()
m.drawparallels(np.arange(-80,81,20), labels=[0, 1, 0, 0], fontsize=40)
m.drawmeridians(np.arange(-180,180,20), labels= [1, 0, 0, 1], fontsize=40)
#f.close
############################################################
filename = os.path.join('/home/lintaoli/dealwith-output/cluster-winter', 'winter-cluster-mean')
f=open(filename, 'r+b', True)
y=pickle.load(f)
f.close

for i in xrange(78):
  xi, yi = m(y['westerly_lon'][0, i:i+2], y['westerly_lat'][0, i:i+2]) 
  z= 1000*(y['westerly_Humidity'][0, i] + y['westerly_Humidity'][0, i+1])/2    # convert the unit from kg/kg to g/kg
  if z<=0.8:
    c=(1.,0.,0.)
  if 0.8<z<=1.0:
    c=(1.,0.5,0.)    
  if 1.0<z<=1.5:
    c=(1., 0.95, 0.)
  if 1.5<z<=2.0:
    c=(0.5, 1., 0.)
  if 2.0<z<=3.0:
    c= (0., 0.8, 1.)
  if 3.0<z<=4.0:
    c=(0., 0.3, 1.)
  if z > 4.0:
    c= (0., 0., 0.5)
  im1 = m.plot(xi, yi, color= c, alpha=1., linewidth=y['n_westerly']/50000.)  #we can specify the color of trajectories by the value of q

for i in xrange(78):
  xi, yi = m(y['easterly_lon'][0, i:i+2], y['easterly_lat'][0, i:i+2]) 
  z= 1000*(y['easterly_Humidity'][0, i] + y['easterly_Humidity'][0, i+1])/2    # convert the unit from kg/kg to g/kg
  if z<=0.8:
    c=(1.,0.,0.)
  if 0.8<z<=1.0:
    c=(1.,0.5,0.)    
  if 1.0<z<=1.5:
    c=(1., 0.95, 0.)
  if 1.5<z<=2.0:
    c=(0.5, 1., 0.)
  if 2.0<z<=3.0:
    c= (0., 0.8, 1.)
  if 3.0<z<=4.0:
    c=(0., 0.3, 1.)
  if z > 4.0:
    c= (0., 0., 0.5)
  im1 = m.plot(xi, yi, color= c, alpha=1., linewidth=y['n_easterly']/20000.)  #we can specify the color of trajectories by the value of q

for i in xrange(78):
  xi, yi = m(y['north_continent_lon'][0, i:i+2], y['north_continent_lat'][0, i:i+2]) 
  z= 1000*(y['north_continent_Humidity'][0, i] + y['north_continent_Humidity'][0, i+1])/2      # convert the unit from kg/kg to g/kg
  if z<=0.8:
    c=(1.,0.,0.)
  if 0.8<z<=1.0:
    c=(1.,0.5,0.)    
  if 1.0<z<=1.5:
    c=(1., 0.95, 0.)
  if 1.5<z<=2.0:
    c=(0.5, 1., 0.)
  if 2.0<z<=3.0:
    c= (0., 0.8, 1.)
  if 3.0<z<=4.0:
    c=(0., 0.3, 1.)
  if z > 4.0:
    c= (0., 0., 0.5)
  im1 = m.plot(xi, yi, color= c, alpha=1., linewidth=y['n_north_continent']/20000.)  #we can specify the color of trajectories by the value of q

for i in xrange(78):
  xi, yi = m(y['else_lon'][0, i:i+2], y['else_lat'][0, i:i+2]) 
  z= 1000*(y['else_Humidity'][0, i] + y['else_Humidity'][0, i+1])/2
  if z<=0.8:
    c=(1.,0.,0.)
  if 0.8<z<=1.0:
    c=(1.,0.5,0.)    
  if 1.0<z<=1.5:
    c=(1., 0.95, 0.)
  if 1.5<z<=2.0:
    c=(0.5, 1., 0.)
  if 2.0<z<=3.0:
    c= (0., 0.8, 1.)
  if 3.0<z<=4.0:
    c=(0., 0.3, 1.)
  if z > 4.0:
    c= (0., 0., 0.5)
  im1 = m.plot(xi, yi, color= c, alpha=1., linewidth=y['n_else']/20000.)  #we can specify the color 
  
########### plot legend ##############

leg_1, = plt.plot([1,2,3], color=(1.,0.,0.), label='RH <= 0.5')
leg_2, = plt.plot([1,2,3], color=(1.,0.5,0.), label='0.5<RH<=1')
leg_3, = plt.plot([1,2,3], color=(1., 0.95, 0.), label='1<RH<=5')
leg_4, = plt.plot([1,2,3], color=(0.5, 1., 0.), label='1<RH<=5')
leg_5, = plt.plot([1,2,3], color=(0., 0.8, 1.), label='5<RH<=10')
leg_6, = plt.plot([1,2,3], color=(0., 0.3, 1.), label='10<RH<=15')
leg_7, = plt.plot([1,2,3], color=(0., 0., 0.5), label='RH > 15')

leg = plt.legend([leg_1, leg_2, leg_3, leg_4, leg_5, leg_6, leg_7], ['q <= 0.8', '0.8<q<=1', '1 <q<=1.5', '1.5<q<=2', '2 <q<=3', '3 <q<=4', 'q > 4'],
           loc=3, prop={'size': 40})

# set the linewidth of each legend object
for legobj in leg.legendHandles:
  legobj.set_linewidth(8.0)

###########################################################
outname='%s.png'%('winter-cluster_traj_overlay')
outfilename=os.path.join('/home/lintaoli/dealwith-output/cluster-winter', outname)
plt.savefig(outfilename)   # remove margin/reduce border width
plt.clf()
```
