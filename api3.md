# 公众号账号信息接口

url请求需带上参数key，每个用户有唯一的key。

所有接口均返回json格式，其中参数ok[true|false]表示是否请求成功.

所有接口只要返回cost=true，就表示请求有效，会进行收费。当cost=true时，即使请求失败，也不要再重试了，这种情况一般是请求资源已经失效。

#### 获取公众号账号信息
```
http://whosecard.com:8081/api/account/info?account=webnotes&key=***

返回格式如下：
{
	name: "小道消息",
	account: "WebNotes",
	description: "在这里，我想为你呈现一幅中国互联网的清明上河图。",
	indexUrl: "http://wx.qlogo.cn/mmhead/Q3auHgzwzM4EOYw3p9pQDznBzXPxFSx5xwQk6LWKAkbhPhHNQNgsCw/0",
	__biz: "MjM5ODIyMTE0MA==",
	certifiedText: "微信认证：Fenng; 冯大辉,丁香园技术产品负责人.",
	accountType: "0",  # "0"为订阅号，"1"为服务号
	ok: true
}
```
