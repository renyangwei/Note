# Markdonw转HTML

## 安装Markdown

    pip install markdown

## 语法高亮

1.安装 Pygments

    pip install Pygments

2.执行下面的命令，生成一个默认的语法高亮css文件，更多可以参考Pygments项目网站

    pygmentize -S default -f html > default.css

3.下载Github风格的样式表，[下载地址](https://gist.github.com/andyferra/2554919)

## 脚本

```python
# -*- coding: utf-8 

import markdown
import os
import sys
reload(sys)
sys.setdefaultencoding('utf8')


def format_markdown_to_html(md_file,html_file):
    '''
    markdown转换成HTML
    '''
    # 读取 markdown 文本
    input_file = codecs.open(md_file, mode="r", encoding="utf-8")
    text = input_file.read()
    # 转为 html 文本
    html = md2html(text)
    # 保存为文件
    output_file = codecs.open(html_file, mode="w", encoding="utf-8")
    output_file.write(html)
    

def md2html(mdstr):
    exts = ['markdown.extensions.extra', 'markdown.extensions.codehilite','markdown.extensions.tables','markdown.extensions.toc']
    html = '''
    <html lang="zh-cn">
    <head>
    <meta content="text/html; charset=utf-8" http-equiv="content-type" />
    <link href="default.css" rel="stylesheet">
    <link href="github.css" rel="stylesheet">
    </head>
    <body>
    %s
    </body>
    </html>
    '''
    ret = markdown.markdown(mdstr,extensions=exts)
    return html % ret


if __name__ == "__main__":
    format_markdown_to_html('test.md', 'test.html')

```

[参考](https://segmentfault.com/a/1190000008993413) 