# 处理XML数据

```go
package main

import (
	"encoding/xml"
	"fmt"
	"io"
	"io/ioutil"
	"os"
)

/********** 解析XML ************/
/**
有两种方法:
1.使用xml.Unmarshal解析到结构，适合体积较小的XML数据
2.使用Decoder解码器解析到结构
*/
type Post struct {
	XMLName  xml.Name  `xml:"post"`    //可以看做根节点
	Id       string    `xml:"id,attr"` //根节点的id属性
	Content  string    `xml:"content"` //根节点的子节点的值
	Author   Author    `xml:"author"`
	Xml      string    `xml:",innerxml"`        //保存该节点里的原始xml数据保存下来
	Comments []Comment `xml:"comments>comment"` //要映射到comments的子元素
}

type Author struct {
	Id   string `xml:"id,attr"`
	Name string `xml:",chardata"` //这也是获得子节点的值
}

type Comment struct {
	Id      string `xml:"id,attr"`
	Content string `xml:"content"`
	Author  Author `xml:"author"`
}

/**
使用xml.Unmarshal解析到结构
*/
func parseXmlUnmarshal() {
	xmlFile, err := os.Open("post.xml")
	if err != nil {
		fmt.Println(err.Error())
		return
	}
	defer xmlFile.Close()
	xmlData, err := ioutil.ReadAll(xmlFile)
	if err != nil {
		fmt.Println(err.Error())
		return
	}
	var post Post
	err = xml.Unmarshal(xmlData, &post) //注意取地址
	if err != nil {
		fmt.Println(err.Error())
		return
	}
	fmt.Println(post)
}

/**
使用解码器解码至结构
*/
func parseXmlDecoder() {
	xmlFile, err := os.Open("post.xml")
	if err != nil {
		fmt.Println(err.Error())
		return
	}
	defer xmlFile.Close()
	decoder := xml.NewDecoder(xmlFile)
	//每进行一次迭代就从解码器里获取一个token
	for {
		t, err := decoder.Token()
		if err == io.EOF {
			break
		}
		if err != nil {
			fmt.Println(err.Error())
			return
		}
		//判断token的类型
		switch se := t.(type) {
		case xml.StartElement:
			if se.Name.Local == "comment" {
				var comment Comment
				decoder.DecodeElement(&comment, &se)
				fmt.Println(comment)
			}
		}
	}
}

/**
通过Marshal创建XML文件
*/
func createXmlByMarshal() {
	post := Post{
		Id:      "1",
		Content: "Hello World",
		Author: Author{
			Id:   "2",
			Name: "Ren",
		},
	}
	//使用MarshalIndent可以更好看
	//prefix：每行的前缀
	//indent：每行缩进
	output, err := xml.MarshalIndent(&post, "", "\t")
	if err != nil {
		fmt.Println(err.Error())
		return
	}
	//加上XML.Header
	if err = ioutil.WriteFile("createByMarshal.xml", []byte(xml.Header+string(output)), 0644); err != nil {
		fmt.Println(err.Error())
		return
	}
}

/**
通过Decoder创建XML
*/
func createXmlByEncoder() {
	post := Post{
		Id:      "1",
		Content: "Hello World",
		Author: Author{
			Id:   "2",
			Name: "Ren",
		},
	}
	xmlFile, err := os.Create("createByEncoder.xml")
	if err != nil {
		fmt.Println(err.Error())
		return
	}
	encoder := xml.NewEncoder(xmlFile)
	encoder.Indent("", "\t")
	err = encoder.Encode(&post)
	if err != nil {
		fmt.Println(err.Error())
		return
	}
}

func main() {
	parseXmlUnmarshal()
	fmt.Println("---------------")
	parseXmlDecoder()
	fmt.Println("---------------")
	createXmlByMarshal()
	fmt.Println("---------------")
	createXmlByEncoder()
}
```