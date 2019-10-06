---
layout: cnpost
title: go modules 由浅入深非官方手册·上：go modules 与公有包
date: 2019-09-17 10:00:00
categories: cn
tags: 计算机应用技术
--- 

__Contents__

* content
{:toc}

### 前言

什么是包？什么是包管理工具？包管理工具的作用是什么？与 ruby 的 gem 或 bundler, Java 的 maven, python 的 pip,乃至 ubuntu 的 apt, RedHat 的 yum 是否类似？有哪些异同？Golang 有哪些包管理工具？有何异同？为什么偏要使用 go modules?

你可能会有以上问题。本文致力于解决以上的问题。当然，若我发现某些地方已经有人做出了精确、精简又通俗易懂，我等只能在一旁拍案叫绝的解释时，就像李白说的 "眼前有景道不得，崔颢题诗在上头"，我便只好把地址贴在 "参考文档" 中，以飨诸君。

另外需要注明的是，本文仅针对 go modules 的入门指引。我或者我引用的其他作者的文章，都是在基础层面告诉你如何使用 go modules，如何像使用 vendor 一样导入一个放在公共仓库（例如：github）中的包，不涉及私有仓库的讨论。如果你恰好有关于私有包导入方面的疑惑，也许下一章节《go modules 由浅入深非官方手册·下：go modules 与私有包》会给你一点启发。

### 包与 Golang 的包

我们不需要事事亲力亲为。有很多东西，尤其是别人开源出来的代码，我们能直接用就直接用了，一个原因是节省了开发成本，另一个原因是自己写的未必就比人家做出来的强。

你用过 python 写过爬虫吗？里面常用到一个 requests 模块，这个模块不是标准库中的，你需要使用 pip install requests 手动安装，还有小游戏模块 pygame 也是如此。requests 和 pygame 都是模块名字，通过指定模块名，pip 就可以去远方获取相关代码片段了。

或者你使用过 ruby 吗？前些日子我尝试用 ruby on rails 搭建网站时刚接触过它。ruby 自带 gem 包管理工具，通过 gem install rails 即可安装 rails 框架，使用的方式与 python 中的 pip 类似。

这些不同语言的包管理器，我的看法是，没有什么大的区别，都是通过一个工具将散落在网络各个角落上的第三方包拽到本地，供自己开发使用。

Golang、Java 与 python、ruby 导入包的格式略有不同。也许是同为编译型 + 静态类型语言的原因（那种刻在骨子里的严谨）。Java 为了保证包命名的唯一性，要求定义包名前加上唯一的前缀，由于互联网上的域名是不会重复的，所以包名就变成了这样：org.apache.logging.log4j。Golang 的第三方包中很大部分来自于 github 上个人或者团队的贡献，当然你肯定也会经常看到 golang.org/x/ 开头的包，这些包之所以用域名开头的原因与 Java 类似，都是要确保地址的唯一性。比如，Golang 标准库中有 net 包，但很多时候我们不直接 import "net",而是 import "golang.org/x/net",同样是 net 包，但导入的代码是不同的。这是与 ruby/python/apt 这些包管理工具不同的地方。

### Golang 包管理器演进的三个阶段 

> 见参考文档 [1]

go modules 是个第三方包的管理工具, 它替代了 vendor, 不再把三方包放入项目文件中, 而仅仅在项目中保存一份 "配置文件" 即 go.mod 文件。个人下载项目后, 可以通过配置文件简单、快捷的下载相关依赖至本地。

### 使用前 go modules 的相关配置

#### 升级 Golang

请升级 Golang 至 1.11+ 版本。建议升级至最新版。本文写作于 2019 年 10 月初，此时最新的版本为 1.13，因此我更新到了 1.13。

#### 查看系统环境变量 GOPATH

查看你的系统环境变量 GOPATH 中是否包含你所在的项目地址,若存在,则将该地址删除,保证你所要迁移的项目不在 GOPATH 中 (原因: go modules 与 GOPATH 的工作模式不同);

#### 检查 IDE 配置

若你使用的集成开发工具为 Goland 或 IDEA, 请在该项目的 GOPATH 配置中取消选中 "Use GOPATH ..." && "Index ...", 确保本项目不在 GOPATH 列表中:

<p>
    <img src="/images/go-modules-gopath-settings.jpg" width="36%">
</p>

我正在使用的 IDE 是 IntelliJ IDEA 2019.2.2。

#### 配置IDE使其支持 go modules

<p>
    <img src="/images/go-modules-settings.jpg" width="36%">
</p>

配置 GOPROXY 是为了在获取一些不方便得到的包时使用代理( 例如golang.org/x/... 模块 ),推荐的 GOPROXY 有:

- [推荐]七牛云: https://goproxy.cn/
- 阿里云: https://mirrors.aliyun.com/goproxy/ 
- goproxy.io:https://goproxy.io/

注意：当你的项目为 GOPATH + vendor 模式时，有时你发现始终无法导入某个位于本地的模块，这时就要看看是否开启了 go modules。因为go modules 模式下导入包的机制与 vendor 是不同的。

### 新项目·使用 go modules 之解决方案



### 老项目·包管理器迁移至 go modules 之解决方案



### 参考文档
1. https://windmt.com/2018/11/08/first-look-go-modules/
2. 