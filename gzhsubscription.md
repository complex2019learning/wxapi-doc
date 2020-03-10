# 订阅公众号最新发文（推送模式）

#### 订阅公众号步骤
* 提供推送回调接口（有新文章时会推送给这个接口）
* 使用订阅接口，进行订阅操作
* 对于订阅失败的号（可能是没有增加到实时更新库里），请批量将biz提交给作者
* 对于不需要再订阅的公众号，可以随时取消订阅

#### 使用须知
* 订阅/取消订阅这两个接口会收取1000次40元的费用，目的是为了防止胡乱操作，望理解
* 获取订阅列表不收费

#### 结算方式
* 除了订阅操作本身产生的费用外，每个号每天也会产生订阅费用，具体费用请咨询作者
* 订阅费用使用后付费结算方式，所以尽量对余额进行预留，防止扣除时余额不足

#### 接口说明
* url请求需带上参数key，每个用户有唯一的key。
* 所有接口均返回json格式，其中参数ok[true|false]表示是否请求成功.
* 如果不明白biz是什么，请参考[FAQ](https://whosecard.com/faq)

##### 当有新文章时的推送方式
```
POST 链接为用户提供的回调接口

回调接口传的时json格式数据，如下：
[
  {
    "biz" : "MzI3NTQxOTA5NA==",
    "mid" : 2247496752,
    "idx" : 6,
    "url" : "http://mp.weixin.qq.com/s?__biz=MzI3NTQxOTA5NA==&mid=2247496752&idx=6&sn=ce24182b39feb7764ea52a06335d6674&scene=0",
    "time" : 1583807728,
    "title" : "小品《四大才子》，乐坏了",
    "content" : "",
    "cover" : "http://mmbiz.qpic.cn/mmbiz_jpg/IRFXibKRUAQsDppLSQx3icI7AuCfGXFfRrGLDPEoAqdEQVNKiagakC1BcpzJWTC1vNnEz6lib8pLYLCickyJFIibcdDA/0?wx_fmt=jpeg"
  },
  ...
]
```

##### 订阅公众号

```
GET http://whosecard.com:8081/api/wx/gzh/subscription/add?biz=***&key=***

query参数解释：
biz: 公众号biz，如: MjM5MjAxNDM4MA==

请求成功会返回如下：
{
  "cost": true,
  "ok": true
}
```

##### 取消订阅公众号
```
GET http://whosecard.com:8081/api/wx/gzh/subscription/dec?biz=***&key=***

query参数解释：
biz: 公众号biz，如: MjM5MjAxNDM4MA==

请求成功会返回如下：
{
  "cost": true,
  "ok": true
}
```

##### 获取订阅的公众号列表
```
GET http://whosecard.com:8081/api/wx/gzh/subscription/list?key=***

query参数解释：
page: 页数，默认为0，每页最多返回100个订阅的biz

请求成功会返回如下：
{
  "bizList": [
    "MjM5OTYyNDYwMA=="
  ],
  "cost": true,
  "count": 1,
  "ok": true
}
```
