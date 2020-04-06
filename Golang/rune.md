# rune

byte 保存ASCII码字符

rune 用来保存UNICODE字符

举例：

```go
var fx = "真"
println(fx)
fxb := []byte(fx)
println(string(fxb[0]))
fxr := []rune(fx)
println(string(fxr[0]))
```

输出：

```
真
ç
真
```

这里有疑问，使用其他接口返回的 `byte[]` 类型里岂不是只能包含ASCII字符