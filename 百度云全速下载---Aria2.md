
---
title: 百度云全速下载教程---Aria2
date: 2017-3-01
---

### 百度云全速下载教程
> 不知道各位平时有没有使用百度云下载但是被百度元下载时的限速气的不行的体验，今天就是在这里教大家如何科学的使用aria2来下载百度云的资源

Aria2是一个轻量级的下载工具，支持http，https，ftp，sftp，bittorrent，metalink等多种协议，能够在windows，linux，macos甚至是Android上面运行。
Aria2有两种下载模式：

<!-- more -->

- 一种为命令行下载模式(cli) 
```
aria2c http://example.com/download/link  //aria2c 加上下载链接地址就可以实现下载
```
- 一种为远程调用(rpc server)

前者上手需要一定的能力，后者更为方便一些，可以理解rpc模式相当于aria2在我们的本机上以后台的形式跑了起来，然后它可以一直监听指定的端口号，一旦需要下载东西就可以调用这个“后台”的api实现下载。当然现在aria2只是以"后台程序"的方式跑起来，还需要一个工具来调用这个后台程序的api，这个“前台程序"就是YAAW，我们可以使用YAAW来轻松实现下载。

YAAW有三种使用方式：
- chrome的插件 [下载地址](https://chrome.google.com/webstore/detail/yaaw-for-chrome/dennnbdlpgjgbcjfgaohdahloollfgoc)
- 也有基于webkit的客户端 [下载地址](https://github.com/yangshun1029/aria2gui/releases/download/1.2.9/Aria2GUI-v1.2.9.zip)  [github项目详情页](https://github.com/yangshun1029/aria2gui)
- 还可以使用在线网页版的[YAAW](http://binux.github.io/yaaw/demo/)  or [webUI](http://ziahamza.github.io/webui-aria2/)

上述的三种方式其实都只是对Aria2的一个界面管理而已，最终的下载功能还是通过Aria2来实现。
Aria2的启动还需要一个配置文件来启动，我把配置文件的内容贴出来，大家粘贴到一个aria2.conf的文件中保存起来

```
    #用户名
    #rpc-user=user
    #密码
    #rpc-passwd=passwd
    #上面的认证方式不建议使用,建议使用下面的token方式
    #设置加密的密钥
    #rpc-secret=token
    #允许rpc
    enable-rpc=true
    #允许所有来源, web界面跨域权限需要
    rpc-allow-origin-all=true
    #允许外部访问，false的话只监听本地端口
    rpc-listen-all=true
    #RPC端口, 仅当默认端口被占用时修改
    #rpc-listen-port=6800
    #最大同时下载数(任务数), 路由建议值: 3
    max-concurrent-downloads=5
    #断点续传
    continue=true
    #同服务器连接数
    max-connection-per-server=5
    #最小文件分片大小, 下载线程数上限取决于能分出多少片, 对于小文件重要
    min-split-size=10M
    #单文件最大线程数, 路由建议值: 5
    split=10
    #下载速度限制
    max-overall-download-limit=0
    #单文件速度限制
    max-download-limit=0
    #上传速度限制
    max-overall-upload-limit=0
    #单文件速度限制
    max-upload-limit=0
    #断开速度过慢的连接
    #lowest-speed-limit=0
    #验证用，需要1.16.1之后的release版本
    #referer=*
    #文件保存路径, 默认为当前启动位置
    dir=/home/acgotaku/Downloads
    #文件缓存, 使用内置的文件缓存, 如果你不相信Linux内核文件缓存和磁盘内置缓存时使用, 需要1.16及以上版本
    #disk-cache=0
    #另一种Linux文件缓存方式, 使用前确保您使用的内核支持此选项, 需要1.15及以上版本(?)
    #enable-mmap=true
    #文件预分配, 能有效降低文件碎片, 提高磁盘性能. 缺点是预分配时间较长
    #所需时间 none < falloc ? trunc << prealloc, falloc和trunc需要文件系统和内核支持
    file-allocation=prealloc
```
我们可以现在可以使用命令将Aria2启动起来：
```
aria2 --conf-path=<path>  //path 就是配置文件存放的路径，需要是绝对路径
```

启动后可以看到Aria2在监听着6800端口

未完，待续。。。