# 等待goroutine完成

如果主线程已经结束，但是goroutine里的工作还没有完成，会中断线程里的工作。这时候需要等待子线程里的任务完成才退出主线程。

我们可以使用 `sycn.WaitGroup`

举例：

```go
package main

import (
	"fmt"
	"sync"
	"time"
)

// 定义全局变量
var wg sync.WaitGroup

func f1()  {
	defer wg.Done()
	for i := 0; i < 5; i++ {
		time.Sleep(time.Second)
		fmt.Println("i=", i)
	}
}

func main() {
	fmt.Println("start...")
	// 每开启一个线程就加一
	wg.Add(1)
	go f1()
	time.Sleep(time.Second)
	// 等待结束，阻塞
	wg.Wait()
	fmt.Println("end...")
}
```

打印结果：

```bash
start...
i= 0
i= 1
i= 2
i= 3
i= 4
end...
```
