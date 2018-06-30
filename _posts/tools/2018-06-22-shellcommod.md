---
layout: blog
istop: false
title: "Linux 之 Shell"
background-image: https://timgsa.baidu.com/timg?image&quality=80&size=b9999_10000&sec=1529677893935&di=ca0822ba046b06a333122b6c85249061&imgtype=0&src=http%3A%2F%2Fuploads.xuexila.com%2Fallimg%2F1511%2F646-15112G45223209.jpg
date:  2018-06-21 19:33:56
category: tools
tags:
- tools
- quickcommad
- shell
---


# 批量替换   
```bash
    sed -i "s/liberxue/xigrug/g" `grep liberxue -rl _site`
```

# 文件大小 <a href="https://www.jb51.net/article/108256.htm" title="Linux中du-查看文件夹大小并按大小进行排序详解">du-</a>
```bash
   du -s * | sort -nr | head   #选出排在前面的10个
```

# 重命名

 [rename](https://blog.csdn.net/qq_27803491/article/details/50404677)
 
 先举个例子来感受下，比如将当前目录下所有*.nc文件中Sam3替换成Stm32，命令如下：
 
> rename -n 's/Sam3/Stm32/' *.nc　　/*确认需要重命名的文件*/
> rename -v 's/Sam3/Stm32/' *.nc　　/*执行修改，并列出已重命名的文件*/
