#获取微信号key

url请求需带上参数key，每个用户有唯一的key。

所有接口均返回json格式，其中参数ok[true|false]表示是否请求成功.

####实时获取微信号key
```
http://whosecard.com:8081/api/wxkeys/fetch?key=***

请求成功会返回一个key：
{
  "ok": true,
  "count": 1,
  "keys": [
    {
      "uin": "***",
      "key": "***",
      "ts": 1508747233,  # key产生时间
      "ttl": 1878  # key剩余有效秒数
    }
  ]
}


获取文章列表python代码示例：

import requests
headers = {
  'X-WECHAT-KEY': '***',
  'X-WECHAT-UIN': '***',
  'User-Agent': 'Mozilla/5.0 (iPhone; CPU iPhone OS 11_0_3 like Mac OS X) AppleWebKit/604.1.38 (KHTML, like Gecko) Mobile/15A432 MicroMessenger/6.5.18 NetType/WIFI Language/zh_CN',
}
url = 'https://mp.weixin.qq.com/mp/profile_ext?action=home&__biz=MTQzMjE1NjQwMQ==&scene=124&devicetype=iOS11.0.3&version=16051220&lang=zh_CN&nettype=WIFI&a8scene=3&fontScale=100&pass_ticket=&wx_header=1'
page = requests.get(url, headers=headers, timeout=5).text

```