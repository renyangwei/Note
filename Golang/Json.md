# Json

## 序列化

两点需要注意：**字段名大写 **和 **写Json注解** 。

暂时理解为注解好了。

```go
type Dog struct {
		ID int `json:"id"`
		Name string `json:"name"`
}
d1 := Dog{ID: 1, Name: "Petter"}
pb, err := json.MarshalIndent(d1, "", "  ")
if err != nil {
		fmt.Println("marshl err=", err.Error())
		return
}
fmt.Println(string(pb))
```

## 反序列化

注意一点：`Unmarshal` 方法要传 **指针 **。

```go
var d2 Dog
	myDog := `{"id":2, "Name":"mydog"}`
	err = json.Unmarshal([]byte(myDog), &d2)
	if err != nil {
		fmt.Println(err)
		return
	}
	fmt.Println(d2)
```

