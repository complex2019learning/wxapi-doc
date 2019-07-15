# 支付方式

⚠️充值费用请在12个月内使用完，过期作废。

```
对于按次数计费的接口，正式使用前要先充值，余额会根据接口调用次数动态更新，余额不足时需及时充值。

余额查询接口：
http://user.whosecard.com:8081/api/user/info?key=***

response:
{
	ok: true,
	balance: 100  # 单位元
}

获取某日的接口调用详情：
http://user.whosecard.com:8081/api/user/consumeDetail?key=***&dt=20181026

想要查询指定日期的消费详情，只需传对于的dt参数即可，格式为: %Y%m%d, 如20181026

response:
{
	ok: true,
	consumeDetail: {}  # 各接口消费详情
}
```
