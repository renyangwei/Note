# git-snv使用

用Git的方式管理SVN。这是git自带的命令，所以我们只要安装Git就能完成SVN项目的管理。

## 从svn克隆

    git svn clone <svn仓库路径> [本地文件夹名] [其他参数] 相当于git clone

    git svn clone -r<开始版本号>:<结束版本号> <svn项目地址> [其他参数]

举例：

    git svn clone -r HEAD http://172.18.2.3:8090

## 从svn同步

    git svn rebase

## 提交到svn

    git svn dcommit