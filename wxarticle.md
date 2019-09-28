# 公众号文章内容

url请求需带上参数key，每个用户有唯一的key。

所有接口均返回json格式，其中参数ok[true|false]表示是否请求成功.

```
http://whosecard.com:8081/api/wx/article?url=***&key=***

eg:
http://whosecard.com:8081/api/wx/article?url=https://mp.weixin.qq.com/s/MHMyuGzdz2ZsFwczjR_T9g&key=***

返回如下：
{
	"ok": true,
	"result": {***}
 }

 默认返回的是json化之后的文章数据，如果只想要原始html页面，可带上参数needJson=0
```
