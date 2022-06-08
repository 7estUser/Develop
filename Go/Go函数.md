## init函数(初始化函数)
- ❗️init函数校准main函数执行前执行。❗️
- 每个package可以定义多个init函数，甚至在同一个go文件也可以有多个init函数。
- 如果一个包没有import其他包，则多个init按出现顺序初始化
- 同一个包多个文件都有init函数则按文件名顺序初始化
- 一般go fmt的话，会对import进行排序，这样子保证初始化行为的可再现性
- 如果一个包有import其他包，则按依赖顺序从最里层包开始初始化
```go
package main
import "fmt"

func init(){
    fmt.Println("init.....")
}
func main(){
    fmt.Println("main.....")
}

##结果##
init.....
main.....
```
## 函数的defer
❗️为了在函数执行完成后，及时释放资源，go的设计者提供了defer（延时机制）  
适用于关闭文件、关闭数据库连接等
```go
package main
import "fmt"

func test() int {
    defer fmt.Println("s1")
    defer fmt.Println("s2")
    var ss int = 10
    fmt.Println("s3")
    return ss
}

func main(){
    ret := test()
    fmt.Println(ret)
}

##结果##
s3
s2
s1
10
```
## 匿名函数
```go
package main
import "fmt"

func main(){
    res := func(n1,n2 int) int{
        return n1 + n2
    }
    
    var s1 int
    var s2 int
    s1 = res(1,2)
    fmt.Println(s1)
    s2 = res(3,4)
    fmt.Println(s2)
}

##结果##
3
7
```
#### 全局匿名
```go
package main
var (
    res := func(n1,n2 int) int{
        return n1 + n2
    }
)
```
## 递归函数
```go
package main
import "fmt"

func digui_func(n1 int){
    if n1 > 2 {
        n1--
        fmt.Println(n1)
        digui_func(n1)
    }
}
func main(){
    digui_func(5)
}

##结果##
4
3
2
```
## 闭包函数
```go
package main 
import "fmt"

func bibao() func (int) int {
    var n int = 10
    return func (x int) int {
        n = n + x
        return n
    }
}
func main(){
    f := bibao()
    f1 := bibao()
    fmt.Println(f(1))
    fmt.Println(f1(2))

}

##结果##
11
12
```