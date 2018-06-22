---
layout: blog
istop: true
title: "linux 替换"
date:  2018-06-21 19:33:56
category: tools
tags:
- tools
- quickcommad
- shell
---

# 批量替换


```{r, engine='bash'}
 sed -i "s/liberxue/xigrug/g" `grep liberxue -rl _site`

```
