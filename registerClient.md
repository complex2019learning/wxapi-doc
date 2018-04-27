# 微信注册-好友辅助

### 注册方上传辅助链接

辅助二维码可以转换为链接，格式如： https://weixin110.qq.com/s/ebe711c8db3

url请求需带上参数key，每个用户有唯一的key。

接口返回json格式，其中参数ok[true|false]表示是否请求成功.


```
接口为GET method。

number为电话号码，verifyUrl参数为辅助链接
http://120.79.10.233:8081/api/wx/register/verify/upload?key=***&number=17021394832&verifyUrl=https://weixin110.qq.com/s/ebe711c8db3

如果上传成功，会返回如下格式数据：
{'ok': true}
反之：
{'ok': false}
```

### 注册方结束后提交状态

```
接口为GET method。

verifyUrl参数为辅助链接, 在获取任务的时候得到的
success=1表示辅助成功，将扣费，如果success=0表示失败，不扣费
http://120.79.10.233:8081/api/wx/register/verify/done?key=***&success=1&verifyUrl=https://weixin110.qq.com/s/ebe711c8db3

对于辅助失败的记录，会逐一进行审核，已确认确实是失败了。

如果请求成功，会返回如下格式数据：
{'ok': true}
反之：
{'ok': false}
```
