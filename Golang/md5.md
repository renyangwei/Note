# md5

```go
func md5Sign(s string) string {
	fmt.Println("md5 string=", s)
	h := md5.New()
	h.Write([]byte(s))
	cipherStr := h.Sum(nil)
    m := hex.EncodeToString(cipherStr)
    fmt.Println("md5=", m)// 输出加密结果
	return m
}
```