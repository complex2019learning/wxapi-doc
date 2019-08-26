# api

所有接口均返回json格式，其中参数ok[true|false]表示是否请求成功，当ok=false时，会返回对应的error字段.

所有接口只要返回ok=true或者cost=true（cost字段不一定返回，不返回的话默认为false），就表示请求有效，会进行收费。

### 相关接口及收费价格如下：[费用查询接口](https://dev.tencent.com/u/iwoods/p/wxapi-doc/git/blob/master/pay.md)

#### 从微信app侧获取公众号历史页，[接口文档](https://dev.tencent.com/u/iwoods/p/wxapi-doc/git/blob/master/api-profile.md)

#### 文章临时链接转永久链接／短链接转长链接，[接口文档](https://dev.tencent.com/u/iwoods/p/wxapi-doc/git/blob/master/api2.md)

#### 获取公众账号信息，如根据account获取账号信息，[接口文档](https://dev.tencent.com/u/iwoods/p/wxapi-doc/git/blob/master/api3.md)

#### 实时获取文章评论/阅读点赞数，[接口文档](https://dev.tencent.com/u/iwoods/p/wxapi-doc/git/blob/master/api4.md)

#### 实时获取文章内容信息，[接口文档](https://dev.tencent.com/u/iwoods/p/wxapi-doc/git/blob/master/wxarticle.md)

#### 获取搜狗公众号/关键字最近N天内的更新文章，[接口文档](https://dev.tencent.com/u/iwoods/p/wxapi-doc/git/blob/master/api5.md)
```
最近N天的范围是：7 >= N >= 1
单次调用计费跟返回的文章数量有关：
文章数量／10，再向上取整，最后乘以0.1，比如返回53篇文章，将收取0.6元。
文章链接均为临时链接。

本接口只要抓取成功，即时没有更新任何文章，也要收取0.1。
```

#### 微信指数，[接口文档](https://dev.tencent.com/u/iwoods/p/wxapi-doc/git/blob/master/wxindex.md)

#### 抖音相关接口，[接口文档](https://dev.tencent.com/u/iwoods/p/wxapi-doc/git/blob/master/douyin.md)

#### 小红书相关接口，[接口文档](https://dev.tencent.com/u/iwoods/p/wxapi-doc/git/blob/master/xiaohongshu.md)

#### 快手相关接口，[接口文档](https://dev.tencent.com/u/iwoods/p/wxapi-doc/git/blob/master/kuaishou.md)

#### b站相关接口，[接口文档](https://dev.tencent.com/u/iwoods/p/wxapi-doc/git/blob/master/bilibili.md)

#### 知乎相关接口，[接口文档](https://dev.tencent.com/u/iwoods/p/wxapi-doc/git/blob/master/zhihu.md)

#### 头条相关接口，[接口文档](https://dev.tencent.com/u/iwoods/p/wxapi-doc/git/blob/master/toutiao.md)

///////////////////////////////////////////////////////////

所有接口均可先免费试用，满意后再付费使用。

如有其它接口需求，可定制开发。

#### 联系QQ：1628121385，添加好友时请注明：wxapi
