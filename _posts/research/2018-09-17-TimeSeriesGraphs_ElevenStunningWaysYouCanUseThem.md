---
layout: blog
tools: true
istop: false
title: "Time Series Graphs & Eleven Stunning Ways You Can Use Them"
background-image: 
date:  2018-06-26 10:13:56
category: research
tags:
- research
- Times-series
---



[Time Series Graphs & Eleven Stunning Ways You Can Use Them](https://blog.csdn.net/xmuecor/article/details/45216797)
==========================================================

2015年04月23日 08:57:31 [rokia_xmu](https://me.csdn.net/u014032673) 阅读数：952

个人分类： [R](https://blog.csdn.net/u014032673/article/category/2102319) [数据可视化](https://blog.csdn.net/u014032673/article/category/2378411)

(This article was first published on **[Plotly Blog](http://blog.plot.ly/post/117105992082)**, and kindly contributed to [R-bloggers)](http://www.r-bloggers.com/)

Many graphs use a [time series](http://en.wikipedia.org/wiki/Time_series), meaning they measure events over time. [William Playfair](http://en.wikipedia.org/wiki/William_Playfair) (1759 - 1823) was a Scottish economist and pioneer of this approach. Playfair invented the line graph. The graph below–one of his most famous–depicts how in the 1750s the Brits started exporting more than they were importing.  
  
  
![](http://i0.wp.com/i.imgur.com/ycJetYr.png?w=456)  
  
  

This post shows how you can use Playfair’s approach and many more for making a time series graph. To embed Plotly graphs in your applications, dashboards, and reports, check out [Plotly Enterprise](https://plot.ly/product/enterprise/).  
  
  

1\. By Year
-----------

  
  
  
First we’ll show an example of a standard time series graph. The data is drawn from a paper on shaving trends. The author concludes that the “dynamics of taste”, in this case facial hair, are _“common expressions of underlying conditions and sequences in social behavior.”_ Time is on the x-axis. The y-axis shows the respective percentages of men’s facial hair styles.  
  
  

[![<br><b>Men's Facial Hair Trends, 1842 to 1972</b>](https://plot.ly/~Dreamshot/1452.png)](https://plot.ly/~Dreamshot/1452/ "<br><b>Men's Facial Hair Trends, 1842 to 1972</b>")

  
  
  
You can click and drag to move the axis, click and drag to zoom, or toggle traces on and off in the legend. The [temperatue graph below](http://moderndata.plot.ly/update-plotly-charts-with-cron-jobs-and-python/) shows how Plotly adjusts data from years to nanoseconds as you zoom. The first timestamp is 2014-12-15 08:55:13.961347, which is how Plotly reads dates. That is, \`yyyy-mm-dd HH:MM:SS.ssssss\`. Now that’s drilling down.  
  
  
![](http://i2.wp.com/i.imgur.com/cdKMdQU.gif?w=456 "source: imgur.com")  
  
  
One of the special things about Plotly is that you can translate plots and data between programming lanuguages, file formats, and data types. For example, the [multiple axis plot](https://plot.ly/online-graphing/tutorials/multiple-y-axes-graphs/) below uses stacked plots on the same time scale for different eonomic indicators. This plot was made using [ggplot2’s time scale](http://docs.ggplot2.org/current/scale_date.html). We can convert the plot into Plotly, allowing anyone to edit the figure from different programming languages or the Plotly web app.  
  
  

[![pce, pop, psavert, uempmed, unemploy](https://plot.ly/~MattSundquist/10864.png)](https://plot.ly/~MattSundquist/10864/ "pce, pop, psavert, uempmed, unemploy")

  
  
  
We have a [time series tutorial](https://plot.ly/online-graphing/tutorials/dates-time-series-and-timestamp-formatting-in-plotly/%20) that explains time series graphs, custom date formats, custom hover text labels, and time series plots in [MATLAB](/), [Python](https://plot.ly/python/time-series/), and [R](https://plot.ly/r/time-series/).  
  
  

2\. Subplots & Small Multiples
------------------------------

  
  
  
Another way to slice your data is by [subplots](https://plot.ly/online-graphing/tutorials/multiple-y-axes-graphs/). These [histograms](http://help.plot.ly/histograms/) were [made with R](http://nbviewer.ipython.org/gist/mkcor/0ee7c73d9ba4c68ddc1a/) and compare yearly data. Each plot shows the annual number of players who had a given batting average in Major League Baseball.  
  
  

[![2004, 2005, 2006, 2007, 2008, 2009, 2010, 2011, 2012, 2013](https://plot.ly/~MattSundquist/11035.png)](https://plot.ly/~MattSundquist/11035/ "2004, 2005, 2006, 2007, 2008, 2009, 2010, 2011, 2012, 2013")

  
  
  
You can also display your data using [small multiples](http://en.wikipedia.org/wiki/Small_multiple), a concept developed by [Edward Tufte](https://twitter.com/EdwardTufte). Small multiples are “illustrations of postage-stamp” size. They use the same graph type to index data by a cateogry or label. Using [facets](http://is-r.tumblr.com/post/33829008995/faceting-as-a-preferable-alternative-to-3-d), we’ve plotted a [dataset of airline passengers](https://stat.ethz.ch/R-manual/R-devel/library/datasets/html/AirPassengers.html). Each subplot shows the overall travel numbers and a reference line for the thousands of passengers travelling that month.  
  
  

[![,     ,     ,     ,     ,     ,     ,     ,     ,     ,     ,     , Jan, Feb, Mar, Apr, May, June, July, Aug, Sep, Oct, Nov, Dec](https://plot.ly/~MattSundquist/10875.png)](https://plot.ly/~MattSundquist/10875/ ",     ,     ,     ,     ,     ,     ,     ,     ,     ,     ,     , Jan, Feb, Mar, Apr, May, June, July, Aug, Sep, Oct, Nov, Dec")

  
  
  

3\. By Month
------------

  
  
  
The heatmap below shows the percentages of people’s birthdays on a given date, gleaned from 480,040 life isurance applications. The x-axis shows months, the y-axis shows the day of the month, and the z shows the % of birthdays on each date.  
  
  

[![<br>How Common is Your Birthday?](https://plot.ly/~Dreamshot/354.png)](https://plot.ly/~Dreamshot/354/ "<br>How Common is Your Birthday?")

  
  
  
To show how values in your data are spaced over different months, we can use [seasonal boxplots](http://stackoverflow.com/questions/12052305/what-is-the-most-elegant-way-to-split-data-and-produce-seasonal-boxplots). The boxes represent how the data is spaced for each month; the dots represent outliers. We’ve used ggplot2 to make our plot and added a smoothed fit with a confidence interval. See our [box plot tutorial](https://plot.ly/box-plot/) to learn more.  
  
  

[![Box plot with Smoothed Fit](https://plot.ly/~MattSundquist/10984.png)](https://plot.ly/~MattSundquist/10984/ "Box plot with Smoothed Fit")

  
  
  
We can use a bar chart with error bars to look at data over a monthly interval. In this case, we’re [using R](http://moderndata.plot.ly/easy-error-bars-with-r-and-plotly/) to make a graph with error bars showing snowfall in Montreal.  
  
  

[![Snowfall in Montreal by Month](https://plot.ly/~chelsea_lyn/158.png)](https://plot.ly/~chelsea_lyn/158/ "Snowfall in Montreal by Month")

  
  
  

4\. A Repeated Event With A Category
------------------------------------

  
  
  
We may want to look at data that is not stricly a time series plot, but still represents changes over time. For example, we may want hourly event data. Below we’re showing the most popular hourly reasons to call [311 in NYC](http://www1.nyc.gov/311/index.page), a number you can call for non-emergency help. The plot is from our [pandas and SQLite guide](https://plot.ly/ipython-notebooks/big-data-analytics-with-pandas-and-sqlite/).  
  
  

[![The 6 Most Common 311 Complaints by Hour in a Day](https://plot.ly/~MattSundquist/10789.png)](https://plot.ly/~MattSundquist/10789/ "The 6 Most Common 311 Complaints by Hour in a Day")

  
  
  
We can also show a before and after effect to examine changes from an event. The plot below, made in an [IPython Notebook](https://plot.ly/ipython-notebooks/ukelectionbbg/), tracks Conservative and Labour election impacts on Pounds and Dollars.  
  
  

[![GBP USD during UK general elections by winning party](https://plot.ly/~MattSundquist/11482.png)](https://plot.ly/~MattSundquist/11482/ "GBP USD during UK general elections by winning party")

  
  
  

5\. A 3D Graph
--------------

  
  
  
We can also use a 3D chart to show events over time. For example, our surface chart below shows the UK Swaps Term Structure with historical dates along the X axis, the Term Structure on the Y axis, and the swap rates over the Z Axis. The message: rates are lower than ever. At the long end of the curve we don’t see a massive increase. This example was made using [cufflinks](https://github.com/santosjorge/cufflinks), a Python library by [Jorge Santos](https://twitter.com/jorgesantos). For more on 3D graphing see our [Python](https://plot.ly/python/3d-plots-tutorial/), [MATLAB](https://plot.ly/matlab/), [R](https://plot.ly/r/), and [web tutorials](https://plot.ly/online-graphing/tags/3d-graphs/).  
  
  

[![<br>UK Swap Rates](https://plot.ly/404.png)](https://plot.ly/~MattSundquist/11399/ "<br>UK Swap Rates")

  
  
  

Sharing & Deploying Plotly
--------------------------

  
  
  
If you liked this post, please consider sharing. We’re [@plotlygraphs](https://twitter.com/plotlygraphs), or email us at feedback at plot dot ly. We have [tutorials](https://plot.ly/online-graphing/) that show how to make and embed graphs in your website, blog, or apps. To learn more about how companies are using Plotly Enterprise across different industries, see our [customer stories](https://plot.ly/product/enterprise/customer-stories/).  
  
  
[](https://plot.ly/product/enterprise/customer-stories/)



