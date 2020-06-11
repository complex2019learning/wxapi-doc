# 公众号账号信息接口

#### 接口说明
* 账号注册请联系qq:1628121385，添加好友时请注明:wxapi
* url请求需带上参数key，每个用户有唯一的key。
* 所有接口均返回json格式，其中参数ok[true|false]表示是否请求成功.
* retCode为返回码，详情参考[返回码说明](https://iwoods.coding.net/p/wxapi-doc/d/wxapi-doc/git/blob/master/retcode.md)
* 当返回ok=false时，可以参考返回的error字段（如果存在的话）
* 一般来说，接口只要返回cost=true，就表示请求有效，会进行收费，此时请不要再重试了，这种情况一般是请求资源已经失效。

#### 获取公众号账号信息
```
http://whosecard.com:8081/api/account/info?account=webnotes&key=***

返回格式如下：
{
	"ok": true,
	"biz": "MjM5ODIyMTE0MA==",
	"name": "小道消息",
	"account": "WebNotes",
	"description": "在这里，我想为你呈现一幅中国互联网的清明上河图。",
	"indexUrl": "http://wx.qlogo.cn/mmhead/Q3auHgzwzM4EOYw3p9pQDznBzXPxFSx5xwQk6LWKAkbhPhHNQNgsCw/0",
	"tags": ["科技互联网"],  # 根据公众号原创/转载文章类型分析统计得出
	"principalName": "Fenng",  # 账号主体名称
	"principalType": "0",  # 账号主体类型: 0个人 1企业 2媒体 3政府
	"verifyStatus": "1",  # 账号认证类型: 0未认证 1个人认证 2组织认证
	"servicePhone": "",  # 电话号码
}
```

<!--
certifiedText: "微信认证：Fenng; 冯大辉,丁香园技术产品负责人.",
accountType: "0",  # "0"为订阅号，"1"为服务号
-->
