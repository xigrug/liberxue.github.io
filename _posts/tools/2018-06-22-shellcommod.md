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
# 删除文件中带有某个字符串的所有行

```bash
sed -e '/xxx/d' a.txt -->打印出来 文件中包含xxx的行都不会显示 使用－i参数的话就直接修改文件了
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

# 加密

Shell脚本加密

$ wget http://www.datsi.fi.upm.es/~frosal/sources/shc-3.8.9b.tgz

$ tar xvf shc-3.8.9b.tgz

$ cd shc-3.8.9b

$ mkdir -p /usr/local/man/man1/  # 创建目录这一步这个是必须的，没这个目录会报错

$ make install

$ shc -v -r -T  -f link_db.sh

执行后，会在脚本所在目录生成两个文件，分别为
link_db.sh.x
link_db.sh.x.c
link_db.sh.x.c 是脚本的源文件，可以直接删除。 link_db.sh.x就是原来脚本的可执行文件，可随意改名，不用赋权，shc处理的过程中有赋权这一步。
