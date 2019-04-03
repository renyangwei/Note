# vim基础

vim有两种操作模式：

- 普通模式
- 插入模式

## 普通模式

- h：左移一个字符
- j：下移动一行
- k：上移动一行
- l：右移动一个字符
- PageDown：下翻一页
- PageUp：上翻一屏
- G：移动到最后一行
- num G：移动到第num行
- gg：移动到第一行
- q：退出
- q!：不保存退出
- w filename：另存为
- wq：保存退出

## 插入模式

- x：删除当前位置的字符
- dd：删除当前行
- u：撤销上一个命令

复制命令

    /[s]

[s]：表示要查找的字符

替换第一个

    :s/old/new

替换所有

    :s/old/new/g