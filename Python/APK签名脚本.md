# APK签名脚本

```python
#!E:\Anaconda3\python
# -*- coding: UTF-8 -*-

"""
APK签名脚本

输入：
apk文件
输出：
签名后的文件，覆盖原文件

注意：
需要在文件当前目录执行脚本
"""


import os
import argparse

def get_parser():
    """
    获取参数
    """
    parser = argparse.ArgumentParser(description='APK签名脚本')
    parser.add_argument('apkfile', metavar='APK_FILE', type=str, nargs=1, help='apk文件')
    return parser


def execute(cmd):
    """
    执行命令
    :param cmd: 命令
    """
    print('cmd=', cmd)
    f = os.popen(cmd, 'r')
    d = f.read()
    print(d)
    print(f.close())


def wrap_sign_cmd(apkfile):
    """
    封装签名命令
    :return: 命令
    """
    return 'jarsigner -keystore F:\MyBin\dyb_new.keystore -storepass dyb@123 -digestalg SHA1 -sigalg SHA1withRSA {} dyb.keystore'.format(apkfile)


if __name__ == '__main__':
    parser = get_parser()
    arges = vars(parser.parse_args())
    apkfile = arges['apkfile'][0]
    print('apkfile={}'.format(apkfile))
    _, ext = os.path.splitext(apkfile)
    if not ext == '.apk':
        print('请输入apk文件')
        exit(1)
    sign_cmd = wrap_sign_cmd(apkfile)
    execute(sign_cmd)

```

