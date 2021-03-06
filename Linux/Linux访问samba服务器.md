# Linux访问samba服务器

> 感谢 https://blog.csdn.net/ZCF1002797280/article/details/49805603 提供参考

## smbclient安装

### Ubuntu

    sudo apt-get install smbclient

### CentOs

    yum install samba-client

## 查看目录的所有共享目录

    smbclient -L [ip]

\[ip\]:samba服务器IP

## 连接共享目录

    smbclient //[ip]]/[dir]

\[ip\]:samba服务器IP

\[dir\]:samba服务器目录

成功后出现提示符smb:\>，就可以开始操作了

## smbclient 常用命令

    ?或help [command]         提供关于帮助或某个命令的帮助

    ![shell command]        执行所用的SHELL命令，或让用户进入 SHELL提示符

    cd [目录]        切换到服务器端的指定目录，如未指定，则 smbclient 返回当前本地目录

    lcd [目录]        切换到客户端指定的目录；

    dir 或ls        列出当前目录下的文件；

    exit 或quit        退出smbclient     

    get file1  file2        从服务器上下载file1，并以文件名file2存在本地机上；如果不想改名，可以把file2省略

    mget file1 file2 file3  filen        从服务器上下载多个文件；

    md或mkdir 目录        在服务器上创建目录

    rd或rmdir   目录        删除服务器上的目录

    put file1 [file2]        向服务器上传一个文件file1,传到服务器上改名为file2；

    mput file1 file2 filen  向服务器上传多个文件

## 将共享目录挂载到本地

    mount -t cifs -o username=xxx,password=xxx //[ip]/[dir] /home/xxx/xxx

\[ip\]:samba服务器IP

\[dir\]:samba服务器目录

如果不需要密码可以不填，像这样

    mount -t cifs -o username=xxx //[ip]/[dir] /home/xxx/xxx
