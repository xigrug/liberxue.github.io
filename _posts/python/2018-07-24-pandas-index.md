---
layout: blog
tools: true
istop: false
title: "Pandas Index"
background-image: http://t0.gstatic.com/images?q=tbn:ANd9GcTCASNmA23DKLc3G_eUXtE0FY-9j1lLWRMYDw0601xMF5L3cNSfIg
date:  2018-07-24 10:13:56
category: tools
tags:
- tools
- python
- pandas
---

# index

[pandas入门——多重索引](https://blog.csdn.net/weixin_39501270/article/details/76832857)

```python
df=df.set_index(["country","director_name"],append=True,drop=False,inplace=True)
# append参数的含义：append指定是否保留原索引，默认为False 
# drop参数的含义：drop是指该列被指定为索引后，是否删除该列，因为该列已经被指定为索引了。 
# inplace参数的含义：inplace是指是否修改原有数据集，默认为否是指返回一个新的数据集

```
[DataFrame 行列选择，切片操作，多重索引取值](https://blog.csdn.net/xingxindou123/article/details/78270769)

对带多重索引的dataframe取值一般使用 xs 
xs可以传入多个不同级别的索引进行筛选,但不支持同一级索引多选 
并且xs返回的是数值而不是引用
```python
df.xs(1, level='b')
```
