###模拟阅读点赞接口

```
此接口为POST method.
接口返回json格式，其中参数ok[true|false]表示是否请求成功.

eg: 
http://whosecard.com:8081/api/mock/read?key***
query string中的key为接口认证key。

请求时需要传入的post body:
{
	"key": key,
	"uin": uin,
	"like": true|false, #可选参数，不传则默认不点赞
	"url": url #此链接为文章长链接，需包含__biz参数
}

返回值：
{"ok": true}
或
{"ok": false, "error":"***"}

url长链接样式如下：
https://mp.weixin.qq.com/s?__biz=MjM5ODIyMTE0MA==&mid=2650969971&idx=1&sn=55f711ca0611651d798acb8aab783807&scene=0
```


###python示例代码

```
import requests
import json
url = 'http://localhost:8081/api/mock/read?key=***'
data = {
  'key':'***',
  'uin':'***',
  'url':'https://mp.weixin.qq.com/s?__biz=MzI0MDYwMzYyMQ==&mid=2247484050&idx=2&sn=0729ce8e19a0cd8a06c34b08356cba41&chksm=e9191a18de6e930e19de9183af414f98ff8a751f15d192f25752f559dc31cd6b215b0cf3bbc2&mpshare=1&scene=1&srcid=0303JSbyBvWZiczaHdVTZmJW#rd',
  'like':True,
}
headers = {'content-type':'application/json'}
r = requests.post(url, data=json.dumps(data), headers=headers)
print(r.json())

返回：
{'ok': True}
```