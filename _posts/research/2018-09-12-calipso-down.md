---
layout: blog
tools: true
istop: false
title: "CALIPSO"
background-image: https://www-calipso.larc.nasa.gov/images/logos/animated_calipso_logo.gif
date:  2018-08-28 10:23:56
category: research
tags:
- research
- satellite
- calipso
- download
---


[CALIPSO数据下载方法与可视化](https://blog.csdn.net/wokaowokaowokao12345/article/details/78421191)
=================
 
引言
--

CALIPSO (Cloud–Aerosol Lidar and Infrared Path nder Satellite Observation) 是NASA和CNES 太阳轨道地球侦察卫星。CALIPSO搭载3个天顶视场的仪器（CALIOP, IIR, WFC），用于观测气溶胶和微米级的云粒。CALIPSO携带的可见光和近红外偏振传感器激光雷达用于观察地球气溶胶和云的相态。卫星数据分发格式为HDF和HDF-EOS，有不同级别的数据产品可供选择。对于很多入门级用户，由于没有人带处于完全自我摸索的研究者来说，下载数据有时候也是比较麻烦的。因为地球观测数据的下载毕竟不是迅雷下载电影那么简单。下面我就针对CALIPSO的数据下载和大家分享。

下载
--

有四种方式订购CALIPSO的数据（数据都是免费的）：  
[https://eosweb.larc.nasa.gov/HBDOCS/langley\_web\_tool.html](https://eosweb.larc.nasa.gov/HBDOCS/langley_web_tool.html), the Reverb Search Tool  
[http://reverb.echo.nasa.gov/reverb](http://reverb.echo.nasa.gov/reverb), and for Level 1 and 2 Lidar data only, the CALIPSO  
[https://www-calipso.larc.nasa.gov/search/login.php](https://www-calipso.larc.nasa.gov/search/login.php), Search and Subset Tool  
如果没有注册的话，需要首先注册一个用户，否则无法下载数据。  
[https://eosweb.larc.nasa.gov/content/calipso-search-and-subset-tool](https://eosweb.larc.nasa.gov/content/calipso-search-and-subset-tool)  
第四种方法可以根据时间 范围等检索数据，比较适合大范围下载数据，很好用。

我使用的是第二种方式，有时候网络访问很慢，网站会跳转到NASA的[对地数据搜索站点](https://search.earthdata.nasa.gov/search)，使用这个网站搜索下载数据更加方便。

### 数据下载

1.  打开网站：[https://search.earthdata.nasa.gov/search](https://search.earthdata.nasa.gov/search)，注册用户  
    
      
    ![这里写图片描述](https://img-blog.csdn.net/20171102090450569?watermark/2/text/aHR0cDovL2Jsb2cuY3Nkbi5uZXQvd29rYW93b2thb3dva2FvMTIzNDU=/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70/gravity/SouthEast)
    
2.  搜索CALIPSO选择自己需要的数据  
    
      
    ![这里写图片描述](https://img-blog.csdn.net/20171102090858328?watermark/2/text/aHR0cDovL2Jsb2cuY3Nkbi5uZXQvd29rYW93b2thb3dva2FvMTIzNDU=/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70/gravity/SouthEast)
    
3.  提交订购申请  
    向NASA Langley Research Center Atmosphere Science Data Center提出申请，它们会制作幷将数据传送服务器。  
    
      
    ![这里写图片描述](https://img-blog.csdn.net/20171102091752422?watermark/2/text/aHR0cDovL2Jsb2cuY3Nkbi5uZXQvd29rYW93b2thb3dva2FvMTIzNDU=/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70/gravity/SouthEast)  
    在用户信息“状态和历史”中可以查看已经订购的数据和状态。  
    ![这里写图片描述](https://img-blog.csdn.net/20171102091812832?watermark/2/text/aHR0cDovL2Jsb2cuY3Nkbi5uZXQvd29rYW93b2thb3dva2FvMTIzNDU=/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70/gravity/SouthEast)  
    我是前天订购的，所以经过一天的等待数据状态是这样。
    
4.  下载数据  
    NASA的LRCASDC提供数据花费时间不等，自提交到能够下载数据，根据数据量的多少、大小不同，ASDC准备的时间会有差别。所以提交数据后，不要着急，也不要怀疑自己操作错误，耐心等待即可。  
    
      
    ![这里写图片描述](https://img-blog.csdn.net/20171102092203852?watermark/2/text/aHR0cDovL2Jsb2cuY3Nkbi5uZXQvd29rYW93b2thb3dva2FvMTIzNDU=/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70/gravity/SouthEast)  
    经过煎熬的等待后，在注册用户留下的邮箱中会收到LRCASDC发送的数据下载链接，收到后抓紧时间下载，虽说可以7天内下载，事实有效期没那么久。  
    ![这里写图片描述](https://img-blog.csdn.net/20171102092212979?watermark/2/text/aHR0cDovL2Jsb2cuY3Nkbi5uZXQvd29rYW93b2thb3dva2FvMTIzNDU=/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70/gravity/SouthEast)  
    下载方法使用ftp传输软件就可以了，这里建议使用FileZilla，免费好用，不解释。
    

HDF文件可视化
--------

对于下载的HDF文件，可以使用官网提供的IDL程序包进行读取。也可以使用HDFView软件读取，也可以使用ccplot读取。笔者采用的是自己编译ccplot读取并对hdf数据进行可视化（绘图），在上篇博文中有关于ccplot的编译方法介绍。  

  
![这里写图片描述](https://img-blog.csdn.net/20171102093001587?watermark/2/text/aHR0cDovL2Jsb2cuY3Nkbi5uZXQvd29rYW93b2thb3dva2FvMTIzNDU=/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70/gravity/SouthEast)  
这是可视化后的效果

结语
--

上面的内容全是作者自己经过一周多的摸索徘徊中总结出的切实可行的操作方案，希望你看到这篇博文后能够少走弯路。

#### Mac OS 环境下安装ccplot并对CloudSat、_CALIPSO_和MODIS_数据_进行_可视化_

![wokaowokaowokao12345](https://avatar.csdn.net/6/1/E/3_wokaowokaowokao12345.jpg) wokaowokaowokao12345 
