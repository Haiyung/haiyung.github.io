---
layout: post
title: go modules 由浅入深非官方手册·下：go modules 与私有包
date: 2019-09-23 15:00:00
categories: blog-cn
tags: 计算机应用技术
--- 

<h2>{{ page.title }}</h2>

* content
{:toc}

2019 年 9 月份，我负责公司 Go 项目包管理工具的迁移工作 -- 从 glide 迁移至 go modules。更换包管理器有以下几个原因：

1. glide 对包的更新、升级支持不太友好，经常出现拉取代码包超时的情况；
2. golang 有了原生支持的包管理工具 -- go modules，新工具易用、高效，完全可以替代作为第三方工具的 glide;
3. glide 近期维护速度极慢；

迁移过程中，根据让人头疼的程度，我把包分成两类：

1. 一类依靠着日趋成熟的 go modules 可以非常方便轻松的解决，它们是公有包，即放在公有仓库中、可自由拿取的包。
2. 另一类是私有包。它既包括一些你从公有包 fork 下来并进行了改造、个性化定制的包，也包括因为项目需要而开发的不对外公开的包，这些包自己就是一个独立的小项目。

在私有包上面，我遇到了许许多多让人抓狂的问题。通过一次又一次试错，有些问题逐渐有了答案，也有些问题限于时间、成本没有直接解决，而是采取了一个折衷的方案。

在本篇文章中，我将把自己在私有包上遇到的问题一一记录在案，如果你也遇到了相同的 "案子"，我真的不希望你被 "犯罪嫌疑人" 耍的团团转，真希望你能尽快将它们绳之以法。

### 声明

尽信书不如无书。

由于 go modules 是 go 1.11 的新特性，直到 1.12 以及新发布的 1.13 版本上才成为默认配置。截至成文前（2019 年 9 月 30 日），网络上可参考的、有价值的中英文文档并不多，绝大部分都是在公有包的基础上教大家使用 go modules，对私有包的讨论并不多，对私有包重定向后 IDE 的感知、跳转也少有人谈及。

十分建议大家在看后将 go modules 真正的操练起来。本篇文章即是操练的结果。因为没有做系统的、代码级的认证，我无法保证文字中的表达句句为真，可能有疏漏的地方、知识点，为此对你造成的误解我感到非常的抱歉。

不过话说回来，真的希望你能通过实践验证我的观点。一方面，勤于思索、勤于动手是个非常优秀的学习方法和习惯；另一方面，一路实践过来的你一旦发现了我的错漏之处，为了不再继续误导其他读者，也请你对于我的那些已经证伪的文章片段大胆的批评、指正，感谢你们。

### go modules 导入包的基本原理、机制

以公有包为例，当你在项目根目录下执行了 go mod init {module_name} 将项目纳入到 go modules 管理后，在当前目录执行 go mod tidy，此时 go modules 会扫描你项目中的所有 import 路径，将项目中引用到的三方包全部拎出来，这些包是 "直接依赖"，例如你项目中用到了 beego，beego 就是直接依赖，但同时 beego 项目还引用了很多依赖，这些依赖是 "间接依赖"。

go modules 会扫描到你所有的直接依赖和间接依赖，把这些依赖信息全部放入 go.mod 文件中，这样就起到了 "管理依赖" 的作用。在 go.mod 文件中，常有某个包路径后跟随 "// indirect" 字样，它就代表该包为间接依赖。

不知道大家还记不记得在 vendor 时代包管理工具的做法：需要在项目内部维护一个巨大的 vendor 包，在调用依赖的时候，优先去 vendor 目录下去查找。这样导致的一个大问题就是本来项目不大，因为依赖的包挺多，搞得项目动不动就一百万行代码。

go modules 把依赖放到了项目外部，并且直接依赖和间接依赖都统一由项目直接管理：

<p>
    <img src="/images/gomod-project-template.jpg" width="66%">
</p>

### go modules 私有包遇到的问题整理

#### 问题一：如何调用项目中的实体

我的项目结构是这样的：
```
project
│   go.mod
│   go.sum
└───folder1
│   │   main.go
└───folder2
   │   hello.go
   │   hi.go
```
我遇到的第一个问题是：在 main.go 里如何调用 folder2 包中的实体？

答：import "project/folder2"

调用本项目中的实体，仅仅需要以 go mod init {module_name} 时定义的 module_name 开头，并书写出相对路径即可。

