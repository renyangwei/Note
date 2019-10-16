# curl 命令

curl命令 是一个利用URL规则在命令行下工作的文件传输工具。

## 文件下载

```bash
curl http://example.com/test.iso -o filename.iso --progress
######################################## 100.0%
```

- -o : 输出到文件，默认输出到屏幕
- --progress : 显示进度条
- --silent : 静默模式（感觉还是有进度条比较好）

如果要批量下载的话可以使用wget，[windows版本下载地址](https://eternallybored.org/misc/wget/)

```bash
wget -i filelist.txt
# filelist保存下载地址
cat filelist.txt
url1
url2
url3
url4
```

## get请求

```bash
curl "http://www.wangchujiang.com"    # 如果这里的URL指向的是一个文件或者一幅图都可以直接下载到本地
curl -i "http://www.wangchujiang.com" # 显示全部信息
curl -l "http://www.wangchujiang.com" # 只显示头部信息
curl -v "http://www.wangchujiang.com" # 显示get请求全过程解析
```

## post请求

```bash
$ curl -d "param1=value1&param2=value2" "http://www.wangchujiang.com/login"

curl -d'login=emma&password=123' -X POST https://wangchujiang.com/login
# 或者
$ curl -d 'login=emma' -d 'password=123' -X POST  https://wangchujiang.com/login
```

`--data-urlencode` 参数等同于 -d，发送 POST 请求的数据体，区别在于会自动将发送的数据进行 URL 编码。

```bash
curl --data-urlencode 'comment=hello world' https://wangchujiang.com/login
# 上面代码中，发送的数据hello world之间有一个空格，需要进行 URL 编码。
读取本地文本文件的数据，向服务器发送

curl -d '@data.txt' https://wangchujiang.com/upload
# 读取data.txt文件的内容，作为数据体向服务器发送。
```

### json格式的post请求

```bash
curl -l -H "Content-type: application/json" -X POST -d '{"phone":"13521389587","password":"test"}' http://wangchujiang.com/apis/users.json
```

### 获取本机外网ip

    curl ipecho.net/plain