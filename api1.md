#公众号即时更新接口

url请求需带上参数key，每个用户有唯一的key。

所有接口均返回json格式，其中参数ok[true|false]表示是否请求成功.

####更新回调接口
```
此接口由用户提供，当公众号更新时，会主动调用此接口，并将公众号account与更新时间timestamp作为query string。

如果返回状态非200，则可通过［主动拉取未发送的更新数据接口］查询。

eg：
回调接口为
http://test.com/api/receiveNotification
则当WebNotes公众号更新时会请求:
http://test.com/api/receiveNotification?account=WebNotes&ts=1496331127
```

####主动拉取未发送的更新数据
```
http://whosecard.com:8081/api/notification/unsended?key=***

此接口与更新回调接口结合使用，用户可主动拉取最近一小时内未发送（包括发送失败或待发送的数据）的更新列表。

当key校验成功后，会返回如下格式数据：
{"ok":true, "notifications":[{'account': 'WebNotes', 'ts': 1496331175}]}
```

####主动拉取更新数据
```
http://whosecard.com:8081/api/notification/list?key=***

此接口与更新回调接口结合使用，用户可主动拉取最近一个小时的公众号更新列表。

当key校验成功后，会返回如下格式数据：
{"ok":true, "notifications":[{'account': 'WebNotes', 'ts': 1496331175}]}
```

####添加公众号
```
http://whosecard.com:8081/api/account/add?account=WebNotes&key=***

account不区分大小写，必须先添加公众号后才能接收／拉取公众号更新通知。

返回格式如下：
{ok: true}
```

####取消订阅公众号
```
http://whosecard.com:8081/api/account/dec?account=WebNotes&key=***

account不区分大小写。

返回格式如下：
{ok: true}
```

####获取订阅公众号列表
```
http://whosecard.com:8081/api/account/list?key=***

account均为小写。

返回格式如下：
{ok: true, "accounts":["webnotes", "yingshidamowang"]}
```

####获取订阅公众号数量
```
http://whosecard.com:8081/api/account/count?key=***

返回格式如下：
{ok: true, "count":100}
```

