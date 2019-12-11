---
layout: post
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

你可能会有以上问题。本文致力于解决以上的问题。当然，若我发现某些地方已经有人做出了精确、精简又通俗易懂、我等只能在一旁拍案叫绝的解释时，就像李白说的 "眼前有景道不得，崔颢题诗在上头"，我便只好把地址贴在 "参考文档" 中，以飨诸君。

另外需要注明的是，本文仅针对 go modules 的入门指引。本篇或者本篇内引用的其他作者的文章，都是在基础层面告诉你如何使用 go modules，如何像使用 vendor 一样导入一个放在公共仓库（例如：github）中的包，不涉及私有仓库的讨论。如果你恰好有关于私有包导入方面的疑惑，也许下一章节《go modules 由浅入深非官方手册·下：go modules 与私有包》会给你一点启发。

### 包与 Golang 包

我们不需要事事亲力亲为。有很多东西，尤其是别人开源出来的代码，我们能直接用就直接用了，一个原因是节省了开发成本，另一个原因是自己写的未必就比人家做出来的强。

你用过 python 写过爬虫吗？里面常用到一个 requests 模块，这个模块不是标准库中的，你需要使用 pip install requests 手动安装，还有小游戏模块 pygame 也是如此。requests 和 pygame 都是模块名字，通过指定模块名，pip 就可以去远方获取相关代码片段了。

或者你使用过 ruby 吗？前些日子我尝试用 ruby on rails 搭建网站时刚接触过它。ruby 自带 gem 包管理工具，通过 gem install rails 即可安装 rails 框架，使用的方式与 python 中的 pip 类似。

这些不同语言的包管理器，我的看法是，没有什么大的区别，都是通过一个工具将散落在网络各个角落上的第三方包拽到本地，供自己开发使用。

Golang、Java 与 python、ruby 导入包的格式略有不同。也许是同为编译型 + 静态类型语言的原因（那种刻在骨子里的严谨）。Java 为了保证包命名的唯一性，要求包名前需加上唯一的前缀，由于互联网上的域名是不会重复的，所以包名就变成了这样：org.apache.logging.log4j。Golang 的第三方包中很大部分来自于 github 上个人或者团队的贡献，当然你肯定也会经常看到 golang.org/x/ 开头的包，这些包之所以用域名开头的原因与 Java 类似，都是要确保地址的唯一性。比如，Golang 标准库中有 net 包，但很多时候我们不直接 import "net",而是 import "golang.org/x/net",同样是 net 包，但导入的代码是不同的。这是与 ruby/python/apt 这些包管理工具不同的地方。

### Golang 包管理器演进的三个阶段 

> 见参考文档 [1]

> Golang 有哪些包管理工具呢？见参考文档 [2]

go modules 是个第三方包的管理工具, 它替代了 vendor, 不再把三方包放入项目文件中, 而仅仅在项目中保存一份 "配置文件" 即 go.mod 文件。个人下载项目后, 可以通过配置文件简单、快捷的下载相关依赖至本地。

### 使用 go modules 前的相关配置

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

#### 配置 IDE 使其支持 go modules

<p>
    <img src="/images/go-modules-settings.jpg" width="36%">
</p>

配置 GOPROXY 是为了在获取一些不方便得到的包时使用代理( 例如golang.org/x/... 模块 ),推荐的 GOPROXY 有:

- [推荐]七牛云: https://goproxy.cn/
- 阿里云: https://mirrors.aliyun.com/goproxy/ 
- goproxy.io:https://goproxy.io/

注意：当你的项目为 GOPATH + vendor 模式时，有时你发现始终无法导入某个位于本地的模块，这时就要看看是否开启了 go modules。因为go modules 模式下导入包的机制与 vendor 是不同的。

### 新项目·使用 go modules 之解决方案

> 官方英文文档请查阅参考文档 [3]

> 中文文档请查阅参考文档 [4]

> 你需要了解 go 的相关命令，在命令行中查看：
> 
> 1. go help（显示所有的 go 命令以及相应命令功能）
>
> 2. go mod help（显示 go mod 支持的所有命令及对应的功能）

1. 在项目根目录下执行 go mod init {module_name} 

   例如 go mod init github.com/haiyung/test；该命令会生成 go.mod 文件，并把当前项目的包交给 go modules 管理。

2. 此时，假如你在实现某个功能时需要导入某个外部包，例如该包为：github.com/ungerik/go-dry

   你需要将该包信息加入 go.mod 中：go mod edit -require=github.com/ungerik/go-dry@654ae31
   
   - 关于 go mod edit 的详细用法请参照：go mod help edit
   - 使用 go mod edit 将某包加入至 go modules 管理中时，需要遵循 "语义化版本"，这个版本可以是 github 中的 release tag（如 v3.10.1），也可以是项目的 commit number（如案例中的 "654ae31"），但是不写不行。

3. 将需要的外部包加入到 go modules 中后，你就可以使用该包了，成品如下 ...

   项目结构：
   ```
   gomod
        - go.mod
        - main.go
   ```
   
   go.mod 信息：
   ```
   module github.com/haiyung/gomod
   go 1.13
   require github.com/ungerik/go-dry 654ae31
   ```
   
   main.go 代码：
   ```
   package main
   import (
           "fmt"
           "github.com/ungerik/go-dry"
   )
   func main() {
           testSlice := []string{"Java",  "Golang", "Python"}
           if dry.StringInSlice("Golang",  testSlice) {
                   fmt.Println("string exists in slice")
           } else {
                   fmt.Println("string not exists in slice")
           }
   }
   ```

