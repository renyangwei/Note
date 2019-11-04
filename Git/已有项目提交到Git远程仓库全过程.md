> 写代码最常遇到的情况是本地已经创建好了一个项目，如何提交到远程仓库，接下来就请跟着我左手右手一个慢动作。感谢[廖雪峰的Git教程
](https://www.liaoxuefeng.com/wiki/0013739516305929606dd18361248578c67b8067c8c017b000)

# 一、安装
## 1. 在Ubuntu上安装
```
sudo apt-get install git
```
## 2. 在Mac OS X上安装
- (推荐)直接从AppStore安装Xcode，运行Xcode，选择菜单“Xcode”->“Preferences”，在弹出窗口中找到“Downloads”，选择“Command Line Tools”，点“Install”就可以完成安装了
- 安装homebrew，然后通过homebrew安装Git，具体方法请参考homebrew的文档：[http://brew.sh/](http://brew.sh/)
## 3. 在Windows上安装Git
可以从Git官网直接[下载安装程序](https://git-scm.com/downloads)

## 4. 全局配置
安装完成后，还需要最后一步设置，在命令行输入：
```
$ git config --global user.name "Name"
$ git config --global user.email "email@example.com"
```
表示你这台机器上所有的Git仓库都会使用这个配置
> 如果安装了Cmder这种Windows命令行神器，自带Git，可以省略安装的步骤

# 二、本地提交
## 1.创建本地仓库
在项目的根目录输入
```
$ git init
```
## 2.添加文件和提交
```
//添加文件
git add 1.txt
git add 2.txt 3.txt
//添加该目录下所有文件
git add .
//提交
git commit -m <message>
```
> 其他操作比如版本回退、撤销和删除操作本文省略，可参考本文开头的教程

## 3.添加并上传远程库
1. 在远程仓库中创建一个仓库（省略操作步骤），注意：`readme.md`文件最好先别选
2. 添加远程仓库
```
$ git remote add <remote> <gitRepository.git>
```
`<remote>`：远程仓库名称，自己命名，git默认的名字是`origin`
`<gitRepository.git>`：远程仓库地址，.git结尾
3. 上传到远程仓库
```
git push -u <remote>  <master>
```
`<remote>`：上一步自己定义的远程仓库名称
`<master>`：当前分支，新建本地仓库时默认为`master`
`-u`：Git不但会把本地的master分支内容推送的远程新的master分支，还会把本地的master分支和远程的master分支关联起来，在以后的推送或者拉取时就可以简化命令
最后输入远程仓库的账号名和密码就可以提交了
## 4.补充
1. 不想每次输入账号和密码怎么办？我们来配置SSH 密钥
SSH 密钥默认储存在账户的主目录下的` ~/.ssh` 目录,Windows则在`C:\Users\Administrator\.ssh`目录
首先先确认一下是否已经有一对密钥，`<something>`和`<something>.pub`，有 `.pub` 后缀的文件就是公钥，另一个文件则是密钥，如果没有就先新建。
在`.ssh`目录打开gitbash，输入
```
$ ssh-keygen
```
连续回车，直到创建完成
复制 `.pub` 文件的内容配置到远程仓库的`设置-SSH公钥`。公钥的样子大致如下：
```
$ cat ~/.ssh/id_rsa.pub
ssh-rsa AAAAB3NzaC1yc2EAAAABIwAAAQEAklOUpkDHrfHY17SbrmTIpNLTGK9Tjom/BWDSU
GPl+nafzlHDTYW7hdI4yZ5ew18JH4JW9jbhUFrviQzM7xlELEVf4h9lFX5QVkbPppSwg0cda3
Pbv7kOdJ/MTyBlWXFCR+HAo3FXRitBqxiX1nKhXpHAZsMciLq8V6RjsNAQwdsdMFvSlVK/7XA
t3FaoJoAsncM1Q9x5+3V0Ww68/eIFmb1zuUFljQJKprrX88XypNDvjYNby6vw/Pb0rwert/En
mZ+AW4OZPnTPI89ZPmVMLuayrD2cE86Z/il8b+gw3r3+1nKatmIkjn2so1d01QraTlMqVSsbx
NrRFi9wrf+M7Q== schacon@agadorlaptop.local
```

然后将远程仓库地址由 https 改为 ssh。

2. 首次提交失败，提示`Push rejected: Push to origin/master was rejected`
先和远程仓库合并
```
git pull <remote> <master>
```
3. 合并文件的时候提示`fatal: refusing to merge unrelated histories`
因为他们是两个不同的项目，要把两个不同的项目合并，需要添加选项`--allow-unrelated-histories`，所以要输入
```
git pull --allow-unrelated-histories <origin> <master>
```
合并后再上传到远程仓库

4. 还有一种保存账号密码的方法,执行
```
git config --global credential.helper store
````
以后再也不用输入密码了，多么方便。