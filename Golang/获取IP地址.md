# 获取IP地址

## 本机IP

```go
func GetIp() (string, error) {
	conn, err := net.Dial("udp", "google.com:80")
	if err != nil {
		Logout(err.Error())
		return "", err
	}
	defer conn.Close()
	if config.Debug {
		return strings.Join([]string{"localhost:", config.Port}, ""), nil
	}
	return strings.Split(conn.LocalAddr().String(), ":")[0] + ":" + config.Port, nil
}
```