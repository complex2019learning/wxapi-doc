#公众号文章，阅读数，点赞数更新接口

url请求需带上参数key，每个用户有唯一的key。

所有接口均返回json格式，其中参数ok[true|false]表示是否请求成功.

####更新回调接口
```
此接口为POST method，由用户提供，当公众号文章，阅读点赞数更新时，会主动调用此接口。

如果返回状态非200，则可通过［主动拉取未发送的更新数据接口］查询。

eg：
回调接口为
http://test.com/api/receiveExtNotification
则当公众号更新文或阅读点赞数据时会传送以下Json格式的Request Body:
{
  "data": [
    {
      "operation": "NEW",
      "account": "banyuetan-weixin",
      "title": "【品读】真正的善良，是让大家都体面",
      "url": "http://mp.weixin.qq.com/s?__biz=MjM5OTU4Nzc0Mg==&mid=2658605478&idx=1&sn=713642344f4b87d3b3e8139137b5c822",
      "timestamp": 1498570320,  #文章发布时间戳
      "clicksCount": 100,  #阅读数
      "likeCount": 3  #点赞数
    },
    {
      "operation": "UPDATE",
      "account": "banyuetan-weixin",
      "title": "just for test",
      "url": "http://test.com",
      "timestamp": 1498570320,
      "clicksCount": 10,
      "likeCount": 1
    }
  ]
}

operation参数可取[NEW|UPDATE]：取NEW时表示是新文章，为UPDATE时表示更新文章的阅读点赞数据。
同一篇文章不会在data中出现两次。
```

####主动拉取未发送的更新数据
```
http://whosecard.com:8081/api/notification/unsendedExt?key=***

此接口与更新回调接口结合使用，用户可主动拉取最近10分钟内未发送（包括发送失败或待发送的数据）的更新列表。

当key校验成功后，会返回如下格式数据：
{
  "ok":true,
  "notifications":[
    {
      "operation": "NEW",
      "account": "banyuetan-weixin",
      "title": "【品读】真正的善良，是让大家都体面",
      "url": "http://mp.weixin.qq.com/s?__biz=MjM5OTU4Nzc0Mg==&mid=2658605478&idx=1&sn=713642344f4b87d3b3e8139137b5c822",
      "timestamp": 1498570320,  #文章发布时间戳
      "clicksCount": 100,  #阅读数
      "likeCount": 3  #点赞数
    }
  ]
}
```

####主动拉取更新数据
```
http://whosecard.com:8081/api/notification/listExt?key=***

此接口与更新回调接口结合使用，用户可主动拉取最近5分钟的更新列表。

当key校验成功后，会返回如下格式数据：
{
  "ok":true,
  "notifications":[
    {
      "operation": "NEW",
      "account": "banyuetan-weixin",
      "title": "【品读】真正的善良，是让大家都体面",
      "url": "http://mp.weixin.qq.com/s?__biz=MjM5OTU4Nzc0Mg==&mid=2658605478&idx=1&sn=713642344f4b87d3b3e8139137b5c822",
      "timestamp": 1498570320,  #文章发布时间戳
      "clicksCount": 100,  #阅读数
      "likeCount": 3  #点赞数
    }
  ]
}
```

####添加公众号
```
http://whosecard.com:8081/api/account/addExt?account=WebNotes&key=***

account不区分大小写，必须先添加公众号后才能接收／拉取公众号更新数据

返回格式如下：
{ok: true}
```

####取消订阅公众号
```
http://whosecard.com:8081/api/account/decExt?account=WebNotes&key=***

account不区分大小写。

返回格式如下：
{ok: true}
```

####获取订阅公众号列表
```
http://whosecard.com:8081/api/account/listExt?key=***

account均为小写。

返回格式如下：
{ok: true, "accounts":["webnotes", "yingshidamowang"]}
```

####获取订阅公众号数量
```
http://whosecard.com:8081/api/account/countExt?key=***

返回格式如下：
{ok: true, "count":100}
```

