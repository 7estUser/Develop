## 生成可执行文件(build命令)
### 命令
```shell
CGO_ENABLED=0 GOOS=windows GOARCH=amd64 go build -o Test main.go
```
- CGO_ENABLED=0：进行编译时， 则会把在目标文件中未定义的符号（外部函数）一起链接到可执行文件中。
- CGO_ENABLED=1：进行编译时， 会将文件中引用libc的库（比如常用的net包），以动态链接的方式生成目标文件。
- GOOS：操作系统	windows、linux、darwin、freebsd
- COARCH：平台架构
`go build -buildmode=plugin -o=a.so a.go`
- 将main包编译为Go插件，非main包被忽略
build命令参考：https://blog.csdn.net/puss0/article/details/113811614?utm_term=-mod%20build%20go&utm_medium=distribute.pc_aggpage_search_result.none-task-blog-2~all~sobaiduweb~default-1-113811614-null-null&spm=3001.4430
### Goland：
Go Build配置:
- Run kind: 选Directory
- Directory： 选你的main包所在文件夹
- Output directory：选择生成文件存放位置
- Working directory：保持默认就好
- Go tool arguments：go build 的参数
![](https://github.com/user-error-404/Develop/blob/main/Go/img/Goland生成可执行文件.png)

## Go环境配置  
- 查看go环境配置：go env  
	goroot和gopath不能一样，goroot是安装/bin路径，gopath是文件的存放目的地和包搜索路径。  
- 修改go环境配置: ( >=1.13 )  
	go env -w GOPATH=""
- 编译加执行  
	go run test.go
