---
title:       "v2rayn代理"
subtitle:    ""
description: ""
date:        2024-12-20T06:19:35Z
author:      "Wayne"
image:       ""
tags:        ["dockerhub", "v2rayn", "github"]
categories:  ["Tech" ]
---


大陆的服务器由于GFW的原因无法访问外网, 故需要使用代理来访问外网。V2rayn是一个不错的代理工具, 配置简单, 使用方便。

### 免费节点订阅地址: 

1. https://www.freeclashnode.com/
2. https://github.com/barry-far/V2ray-Configs.git

### 解决dockerhub无法pull image的问题: 

国内阿里云和各个大学提供的docker镜像源服务都已停服，通过Va2ryn可以很方便的解决这个问题。

1. v2rayn配置打开*允许来自局域网的连接*；
2. 确定v2rayn的本地socket监听端口，如10808，http端口会+1切记；
3. 配置docker的daemon.json文件；
   ```
   [wangchen@localhost ~]$ cat /etc/docker/daemon.json 
    {
    "proxies": {
        "https-proxy": "http://192.168.137.1:10809",
        "http-proxy": "http://192.168.137.1:10809"
    }
    }
   ```  
   <span style="color:red;">记住这里的ip需要修改成v2rayn实际监听的网卡的ip地址</span>
4. 重启docker服务；

### 同理解决github不稳定问题

这里git直接将github的https代理设置到v2rayn的代理端口10808即可，不需要用http 10809端口，可能10809端口也可以没有尝试验证。

```
[wangchen@localhost ~]$ git config --list
user.email=xxxx
user.name=xxxx
https.https://github.com/.proxy=http://192.168.137.1:10808
```  

