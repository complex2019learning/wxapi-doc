# 订阅公众号最新发文（推拉结合）

#### 接口说明
* 账号注册请联系qq:1628121385，添加好友时请注明:wxapi
* url请求需带上参数key，每个用户有唯一的key。
* 所有接口均返回json格式，其中参数ok[true|false]表示是否请求成功.
* retCode为返回码，详情参考[返回码说明](https://iwoods.coding.net/p/wxapi-doc/d/wxapi-doc/git/blob/master/retcode.md)
* 当返回ok=false时，可以参考返回的error字段（如果存在的话）
* 如果不明白biz是什么，请参考[FAQ](https://whosecard.com/faq)

#### 使用步骤
* 提供推送回调接口（有新文章时会推送给这个接口），如果不提供回调接口，可自行拉取数据
* 使用订阅接口，进行订阅操作
* 对于订阅失败的号（可能是没有增加到实时更新库里），请批量将biz提交给作者
* 对于不需要再订阅的公众号，可以随时取消订阅

#### 使用须知
* 订阅/取消订阅这两个接口会收取1000次40元的费用，目的是为了防止胡乱操作，望理解
* 获取订阅列表不收费，推送/拉取数据不收费
* 本功能提供推拉两种获取数据的方式，如果非常在意实时性，请提供推送回调接口，如果对实时性不那么敏感，可以使用拉取接口自行控制频率
* 数据最长保留三天，过期不候

#### 结算方式
* 除了订阅操作本身产生的费用外，每个号每天也会产生订阅费用，具体费用请咨询作者
* 订阅费用使用后付费结算方式，所以尽量对余额进行预留，防止扣除时余额不足
* 每天会对前一天进行后付费结算

##### 获取订阅费用清单
```
GET http://whosecard.com:8081/api/wx/gzh/subscription/consume?key=***

query参数解释：
page: 页数，默认为0，每页最多返回100天的数据

请求成功会返回如下：
{
  "consume": [
    {
      "cost": 0.1,  # 当天订阅总费用
      "deducted": true, # 是否已从余额里扣除
      "dt": "20200425",  # 日期
      "gzhCount": 2,  # 当天订阅的公众号数量
      "unitPrice": 0.05  # 订阅单价
    }
  ],
  "cost": true,
  "count": 1,
  "hasMore": false,
  "ok": true,
  "retCode": 0
}
```

##### 当有新文章时的推送方式
```
POST 链接为用户提供的回调接口

回调接口传的时json格式数据，如下：
[
  {
    "biz" : "MzI3NTQxOTA5NA==",
    "nickname" : "说江苏",
    "alias" : "JS71038",
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

⚠️注意：本接口在调用时，只要response code为200，则认为推送成功，否则按一定间隔进行三次重试。
```

##### 拉取自己订阅的发文列表
```
GET http://whosecard.com:8081/api/wx/gzh/subscription/pull?key=***

每次拉取最多获取100篇文章，按文章入库倒序返回，如果需要翻页，请传递上一页返回的cursor参数
可传biz参数获取指定公众号的发文列表，多个公众号用半角逗号分隔，一次最多指定50个

返回数据如下：
{
  "articles": [
    {
      "biz" : "MzI3NTQxOTA5NA==",
      "nickname" : "说江苏",
      "alias" : "JS71038",
      "mid" : 2247496752,
      "idx" : 6,
      "url" : "http://mp.weixin.qq.com/s?__biz=MzI3NTQxOTA5NA==&mid=2247496752&idx=6&sn=ce24182b39feb7764ea52a06335d6674&scene=0",
      "time" : 1583807728,
      "title" : "小品《四大才子》，乐坏了",
      "content" : "",
      "cover" : "http://mmbiz.qpic.cn/mmbiz_jpg/IRFXibKRUAQsDppLSQx3icI7AuCfGXFfRrGLDPEoAqdEQVNKiagakC1BcpzJWTC1vNnEz6lib8pLYLCickyJFIibcdDA/0?wx_fmt=jpeg"
    }
  ],
  "cost": true,
  "count": 1,
  "cursor": "5e6714290b6ecd4a8b1b4d0a",
  "hasMore": false,
  "ok": true
}
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
