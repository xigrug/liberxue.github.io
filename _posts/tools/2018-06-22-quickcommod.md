---
layout: blog
istop: false
title: "linux 替换"
background-image: https://timgsa.baidu.com/timg?image&quality=80&size=b9999_10000&sec=1529677893935&di=ca0822ba046b06a333122b6c85249061&imgtype=0&src=http%3A%2F%2Fuploads.xuexila.com%2Fallimg%2F1511%2F646-15112G45223209.jpg
date:  2018-06-21 19:33:56
category: tools
tags:
- tools
- quickcommad
- shell
---

# 批量替换
<head>
    <title>Rouge</title>
    <link media="all" rel="stylesheet" type="text/css" href="../../assets/rouge/rouge.css" />
    <style>
        pre{
            background: rgba(0, 0, 0, 0.95);
        }
    </style>
</head>

<body>
    {% highlight shell %}
    sed -i "s/liberxue/xigrug/g" `grep liberxue -rl _site`
    {% endhighlight %}
</body>
