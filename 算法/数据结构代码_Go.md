# 数据结构代码

## 1.稀疏数组

当一个数组中大部分元素为0或者同为一个值时，可以用稀疏数组保存。即只记录不同的值。

第一个值一般记录原始大小。

```go
package main

import (
	"encoding/json"
	"fmt"
	"io/ioutil"
)

const (
	BLACK_CHESS = 1 // 黑子
	WIHTE_CHESS = 2 // 白子
	FILE_NAME = "data.json"
)

type ValNode struct {
	Row int `json:"row"`
	Col int `json:"col"`
	Val int `json:"val"`
}


// 稀疏数组
func main() {
	var chessMap [10][10]int
	chessMap[1][5] = BLACK_CHESS
	chessMap[2][3] = WIHTE_CHESS
	chessMap[4][6] = BLACK_CHESS
	chessMap[7][9] = WIHTE_CHESS

	for _, v := range chessMap {
		for _, v2 := range v {
			fmt.Printf("%d\t", v2)
		}
		fmt.Println()
	}

	var sparseArr []ValNode
	// 第一个结构体记录原始数组的大小
	sparseArr = append(sparseArr, ValNode{Row: len(chessMap), Col: len(chessMap[0]), Val: 0})
	for r, v := range chessMap {
		for c, v2 := range v {
			if v2 != 0 {
				valNode := ValNode{Row: r, Col: c, Val: v2}
				sparseArr = append(sparseArr, valNode)
			}
		}
	}
	// 打印
	for _, node := range sparseArr {
		fmt.Println(node)
	}
	// 存到文件,用json格式
	j, err := json.Marshal(sparseArr)
	if err != nil {
		fmt.Println(err)
		return
	}
	err = ioutil.WriteFile(FILE_NAME, j, 0666)
	if err != nil {
		fmt.Println(err)
		return
	}
	// 恢复
	b, err := ioutil.ReadFile(FILE_NAME)
	if err != nil {
		fmt.Println(err)
		return
	}
	var sparseSlice []ValNode
	err = json.Unmarshal(b, &sparseSlice)
	if err != nil {
		fmt.Println(err)
		return
	}
	fmt.Println("恢复后的棋盘")
	for _, sp := range sparseSlice {
		fmt.Println(sp)
	}

}
```

## 2.环形队列

```go
package main

import (
	"errors"
	"fmt"
)

/**
环形队列
思路：
1.创建一个数组，设置最大值
2.一个指向队首的指针front和一个指向队尾的指针real，初始化为0
3.提供三个方法：push,pop和show
4.当push的时候，real 指针往后移
5.pop的时候front指针往后移
6.当两个指针重合的时候，就空了
7.当real指针加一取模后等于头就满了

实际容量是数组容量减一
*/

type CircleQueue struct {
	MaxSize int  // 最大数量
	Array [5]int  // slice
	Head int	 // 指向队首
	Tail int	 // 指向队尾
}

// 加入队列
func (queue *CircleQueue) Push(val int) error {
	if queue.IsFull() {
		return errors.New("queue is full")
	}
	queue.Array[queue.Tail] = val
	queue.Tail = (queue.Tail + 1) % queue.MaxSize
	return nil
}

// 弹出
func (queue *CircleQueue) Pop() (val int, err error) {
	if queue.IsEmpty() {
		return 0, errors.New("queue is empty")
	}
	val = queue.Array[queue.Head]
	queue.Head = (queue.Head + 1) % queue.MaxSize
	return val, nil
}

// 显示队列
func (queue *CircleQueue) ShowQueue() {
	size := queue.Size()
	if size == 0 {
		fmt.Println("queue is empty")
		return
	}
	var tempHead = queue.Head
	for i := 0; i < size; i++ {
		fmt.Printf("arr[%d]=%d\t", tempHead, queue.Array[tempHead])
		tempHead = (tempHead + 1) % queue.MaxSize
	}
	fmt.Println()
}

// 判断队列已满
func (queue *CircleQueue)IsFull() bool {
	return (queue.Tail + 1) % queue.MaxSize == queue.Head
}

// 是否为空
func (queue *CircleQueue) IsEmpty() bool {
	return queue.Head == queue.Tail
}

// 有多少个元素
func (queue *CircleQueue) Size() int {
	return (queue.Tail - queue.Head + queue.MaxSize) % queue.MaxSize
}

func main() {
	// 队列
	circleQueue := CircleQueue{MaxSize: 5}

	circleQueue.ShowQueue()

	err := circleQueue.Push(1)
	ifError(err)

	err = circleQueue.Push(4)
	ifError(err)

	err = circleQueue.Push(6)
	ifError(err)

	err = circleQueue.Push(5)
	ifError(err)

	err = circleQueue.Push(7)
	ifError(err)

	circleQueue.ShowQueue()

	err = circleQueue.Push(7)
	ifError(err)

	v, err := circleQueue.Pop()
	ifError(err)
	fmt.Printf("pop value=%d\n", v)

	circleQueue.ShowQueue()
}

func ifError(err error) {
	if err != nil {
		fmt.Println(err)
	}
  
}
```

