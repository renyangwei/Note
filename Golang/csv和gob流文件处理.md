# xml和gob流文件处理

```go
package main

import (
	"bytes"
	"encoding/csv"
	"encoding/gob"
	"fmt"
	"io/ioutil"
	"os"
	"strconv"
)

type Post struct {
	Id      int
	Content string
	Author  string
}

const (
	CsvFileName = "posts.csv"
	GobFileName = "post.gob"
)

/**
 *	处理csv文件
 */
func csvFile() {
	//创建csv文件,写入数据
	csvFile, err := os.Create(CsvFileName)
	if err != nil {
		fmt.Println(err.Error())
		return
	}
	defer csvFile.Close()
	allPosts := []Post{
		{Id: 1, Content: "Hello", Author: "Ren"},
		{Id: 2, Content: "Hi", Author: "Lang"},
	}
	writer := csv.NewWriter(csvFile)
	for _, post := range allPosts {
		line := []string{strconv.Itoa(post.Id), post.Content, post.Author}
		err := writer.Write(line)
		if err != nil {
			fmt.Println(err.Error())
			return
		}
	}
	writer.Flush()

	//读取csv文件
	file, err := os.Open(CsvFileName)
	if err != nil {
		fmt.Println(err.Error())
		return
	}
	defer file.Close()

	reader := csv.NewReader(file)
	//如果该值为正数，这个值当做每条记录的字段量，当读取器从CSV文件里读取出的字段量少于这个值时会报错
	//如果为负数，少了字段也不会报错
	//如果为0，第一条记录的字段量作为FieldsPerRecord的值
	reader.FieldsPerRecord = -1
	records, err := reader.ReadAll()
	if err != nil {
		fmt.Println(err.Error())
		return
	}
	var posts []Post
	for _, item := range records {
		id, _ := strconv.ParseInt(item[0], 10, 0)
		post := Post{Id: int(id), Content: item[1], Author: item[2]}
		posts = append(posts, post)
	}
	fmt.Println(posts[0].Id)
	fmt.Println(posts[0].Content)
	fmt.Println(posts[0].Author)
}

/**
 * 使用gob包保存和读取二进制数据
 */
func gobFile() {
	post := Post{Id: 1, Content: "Hello,World", Author: "Ren"}
	store(post, GobFileName)
	var postRead Post
	load(&postRead, GobFileName)
	fmt.Println(postRead)
}

func store(data interface{}, fileName string) {
	buffer := new(bytes.Buffer)
	encoder := gob.NewEncoder(buffer)
	err := encoder.Encode(data)
	if err != nil {
		fmt.Println(err.Error())
		return
	}
	err = ioutil.WriteFile(fileName, buffer.Bytes(), 0666)
	if err != nil {
		fmt.Println(err.Error())
		return
	}
}

func load(data interface{}, fileName string) {
	raw, err := ioutil.ReadFile(fileName)
	if err != nil {
		fmt.Println(err.Error())
		return
	}
	buffer := bytes.NewBuffer(raw)
	dec := gob.NewDecoder(buffer)
	err = dec.Decode(data)
	if err != nil {
		fmt.Println(err.Error())
		return
	}
}

func main() {
	csvFile()
	gobFile()
}
```