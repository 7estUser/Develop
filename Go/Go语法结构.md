注意⚠️：  
函数、变量等名首字母小写：private  
函数、变量等名首字母大写：public  
go对象使用注意：*指针引用和值拷贝的区别  
# 编写格式

## 导入package：
```go
	#导入的包必须全部都要被调用，不然会报错
	import{
		"fmt"
		"io"
	}
	包别名：
	import{
		shuchu "fmt"
	}
	使用时：shuchu.Println("别名调用")
```
## 常量定义：
```go
	单个：const _name [type] = value
	多个：const(
			name1 = value1
			name2 = value2
		 )
	#常量一般为字母全部大写。
	#const 多个定义时，没有赋值的对像向上引用，和上面的对像赋值相同。
```
## 全局变量定义：
```go	
	type _name [type] = value
	var _name [type] = value
```
## 非全局变量定义：
```go	
	var _name [type] = value
	_name := value 	只可以在方法体内使用
```
## 接口定义：
```go	
	type interface_name interface{#抽象方法}
```
❗️❗️❗️  
#只定义方法名称，不写具体实现，某个类型如果拥有该接口的所有方法实现，即实现了这个接口  
#一个类型可以同时实现多个接口，且接口间相互独立，彼此不知道对方如何实现。其实就是这个类型包含了多个接口里所有的方法实现。  
#空接口interface{}可以作为任何类型数据的容器（任何数据的父类，等效java中的Object类）  
❗️❗️❗️
## 结构体定义：
```go	
	type className struct{#属性}
```
⚠️注意：在初始化结构(类)的时候，使用取地址符 & 来初始化, `&testClass{}`
## 类定义：
❗️就是通过结构体绑定方法❗️
```go
	func (test *className) funcName() string {}
```
## 方法定义：
```go	
	func funcName(parameter classType) [return_type]{}
```
❗️方法和类定义的区别：结构体(类)中的方法是在结构体(类)外定义的,且类定义的名字前是有括号，里面填写结构体类型  
⚠️[func init(){}是特殊的方法](Go函数.md)
## Demo
```go
	//定义接口
	type Sayer interface{
		say()
	}
	//定义结构体
	type dog struct{}
	type cat struct{}
	//值类型接收者实现接口
	func (d dog) say(){
		fmt.Println("汪汪")
	}
	//指针类型接收者实现接口
	func (c *cat) say(){
		fmt.Println("喵喵")
	}
	//此时dog和cat类都属于Sayer，以为他们都实现了Sayer接口里的所有方法
	func main(){
		var x Sayer
		d1 := dog{}
		x = d1	//x可以接受dog类型
		x.say()
		d2 := &dog{}
		x = d2	//x可以接受*dog类型
		x.say()

		c1 := cat{}
		x = c1 	//❗️报错，x不可以接受cat类型
		x.say()
		c2 := &cat{}
		x = c2 	//x可以接受*cat类型
		x.say()
	}
```
1. 使用值接收实现接口后，不管是值类型的 `dog` 结构体还是指针类型的 `*dog` 都可以赋值给该接口变量。  
2. 使用指针接收实现接口后，只能将指针类型的 `*cat` 赋值给该接口变量，而值类型的 `cat` 不能赋值。  
--------------------------------------------------------------------------
# 内置语法/函数使用：

