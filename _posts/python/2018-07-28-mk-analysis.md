---
layout: blog
book: true
title: "MK"
background-image:
date:  2018-07-28 22:00:00
category: python
tags:
- data
- python
- analysis
---

[Python实现MK检验算法](http://bbs.06climate.com/forum.php?mod=viewthread&tid=67298)

Python 实现MK检验算法，需要用到numpy模块。需要注意输入文件数据格式为一行一数据如附件data.png.输出文件格式，第一列为UF，第二列为UB，第三四列为-1.96，1.96，如附件output.png。

```python
import numpy as np
def getuf(data):
    l = len(data)
    s = np.zeros(l,dtype=np.int32)
    uf = np.zeros(l)
    for i in range(1,l):
        r = 0
        for j in range(i):
            if(data > data[j]):
                r = r + 1
        s = s[i-1] + r
        index = i + 1
        e = (index * (index-1)) / 4
        v = index * (index - 1) * (2 * index + 5) / 72
        uf = (s - e) / np.sqrt(v)
        uf = round(uf,2)
    return uf
def main():
    ufinput = np.loadtxt("data.txt")
    uf = getuf(ufinput)
    ubinput = ufinput[::-1]
    temp = getuf(ubinput) * (-1)
    ub = temp[::-1]
    a1 = np.empty_like(uf)
    a1[:] = -1.96
    a2 = a1 * (-1)
    output = np.array([uf, ub, a1, a2])
    np.savetxt("output.txt", output.T, "%.2f", delimiter = "\t")
if __name__ == '__main__':
    main()
```


## [一些MK突变检验的例子](http://bbs.06climate.com/forum.php?mod=viewthread&tid=35802&extra=&page=1)

   [关于MK突变检验的理解及疑问 ](http://bbs.06climate.com/forum.php?mod=viewthread&tid=49601&extra=&page=1)

   [MK检验 图的UF UB交点问题及2个小小问题，请高手不吝赐教啦](http://muchong.com/html/201412/8306531.html)

# [up-rs-esp](https://up-rs-esp.github.io/mkt/)

# [python改写MK趋势检验](https://www.jianshu.com/p/1d895e2ae89f)

# [github1](https://github.com/UP-RS-ESP/mkt)

# [github2](https://github.com/mps9506/Mann-Kendall-Trend/blob/master/mk_test.py) [question](https://stackoverflow.com/questions/46856314/using-mann-kendall-in-python-with-a-lot-of-data) [test](http://michaelpaulschramm.com/2015/08/01/simple-time-series-trend-analysis/)
