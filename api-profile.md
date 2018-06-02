#实时获取公众号历史发文页面

url请求需带上参数key，每个用户有唯一的key。

所有接口均返回json格式，其中参数ok[true|false]表示是否请求成功.

```
http://lapi.whosecard.com:8081/api/wx/profile?biz=***&key=***

eg:
http://lapi.whosecard.com:8081/api/wx/profile?biz=MjM5ODIyMTE0MA==&key=***

返回如下：
{
	"ok": true,
	"html": "历史列表页html文本"
 }
 
 默认最多返回最近十次发文（⚠️不是十篇也不是十天，是十次）
 
 如果需要翻页，需要带上offset参数，如offset=10，则返回从第11次开始的10次文章，此参数与微信接口的offset参数含义一致。

```