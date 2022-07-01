## String字符串相关方法
#### 类型转换
> string转int  
`strconv.Atoi(string)`  
> int转string  
`strconv.Itoa(int)`

#### 字符串内容
> 是否包含指定字符  
`strings.Contains("目标字符","指定字符")`  
> 是否指定字符末尾  
`strings.HasSuffix("目标字符","指定字符")`
> 删除指定字符末尾(循环操作)
`strings.TrimRight("目标字符","指定字符")`

#### 判断是否相等
> 区分大小写  
`StringA == StringB`  
> 不区分大小写  
`strings.EqualFold(StringA, StringB)`  

#### string转json
⚠️必须要先知道json里面的类型，然后构建对应的结构体,string转json必须有对应的结构体。
```go
type jsonData struct {
	Meta meta   `json":meta"`
	Data []data `json":data"`
}
type meta struct {
	Code    int    `json":code"`
	Message string `json":message"`
}

type data struct {
	Id          string `json":id"`
	Name        string `json":name"`
	Remote_addr string `json":remote_addr"`
	Created_at  string `json":created_at"`
}
var repJson jsonData
err := json.Unmarshal([]byte(responseData), &repJson)
print(repJson.Data[0].Id)
```
