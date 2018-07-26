---
layout: blog
tools: true
istop: false
title: "Python Read Data"
background-image: https://www.digitalvidya.com/wp-content/uploads/2017/04/Python-1170x630.jpg
date:  2018-06-22 10:13:56
category: tools
tags:
- tools
- quickhtml
- python
---

# 行

[Read next line in Python](https://stackoverflow.com/questions/33853900/read-next-line-in-python?rq=1)

```python

def searcher():
    print("Please enter the term you would like the definition for")
    find = input()

    with open("glossaryterms.txt", "r") as f:       
        words = list(map(str.strip, f.readlines()))
        try: 
            print(words[words.index(find) + 1])
        except:
            print("Sorry the word is not found.")
```

[add one row in a pandas.DataFrame](https://stackoverflow.com/questions/10715965/add-one-row-in-a-pandas-dataframe)
[【跟着stackoverflow学Pandas】add one row in a pandas.DataFrame -DataFrame添加行](https://blog.csdn.net/tanzuozhev/article/details/76735660)   **这里 Series 必须是 dict-like 类型**

[跟着stackoverflow学Pandas专辑](https://blog.csdn.net/column/details/16726.html)

# 列

## pandas 选择某几列

col_n = ['名称','收盘价','日期']

a = pd.DataFrame(df,columns = col_n)
