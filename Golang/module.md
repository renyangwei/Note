# Go module

暂时搞明白的就是在项目目录下新建 *go.mod*文件，输入

```
// go.mod
module {项目名}
```

前提是项目不在 GoPath 目录

然后执行 `go build`，就会自动下载依赖项，同时编辑 *go.mod*文件，然后生成一个 *go.sum*文件，都是用来保存依赖的，下载的依赖包缓存在 *$GOPATH/src/mod* 下面。

> 不过本人用的1.13版本发现依赖包缓存在 *$GOPATH/pkg/mod* 目录下。