---
title:       "hugo"
subtitle:    ""
description: "hugo使用学习历程"
date:        2024-12-19
author:      "Wayne"
image:       ""
tags:        ["hugo"]
categories:  ["Tech" ]
---

## Centos7上使用docker安装hugo开发环境

由于centos7上无法安装新版本的nodejs(centos7的glibc动态库版本太低不支持新版本nodejs)，所以使用docker安装hugo开发环境比较方便快捷

1. pull hugo镜像(hugomods/hugo)  
   `docker pull hugomods/hugo`
2. `docker run -it -v $PWD:/src --name hugo -p 1313:1313 hugomods/hugo /bin/sh`
3. `docker exec -it hugo /bin/sh`
4. 进入hugo容器后，就可以在里面运行各种hugo命令了(hugo new site myblog/hugo new content/hugo server等)

## content中的markdown文件不支持raw html语法

content中的markdown文件中的内容不支持html语法,如 `<span style:"red";>xxx</span>`,解决办法:  
hugo.toml中添加下面的内容:
```
[markup]
[markup.goldmark]
[markup.goldmark.renderer]
unsafe = true
```

## hosting hugo site on github pages




