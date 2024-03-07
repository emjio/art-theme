---
title: wsl 使用介绍
desc: WSL是Windows Subsystem for Linux的缩写，是微软推出的运行在Windows子系统上的Linux系统。WSL 2提高了文件系统性能和系统调用兼容性。相比虚拟机，WSL提供完整的Linux环境，具有对Windows程序的调用能力，方便双向操作。使用WSL带来Linux开发友好性、快捷的程序安装、高效的文件执行和IO任务性能提升。安装WSL简便，配置环境后可安装oh-my-zsh等工具，在VS Code中集成WSL进行开发。利用npm包n、tmux、batcat、zsh插件可提升效率，通过alias快速调用Windows程序。
theme: normal
pubDate: 2022/1/16 
author: pakchoi
hero: "https://blog-emjio.vercel.app/wsl/0.png"
categories: 
    - linux
    - vim 
    - wsl
    - vscode
---


## [WSL是什么？](https://blog-emjio.vercel.app/wsl#wsl%E6%98%AF%E4%BB%80%E4%B9%88)

WSL是微软出品的 运行在Windows子系统。全称`Windows Subsystem for Linux`

到现在已经到了第二个版本

> WSL 2 是适用于 Linux 的 Windows 子系统体系结构的一个新版本，它支持适用于 Linux 的 Windows 子系统在 Windows 上运行 ELF64 Linux 二进制文件。 它的主要目标是​**提高文件系统性能**​，以及添加​**完全的系统调用兼容性**​。

在WSL中你将获得一套完整的Linux环境（继承自Window）和对Window程序的调用能力。

<iframe width="100%" height="315" src="https://www.youtube.com/embed/48k317kOxqg" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen=""></iframe>

## [为什么不直接用虚拟机？](https://blog-emjio.vercel.app/wsl#%E4%B8%BA%E4%BB%80%E4%B9%88%E4%B8%8D%E7%9B%B4%E6%8E%A5%E7%94%A8%E8%99%9A%E6%8B%9F%E6%9C%BA)

与虚拟机不同。他是一个运行在Window 环境下由微软的某种桥接技术进行连接的系统运行方式。对于Window 而言，Linux 是其子系统。对于Linux ，Windows 是挂载在他上面的几个目录。得益于这种酷炫的连接方式。我们可以非常方便的在两个系统中进行双向操作。

## [前置知识](https://blog-emjio.vercel.app/wsl#%E5%89%8D%E7%BD%AE%E7%9F%A5%E8%AF%86)

* 基本的Linux 命令认知（快速入门linux可以参考另一篇文章）

[linux服务器维护](https://blog-emjio.vercel.app/linux/)

* 不愿意就此打住的脑子
* 持续改进的心

## [使用他能带来什么好处？](https://blog-emjio.vercel.app/wsl#%E4%BD%BF%E7%94%A8%E4%BB%96%E8%83%BD%E5%B8%A6%E6%9D%A5%E4%BB%80%E4%B9%88%E5%A5%BD%E5%A4%84)

* Linux 天然的开发亲和力
* 方便快捷的各类程序安装
* 高效率的文件执行/IO密集任务性能提升明显
* 高度自定义化的Shell集成
* 沉浸式的开发体验
* 无限的可能性

## [如何使用一个WSL环境？](https://blog-emjio.vercel.app/wsl#%E5%A6%82%E4%BD%95%E4%BD%BF%E7%94%A8%E4%B8%80%E4%B8%AAwsl%E7%8E%AF%E5%A2%83)

### [安装WSL](https://blog-emjio.vercel.app/wsl#%E5%AE%89%E8%A3%85wsl)

安装过程见微软官方文档 只需要几次命令输入即可快速拥有\`

[安装 WSL](https://docs.microsoft.com/zh-cn/windows/wsl/install)

我们在内部使用的时候也发现了一些在安装上的问题

当然绝大部分问题可以直接访问WSL的github 仓库

[https://github.com/microsoft/WSL](https://github.com/microsoft/WSL)

### [配置你的环境](https://blog-emjio.vercel.app/wsl#%E9%85%8D%E7%BD%AE%E4%BD%A0%E7%9A%84%E7%8E%AF%E5%A2%83)

安装和基础的终端配置可见此处。目前最好的wsl入门中文文档

[Dev on Windows with WSL](https://dowww.spencerwoo.com/)

安装世界上最酷的shell环境`oh-my-zsh`

(如果不会科学上网可以找gitee上的镜像)

然后安装一切你喜欢的插件

这里是一个列举了zsh知名插件的仓库地址

[https://github.com/unixorn/awesome-zsh-plugins.git](https://github.com/unixorn/awesome-zsh-plugins.git)

## [真实wsl 开发使用演示](https://blog-emjio.vercel.app/wsl#%E7%9C%9F%E5%AE%9Ewsl-%E5%BC%80%E5%8F%91%E4%BD%BF%E7%94%A8%E6%BC%94%E7%A4%BA)

首先贴出一份我自己的个人配置作为参考

[https://github.com/emjio/oh-my-zsh-backup](https://github.com/emjio/oh-my-zsh-backup)

### [在vscode 中集成wsl 开发](https://blog-emjio.vercel.app/wsl#%E5%9C%A8vscode-%E4%B8%AD%E9%9B%86%E6%88%90wsl-%E5%BC%80%E5%8F%91)

你只需要把你的项目代码放在你的wsl 的文件夹里面

wsl 中 进入目录

<pre class="shiki material-default" bash="true"><div class="code-container"><code><div class="line"><span>code </span><span>.</span></div></code></div></pre>

![Untitled](https://blog-emjio.vercel.app/wsl/0.png)

只在`linux`中被支持的 npm 包 `n`

可以支持快速多个版本的NodeJs的安装和切换

![Untitled](https://blog-emjio.vercel.app/wsl/1.png)

使用`tmux` 在一个终端中进行拆分和任务切换

![Untitled](https://blog-emjio.vercel.app/wsl/2.png)

能够根据格式读取文件并且进行语法高亮的`batcat`

![Untitled](https://blog-emjio.vercel.app/wsl/3.png)

能够帮你进行命令正确提示和历史命令输入建议的 `zsh-syntax-highlighting` 和 `zsh-autosuggestions`

![Untitled](https://blog-emjio.vercel.app/wsl/4.png)

错误命令为红色

![Untitled](https://blog-emjio.vercel.app/wsl/5.png)

正确命令为绿色并且如果输入的这部分是历史输入过的会进行提示

这对于前端经常输入 yarn 或者`yarn serve` 非常省事情 你只要打个y 就能提示出来了

一个非常沙雕的工具 “thefuck\`\`\` 会根具你上次输入错误的命令提示你正确的

![Untitled](https://blog-emjio.vercel.app/wsl/6.png)

最后就是各种提升效率的alias

![Untitled](https://blog-emjio.vercel.app/wsl/7.png)

上面分别是

* 快速在文件浏览器打开当前路径
* 快速复制当前路径到粘贴板
* 快速打开google 搜索某个关键词
* 快速大概github 搜索某个关键词

所以你就知道了wsl 可以快速的调用windows 下面的任何程序，并根据他提供的参数进行快速的启动。
