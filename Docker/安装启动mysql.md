# 安装启动mysql

```bash
# 下载并启动
$ docker run --name mysql-test -e MYSQL_ROOT_PASSWORD=123456 -d mysql:tag
# 进入容器
$ docker exec -it mysql bash
# 登录mysql
mysql -u root -p
```

tag可选5.6或者8.0.20或者不填

其他操作参考Mysql数据库。