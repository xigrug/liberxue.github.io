---
layout: blog
book: true
title: "Python time_series_analysis"
background-image:  
date:  2018-07-24 19:03:56
category: research
tags:
- tools
- python
- time
- earthpy
---
[Pandas日期数据处理：如何按日期筛选、显示及统计数据](https://www.jianshu.com/p/b91e3ae940ec)

[Time series analysis with pandas](http://earthpy.org/pandas-basics.html)

[Time series analysis with pandas. Part 2](http://earthpy.org/time_series_analysis_with_pandas_part_2.html)

[利用python进行数据分析-时间序列3](https://blog.csdn.net/zhuhengv/article/details/52331572)

[Pandas中时间和日期处理](https://www.jianshu.com/p/96ea42c58abe)

[Pandas—时间索引](https://blog.csdn.net/qq_14959801/article/details/77566978)

[用 python 对人们使用自行车情况分析与预测](https://juejin.im/entry/58ec4365a22b9d00633e4c9e)

[Introduction-to-Time-Series-Analysis-with-Pandas PDF](https://itweekend.events/wp-content/uploads/2017/06/Alexander-Hendorf-Introduction-to-Time-Series-Analysis-with-Pandas.pdf)

# 工作日

[Count Workdays vs Weekends usage in pandas](https://stackoverflow.com/questions/46129799/count-workdays-vs-weekends-usage-in-pandas)

[How to group time series data by Monday, Tuesday .. ? pandas](https://stackoverflow.com/questions/28729710/how-to-group-time-series-data-by-monday-tuesday-pandas)

[Business days in Python](https://stackoverflow.com/questions/2224742/business-days-in-python) with two pakage [business_calendar](https://pypi.org/project/business_calendar/)  and [timeboard](https://github.com/mmamaev/timeboard)

[Python-获取法定节假日](https://blog.csdn.net/iamlvshijie/article/details/72630869)

## [pandas-resample-documentation](https://stackoverflow.com/questions/17001389/pandas-resample-documentation)

B       business day frequency
C       custom business day frequency (experimental)
D       calendar day frequency
W       weekly frequency
M       month end frequency
SM      semi-month end frequency (15th and end of month)
BM      business month end frequency
CBM     custom business month end frequency
MS      month start frequency
SMS     semi-month start frequency (1st and 15th)
BMS     business month start frequency
CBMS    custom business month start frequency
Q       quarter end frequency
BQ      business quarter endfrequency
QS      quarter start frequency
BQS     business quarter start frequency
A       year end frequency
BA      business year end frequency
AS      year start frequency
BAS     business year start frequency
BH      business hour frequency
H       hourly frequency
T       minutely frequency
S       secondly frequency
L       milliseonds
U       microseconds
N       nanoseconds

[resample-interpolate-time-series-data-python](https://machinelearningmastery.com/resample-interpolate-time-series-data-python/)

## [python 日期变量 判断节假日](http://bbs.pinggu.org/thread-5980288-1-1.html)

```python

from datetime import datetime
import pandas as pd

startdate = '2016-01-01'
enddate = '2016-12-31'
holiday = ['01-01', '05-01']

datalist = list(pd.date_range(start=startdate, end=enddate))
df = pd.DataFrame({'date':datalist})

df['month'] = df['date'].apply(lambda x: x.month) 
df['day'] = df['date'].apply(lambda x: x.day) 
df['weekday'] = df['date'].apply(lambda x: x.weekday()+1)

#工作日与休息日
isrest = ((df['weekday'] == 6) | (df['weekday'] == 7))  
df['label'] = isrest*1
#节假日
for h in holiday:
    #h = '01-01'
    h_month,h_day = h.split('-')
    h_index = ((df['month'] == int(h_month)) & (df['day'] == int(h_day)))
    df.loc[h_index, 'label'] = 2

```
[np.is_busday()  Custom Weekmasks](https://docs.scipy.org/doc/numpy-1.13.0/reference/arrays.datetime.html)

[Custom Frequency Ranges & Custom Business Days & Business Hour](https://pandas.pydata.org/pandas-docs/stable/timeseries.html)

[Convert dataframe date row to a weekend / not weekend value](https://stackoverflow.com/questions/32278728/convert-dataframe-date-row-to-a-weekend-not-weekend-value)

```python
df['WEEKDAY'] = ((pd.DatetimeIndex(df.index).dayofweek) // 5 == 1).astype(float)
```

[Pandas-office-10分钟开始](https://www.jianshu.com/p/dcb2a5fce1c4)

# 绘图

[pandas-seaborn-a-guide-to-handle-visualize-data-elegantly](https://tryolabs.com/blog/2017/03/16/pandas-seaborn-a-guide-to-handle-visualize-data-elegantly/)
