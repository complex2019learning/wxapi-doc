#快手接口

url请求需带上参数key，每个用户有唯一的key。

所有接口均返回json格式，其中参数ok[true|false]表示是否请求成功.


####1. 获取用户信息（web版）
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

除了返回个人信息外，同时也会返回最近发布的一批视频信息。
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

ps：这个接口的单视频放在currentWork字段中，此外还会返回user profile以及user最近发布的视频列表。
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
