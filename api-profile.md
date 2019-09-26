#实时获取公众号历史发文页面

url请求需带上参数key，每个用户有唯一的key。

所有接口均返回json格式，其中参数ok[true|false]表示是否请求成功.

⚠️微信公众号的历史文章，根据发文顺序，越新的文章，链接里的mid参数越大，同一时间发布的文章链接里具有相同的mid参数，但idx不同，idx=1时是头条文章，以此类推。

⚠️由于公众号发布的文章时间字段不一定全局统一，比如搜狗和app里统计的发文时间就是不一样的，所以不建议使用时间作为判断是否有新增文章的依据，为了100%保证文章发布顺序，请使用mid进行判断。

## 请使用此接口

```
http://whosecard.com:8081/api/wx/articles?biz=***&key=***

eg:
http://whosecard.com:8081/api/wx/articles?biz=MjM5ODIyMTE0MA==&key=***

返回如下：
{
    "ok": true,
    "articles": [
        {
            "content": "欢迎点击上方的“华尔街日报中文网”关注我们1月24日，百度在北京首都体育馆举办年会，公司创始人李彦宏身披“黄",
            "cover": "http://mmbiz.qpic.cn/mmbiz/IMSWclibDr4T4gcX6FzS6RiaeHy135yylRsU9kCYibabkWcLgibJa6HqHDAptmZuO0icc1uRk0tAQiciaTVsUEicWmFw3w/0",
            "time": 1423215709, # ⚠️此处为文章创建时间，不等于文章发布时间，如果要获取发布时间，可参考【文章详情接口】
            "title": "专栏 | 中国互联网年会盛筵说明什么？",
            "url": "https://mp.weixin.qq.com/s?__biz=MTYzMjQ3NTYwMQ==&mid=204045670&idx=1&sn=8e6b09e428cdfcecfa018382d04e6647#rd"
        },
        ...
    ]
}
 
 默认最多返回最近十次发文（⚠️不是十篇也不是十天，是十次）

 如果需要翻页，需要带上offset参数，如offset=10，则返回从第11次开始的10次文章，此参数与微信接口的offset参数含义一致。

如果是接口本身导致的失败则不会扣费，建议请求失败时设置最大重试次数。
```

## 此接口即将下线，请新用户不要使用，老用户尽快迁移到新接口
```
http://whosecard.com:8081/api/wx/profile?biz=***&key=***

eg:
http://whosecard.com:8081/api/wx/profile?biz=MjM5ODIyMTE0MA==&key=***

返回如下：
{
	"ok": true,
	"html": "历史列表页html文本"
 }

 默认最多返回最近十次发文（⚠️不是十篇也不是十天，是十次）

 如果需要翻页，需要带上offset参数，如offset=10，则返回从第11次开始的10次文章，此参数与微信接口的offset参数含义一致。

⚠️注意，如果是公众号自身的问题导致失败，依旧会扣费，并在error字段返回失败原因，同时会返回cost字段为true，如下：
{'ok': false, 'error': '此帐号已申请公众号帐号迁移流程，被冻结/回收，小主页暂无法访问。', 'cost': true}
{'ok': false, 'error': '此帐号已自主注销，内容无法查看。', 'cost': true}
{'ok': false, 'error': '经大量用户投诉，此帐号存在违规行为，已限制跳转到小主页。', 'cost': true}
# 之后可能会扩展更多公众号异常场景，建议使用cost字段判断是否需要重试

如果收到cost=true的失败返回结果，就不用再重试请求了。
如果是接口本身导致的失败则不会扣费，建议请求失败时设置最大重试次数。
```