#公众号即时更新接口

url请求需带上参数key，每个用户有唯一的key。

所有接口均返回json格式，其中参数ok[true|false]表示是否请求成功.

####更新回调接口
```
此接口为POST method，由用户提供，当公众号更新时，会主动调用此接口，回传数据包括公众号account，更新时间ts，文章列表essays。

对于最新订阅的公众号，只会抓取当前订阅时间以后的文章列表。

如果返回状态非200，则可通过［主动拉取未发送的更新数据接口］查询。

eg：
回调接口为
http://test.com/api/receiveNotification

则当公众号更新时会传送如下Json格式的Request Body: (request body被json dumps成了字符串，接收数据后需要进行json格式处理)
{
  "data": {
        "account" : "Learnlord",
        "ts" : 1500944415,
        "essays" : [ 
            {
                "title" : "他是英国最残暴、最文艺的罪犯,40年间蹲过120座监狱,却用一双手温暖了大家的心",
                "url" : "http://mp.weixin.qq.com/s?__biz=MjM5OTA5MzQzNQ==&mid=2651161756&idx=3&sn=cd5e6a26abd0804806b0d92b9b4a0a65&scene=0#wechat_redirect"
            }, 
            {
                "title" : "CNN评选出美国Top50中餐厅,看完我只想去大吃特吃!",
                "url" : "http://mp.weixin.qq.com/s?__biz=MjM5OTA5MzQzNQ==&mid=2651161756&idx=2&sn=c6a37032423c58cfdc5d3509009c725a&scene=0#wechat_redirect"
            }
        ]
    }
}

```

####主动拉取未发送的更新数据
```
http://whosecard.com:8081/api/notification/unsended?key=***

此接口与更新回调接口结合使用，用户可主动拉取最近一小时内未发送（包括发送失败或待发送的数据）的更新列表。

当key校验成功后，会返回如下格式数据：
{"ok":true, "notifications":[{'account': 'WebNotes', 'ts': 1496331175}]}

如果想自定义取一天内任一段时间内的数据，通过传入查询的开始时间戳start与结束时间戳end（不传则默认结束时间戳为当前时间）.
自定义时间段不能超过30分钟，即end-start<=1800

eg:
http://whosecard.com:8081/api/notification/unsended?key=***&start=1499066515&end=1499066615
```

####主动拉取更新数据
```
http://whosecard.com:8081/api/notification/list?key=***

此接口与更新回调接口结合使用，用户可主动拉取最近一个小时的公众号更新列表。

当key校验成功后，会返回如下格式数据：
{"ok":true, "notifications":[{'account': 'WebNotes', 'ts': 1496331175}]}

可自定义取一天内任意时间段的数据，方法同上。
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

