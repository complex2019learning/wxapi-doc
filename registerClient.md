# 微信注册-好友辅助

### 上传辅助链接

辅助二维码可以转换为链接，格式如： https://weixin110.qq.com/s/ebe711c8db3

url请求需带上参数key，每个用户有唯一的key。

接口返回json格式，其中参数ok[true|false]表示是否请求成功.


```
接口为GET method。

verifyUrl参数为辅助链接
http://user.whosecard.com:8081/api/wx/register/verify/upload?key=***&verifyUrl=https%3a%2f%2fweixin110.qq.com%2fs%2febe711c8db3

如果上传成功，会返回如下格式数据：
{'ok': true}
反之：
{'ok': false}
```


