# 公众号文章内容

#### 接口说明
* 账号注册请联系qq:1628121385，添加好友时请注明:wxapi
* url请求需带上参数key，每个用户有唯一的key。
* 所有接口均返回json格式，其中参数ok[true|false]表示是否请求成功.
* retCode为返回码，详情参考[返回码说明](https://github.com/iwoods100/wxapi-doc/blob/master/retcode.md)
* 当返回ok=false时，可以参考返回的error字段（如果存在的话）
* 一般来说，接口只要返回cost=true，就表示请求有效，会进行收费，此时请不要再重试了，这种情况一般是请求资源已经失效。

```
http://whosecard.com:8081/api/wx/article?url=***&key=***

eg:
http://whosecard.com:8081/api/wx/article?url=https://mp.weixin.qq.com/s/MHMyuGzdz2ZsFwczjR_T9g&key=***

⚠️url参数需要进行urlencode

返回如下：
{
	"ok": true,
	"result": {***}
 }

默认返回的是json化之后的文章数据，如果只想要原始html页面，可带上参数needJson=0
```
