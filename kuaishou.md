# 快手接口

url请求需带上参数key，每个用户有唯一的key。

所有接口均返回json格式，其中参数ok[true|false]表示是否请求成功.

#### 根据用户分享链接获取用户id信息
```
http://whosecard.com:8081/api/kuaishou/userIdInfo?profileUrl=***&key=***

参数prifileUrl为快手个人页的分享链接，需要urlencode，比如：
https://live.kuaishou.com/profile/xq935932775
编码后为
https%3a%2f%2flive.kuaishou.com%2fprofile%2fxq935932775

返回如下：
{
  "ok": true,
  "result": {
    "userEid": "xq935932775",
    "userId": 344153274
  }
}
```

#### 获取用户个人信息（app版）
```
http://whosecard.com:8081/api/kuaishou/profile?userId=***&key=***

userId为用户唯一数字id，如: 119808726
返回如下：
{
  "ok": true,
  "result": {
    ... # 返回值与官方接口一样，字段比较多，按字面意思理解即可
  }
}

ps：所有统计性数字上万后会使用缩写，比如：3.1w
```

#### 获取单个视频的信息（app版）
```
http://whosecard.com:8081/api/kuaishou/photo/profile?photoId=***&key=***

photoId是视频的唯一数字id，如：5189835632447473584

返回如下：
{
  "ok": true,
  "result": {
    ... # 返回值与官方接口一样
  }
}
```

#### 获取小店商品列表
```
http://whosecard.com:8081/api/kuaishou/grocery/product?userId=358250606&page=1&key=***

userId为快手用户id。
page指定页数，从1开始。

返回如下：
{
  "ok": true,
  "result": {
    ... # 返回值与官方接口一样
  }
}
```

#### 获取用户视频流Feed（app版）
```
http://whosecard.com:8081/api/kuaishou/user/feeds?userId=119808726&pcursor=***&key=***

userId为快手用户唯一数字id。
pcursor用于翻页，第一页不用填，返回结果的pcursor值为下一页的请求参数。

返回如下：
{
  "ok": true,
  "result": {
    ... # 返回值与官方接口一样
  }
}
```

#### 获取tag的Feed流（app版）
```
http://whosecard.com:8081/api/kuaishou/tag/feeds?tag=手机摄影&feedType=***&pcursor=***&key=***

tag为指定话题参数。
feedType为请求feed类型，一共两种：热门与最近，分别取值为: hot|recent。
pcursor用于翻页，第一页不用填，返回结果的pcursor值为下一页的请求参数。

返回如下：
{
  "ok": true,
  "result": {
    ... # 返回值与官方接口一样
  }
}
```

#### 获取tag详情页（app版）
```
http://whosecard.com:8081/api/kuaishou/tag/info?tag=手机摄影&key=***

tag为指定话题参数。

返回如下：
{
  "ok": true,
  "result": {
    ... # 返回值与官方接口一样
  }
}
```

#### location poi接口（app版）
```
http://whosecard.com:8081/api/kuaishou/location/poi?poiId=***&subPath=***&pcursor=***&key=***

poiId为位置id，如：68088943
subPath可取值为: detail与feed，分别代表详情页与feed页。
当subPath=feed时，pcursor用于翻页，第一页不用填，返回结果的pcursor值为下一页的请求参数。

返回如下：
{
  "ok": true,
  "result": {
    ... # 返回值与官方接口一样
  }
}
```
