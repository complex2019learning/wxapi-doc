#api接口描述

所有接口均为GET接口，url请求需带上参数key，每个用户有唯一的key。

所有接口均返回json格式，其中参数ok[true|false]表示是否请求成功.

####更新回调接口
```
此接口由用户提供，当公众号更新时，会主动调用此接口，并将公众号account与更新时间timestamp作为query string。
eg：
回调接口为
http://test.com/api/receiveNotification
则当WebNotes公众号更新时会请求:
http://test.com/api/receiveNotification?account=WebNotes&ts=1496331127
```

####主动拉取更新数据
```
http://whosecard.com:8081/api/notifications?key=***

此接口与更新回调接口结合使用，用户可主动拉取最近一个小时的公众号更新列表。

当key校验成功后，会返回如下格式数据：
{"ok":true, "notifications":[{'account': 'WebNotes', 'ts': 1496331175}]}
```

####添加公众号
```
http://whosecard.com:8081/api/addaccount?account=WebNotes&key=***

account不区分大小写，必须先添加公众号后才能接收／拉取公众号更新通知。

返回格式如下：
{ok: true}
```

####取消订阅公众号
```
http://whosecard.com:8081/api/decaccount?account=WebNotes&key=***

account不区分大小写。

返回格式如下：
{ok: true}
```

####获取订阅公众号列表
```
http://whosecard.com:8081/api/getaccounts?key=***

account均为小写。

返回格式如下：
{ok: true, "accounts":["webnotes", "yingshidamowang"]}
```

####获取订阅公众号数量
```
http://whosecard.com:8081/api/accountnum?key=***

返回格式如下：
{ok: true, "count":100}
```

####公众号文章临时链接转为永久链接
```
http://whosecard.com:8081/api/transferurl?url=***&key=***

参数中的url为urlencode后的临时链接（从搜狗获取的文章链接）
eg:
http://whosecard.com:8081/api/transferurl?url=https%3a%2f%2fmp.weixin.qq.com%2fs%3ftimestamp%3d1495560892%26src%3d3%26ver%3d1%26signature%3diwHBaGJJBumXB4o0dEjdFM-Tm4DoYVUBEbzMGXK9Mb3Zy8Xbv8TJuJRRYq4*XWheCnRL1ZUMtIZeqGJfFMyMlE3hKi-3*7EMlUMaEid3BV4Ip5CjG3uihOI3OSpK07dkjTLw2LXxfp103Kcq4Gkc*I0ekHo4gu*lHbiFG8qRPSg%3d&key=***
```

####公众号文章短链接转为长链接
```
http://whosecard.com:8081/api/transferurl/short2long?url=***&key=***

参数中的url为urlencode后的短链接
eg:
http://whosecard.com:8081/api/transferurl/short2long?url=https%3a%2f%2fmp.weixin.qq.com%2fs%2fAuyufPtU1UeusDS6B34VZg&key=***
```