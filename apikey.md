#获取微信号key

url请求需带上参数key，每个用户有唯一的key。

所有接口均返回json格式，其中参数ok[true|false]表示是否请求成功.

####实时获取公众号文章阅读点赞数据
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

```