## slice切片(动态数组)：
```go	
	创建：make([]Type,len,cap)	len:元素个数	cap:容量，可以省略，省略时和len值相同。
	#slice实际为(指针)指向底层的数组，所以多个slice指向相同底层数组时(数组内存地址相同)，其中一个改变也会影响其他全部。
	#当slice容量改变(扩容时)，数组内存地址就会改变，即成为一个新的数组，不在影响其他slice。
	#b := a[2:5] 方式取数组时，[]下标左包含右不包含，数组b的实际容量为a数组2开始到数组最后的长度。
```
⚠️ `a := [4]int{1,2,3,4}` ：go中，只有\[\]括号里带数字的是定长数组，其余皆为切片  
## range迭代：
```go	
	for i,v:=range slice{slice[i]=v}
	for k,v:=range map{map[k]=v}
	#v是值的拷贝，v的操作都不会影响原始的值。所以对原始数据进行操作的话，需要使用i或者k。
```
## exception处理：
```go	
	defer panic recover
	等价于 try...catch...finally
	1、defer是倒序调用且函数发生错误也会执行，类似finally，但是要写在panic前面。
	2、panic语句会终止其后面要执行的代码（运行报错）
	3、recover用来捕获panic，可以处理goroutine的panicking过程，从而恢复程序继续运行，只在defer中使用有效
		子函数 panic ，并且有 recover，不影响主函数的执行（输出recover捕获的异常后主函数继续执行）；
		子函数 panic，主函数 recover，程序不会终止执行（输出recover捕获的异常），但是panic子函数后面的主函数代码不会再执行；
		子协程 panic，主函数 recover，程序会终止执行（报错）；
		子协程 panic，子协程 recover，不影响主函数执行（最后输出recover捕获的异常）
	defer func(){ //defer声明必须在panic前面
		err := recover() //panic传入的内容
	}()
	panic("异常信息") //后面的代码不会再执行
```
## reflect反射：	
	#只有interface类型才有反射,用来获取结构(类)的内部信息。
	reflect.TypeOf() 可以获得任意值的类型对象(reflect.Type)
		.Name() 对象类型名称  
		.Kind() 对象归属种类	
		.NumField() 返回对象包含字段个数  
		.Field(i) 返回对象包含字段中第i个字段值对像（name，type，value：.Interface()）  
		#NumField()和Field(i)结合使用遍历结构体的每个字段  
		.NumMethod() 返回结构体定义的方法个数  
		.Method(i) 返回结构体的第i个方法   
	reflect.ValueOf() 获取reflect.Value 对像，reflect.Value 与原值间可以通过值包装和值获取互相转化。  
## concurrency并发:	
	使用并发：通过 go 关键字来开启 goroutine 即可  
	`go + 方法名`
## channel通道：
```go	
	#是goroutine沟通的桥梁，用于两个goroutine之间来通过传递一个指定类型的值来同步运行和通信。
	创建通道：
		ch := make(chan type)
		#默认情况下，通道是不带缓冲区的,发送的同时就必须有其他地方接收,没有接收之前当前线程就会阻塞。
		#创建有缓冲区的通道：ch := make(chan int,10)，未被填满之前不会发生阻塞。
	发送/接收值：
		ch <- v	 	// 把 v 发送到通道 ch
		v := <-ch   // 从 ch 接收数据，并把值赋给 v
	遍历通道：
		for rangge{}
	关闭通道：
		close(chanName)
		v,ok := <-ch
		#通道关闭后，ok 就为 false，可以通过这个来判断通道是否被关闭。
```
## select随机处理通信操作：
```go	
	select{
		case i1 = <- c1:
		case c2 <- i2:
	}
	#每个 case 必须是一个通信操作，要么是发送要么是接收。
	#有多个case都可以运行，会随机的执行一个。
	否则：
	如果有 default 子句，则执行该语句。
	如果没有 default 子句，select 将阻塞，直到某个通信可以运行；Go 不会重新对 channel 或值进行求值。
	可用空的select来阻塞main函数。
```
## 命令行参数解析
```go
import "flag"
var name strings
var age int
var is bool
flag.StringVar(&name, "name", "张三", "姓名")   //绑定对象，命令行参数名称，默认值，参数说明
flag.IntVar(&age, "age", 18, "年龄")
flag.BoolVar(&married, "married", false, "婚否")
flag.Parse()    //参数解析
```
## 语法糖
### ... 的用法
1. 第一个用法主要是用于函数有多个不定参数的情况，表示为可变参数，可以接受任意个数但相同类型的参数。
```go
func test1(args ...string) {} //可以接受任意个string参数
```
2. 第二个用法是slice可以被打散进行传递。
```go
var strss= []string{"qwr","234","yui"}
var strss2= []string{ "qqq","aaa","zzz","zzz"}
strss=append(strss,strss2...) //strss2的元素被打散一个个append进strss
```
------------------------------------------------------------------------------------------