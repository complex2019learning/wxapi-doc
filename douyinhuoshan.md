# 实时抖音火山版接口

#### 接口说明
* 账号注册请联系qq:1628121385，添加好友时请注明:wxapi
* url请求需带上参数key，每个用户有唯一的key。
* 所有接口均返回json格式，其中参数ok[true|false]表示是否请求成功.
* retCode为返回码，详情参考[返回码说明](https://iwoods.coding.net/p/wxapi-doc/d/wxapi-doc/git/blob/master/retcode.md)
* 当返回ok=false时，可以参考返回的error字段（如果存在的话）
* 一般来说，接口只要返回cost=true，就表示请求有效，会进行收费，此时请不要再重试了，这种情况一般是请求资源已经失效。

**除非特殊说明，默认都是从app接口获取数据。**

#### 实时获取单个视频详细信息
```
http://whosecard.com:8081/api/douyin/huoshan/item/info?key=***&item_id=6799640884544687375

item_id为视频id，值得注意的是，抖音火山版的视频id与抖音app的视频id是互通的（当然抖音app里的视频不一定完全同步到火山app里）

返回如下：
{
  "ok": true,
  "result": {
    ... # 返回值与官方接口一样，字段比较多，按字面意思理解即可
  },
  "cost": true,
  "retCode": 0
}

result包含了抖音返回的所有字段数据，除了statistics字段外还会返回其它字段，按照字面意思理解即可。

当视频不存在时，则返回如下：
{
  "cost": true,
  "error": "作品不存在",
  "ok": false,
  "retCode": 1002
}
```
