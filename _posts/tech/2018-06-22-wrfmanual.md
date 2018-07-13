---
layout: blog
tech: true   
istop: false  
title: "WRF 安装运行入门指南"
background-image: https://www.mmm.ucar.edu/sites/default/files/images/wrf_final_logo_150x127.jpg  
date:  2018-06-22 18:13:56  
category: tech   
tags:   
- tools 
- quick 
- wrf 
---   
# WRF在线资源

[WRF user_guide_v4](http://www2.mmm.ucar.edu/wrf/users/docs/user_guide_v4/v4.0/)    

[视频教程](https://pan.baidu.com/s/1AMu-xaqW0OMH1GtzuybZdg)    
[Configuring WRF 3.8 on Ubuntu Server 16.04](https://pan.baidu.com/s/17i2gmpLnfJaag5k0IzUv1g) 密码: vezf

WRF官网 [compilation_tutorial](http://www2.mmm.ucar.edu/wrf/OnLineTutorial/compilation_tutorial.php)

[WRF](http://murdoch-atmos.wikidot.com/wrf) 运行步骤

[aoddy](https://www.aoddy.com/2014/09/09/how-to-install-wrf-3-6-1-on-ubuntu-14-10-server/)

----

# **[WRF 安装运行入门指南](https://github.com/xigrug/xigrug.github.io/blob/master/book/WRF_MANUAL_V2.2.pdf)**

(WPS WRF_SI WRFV2.2 NCARG GrADS)
```
2007.04.    
by aioply 编辑整理    
```
* 目录    
* 1 WRF模式简介                     
* 2 准备工作（SSH和NetCDF）           
* 3 WPS+WRFV2.2安装运行简介           
   * 3.0. ～收集数据～                   
   * 3.1. ～安装前奏～                   
   * 3.2. ～安装WPS～                 
   * 3.3. ～运行WPS～               
   * 3.4. ～安装WRFV2.2～                  
   * 3.5. ～运行WRFV2.2～                   
* 4 WRF_SI+WRFV2.2安装运行简介                
   * 4.0. ～收集数据～                    
   * 4.1. ～安装WRF_SI～                 
     * 4.1.1. ～定义环境变量～            
     * 4.1.2. ～安装WRF_SI～              
     * 4.1.3. ～使用WRFSI的GUI～                
   * 4.2. ～运行WRF_SI～                  
     * STEP1: Localize model domain and create static files            
     * STEP2: DeGrib GRIB files                 
     * STEP3: Interpolate meteorological data              
   * 4.3. ～安装WRFV2.2～                 
   * 4.4. ～运行WRFV2.2～              
* 5 安装运行WRF2GrADS 
* 6 在UNXI下安装GrADS 
* 7 利用其它数据的练习 （ds083.2）  
* 附录 1 ：安装NCAR Graphic   
* 附录 2 ：关于WRF_SI2.0中wrfsi.nl的参数配置说明（中文版）  
* 附录 3 ：关于WRFV2.2中namelist.input的参数配置说明（中文版）     
* 附录 4 ：一些简单的UNIX命令   
