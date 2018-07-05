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

# [回归模型评估指标](https://mp.weixin.qq.com/s?__biz=MzI2Mjg5NDA4Ng==&mid=2247483891&idx=1&sn=36c23b0528e364f950d7b3e615914d28&chksm=ea45669add32ef8ca36b8a36062124e7664679919d847d1638bf6c1dd34967d1431cf7177d72&mpshare=1&scene=1&srcid=0704dVKqgofD0T1ibdbST9ez#rd)

> * 1.平均绝对误差（Mean Absolute Error）
> * 2.均方误差（Mean Squared Error）
MSE回归任务最常用的一个指标。
对比MAE，MSE可以放大预测偏差较大的值，可以比较不同预测模型的稳定性，应用场景相对多一点。
> * 3.方均根差（Root Mean Absolute Error）
缺点是因为使用的是平均误差，对异常值比较敏感，如果回归器对某个点的回归值很不合理，那么它的误差则比较大，从而会对RMSE的值有较大影响，即平均值是非鲁棒的。
> * 4. 误差中位数（Mean Absolute Percentage Error）
MAPE不仅仅考虑了预测值和真实值之间的误差，还考虑了误差和真实值之间的比例
> * 5.残差平方和
总平均值
y表示观测数据的平均值，
SStot表示数据集的离散程度；
SSres表示预测数据和原始数据的误差；
> * 6.R平方
R平方是多元回归中的回归平方和占总平方和的比例，它是度量多元回归方程中拟合程度的一个统计量，反映了在因变量Y的变差中被估计的回归方程所解释的比例。R平方越接近1，表明回归平方和占总平方和的比例越大，回归线与各观测点越接近。R平方>0.4表示模型拟合效果越好；但数据集越大，R平方越大，因此，不同数据集的模型结果比较会有一定的误差。
> * 7.校正R平方
n是数据集大小，K是变量个数，消除了样本数量和特征数量的影响；
> * 8. RMSPE
