---
layout:     post
title:      ShadowsocksR && clash for windows，ShadowsocksX-NG && clashX 配合做代理
subtitle:   
date:       2019-3-1
author:     benjamingao
header-img: #img/clash.png
catalog: true
tags:
    - 翻墙
    - 代理
---

## 前言

> 本文参考：
>> https://blog.nliu.work/post/20171105-surge-ssr-v2ray/#surge-%E9%83%A8%E5%88%86
>> http://dsh.li/blog/15165280517003.html

- 假设你已经会使用这两款软件

### 这样配合的作用

- 能够是 clash “使用” SSR 协议

## macOS

### ShadowsocksX-NG

> 软件版本：版本 1.4.3-R8 (2)

- ShadowsocksX-NG 里设代理模式为 **手动模式**

### clashX

> 软件版本：1.9.5

- 编辑配置文件，假设你已经理解配置文件了

```yaml
Proxy:
# name：随意，我这里是 socks;
# type：不可更改
# server：一般本地都是这个地址
# port：这里的端口填写 ShadowsocksX-NG 里高级设置的本地 socks5 监听端口

# socks5
- { name: "socks", type: socks5, server: 127.0.0.1, port: 1086 }

Proxy Group:
# name：依据 Rule 所对应的修改
# type：不可更改
# proxies：不可更改

# select
- { name: "Proxy", type: select, proxies: ["socks"] }
```

### 补充图片

![](https://ws1.sinaimg.cn/large/005Fm2E0ly1g0nmvjyzzfj30dc03lt8y.jpg)

## windows

### shadowsocksR

这样设置：

![](https://ws1.sinaimg.cn/large/005Fm2E0ly1g0ppg469j2j30bw0axmxl.jpg)

### clash for windows

- 编辑配置文件，假设你已经理解配置文件了

```yaml
Proxy:
# name：随意，我这里是 socks;
# type：不可更改
# server：一般本地都是这个地址
# port：这里的端口填写 shadowsocksR 里高级设置的本地 socks5 监听端口

# socks5
- { name: "socks", type: socks5, server: 127.0.0.1, port: 1080 }

Proxy Group:
# name：依据 Rule 所对应的修改
# type：不可更改
# proxies：不可更改

# select
- { name: "Proxy", type: select, proxies: ["socks"] }
```

![](https://ws1.sinaimg.cn/large/005Fm2E0ly1g0ppjfqi5aj30h70ef0tf.jpg)

#### clash for windows 代理成功的表现：

登陆谷歌，注意 General 里 System proxy 要打钩。

![](https://ws1.sinaimg.cn/large/005Fm2E0ly1g0ppjomtjpj30wi0r0wmp.jpg)

## Bug

- 在两款软件如此设置、使用以后，如果你此时把 `ShadowsocksX-NG` 退出，然后再打开 `ShadowsocksX-NG` 这个软件，这时代理不起作用，`clashX` 是不走流量的。这时的一个解决办法是把 `clashX` 里的系统代理关闭，然后再打开，就又可以走流量了。

