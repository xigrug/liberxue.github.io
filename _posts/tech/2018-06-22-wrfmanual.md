---   <br>
layout: blog   <br>
tech: true   <br>
istop: false   <br>
title: "WRF 安装运行入门指南"   <br>
background-image: https://www.mmm.ucar.edu/sites/default/files/images/wrf_final_logo_150x127.jpg   <br>
date:  2018-06-22 18:13:56   <br>
category: tech   <br>
tags:   <br>
- tools   <br>
- quick   <br>
- wrf   <br>
---   <br>
   <br>
[WRF user_guide_v4](http://www2.mmm.ucar.edu/wrf/users/docs/user_guide_v4/v4.0/)   <br>
[视频教程](https://pan.baidu.com/s/1AMu-xaqW0OMH1GtzuybZdg)   <br>
# WRF 安装运行入门指南   <br>
   <br>
（WPS WRF_SI WRFV2.2 NCARG GrADS）   <br>
   <br>
```   <br>
2007.04.   <br>
by aioply 编辑整理   <br>
```   <br>
   <br>
## WRF安装运行入门指南   <br>
   <br>
      - 前言 ···································· 目录   <br>
- 1. WRF模式简介 ································   <br>
- 2. 准备工作（SSH和NetCDF） ·························   <br>
- 3. WPS+WRFV2.2安装运行简介 ·························   <br>
   - 3.0. ～收集数据～ ····························   <br>
   - 3.1. ～安装前奏～ ····························   <br>
   - 3.2. ～安装WPS～ ····························· ～ WPS ～   <br>
   - 3.3. ～运行WPS～ ·····························   <br>
   - 3.4. ～安装WRFV2.2～ ····························· ～ WRFV2.2 ～   <br>
   - 3.5. ～运行WRFV2.2～ ····························   <br>
- 4. WRF_SI+WRFV2.2安装运行简介 ······················   <br>
   - 4.0. ～收集数据～ ······························   <br>
   - 4.1. ～安装WRF_SI～ ···························· ～ WRF_SI ～   <br>
         - 4.1.1. ～定义环境变量～ ·························   <br>
         - 4.1.2. ～安装WRF_SI～ ·························   <br>
         - 4.1.3. ～使用WRFSI的GUI～ ······················   <br>
   - 4.2. ～运行WRF_SI～ ···························   <br>
         - STEP1: Localize model domain and create static files ··············   <br>
         - STEP2: DeGrib GRIB files ························   <br>
         - STEP3: Interpolate meteorological data ··················   <br>
   - 4.3. ～安装WRFV2.2～ ··························· ～ WRFV2.2 ～   <br>
   - 4.4. ～运行WRFV2.2～ ···························   <br>
- 5. 安装运行WRF2GrADS ·····························   <br>
- 6. 在UNXI下安装GrADS ·····························   <br>
- 7. 利用其它数据的练习 （ds083.2） ·······················   <br>
- 附录 1 ：安装NCAR Graphic ····························   <br>
- 附录 2 ：关于WRF_SI2.0中wrfsi.nl的参数配置说明（中文版） ·············   <br>
- 附录 3 ：关于WRFV2.2中namelist.input的参数配置说明（中文版） ············   <br>
- 附录 4 ：一些简单的UNIX命令 ···························   <br>
   <br>
   <br>
# 前言   <br>
   <br>
连我自己也没想到，还会接着WRF版本的更新，不自量力地整理出第三版入门指南。但我想这将是   <br>
   <br>
自己能整理出来的最后一个版本了。曾经在发布第二版时承诺要增加WRF的namelist.input和WRF2GrADS   <br>
   <br>
的control_file文件的翻译以及NCARG和WRF-3DVAR的安装运行入门等相关内容。可惜自己的能力和精   <br>
   <br>
力有限，control_file和WRF-3DVAR的工作没有做完，十分抱歉。不过有兴趣的人可以接着做。   <br>
   <br>
由于第二版和第三版的初衷一样，就把第二版的前言稍作修改就又再贴上了。   <br>
   <br>
我是WRF的初学者。   <br>
   <br>
在自己刚接触WRF时亦曾在Google上搜索过WRF中文手册之类的东西，但没有任何收获。WRF主   <br>
   <br>
页提供的教程虽然详细，但对于不熟悉UNIX系统和头一次接触气象模式的人来说，几乎就是无从下手。   <br>
   <br>
于是师姐RODA把自己当时的自学笔记借给我。我十分感谢她的帮助。后来我在自学的基础上，又加以补   <br>
   <br>
充和整理，编辑成了《WRF 安装运行入门指南》（WRF_SI+WRF版本，2006.10.28成稿）。随后，自己又   <br>
   <br>
在运转WRF的过程中积累经验，又赶上WPS的发放，就一并整理了出来，分享给大家。希望这本指南能   <br>
   <br>
对WRF初学者有一定的帮助。也许还有很多和我一样从没接触过UNIX系统的人，我也尽量把安装过程   <br>
   <br>
和命令文的输入方法写得详细。希望任何WRF的初学者们都能顺利地看懂这本指南，并能顺利地安装并   <br>
   <br>
运行起WRF模式。   <br>
   <br>
同时，限于整理者的水平，在本指南中不仅用词十分简陋，而且对许多专用术语也未能正确翻译和使   <br>
   <br>
用，希望大家在使用的时候，请以WRF主页的tutorial为主，把本指南作为参考来用。同时强烈建议大家再   <br>
   <br>
安装运行WRF的时候，把自己做过的内容、遇到的错误等信息详细记录下来，不仅有利于以后的复习，也   <br>
   <br>
方便错误的查找。不敢期待这本指南能会有多大的用途。但是，我想多一些基础性的教程，就会多一些感   <br>
   <br>
兴趣的人，多一些研究者。特别是在论坛上交流讨论的时候，大家就不会再把时间浪费在一些初级问题上，   <br>
   <br>
更多的是挖掘它的内涵。当然，这些东西只靠几个人的经验和能力是远远不够的，需要大家的支持。为了   <br>
   <br>
方便更多的人学习WRF，我希望大家能把自己在转WRF时的经验和遇到的问题及解决办法介绍出来，整理   <br>
   <br>
后和指南一并贴出。如果能得到大家的响应，我想这本指南会帮助更多的人学习WRF模式。   <br>
   <br>
根据使用的计算机的软硬件的差别，在编译的过程当中不会一帆风顺；编译通不过的原因也多种多样。   <br>
   <br>
特别是在运行的初期阶段，个人的错误操作原因为多。遇到了问题时不要焦急、也不要气馁，在自己寻求   <br>
   <br>
答案未果的情况下，多到动力论坛和wrf forum里和大家交流交流。   <br>
   <br>
在使用指南的过程中，如果你认为当中有翻译不恰当，用词有错误，或者是有任何意见或建议的话，   <br>
   <br>
敬请来信告知aioply@163.com。谢谢。   <br>
   <br>
在整理本指南的时候，得到了动力论坛（LASG）『资料与数据处理』版主ustcsunl的大力支持；以及   <br>
   <br>
动力论坛上的网友tzhang、tanghao和穹山提供的参考资料；在模式及其相关软件的学习过程当中   <br>
   <br>
windrisingdl的无私的帮助。namelist.input的翻译也是多亏有tanghao和windrisingdl的支持和帮助才得以完   <br>
   <br>
成大部分内容。当然，donglipl，leepy，yuhuaying，zhucoffee等坛友提供了宝贵的参考意见和建议，特别   <br>
   <br>
还有light，distance4lee提供的修改意见，对本指南的最后成形起了很大的作用，在此一并表示感谢。   <br>
   <br>
   <br>
注：在本指南的第 3 部分和第 4 部分分别记述了WPS+WRFV2.2和WRF_SI+WRFV2.2的安装运行方法，   <br>
   <br>
实际使用时可任选其一（WRF的开发者们推荐使用前者）。   <br>
   <br>
指南中以绿色书写的部分为UNIX的命令文，蓝色为链接部分。   <br>
   <br>
   <br>
# 1 ．＜WRF模式简介＞   <br>
   <br>
Weather Research and Forecasting Model(WRF)被誉为是次世代的中尺度天气预报模式。二战后，由于计算   <br>
   <br>
机技术的迅猛发展，气象预报技术也随之突飞猛进。短短的几十年里，世界各地的气象研究机关开发出了   <br>
   <br>
各自的相对独立的气象模式。这些模式之间缺少互换性，对科研及业务上的交流极其不便。从上世纪 90   <br>
   <br>
年代后半开始，美国对这种乱立的模式状况进行反省。最后由美国环境预测中心（NCEP）,美国国家大气   <br>
   <br>
研究中心（NCAR）等美国的科研机构为中心开始着手开发一种统一的气象模式。终于于 2000 年开发出了   <br>
   <br>
WRF模式。同时，为使研究成果能够迅速地应用到现实的天气预报当中去，WRF模式分为ARW(the   <br>
   <br>
Advanced Research WRF)和NMM(the Nonhydrostatic Mesoscale Model)两种，即研究用和业务用两种形   <br>
   <br>
式，分别由NCEP和NCAR管理维持着。本指南中使用的是前者WRF ARW。   <br>
   <br>
WRF模式为完全可压缩以及非静力模式，采用F90语言编写。水平方向采用Arakawa C(荒川C)网格   <br>
   <br>
点，垂直方向则采用地形跟随质量坐标。WRF模式在时间积分方面采用三阶或者四阶的Runge-Kutta算法。   <br>
   <br>
WRF模式不仅可以用于真实天气的个案模拟，也可以用其包含的模块组作为基本物理过程探讨的理论根   <br>
   <br>
据。WRF的开发组是这样介绍WRF模式的特点的：   <br>
   <br>
The WRF model is a fully compressible, nonhydrostatic model (with a hydrostatic option). Its vertical   <br>
   <br>
coordinate is a terrain-following hydrostatic pressure coordinate. The grid staggering is the Arakawa   <br>
   <br>
C-grid. The model uses the Runge-Kutta 2nd and 3rd order time integration schemes and 2nd to 6th order   <br>
   <br>
advection schemes in both horizontal and vertical directions. It uses a time-split small step for acoustic and   <br>
   <br>
gravity-wave modes. The dynamics conserves scalar variables.   <br>
   <br>
   <br>
   <br>
- Real-data and idealized simulations   <br>
- Various lateral boundary condition options for real-data and idealized simulations   <br>
- Full physics options   <br>
- Non-hydrostatic and hydrostatic (runtime option)   <br>
- One-way, two-way nesting and moving nest   <br>
- Three-dimensional analysis nudging   <br>
- Observation nudging   <br>
- Applications ranging from meters to thousands of kilometers   <br>
   <br>
另外模式的输出及其后的分析承接前一代MM5的系统，透过RIP、NCAR Graphic、Vis5D以及GRADS   <br>
   <br>
等绘图软件绘制各种气象场。   <br>
   <br>
WRF的最新版本是 2006 年的圣诞节前 12 月 22 日推出的Ver2.2。这一版本里，在修补了前一版本的许多   <br>
   <br>
错误之上，新增了许多模块。不仅推出了WRF的前处理WRFSI的进化版WPS，作为过渡还仍然保留了WRF   <br>
   <br>
本体和WRFSI的衔接。   <br>
   <br>
   <br>
### WRF模式的流程示意图如下：   <br>
   <br>
![wrf-demo](http://www2.mmm.ucar.edu/wrf/users/docs/user_guide_v4/v4.0/users_guide_chap1.fld/image001.png)   <br>
```   <br>
出处：User’s Guide for Advanced Research WRF (ARW) Modeling System Version 2.   <br>
```   <br>
   <br>
# 2 ．＜准备工作＞   <br>
   <br>
注:本文所记述的安装过程仅是在编译器等软件安装完备的条件下进行的。限于笔者的知识水平有限，对这   <br>
   <br>
些基本环境的设定不能进行意义描述，十分抱歉。   <br>
   <br>
设定SSH   <br>
   <br>
要进行正规的模拟气象的运算，就必须要有Super-Computer。如果没有条件，可直接进入安装部分。   <br>
   <br>
不需要连接Super-Computer的人可直接进入下一步安装过程。   <br>
   <br>
＜首先，把自己的电脑和supercomputer进行连接＞   <br>
   <br>
① 我们使用SSHSecureShellClient-3.2.9 共享软件。从网上可以下载得到。好像目前只有英语版的。没关   <br>
   <br>
系，既然要搞天气预报了，这点简单的英语应该不算难的。   <br>
   <br>
② 安装SSHSecureShellClient。在桌面上会出现两个图标。点击白色的。Edit—〉Setting—〉ProfileSetting—〉   <br>
   <br>
connection。在里面填上自己的Host，User，Port。点击OK。软件会记住你的Host，User，Port，以后   <br>
   <br>
每回只需输入密码即可使用。然后点击Quick connect。会出现一个小窗口。   <br>
   <br>
里面记载了自己的Host Name，User Name，Port Number，Authentication Method信息，在Authentication   <br>
   <br>
Method处选择Password，点击Connect。然后输入密码，如果成功的话就应该会和supercomputer连接上   <br>
   <br>
了。   <br>
   <br>
还有一个黄色的图标SSH Secure File Transfer Client，此程序可用于自己当前计算机和supercomputer之间   <br>
   <br>
的文件传输交换，支持直接拖拽文件。   <br>
   <br>
第一次和supercomputer连接上后，马上进行密码变更。操作顺序如下：   <br>
   <br>
¾ passwd   <br>
   <br>
Changing password for user user   <br>
   <br>
Enter login(LDAP) password : (旧密码)   <br>
   <br>
New UNIX password: (新密码)   <br>
   <br>
Retype new UNIX password: (新密码)   <br>
   <br>
LDAP password information changed for user   <br>
   <br>
Passwd: all authentication tokens updated successfully.   <br>
   <br>
   <br>
   <br>
Software requirement   <br>
   <br>
重要！首先检查自己是否已经具备了运行WRF的工作环境和机器配置条件。   <br>
   <br>
   <br>
- Fortran 90 or 95 and c compiler   <br>
- perl 5.04 or better   <br>
- If MPI and OpenMP compilation is desired, it requires MPI or OpenMP libraries   <br>
- WRF I/O API supports netCDF, PHD5, GriB 1 and GriB 2 formats, hence one of these libraries needs to be   <br>
available on the computer where you compile and run WRF   <br>
   <br>
Bash 和 Csh   <br>
   <br>
安装之前，一定要弄清楚自己所使用的计算机的shell。一般输入下面的命令就可以得到答案。   <br>
* echo $SHELL   <br>
   <br>
如果答案是csh，就请参考Online tutorial里的命令文的输入方法。   <br>
   <br>
本指南使用的是bash。如何区别这两种shell的写法，请另行找书参考。   <br>
   <br>
安装NetCDF   <br>
   <br>
安装运行WRF模式之前，必须要安装NetCDF。可以通过下面的网址下载。   <br>
   <br>
[http://www.unidata.ucar.edu/software/netcdf/index.html](http://www.unidata.ucar.edu/software/netcdf/index.html)   <br>
   <br>
使用gunzip和tar命令对文件进行解压，展开。   <br>
```   <br>
 tar –xvf netcdf-3.6.1.tar   <br>
 cd netcdf-3.6.1/src   <br>
 ./configure --prefix=/home/user/you/（安装在指定的目录下）   <br>
```   <br>
检查/netcdf-3.6.1/src 目录下的 macros.make 文件。   <br>
   <br>
 vi macros.make   <br>
   <br>
（在此处，使用vi命令。UNIX的初学者注意：用vi命令可以编辑文件，不保存退出时按顺序按下   <br>
   <br>
<Esc> : q! <shift+1>键，即可退出；若要保存后退出可按 <Esc> : w q 共四键）   <br>
   <br>
注意到INSTALL行。如果此行是INSTALL = /usr/bin/install –c 即可；如果不是，要按此修正。   <br>
   <br>
¾ make check   <br>
   <br>
¾ make install (UNIX下安装软件的一般步骤: 1../configure 2. make 3. make install )   <br>
   <br>
此时，要确认在prefix的地方（这回是/home/user/you/）会有bin, lib, include和man目录生成。   <br>
   <br>
设定NetCDF的环境变量：   <br>
   <br>
¾ NETCDF=/home/user/you;export NETCDF   <br>
   <br>
2007 年 3 月初，推出了NetCDF-3.6.2版本。使用最新版或者前一版都可以安装运行WRF Model。   <br>
   <br>
   <br>
同时，为方便使用，我们可以将某些环境变量登录到 .bashrc里。例如上面的NetCDF的环境变量。   <br>
   <br>
注意：慎重修改.bashrc文件！！！   <br>
   <br>
1 ） 在/home/user/you/目录下输入   <br>
   <br>
¾ vi .bashrc   <br>
   <br>
2 ） 输入NetCDF的环境变量。键入<Esc> : w q保存退出。   <br>
   <br>
3 ） 键入如下命令即可定义环境变量：   <br>
   <br>
¾ source ~/.bashrc   <br>
   <br>
   <br>
   <br>
# 3 ．＜WPS+WRFV2.2安装运行简介＞   <br>
   <br>
请参照网页http://www.mmm.ucar.edu/wrf/OnLineTutorial/index.htm，内有详细的Online Tutorial。本章的内容   <br>
   <br>
是参照上述网页的内容进行翻译，并结合自己在操作过程中遇到的困难进行归纳整理而完成的。其中，本   <br>
   <br>
章和第 4 章的WRFV2.2部分基本一致（只有ln处稍有不同），重复书写难免会有些累赘。但为了保持WPS   <br>
   <br>
和WRF_SI各自运行的连贯性，请读者在使用时注意！   <br>
   <br>
##3.0． ～收集数据～   <br>
   <br>
Get Source Code   <br>
   <br>
下载WRF模式的源码。在下载之前要认真阅读此页 的内容，并从中可以下载到WRF的Source_Codes。第   <br>
   <br>
一次使用要注册；已经注册过的要登陆。   <br>
   <br>
把所需要的，最新的Source_Codes收集在一起，分类放到同一个目录下，比如:   <br>
   <br>
在/home/user/you/下建立一个名为Source_Codes_and_Graphics_Software的源码存放区。例如：   <br>
   <br>
¾ mkdir Source_Codes_and_Graphics_Software   <br>
   <br>
并且为以防万一，把收集到的Source_Codes刻成CD或者DVD，作为备份。   <br>
   <br>
   <br>
Program Flow   <br>
   <br>
根据自己的研究需要，下载下列程序：   <br>
   <br>
· 仅需要模拟理想状态问题：   <br>
   <br>
   <br>
WRF-ARW Model + PostProcessing   <br>
   <br>
· 需要模拟实际问题：   <br>
   <br>
WPS + WRF-ARW Model + PostProcessing   <br>
   <br>
· 模拟加入影响变动值后的实际问题：   <br>
   <br>
WPS + WRF-Var + WRF-ARW Model + PostProcessing   <br>
（如果想使用WRF-Var ，还要另外学习其使用方法WRF-Var Online Tutorial）   <br>
   <br>
   <br>
   <br>
Documentation   <br>
   <br>
Users' Guide   <br>
   <br>
User’s Guide 里包含了全部的WRF OnLine Tutorial。并且，User’s Guide 是每半年更新一次，为更好的使   <br>
   <br>
用WRF ARW model，请使用最新版的。在运行模式之前，下载一份User’s Guide作为指导教程。   <br>
   <br>
WRF ARW Technical Note   <br>
   <br>
PDF文件。在此Note里包含有以下内容：   <br>
   <br>
· ARW model 的方程式，discretization，初期设定，nesting的概要   <br>
   <br>
· 模式中利用可能的Physical Options 的概要   <br>
   <br>
· WRF-Var的概要   <br>
   <br>
Bi-Annual Tutorial Presentation   <br>
   <br>
开发人员编写的PowerPoint，可以算是WRF模式讲解的精华。强烈建议仔细，反复阅读。在转WRF的过   <br>
   <br>
   <br>
### 程中，不同时期，怀着不同目的时，会有不同的理解和收获。对初次学习WRF模式的人会有很大的帮助。   <br>
   <br>
WRF-Var   <br>
   <br>
有关WRF-Var的解释说明和WRF-Var OnLine Tutorial 的连接。   <br>
   <br>
WRFSI   <br>
   <br>
在此页，不仅有WRFSI的说明，还可以下载一些必要相关的软件。   <br>
   <br>
```   <br>
＊ 从WRF的主页（WRF ARW Users Pages）上可以得到更多的情报和一些很有用的解释说明。   <br>
```   <br>
Case Study   <br>
   <br>
在此，以Hurricane Katrina (August 28，2005) 为例进行WRF test run练习。   <br>
   <br>
为了Case Study 和下载练习所需的数据，必须准备足够的硬盘空间。然后建立working directory工作域。   <br>
   <br>
我自己的是建立在/home/user/you/下的。   <br>
   <br>
例如你可以输入:（输入命令文时严格区分字母大小写）   <br>
   <br>
¾ mkdir WRF （建立目录）   <br>
   <br>
¾ cd WRF （进入目录）   <br>
   <br>
（返回上一目录的命令是cd .. ）   <br>
   <br>
在global AVN data 处下载所练习用的气象数据。   <br>
   <br>
本次的case study 的领域如右图所示。   <br>
   <br>
### WRF ARW模式里，主要流程如下图所示：   <br>
   <br>
### WPS是和WRFV2.2一同被推出的，可以看成是WRF_SI的进化版。   <br>
   <br>
   <br>
## 3.1． ～安装前奏～   <br>
   <br>
Get Source Code   <br>
   <br>
下载WPS和WRFV2.2的source code。。   <br>
   <br>
建立一个名为WRF的工作目录（如果在上一页已经建立了的话，此处就没有必要再建立了）。   <br>
   <br>
（比如说我是在/home/user/you/里建立的）。   <br>
   <br>
¾ mkdir WRF   <br>
   <br>
   <br>
Unpack the Code   <br>
   <br>
把下载到的WPS.TAR.gz和WRFV2.TAR.gz文件复制到新建的WRF目录下。然后进行解压和展开工作。   <br>
   <br>
因为版本可能会随时被更新，请保持下载最新版学习使用。   <br>
复制：   <br>
¾ cp WPS.TAR.gz /home/user/you/WRF/（可参考cp命令的使用方法）   <br>
¾ cp WRFV2.TAR.gz /home/user/you/WRF/   <br>
解压：   <br>
¾ gunzip WPS.TAR.gz   <br>
¾ gunzip WRFV2.TAR.gz （对文件进行解压）   <br>
打开TAR file：   <br>
¾ tar –xvf WPS.TAR   <br>
¾ tar –xvf WRFV2.TAR （不要忘记 –xvf ）   <br>
于是，会有WPS/和WRFV2/目录被做成。   <br>
   <br>
Compile WRFV2.2 First   <br>
安装WPS有点麻烦，因为安装WPS时要用到WRFV2.2里的几个文件库。所以在安装WPS之前还要先安装   <br>
好WRFV2.2。详细的安装过程请参照本指南的3.4.节安装WRFV2.2。这里，只为安装WPS记述安装过程的   <br>
几步命令文。   <br>
¾ cd /home/user/you/WRF/WRFV   <br>
¾ ./configure   <br>
¾ 1 （如果考虑到了并行计算、嵌套等问题，请选择 3 。详见后文）   <br>
¾ ./compile em_real >& compile.log   <br>
如果在WRFV2/main/目录下生成了real.exe和wrf.exe等可执行文件，则表明WRFV2.2编译成功。下一步   <br>
可以进行安装WPS了。   <br>
   <br>
在运行WPS时，使用NCARG可以随时把各步骤的设定信息以图像的形式表现出来，方便大家随时进行确   <br>
认和更改。当然，是否安装NCARG和成功与否，与最后的WRF模式的运行无关。NCARG软件可以作为选   <br>
择安装项。具体的安装方法请参考附录 1 。   <br>
   <br>
   <br>
## 3.2. ～安装WPS～   <br>
   <br>
Examine the Source Code   <br>
进入到/home/user/you/WRF/WPS/目录下   <br>
¾ cd WPS   <br>
检查目录中的内容。   <br>
¾ ls –all （ls –a亦可）   <br>
会有如下内容表示：   <br>
Inside this directory, you will find the following files and directories:   <br>
-rw-r--r-- 1 you user 5074 Sep 15 13:05 README   <br>
-rw-r--r-- 1 you user 13 Nov 14 14:49 VERSION   <br>
drwxr-xr-x 2 you user 32768 Nov 14 14:48 arch   <br>
-rwxr-xr-x 1 you user 1672 Sep 08 18:50 clean   <br>
-rwxr-xr-x 1 you user 3349 Sep 12 11:11 compile   <br>
-rwxr-xr-x 1 you user 4257 Jul 19 13:47 configure   <br>
drwxr-xr-x 5 you user 32768 Nov 14 14:48 geogrid   <br>
-rwxr-xr-x 1 you user 1138 Aug 03 10:09 link_grib.csh   <br>
drwxr-xr-x 4 you user 32768 Nov 14 14:48 metgrid   <br>
-rw-r--r-- 1 you user 1638 Oct 30 11:54 namelist.wps   <br>
drwxr-xr-x 7 you user 32768 Nov 14 14:48 test_suite   <br>
drwxr-xr-x 4 you user 32768 Nov 14 14:48 ungrib   <br>
drwxr-xr-x 3 you user 32768 Nov 14 14:48 util   <br>
   <br>
README文件里有与程序安装和运行有关的有用情报。运行之前最好阅读一次。   <br>
WPS目录下的文件分类：   <br>
Source code directories:   <br>
geogrid/ Directory containing code to create the static data   <br>
metgrid/ Directory containing code to create input to WRFV   <br>
ungrib/ Directory containing code to unpack GRIB data   <br>
util/ Directory containing some utilities   <br>
Scripts:   <br>
clean Script to clean created files, executables   <br>
compile Script for compiling WPS code   <br>
configure Script to configure the configure.wps file for compile   <br>
link_grib.csh Script to link GRIB files   <br>
arch/ Directory where compile options are gathered   <br>
namelist.wps WPS namelist   <br>
   <br>
   <br>
Configure WPS   <br>
键入：   <br>
¾ ./configure   <br>
此时，屏幕上会显示出计算机所支持的平台。   <br>
you@tgg075004:/home/user/you/WRF/WPS> ./configure   <br>
Will use NETCDF in dir: /home/user/you/   <br>
$JASPERLIB or $JASPERINC not found in environment, configuring to build without grib2 I/O...   <br>
------------------------------------------------------------------------   <br>
Please select from among the following supported platforms.   <br>
   <br>
1. PC Linux x86_64 (IA64 and Opteron), PGI compiler 5.2 or higher, serial, NO GRIB   <br>
2. PC Linux x86_64 (IA64 and Opteron), PGI compiler 5.2 or higher, serial   <br>
3. PC Linux x86_64 (IA64 and Opteron), PGI compiler 5.2 or higher, DM parallel, NO GRIB   <br>
4. PC Linux x86_64 (IA64 and Opteron), PGI compiler 5.2 or higher, DM parallel   <br>
5. PC Linux x86_64 (IA64 and Opteron), PathScale compiler 2.1 or higher, serial, NO GRIB   <br>
6. PC Linux x86_64 (IA64 and Opteron), PathScale compiler 2.1 or higher, DM parallel, NO GRIB   <br>
    Enter selection [1-6] :   <br>
（由于计算机的差异，有可能会显示出其他的平台选项）   <br>
作为练习，我们选择最为基本的（serial）。然后键入：   <br>
¾ 1   <br>
如果需要使用MPI并行运行的话，就要选择 3 或者 4 。其区别应该可以一目了然吧。   <br>
   <br>
然后会出现以下的对话：   <br>
------------------------------------------------------------------------   <br>
Configuration successful. To build the WPS, type: compile   <br>
------------------------------------------------------------------------   <br>
   <br>
这时将会有configure.wps 文件被做成。如果有必要，对文件compile options/paths也要进行编辑。   <br>
   <br>
Compile WPS   <br>
然后开始编译模块。   <br>
¾ ./compile >& compile.log   <br>
如果编辑成功，会有以下的可执行文件被做成！   <br>
lrwxrwxrwx 1 you user 23 Mar 9 13:01 geogrid.exe -> geogrid/src/geogrid.exe*   <br>
lrwxrwxrwx 1 you user 23 Mar 9 13:02 metgrid.exe -> metgrid/src/metgrid.exe*   <br>
lrwxrwxrwx 1 you user 21 Mar 9 13:01 ungrib.exe -> ungrib/src/ungrib.exe*   <br>
如果编辑失败了，请确认compile.log里的错误信息。   <br>
geogrid.exe Generate static data   <br>
metgrid.exe Generate input data for WRFV   <br>
ungrid.exe Unpack GRIB data   <br>
   <br>
   <br>
另外，还有一些有用的工具会被链接到util/目录下。   <br>
lrwxrwxrwx 1 you user 16 Mar 9 17:46 avg_tsfc.exe -> src/avg_tsfc.exe*   <br>
lrwxrwxrwx 1 you user 25 Mar 9 17:46 g1print.exe -> ../ungrib/src/g1print.exe*   <br>
lrwxrwxrwx 1 you user 25 Mar 9 17:46 g2print.exe -> ../ungrib/src/g2print.exe*   <br>
lrwxrwxrwx 1 you user 16 Mar 9 17:46 mod_levs.exe -> src/mod_levs.exe*   <br>
lrwxrwxrwx 1 you user 15 Mar 9 17:46 plotfmt.exe -> src/plotfmt.exe*   <br>
lrwxrwxrwx 1 you user 17 Mar 9 17:46 plotgrids.exe -> src/plotgrids.exe*   <br>
lrwxrwxrwx 1 you user 23 Mar 9 17:46 rd_intermediate.exe -> src/rd_intermediate.exe*   <br>
   <br>
```   <br>
avg_tsfc.exe Computes daily mean surface temperature from intermediate files. Recommended for   <br>
using with the 5-layer soil model (sf_surface_physics = 1) in WRF   <br>
g1print.exe List the contents of a GRIB1 file   <br>
g2print.exe List the contents of a GRIB2 file   <br>
mod_levs.exe Remove superfluous levels from 3-d fields in intermediate files   <br>
plotfmt.exe Plot intermediate files (dependent on NCAR Graphics - if you don't have these   <br>
libraries, plotfmt.exe will not compile correctly)   <br>
plotgrids.exe Generate domain graphics. An exellent tool to configure domains before running   <br>
geogrid.exe (dependent on NCAR Graphics - if you don't have these libraries,   <br>
plotgrids.exe will not compile correctly)   <br>
rd_intermediate.exe Read intermediate files   <br>
如果还未安装NCARG或者安装失败，则不会出现plotfmt.exe和plotgrids.exe两个可执行文件。这两个   <br>
文件的有无并不会影响到WRF的正常运行。   <br>
You are now ready to run the WPS.   <br>
```   <br>
## 3.3. ～运行WPS～   <br>
   <br>
WPS用来建立WRFV2的输入文件。其流程如下图所示：   <br>
   <br>
geogrid和ungrib 属并列关系，运行不分先后。   <br>
geogrid 建立“静态的”地面数据。   <br>
ungrib 解压GRIB 气象数据，并归纳成一个 intermediate 文件格式。   <br>
metgrid 把气象数据水平插入模式领域内。   <br>
metgrid的输出文件将被用作WRFV2.2的输入文件。   <br>
   <br>
   <br>
Get Terrestrial Input Data   <br>
同样，在WRF目录里建立WPS_GEOG目录，用来盛放模式用的地表面静态数据。   <br>
下载WPS_GEOG数据，将模式所需的地表数据解压。这些数据分两类，一类是general input files；另一类   <br>
数据是根据解像度分为10m、5m、2m和30s（即大约分别为110km，55km，20km和1km）共 4 种。如果   <br>
不确定要使用哪一种，可以把这些数据全部保存起来，以后备用。   <br>
-rw-r--r-- 1 you user 190945280 Mar 10 14:10 geog_10m.tar.gz   <br>
-rw-r--r-- 1 you user 4403015680 Mar 10 14:11 geog_2m.tar.gz   <br>
-rw-r--r-- 1 you user 4686346240 Mar 10 14:14 geog_30s.tar.gz   <br>
-rw-r--r-- 1 you user 725934080 Mar 10 14:19 geog_5m.tar.gz   <br>
-rw-r--r-- 1 you user 76021760 Mar 10 14:31 geog_general.tar.gz   <br>
在WRF/WPS_GEOG/目录下：使用gunzip和tar命令进行解压。   <br>
解压后，会自动生成名为geog/的目录。在geog/目录里包含有这 4 种解像度的目录，每个目录里都有介绍   <br>
数据的index文件。   <br>
   <br>
* Run geogrid.exe   <br>
编辑namelist.wps文件，作以下领域设定的修改。为方便初学者学习，未考虑嵌套问题。   <br>
max_dom = 1,   <br>
e_we = 75,   <br>
e_sn = 70,   <br>
map_proj = 'mercator',   <br>
ref_lat = 25.00,   <br>
ref_lon = -85.00,   <br>
truelat1 = 0.0,   <br>
truelat2 = 0.0,   <br>
stand_lon = -85.00,   <br>
geog_data_path = '/home/user/you/WRF/WPS_GEOG/geog'   <br>
   <br>
我们可以使用NCAR Graphic来查看我们的领域设定。具体方法请参考WRF网站的Tutorial。   <br>
如果满意，继续运行geogrid.exe，生成静态数据。   <br>
* ./geogrid.exe   <br>
如果使用并行（4CPUs）计算的话，   <br>
* mpirun –np 4 geogrid.exe   <br>
在运行过程当中，会出现如下的画面信息：   <br>
   <br>
```   <br>
Parsed 11 entries in GEOGRID.TBL   <br>
Processing domain 1 of 1   <br>
Processing XLAT and XLONG   <br>
Processing MAPFAC   <br>
Processing F and E   <br>
Processing ROTANG   <br>
```   <br>
   <br>
```   <br>
Processing LANDUSEF   <br>
Calculating landmask from LANDUSEF (WATER = 16)   <br>
Processing HGT_M   <br>
Processing HGT_U   <br>
Processing HGT_V   <br>
Processing SOILTEMP   <br>
Processing SOILCTOP   <br>
Processing SOILCAT   <br>
Processing SOILCBOT   <br>
Processing ALBEDO12M   <br>
Processing GREENFRAC   <br>
Processing SNOALB   <br>
Processing SLOPECAT   <br>
Processing SLOPECAT   <br>
!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!   <br>
! Successful completion of geogrid.!   <br>
!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!   <br>
```   <br>
最后如果出现了"Successful completion of geogrid"，即表明运行成功。同时也会出现包含运行过程的   <br>
geogrid.log文件。   <br>
出现成功信息后，确认是否有静态的数据生成：   <br>
-rw-r--r-- 1 you user 2133896 Mar 10 15:01 geo_em.d01.nc   <br>
这里生成的.nc文件是NetCDF格式的文件。如果安装了graphical tool，我们还可以将这些数据进行可视化处   <br>
理。   <br>
   <br>
* ./ungrid.exe   <br>
整个练习用的数据可以计算 72 小时（网上的Tutorial 里只进行了最先的 24 小时的计算）。所以namelist.wps   <br>
里的设定如下：   <br>
start_date = '2005-08-28_00:00:00',   <br>
end_date = '2005-08-31_00:00:00',   <br>
interval_seconds = 21600   <br>
   <br>
下载 客观分析数据，并单独放到一个目录。最好保持各种不同的计算数据放到各自的目录里，例如放到   <br>
/home/user/you/WRF/DATA/Katrina/目录下。这些数据是global GFS/AVN GRIB1 data, available every 6 hours,   <br>
from 2005082800 to 2005083100。然后使用gunzip和tar来解压。   <br>
使用link_grib.csh文件把这些数据链接到WPS目录下。   <br>
例如，把这些数据解压后放到了/home/user/you/WRF/DATA/Katrina/目录下，其链接方法如下：   <br>
* ./link_grib.csh /home/user/you/WRF/DATA/Katrina/avn_   <br>
然后，我们会看到WPS目录里多了以下文件：   <br>
   <br>
   <br>
lrwxrwxrwx 1 you user 49 Mar 12 13:02 GRIBFILE. AAA -> /home/user/you/WRF/DATA/avn_050828_00_   <br>
lrwxrwxrwx 1 you user 49 Mar 12 13:02 GRIBFILE. AAB -> /home/user/you/WRF/DATA/avn_050828_00_   <br>
lrwxrwxrwx 1 you user 49 Mar 12 13:02 GRIBFILE. AAC -> /home/user/you/WRF/DATA/avn_050828_00_   <br>
lrwxrwxrwx 1 you user 49 Mar 12 13:02 GRIBFILE. AAD -> /home/user/you/WRF/DATA/avn_050828_00_   <br>
lrwxrwxrwx 1 you user 49 Mar 12 13:02 GRIBFILE. AAE -> /home/user/you/WRF/DATA/avn_050828_00_   <br>
lrwxrwxrwx 1 you user 49 Mar 12 13:02 GRIBFILE. AAF -> /home/user/you/WRF/DATA/ avn_050828_00_   <br>
lrwxrwxrwx 1 you user 49 Mar 12 13:02 GRIBFILE. AAG -> /home/user/you/WRF/DATA/avn_050828_00_   <br>
lrwxrwxrwx 1 you user 49 Mar 12 13:02 GRIBFILE. AAH -> /home/user/you/WRF/DATA/avn_050828_00_   <br>
lrwxrwxrwx 1 you user 49 Mar 12 13:02 GRIBFILE. AAI -> /home/user/you/WRF/DATA/avn_050828_00_   <br>
lrwxrwxrwx 1 you user 49 Mar 12 13:02 GRIBFILE. AAJ -> /home/user/you/WRF/DATA/avn_050828_00_   <br>
lrwxrwxrwx 1 you user 49 Mar 12 13:02 GRIBFILE. AAK -> /home/user/you/WRF/DATA/avn_050828_00_   <br>
lrwxrwxrwx 1 you user 49 Mar 12 13:02 GRIBFILE. AAL -> /home/user/you/WRF/DATA/avn_050828_00_   <br>
lrwxrwxrwx 1 you user 49 Mar 12 13:02 GRIBFILE. AAM -> /home/user/you/WRF/DATA/avn_050828_00_   <br>
   <br>
把Vtable 链接到当前目录（WRF/WPS/）下。因为我们使用的数据是GFS/AVN data, 所以使用GFS Vtable。   <br>
连接方法如下：   <br>
¾ ln -sf ungrib/Variable_Tables/Vtable.GFS Vtable   <br>
结果是生成下面的文件：   <br>
lrwxrwxrwx 1 you user 33 Mar 12 18:14 Vtable -> ungrib/Variable_Tables/Vtable.GFS   <br>
   <br>
运行ungrib.exe，并保留log文件。   <br>
¾ ./ungrib.exe >& ungrib.log   <br>
最好不要在这里使用并行。   <br>
最后屏幕里会出现下面的信息表示运行成功：   <br>
!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!   <br>
! Successful completion of ungrib.!   <br>
!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!   <br>
这时目录里会出现以下几个文件：   <br>
-rw-r--r-- 1 you user 38869928 Mar 13 15:20 FILE:2005-08-28_   <br>
-rw-r--r-- 1 you user 38869928 Mar 13 15:20 FILE:2005-08-28_   <br>
-rw-r--r-- 1 you user 38869928 Mar 13 15:20 FILE:2005-08-28_   <br>
-rw-r--r-- 1 you user 38869928 Mar 13 15:20 FILE:2005-08-28_   <br>
-rw-r--r-- 1 you user 38869928 Mar 13 15:20 FILE:2005-08-29_   <br>
-rw-r--r-- 1 you user 38869928 Mar 13 15:20 FILE:2005-08-29_   <br>
-rw-r--r-- 1 you user 38869928 Mar 13 15:20 FILE:2005-08-29_   <br>
-rw-r--r-- 1 you user 38869928 Mar 13 15:20 FILE:2005-08-29_   <br>
-rw-r--r-- 1 you user 38869928 Mar 13 15:20 FILE:2005-08-30_   <br>
-rw-r--r-- 1 you user 38869928 Mar 13 15:20 FILE:2005-08-30_   <br>
-rw-r--r-- 1 you user 38869928 Mar 13 15:20 FILE:2005-08-30_   <br>
-rw-r--r-- 1 you user 38869928 Mar 13 15:20 FILE:2005-08-30_   <br>
-rw-r--r-- 1 you user 38869928 Mar 13 15:20 FILE:2005-08-31_   <br>
   <br>
The log file created during this step is very important. It contains information regarding the fields which were   <br>
found in the input file and on which level these fields are available.   <br>
在这里，我们也同样可以使用NCAR Graphic来查看我们的领域设定。具体方法请参考WRF网站的Tutorial。   <br>
   <br>
   <br>
Run metgrid.exe   <br>
最后一部最简单，只要输入下面的命令即可：   <br>
* ./metgrid.exe   <br>
如果使用并行（4CPUs）计算的话，   <br>
* mpirun –np 4 metgrid.exe   <br>
运行结束后屏幕出现这样的信息：   <br>
Processing domain 1 of 1.   <br>
Processing 2005-08-28_00:00:   <br>
./FILE   <br>
Processing 2005-08-28_06:00:   <br>
./FILE   <br>
...（此处省略若干行）   <br>
Processing 2005-08-30_18:00:   <br>
./FILE   <br>
Processing 2005-08-31_00:00:   <br>
./FILE   <br>
!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!   <br>
! Successful completion of metgrid.!   <br>
!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!   <br>
   <br>
同时在目录里还会生成下面的几个NetCDF文件：   <br>
-rw-r--r-- 1 you user 5932836 Mar 13 15:27 met_em.d01.2005-08-28_00:00:00.nc   <br>
-rw-r--r-- 1 you user 5932836 Mar 13 15:27 met_em.d01.2005-08-28_06:00:00.nc   <br>
-rw-r--r-- 1 you user 5932836 Mar 13 15:27 met_em.d01.2005-08-28_12:00:00.nc   <br>
-rw-r--r-- 1 you user 5932836 Mar 13 15:27 met_em.d01.2005-08-28_18:00:00.nc   <br>
-rw-r--r-- 1 you user 5932836 Mar 13 15:28 met_em.d01.2005-08-29_00:00:00.nc   <br>
-rw-r--r-- 1 you user 5932836 Mar 13 15:27 met_em.d01.2005-08-29_06:00:00.nc   <br>
-rw-r--r-- 1 you user 5932836 Mar 13 15:27 met_em.d01.2005-08-29_12:00:00.nc   <br>
-rw-r--r-- 1 you user 5932836 Mar 13 15:27 met_em.d01.2005-08-29_18:00:00.nc   <br>
-rw-r--r-- 1 you user 5932836 Mar 13 15:28 met_em.d01.2005-08-30_00:00:00.nc   <br>
-rw-r--r-- 1 you user 5932836 Mar 13 15:27 met_em.d01.2005-08-30_06:00:00.nc   <br>
-rw-r--r-- 1 you user 5932836 Mar 13 15:27 met_em.d01.2005-08-30_12:00:00.nc   <br>
-rw-r--r-- 1 you user 5932836 Mar 13 15:27 met_em.d01.2005-08-30_18:00:00.nc   <br>
-rw-r--r-- 1 you user 5932836 Mar 13 15:28 met_em.d01.2005-08-31_00:00:00.nc   <br>
   <br>
这些文件都是NetCDF格式，可以使用ncdump工具来查看。   <br>
¾ ncdump -h met_em.d01.2005-08-28_00:00:00.nc   <br>
我们还可以查以图片的方式来查看这些数据。   <br>
恭喜你，到这里你已经成功了一半，下一步要运行WRFV2.2的本体计算部分了。   <br>
   <br>
You are now ready to run the WRFV2.   <br>
   <br>
   <br>
## 3.4. ～安装WRFV2.2～   <br>
   <br>
这里，如果是运行real case，流程示意图如下：   <br>
   <br>
如果是运行ideal case，最后部分的流程示意图如下：   <br>
   <br>
ideal case和real case的运行方法大同小异，在本指南里不对ideal case的安装运行进行详细描述。   <br>
   <br>
安装之前要仔细设计好自己要做的实验，选好实验case和运行条件。例如是real还是ideal；是single   <br>
还是palalell；是否需要nesting等等。因为每修改一次运行条件都要重新进行编译，这样就会浪费掉许   <br>
多时间。   <br>
   <br>
Examine the Source Code   <br>
在WRF/目录下...   <br>
¾ cd WRFV   <br>
检查目录中的内容。   <br>
¾ ls –all （ls –a亦可）   <br>
会有如下内容表示：   <br>
-rw-r--r-- 1 you user 16421 Oct 21 2005 Makefile   <br>
-rw-r--r-- 1 you user 7250 Nov 9 2005 README   <br>
-rw-r--r-- 1 you user 7238 Oct 5 2005 README.NMM   <br>
-rw-r--r-- 1 you user 2548 May 18 2004 README_test_cases   <br>
drwxr-xr-x 2 you user 4096 Apr 11 16:00 Registry   <br>
drwxr-xr-x 2 you user 4096 Nov 9 2005 arch   <br>
drwxr-xr-x 2 you user 4096 Nov 9 2005 chem   <br>
-rwxr-xr-x 1 you user 1078 May 24 2005 clean   <br>
-rwxr-xr-x 1 you user 6913 Oct 21 2005 compile   <br>
-rwxr-xr-x 1 you user 10636 May 7 2005 configure   <br>
drwxr-xr-x 2 you user 4096 Apr 20 20:01 dyn_em   <br>
drwxr-xr-x 2 you user 4096 Nov 9 2005 dyn_exp   <br>
drwxr-xr-x 2 you user 4096 Nov 9 2005 dyn_nmm   <br>
drwxr-xr-x 12 you user 4096 Nov 9 2005 external   <br>
drwxr-xr-x 2 you user 4096 Apr 11 16:02 frame   <br>
   <br>
   <br>
```   <br>
drwxr-xr-x 2 you user 4096 Mar 14 16:44 inc   <br>
drwxr-xr-x 2 you user 4096 Mar 14 16:44 main   <br>
drwxr-xr-x 2 you user 4096 Apr 11 16:13 phys   <br>
drwxr-xr-x 2 you user 4096 Mar 14 16:44 run   <br>
drwxr-xr-x 2 you user 8192 Mar 14 16:44 share   <br>
drwxr-xr-x 11 you user 4096 Nov 9 2005 test   <br>
drwxr-xr-x 3 you user 4096 Apr 11 16:01 tools   <br>
```   <br>
README文件里有与程序安装和运行有关的有用情报。运行之前最好阅读一次。   <br>
WRFV2目录下的文件分类：   <br>
Source code directories:   <br>
chem/ Directory containing modules for chemistry (not currently supported)   <br>
dyn_em/ Directory containing modules for dynamics in WRF ARW core   <br>
dyn_nmm/ Directory containing modules for dynamics in WRF NMM core   <br>
dyn_exp/ Directory for a 'toy' dynamical core   <br>
external/ Directory containing external packages， such as those for IO， time keeping and MPI   <br>
frame/ Directory containing modules for WRF framework   <br>
inc/ Directory containing include files   <br>
main/ Directory for main routines， such as wrf.F， and all executables after install   <br>
phys/ Directory for all physics modules   <br>
share/ Directory containing mostly modules for WRF mediation layer and WRF I/O   <br>
tools/ Directory containing tools   <br>
Scripts:   <br>
clean Script to clean created files， executables   <br>
compile Script for compiling WRF code   <br>
configure Script to configure the configure.wrf file for compile   <br>
Makefile Top-level makefile   <br>
Registry/ Directory for WRF Registry file   <br>
arch/ Directory where compile options are gathered   <br>
run/ Directory where one may run WRF   <br>
test/ Directory that contains 7 test case directories， may be used to run WRF   <br>
   <br>
Environment Variable-NetCDF   <br>
对NetCDF环境变量进行定义：   <br>
¾ NETCDF=/home/user/you;export NETCDF   <br>
   <br>
Configure WRFV   <br>
键入：   <br>
* ./configure   <br>
在此，会显示出计算机所支持的平台。   <br>
   <br>
   <br>
```   <br>
checking for perl5... no   <br>
checking for perl... found /usr/bin/perl (perl)   <br>
Will use NETCDF in dir: /home/user/you/netcdf-3.6.   <br>
PHDF5 not set in environment. Will configure WRF for use without.   <br>
$JASPERLIB or $JASPERINC not found in environment, configuring to build without grib2 I/O...   <br>
------------------------------------------------------------------------   <br>
Please select from among the following supported platforms.   <br>
```   <br>
1. PC Linux x86_64 (IA64 and Opteron), PGI compiler 5.2 or higher (Single-threaded, no nesting)   <br>
2. PC Linux x86_64 (IA64 and Opteron), PGI 5.2 or higher, DM-Parallel (RSL, MPICH, Allows   <br>
nesting)   <br>
3. PC Linux x86_64 (IA64 and Opteron), PGI 5.2 or higher DM-Parallel (RSL_LITE, MPICH,   <br>
Allows nesting, No periodic LBCs)   <br>
4. PC Linux x86_64 (IA64 and Opteron), PGI compiler 5.2 or higher (Single-threaded, RSL, Allows   <br>
nesting)   <br>
5. AMD x86_64 Intel xeon i686 ia32 Xeon Linux, ifort compiler (single-threaded, no nesting)   <br>
6. AMD x86_64 Intel xeon i686 ia32 Xeon Linux, ifort compiler (single threaded, allows nesting   <br>
using RSL without MPI)   <br>
7. AMD x86_64 Intel xeon i686 ia32 Xeon Linux, ifort compiler (OpenMP)   <br>
8. AMD x86_64 Intel xeon i686 ia32 Xeon Linux, ifort compiler SM-Parallel (OpenMP, allows   <br>
nesting using RSL without MPI)   <br>
9. AMD x86_64 Intel xeon i686 ia32 Xeon Linux, ifort+icc compiler DM-Parallel (RSL, MPICH,   <br>
allows nesting)   <br>
10. AMD x86_64 Intel xeon i686 ia32 Xeon Linux, ifort+gcc compiler DM-Parallel (RSL, MPICH,   <br>
allows nesting)   <br>
11. PC Linux x86_64 (IA64 and Opteron), PathScale 2.1 or higher (Single-threaded, no nesting)   <br>
12. PC Linux x86_64 (IA64 and Opteron), PathScale 2.1 or higher DM-Parallel (RSL_LITE,   <br>
PathScale MPICH, No periodic LBCs)   <br>
13. Cray XT3 Catamount/Linux x86_64 (Opteron), PGI 5.2 or higher DM-Parallel (RSL_LITE,   <br>
MPICH, Allows nesting, Periodic in X only)   <br>
   <br>
```   <br>
Enter selection [1-13] :   <br>
（根据计算机的差异，也许会显示出更多的平台选项）   <br>
```   <br>
作为练习，我们选择最为基本的（single-threaded，no nesting）。然后键入：   <br>
¾ 1   <br>
注意：如果需要进行并行计算或者嵌套，要注意括号里的说明项。例如，可以先选择 3 。在此步骤，将有   <br>
configure.wrf 文件被做成。如果有必要，对此文件的compile options/paths也要进行编辑。   <br>
   <br>
   <br>
Compile WRFV2   <br>
* ./compile   <br>
然后屏幕出现：   <br>
Usage:   <br>
compile wrf compile wrf in run dir (NOTE: no real.exe, ndown.exe, or ideal.exe generated)   <br>
or choose a test case (see README_test_cases for details) :   <br>
compile em_b_wave   <br>
compile em_esmf_exp   <br>
compile em_grav2d_x   <br>
compile em_hill2d_x   <br>
compile em_quarter_ss   <br>
compile em_real   <br>
compile em_squall2d_x   <br>
compile em_squall2d_y   <br>
compile exp_real   <br>
compile nmm_real   <br>
compile -h help message   <br>
   <br>
因为要运行WRF ARW real data case，所以选择em_real。   <br>
然后开始编译模块。   <br>
* ./compile em_real >& compile.log   <br>
运行会稍微花一点时间。（如果在./configure处选择了 3 ，你会有将近 30 分钟左右的时间来喝杯咖啡）   <br>
如果在进行过程当中自己弄出错了，或者要更改configure、compile等的选项，可以用 “clean -a”的命令来   <br>
清理所有的 built files，including configure.wrf。   <br>
* ./clean -a   <br>
然后开始重新编译WRFV2.2。   <br>
   <br>
编译结束后，打开compile.log确认是否有错误信息存在。如果编辑成功，在main/目录下会有以下的文件被   <br>
做成！   <br>
-rwxr-xr-x 1 you user 13612035 Mar 14 15:11 ndown.exe   <br>
-rwxr-xr-x 1 you user 13237353 Mar 14 15:11 nup.exe   <br>
-rwxr-xr-x 1 you user 10909533 Mar 14 15:11 real.exe   <br>
-rwxr-xr-x 1 you user 13237353 Mar 14 15:11 wrf.exe   <br>
ndown.exe 用于one-way nesting 。   <br>
nup.exe 用在WRF_3DVAR。   <br>
real.exe用于real data cases的初期化   <br>
wrf.exe用于WRF model integration   <br>
这些文件被从main/目录链接到了run/，test/em_real/目录下。   <br>
（如果运行其它idealized cases，方法一样。在./compile em_real >& compile.log处选择相应的文件选项。   <br>
不过之后会生成ideal.exe可执行文件）   <br>
   <br>
   <br>
## 3.5. ～运行WRFV2.2～   <br>
   <br>
Edit namelist.input   <br>
到run/ 或 test/em_real 目录下运行WRFV2.2。在这里，我选择后者。   <br>
¾ cd test/em_real   <br>
（如果在em_real下不能正常运行real.exe的话，可以到run目录下试试）   <br>
然后键入ls –l后，目录里包含有下面这些文件：   <br>
lrwxrwxrwx 1 you user 22 Mar 14 17:49 CAM_ABS_DATA -> ../../run/CAM_ABS_DATA   <br>
lrwxrwxrwx 1 you user 25 Mar 14 17:49 CAM_AEROPT_DATA -> ../../run/CAM_AEROPT_DATA   <br>
lrwxrwxrwx 1 you user 23 Mar 14 17:49 ETAMPNEW_DATA -> ../../run/ETAMPNEW_DATA   <br>
lrwxrwxrwx 1 you user 21 Mar 14 17:49 GENPARM.TBL -> ../../run/GENPARM.TBL   <br>
lrwxrwxrwx 1 you user 21 Mar 14 17:49 LANDUSE.TBL -> ../../run/LANDUSE.TBL   <br>
lrwxrwxrwx 1 you user 25 Mar 14 17:49 README.namelist -> ../../run/README.namelist   <br>
-rw-r--r-- 1 you user 5166 Dec 20 10:25 README.obs_fdda   <br>
lrwxrwxrwx 1 you user 19 Mar 14 17:49 RRTM_DATA -> ../../run/RRTM_DATA   <br>
lrwxrwxrwx 1 you user 22 Mar 14 17:49 SOILPARM.TBL -> ../../run/SOILPARM.TBL   <br>
lrwxrwxrwx 1 you user 21 Mar 14 17:49 VEGPARM.TBL -> ../../run/VEGPARM.TBL   <br>
lrwxrwxrwx 1 you user 22 Mar 14 17:49 grib2map.tbl -> ../../run/grib2map.tbl   <br>
lrwxrwxrwx 1 you user 21 Mar 14 17:49 gribmap.txt -> ../../run/gribmap.txt   <br>
-rw-r--r-- 1 you user 1762 Feb 19 2005 landFilenames   <br>
-rwxr-xr-x 1 you user 4663 Dec 19 04:13 namelist.input   <br>
-rw-r--r-- 1 you user 5647 Dec 15 06:28 namelist.input.chem   <br>
-rwxr-xr-x 1 you user 5732 Dec 19 04:13 namelist.input.grid_fdda   <br>
-rwxr-xr-x 1 you user 5902 Dec 19 04:13 namelist.input.jan00   <br>
-rwxr-xr-x 1 you user 5901 Dec 15 06:28 namelist.input.jun01   <br>
-rwxr-xr-x 1 you user 5655 Dec 19 04:13 namelist.input.obs_fdda   <br>
-rwxr-xr-x 1 you user 4804 Dec 19 04:13 namelist.input.si   <br>
-rwxr-xr-x 1 you user 6108 Dec 19 04:13 namelist.input.wps   <br>
lrwxrwxrwx 1 you user 20 Mar 14 17:49 ndown.exe -> ../../main/ndown.exe   <br>
lrwxrwxrwx 1 you user 18 Mar 14 17:49 nup.exe -> ../../main/nup.exe   <br>
lrwxrwxrwx 1 you user 25 Mar 14 17:49 ozone.formatted -> ../../run/ozone.formatted   <br>
lrwxrwxrwx 1 you user 29 Mar 14 17:49 ozone_lat.formatted -> ../../run/ozone_lat.formatted   <br>
lrwxrwxrwx 1 you user 30 Mar 14 17:49 ozone_plev.formatted -> ../../run/ozone_plev.formatted   <br>
lrwxrwxrwx 1 you user 19 Mar 14 17:49 real.exe -> ../../main/real.exe   <br>
-rw-r--r-- 1 you user 10240 Dec 9 16:40 run_1way.tar   <br>
-rw-r--r-- 1 you user 20480 Jan 20 2006 run_2way.tar   <br>
-rw-r--r-- 1 you user 10240 Jan 20 2006 run_restart.tar   <br>
lrwxrwxrwx 1 you user 17 Mar 14 17:49 tr49t67 -> ../../run/tr49t67   <br>
lrwxrwxrwx 1 you user 17 Mar 14 17:49 tr49t85 -> ../../run/tr49t85   <br>
lrwxrwxrwx 1 you user 17 Mar 14 17:49 tr67t85 -> ../../run/tr67t85   <br>
   <br>
   <br>
```   <br>
lrwxrwxrwx 1 you user 25 Mar 14 17:49 urban_param.tbl -> ../../run/urban_param.tbl   <br>
lrwxrwxrwx 1 you user 18 Mar 14 17:49 wrf.exe -> ../../main/wrf.exe   <br>
```   <br>
新生成的文件的用途和说明，如下表归纳所示：   <br>
ETAMPNEW_DATA Variables for the Ferrier (new Eta) microphysics scheme, (binary file).   <br>
CAM_ABS_DATA CAM radiation variables (binary files).   <br>
CAM_AEROPT_DATA Details available in phys/module_ra_cam.F   <br>
ozone.formatted   <br>
ozone_lat.formatted   <br>
ozone_plev.formatted   <br>
Data for the 16 longwave spectral bands used in RRTM (binary file).   <br>
RRTM_DATA   <br>
Details available in phys/module_ra_rrtm.F   <br>
tr49t67 Data for the GFDL radiation scheme (binary files).   <br>
tr49t85 Details available in phys/module_ra_gfdleta.F   <br>
tr67t85   <br>
Land surface parameters required by the LSM models. The file is an ASCII table.   <br>
LANDUSE.TBL   <br>
Details available in phys/module_physics_init.F   <br>
GENPARM.TBL Soil and vegetation parameters required by the Noah LSM model. The files are   <br>
ASCII tables.   <br>
SOILPARM.TBL Details available in phys/module_sf_noahlsm.F and phys/module_sf_urban.F   <br>
VEGPARM.TBL   <br>
urban_param.tbl   <br>
grib2map.tbl   <br>
gribmap.txt   <br>
Tables required for creating GRIB1 and GRIB2 output.   <br>
   <br>
```   <br>
namelist.input Sample namelists to set up and run real.exe and wrf.exe   <br>
namelist.input.jan00 namelist.input will always be used by real.exe and wrf.exe   <br>
namelist.input.jun01 .jan00 and .jun01 have been set up for our default test cases   <br>
namelist.input.wps .wps and .SI are samples of different setups required depending on the   <br>
preprocesssor used.   <br>
namelist.input.SI Details of all the namelist options are available in the README.namelist file.   <br>
```   <br>
针对本次的OnLine Tutorial case，编辑namelist.input。归纳一下，主要修改以下几点：   <br>
Start date: 2005082800   <br>
End date: 2005083100   <br>
Interval: 21600 sec (6 hours)   <br>
Grid points in EW direction: 75   <br>
Grid points in SN direction: 70   <br>
Number of vertical levels: 31   <br>
Grid distance: 30km   <br>
namelist.input文件被用在了real.exe和wrf.exe可执行文件的运行等处。   <br>
   <br>
   <br>
Link   <br>
把在WPS处做成的met_em.d01_0508* files链接到WRFV2/run/ 或者WRFV2/test/em_real/ 目录下。   <br>
¾ ln –sf /home/user/you/WRF/WPS/met_em.d01.2005-08*.   <br>
使用方法可以参考ln 命令   <br>
   <br>
Run real.exe   <br>
进行single processor运行。例如本次的演习。   <br>
* ./real.exe   <br>
如果是DM(distributed memory) parallel systems，就会需要mpirun command。例如，如果是Linux cluster，   <br>
实行4CPUs的MPI code的命令就是：   <br>
* mpirun –np 4 real.exe   <br>
可以根据自己的条件选择CPU的个数。同时不要忘记，在./configure 处要选择与之相对应的平台。   <br>
在键入./real.exe 后，最好不要打扰计算机的运行。如果运行成功的话，最后会有wrfbdy_d01和wrfinput_d01   <br>
文件生成。   <br>
   <br>
Check Your rsl Files   <br>
如果进行了并行计算，运行完real.exe或者wrf.exe之后，要检查rsl.out.*和rsl.error.*（对于每个processor，都   <br>
会出现rsl.out和rsl.error）。在rsl.out.0000和rsl.error.0000里包含了重要的情报。如果运行失败，error message   <br>
有可能存在于这些文件当中的某一个文件里。同时，在namelist.input 里有debug_level一项。这一项对应的   <br>
有效数值为 0 ， 50 ， 100 ， 200 ， 300 等，数值越大，在rsl.out.*和rsl.error.*里输出的信息就越详细，越有利   <br>
于寻找错误的根源。如果多次运行都不能成功，请考虑使用此项。   <br>
使用head –n 30 rsl.out.* 和tail –n 30 rsl.out.* 命令来查看rsl的文件头 30 行和文件尾 30 行。   <br>
如果运行real.exe成功，则在rsl.out.0000的最后会有提示：   <br>
   <br>
SUCCESS COMPLETE REAL_EM INIT   <br>
   <br>
因为wrf.exe也会生成同名的log文件，所以把上面的rsl.out.*和rsl.error.*移动到其他目录，或者删掉。   <br>
   <br>
Run wrf.exe   <br>
* ./wrf.exe   <br>
如果是 single processor machine，输入./wrf.exe。   <br>
如果是DM(distributed memory) parallel systems，会有需要mpirun command的场合。例如，如果是Linux   <br>
cluster，实行4CPUs的MPI code的命令就是：   <br>
* mpirun –np 4 wrf.exe   <br>
   <br>
如果全部进行顺利的话，新的wrfout_d01 file将会被做成。   <br>
从 2005082800 到 2005083100 的 72 小时份的文件将被做成。用ncdump可以查看wrfout_d01 file里的信息。   <br>
* ncdump –h wrfout_d01_2005-08-28_00:00:00 参照   <br>
   <br>
wrf: SUCCESS COMPLETE WRF   <br>
   <br>
   <br>
# 4．＜WRF_SI+WRFV2.2的安装运行＞   <br>
   <br>
请参照网页http://www.mmm.ucar.edu/wrf/OnLineTutorial/WRFSI/，内有详细的Online Tutorial。   <br>
本章的内容是参照上述网页的内容进行翻译，并结合自己在操作过程中遇到的困难进行归纳整理完成的。   <br>
   <br>
## 4.0. ～收集数据～   <br>
   <br>
Get Source Code   <br>
和WPS+为WRFV2.2一样，把所需要的，最新的Source_Codes收集在一起，分类放到同一个目录下。   <br>
下载WRF_SI和WRFV2.2的source code。   <br>
在/home/user/you/目录下建立一个名为Source_Codes_and_Graphics_Software的源码存放区。例如：   <br>
¾ mkdir Source_Codes_and_Graphics_Software   <br>
并且为以防万一，把收集到的Source_Codes刻成CD或者DVD，作为备份。   <br>
   <br>
Unpack the Code   <br>
在/home/user/you/目录下建立一个名为WRF的工作目录：   <br>
* mkdir WRF   <br>
把下载到的wrfsi_v2.1.2.tar.gz和WRFV2.TAR.gz文件复制到新建的WRF目录下。然后解压和展开。   <br>
* cp wrfsi_v2.1.2.tar.gz /home/user/you/WRF/ （可参考cp命令的使用方法）   <br>
* cp WRFV2.TAR.gz /home/user/you/WRF/   <br>
解压：   <br>
* gunzip wrfsi_v2.1.2.tar.gz （对文件进行解压）   <br>
* gunzip WRFV2.TAR.gz   <br>
打开TAR file。   <br>
* tar –xvf wrfsi_v2.1.2.tar （不要忘记 –xvf ）   <br>
* tar –xvf WRFV2.TAR   <br>
于是，会有wrfsi/和WRFV2/目录被做成。   <br>
   <br>
## 4.1. ～安装WRF_SI～   <br>
   <br>
### 4.1.1． ～定义环境变量～   <br>
Examine the Source Code   <br>
在/home/user/you/WRF/目录下   <br>
* cd wrfsi   <br>
检查目录中的内容。   <br>
* ls –all （ls –a亦可）   <br>
会有如下内容表示：   <br>
total 156   <br>
drwxr-xr-x 9 you user 4096 Mar 10 08:08.   <br>
drwxr-xr-x 3 you user 4096 May 25 19:04 ..   <br>
   <br>
   <br>
```   <br>
-rw-r--r-- 1 you user 15975 Jun 19 2004 CHANGES   <br>
-rw-r--r-- 1 you user 11166 Mar 12 2003 HOW_TO_RUN.txt   <br>
-rw-r--r-- 1 you user 4405 Jan 18 2003 INSTALL   <br>
-rw-r--r-- 1 you user 4101 Dec 11 2003 Makefile   <br>
-rw-r--r-- 1 you user 30421 Jan 28 2005 README   <br>
-rw-r--r-- 1 you user 12661 Mar 8 2005 README.wrfsi_nl   <br>
drwxr-xr-x 7 you user 4096 Aug 23 2005 data   <br>
drwxr-xr-x 2 you user 4096 Mar 6 07:18 etc   <br>
drwxr-xr-x 7 you user 4096 Aug 3 2005 extdata   <br>
drwxr-xr-x 3 you user 4096 Aug 3 2005 graphics   <br>
drwxr-xr-x 5 you user 4096 Mar 10 08:11 gui   <br>
-rwxr-xr-x 1 you user 27153 Mar 10 08:08 install_wrfsi.pl   <br>
drwxr-xr-x 12 you user 4096 Aug 3 2005 src   <br>
drwxr-xr-x 3 you user 4096 Aug 23 2005 util   <br>
```   <br>
在CHANGES文件里写入了最近更新的全部code。   <br>
HOW_TO_RUN.txt·INSTALL·README·README.wrfsi_nl 文件里有与程序安装和运行有关的有用情   <br>
报。运行之前最好阅读一次。install_wrfsi.pl 是用来编译WRF_SI或安装perl script用的。   <br>
   <br>
Set Environment Variables   <br>
安装和运行WRF_SI之前要先记述环境变量。   <br>
无论是定义环境变量，还是使用初期值，在/home/user/you/WRF/wrfsi/中的config_paths文件中都可以找得   <br>
到。可以用cat和vi命令：cat config_paths进行阅览，vi config_paths进行修改。   <br>
正确定义环境变量，对正确的安装和运行WRF_SI程序来说很重要。   <br>
注意：在这里没有对包含有Input GriB 数据文件的文件夹进行环境变量的定义。这个定义将在使用namelist   <br>
file that the grib_prep 时输入。   <br>
   <br>
NetCDF   <br>
安装WRFV2之前，要对NetCDF的环境变量进行定义。   <br>
 NETCDF=/home/user/you;export NETCDF   <br>
   <br>
SOURCE_ROOT   <br>
定义source root directory路径。   <br>
 SOURCE_ROOT=/home/user/you/WRF/wrfsi;export SOURCE_ROOT   <br>
   <br>
INSTALLROOT   <br>
定义install root directory路径。   <br>
 INSTALLROOT=/home/user/you/WRF/wrfsi;export INSTALLROOT   <br>
   <br>
   <br>
### EXR_DATAROOT   <br>
   <br>
定义degribed （媒体）的directory路径。   <br>
 EXT_DATAROOT=/home/user/you/WRF/wrfsi/extdata;export EXT_DATAROOT   <br>
   <br>
TEMPLATES   <br>
放置templates directory的地方。这个目录里包含有为修正自己构筑的case时所需要的SI namelist 文件。   <br>
仅和运行SI（不使用GUI）时相关联。   <br>
 TEMPLATES=/home/user/you/WRF/wrfsi/templates;export TEMPLATES   <br>
   <br>
DATAROOT & MOAD_DATAROOT   <br>
DARAROOT可以把含有复数的sundirectory（MOAD_DATAROOT）放置在最上部的directory。如果那里   <br>
仅有一个MOAD_DATAROOT时，MOAD_DATAROOT可以和DATAROOT directory相同。   <br>
 DATAROOT=/home/user/you/WRF/wrfsi/domains;export DATAROOT   <br>
但是，不可设定为wrfsi/data directory。   <br>
MOAD_DATAROOT是用来运行个别案例的目录。对于此环境变量，并没有设定其初期值。通常是如下   <br>
定义：（现在并不需要输入下面的语句，仅作参考用。对此环境变量的指定还会在后面进行描述。）   <br>
 MOAD_DATAROOT=/home/user/you/WRF/wrfsi/domains/case-name;export MOAD_DATAROOT   <br>
   <br>
GEOG_DATAROOT   <br>
此环境变量可以指定自己的terrestrial input data（terrain，landuse，etc.）的目录。   <br>
总之，在此处（即为GEOG），必须事先放入最初下载的Source_Codes。一共 21 个gz文件。这些数据可以   <br>
从WRF_SI处下载得到。把数据放到/WRF/wrfsi/extdata/GEOG内，然后用前面用过的gunzip 和 tar 命令逐   <br>
个进行解冻。定义：   <br>
 GEOG_DATAROOT=/home/user/you/WRF/wrfsi/extdata/GEOG;export GEOG_DATAROOT   <br>
   <br>
NCL_COMMAND   <br>
如果要使用GUI，我们还要进行环境变量的设定。使用GUI，可以制作出terrestrial input data的画像。   <br>
 NCL_COMMAND=/home/user/you/ncl;export NCL_COMMAND   <br>
   <br>
```   <br>
为方便使用，我们可以将这些环境变量也登录到 .bashrc里。   <br>
1 ） 在/home/user/you/目录下输入   <br>
* vi .bashrc   <br>
2 ） 输入上面除了MOAD_DATAROOT以外的８个环境变量。其中，NetCDF在上面已经登   <br>
录过。然后键入 <Esc> : w q保存退出。   <br>
3 ） 键入下面命令即可定义环境变量：   <br>
* source ~/.bashrc   <br>
```   <br>
   <br>
### 4.1.2． ～安装 WRF_SI～   <br>
   <br>
Install WRF_SI   <br>
* perl install_wrfsi.pl   <br>
在画面上会出现下面的对话：   <br>
Routine: Install_wrfsi   <br>
Path to perl: /usr/bin/perl   <br>
--path_to_netcdf not specified， attempting to determine...   <br>
netCDF path found from environment variable.   <br>
Do you want to install the WRF SI graphical user interface? [y|n]:   <br>
   <br>
在此处，如果选择“n”的话，只会安装WRF_SI。选择“y”，会一起安装GUI。   <br>
我们在此选择“y”。（例：如下表示。“n”，“y”）   <br>
* y   <br>
   <br>
如果安装成功，在下面的目录里会有下面几个可执行文件生成。   <br>
* cd /home/user/you/WRF/wrfsi/bin   <br>
* ls –l   <br>
-rwxr-xr-x 1 you user 870534 Jul 12 16:01 grib_prep.exe   <br>
-rwxr-xr-x 1 you user 1901081 Jul 12 16:02 gridgen_model.exe   <br>
-rwxr-xr-x 1 you user 1760763 Jul 12 16:01 hinterp.exe   <br>
-rwxr-xr-x 1 you user 1647080 Jul 12 16:02 siscan   <br>
-rwxr-xr-x 1 you user 1754324 Jul 12 16:02 staticpost.exe   <br>
-rwxr-xr-x 1 you user 2018603 Jul 12 16:01 vinterp.exe   <br>
还有，检查一下在下面的目录里是否有makefile生成。   <br>
* cd /home/user/you/WRF/wrfsi/src/include   <br>
makefile_alpha.inc.in   <br>
＊ 如果install 失败了... ... 在ARW OnLine Tutorial里登载了一些error解决办法，请参考使用。   <br>
   <br>
### 4.1.3． ～使用WRF_SI的GUI～   <br>
Run WRF_SI with GUI   <br>
如果想运行GUI，会使用到X-window软件。我使用的是名为EXODUS的软件，需要通过SSH软件和超算进   <br>
行连接。再有，这里的记述的方法也许仅适用于我所使用的超算，仅供参考。WRF_SI web site上的方法自   <br>
己没有研究过，在这里不能详细写出，请原谅。在输入下面语句之前要先打开X-window。   <br>
 ssh –Y login.wrftest.ac.cn (自己的host name)   <br>
 export DISPLAY=192.168.111.111:0.0 （自己的PC的IP地址）   <br>
 LANG=C   <br>
 export LANG   <br>
 qmon &   <br>
（到这里是连接UNIX系统和X-window的命令语句，在使用画图软件GrADS时也会用到）   <br>
   <br>
   <br>
### 然后打开WRF_SI的GUI系统：   <br>
   <br>
 cd /home/user/you/WRF/wrfsi   <br>
 ./wrf_tools   <br>
在画面上会有GUI显现。详细信息请参照WRF_SI web site。   <br>
（以上的操作方法有可能会和其它软件不同。例如，x-win，x-winPro等软件就不需要什么特殊的设定。跳   <br>
过4.1.3节，仍可继续运行WRFV2。）   <br>
   <br>
## 4.2． ～运行WRF_SI～   <br>
   <br>
WRF_SI里主要有三个步骤，并且每一步都需要对相应的namelist文件进行编辑：   <br>
STEP1：设定领域 ——〉 编辑wrfsi.nl的 1 、 2 部分   <br>
STEP2：指定气象数据 ——〉 编辑grib_prep.nl文件   <br>
STEP3：向领域内插入气象数据 ——〉 编辑wrfsi.nl的 3 、 4 部分   <br>
   <br>
Run WRF_SI   <br>
STEP1: Localize model domain and create static files   <br>
在此处设定对象领域，建立为运行WRF所必须的静态目录。到此阶段，各模式领域的设定仅一次即可。   <br>
Localization所必需的script: /home/user/you/WRF/wrfsi/etc/window_domain_rt.pl   <br>
Namelist: wrfsi.nl   <br>
   <br>
此处把存放模拟用的数据的目录命名为OnlineTut 。在/WRF/wrfsi/下：   <br>
 cd domains   <br>
 mkdir OnlineTut   <br>
设定环境变量（在上面Set Environment Variables处描述过）   <br>
 MOAD_DATAROOT=/home/user/you/WRF/wrfsi/domains/OnlineTut;export MOAD_DATAROOT   <br>
做成TEMPLATE。   <br>
 cd /home/user/you/WRF/wrfsi/templates   <br>
 cp –r default OnlineTut   <br>
 chmod –R u+w OnlineTut   <br>
 cd OnlineTut   <br>
   <br>
Edit wrfsi.nl   <br>
wrfsi.nl文件被用于step1（localization）和step3（interpolation of data）。在wrfsi.nl网页中：红色部分与step1，   <br>
紫色部分与step3相关联。关于namelist中变量的详细内容请参照README.wrfsi_nl，附录 2 的中文版也许也   <br>
会有很大帮助。   <br>
现在，我们开始编译wrfsi.nl文件。建议两部分一起编辑。   <br>
进入/home/user/you/WRF/wrfsi/templates/下的OnlineTut目录。使用vi命令对wrfsi.nl进行编辑。（<Esc>变   <br>
换输入形式；x 键可删除字符；i或a键可插入字符）   <br>
1.通过编辑hgridspec 来设定所使用的模式。我们将模拟Hurricane Katrina。   <br>
2.在此，关键是要核对通向terrestrial data的path及其它的环境变量是否被正确定以这两个方面内容。还要检   <br>
   <br>
   <br>
查确认sfcfiles的内容。   <br>
3.interp_control部分，设定内插data。对于本次的模拟练习，要检查确认INIT_ROOT和LBC_ROOT是否被   <br>
正确定义。使用AV N d a t a时，这些变量都需要被设定。如果使用不同的模式，变更sigma level时，在此   <br>
步骤下还要变更LEVELS。对此次的数值模拟，我们使用的初期值为31 levels。   <br>
4.检查si_path是否被定义在intermediate files（/home/user/you/WRF/wrfsi/extdata/）处。   <br>
通过对模式构成的编辑，调整模式领域的适用准备。   <br>
 cd /home/user/you/WRF/wrfsi   <br>
 ./etc/window_domain_rt.pl –w wrfsi –t /home/user/you/WRF/wrfsi/templates/OnlineTut   <br>
运行后，有这样的画面出现。中间会停顿十几秒，最后表示的是设定完成的提示信息：   <br>
   <br>
*****************************************   <br>
******* Domain Localization complete ******   <br>
*****************************************   <br>
在log file（/home/user/you/WRF/wrfsi/domains/OnlineTut/log/localize_domain.log.date）处可以查看运行是否   <br>
成功。（date是刚才的运行时间）   <br>
   <br>
如果static file被做成了的话，就表示运行成功了。   <br>
¾ /home/user/you/WRF/wrfsi/domains/OnlineTut/static/static.wrfsi.d01   <br>
可以使用ncdump –h /home/user/you/WRF/wrfsi/domains/OnlineTut/static/static.wrfsi.d01，来浏览有什么   <br>
内容被写进了文件。如果这个文件被成功地建立了，就可以向输入GRIB 的deGrib移动了。   <br>
   <br>
STEP2: deGrib GRIB files   <br>
对所有的GRIB 数据文件都需要进行deGrib。   <br>
Script needs to deGrib GRIB file: /home/user/you/WRF/wrfsi/etc/grib_prep.pl   <br>
Namelist: /home/user/you/WRF/wrfsi/extdata/static/grib_prep.nl   <br>
运行自己所需要的数值模拟，必须有相对应的GRIB数据文件。作为本次的模拟练习，我们可以从网上下载   <br>
到AVN test data for the Katrina case。   <br>
Katrina case   <br>
· Global AVN/GFS (90.0 to -90.0 by 1.0 latitude & 0.0 to 360.0 by 1.0 longitude)   <br>
· List of field available in these files   <br>
· Start date: 2005082800   <br>
· End date: 2005083100   <br>
· Frequency: 6 hourly   <br>
·   <br>
把上面下载到的文件放入其专用的文件夹里，例如创建 ../WRF/wrfsi/case-name/。（推荐把各种模拟用的气   <br>
象数据资料放到各自专用的文件夹里，每次模拟都在各自的文件夹里运行）   <br>
在/home/user/you/WRF/wrfsi/下，建立一个名为Katrina 的目录，放入下载到的GRIB 数据文件。   <br>
¾ mkdir Katrina   <br>
把下载到的Katrina_AVN_input.tar.gz文件复制到Katrina目录里。然后解压。   <br>
¾ tar xvfz Katrina_AVN_input.tar.gz   <br>
   <br>
   <br>
Edit grib_prep.nl   <br>
在/home/user/you/WRF/wrfsi/extdata/static/目录下，使用vi编辑grib_prep.nl文件。   <br>
编辑gpinput_defs部分的时候，要注意上下文之间的位置关系，各种SRC* 都是上下相互对应的。   <br>
当我们有AV N d a t a的时候，对3th path in the SRCPATH变量必须定义到含有GRIB input file的directory。   <br>
具体的编辑方法可参考下面的例子（已编辑完）：   <br>
&filetimespec   <br>
START_YEAR = 2005   <br>
START_MONTH = 08   <br>
START_DAY = 28   <br>
START_HOUR =00   <br>
START_MINUTE = 00   <br>
START_SECOND = 00   <br>
END_YEAR = 2005   <br>
END_MONTH = 08   <br>
END_DAY = 31   <br>
END_HOUR = 00   <br>
END_MINUTE = 00   <br>
END_SECOND = 00   <br>
INTERVAL = 21600   <br>
/   <br>
   <br>
```   <br>
&gpinput_defs   <br>
SRCNAME = 'ETA', 'GFS', 'AV N', 'RUCH', 'NNRP', 'NNRPSFC', 'SST'   <br>
SRCVTAB = 'ETA', 'GFS', 'AV N', 'RUCH', 'NNRPSFC', 'NNRPSFC', 'SST'   <br>
SRCPATH = '/public/data/grids/eta/40km_eta212_isobaric/grib',   <br>
'/public/data/grids/gfs/0p5deg/grib',   <br>
'/home/user/you/WRF/wrfsi/Katrina', （刚才的解压目录）   <br>
'/rt0/rucdev/nrelwind/run/maps_fcst',   <br>
'/path/to/nnrp/grib',   <br>
'/path/to/nnrp/sfc/grib',   <br>
'/public/data/grids/ncep/sst/grib'   <br>
SRCCYCLE = 6, 6, 6 , 6, 12, 12, 24   <br>
SRCDELAY = 3, 4, 4 , 3, 0, 0, 12   <br>
/   <br>
```   <br>
键入<Esc> : w q保存退出。准备运行script。   <br>
¾ cd /home/user/you/WRF/wrfsi   <br>
¾ ./etc/grib_prep.pl -s 2005082800 -l 72 -t 6 AVN （ l 为小写的L）   <br>
（特别要注意选项的含义：-s=start time， -l=forecast length， -t=interval）   <br>
运行结束后，检查/home/user/you/WRF/wrfsi/extdata/log/gp_AVN.200508280.log文件。   <br>
   <br>
   <br>
如果成功了，将在/home/user/you/WRF/wrfsi/extdata/extprd里有生成intermediate files文件。   <br>
（一般情况下，如果没有对上面的文件进行正确编辑，则不会产生下面的文件。）   <br>
-rw-rw-rw- 1 you user 38867544 Mar 20 12:22 AVN:2005-08-28_00   <br>
-rw-rw-rw- 1 you user 38867544 Mar 20 12:22 AVN:2005-08-28_06   <br>
-rw-rw-rw- 1 you user 38867544 Mar 20 12:22 AVN:2005-08-28_12   <br>
-rw-rw-rw- 1 you user 38867544 Mar 20 12:22 AVN:2005-08-28_18   <br>
-rw-rw-rw- 1 you user 38867544 Mar 20 12:22 AVN:2005-08-29_00   <br>
-rw-rw-rw- 1 you user 38867544 Mar 20 12:22 AVN:2005-08-29_06   <br>
-rw-rw-rw- 1 you user 38867544 Mar 20 12:22 AVN:2005-08-29_12   <br>
-rw-rw-rw- 1 you user 38867544 Mar 20 12:22 AVN:2005-08-29_18   <br>
-rw-rw-rw- 1 you user 38867544 Mar 20 12:22 AVN:2005-08-30_00   <br>
-rw-rw-rw- 1 you user 38867544 Mar 20 12:22 AVN:2005-08-30_06   <br>
-rw-rw-rw- 1 you user 38867544 Mar 20 12:22 AVN:2005-08-30_12   <br>
-rw-rw-rw- 1 you user 38867544 Mar 20 12:22 AVN:2005-08-30_18   <br>
-rw-rw-rw- 1 you user 38867544 Mar 20 12:22 AVN:2005-08-31_00   <br>
此处成功了的话，就表示准备好了向在step1（localization）处做成的WRF model领域内插数据的工作。   <br>
   <br>
STEP3: Interpolate meteorological data   <br>
在此处，向模式领域里插入气象数据。将会运行hinterp和vinterp部分。   <br>
Script needed: /home/user/you/WRF/wrfsi/etc/wrfprep.pl   <br>
Namelist: wrfsi.nl   <br>
＊ 如果在step1里，已经对wrfsi.nl编辑过了，此处就没有必要再编辑了。   <br>
＊ 如果，在运行wrfprel.pl之前，想要更改inter_control或si_paths部分，对   <br>
/home/user/you/WRF/wrfsi/domains/OnlineTut/static/wrfsi.nl也要编辑。不是复本   <br>
/home/user/you/WRF/wrfsi/templates/OnlineTut/wrfsi.nl。   <br>
   <br>
准备运行script。   <br>
¾ cd /home/user/you/WRF/wrfsi   <br>
¾ ./etc/wrfprep.pl -s 2005082800 -f 72 -t 6   <br>
这是wrfsi.nl里的时间设定部分（filetimespec），可以用命令文进行覆盖。（特别要注意选项的含义：-s=start   <br>
time， -f=forecast length， -t=interval）   <br>
在运行当中，你会看到如下画面。   <br>
Routine: wrfprep.pl   <br>
INSTALLROOT = /home/user/you/WRF/wrfsi   <br>
MOAD_DATAROOT = /home/user/you/WRF/wrfsi/domains/OnlineTut   <br>
Start time: 2005/08/28 00:00:00   <br>
End time: 2005/08/31 00:00:00   <br>
CYCLE.0524000000072   <br>
ictime = 2005-08-28_00   <br>
lbctime = 2005-08-28_06   <br>
   <br>
   <br>
```   <br>
lbctime = 2005-08-28_12   <br>
lbctime = 2005-08-28_18   <br>
lbctime = 2005-08-29_00   <br>
lbctime = 2005-08-29_06   <br>
lbctime = 2005-08-29_12   <br>
lbctime = 2005-08-29_18   <br>
lbctime = 2005-08-30_00   <br>
lbctime = 2005-08-30_06   <br>
lbctime = 2005-08-30_12   <br>
lbctime = 2005-08-30_18   <br>
lbctime = 2005-08-31_00   <br>
/home/user/you/WRF/wrfsi/domains/OnlineTut/siprd/hinterp.d01.2005-08-31_00:00:00   <br>
/home/user/you/WRF/wrfsi/domains/OnlineTut/siprd/wrf_real_input_em.d01.2005-08-31_00:00:00   <br>
```   <br>
运行结束后，检查一下/home/user/you/WRF/wrfsi/domains/OnlineTut/log里的log file。   <br>
有以下的文件出现即可。   <br>
2005082800.hinterp   <br>
2005082800.vinterp   <br>
2005082800.wrfprep   <br>
   <br>
成功了的话，在/home/user/you/WRF/wrfsi/domains/OnlineTut/siprd里将有下面几个文件生成。   <br>
-rw-r--r-- 1 you user 185 Mar 21 15:13 CYCLE.0524000000072   <br>
-rw-r--r-- 1 you user 2821104 Mar 21 15:13 hinterp.d01.2005-08-28_00:00:00   <br>
-rw-r--r-- 1 you user 2821104 Mar 21 15:13 hinterp.d01.2005-08-28_06:00:00   <br>
-rw-r--r-- 1 you user 2821104 Mar 21 15:13 hinterp.d01.2005-08-28_12:00:00   <br>
-rw-r--r-- 1 you user 2821104 Mar 21 15:14 hinterp.d01.2005-08-28_18:00:00   <br>
-rw-r--r-- 1 you user 2821104 Mar 21 15:14 hinterp.d01.2005-08-29_00:00:00   <br>
-rw-r--r-- 1 you user 2821104 Mar 21 15:14 hinterp.d01.2005-08-29_06:00:00   <br>
-rw-r--r-- 1 you user 2821104 Mar 21 15:14 hinterp.d01.2005-08-29_12:00:00   <br>
-rw-r--r-- 1 you user 2821104 Mar 21 15:14 hinterp.d01.2005-08-29_18:00:00   <br>
-rw-r--r-- 1 you user 2821104 Mar 21 15:14 hinterp.d01.2005-08-30_00:00:00   <br>
-rw-r--r-- 1 you user 2821104 Mar 21 15:14 hinterp.d01.2005-08-30_06:00:00   <br>
-rw-r--r-- 1 you user 2821104 Mar 21 15:14 hinterp.d01.2005-08-30_12:00:00   <br>
-rw-r--r-- 1 you user 2821104 Mar 21 15:14 hinterp.d01.2005-08-30_18:00:00   <br>
-rw-r--r-- 1 you user 2821104 Mar 21 15:14 hinterp.d01.2005-08-31_00:00:00   <br>
-rw-r--r-- 1 you user 368 Mar 21 15:14 hinterp.global.metadata   <br>
-rw-r--r-- 1 you user 4338960 Mar 21 15:14 wrf_real_input_em.d01.2005-08-28_00:00:00   <br>
-rw-r--r-- 1 you user 4338576 Mar 21 15:14 wrf_real_input_em.d01.2005-08-28_06:00:00   <br>
-rw-r--r-- 1 you user 4338576 Mar 21 15:14 wrf_real_input_em.d01.2005-08-28_12:00:00   <br>
-rw-r--r-- 1 you user 4338576 Mar 21 15:14 wrf_real_input_em.d01.2005-08-28_18:00:00   <br>
   <br>
   <br>
```   <br>
-rw-r--r-- 1 you user 4338576 Mar 21 15:14 wrf_real_input_em.d01.2005-08-29_00:00:00   <br>
-rw-r--r-- 1 you user 4338576 Mar 21 15:14 wrf_real_input_em.d01.2005-08-29_06:00:00   <br>
-rw-r--r-- 1 you user 4338576 Mar 21 15:14 wrf_real_input_em.d01.2005-08-29_12:00:00   <br>
-rw-r--r-- 1 you user 4338576 Mar 21 15:14 wrf_real_input_em.d01.2005-08-29_18:00:00   <br>
-rw-r--r-- 1 you user 4338576 Mar 21 15:14 wrf_real_input_em.d01.2005-08-30_00:00:00   <br>
-rw-r--r-- 1 you user 4338576 Mar 21 15:14 wrf_real_input_em.d01.2005-08-30_06:00:00   <br>
-rw-r--r-- 1 you user 4338576 Mar 21 15:13 wrf_real_input_em.d01.2005-08-30_12:00:00   <br>
-rw-r--r-- 1 you user 4338576 Mar 21 15:13 wrf_real_input_em.d01.2005-08-30_18:00:00   <br>
-rw-r--r-- 1 you user 4338576 Mar 21 15:13 wrf_real_input_em.d01.2005-08-31_00:00:00   <br>
```   <br>
到此处你也成功了的话，我们就已经做好运行WRF ARM模式的准备好了。   <br>
   <br>
## 4.3. ～安装WRFV2.2～   <br>
   <br>
Examine the Source Code   <br>
¾ cd WRFV2   <br>
在这个目录下存在有以下的文件和目录：   <br>
-rw-r--r-- 1 you user 16421 Oct 21 2005 Makefile   <br>
-rw-r--r-- 1 you user 7250 Nov 9 2005 README   <br>
-rw-r--r-- 1 you user 7238 Oct 5 2005 README.NMM   <br>
-rw-r--r-- 1 you user 2548 May 18 2004 README_test_cases   <br>
drwxr-xr-x 2 you user 4096 Apr 11 16:00 Registry   <br>
drwxr-xr-x 2 you user 4096 Nov 9 2005 arch   <br>
drwxr-xr-x 2 you user 4096 Nov 9 2005 chem   <br>
-rwxr-xr-x 1 you user 1078 May 24 2005 clean   <br>
-rwxr-xr-x 1 you user 6913 Oct 21 2005 compile   <br>
-rwxr-xr-x 1 you user 10636 May 7 2005 configure   <br>
drwxr-xr-x 2 you user 4096 Apr 20 20:01 dyn_em   <br>
drwxr-xr-x 2 you user 4096 Nov 9 2005 dyn_exp   <br>
drwxr-xr-x 2 you user 4096 Nov 9 2005 dyn_nmm   <br>
drwxr-xr-x 12 you user 4096 Nov 9 2005 external   <br>
drwxr-xr-x 2 you user 4096 Apr 11 16:02 frame   <br>
drwxr-xr-x 2 you user 4096 Mar 21 16:44 inc   <br>
drwxr-xr-x 2 you user 4096 Mar 21 16:44 main   <br>
drwxr-xr-x 2 you user 4096 Apr 11 16:13 phys   <br>
drwxr-xr-x 2 you user 4096 Mar 21 16:44 run   <br>
drwxr-xr-x 2 you user 8192 Mar 21 16:44 share   <br>
drwxr-xr-x 11 you user 4096 Nov 9 2005 test   <br>
drwxr-xr-x 3 you user 4096 Apr 11 16:01 tools   <br>
在README file里，写有关于code的有用信息和模式运行的设定方法。   <br>
   <br>
   <br>
### WRFV2目录下的文件分类：   <br>
   <br>
Source code directories:   <br>
chem/ Directory containing modules for chemistry (not currently supported)   <br>
dyn_em/ Directory containing modules for dynamics in WRF ARW core   <br>
dyn_nmm/ Directory containing modules for dynamics in WRF NMM core   <br>
dyn_exp/ Directory for a 'toy' dynamical core   <br>
external/ Directory containing external packages， such as those for IO， time keeping and MPI   <br>
frame/ Directory containing modules for WRF framework   <br>
inc/ Directory containing include files   <br>
main/ Directory for main routines， such as wrf.F， and all executables after install   <br>
phys/ Directory for all physics modules   <br>
share/ Directory containing mostly modules for WRF mediation layer and WRF I/O   <br>
tools/ Directory containing tools   <br>
Scripts:   <br>
clean Script to clean created files， executables   <br>
compile Script for compiling WRF code   <br>
configure Script to configure the configure.wrf file for compile   <br>
Makefile Top-level makefile   <br>
Registry/ Directory for WRF Registry file   <br>
arch/ Directory where compile options are gathered   <br>
run/ Directory where one may run WRF   <br>
test/ Directory that contains 7 test case directories， may be used to run WRF   <br>
   <br>
Environment Variable-NETCDF   <br>
定义NetCDF环境变量：   <br>
¾ NETCDF=/home/user/you;export NETCDF   <br>
   <br>
Configure WRFV2   <br>
键入：   <br>
¾ ./configure   <br>
在此，会显示出计算机所支持的平台。   <br>
checking for perl5... no   <br>
checking for perl... found /usr/bin/perl (perl)   <br>
Will use NETCDF in dir: /home/user/you/netcdf-3.6.1   <br>
PHDF5 not set in environment. Will configure WRF for use without.   <br>
$JASPERLIB or $JASPERINC not found in environment, configuring to build without grib2 I/O...   <br>
------------------------------------------------------------------------   <br>
Please select from among the following supported platforms.   <br>
   <br>
1. PC Linux x86_64 (IA64 and Opteron), PGI compiler 5.2 or higher (Single-threaded, no nesting)   <br>
   <br>
   <br>
2. PC Linux x86_64 (IA64 and Opteron), PGI 5.2 or higher, DM-Parallel (RSL, MPICH, Allows   <br>
nesting)   <br>
3. PC Linux x86_64 (IA64 and Opteron), PGI 5.2 or higher DM-Parallel (RSL_LITE, MPICH,   <br>
Allows nesting, No periodic LBCs)   <br>
4. PC Linux x86_64 (IA64 and Opteron), PGI compiler 5.2 or higher (Single-threaded, RSL, Allows   <br>
nesting)   <br>
5. AMD x86_64 Intel xeon i686 ia32 Xeon Linux, ifort compiler (single-threaded, no nesting)   <br>
6. AMD x86_64 Intel xeon i686 ia32 Xeon Linux, ifort compiler (single threaded, allows nesting   <br>
using RSL without MPI)   <br>
7. AMD x86_64 Intel xeon i686 ia32 Xeon Linux, ifort compiler (OpenMP)   <br>
8. AMD x86_64 Intel xeon i686 ia32 Xeon Linux, ifort compiler SM-Parallel (OpenMP, allows   <br>
nesting using RSL without MPI)   <br>
9. AMD x86_64 Intel xeon i686 ia32 Xeon Linux, ifort+icc compiler DM-Parallel (RSL, MPICH,   <br>
allows nesting)   <br>
10. AMD x86_64 Intel xeon i686 ia32 Xeon Linux, ifort+gcc compiler DM-Parallel (RSL, MPICH,   <br>
allows nesting)   <br>
11. PC Linux x86_64 (IA64 and Opteron), PathScale 2.1 or higher (Single-threaded, no nesting)   <br>
12. PC Linux x86_64 (IA64 and Opteron), PathScale 2.1 or higher DM-Parallel (RSL_LITE,   <br>
PathScale MPICH, No periodic LBCs)   <br>
13. Cray XT3 Catamount/Linux x86_64 (Opteron), PGI 5.2 or higher DM-Parallel (RSL_LITE,   <br>
MPICH, Allows nesting, Periodic in X only )   <br>
   <br>
```   <br>
Enter selection [1-13] :   <br>
（根据计算机的差异，有可能会显示出更多的平台选项）   <br>
```   <br>
作为练习，我们选择最为基本的（single-threaded， no nesting）。然后键入：   <br>
¾ 1   <br>
如果要进行并行计算或者嵌套的话，就要选择 3 。   <br>
在此步骤，将有configure.wrf 文件被做成。如果有必要，对此文件的compile options/paths也要进行编辑。   <br>
   <br>
Compile WRFV2   <br>
¾ ./compile   <br>
然后屏幕出现：   <br>
Usage:   <br>
compile wrf compile wrf in run dir (NOTE: no real.exe， ndown.exe， or ideal.exe generated)   <br>
or choose a test case (see README_test_cases for details) :   <br>
compile em_b_wave   <br>
compile em_grav2d_x   <br>
compile em_hill2d_x   <br>
compile em_quarter_ss   <br>
   <br>
   <br>
compile em_real   <br>
compile em_squall2d_x   <br>
compile em_squall2d_y   <br>
compile exp_real   <br>
compile nmm_real   <br>
compile -h help message   <br>
因为要对WRF ARW real data case进行编辑，所以选择em_real。   <br>
   <br>
然后开始编译模块。   <br>
* ./compile em_real >& compile.log   <br>
运行会稍微花一点时间。（如果在./configure处选择了 3 ，这时你会有将近 30 分钟左右的时间来喝杯咖啡。）   <br>
如果在进行过程当中自己弄出错了，或者要更改configure、compile等的选项，可以用 “clean -a”的命令来   <br>
清理所有的 built files，including configure.wrf。   <br>
* ./clean -a   <br>
然后再重新编译WRFV2.2。   <br>
   <br>
编译结束后，打开compile.log确认是否有错误信息存在。如果编辑成功，在main/目录下会有以下的文件被   <br>
做成！   <br>
-rwxr-xr-x 1 you user 13612035 Mar 22 15:11 ndown.exe   <br>
-rwxr-xr-x 1 you user 13237353 Mar 22 15:11 nup.exe   <br>
-rwxr-xr-x 1 you user 10909533 Mar 22 15:11 real.exe   <br>
-rwxr-xr-x 1 you user 13237353 Mar 22 15:11 wrf.exe   <br>
ndown.exe 用于one-way nesting 。   <br>
nup.exe 用在WRF_3DVAR。   <br>
real.exe用于real data cases的初期化   <br>
wrf.exe用于WRF model integration   <br>
这些文件被从main/目录链接到了run/，test/em_real/目录下。   <br>
（如果运行其它idealized cases，方法也一样。在./compile em_real >& compile.log处选择相应的文件选项。   <br>
不过做后会生成ideal.exe）   <br>
   <br>
## 4.4. ～运行WRFV2.2～   <br>
   <br>
Edit namelist.input   <br>
移动到run/ 或 test/em_real 目录下。无论哪个都可以。在这里，我们选择后者。   <br>
¾ cd test/em_real   <br>
（如果在em_real下不能正常运行real.exe的话，可以到run目录下试试）   <br>
   <br>
在此处会有以下文件生成。   <br>
lrwxrwxrwx 1 you user 23 Mar 22 15:11 ETAMPNEW_DATA -> ../../run/ETAMPNEW_DATA   <br>
lrwxrwxrwx 1 you user 21 Mar 22 15:11 GENPARM.TBL -> ../../run/GENPARM.TBL   <br>
   <br>
   <br>
lrwxrwxrwx 1 you user 21 Mar 22 15:11 LANDUSE.TBL -> ../../run/LANDUSE.TBL   <br>
lrwxrwxrwx 1 you user 25 Mar 22 15:11 README.namelist -> ../../run/README.namelist   <br>
lrwxrwxrwx 1 you user 19 Mar 22 15:11 RRTM_DATA -> ../../run/RRTM_DATA   <br>
lrwxrwxrwx 1 you user 22 Mar 22 15:11 SOILPARM.TBL -> ../../run/SOILPARM.TBL   <br>
lrwxrwxrwx 1 you user 21 Mar 22 15:11 VEGPARM.TBL -> ../../run/VEGPARM.TBL   <br>
lrwxrwxrwx 1 you user 21 Mar 22 15:11 gribmap.txt -> ../../run/gribmap.txt   <br>
-rw-r--r-- 1 you user 1762 Feb 19 2005 landFilenames   <br>
-rw-r--r-- 1 you user 5485 Mar 21 17:03 namelist.input   <br>
-rwxr-xr-x 1 you user 5489 Jun 20 2005 namelist.input.jan00   <br>
-rwxr-xr-x 1 you user 5488 Jun 20 2005 namelist.input.jun01   <br>
lrwxrwxrwx 1 you user 20 Mar 22 15:11 ndown.exe -> ../../main/ndown.exe   <br>
lrwxrwxrwx 1 you user 19 Mar 22 15:11 real.exe -> ../../main/real.exe   <br>
-rw-r--r-- 1 you user 10240 Sep 17 2004 run_1way.tar   <br>
-rw-r--r-- 1 you user 10240 Oct 18 2005 run_restart.tar   <br>
lrwxrwxrwx 1 you user 17 Mar 22 15:11 tr49t67 -> ../../run/tr49t67   <br>
lrwxrwxrwx 1 you user 17 Mar 22 15:11 tr49t85 -> ../../run/tr49t85   <br>
lrwxrwxrwx 1 you user 17 Mar 22 15:11 tr67t85 -> ../../run/tr67t85   <br>
lrwxrwxrwx 1 you user 18 Mar 22 15:11 wrf.exe -> ../../main/wrf.exe   <br>
这些文件的用途见上一章的运行WRFV2.2部分。   <br>
   <br>
针对本次的OnLine Tutorial case，编辑namelist.input。   <br>
归纳一下，主要修改以下几点。   <br>
Start date: 2005082800   <br>
End date: 2005083100   <br>
Interval: 21600 sec (6 hours)   <br>
Grid points in EW direction: 75   <br>
Grid points in SN direction: 70   <br>
Number of vertical levels: 31   <br>
Grid distance: 30km   <br>
同样, namelist.input也被用在了real.exe和wrf.exe可执行文件处（应该也是被链接过去的吧）。   <br>
   <br>
Link   <br>
把在WRF_SI处做成的wrf_real_input* files链接到WRFV2/test/em_run/ 目录下。   <br>
* ln -sf /home/user/you/WRF/wrfsi/domains/OnlineTut/siprd/wrf_real_input_em.d01.2005-08-*.   <br>
使用方法可以参考ln 命令   <br>
   <br>
Run real.exe   <br>
进行single processor 运行。   <br>
* ./real.exe   <br>
如果是DM(distributed memory) parallel systems，就会需要mpirun command 。例如，对于Linux cluster，   <br>
   <br>
   <br>
要运行 4 个CPU的MPI code的命令文就是：   <br>
* mpirun –np 4 real.exe   <br>
可以根据自己的条件选择CPU的个数。同时不要忘记，在./configure 处要选择对应的平台。   <br>
在键入./real.exe 后，最好不要打扰计算机的运行。如果运行成功的话，最后会有 wrfbdy_d01 和   <br>
wrfinput_d01文件生成。   <br>
   <br>
Check your rsl file   <br>
确认rsl.out.*和rsl.error.*（对于每个processor，都 会 出 现rsl.out和rsl.error）。在rsl.out.0000和rsl.error.0000里包   <br>
含了重要的情报。如果运行失败，error message有可能存在于这些文件当中的某一个文件里。同时，在   <br>
namelist.input 里有debug_level一项。这一项对应的数值为 0 ， 50 ， 100 ， 200 ， 300 等，数值越大，在rsl.out.*   <br>
和rsl.error.*里输出的信息越详细，有利于寻找错误的根源。如果运行不能成功，请考虑使用此项。   <br>
使用head –n 30 rsl.out.* 和tail–n 30 rsl.out.* 命令来查看rsl的文件头 30 行和文件尾 30 行。   <br>
如果运行real.exe成功，则在rsl.out.0000的最后会有提示：   <br>
   <br>
SUCCESS COMPLETE REAL_EM INIT   <br>
   <br>
因为wrf.exe也会生成同名的log文件，所以把上面的rsl.out.*和rsl.error.*移动到其他目录，或者删掉。   <br>
   <br>
Run wrf.exe   <br>
进行single processor 运行。   <br>
* ./wrf.exe   <br>
如果是DM(distributed memory) parallel systems，会有需要mpirun command的场合。例如，如果是Linux   <br>
cluster，实行4CPUs的MPI code的命令就是：   <br>
* mpirun –np 4 wrf.exe   <br>
   <br>
如果全部进行顺利的话，会有wrfout_d01_file被做成。   <br>
从 2005082800 到 2005083100 的 72 小时份的文件将被做成。用ncdump可以查看wrfout_d01 file里的信息。   <br>
* ncdump –h wrfout_d01_2005-08-28_00:00:00 参照   <br>
   <br>
wrf: SUCCESS COMPLETE WRF   <br>
   <br>
   <br>
# 5.＜安装使用WRF2GrADS＞   <br>
   <br>
在WRF的tool里直接介绍了四种气象作图的工具，并为他们提供了相应的文件格式的转换工具。   <br>
它们是：   <br>
· NCL   <br>
· RIP4   <br>
· WRF-to-Grads   <br>
· WRF-to-vis5d   <br>
对于这四种制图软件，WRF有专门的讲解PowerPoint。如果想知道的更多，可以下载WRF Post-Processing。   <br>
   <br>
其中Grads的历史悠久，功能强大，使用也不算麻烦。并且，在一些有实力的论坛上对GrADS的讨论也   <br>
比较多，有什么不明白的问题可以从论坛里得到一定的帮助。作为练习，把WRF的output数据转化成可   <br>
用于GrADS的数据格式。   <br>
   <br>
Install wrf2grads   <br>
具体方法可参照WRF2GrADS的相关网页。   <br>
从已经下载的Source_Codes中复制wrf2grads.tar.gz 文件到/home/user/you/WRF下，用gunzip 和 tar命令进行   <br>
解压。   <br>
¾ gunzip wrf2grads.tar.gz   <br>
¾ tar –xvf wrf2grads.tar   <br>
在/home/user/you/目录下会产生名为WRF2GrADS的目录。主要有以下文件：   <br>
Makefile   <br>
README   <br>
control_file   <br>
control_file_height   <br>
control_file_pressure   <br>
module_wrf_to_grads_netcdf.F   <br>
module_wrf_to_grads_util.F   <br>
wrf_to_grads.F   <br>
   <br>
Edit Makefile & control_file   <br>
在使用WRF2GrADS之前，一定要仔细阅读其自带的README文件。   <br>
 cd WRF2GrADS   <br>
我们需要通过编辑Makefile来选择一款适合于自己计算机的描述。   <br>
 vi Makefile   <br>
   <br>
   <br>
### 比如，适合我使用的计算机的描述是：   <br>
   <br>
### ......   <br>
   <br>
```   <br>
# linux flags（PGI）   <br>
```   <br>
```   <br>
#LIBNETCDF = -L/usr/local/netcdf/lib -lnetcdf -lm   <br>
#INCLUDE = -I/usr/local/netcdf/include -I./   <br>
#FC = pgf90   <br>
#FCFLAGS = -g -C -Mfree   <br>
#FCFLAGS = -fast -Mfree   <br>
#CPP = /usr/bin/cpp   <br>
#CPPFLAGS = -I. -C -traditional -DRECL4   <br>
......   <br>
（我们可以根据“FC = ”的性质来选择适合我们计算机的描述）   <br>
```   <br>
```   <br>
然后对Makefile进行编辑(红色部分)：   <br>
```   <br>
```   <br>
......   <br>
# linux flags (PGI)   <br>
```   <br>
```   <br>
LIBNETCDF = -L/home/user/you/lib -lnetcdf -lm   <br>
INCLUDE = -I/home/user/you/include -I./   <br>
FC = pgf90   <br>
FCFLAGS = -g -C -Mfree   <br>
FCFLAGS = -fast -Mfree   <br>
CPP = /usr/bin/cpp   <br>
CPPFLAGS = -I. -C -traditional -DRECL4   <br>
......   <br>
```   <br>
注意：一定要去掉描述语句前的 # 字符号。然后<Esc> : w q 保存退出。   <br>
然后键入:   <br>
 make   <br>
在目录下会自动生成名为 wrf_to_grads 的可执行文件。   <br>
   <br>
通过对control_file文件的编辑，使wrf2grads可以生成时间相对应的output文件。生成的文件为可使用在   <br>
GrADS里的.ctl和.dat文件。例如：   <br>
 vi control_file   <br>
   <br>
   <br>
### 然后，主要对以下信息进行编辑：   <br>
   <br>
- set times to be processed   <br>
- set variables to be processed   <br>
- define the input file   <br>
- specify if the input is real/ideal/static data   <br>
- set levels to interpolate too   <br>
   <br>
例如，对于我自己的文件，编辑部分的control_file的如下：   <br>
   <br>
```   <br>
7! number of times to put in GrADS file，negative means ignore the times   <br>
2005-08-28_00:00:00   <br>
2005-08-28_12:00:00   <br>
2005-08-29_00:00:00   <br>
2005-08-29_12:00:00   <br>
2005-08-30_00:00:00   <br>
2005-08-30_12:00:00   <br>
2005-08-31_00:00:00   <br>
end_of_time_list   <br>
! 3D variable list for GrADS file   <br>
! indent one space to skip   <br>
......   <br>
/DATA/real/wrfinput_d01   <br>
```   <br>
```   <br>
/home/user/you/WRF/WRFV2/run/wrfout_d01_2005-08-28_00:00:00   <br>
```   <br>
```   <br>
/DATA/b_wave/wrfout_d01_0001-01-01_00:00:00   <br>
/DATA/grav2d_x/wrfout_d01_0001-01-01_00:00:00   <br>
......   <br>
```   <br>
编辑好后键入<Esc> : w q 保存退出。   <br>
   <br>
注意：   <br>
①. 在这里编辑的第一个数字与下面的列出的时间相对应。在GrADS里，这个数字被用在了t时次。例   <br>
如：我们在GrADS里，可使用命令：set t 1 7。当数字少于下面给出的时间列的时候，output文件   <br>
里只会生成前几个时间列的数据;当数字为负的时候，会忽略数字，并对后面所有列出的时间进行   <br>
处理。   <br>
②. 最后，前往不能忘记要加上end_of_time_list作为结尾。   <br>
③. 在control_file的编辑过程中不可多加空行，不然会产生error。   <br>
④. 暂时未对input data , set levels 等项进行编辑。   <br>
   <br>
   <br>
Run wrf2grads   <br>
开始运行转换。   <br>
¾ ./wrf_to_grads control_file wrfout_d01_2005-08-28_00:00:00 - v   <br>
直接运行wrf_to_grads和control_file文件。在这里，wrfout_d01_2005-08-28_00:00:00是转换后生成文件的   <br>
文件名，可以自行定义任意文件名；最后的–v是表示属性。   <br>
如果顺利，格式转换完后会出现如下的信息：   <br>
... ...   <br>
writing out variable, time 7 3   <br>
time 2005-08-3 0 _00:00:00, output variable Z   <br>
getting data for HGT   <br>
writing out variable, time 8 3   <br>
time 2005-08-30_00:00:00, output variable HGT   <br>
   <br>
```   <br>
--------------------------------------------------   <br>
Gracefull STOP   <br>
--------------------------------------------------   <br>
```   <br>
在当目录下会生成 ****.ctl 和 ****.dat 文件。例如：   <br>
wrfout_d01_2005-08-28_00:00:00.ctl   <br>
wrfout_d01_2005-08-28_00:00:00.dat   <br>
这两个文件ctl和dat将会在GrADS 画图软件中使用。   <br>
   <br>
   <br>
#6.＜在UNIX系统下安装GrADS＞   <br>
   <br>
GrADS是一款功能强大的气象绘图工具。关于GrADS的中文版的使用手册，可以到LASG（大气科学和地   <br>
球流体力学数值模拟国家重点实验室）的动力论坛专业绘图软件去下载。里面还介绍了在WINDOWS下的   <br>
安装方法。关于GrADS软件，可以到其主页下载。对于不同的平台，提供了相应的版本。我是在UNIX系   <br>
统下安装的GrADS，在这里只是简单的描叙UNIX系统下的安装过程。如果只需要source_code ,可以使用   <br>
grads-src-1.8sl1 或 grads-src-1.9b4 。我使用的是后者。   <br>
在Windows下的安装方法请参考LASG编的《GrADS实用手册》。   <br>
   <br>
Install GrADS   <br>
安装之前，定义NetCDF的环境变量。   <br>
¾ NETCDF=/home/user/you;export NETCDF   <br>
把grads-src-1.9b4 下载到/home/user/you/目录下，用gunzip和tar 解冻。会生成一个名为grads-1.9b4的文   <br>
件夹。进入文件夹，键入以下命令进行软件的安装。   <br>
¾ ./configure   <br>
¾ make   <br>
¾ make install   <br>
安装完毕。   <br>
   <br>
Set Environment Variables   <br>
使用Grads前要进行环境变量的定义。对GADDIR，GASCRP，GAUDFT，PAT H四个环境变量进行定义。   <br>
如下：   <br>
¾ GADDIR=/home/user/you/grads-1.9b4/data;export GADDIR   <br>
¾ GASCRP=/home/user/you/grads-1.9b4;export GASCRP   <br>
¾ GAUDFT=/home/user/you/grads-1.9b4/data;export GAUDFT   <br>
¾ PATH=$PATH:$GADDIR;export PATH   <br>
这些环境变量同样可以加入上面的隐藏文件.bashrc中。   <br>
   <br>
Open GUI   <br>
因为要使用GUI，可以先运行前面讲过的方法打开GUI。   <br>
   <br>
Run GrADS   <br>
然后进入存放有wrfout_d01_2005-08-28_00:00:00.ctl 和wrfout_d01_2005-08-28_00:00:00.dat 的文件夹，即   <br>
生成ctl和dat文件的目录WRF2GrADS。   <br>
¾ cd /home/user/you/WRF2GrADS   <br>
这里的.ctl和.dat文件即是由WRF2GrADS生成的文件。在此目录下，键入如下命令文来打开grads。   <br>
¾ /home/user/you/grads-1.9b4/bin/gradsc   <br>
这时有一个窗口被打开，这就是我们要进行查看绘图的窗口。同时还会出现如下的对话：   <br>
   <br>
   <br>
```   <br>
Grid Analysis and Display System (GrADS) Version 1.9b4   <br>
Copyright (c) 1988-2005 by Brian Doty and IGES   <br>
Center for Ocean-Land-Atmosphere Studies (COLA)   <br>
Institute for Global Environment and Society (IGES)   <br>
GrADS comes with ABSOLUTELY NO WARRANTY   <br>
See file COPYRIGHT for more information   <br>
Config: v1.9b4 32-bit little-endian lats   <br>
Issue 'q config' command for more information.   <br>
Landscape mode? (no for portrait):   <br>
```   <br>
键入y和回车或者直接回车选择默认，就会直接进入GrADS的对话模式。   <br>
......   <br>
Landscape mode? (no for portrait): y   <br>
GX Package Initialization: Size = 11 8.5   <br>
ga>   <br>
   <br>
在提示符 ga> 后输GrADS命令文，就可操作GrADS进行制图了。   <br>
关于GrADS的具体使用方法，可以参考LASG编的《GrADS实用手册》。   <br>
   <br>
   <br>
# 7.＜利用其它数据的练习＞   <br>
   <br>
通过对《WRF V2安装运行入门指南》的前面的 6 节的学习，大家应该都了解了WRF的基本运行步骤了。   <br>
这时，你也一定想通过运行一些其它领域和时间的案例，来巩固和验证自己对WRF的理解和运用。我们   <br>
可以从WRF推荐的几个网页上下载一些数据来使用。   <br>
   <br>
Download Dataset   <br>
＊ 静态数据：可以使用已经装好的Katrina的那款；   <br>
＊ 气象数据：WRF_SI和WPS的输入数据的格式有grid1和grid2。我们可以到NCAR的dss处下载ds083.2数   <br>
据来使用。ds083.2是NECP的客观分析数据FNL形式。在其下载页面上仅登有最近一年的数据可供免费下   <br>
载。这些数据的文件名格式是fnl_YYMMDD_hh_mm ，即 fnl_年年月月日日_时时_分分 。注意：MS的IE   <br>
下载到的这些数据通常会被追加成 .txt 的文本格式。不要轻易打开，去掉后面的.txt一样可用。个人经验，   <br>
使用Opera也许下载会更方便。这些气象数据都是全球范围的。除此之外，还有其他现成的数据可以使用。   <br>
参考WRF的网页。   <br>
   <br>
～ WPS+WRFV2.2 ～   <br>
WPS   <br>
Run WPS   <br>
在WRF/WPS/目录下，编辑namelist.wps。   <br>
¾ ./geogrid.exe   <br>
并行计算的话   <br>
¾ mpirun -np 4 geogrid.exe   <br>
¾ ./link_grib.csh /home/user/you/WRF/DATA/TESTDATA/fnl_0610   <br>
¾ ln -sf ungrib/Variable_Tables/Vtable.GFS Vtable   <br>
¾ ./ungrib.exe >& ungrib.log   <br>
¾ ./metgrid.exe   <br>
并行计算的话   <br>
¾ mpirun –np 4 metgrid.exe   <br>
   <br>
WRFV2.2   <br>
在/WRF/WRFV2/目录下   <br>
¾ cd test/em_real or cd run   <br>
编辑namelist.input   <br>
¾ ln –sf /home/user/you/WRF/WPS/met_em.d01.2005-08*.   <br>
¾ ./real.exe   <br>
并行计算的话...   <br>
¾ mpirun –np 4 real.exe   <br>
¾ ./wrf.exe   <br>
并行计算的话...   <br>
¾ mpirun –np 4 wrf.exe   <br>
   <br>
   <br>
～ WRF_SI+WRFV2.2 ～   <br>
WRF_SI   <br>
Set Environment Variables   <br>
定义环境变量 可使用source ~/.bashrc 命令。   <br>
   <br>
Run WRF_SI   <br>
STEP1   <br>
在/WRF/wrfsi/目录下：   <br>
¾ cd domains   <br>
¾ mkdir TestOne   <br>
¾ MOAD_DATAROOT=/home/user/you/WRF/wrfsi/domains/TestOne;export MOAD_DATAROOT   <br>
¾ cd /home/user/you/WRF/wrfsi/templates   <br>
¾ cp –r default TestOne   <br>
¾ chmod –R u+w TestOne   <br>
¾ cd TestOne   <br>
编辑wrfsi.nl的 1 和 2 部分   <br>
¾ cd /home/user/you/WRF/wrfsi   <br>
¾ ./etc/window_domain_rt.pl -w wrfsi -t /home/user/you/WRF/wrfsi/templates/TestOne   <br>
STEP2   <br>
新建一个专门存放TestOne用的气象数据文件夹。比如说，在/WRF/wrfsi/下建立一个名为FTestone 的目录。   <br>
把要处理的数据放入FTestone目录下。同时要注意：①文件名格式；②数据时间上的连续；③不要放入无   <br>
关文件。比如说，我在FTestone目录里存放了fnl_061020_12_00～fnl_061022_00_00共 6 个数据文件。   <br>
编辑grib_prep.nl 硬性指定数据文件为“AVN”数据。   <br>
¾ cd /home/user/you/WRF/wrfsi   <br>
¾ ./etc/grib_prep.pl -s 2006102012 -l 36 –t 6 AVN   <br>
STEP3   <br>
编辑wrfsi.nl的 3 和 4 部分：特别注意下面两个变量的设定为“AVN”：   <br>
INIT_ROOT = 'AVN'   <br>
LBC_ROOT = 'AVN'   <br>
¾ cd /home/user/you/WRF/wrfsi   <br>
¾ ./etc/wrfprep.pl –s 2006102012 -f 36 -t 6   <br>
   <br>
WRF V2.2   <br>
在/WRF/WRFV2/目录下，   <br>
¾ cd test/em_real or cd run   <br>
编辑namelist.input   <br>
¾ ln -sf /home/user/you/WRF/wrfsi/domains/TestOne/siprd/wrf_real_em.d01.2006-10-*.   <br>
¾ ./real.exe   <br>
并行计算的话...   <br>
¾ mpirun –np 4 real.exe   <br>
   <br>
   <br>
¾ ./wrf.exe   <br>
并行计算的话...   <br>
¾ mpirun –np 4 wrf.exe   <br>
   <br>
WRF2GrADS   <br>
在/home/user/you/WRF/目录下   <br>
¾ cd WRF2GrADS   <br>
编辑control_file   <br>
然后运行wrf_to_grads。   <br>
¾ ./wrf_to_grads control_file Te s t O n e -v   <br>
   <br>
GrADS   <br>
Set Environment Variables   <br>
定义环境变量 如果把环境变量一并写入.bashrc里的话,可以省去这一步骤。   <br>
在这里要运行GUI，所以要事先打开X-window。   <br>
¾ cd /home/user/you/WRF2GrADS   <br>
¾ /home/user/you/grads-1.9b4/bin/gradsc   <br>
进入GrADS软件的操作 ......   <br>
¾ open TestOne.ctl   <br>
....   <br>
   <br>
   <br>
### 附录1:安装NCARG （NCAR Graphic）   <br>
NCARG是NCAR Graphic，由NCAR开发的视图工具。与GrADS相比，NCARG的应用并不广泛。但作   <br>
为NCAR 的产品，被积极地用在了WPS的领域查看和设计等中途工作，而且对于有些工作也可以使用   <br>
gradsnc来代替执行。但NCAR既然提到了使用NCARG，就 姑 且 把NCARG的安装方法一并记述下来，以   <br>
供日后参考使用考。   <br>
NCARG的下载方法和详细的安装方法，请参考其主页。   <br>
   <br>
Install NCARG   <br>
把NCARG下载到WRF/目录下并解压。   <br>
* gunzip ncarg-4.4.1.src.tar.gz   <br>
* tar –xvf ncarg-4.4.1.src.tar   <br>
这时，WRF/目录下会生成名为ncarg-4.4.1的目录。然后定义环境变量。   <br>
* NCARG=/home/user/you/WRF/ncarg-4.4.1;export NCARG   <br>
* cd ncarg-4.4.1   <br>
* ./Configure –v   <br>
   <br>
如果顺利，屏幕开始出现一些对话，你会被问到几个问题。这时你必须要清楚自己使用的计算机的环境设   <br>
定状况：安装NCARG时的默认设置是/usr/local/ncarg/lib等等，这些都必须更改为NCARG的路径（例如，   <br>
可更改为/home/user/you/WRF/ncarg-4.4.1/lib）。其它环境设定状况例如：使用的X11软件是32-bit还是64-bit   <br>
（X11的开发等原因，一般有/usr/X11R6/lib (32bit环境）和/usr/X11R6/lib64 (64bit环境））、X11的路径等   <br>
等。也会被问到是否安装HDF，选no和yes均可。关于其他问题，请自己仔细阅读判断并回答。   <br>
   <br>
环境设定结束后，安装之前我们仍然可以最后确定一下我们的选择和设定：   <br>
¾ make Info   <br>
然后屏幕中出现下面的信息：   <br>
   <br>
```   <br>
NCAR Graphics - Version 4.4.1 Installation Configuration   <br>
System File LINUX   <br>
Binary Install Directory /home/user/you/WRF/ncarg-4.4.1/bin   <br>
Library Install Directory /home/user/you/WRF/ncarg-4.4.1/lib   <br>
Include Install Directory /home/user/you/WRF/ncarg-4.4.1/include   <br>
Manpage Install Directory /home/user/you/WRF/ncarg-4.4.1/man   <br>
Config Install Directory /home/user/you/WRF/ncarg-4.4.1/lib/ncarg/config   <br>
Data Base Directory /home/user/you/WRF/ncarg-4.4.1/lib/ncarg/database   <br>
Programmer Doc Dir /home/user/you/WRF/ncarg-4.4.1/lib/ncarg/doc   <br>
Reloc Obj. Directory /home/user/you/WRF/ncarg-4.4.1/lib/ncarg/robj   <br>
Examples Directory /home/user/you/WRF/ncarg-4.4.1/lib/ncarg/examples   <br>
Tutorial Directory /home/user/you/WRF/ncarg-4.4.1/lib/ncarg/tutorial   <br>
Test Directory /home/user/you/WRF/ncarg-4.4.1/lib/ncarg/tests   <br>
```   <br>
   <br>
```   <br>
X App. Def. Directory /home/user/you/WRF/ncarg-4.4.1/lib/ncarg/xapp   <br>
f77 Compiler pgf95   <br>
f77 Flags -O   <br>
C Compiler gcc   <br>
cc Flags -ansi -O -I./include -I/usr/X11R6/include -DSYSV -D_POSIX_SOURCE   <br>
-D_XOPEN_SOURCE -DByteSwapped -DNeedFuncProto   <br>
```   <br>
对话结束后，输入make Everything进行NCARG软件安装。   <br>
¾ make Everything >& make-output &   <br>
安装过程是在后台进行的。我们可以使用tail命令来随时可以查看日志文件make-output的输出内容。   <br>
¾ tail -f make-output   <br>
如果中途出现了错误信息，请参考Restarting the installation，再进行reinstall。   <br>
   <br>
安装结束后，定义环境变量：   <br>
¾ NCARG_ROOT=/home/user/you/WRF/ncarg-4.4.1;export NCARG_ROOT   <br>
¾ PATH=$NCARG_ROOT/bin:$PATH   <br>
¾ MANPATH=$NCARG_ROOT/man:$MANPATH   <br>
   <br>
Check NCARG   <br>
校验NCARG的安装是否成功。NCARG里自带有检验安装的程序。这时要打开X-window，并对相应的GUI   <br>
环境进行设定。然后按下面的方法运行。   <br>
¾ ncargex cpex08   <br>
NCAR Graphics Fortran Example <cpex08>   <br>
Copying cpex08.f   <br>
Copying cpexcc.f   <br>
Compiling and linking...   <br>
pgf95 -O -o cpex08 cpexcc.f cpex08.f -L/home/user/you/WRF/ncarg-4.4.1/lib -L/usr/X11R6/lib64   <br>
-lncarg -lncarg_gks -lncarg_c -lX11 -lXext   <br>
cpexcc.f:   <br>
cpex08.f:   <br>
Executing <cpex08>...   <br>
PLOT TITLE WAS EXAMPLE 8   <br>
INTEGER WORKSPACE USED 120   <br>
REAL WORKSPACE USED 400   <br>
AREA MAP SPACE USED 93250   <br>
FORTRAN STOP   <br>
Metafile file is named cpex08.ncgm.   <br>
¾ ctrans –d X11 cpex08.ncgm   <br>
然后，屏幕中会出现右图。   <br>
关于如何在WPS中使用NCARG，请参考WPS的网页。   <br>
   <br>
   <br>
### 附录2:   <br>
在WRF_SI阶段，对wrfsi.nl的设定极为重要。这是我在网上（LASG的动力论坛）收集到的有关wrfsi.nl   <br>
的参数配置的中文说明。大家也可到原地址下载。   <br>
   <br>
关于WRFSI2.0中wrfsi.nl的参数配置说明（中文版）   <br>
(这条文章已经被阅读了n次) 时间：2004/06/24 02:53pm 来源：meteogg   <br>
[这个贴子最后由meteogg在 2004/06/24 02:54pm 编辑]   <br>
   <br>
折腾了一天，终于把它整理成中文，希望能对使用者有帮助。另外有解释的不合适的地方，请提意见。全   <br>
文如下：   <br>
   <br>
A. PROJECT_ID Section   <br>
   <br>
该部分为说明部分。该部分的设置不影响WRF_SI 的运行，但是便于在输出元数据中说明运行。   <br>
   <br>
1. SIMULATION_NAME: 指定本次运行实验的名称。   <br>
2. USER_DESC: 描述运行者。   <br>
   <br>
B. FILETIMESEPC Section   <br>
   <br>
该部分确定SI要处理的数据的起始和终止时间。注意：如果要用wrfprep.pl 运行hinterp/vinterp （我们建   <br>
议您必须......），脚本会自动为您编辑这些值。时间为世界时。   <br>
   <br>
1. START_YEAR: 四位数表示起始年。   <br>
2. START_MONTH: 两位数表示起始月份。   <br>
3. START_DAY: 两位数表示起始日期。   <br>
4. START_MINUTE: 两位数表示起始的分钟数。   <br>
5. START_HOUR: 两位数表示起始的小时数。   <br>
6. START_SECOND: 两位数表示起始的秒数。   <br>
7-12. END_YEAR-END_SECOND: 和1-5一样， 但是为结束时间。   <br>
13. INTERVAL: 输出的时间间隔，单位为秒。   <br>
   <br>
C. HGRIDSPEC section   <br>
   <br>
该部分定义WRF的水平格点。   <br>
   <br>
1. NUM_DOMAINS: 区域数。如果不嵌套，则定义为 1 。   <br>
2. XDIM/YDIM: MOAD（母区域）的格点数。尽管区域数大于 1 ，即有嵌套时，在wrfsi.nl中也仅设置   <br>
一个母区域的X和Y方向上的格点， 因为嵌套区域的xdim和ydim根据其它参数自动计算（见下面的设   <br>
置 5 ）。   <br>
   <br>
   <br>
注意：WRF_SI 将底图定义为“非交错”网格。运用Arakawa-C 交错格点假设所有 3 维变量（U， V，   <br>
和质量）关于这些点是交错格点。对于定义的非交错格点，U格点向上交错了0.5个格点，V格点向右交   <br>
错了0.5个格点，质量网格分别向上向右交错了0.5个格点。 为了便于说明，下面给出一个(XDIM，YDIM)   <br>
= (4，4)的例子：   <br>
   <br>
+ V + V + V +   <br>
U T U T U T U   <br>
+ V + V + V +   <br>
U T U T U T U   <br>
+ V + V + V +   <br>
U T U T U T U   <br>
+ V + V + V +   <br>
   <br>
(+) 为根据namelist中的参数定义的点。(T)为由WRF预报模式提供和输出的质量变量的格点位置。(U)   <br>
点为由WRF模式提供和输出的U动量变量的格点位置。 (V)点为由WRF模式提供和输出的V动量变量   <br>
的格点位置。这样，如果WRF_SI配置使用维数(XDIM， YDIM)，则模式输出如下：   <br>
   <br>
(XDIM-1，YDIM-1)维的质量变量   <br>
(XDIM，YDIM-1)维的U动量   <br>
(XDIM-1，YDIM)维的V动量   <br>
   <br>
3. PARENT_ID: 嵌套区域的母区域的标号。注意MOAD 本身没有母区域，因此PARENT_ID 的第一列   <br>
总是设为 1 。第二列必须等于 1 。总列数必须等于NUM_DOMAINS。   <br>
4. RATIO_TO_PARENT: 该整数指定每个子区域和它们母区域的格距比。典型值为 2 和 3 ，但是也可以   <br>
更大一些。该参数的列数必须等于NUM_DOMAINS。   <br>
5. DOMAIN_ORIGIN_[LLI/LLJ/URI/URJ]: 这四个参数定义每个子区域在其母区域中西南（左下[LL]）和   <br>
东北（右上[UR]）角的i/j 方向的格点位置。对于MOAD 而言，SW = 1， 1 ； NE = xdim，ydim。则子   <br>
区域的xdim，ydim 值可由下式计算（SI中自动计算）：   <br>
   <br>
xdim = (uri-lli)*ratio_to_parent+1，   <br>
ydim = (urj-llj)*ratio_to_parent+1.   <br>
   <br>
6. MAP_PROJ_NAME: 该字符串指定地图投影的方式。有效选项如下：   <br>
"polar" -> 极射投影   <br>
"lambert" -> 兰伯托等角投影（正割和正切）   <br>
"mercator" -> 麦卡托   <br>
   <br>
   <br>
### 7. MOAD_KNOWN_LAT/MOAD_KNOWN_LON: 网格中心点的经纬度。单位为度，正的纬度表示北半球，   <br>
   <br>
### 负值表示南半球。纬度在-90 和 90 之间，经度在-180河 180 之间。   <br>
   <br>
### 8. MOAD_STAND_LATS: 两个实数表示标准纬度（此处格距不变）。必须在-90和 90 之间，根据投影   <br>
   <br>
### 选取该参数的值：   <br>
   <br>
### 极射投影：第一个参数为格距不变的纬度，可设为中心纬度。第二个参数南/北半球为+/-90.。   <br>
   <br>
### 兰勃托投影：两个值均与中心纬度正负号相同。对于正切投影，两个参数设为同一个值（通常设为中   <br>
   <br>
### 心纬度）。而对于正割投影，两个参数必须为不同值。   <br>
   <br>
### 麦卡托投影：第一个参数为格距不变的纬度（通常为中心纬度）。第二个参数没有用到。   <br>
   <br>
9. MOAD_STAND_LONS: 该参数指定于y坐标平行的经度(-180->180)。通常设为中心经度。   <br>
10. MOAD_DELTA_X/MOAD_DELTA_Y: 该浮点数分别指定东西和南北向的格距，单位为米。目前，两   <br>
个值必须相同。嵌套子区域的格距由SI和GUI自动计算(见文件 src/lib/get_wrfsi_config.f 中的function   <br>
grid_spacing_wrf_m(nest))：   <br>
   <br>
grid_spacing_wrf_m = moad_delta_x   <br>
i = nest:   <br>
do while (i.ne.1)   <br>
grid_spacing_wrf_m = grid_spacing_wrf_m/ratio_to_parent(i)   <br>
i = parent_id(i)   <br>
enddo   <br>
   <br>
11. SILAVWT_PARM_WRF (见README_toptwvl_silavwt in src/grid):   <br>
12. TOPTWVL_PARM_WRF (见README_toptwvl_silavwt in src/grid):   <br>
   <br>
D. SFCFILES Section   <br>
   <br>
该部分指定静态数据的路径，这些静态的全球地理数据由下面ftp网址获取：   <br>
ftp://aftp.fsl.noaa.gov/divisions/frd-laps/WRFSI/Geog_Data   <br>
每个数据集必须有它自己的子目录！   <br>
   <br>
1. TOPO_30S: 源自USGS 的 30 秒地形高度数据的路径。   <br>
2. PCTLAND_10M: 10分的土地分类资料的路径。   <br>
   <br>
   <br>
### 3. LANDUSE_30S: 30秒USGS 24种土壤利用类型资料的路径。   <br>
   <br>
### 4. SOILTYPE_TOP_30S: 30秒FAO 上层 16 种土壤类型资料的路径。   <br>
   <br>
### 5. SOILTYPE_BOT_30S: 和(4)相同，但是为底层。   <br>
   <br>
### 6. GREENFRAC: 植被分类数据的路径。   <br>
   <br>
### 7. SOILTEMP_1DEG: 1度年平均深层土壤温度数据的路径。   <br>
   <br>
### 8. ALBEDO_NCEP: 反照率的月气候数据的路径。（归一为局地天顶）。   <br>
   <br>
### 9. SSTEMP: 未使用，预留给气候的SST数据。   <br>
   <br>
E. INTERP_CONTROL section   <br>
该部分控制输入的格点资料的水平和垂直插值。   <br>
   <br>
1. NUM_ACTIVE_SUBNESTS: 如果C部分hgridspec中NUM_DOMAINS > 1，（即在母区域MOAD中   <br>
实行的嵌套网格），该参数表示多少个子区域进行水平和垂直插值来产生初始条件。如果仅处理MOAD，   <br>
则NUM_ACTIVE_SUBNESTS必须设为 0 。 NUM_ACTIVE_SUBNESTS 设定ACTIVE_SUBNESTS 参   <br>
数的维数，必须在 0 和sets NUM_DOMAINS-1 (含)之间.   <br>
2. ACTIVE_SUBNESTS: 如果 NUM_ACTIVE_SUBNESTS >=1 ，该参数为对应于   <br>
NUM_ACTIVE_SUBNESTS参数的一系列整数，每一个整数为预生成初始条件的子区域的ID号。每个数   <br>
值互不相同，且必须>=2 以及<=NUM_DOMAINS。当仅处理MOAD 区时(NUM_ACTIVE_SUBNEST = 0)，   <br>
该参数没有用。该参数与NUM_ACTIVE_SUBNESTS结合起来，可以设定多个同级子区域，但是在实际   <br>
运行WRF的初始化时仅选取一个子区域来处理。   <br>
3. PTOP_PA: 指定模式顶，单位为Pa。默认值为5000Pa。   <br>
4. HINTERP_METHOD: 整数，指定大气变量的插值方法。编号：   <br>
   <br>
0: 最近邻方法 (不推荐使用)   <br>
1: 4位双线性插值（如果输入和输出数据的分辨率相同，使用该选项）   <br>
2: 16位   <br>
   <br>
5. LSM_HINTERP_METHOD: 整数，指定地貌数据场所使用的插值方法。编号与上面的相同。建议的默   <br>
认值为 0 或 1 。注意：如果想使用背景资料的土地利用和土地分类，该参数必须设为 0 ，而且必须由输入   <br>
数据集中获取"VEGCAT" 和 "SOILCAT"，其中VEGCAT 为主要的土壤利用分类（USGS 为 24 种）的 2   <br>
维数组，SOILCAT为FAO主要土壤类型的 2 维数组。   <br>
   <br>
   <br>
### 6. NUM_INIT_TIMES: 整数，目前设为 1 。控制输出时间数来使用由"INIT_ROOT" 和 "LSM_ROOT" 指   <br>
   <br>
定的前缀文件。将来可以支持分析"nudging"。在 1 ：NUM_INIT_TIMES 这段时间内，使用由   <br>
INIT_ROOT/LSM_ROOT指定的数据，然后剩下的时段转而使用由"LBC_ROOT"指定的数据。如果设为 0 ，   <br>
所有的数据都来自LBC_ROOT 和 CONSTANTS_FULL_NAME。设为 1 时，与侧边界条件相比，模式可   <br>
以用不同来源的资料进行初始化得到初始场和陆面信息。   <br>
   <br>
7. INIT_ROOT: 在1:NUM_INIT_TIMES 时段内所使用数据的前缀。Wrfprep.pl脚本会在ANALPATH（见   <br>
SI_PATHS部分）中访问带有该前缀和相应时间后缀的文件。该参数仅当NUM_INIT_TIMES > 0时有用。   <br>
9. LBC_ROOT: 侧边界条件的时次所使用的数据文件的前缀。wrfprep.pl 脚本会连接"LBCPATH"目录下   <br>
的所有带有该前缀和有效时间后缀的文件。   <br>
10. LSM_ROOT: 对于每一个NUM_INIT_TIME (当 NUM_INIT_TIMES >0)， wrfprep.pl 脚本会连接在   <br>
LSMPATH 下相应时间的带有该前缀的一个文件。该参数用来指定除INIT_ROOT以外的 NOAH LSM 方   <br>
案中的输入数据。   <br>
11. CONSTANTS_FULL_NAME: 指定在"CONSTANTS_PATH"中搜寻的一系列文件名。搜寻到的文件中   <br>
的数据将在每个输出时间中使用，并且在LSM_ROOT/INIT_ROOT/LBC_ROOT 文件中作备份。   <br>
12. VERBOSE_LOG: 逻辑型参数。设为true 时在出现错误时提供更多的记录信息。   <br>
13. OUTPUT_COORD: 指定输出数据在何种垂直坐标上。有四种字符串选项：   <br>
   <br>
'ETAP': 输入数据在由LEVELS 参数指定的eta面上转化为WRF的质量形式的输出数据。   <br>
'NMMH': 输入数据在由LEVELS 参数指定的NMM 面上转化为WRF的NCEP NMM 形式的输出数   <br>
据。   <br>
'ZETA': 不再支持该坐标，选此不能正常运行！   <br>
   <br>
14. LEVELS: 按大气中的上升顺序的WRF模式中使用的垂直层次列表。如果OUTPUT_COORD 设为   <br>
'ZETA'，这些数值从 0 变化到模式顶，单位为米。如果OUTPUT_COORD 为 "ETAP"，该参数由1.0变化   <br>
到0.0。   <br>
   <br>
F. SI_PATHS Section   <br>
指定grib_prep 输出数据文件的路径。多数情况下所有这些均设为同一路径 ($EXT_DATAROOT/extprd).   <br>
   <br>
1. ANALPATH: 当NUM_INIT_TIMES > 0时文件名带有INIT_ROOT前缀的文件的路径。   <br>
2. LBCPATH: 对于所有大于 NUM_INIT_TIMES的时间段，文件名带有LBC_ROOT前缀的文件的路径。   <br>
3. LSMPATH: 对于所有0:NUM_INIT_TIMES的时间段内文件名带有LSM_ROOT前缀的文件所在路径。   <br>
4. CONSTANTS_PATH: 对于所有时间段文件名为CONSTANTS_FULL_NAME 中所包括的文件的路径。   <br>
   <br>
   <br>
### 附录3:   <br>
在WRF本体计算里，namelist.input的设定最重要。这里记述了大部分的运行设置情报。这些参数   <br>
变量的翻译是在tanghao（动力论坛）提供的WRFV2.0版本的namelist.input的翻译基础之上做了一些补   <br>
充。同时也十分感谢windrisingdl作的补充工作。限于个人的精力，全部的翻译工作没有完成。   <br>
namelist中参数变量的取值   <br>
   <br>
```   <br>
变量名 取值 描述   <br>
&time_control^ 时间控制   <br>
run_days 1 运行时间（天）   <br>
run_hours 0 运行时间（小时）   <br>
注意：如果模式积分时间大于 1 天，则可同时设置run_days和_run_hours，   <br>
也可设置run_hours一个参数。比如：模式运行的总时间长度为 36 小时，   <br>
则可设置run_days=1，且run_hours=12，或者设置run_days=0，且   <br>
run_hours=36。   <br>
run_minutes 0 运行时间（分钟）   <br>
run_seconds 0 运行时间（秒）   <br>
start_year(max_dom) 2001 四位数字表示的起始年份   <br>
start_month(max_dom) 06 两位数字(01-12)表示的起始月份   <br>
start_day(max_dom) 11 两位数字(01-31)表示的起始日数   <br>
start_hour(max_dom) 12 两位数字(00-23)表示的起始小时数   <br>
start_minute(max_dom) 00 两位数字(00-59)表示的起始分钟数   <br>
start_second (max_dom) 00 两位数字(00-59)表示的起始秒数   <br>
end_year(max_dom) 2001 四位数字表示的终止年份   <br>
end_month(max_dom) 06 两位数字(01-12)表示的终止月份   <br>
end_day(max_dom) 12 两位数字(01-31)表示的终止日数   <br>
end_hour(max_dom) 12 两位数字(00-23)表示的终止小时数   <br>
end_minute(max_dom) 00 两位数字(00-59)表示的终止分钟数   <br>
end_second (max_dom) 00 两位数字(00-59)表示的终止秒数   <br>
说明：模式的积分是用起止时间设置来控制。real.exe的   <br>
起止也是用起止时间参数来设定的。模式的积分时间可   <br>
以用run_days、run_hours等来控制，也可以用end_year、   <br>
end_month等来控制。但前者run_days等优先于后者   <br>
end_year等。而在real.exe中只用end_year等来控制结束   <br>
时间信息。   <br>
interval_seconds 21600 前处理程序的两次分析时间之间的时间间隔，以秒为单   <br>
位。也即模式的实时输入数据的时间间隔，一般为输入   <br>
边界条件的文件的时间间隔。   <br>
input_from_file (max_dom) .true / .false 嵌套初始场输入选项。嵌套时，指定嵌套网格是否用不   <br>
同的初始场文件。   <br>
fine_inpur_stream (max_dom) 0   <br>
2   <br>
selected fields from nest input   <br>
```   <br>
   <br>
history_interval (max_dom) 60 指定模式结果输出的时间间隔，以分钟为单位。   <br>
history_interval_mo(max_dom) 1 指定模式结果输出的时间间隔，以月数为单位。   <br>
history_interval_d(max_dom) 1 指定模式结果输出的时间间隔，以日数为单位。   <br>
history_interval_h(max_dom) 1 指定模式结果输出的时间间隔，以小时为单位。   <br>
history_interval_m(max_dom) 1 指定模式结果输出的时间间隔，以分钟为单位。   <br>
history_interval_s(max_dom) 1 指定模式结果输出的时间间隔，以秒数为单位。   <br>
frame_per_outfile(max_dom) 1 output times per history output file, used to split output files   <br>
into smaller pieces.   <br>
restart .true / .false 是否进行重行启动   <br>
restart_interval 1440 指定模式结果输出的时间间隔，以分钟为单位。   <br>
auxinput1_inname "met_em.d<domain>_<date>"   <br>
"wrf_real_input_em.d<domain>_<date>"   <br>
io_form_history 2 2 = NetCDF   <br>
io_form_restart 2 指定模式断点重启输出的格式, 2为netCDF格式   <br>
io_form_input 2 2 = NetCDF   <br>
io_form_boundary 指定模式边界条件数据的格式   <br>
1 二进制格式   <br>
2 NetCDF格式   <br>
4 PHD5格式   <br>
5 GRIB1格式   <br>
debug_level 0 此选项指定模式运行时的调试信息输出等级。取值可为   <br>
0,50,100,200,300，数值越大，调试信息输出就越多，默   <br>
认值为 0 。   <br>
auxhist2_outname “rainfall” 指定模式加密输出文件的文件名，缺省时取值为   <br>
“auxhist2_d_”。另外，需要指出的是，加密输出变量需要   <br>
修改注册表文件Registry.EM。   <br>
auxhist2_interval 10 此参数指定模式加密结果输出的时间间隔，以分钟为单   <br>
位。   <br>
io_form_auxhist2 2 指定模式加密输出文件的格式, 2为NetCDF格式。   <br>
nocolons .true / .false   <br>
write_input .true / .false 输出的初始场格式写成与模式结果文件格式一致   <br>
inputout_interval 180 输出的初始场文件的时间间隔，以分钟为单位   <br>
input_outname "wrf_3dv_input_d<domain>_<date>"   <br>
inputout_begin_y 0 四位数字表示输出3DVAR数据开始年份。   <br>
inputout_begin_mo 0 两位数字表示输出3DVAR数据开始月份。   <br>
inputout_begin_d 0 两位数字表示输出3DVAR数据开始日期。   <br>
inputout_begin_h 3 两位数字表示输出3DVAR数据开始时次。   <br>
inputout_begin_m 0 两位数字表示输出3DVAR数据开始分钟数。   <br>
inputout_begin_s 0 两位数字表示输出3DVAR数据开始秒数。   <br>
inputout_end_y 0 四位数字表示输出3DVAR数据终止年份。   <br>
   <br>
   <br>
inputout_end_mo 0 两位数字表示输出3DVAR数据终止月份。   <br>
inputout_end_d 0 两位数字表示输出3DVAR数据终止日期。   <br>
inputout_end_h 12 两位数字表示输出3DVAR数据终止时次。   <br>
inputout_end_m 0 两位数字表示输出3DVAR数据终止分钟数。   <br>
inputout_end_s 0 两位数字表示输出3DVAR数据终止秒数。   <br>
以上示范设置表明输入格式数据是从 3 小时后开始输出，直到 12 小时，   <br>
时间间隔是 180 分钟，即每 3 小时输出一次。   <br>
   <br>
变量名 取值 描述   <br>
&domains 区域定义：尺度、嵌套参数   <br>
time_step 60 积分的时间步长，为整型数，单位为秒，在真实大气中   <br>
推荐值为dx公里数的 6 倍   <br>
time_step_fract_num 0 实数型时间步长的分子部分   <br>
time_step_fract_den 1 实数型时间步长的分母部分   <br>
说明：如果想以60.3秒作为积分时间步长，那么可以设置time_step=60，   <br>
time_step_fract_num=3，并且设置time_step_fract_den=10。其 中time_step   <br>
对应与时间步长的整数部分，time_step_fract_num/time_step_fract_den对   <br>
应于时间步长的小数部分。   <br>
   <br>
max_dom 1 计算区域个数。计算区域默认值为 1 ，如果使用嵌套功能，   <br>
则max_dom大于 1 。   <br>
s_we(max_dom) 1 x方向(西-东方向)的起始格点值 (通常为1)   <br>
e_we(max_dom) 91 x方向(西-东方向)的终止格点值 (通常为x方向的格点数)   <br>
s_sn (max_dom) 1 y方向(南-北方向)的起始格点值 (通常为1)   <br>
e_sn (max_dom) 82 y方向(南-北方向)的终止格点值 (通常为y方向的格点数)   <br>
s_vert (max_dom) 1 z方向(垂直方向)的起始格点值   <br>
e_vert (max_dom) 28 z方向(垂直方向)的终止格点值，即全垂直eta层的总层   <br>
数。垂直层数在各嵌套网格中必须保持一致。   <br>
num_metgrid_levels 40 number of vertical levels of 3d meteorological fields coming   <br>
from WPS metgrid program   <br>
eta_levels 1.0,0.99,...0.0   <br>
force_sfc_in_vinterp 1   <br>
p_top_requested 1   <br>
lagrange_type 1   <br>
lowest_lev_from_sfc .true / .false   <br>
dx (max_dom) 10000 指定x方向的格距（单位为米）。在真实大气方案中，   <br>
此参数值必须与输入数据中的x方向格距一致。   <br>
dy (max_dom) 10000 指定y方向的格距（单位为米）。在真实大气方案中，   <br>
此参数值必须与输入数据中的y方向格距一致。   <br>
ztop (max_dom) 19000 指定模式顶的高度。在质量坐标动力框架中，此高度值   <br>
仅用于理想实验方案。   <br>
   <br>
   <br>
grid_id (max_dom) 1 计算区域的编号，一般是从 1 开始。   <br>
parent_id (max_dom) 0 嵌套网格的上一级网格（母网格）的编号，一般是从 0   <br>
开始。   <br>
i_parent_start (max_dom) 0 嵌套网格的左下角（LLC）在上一级网格（母网格）中x   <br>
方向的起始位置   <br>
j_parent_start (max_dom) 0 嵌套网格的左下角（LLC）在上一级网格（母网格）中y   <br>
方向的起始位置   <br>
parent_grid_ratio (max_dom) 1 嵌套时，母网格相对于嵌套网格的水平网格比例。在真   <br>
实大气方案中，此比例必须为奇数；在理想大气方案中，   <br>
如果将返馈选项feedback设置为 0 的话，则此比例也可   <br>
以为偶数   <br>
parent_time_step_ratio (max_dom) 1 嵌套时，母网格相对于嵌套网格的时间步长比例。   <br>
   <br>
feedback 1 嵌套时，嵌套网格向母网格得反馈作用。设置为 0 时，   <br>
无反馈作用。而反馈作用也只有在母网格和子网格的网   <br>
格比例(parent_grid_ratio)为奇数时才起作用。   <br>
smooth_option 向上一级网格（母网格）反馈的平滑选项，只有设置了   <br>
反馈选项为 1 时才起作用的。   <br>
0 不平滑   <br>
1 1-2-1 平滑   <br>
2 smoothing-desmoothing   <br>
num_moves 2 移动嵌套网格总移动次数。   <br>
move_id 2 每一次移动嵌套网格区域编号列表。   <br>
move_interval 60,120 每一次移动的启动时间列表，单位为分钟，自模式积分   <br>
起始时刻算起。   <br>
   <br>
move_cd_x 1,-1 在i方向（即东西方向）每一次相对于父网格移动格点数。   <br>
   <br>
move_cd_y -1,1 在j方向（即南北方向）每一次相对于父网格移动格点数。   <br>
   <br>
vortex_interval 15 经过多长时间计算一次涡旋的位置，单位为分钟   <br>
max_vortex_interval 40 涡旋的最大移动速度，用于计算新涡旋位置的搜索半径。   <br>
   <br>
corral_dist 8   <br>
   <br>
### 移动嵌套网格靠近粗网格边界允许的最大网格单元数，此   <br>
   <br>
### 参数也就是规定了移动网格靠近粗网格允许的最大距离。   <br>
   <br>
### 变量名 取值 描述   <br>
   <br>
&physics^ 物理方案   <br>
说明：虽然不同的嵌套网格可以使用不同的物理方案，但必须注意各种   <br>
方案的使用条件和范围。   <br>
mp_physics (max_dom) 设置微物理过程方案，默认值为 0 。   <br>
0 不采用微物理过程方案   <br>
1 Kessler 方案 (暖雨方案)   <br>
   <br>
   <br>
2 Lin 等的方案 (水汽、雨、雪、云水、冰、冰雹)   <br>
3 WSM 3类简单冰方案   <br>
4 WSM 5类方案   <br>
5 Ferrier(new Eta)微物理方案(水汽、云水)   <br>
6 WSM 6类冰雹方案   <br>
8 新Thompson的冰雹方案   <br>
98 NCEP 3类简冰方案 (水汽、云/冰和雨/雪)   <br>
99 NCEP 5类方案(水汽、雨、雪、云水和冰)（将放弃）   <br>
mp_zero_out   <br>
选用微物理过程时，保证Qv .GE. 0, 以及当其他一些水   <br>
汽变量小于临界值时，将其设置为 0 。   <br>
0 表示不控制   <br>
1 除了Qv外，所有的其他水汽变量当其小于临界值时，则   <br>
设置为 0   <br>
2 确保Qv .GE. 0, 并且所有的其他水汽变量当其小于临界   <br>
值时，则设置为 0 。   <br>
mp_zero_out_thresh 1.e-8 水汽变量（Qv除外）的临界值，低于此值时，则设置为   <br>
0 (kg/kg)。   <br>
ra_lw_physics (max_dom) 此选项指定长波辐射方案，默认值为 0 。   <br>
0 不采用长波辐射方案   <br>
1 rrtm 方案   <br>
99 GFDL (Eta) 长波方案 (semi-supported)   <br>
ra_sw_physics (max_dom) 此选项指定短波辐射方案，默认值为 0 。   <br>
0 不采用短波辐射方案   <br>
1 Dudhia 方案   <br>
2 Goddard 短波方案   <br>
99 GFDL (Eta) 短波方案 (semi-supported)   <br>
radt (max_dom) 30 此参数指定调用辐散物理方案的时间间隔，默认值为 0,   <br>
单位为分钟。建议与dx的公里数取同样的值。   <br>
cam_abs_freq_s 21600 CAM clearsky longwave absorption calculation frequency   <br>
(recommended minimum value to speed scheme up)   <br>
levsiz 59 for CAM radiation input ozone levels   <br>
paerlev 29 for CAM radiation input aerosol levels   <br>
cam_abs_dim1 4 for CAM absorption save array   <br>
cam_abs_dim2 same as e_vert for CAM 2nd absorption save array   <br>
sf_sfclay_physics (max_dom) 此选项指定近地面层(surface-layer)方案，默认值为 0 。   <br>
0 不采用近地面层方案   <br>
1 Monin-Obukhov 方案   <br>
2 MYJ Monin-Obukhov 方案 (仅用于MYJ 边界层方案)   <br>
sf_surface_physics (max_dom) 此选项指定陆面过程方案，默认值为 0 。   <br>
0 不采用陆面过程方案   <br>
   <br>
   <br>
### 1 热量扩散方案   <br>
   <br>
2 Noah 陆面过程方案   <br>
3 RUC 陆面过程方案   <br>
bl_pbl_physics (max_dom) 此选项指定边界层方案，默认值为 0   <br>
0 不采用边界层方案   <br>
1 YSU 方案   <br>
2 Eta Mellor-Yamada-Janjic TKE(湍流动能) 方案   <br>
3 NCEP Global Forecast System方案   <br>
99 MRF 方案（将放弃）   <br>
bldt (max_dom) 0 此参数指定调用边界层物理方案的时间间隔，默认值为   <br>
0 ，单位为分钟。此参数指定调用边界层物理方案的时间   <br>
间隔，默认值为 0 ，单位为分钟。0 (推荐值)表示每一个   <br>
时间步长都调用边界层物理方案。   <br>
cu_physics (max_dom) 此选项指定积云参数化方案，默认值为 0 。   <br>
0 不采用积云参数化方案   <br>
1 浅对流Kain-Fritsch (new Eta)方案   <br>
2 Betts-Miller-Janjic 方案   <br>
3 Grell-Devenyi 集合方案   <br>
4 Simplified Arakawa-Schubert方案   <br>
99 老Kain-Fritsch 方案   <br>
cudt (max_dom) 0 积云参数化方案的调用时间间隔，默认值为 0, 单位为分   <br>
钟。 一般的积云参数化方案是每一步都要调用，但如果   <br>
是用Kain-Fritsch 方案(cu_physics=1)，则可以设cudt=5。   <br>
isfflx 1 在选用扰动边界层和陆面物理过程时(sf_sfclay_physics =   <br>
1)是否考虑地面热量和水汽通量，默认值为 1 。   <br>
0 不考虑地面通量   <br>
1 考虑地面通量   <br>
ifsnow 0 是否考虑雪盖效应。考虑雪盖效应时，必须要有雪盖输   <br>
入场。默认值为 0 ，只有在利用扰动边界层PBL预报土   <br>
壤温度时才有效，即sf_surface_physics = 1。   <br>
0 不考虑雪盖效应   <br>
1 考虑雪盖效应   <br>
icloud 1 辐射光学厚度中是否考虑云的影响，默认值为 1 。仅当   <br>
ra_sw_physics = 1 和 ra_lw_physics = 1时有效。   <br>
0 不考虑云的影响   <br>
1 考虑云的影响   <br>
swrat_scat 1 scattering tuning parameter (default 1. is 1.e-5 m2/kg)   <br>
surface_input_source 土地利用类型和土壤类型数据的来源格式，默认值为 1 。   <br>
1 SI/gridgen（由SI的gridgen_model.exe程序产生）   <br>
2 其他模式产生的GRIB码数据(VEGCAT/SOILCAT 数据   <br>
   <br>
   <br>
都在由SI产生的wrf_real_input_em 文件中)   <br>
num_soil_layers 指定陆面模式中的土壤层数，默认值为 5   <br>
5 热量扩散方案   <br>
4 Noah 陆面过程方案   <br>
6 RUC 陆面过程方案   <br>
maxiens 1 默认值为 1 ，仅用于积云参数化方案中的Grell-Devenyi   <br>
集合方案   <br>
maxens 3 默认值为 3 ，仅用于积云参数化方案中的Grell-Devenyi   <br>
集合方案   <br>
maxens2 3 默认值为 3 ，仅用于积云参数化方案中的Grell-Devenyi   <br>
集合方案   <br>
maxens3 16 默认值为 16 ，仅用于积云参数化方案中的Grell-Devenyi   <br>
集合方案   <br>
ensdim 144 默认值为 144 ， 仅用于积云参数化方案中的   <br>
Grell-Devenyi集合方案   <br>
以上这些用于Grell-Devenyi方案的默认值，都是推荐使用的数值，请谨   <br>
慎修改。   <br>
seaice_threshold 271   <br>
海冰温度临界值。当TSK小于此临界值时，如果模式格   <br>
点是水体，陆面过程选用 5 层的SLAB方案，则将此模   <br>
式格点设置为陆地，且为永久性冰体；如果模式格点是   <br>
水体，陆面过程选用Noah方案，则将此模式格点设置为   <br>
陆地，且为永久性冰体，并将设置 0 ～ 3 米的TEMPS，   <br>
以及设置SMOIS和SH2O。   <br>
sst_update 0   <br>
   <br>
### 1   <br>
   <br>
### 时变海温控制参数。 0 表示不用， 1 表示使用。如果选择   <br>
   <br>
```   <br>
使用时变海温，则real.exe会从wrflowinp_d01文件中读   <br>
取SST和VEGFRA数据，wrf.exe则会以更新边条件数   <br>
据相同的时间间隔来更新这些数据。要使用此功能，则   <br>
在参数列表文件namelist.input的时间控制区还必须包含   <br>
auxinput5_interval, auxinput5_end_h, 和   <br>
auxinput5_inname = "wrflowinp_d<domain>"。   <br>
```   <br>
变量名 取值 描述   <br>
&fdda   <br>
grid_fdda (max_dom) 1 grid-nudging fdda on (=0 off) for each domain   <br>
gfdda_inname "wrffdda_d<domain>"   <br>
   <br>
变量名 取值 描述   <br>
&dynamics 扩散、抑制、平流   <br>
dyn_opt 2 模式框架配置选项，欧拉质量坐标   <br>
rk_ord Runge-Kutta时间积分方案阶数，默认值为 3   <br>
   <br>
   <br>
2 Runge-Kutta二阶   <br>
3 Runge-Kutta三阶 (推荐)   <br>
diff_opt 湍流和混合作用选项，默认值为 0   <br>
0 没有湍流或者显式空间数值滤波(km_opt将被忽略)   <br>
1 老扩散方案, 计算坐标面上二阶扩散项。如果没有指定   <br>
PBL选项，则用kvdif选项当作垂直扩散系数。通常用于   <br>
km_opt=1或者 4 。（在真实大气方案的水平分辨率格距   <br>
小于10km时，推荐使用 1 ）   <br>
2 新扩散方案, 计算物理空间(x,y,z)中的混合作用项(应力   <br>
形式)。用km_opt来指明湍流参数化过程。   <br>
km_opt 湍涡系数选项，默认值为 1   <br>
1 固定不变 (用参数配置第三部分的khdif, kvdif参数值)。   <br>
与diff_opt=1的区别在于km_opt的水平扩散作用不在模   <br>
式的zeta面上。因此，只有在没有地形的情况下，这两   <br>
个选项的作用才是相同的。   <br>
2 1.5 阶TKE(湍流动能)闭合（3D）   <br>
3 Smagorinsky 一阶闭合。 2 和 3 在水平格距大于2km时，   <br>
不推荐使用。   <br>
4 水平 Smagorinsky 一阶闭合。 4 在水平格距小于10km   <br>
时，推荐使用。   <br>
diff_6th_opt 0 6th-order numerical diffusion   <br>
0 no 6th-order diffusion (default)   <br>
1 6th-order numerical diffusion   <br>
2 6th-order numerical diffusion but prohibit up-gradient diffusion   <br>
diff_7th_factor 0.12 6th-order numerical diffusion non-dimensional rate (max   <br>
value 1.0 corresponds to complete removal of 2dx wave in   <br>
one timestep)   <br>
damp_opt 顶层抽吸作用标志选项 (当diff_opt = 1时，此选项失效)，   <br>
默认值为。 同时，必需在参数配置第三部分设置zdamp   <br>
和dampcoef参数。   <br>
0 无抽吸作用   <br>
1 有抽吸作用   <br>
2 with Rayleigh damping (dampcoef inverse time scale [1/s]   <br>
e.g. .003; not for real-data cases)   <br>
w_damping 垂直速度拟制标志选项 (用于实际业务) 默认值为 0 。   <br>
0 无抑制作用   <br>
1 有抑制作用   <br>
zdamp (max_dom) 5000 此参数设定模式顶部的抽吸厚度。推荐值为 5000 米，(仅   <br>
用于理想大气)   <br>
dampcoef (max_dom) 0 指定抽吸系数(仅用于理想大气)   <br>
base_temp 290 基本海平面温度（仅用于真实大气、质量坐标）   <br>
   <br>
   <br>
base_pres 100000 基本海平面气压，请不要改变推荐值   <br>
base_lapse 50 基本温度垂直递减率（仅用于真实大气、质量坐标），   <br>
请不要改变推荐值   <br>
khdif (max_dom) 0 水平扩散系数(单位为m^2/s)，默认值为 0 。使用此参数   <br>
时，必须设定选项diff_opt = 1 或者km_opt = 1。   <br>
kvdif (max_dom) 0 此参数设定垂直扩散系数(单位为m^2/s)，默认值为 0 。使   <br>
用此参数时，必须设定选项diff_opt = 1 或者km_opt = 1。   <br>
smdiv(max_dom) 0.1 辐散抽吸(系数) (通常取为0.1)，默认值为 0 。 此参数在   <br>
时间分裂RK方案中用于选择性地消除声波。   <br>
emdiv (max_dom) 0.01 额外模态滤波系数，默认值为 0.01。 （仅用于真实大气、   <br>
质量坐标）   <br>
epssm (max_dom) 0.1 此参数指定垂直声波的离心时间(time off-centering)，默   <br>
认值为 0.1。   <br>
non_hydrostatic(max_dom) .true. 模式动力框架参数，指定模式动力框架是否是非静力模   <br>
式，.true.为非静力，.false.为静力，默认为.False.。   <br>
pert_coriolis (max_dom) .false 科氏参数，仅影响扰动风场 (适用于理想方案)   <br>
mix_full_fields .false 与diff_opt = 2配合使用。除高分辨率的理想模拟外，推   <br>
荐取值为".true."，但damp_opt 不能同时为 1 。当   <br>
取”.false.”时，表示混合前扣除 1 维的静态廓线（base-state   <br>
profile）。   <br>
h_mom_adv_order (max_dom) 5 此选项指定水平动量平流的阶数，默认值为 3 。(例如5=5   <br>
阶，等等) ，有效值为 2 ～ 6 ，推荐值为 5 。   <br>
v_mom_adv_order (max_dom) 3 此选项指定垂直动量平流的阶数，默认值为 3 。有效值   <br>
为 2 ～ 6 ，推荐值为 3 。   <br>
h_sca_adv_order (max_dom) 5 此选项指定水平标量(scalar)平流的阶数，默认值为 3 。   <br>
有效值为 2 ～ 6 ，推荐值为 5 。   <br>
v_sca_adv_order (max_dom) 3 此选项指定垂直标量平流的阶数，默认值为 3 。有效值   <br>
为 2 ～ 6 ，推荐值为 3 。   <br>
time_step_sound (max_dom) 4 每一时间步长中声波的步数(sound steps)。通常为 4 ，默   <br>
认值为 10 。如果时间步长远大于6×dx（公里），则需   <br>
增加声波步数。   <br>
pd_moist .false positive definite advection of moisture   <br>
pd_scalar .false positive definite advection of scalars   <br>
pd_tke .false positive definite advection of chem variables   <br>
pd_chem .false positive definite advection of tke   <br>
tke_drag_coefficient (max_dom) 0 surface drag coefficient (Cd, dimensionless) for diff_opt=2   <br>
only   <br>
tke_heat_flux (max_dom) 0 surface thermal flux (H/(rho*cp), K m/s) for diff_opt=2   <br>
only   <br>
   <br>
   <br>
### 变量名 取值 描述   <br>
   <br>
&bdy_control 边界条件控制   <br>
spec_bdy_width 5 边界过渡的格点总行数，默认值为 5 。此参数只用于真实大   <br>
气方案。参数的大小至少为spec_zone 和 relax_zone的和。   <br>
spec_zone 1 指定区域(specified zone)的格点数，默认值为 1 。指定边   <br>
条件时起作用, 此参数只用于真实大气方案。   <br>
relax_zone 4 指定松弛区域的格点数，默认值为 4 。指定边条件时起作   <br>
用，此参数只用于真实大气方案。   <br>
specified (max_dom) .false. 是否使用特定边条件，逻辑型, 默认值为 .false.。 特定   <br>
边条件选项只用于真实大气方案的数值模拟中，并且要   <br>
求多个时次的边条件数据(文件wrfbdy)。   <br>
periodic_x (max_dom) .false. 在x方向是否使用周期性边界条件。逻辑型, 默认值   <br>
为 .false.。 通常只用于理想大气试验方案。   <br>
symmetric_xs (max_dom) .false. 在x方向的起始点(西边界)是否使用对称性边界条件。逻   <br>
辑型, 默认值为 .false.。通常只用于理想大气试验方案。   <br>
symmetric_xe (max_dom) .false. 在x方向的终止点(东边界)是否使用对称性边界条件。逻   <br>
辑型, 默认值为 .false.。通常只用于理想大气试验方案。   <br>
open_xs (max_dom) .false. 在x方向的起始点(西边界)是否使用自由边界条件。逻辑   <br>
型, 默认值为 .false.。通常只用于理想大气试验方案。   <br>
open_xe (max_dom) .false. 在x方向的终止点(东边界)是否使用自由边界条件。逻辑   <br>
型, 默认值为 .false.。通常只用于理想大气试验方案。   <br>
periodic_y (max_dom) .false. 在y方向是否使用周期性边界条件。 逻辑型, 默认值   <br>
为 .false.。通常只用于理想大气试验方案。   <br>
symmetric_ys (max_dom) .false. 在y方向的起始点(南边界)是否使用对称性边界条件。逻   <br>
辑型, 默认值为 .false.。通常只用于理想大气试验方案。   <br>
symmetric_ye (max_dom) .false. 在y方向的终止点(北边界)是否使用对称性边界条件。逻   <br>
辑型, 默认值为 .false.。通常只用于理想大气试验方案。   <br>
open_ys (max_dom) .false. 在y方向的起始点(南边界)是否使用自由边界条件。逻辑   <br>
型, 默认值为 .false.。通常只用于理想大气试验方案。   <br>
open_ye (max_dom) .false. 在y方向的终止点(北边界)是否使用自由边界条件。逻辑   <br>
型, 默认值为 .false.。通常只用于理想大气试验方案。   <br>
nested (max_dom) .false. 此选项设定嵌套边界条件。逻辑型, 默认值为 .false.。   <br>
   <br>
变量名 取值 描述   <br>
&namelist_quilt 参数列表的这一部分用于控制MPI异步通讯形式的输入/输出。   <br>
nio_tasks_per_group 此参数指定模式需要多少个I/O处理器：   <br>
0 不要求单独的I/O处理器。   <br>
n 如果 n>0, 表明需要n个I/O处理器。   <br>
nio_groups 1 设置为 1 ，目前为预留参数，请勿改动。   <br>
   <br>
   <br>
tile_sz_x 0 在共享式内存进程中指定x方向计算的格点数，默认值   <br>
为 0 。 如果指定了numtiles，则不需要此参数。   <br>
tile_sz_y 0 在共享式内存进程中指定y方向计算的格点数，默认值   <br>
为 0 。 如果指定了numtiles，则不需要此参数。   <br>
numtiles 1 此参数在共享式内存进程中指定每个内存块中的内存片   <br>
数，默认值为 1 。(或者是指定上面tile_sz_x和tile_sz_y   <br>
两个参数)   <br>
nproc_x -1 区域分解时，指定x方向上的上的线程数，默认值为－ 1 。   <br>
nproc_y -1 区域分解时，指定x方向上的上的线程数，默认值为－ 1 。   <br>
-1 程序自动分解   <br>
>1 用于分解的数目。   <br>
   <br>
   <br>
### 附录4:一些简单的UNIX命令：   <br>
```   <br>
 cd 命令   <br>
cd directory 改变工作目录   <br>
 ls 命令   <br>
-a 显示目录下所有子目录与文件(包括隐藏文件)   <br>
-l 显示文件的详细信息   <br>
 cp命令   <br>
 cp –r default OnlineTut   <br>
-r 递归复制源目录下所有的子目录和文件   <br>
 chmod 命令   <br>
 chmod -R u+w OnlineTut   <br>
chmod ：chang mode 改变文件或目录的访问权限   <br>
-R 以递回的方式逐个对当前目录下的所有档案与子目录进行相同的权   <br>
限变更   <br>
+ 增加权限   <br>
   <br>
- 取消权限   <br>
u 表示该档案的拥有者   <br>
w 表示可写入权   <br>
 vi 命令   <br>
 vi file_name 开始编辑或者创建一个文件   <br>
编辑命令： <Esc> 模式切换   <br>
x 删除光标所在文字   <br>
dd 删除光标所在行   <br>
a 在光标后新增文字   <br>
i 在光标前新增文字   <br>
o 在光标下方新增一行   <br>
O 在光标上方新增一行   <br>
:wq 以原档案名保存并退出   <br>
:q! 不保存文档强制退出   <br>
 rm命令   <br>
rm file_name 删除文件   <br>
rm –r deirectory_name 递归删除全部目录和子目录   <br>
 mkdir命令   <br>
mkdir directory_name 创建新目录   <br>
 rmdir 命令   <br>
rmdir directory_name 删除空目录   <br>
 unzip命令   <br>
 gunzip xxxxx.tar.gz 解压缩。   <br>
   <br>
   <br>
 tar命令   <br>
 tar –xvf xxxxx.tar 解压文件   <br>
x 从档案文件中释放文件   <br>
v 详细报告tar处理的文件信息   <br>
f 使用档案文件或设备，这个选项通常是必选的   <br>
可以和上面的⑨合写成 tar xvfz xxxxx.tar.gz   <br>
 clear命令   <br>
清除屏幕上的信息   <br>
 pwd 命令   <br>
 pwd 显示出当前工作目录的绝对路径   <br>
 <Ctrl> + C   <br>
强制放弃正在执行的任务   <br>
 exit 命令   <br>
退出UNIX系统（包括退出SSH）   <br>
```   <br>
