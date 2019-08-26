#公众号链接转换接口

url请求需带上参数key，每个用户有唯一的key。

所有接口均返回json格式，其中参数ok[true|false]表示是否请求成功.

####公众号文章临时链接转为永久链接
```
http://whosecard.com:8081/api/url/transfer/tmp2forever?url=***&key=***

参数中的url为urlencode后的临时链接（从搜狗获取的文章链接）
eg:
http://whosecard.com:8081/api/url/transfer/tmp2forever?account=heromoba&url=https%3a%2f%2fmp.weixin.qq.com%2fs%3ftimestamp%3d1499228713%26signature%3d%252ABryvh1ys7%252Aw7NILRK8LfHt4ud1tqhEFCATivcmncThCG7G3CsgWG-Yef18Y1YhBDxhFiX-DhxNbOJhMMkmWeSNT5A4W6cGua1X8V3-BybK4eV7Lkb7OIXjrf1ct3v3gf3colF%252A8zdJ1k61J-tGFKABYiJNuNmyBjguKrA7CLvg%253D%26src%3d3%26ver%3d1&key=***

注意⚠️：
临时链接最好在失效之前转换，否则具有不稳定因素！
如果真的失效了，则必须在参数中加上biz或者account才能转换(两者至少传一个，否则无法转换)，优先传biz参数，使用account具有一定转换失败的风险， 如下：
http://whosecard.com:8081/api/url/transfer/tmp2forever?url=***&key=***&biz=***&account=***

请求成功时，返回如下结果：
{
  "ok": true,
  "src_url": "https://mp.weixin.qq.com/s?timestamp=1561708379&src=3&ver=1&signature=wYdQBBbMHKOR68DIFHz*qKPOeQCaIBHC80MM8pzcvy96NapCddwKvSMGSN4jTHlUQDIo8ziQ7s52eDvC-1p*Q*qEueAtJyrkypYIa7REs87ywnhquvMXeOcYM*Gt8nixDIfCn55GmwMND90PFAZ5nIg40NtrpRlkOefqPO3NO3Q=",  # 请求的临时链接
  "url": "http://mp.weixin.qq.com/s?__biz=MTg0MzMwODA0MQ==&mid=2653363568&idx=1&sn=349edab2dc39924bab466b2d7a1afda9&scene=0#wechat_redirect"  # 转换成功的永久链接
}

划重点：如果给的链接是无效的，则会返回：
{"ok": false, "error": "check_url error", "cost": true}
此时会正常收费，所以不要再重复提交此无效链接！

其它可能返回的error response:
{"ok": false, "error": "request error"}  # 请求过程出错，可重试
{"ok": false, "error": "invalid wxkey."}  #  请求过程出错，可重试
{'ok': false, 'error': 'get biz failed.'}  # biz获取失败，请检查后重试
{'ok': false, 'error': 'url is not correct.'}  # url不是临时链接，不要重试
{'ok': false, 'error': 'request too fast.'}  # 请求太快，请放慢频率
```

####公众号文章短链接转为长链接
```
http://whosecard.com:8081/api/url/transfer/short2long?url=***&key=***

参数中的url为urlencode后的短链接
eg:
http://whosecard.com:8081/api/url/transfer/short2long?url=https%3a%2f%2fmp.weixin.qq.com%2fs%2fAuyufPtU1UeusDS6B34VZg&key=***

请求成功返回如下：
{
  "ok": true,
  "url": "http://mp.weixin.qq.com/s?__biz=MTQzMjE1NjQwMQ==&mid=2655540054&idx=1&sn=f8ded2092ae3882242a3c06ec9050778&chksm=66dffcc851a875de8200ba910dd0eb88718ce0ae4df625628a2c4ee271f96cd63c5e248bdce8#rd",
  "src_url": "https://mp.weixin.qq.com/s/AuyufPtU1UeusDS6B34VZg"
}
```


####公众号文章长链接转为短链接
```
http://whosecard.com:8081/api/url/transfer/long2short?url=***&key=***

参数中的url为urlencode后的长链接
eg:
http://whosecard.com:8081/api/url/transfer/long2short?url=https%3a%2f%2fmp.weixin.qq.com%2fs%3f__biz%3dMjM5MzI5NTU3MQ%3d%3d%26mid%3d2651456339%26idx%3d1%26sn%3db28ead72f72decc7993d2db6a4a7f437%26scene%3d0%23wechat_redirect&key=***

请求成功返回如下：
{
  "ok": true,
  "src_url": "https://mp.weixin.qq.com/s?__biz=MjM5MzI5NTU3MQ==&mid=2651456339&idx=1&sn=b28ead72f72decc7993d2db6a4a7f437&scene=0#wechat_redirect",
  "url": "https://mp.weixin.qq.com/s/FRaR_KtuKr7GKdyuZF2B4g"
}
```