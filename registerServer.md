# 微信注册-好友辅助

### 辅助方获取一个任务

辅助二维码可以转换为链接，格式如： https://weixin110.qq.com/s/ebe711c8db3

url请求需带上参数key，每个用户有唯一的key。

接口返回json格式，其中参数ok[true|false]表示是否请求成功.


```
接口为GET method。

http://120.79.10.233:8081/api/wx/register/verify/fetch?key=***

如果上传成功，会返回如下格式数据：（verifyUrl参数为辅助链接）
{
	'ok': true,
	'verifyUrl': 'https://weixin110.qq.com/s/8011677271c',  # 辅助链接
	'expiredTS': 1524662283,  # 链接过期的时间戳，为上传时间+300秒
}
反之：
{'ok': false}

注意！为了防止重复派发，每个任务只会被获取一次，所以不要滥用此接口，尽量获取一次就完成一次！
```


