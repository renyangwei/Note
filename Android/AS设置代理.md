# Android Studio设置代理

> 如果使用ShadowSocks可以用这种方法

1. File -> Settings -> HTTP Proxy
2. 选择Manual proxy configuration和Socks
3. Host name:172.0.0.1
4. Port number: 1080

解释

- Manual proxy configuration翻译过来是人工设置代理的意思
- ShadowSocks是SOCKS代理方式
- 127.0.0.1的意思是用你本机做代理
- 1080是ShadowSocks默认的端口号

# SDK Manager代理

1. Host name: mirrors.neusoft.edu.cn
2. Port number: 80
3. 勾选Others下的Force HTTPS....

So easy!