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