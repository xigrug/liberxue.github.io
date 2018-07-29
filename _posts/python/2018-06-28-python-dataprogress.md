---
layout: blog
tools: true
istop: false
title: "Python Data"
background-image: https://www.onlinebooksreview.com/uploads/blog_images/2017/11/08_Top+5+Libraries+for+Data+Science+in+Python.jpg
date:  2018-06-28 20:13:56
category: tools
tags:
- tools
- quickhtml
- python
---

# 插值

[反距离加权（IDW）插值](https://stackoverflow.com/questions/3104781/inverse-distance-weighted-idw-interpolation-with-python)

[Interpolation between grids with cKDTree](http://earthpy.org/interpolation_between_grids_with_ckdtree.html)
[Interpolation between grids with Basemap](http://earthpy.org/interpolation_between_grids_with_basemap.html)

[Point Interpolation](https://unidata.github.io/MetPy/latest/examples/gridding/Point_Interpolation.html#sphx-glr-examples-gridding-point-interpolation-py)

> Scipy.interpolate linear

> Natural neighbor interpolation (MetPy implementation)

> Cressman interpolation
  研究表明，温度相关参数的最优空间插值搜索半径介于150～250km之间 ［潘耀忠，龚道溢，邓磊，等．２００４．基于ＤＥＭ的中国陆地多年平均温度插值方法［Ｊ］．地理学报，2004,59(3)：366－374．］
[mipylib.numeric.minum.griddata(points, values, xi=None, **kwargs)](http://www.meteothinker.com/docs/meteoinfolab/numeric/functions/griddata.html)
https://journals.ametsoc.org/doi/pdf/10.1175/JTECH-D-15-0250.1
https://www3.epa.gov/scram001/adhoc/Gaudet2012.pdf
https://esrl.noaa.gov/csd/events/iwaqfr/presentations/posters/Zhao_Theme5.pdf
https://www.jcsda.noaa.gov/documents/meetings/wkshp2008/5/kondragunta_jcsdapresentation_10jun08.pdf
https://www.hindawi.com/journals/amete/2016/9873815/ 伴随
基于观测、模拟和同化数据的 PM2.5 污染回顾分析

> Barnes Interpolation

> Radial basis function interpolation 

[Inverse Distance Verification: Cressman and Barnes](https://unidata.github.io/MetPy/latest/examples/gridding/Inverse_Distance_Verification.html)

**[scipy.interpolate.griddata](https://docs.scipy.org/doc/scipy/reference/generated/scipy.interpolate.griddata.html)** ~= [matlab-griddata](https://ww2.mathworks.cn/help/matlab/ref/griddata.html)

[matplotlib自带插值](https://matplotlib.org/examples/pylab_examples/griddata_demo.html)

[Interpolation points data into 2-d shapefile with matplotlib](https://stackoverflow.com/questions/41315583/interpolation-points-data-into-2-d-shapefile-with-matplotlib)

## 例子

[使用python的Basemap (2) - MetPy和wrf-python的內插](https://home.gamer.com.tw/creationDetail.php?sn=3880741)

紀錄分別使用MetPy和wrf-python兩種套件做內插的結果

目的是要做在850hPa上的溫度場

使用兩種方式做，分別為

1. MetPy的log_interp

2. wrf-python的interpz3d

[MetPy:](https://unidata.github.io/MetPy/latest/index.html)

![in1](https://raw.githubusercontent.com/xigrug/xigrug.github.io/master/picture/in1.PNG)

這裡的matplotlib應該是不需要import進來，忘記刪掉了
mcalc則是之後內插要用的
metpy.constant那邊import進去的那兩個常數是算位溫時會用到

![in2](https://raw.githubusercontent.com/xigrug/xigrug.github.io/master/picture/in2.PNG)

一樣只是讀檔讀資料
因為內插到等壓面上，所以也要讀氣壓資料，P是基本場，PB是擾動場
溫度的部分，nc檔裡面的T指的是擾動位溫，所以先加個300K的基本場


![in3](https://raw.githubusercontent.com/xigrug/xigrug.github.io/master/picture/in3.PNG)

然後MetPy我翻了老半天
裡面只有溫度轉位溫的函式，沒有位溫轉溫度的
所以只好自己手動算 ( 就是為什麼前面會import P0跟Kappa這兩個常數)
溫度和位溫的關係式我有用LaTex打在上面，看起來比較厲害一點

下面就是內插的部份了
MetPy的 log_interp 可以一次內插到很多個位置上
不過我只有要850hPa，所以 pLevs 就只有設在850上

log_interp的文件在這
https://unidata.github.io/MetPy/latest/api/generated/metpy.calc.log_interp.html#metpy.calc.log_interp
其實我看了說明之後也不太確定為什麼會是用這個 log_interp來做內插
不過我看MetPy裡面示範從模式的Sigma座標內插到等壓面就是用這個
所以我就直接學它了

log_interp 其實可以一次內插很多種變數
所以假設我打 log_interp( plevs, pressure, temperature, qvapor, axis=1 )
這樣就會回傳 1. 溫度在plevs這個壓力面的內插值和 2. 水氣在plevs這個壓力面的內插值
不過我只有要內插溫度就是了
axis = 1 則是看要內插的是哪個維度
因為temperature是四維的變數： ( 時間, Z方向, Y方向, X方向 )
所以axis = 1來指定是內插 Z方向
而內插的結果會保留Z方向這個維度： ( 61, 27, 150, 150)    ->   ( 61, 1, 150, 150)
所以再用np.squeeze讓它變三維就好



![in4](https://raw.githubusercontent.com/xigrug/xigrug.github.io/master/picture/in4.PNG)

畫圖就跟上一篇畫降雨的差不多了，換個變數而已
最後結果是這樣

![in5](https://raw.githubusercontent.com/xigrug/xigrug.github.io/master/picture/in5.PNG)

----

看起來跟之前用NCL畫的不太一樣
但是用非常大概的角度看的話，主要的低溫部分都差不多
可能是因為這裡是用單一個模式輸出的去畫，之前用NCL畫的是系集平均吧



[wrf-python](http://wrf-python.readthedocs.io/en/latest/index.html)
用wrf-python畫的其實步驟也差不多，換個函數而已


![in6](https://raw.githubusercontent.com/xigrug/xigrug.github.io/master/picture/in6.PNG)

![in7](https://raw.githubusercontent.com/xigrug/xigrug.github.io/master/picture/in7.PNG)

使用wrf-python來把位溫轉溫度時，因為有wrf.tk可用所以就不用再自己算了
而且還可以指定單位，所以就直接設是攝氏了

內插的部分使用 wrf.interpz3d
這邊用起來感覺比較簡單一點，丟溫度場、氣壓場和想要內插的氣壓面
就會回傳內插完、在指定等壓面上的溫度場了
不需要像用MetPy的log_interp時一樣要指定內插的維度
不過要注意，wrf.interpz3d 規定丟進去的變數 ( 這裡就是指要做內插的溫度場和氣壓場) 最右邊的維度必須是nz * ny * nx，然後兩個變數的維度都要一模一樣
像這裡的溫度和氣壓場，都是 ( 61, 27, 150, 150 )，分別是時間、Z方向、Y方向、X方向
所以就符合wrf.interpz3d的要求

另外不像MetPy的log_interp
wrf.interpz3d不能一次內插到好幾個位置上
所以假設想要找在950hPa、850hPa、750hPa、500hPa的溫度場
就只能老實的寫個迴圈做4次內插了


![in8](https://raw.githubusercontent.com/xigrug/xigrug.github.io/master/picture/in8.PNG)

畫圖的部分大概是這樣，反正和上面的幾乎一樣
最後的結果會長這樣

![in9](https://raw.githubusercontent.com/xigrug/xigrug.github.io/master/picture/in9.PNG)
和用MetPy內插的結果根本幾乎一樣
我找了超久才找到不一樣的地方

所以兩種應該是都沒什麼差
就看之後遇到的情況或心情決定用哪個了
如果資料讀出來就直接內插畫圖，那應該MetPy或wrf-python都可
不過如果有需要做一些計算才要畫，那看起來優先用wrf-python處理應該還是比較好一點

不過wrf-python有建議再裝PyNgl來做畫圖的部分
但PyNgl好像還沒有支援python 3.X版本
而且試過NCL的畫圖方式後還是比較喜歡MATLAB / matplotlib的感覺
所以就沒有研究了

## plot

[Interpolation points data into 2-d shapefile with matplotlib](https://stackoverflow.com/questions/41315583/interpolation-points-data-into-2-d-shapefile-with-matplotlib)

## 点到点的插值

[Python interpolate point value on 2D grid](https://stackoverflow.com/questions/42504987/python-interpolate-point-value-on-2d-grid)  scipy.interpolate.griddata or scipy.interpolate.interp2d

# 距离

[概率分布之间的距离度量以及python实现](https://www.cnblogs.com/wt869054461/p/7156397.html)

# 回归

## **[PythonMachineLearning](https://github.com/tirthajyoti/PythonMachineLearning)**

[Linear_Regression_Methods](https://github.com/tirthajyoti/PythonMachineLearning/blob/master/Linear_Regression_Methods.ipynb)

# 通量
[Fluxpart](http://fluxpart.readthedocs.io/en/latest/tutorial.html) is a Python 3 module that implements the Scanlon and Sahu [SS08] method for partitioning eddy covariance measurements of water vapor and carbon dioxide fluxes into stomatal (transpiration, photosynthesis) and nonstomatal (evaporation, respiration) components, e.g.

#EOF 分析
[用Python做EOF分析](http://bbs.06climate.com/forum.php?mod=viewthread&tid=53258)

# other questions?

[how to interpolate points in a specific interval on a plot formed by loading a txt file in to scipy program?](https://stackoverflow.com/questions/16070219/how-to-interpolate-points-in-a-specific-interval-on-a-plot-formed-by-loading-a-t)
