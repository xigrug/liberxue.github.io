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
- markdown
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
