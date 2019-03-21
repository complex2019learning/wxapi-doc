#快手接口

url请求需带上参数key，每个用户有唯一的key。

所有接口均返回json格式，其中参数ok[true|false]表示是否请求成功.


####1. 获取用户个人信息（web版）
```
http://whosecard.com:8081/api/kuaishou/profile?profileUrl=***&key=***

参数prifileUrl为快手个人页的分享链接，需要urlencode，比如：
https://live.kuaishou.com/profile/xq935932775
编码后为
https%3a%2f%2flive.kuaishou.com%2fprofile%2fxq935932775

返回如下：
{
  "ok": true,
  "result": {
    ... # 返回值与官方接口一样，字段比较多，按字面意思理解即可
  }
}

ps：所有统计性数字上万后会使用缩写，比如：3.1w
```

####2. 获取单个视频的信息（web版）
```
http://whosecard.com:8081/api/kuaishou/photo/profile?photoUrl=***&key=***

photoUrl为单个视频的分享链接，比如：https://live.kuaishou.com/u/3xtn3m4vezveq6u/3x2izyrw6bup9nm， 同样需要urlencode

返回如下：
{
  "ok": true,
  "result": {
    ... # 返回值与官方接口一样
  }
}
```

####3. 获取小店商品列表
```
http://whosecard.com:8081/api/kuaishou/grocery/product?userId=358250606&page=1&key=***

userId为快手用户ID。
page指定页数，从1开始。

返回如下：
{
  "ok": true,
  "result": {
    ... # 返回值与官方接口一样
  }
}
```

####4. 获取用户视频流Feed
```
http://whosecard.com:8081/api/kuaishou/user/feeds?userId=3xtn3m4vezveq6u&pcursor=***&key=***

userId为快手用户ID。
pcursor用于翻页，第一页不用填，返回结果的pcursor值为下一页的请求参数。

返回如下：
{
  "ok": true,
  "result": {
    ... # 返回值与官方接口一样
  }
}
```

####5. 获取tag的Feed流
```
http://whosecard.com:8081/api/kuaishou/tag/feeds?tag=手机摄影&pcursor=***&key=***

tag为指定话题参数。
pcursor用于翻页，第一页不用填，返回结果的pcursor值为下一页的请求参数。

返回如下：
{
  "ok": true,
  "result": {
    ... # 返回值与官方接口一样
  }
}
```