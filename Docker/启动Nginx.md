# 启动Nginx

    docker run --name myNginx -v /home/renyangwei/mdwiki:/usr/share/nginx/html:ro -d -p 8001:80 nginx:1.15.8-alpine

`myNginx` : 自定义名称

`/home/renyangwei/mdwiki` : 自定义目录

修改了目录下的文件后记得清理浏览器缓存。