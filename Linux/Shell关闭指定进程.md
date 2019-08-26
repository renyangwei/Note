# Shell 关闭指定进程

```bash
ps -ef | grep fltxweb | grep -v grep | cut -c 9-15 | xargs kill -9
```

说明：

- `ps -ef`：查看所有进程
- `grep fltxweb`：过滤名字包含fltxweb的进程
- `grep -v grep`：列出的进程中去除含有关键字 `grep` 的进程
- `cut -c 9-15`：截取进程号PID
- `xargs kill -9`：`xargs` 命令用来把前面的输出（PID）作为 `kill -9` 的参数