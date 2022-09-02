### 生成随机数
```go
//100以内随机数
//伪随机数
rand.Seed(time.Now().UnixNano())
i := rand.Intn(100)
//真随机数
n, _ := rand.Int(rand.Reader, big.NewInt(100))
n.Int64()

//随机字符串
var defaultLetters = []rune("abcdefghijklmnopqrstuvwxyzABCDEFGHIJKLMNOPQRSTUVWXYZ0123456789")
func RandomString(n int, allowedChars ...[]rune) string {
   var letters []rune
   if len(allowedChars) == 0 {
      letters = defaultLetters
   }else {
      letters = allowedChars[0]
   }
   b := make([]rune, n)
   for i := range b {
      b[i] = letters[rand.Intn(len(letters))]
   }
   return string(b)
}
```
- math/rand     // 伪随机
- crypto/rand   // 真随机(性能比math/rand要低很多，差十倍)
- 对于不涉及到密码类的开发工作直接使用math/rand+基于时间戳的种子rand.Seed(time.Now().UnixNano())一般都能满足需求
- 对于涉及密码类的开发工作一定要用crypto/rand
- 如果想生成随机字符串，可以先列出字符串，然后基于随机数选字符的方式实现
