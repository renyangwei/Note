# ls命令

1.列出当前目录和文件

```bash
$ls
Android   Git   Interview    Mysql     README.md   Windows   Docker    Golang    Linux     Python    Tools     assets
```

2.区分目录和文件

```bash
$ls -F
Android/   Git/       Interview/ Mysql/     README.md  Windows/    Docker/    Golang/    Linux/     Python/    Tools/     assets/
```

3.显示隐藏目录

```bash
$ls -a
.         .git      Docker    Golang    Linux     Python    Tools     assets    ..        Android   Git       Interview Mysql     README.md     Windows
```

4.递归显示

```bash
$ls -F -R
Android/   Git/       Interview/ Mysql/     README.md  Windows/    Docker/    Golang/    Linux/     Python/    Tools/     assets/

./Android:
AS设置代理.md
Android Studio Logcat过滤不需要的日志.md
Apktool编译报错文件名或扩展名太长.md
关于so文件的版本问题.md
通用函数.md
模拟器本机地址映射.md
```

5.长列表(就是`ll`)

```bash
$ls -l
drwxr-xr-x   8 renyangwei  staff   272  2 26 00:38 Android
drwxr-xr-x   3 renyangwei  staff   102  2 26 00:38 Docker
drwxr-xr-x   3 renyangwei  staff   102  2 26 00:38 Git
drwxr-xr-x   8 renyangwei  staff   272  2 26 00:38 Golang
drwxr-xr-x   3 renyangwei  staff   102  2 26 00:38 Interview
drwxr-xr-x   7 renyangwei  staff   238  2 26 00:46 Linux
drwxr-xr-x   3 renyangwei  staff   102  2 26 00:38 Mysql
drwxr-xr-x  10 renyangwei  staff   340  2 26 00:38 Python
-rw-r--r--   1 renyangwei  staff  2567  2 26 00:38 README.md
drwxr-xr-x   4 renyangwei  staff   136  2 26 00:38 Tools
drwxr-xr-x   3 renyangwei  staff   102  2 26 00:38 Windows
drwxr-xr-x  11 renyangwei  staff   374  2 26 00:38 assets
```

6.过滤列表输出,后面接正则表达式

```bash
$ls -l G*
Git:
total 8
-rw-r--r--  1 renyangwei  staff  3980  2 26 00:38 已有项目提交到Git远程仓库全过程.md

Golang:
total 48
-rw-r--r--  1 renyangwei  staff  1582  2 26 00:38 GolangHttp操作.md
-rw-r--r--  1 renyangwei  staff   133  2 26 00:38 Windows后台执行.md
-rw-r--r--  1 renyangwei  staff  2517  2 26 00:38 csv和gob流文件处理.md
-rw-r--r--  1 renyangwei  staff   866  2 26 00:38 postgres数据库连接.md
-rw-r--r--  1 renyangwei  staff  3142  2 26 00:38 处理XML数据.md
-rw-r--r--  1 renyangwei  staff  1726  2 26 00:38 原生服务器示例.md
```