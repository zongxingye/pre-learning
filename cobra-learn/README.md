#cobra的入门级应用
#1.本demo的使用方法：首先在终端打开本项目并进入到cobra-learn的文件夹：cd cobra-learn；之后 go mod tidy,完善项目所需的包管理；之后运行go build -o cobra-learn ,得到编译后的可执行文件； 最后在终端运行./cobra-learn 
或者运行 ./cobra-learn add 1 1,即可得到不同的结果。


#2. 从头搭建基于cobra的golang项目的cli：
步骤如下：1.mkdir demo && cd demo
	  2.go mod init demo
	  3.go get -u github.com/spf13/cobra/cobra
	  4.cobra init --pkg-name demo
在终端中输入如下命令之后则会生成最基本的项目结构。若第三条命令超市，则更换goproxy：export GOPROXY=https://goproxy.cn
之后在cmd/root.go 文件中的rootCmd的内部注释去掉，并在run函数中加入可以执行的方法，推荐加一个print测试。之后go build -o demo ,再按着#1中的方法去执行即可。
#3.添加子命令
步骤如下：1.在项目根目录终端中输入cobra add add
	  2.在cmd/add.go文件中添加intAdd方法
	  3.在addCmd中的run属性中挂载上述方法
	  4.输入go build -o demo
	  5.输入./demo add 10 20