4. 确认 GOPROXY 是否绑定 https://goproxy.cn/ 

   在命令行执行 echo $GOPROXY，若返回空，go modules 管理下的该项目包的下载将默认走 https://proxy.golang.org 代理，由于 GFW 的缘故，这个代理是不通的，这会导致下一步下载包的过程失败，失败信息如下：
   
   ```
   go get github.com/astaxie/beego
   报错信息： 
   go get github.com/astaxie/beego: module github.com/astaxie/beego: Get https://proxy.golang.org/github.com/astaxie/beego/@v/list: dial tcp 172.217.24.17:443: i/o timeout
   ```
   
   你需要配置 GOPROXY： export GOPROXY=https://goproxy.cn/
   
   配置完成后请验证： echo $GOPROXY

5. 现在仅仅有了 go.mod 配置信息，并配置了国内的代理，接下来我们通过配置文件 go.mod 将需要的包下载至本地。

   ```
   go mod download
   // 这个命令负责将 go.mod 中指明的包下载至 GOPATH/pkg/mod 中，若你环境中的 GOPATH 为空，则会创建默认路径 - 家目录下的 go 文件夹中。
   ```

6. 现在你可以测试一下了，执行 go run main.go 看代码能不能正常跑起来。

   其实，当你完善了 go.mod 文件，并不需要第 5 步的手动下载。只要在 go modules 包管理模式下，不管你执行 go run 还是 go build/go install，它都会先后执行三个步骤：
   
   - 扫描项目文件，查看有无遗漏的第三方包，若有，则把该包最新版本信息更新至 go.mod 中；
   - 执行 go mod download
   - 执行对应的 go run/go build/go install 命令

7. go.mod 和 go.sum 文件的作用

   go.mod 文件记录了所需要的三方包地址、版本,主要用于支持可重现构建。
   
   go.sum 文件主要记录了所有在构建过程中访问到的模块的 checksums，用于保证我们的代码在传输过程中没有被纂改。

8. go mod 其他命令
   
   - go mod tidy 根据现有项目的导入路径自动更新依赖包管理, 下载相关依赖至本地, 并清除无用的依赖
   - go mod edit -droprequire=github.com/ungerik/go-dry 操作 go.mod 文件，删除指定的依赖
   - go clean -modcache 删除本地存储的所有 mod

### 老项目·包管理器迁移至 go modules 之解决方案

因为是老项目，所以该项目很可能已经存在若干个第三包依赖了。此处我们仍不探究私有包的引用，比如贵司内部可能有自己的工具包，该工具包放在了自己私有仓库中，这样的包我们暂时不做讨论。现在我们假设你的老项目仅用到了公共仓库中的三方包。

1. 在项目根目录下执行 go mod init {module_name}，初始化 go modules，生成 go.mod 文件。

   假如你的项目正在使用 glide、dep 之类的工具，初始化操作会自动接管之前的包管理器，把之前包管理器中存放的相关包信息复制到 go.mod 文件中。

2. 如上一小节《新项目·使用 go modules 之解决方案》中第 4 点一样：确认 GOPROXY 是否绑定 https://goproxy.cn/ 

3. 如果 go mod 此时已经接管了之前使用的包管理工具，那么 go.mod 文件中想必或多或少已经导入了些许三方包信息；如果之前没有任何包管理器，那么 go.mod 文件将是空的。

   接下来，你需要扫描你的项目，把所有依赖包信息导入至 go.mod 文件，使用命令 go mod tidy 即可一键完成。

4. 尝试编译一下吧。

### 参考文档
1. Go 包管理解决之道（发布于 2018 年） https://windmt.com/2018/11/08/first-look-go-modules/

   Go 包管理的前世今生（发布于 2017 年） https://www.infoq.cn/article/history-go-package-management

2. 包管理工具官方汇总 https://github.com/golang/go/wiki/PackageManagementTools

3. Go Modules 官方入门教程[英文]
   
   Modules（持续更新中） https://github.com/golang/go/wiki/Modules
   
   The Go Blog - Using Go Modules https://blog.golang.org/using-go-modules
   
   The Go Blog - Migrating To Go Modules https://blog.golang.org/migrating-to-go-modules
   
   The Go Blog - Publishing Go Modules https://blog.golang.org/publishing-go-modules

4. Go Modules 中文入门教程

   Go Modules 内部分享（发布于 2019 年 5 月） https://xuanwo.io/2019/05/27/go-modules/
   
   Go Modules 迁移实战经验（发布于 2019 年 8 月） https://xuanwo.io/2019/08/22/go-modules-migrate/
   
   初窥Go module（发布于 2018 年 7 月）https://tonybai.com/2018/07/15/hello-go-module/

5. Go 命令中文翻译 https://www.cnblogs.com/sunsky303/p/10788982.html

5. 七牛云 Go Modules 代理仓库服务: https://goproxy.cn/

6. 阿里云 Go Modules 代理仓库服务: https://mirrors.aliyun.com/goproxy/

7. GOPROXY.IO 提供的 Go Modules 代理仓库服务: https://goproxy.io/

8. 其他中文教程汇总

   - https://ieevee.com/tech/2017/07/10/go-import.html
   - https://lingchao.xin/post/using-go-modules.html
   - http://blog.ipalfish.com/?p=443
   - https://www.w3xue.com/exp/article/20191/18332.html
   - https://www.cnblogs.com/dhcn/p/11321376.html
   - https://objcoding.com/2018/09/13/go-modules/
   - https://mojotv.cn/2019/04/02/go-1.2-go-mod-tutorial
   - https://www.v2ex.com/t/566723
   - https://mp.weixin.qq.com/s/QZAgSZsaQ1H6lKkhaFgxoA
   - https://blog.csdn.net/zl1zl2zl3/article/details/83181165
   - https://juejin.im/post/5c6ac37cf265da2de7134242