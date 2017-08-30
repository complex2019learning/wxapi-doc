#实时获取公众号阅读点赞接口

url请求需带上参数key，每个用户有唯一的key。

所有接口均返回json格式，其中参数ok[true|false]表示是否请求成功.

####实时获取公众号文章阅读点赞数据
```
http://whosecard.com:8081/api/msg/ext?url=***&key=***

参数中的url为urlencode后的永久链接
eg:
http://whosecard.com:8081/api/msg/ext?url=https%3a%2f%2fmp.weixin.qq.com%2fs%3f__biz%3dMjM5MzI5NTU3MQ%3d%3d%26mid%3d2651456339%26idx%3d1%26sn%3db28ead72f72decc7993d2db6a4a7f437%26scene%3d0%23wechat_redirect&key=***

返回如下：
{"ok": true, "clicksCount": 56602, "likeCount": 196, "advertisementNum": 1}

advertisementNum为该文章的附带广告数量，仅开通广点通的公众号才有。
```
