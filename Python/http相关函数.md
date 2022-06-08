### urlparse模块用于解析url中的参数,对url按照一定格式进行拆分或拼接 
```python
	import urlparse
	url_change = urlparse.urlparse('https://i.cnblogs.com/EditPosts.aspx?opt=1')
	print(url_change)
```
输出：
```
	seResult(scheme='https', netloc='i.cnblogs.com', path='/EditPosts.aspx', params='', query='opt=1', fragment='')
	scheme ：协议，netloc ：域名服务器，path ：相对路径，params ：参数，query ：查询的条件
```
### url请求走代理
```python
	proxies={
	'http':'127.0.0.1:8080',
	'https':'127.0.0.1:8080'
	}
	r = requests.get(url,proxies=proxies)
```
### url特殊字符编码
```python
	import urllib.parse
	encoded_url = urllib.parse.quote(url)
```