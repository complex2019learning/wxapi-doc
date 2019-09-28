# 公众号账号信息接口

url请求需带上参数key，每个用户有唯一的key。

所有接口均返回json格式，其中参数ok[true|false]表示是否请求成功.

#### 获取公众号账号信息
```
http://whosecard.com:8081/api/account/info?account=webnotes&key=***

返回格式如下：
{
	name: "小道消息",
	account: "WebNotes",
	description: "在这里，我想为你呈现一幅中国互联网的清明上河图。",
	uuid: "C1080392D32744FD45596A58F74C7D84",  # 微信公众号内部id，一般用不上
	tags: [  # 公众号标签，仅供参考
		"自媒体人",
		"TMT个人"
	],
	maxReleaseTimes: "2",  # 每天发布文章次数上限
	indexUrl: "http://wx.qlogo.cn/mmhead/Q3auHgzwzM4EOYw3p9pQDznBzXPxFSx5xwQk6LWKAkbhPhHNQNgsCw/0",
	__biz: "MjM5ODIyMTE0MA==",
	certifiedText: "微信认证：Fenng; 冯大辉,丁香园技术产品负责人.",
	accountType: "0",  # "0"为订阅号，"1"为服务号
	ok: true
}
```
