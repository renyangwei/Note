# Windows编译Linux和Mac执行文件

**Mac**

```bash
SET CGO_ENABLED=0
SET GOOS=darwin
SET GOARCH=amd64
go build main.go
```

**Linux**

```bash
SET CGO_ENABLED=0
SET GOOS=linux
SET GOARCH=amd64
go build main.go
```

`GOOS`：目标平台的操作系统（darwin、freebsd、linux、windows） 

`GOARCH`：目标平台的体系架构（386、amd64、arm） 