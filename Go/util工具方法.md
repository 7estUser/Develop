### 生成随机数
```go
//100以内随机数
//伪随机数
import math/rand
rand.Seed(time.Now().UnixNano())
i := rand.Intn(100)
//真随机数
import crypto/rand
n, _ := rand.Int(rand.Reader, big.NewInt(100))
n.Int64()

//随机字符串
func RandomString(length int) string {
   chars := "ABCDEFGHIJKLMNOPQRSTUVWXYZabcdefghijklmnopqrstuvwxyz0123456789"
   result := make([]byte, length)
   rand.Seed(time.Now().UnixNano())
   for i := 0; i < length; i++ {
      result[i] = chars[rand.Intn(len(chars))]
   }
   return string(result)
}
```
- math/rand     // 伪随机，每次程序启动产生的都是一样的。
- crypto/rand   // 真随机(性能比math/rand要低很多，差十倍)
- 对于不涉及到密码类的开发工作直接使用math/rand+基于时间戳的种子rand.Seed(time.Now().UnixNano())一般都能满足需求
- 对于涉及密码类的开发工作一定要用crypto/rand
- 如果想生成随机字符串，可以先列出字符串，然后基于随机数选字符的方式实现
