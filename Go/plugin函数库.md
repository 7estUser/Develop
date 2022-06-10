## plugin的go代码编写要求
1. 包名称必须是main
2. 没哟main函数
3. 必须有可以导出（访问）的变量或者方法（也就是首字母大写）
## 编译成 .so 文件
`go build -buildmode=plugin -o=test.so test.go`
## 使用plugin插件
`p,err := plugin.Open("test.so")`
⚠️plugin(.so)插件被打开加载后(即执行了plugin.Open()方法以后),插件的init()初始化函数才开始执行。  
⚠️也就是说main函数执行前plugin的init()函数是不会执行的。插件只被初始化一次,不能被关闭。   
- 寻找插件中可用变量 plug.Lookup("")
`doc,err := p.Lookup("tester")`
  
详细介绍：https://blog.csdn.net/owenzhang24/article/details/122233877