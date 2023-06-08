## String字符串相关方法
#### 转换
> string转int  
`i, _ := strconv.Atoi(string)`  
> int转string  
`i, _ := strconv.Itoa(int)`

#### 内容
> 是否包含指定字符  
`strings.Contains("目标字符","指定字符")`  
> 计算指定字符串的数量
`count := strings.Count(str, "abc")`
> 是否指定字符末尾  
`strings.HasSuffix("目标字符","指定字符")`  
> 删除指定字符末尾(循环操作)
`strings.TrimRight("目标字符","指定字符")`  
> 获取第一个双引号的位置
`start := strings.Index(s, "\"")`  
> 获取第二个双引号的位置
`end := strings.Index(s[start+1:], "\"")`  
> 获取双引号中间的字符串
`substr := targetString[start+1 : start+1+end]`  
> 去掉两侧的空白字符
`substr = strings.Trim(substr, " \t\r\n")`  
> 按字符分割
`lines := strings.Split(string(data), "\n")`  
>去除字符串两端的空格
`strings.TrimSpace(" abc d ")`

#### 判断
> 区分大小写  
`StringA == StringB`  
> 不区分大小写  
`strings.EqualFold(StringA, StringB)`  

#### string转type
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
