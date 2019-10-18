# Golang Http操作

## Http Get

```go
func httpGet(httpUrl string) ([]byte, error) {
    resp, err := http.Get(httpUrl)
    if err != nil {
        log.Println("httpGet err:", err)
        return nil, err
    }
    defer resp.Body.Close()
    body, err := ioutil.ReadAll(resp.Body)
    if err != nil {
        log.Println("httpGet err:", err)
        return nil, err
    }
    log.Println(string(body))
    return body, nil
}
```

## Http Post

```go
func httpPost(httpUrl string, data string) ([]byte, error) {
	body := bytes.NewBuffer([]byte(data))
	log.Println("body:", body)
	log.Println("httpUrl:", httpUrl)
	resp, err := http.Post(httpUrl, "application/x-www-form-urlencoded", body)
	if err != nil {
		log.Println("post err:", err)
		return nil, err
	}
	defer resp.Body.Close()
	respBody, err := ioutil.ReadAll(resp.Body)
	if err != nil {
		log.Println("resp err:", err)
		return nil, err
	}
	return respBody, nil
}
```

## 复杂的请求

用于自定义header、cookie等参数

```go
func httpDo() {
    client := &http.Client{} 
    req, err := http.NewRequest("POST", "http://www.01happy.com/demo/accept.php", strings.NewReader("name=cjb"))
    if err != nil {
        // handle error
    }
    req.Header.Set("Content-Type", "application/x-www-form-urlencoded")
    req.Header.Set("Cookie", "name=anny")
    resp, err := client.Do(req)
    defer resp.Body.Close()
    body, err := ioutil.ReadAll(resp.Body)
    if err != nil {
        // handle error
    }
    fmt.Println(string(body))
}
```

推荐一个很好的 [Go example](https://github.com/chenjiebin/goexample)