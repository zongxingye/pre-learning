#go modules学习心得

go modules 可以说让go开发变得更加无脑轻松，其基本上淘汰了GOPATH，实现了类语言级的包管理工具。 有了go mod，我们不需要再在gopath下进行开发。
#总的来说，go modules的核心主要有三个部分：modules，packages和version，每一个核心部分内部以及底层都有着一定复杂的算法和实现方式。此文暂时不做底层的介绍，不过最近看了个帖子觉得受益非浅，链接：https://duyanghao.github.io/golang-module/

# go modules的主要命令
go mod init (初始化module，后面可以加module的name)
go mod tidy(增加所需要的包并移除无用的包)
go mod download(下载模块到本地缓存)
go mod graph(打印各模块的依赖图)

以上是常用的命令，但是这里要提一下的是在go.mod 文件中的几个命令
replace 替换引用制定的包，比如有的时候我们对依赖包的版本有一定的需求
require 所需要的依赖包，如果不是直接引用 用// indirect标注



