# shell脚本问题记录

## 在Linux中执行.sh脚本，异常`/bin/sh^M: bad interpreter: No such file or directory`

解决方法：

1.在windows下转换

利用一些编辑器如UltraEdit或EditPlus等工具先将脚本编码转换，再放到Linux中执行。转换方式如下（UltraEdit）：*File-->Conversions-->DOS->UNIX* 即可

2.在Linux中转换

首先要确保文件有可执行权限 

    chmod a+x filename 

然后修改文件格式 

    vi filename 

利用如下命令查看文件格式 

    :set ff 或 :set fileformat

可以看到如下信息 

    fileformat=dos 或 fileformat=unix 

利用如下命令修改文件格式 

    :set ff=unix 或 :set fileformat=unix 
    :wq

最后再执行文件 

    ./filename

## 格式化时间

    DATE=`date '+%Y-%m-%d %H:%M:%S'`