#### 问题二：私有包放到哪里

我所在的公司搭建了仅能内网访问的 gitlab，并且登陆时有各种权限限制。我们在 go mod tidy 时，go modules 默认使用 GOPROXY 代理去获取包，而使用的 GOPROXY 代理肯定无法访问我司内网。这就成了一个大难题，要公有包自动使用 GOPROXY 代理，私有包走内网，如何实现呢？

我到现在也没有较好的解决方案。听说项目 https://docs.gomods.io/ 正在处理以上的问题,有兴趣的朋友可以尝试一下。

我最终还是把私有包放入项目内部了，那么我的项目结构就成了这样：

```
project
│   go.mod
│   go.sum
└───extensions
│   └───beego
│       │   repo.go
│       │   repo_test.go
│       │   ...
│   └───gorm
│       │   repo2.go
│       │   repo2_test.go
│       │   ...
└───folder1
│   │   main.go
└───folder2
   │   hello.go
   │   hi.go
```

#### 问题三：私有包放入项目中后，引用时还能用原来的引用方式吗
   
我在第 1 个问题中说，要引入本项目中的实体，需要从 module_name 开始引入相对路径。那么我项目中引用了 beego，这个 beego 我们还做了个性化处理，引用时怎么办？

要 import "project/extensions/beego" 这样吗？beego 作者 astaxie 好像不太能接受这样的导入哦，我相信你也认为这很丑，对吗？

能不能还是使用 github.com/astaxie/beego 呢？

当然可以。我们需要告诉 go modules，当拿 beego 包时不要去网络中取，而是直接使用当前项目中的某个目录下的 beego 就行了。有两个步骤：

1. 先将 go.mod 中的 beego 版本置为 v0.0.0，这只是为了标记该包为无版本信息的本地包：go mod edit -require=github.com/astaxie/beego@v0.0.0

2. 再将包转向至本地路径： go mod edit -replace=github.com/astaxie/beego@v0.0.0=./extensions/beego

这样，导入路径不变，还能把私有包转移到项目内部。

不过，这里面隐藏着一些问题，容我另起一个新问题。

#### 问题四：私有包中的间接依赖问题

私有包放入项目中后，也做了转向，可是发现私有包中又引用了好多包，在 IDE 中的表现是：引用错误，在你环境下找不到对应包的代码，这怎么办？

我在本文第三章节 "go modules 导入包的基本原理、机制" 中提到过，这些直接依赖的依赖包，我们称为 "间接依赖"。

在导入 github 上的第三方包时，go modules 自动为我们解析了需要哪些间接依赖。但我们现在导入的是私有包，该私有包存放在项目内部。

**私有包的间接依赖问题需要我们自己解决**。解决办法如下：

1. 以上文提到的私有包 beego 为例，我需要进入 extensions/beego 目录，在这个目录的根目录下执行：go mod init github.com/astaxie/beego

2. 继续在该目录下执行：go mod tidy

3. 进入主项目目录下，在本项目中即为 project 目录下，再次执行 go mod tidy

后面两次执行了 go mod tidy，作用是不相同的。在 beego 中执行 tidy 是将间接依赖同步至 beego 维护的包管理工具中。主项目目录下执行的 tidy 是重新扫描整个项目的依赖，更新依赖信息。

这样操作后，你再看看私有包中的依赖是不是被引用到了呢？私有包中的函数、方法能不能在你的 IDE 中正确无误的跳转呢？

#### 问题五：私有包的 module_name 问题

私有包的 module_name 要求必须是域名开头，表示你是一个标准的仓库，比如 github.com/haiyung/gomod。但是你单单起名为 haiyung/gomod 就会出问题。出问题的地方是：当你在主项目根目录下执行 go mod tidy，go modules 无法识别 haiyung/gomod 这个引用地址。并且你将 haiyung/gomod 这个包转向至本地时，也会有明显的报错：
```
执行 go mod edit -replace=haiyung/gomod=./extensions/gomod 时错误信息可见。
```

### 非必要参考文档

- https://segmentfault.com/a/1190000018414744
- http://blog.ipalfish.com/?p=443
- https://www.cnblogs.com/rongfengliang/p/11419210.html
- https://juejin.im/post/5c8f9f8ef265da612c3a34b9
- https://blog.csdn.net/weixin_34310369/article/details/88664341
- https://www.cnblogs.com/apocelipes/p/9609895.html