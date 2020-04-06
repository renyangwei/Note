# Go module

其实不难。Take it easy。

只有几个步骤：

1. 安装，去官网下载安装 （不用再设置GOPATH，安装的时候设置好了）；
2. 设置代理 （`go env -w GOPROXY=https://goproxy.cn`）；
3. 在任意目录（除了了GOPATH）下新建go文件；
4. 在终端输入命令 `go mod init {your project name}`。

如果要导入包有两种方式：

1. 使用命令 `go get`，会将包下载并放到 *$GOPATH/pkg/mod* 目录下，然后在项目里就可以引用（这种方式和Python差不多，适合自己开发）；
2. 直接在项目里引用，再执行 `go build`，会自动下载并编译工程（这种方式适合在使用别人工程的时候使用）。

如果想导入自己工程里的包怎么办，写法为：`module名 + / + 包名`

举例：

先看目录结构，一个 *mian.go* 文件和一个 *utils* 目录

```
.
├── go.mod
├── go.sum
├── main.go
└── utils
    └── utils.go
```

*go.mod*

```
module com/ren/daydayup

go 1.14
```

*main.go*

```go
package main

import (
    // 导入本地包一定要写module名
	"com/ren/daydayup/utils"
	"fmt"
)

func main()  {
	fmt.Println(utils.Add(1, 2))
}
```

*utils.go*

```go
// Package utils My Porject Utils
package utils

// Add a and b
func Add(a, b int) int {
	return a + b
}
```