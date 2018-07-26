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

# 工作日

[Count Workdays vs Weekends usage in pandas](https://stackoverflow.com/questions/46129799/count-workdays-vs-weekends-usage-in-pandas)

[How to group time series data by Monday, Tuesday .. ? pandas](https://stackoverflow.com/questions/28729710/how-to-group-time-series-data-by-monday-tuesday-pandas)

[Business days in Python](https://stackoverflow.com/questions/2224742/business-days-in-python) with two pakage [business_calendar](https://pypi.org/project/business_calendar/)  and [timeboard](https://github.com/mmamaev/timeboard)

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

[Custom Frequency Ranges & Custom Business Days & Business Hour](https://pandas.pydata.org/pandas-docs/stable/timeseries.html)
