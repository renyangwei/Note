# 操作Redis

```go
package main

import (
	"fmt"
	"github.com/garyburd/redigo/redis"
)

func main() {
	fmt.Println("hello")
	// 连接
	conn, err := redis.Dial("tcp", "127.0.0.1:6379")
	if err != nil {
		fmt.Println(err)
		return
	}
	defer conn.Close()

	// 设置字符串
	_, err = conn.Do("Set", "name", "renyangwei")
	if err != nil {
		fmt.Println(err)
		return
	}

	// 获取, 将结果转换成字符串
	result, err := redis.String(conn.Do("Get", "name"))
	if err != nil {
		fmt.Println(err)
		return
	}
	fmt.Println("result=", result)

	// 其他类似，以后再写
}
```

还可以写连接池。

当然也有其他Redis库可以使用。

