## Goland：
Go Build配置:
- Run kind: 选Directory
- Directory： 选你的main包所在文件夹
- Output directory：选择生成文件存放位置
- Working directory：保持默认就好
- Go tool arguments：go build 的参数
![](https://github.com/user-error-404/Develop/blob/main/Go/img/Goland生成可执行文件.png)

## 命令行
```shell
CGO_ENABLED=0 GOOS=windows GOARCH=amd64 go build -o Test main.go
```
CGO_ENABLED=0：进行编译时， 则会把在目标文件中未定义的符号（外部函数）一起链接到可执行文件中。
CGO_ENABLED=1：进行编译时， 会将文件中引用libc的库（比如常用的net包），以动态链接的方式生成目标文件。
GOOS：操作系统
COARCH：平台架构
