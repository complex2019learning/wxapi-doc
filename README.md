# wxapi

#### 相关接口及收费价格如下：[费用查询接口](https://dev.tencent.com/u/iwoods/p/wxapi-doc/git/blob/master/pay.md)

##### 公众号即时更新接口， [接口文档](https://dev.tencent.com/u/iwoods/p/wxapi-doc/git/blob/master/api1.md)

```
接口描述：

仅支持搜狗能搜到的订阅号，当公众号更新图文消息时，半小时内通知客户。

目前支持两种通知方式：
1.主动回调客户提供的接口
2.客户主动调用接口查询最近有更新的公众号列表

建议使用第一种方式，第二种可作为辅助使用。

⚠️须知：
本服务只针对能在搜狗搜到的公众号，对于现在或将来搜不到的公众号，无法提供服务。
公众号延时偶尔超过半小时属于正常现象，因为搜狗同步本身也不是实时的。
因为此接口是从搜狗抓取，所以对于更新的文章列表，允许1%的文章丢失率，但不影响回调本身，且在更新触发后，会优先调用app的历史页接口，因此漏文章的概率算是很低了。

如果担心搜狗不够稳定，建议结合公众号历史页接口，每隔一段时间单独对所有号查询一次历史页，具体间隔由自身场景需求决定。

如果无法接受以上须知，请不要使用这个服务！！！
```

##### 从微信app侧获取公众号历史页，[接口文档](https://dev.tencent.com/u/iwoods/p/wxapi-doc/git/blob/master/api-profile.md)

##### 文章临时链接转永久链接／短链接转长链接，[接口文档](https://dev.tencent.com/u/iwoods/p/wxapi-doc/git/blob/master/api2.md)

##### 获取公众账号信息，如根据account获取账号信息，[接口文档](https://dev.tencent.com/u/iwoods/p/wxapi-doc/git/blob/master/api3.md)

##### 实时获取文章评论/阅读点赞数，[接口文档](https://dev.tencent.com/u/iwoods/p/wxapi-doc/git/blob/master/api4.md)

##### 获取搜狗公众号/关键字最近N天内的更新文章，[接口文档](https://dev.tencent.com/u/iwoods/p/wxapi-doc/git/blob/master/api5.md)
```
最近N天的范围是：7 >= N >= 1
单次调用计费跟返回的文章数量有关：
文章数量／10，再向上取整，最后乘以0.1，比如返回53篇文章，将收取0.6元。
文章链接均为临时链接。

本接口只要抓取成功，即时没有更新任何文章，也要收取0.1。
```

##### 微信指数，[接口文档](https://dev.tencent.com/u/iwoods/p/wxapi-doc/git/blob/master/wxindex.md)

##### 抖音相关接口，[接口文档](https://dev.tencent.com/u/iwoods/p/wxapi-doc/git/blob/master/douyin.md)

##### 小红书相关接口，[接口文档](https://dev.tencent.com/u/iwoods/p/wxapi-doc/git/blob/master/xiaohongshu.md)

///////////////////////////////////////////////////////////

所有接口均可先免费试用，满意后再付费使用。

如有其它接口需求，可定制开发。

#### 联系QQ：1628121385，添加好友时请注明：wxapi
