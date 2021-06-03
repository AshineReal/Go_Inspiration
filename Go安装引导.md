 [TOC]

# 安装引导



打开[go官网下载页](https://golang.org/dl/)

根据下载页提示官方提供了两大类下载安装流程：

1. 官方编译好的二进制发布包（需要选择与你当前系统对应的包）

2. 用户下载go源码自行编译（源码编译的方式可方便调试源码）



## 使用官方预编译的二进制发布包安装

如你选择使用编译好的二进制发布包，官方提供了两种安装方式：

1. 使用Installer(安装器：即用户安装引导程序，按照引导提示一步步走即可完成安装)
2. 使用Archive(归档打包：直接解压完成的文件夹就是go的安装路径)

再根据[安装引导提示](https://golang.org/doc/install) （以下是macos系统的安装引导，其它系统请参照引导页提示）

1. 根据引导页提示安装，安装路径默认是在/usr/local/go，然后你需要将/usr/local/go/bin这个路径放入你的PATH环境变量。然后重新打开命令终端使改动生效（或者使用source命令）。

2. 使用以下终端命令验证你已经成功安装go。

   ```shell
   go version
   ```

3. 验证是否命令行打印了Go的版本信息



使用官方预编译的二进制发布包的安装方式比较简单，这里不再赘述。

下面重点介绍需要对源码分析调试有需求的源码编译安装



## 使用源码编译安装



[源码编译安装的官方引导页](https://golang.org/doc/install/source)



### 介绍

Go是一个开源工程，使用BSD风格的认证。这个文档介绍了如何拉取源码，在你的机器上构建，并运行它们。

官方提供了两种Go编译器工具链。这个文档专注于gc (go compiler) Go编译器和工具。如需了解如何使用gccgo（一个更加传统的编译器使用GCC后端）来编译，[请看这里](https://golang.org/doc/install/gccgo).



### 安装Go 编译器以自举

Go工具链是使用go来编写的（1.4版本以后）。为了构建它们，你需要安装一个Go编译器。初始化构建工具的脚本需要一个"go"命令在$PATH环境变量中定义，只要你已经安装了一次go并配置了$PATH环境变量，你就准备好使用源码构建Go了。或者如你喜欢你可以设置$GOROOT_BOOTSTRAP到go安装根目录用来构建新的go工具链；$GOROOT_BOOTSTRAP/bin/go 这个路径应该成为go命令使用的路径。



有4个获取自举工具链的方式：

* 下载一个最近的Go正式发布版二进制文件.
* 使用一个安装了go的系统交叉编译出一个工具链.
* 使用gccgo编译器.
* 从Go1.4 编译一个工具链，最后一个带有c编写的编译器.



这里我推荐使用第一种方式，直接安装一个go发布版，然后将这个go作为源码编译的编译器工具链



### 拉取源码仓库

使用终端cd到你想要安装go的文件夹路径，并且保证goroot路径不存在。然后clone仓库并拉取最新发布tag（目前是go1.16.4）:

```shell
git clone https://go.googlesource.com/go goroot
cd goroot
git checkout go1.16.4
```



### 安装Go

 运行以下命令构建Go发布版

```shell
cd src
./all.bash
```



如果正常的话，终端会打印出像如下的描述信息：

```shell
ALL TESTS PASSED

---
Installed Go for linux/amd64 in /home/you/go.
Installed commands in /home/you/go/bin.
*** You need to add /home/you/go/bin to your $PATH. ***
```



最后几行反映了操作系统，架构，安装根目录等详细信息。

使用all.bash脚本运行了一些重要的测试，需要比仅仅构建Go花费更多时间，如果你不需要运行测试模块就使用make.bash代替all.bash。



### 测试你的安装

通过构建一个简易的程序来检查Go已经被正确安装。

创建一个文件名为hello.go 然后填入以下代码段:

```go
package main

import "fmt"

func main() {
	fmt.Printf("hello, world\n")
}
```



然后使用go工具运行它：

```shell
go run hello.go
hello,world
```

如果看到"hello,world"这几个字代表Go被正确安装了。



### 设置你的工作环境

[如何编写go代码](https://golang.org/doc/code.html)文档提供了一些使用go工具的精辟设置指导



### 保持版本更新

最新的发布版版会在[这里](https://groups.google.com/group/golang-announce).每个发布会提到最新的发布版本tag 比如，go1.16.4

使用如下命令更新版本

```shell
cd go/src
git fetch
git checkout go1.16.4
```









