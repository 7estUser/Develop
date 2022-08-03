## 时间单位
```golang
时 	 Hour = 60 * Minute		
分 	 Minute = 60 * Second
秒 	 Second = 1000 * Millisecond
毫秒  Millisecond = 1000 * Microsecond	千分之一秒
微秒  Microsecond = 1000 * Nanosecond	百万分之一秒
纳秒  Nanosecond	 = 1	十亿分之一秒  
```
## time 类型
- time.ParseDuration("1h")：解析持续时间字符串  
- Sub()：计算时间间隔
- Zone()：返回时区和和偏移量(UTC以东的秒数)
## Duration 类型
Duration：持续时间  ⚠️基本单位：Nanosecond(纳秒)  
- Milliseconds()：以整数毫秒计数的形式查找持续时间  
- Microseconds()：微秒	Minutes()：