## 3.单链表

一般来说，为了比较好的对单链表进行增删改查，我们会给它设置一个头节点，主要作用是标识链表头，而且不存放数据。

用链表实现队列更方便，效率更高。

```go
package main

import "fmt"

// 单链表
type HeroNode struct {
	no       int
	name     string
	nickName string
	next     *HeroNode	// 指向下一个节点
}

// 直接在最后插入
func insertLast(head *HeroNode, new *HeroNode) {
	temp := head
	for {
		if temp.next == nil {  // 如果找到最后则跳出
			break
		}
		temp = temp.next  // 不断指向下一个节点
	}
	temp.next = new
}

// 排序插入，根据no的大小
func insertSort(head *HeroNode, new *HeroNode) {
	temp := head
	flag := true
	// 比较新节点和temp的下一个节点
	for {
		if temp.next == nil { // 到了链表最后
			break
		} else if new.no < temp.next.no  {
			// new 应该插入到temp的下一个
			break
		} else if new.no == temp.next.no {
			flag = false
		}
		temp = temp.next  // 不断指向下一个节点
	}
	if !flag {
		fmt.Println("对不起，节点已经存在,no=", new.no)
		return
	} else {
		// 插入节点
		new.next = temp.next
		temp.next = new
	}
}

// 删除一个节点
// no : 删除的number
func deleteNode(head *HeroNode, no int)  {
	temp := head
	finded := false
	for {
		if temp.next == nil { // 到了链表最后
			break
		} else if no == temp.next.no {
			finded = true
			break
		}
		temp = temp.next  // 不断指向下一个节点
	}
	if finded {
		temp.next = temp.next.next
	} else {
		fmt.Println("没有找到")
	}
}

func showAll(head *HeroNode) {
	temp := head
	// 先判断是不是空链表
	if temp.next == nil {
		fmt.Println("空空如也")
		return
	}
	// 遍历链表
	for {
		fmt.Printf("[%d, %s, %s]->", temp.next.no, temp.next.name, temp.next.nickName)
		temp = temp.next
		if temp.next == nil {
			break
		}
	}
	fmt.Println()
}

func main() {
	head := HeroNode{}
	node1 := HeroNode{no: 1, name: "宋江", nickName: "及时雨"}
	node2 := HeroNode{no: 2, name: "吴用", nickName: "智多星"}
	node3 := HeroNode{no: 3, name: "林冲", nickName: "豹子头"}
	node4 := HeroNode{no: 4, name: "X", nickName: "x"}
	//insertLast(&head, &node2)
	//insertLast(&head, &node3)
	//insertLast(&head, &node1)
	insertSort(&head, &node2)
	insertSort(&head, &node4)
	insertSort(&head, &node3)
	insertSort(&head, &node1)
	showAll(&head)
	deleteNode(&head, 3)
	showAll(&head)
}
```

还有 **双向链表** 和 **环形链表**，先放一放，估计也很少用到。

## 4. 栈

应用场景：

1. 子程序调用：在跳往子程序前，会将下个指令的地址保存在栈中，直到子程序执行完，再从栈中取出；
2. 处理递归调用；
3. 表达式的求值与转换；
4. 二叉树遍历；
5. 图形的深度优先搜索法。

```go
package chapter2

import (
	"errors"
	"fmt"
)

// 实现一个栈
// 出栈、入栈、遍历

type Stack struct {}

var arr [5]int		// 用数组实现栈
var pointer = -1	// 位置指针

// 出栈
func (this *Stack) Pop() (val int, err error){
	if pointer < 0 {
		return -1, errors.New("stack is empty")
	}
	val = arr[pointer]
	pointer -= 1
	return val, nil
}

// 入栈
func (this *Stack) Push(val int) {
	if pointer >= len(arr)-1 {
		fmt.Println("stack is full")
		return
	}
	pointer += 1
	arr[pointer] = val
}

// 遍历
func (this *Stack) List() {
	if pointer < 0 {
		fmt.Println("stack is empty")
		return
	}
	fmt.Println("stack list:")
	for i := pointer; i >= 0; i-- {
		fmt.Println(arr[i])
	}
}
```

表达式求值思路：

1. 用两个栈，一个保存数，一个保存操作符；
2. 如果已经入栈的操作符优先级比要入栈的低，那么先计算