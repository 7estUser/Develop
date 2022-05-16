## Resty
#### 优点
请求HTTPS等协议的时候，不用自己写跳过ssl证书认证，Resty可以直接连。
#### 安装库
`go get -u github.com/go-resty/resty/v2`
#### demo
```go
- //创建client对象
client := resty.New()
- //设置超时时间
client.SetTimeout(15*time.Second)
- //.R()创建请求对象，设置header、body等，发送post请求
resp,err := client.R().SetHeader("Content-Type","application/json").SetBody('{"id":1}').Post("www.t.com")
```
#### 请求对象`.R()`属性
```go
SetQyeryString("name=d&age=18")
SetQyeryParams(map[string]string("name":"d","age":"18",))
// 传入map[string]string，resty会自动帮我们拼接
SetPathParams(map[string]string{"user":"test",}).Get("/v1/user/{user}/info")
//传入map[string]string参数，然后后面的 URL 路径中就可以使用这个map中的键了,⚠️路径中的键需要用{}包起来。
SetContentLength(true)
//携带Content-Length首部，resty自动计算
SetAuthToken("xixixi")
SetResult(&result)
//SetReault()将请求结果body封装到指定对象里，var result []*Repository,Repository是自定义的type
```
#### 响应对象resp属性
```go
StatusCode()：	状态码
Status()：		状态码和状态信息
Cookies()：		服务器通过Set-Cookie首部设置的 cookie 信息
Time()：			从发送请求到收到响应的时间
ReceivedAt()：	接收到响应的时刻 
Proto()：		协议
Size()：			响应大小
Header()：		响应首部信息
```
#### 辅助功能
在请求对象.R()上调用`EnableTrace()`方法启用 `trace`，请求完成之后，调用请求响应对象的`TraceInfo()`方法获取信息
```go
resp,err := client.R().EnableTrace().Get("www.t.com")
ti := resp.Request.TraceInfo()
fmt.println(ti.DNSLookup)
```
可以获取以下信息：
- DNSLookup：DNS 查询时间，如果提供的是一个域名而非 IP，就需要向 DNS 系统查询对应 IP 才能进行后续操作；
- ConnTime：获取一个连接的耗时，可能从连接池获取，也可能新建；
- TCPConnTime：TCP 连接耗时，从 DNS 查询结束到 TCP 连接建立；
- TLSHandshake：TLS 握手耗时；
- ServerTime：服务器处理耗时，计算从连接建立到客户端收到第一个字节的时间间隔；
- ResponseTime：响应耗时，从接收到第一个响应字节，到接收到完整响应之间的时间间隔；
- TotalTime：整个流程的耗时；
- IsConnReused：TCP 连接是否复用了；
- IsConnWasIdle：连接是否是从空闲的连接池获取的；
- ConnIdleTime：连接空闲时间；
- RequestAttempt：请求执行流程中的请求次数，包括重试次数；
- RemoteAddr：远程的服务地址，IP:PORT格式。