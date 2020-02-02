# 搜索指定关键词的文章列表

url请求需带上参数key，每个用户有唯一的key。

所有接口均返回json格式，其中参数ok[true|false]表示是否请求成功.

```
⚠️本接口目前免费试用中，可直接调用不收费，试用阶段每个关键词最多返回前100篇文章。欢迎提供建议，如需加入指定公众号，可提交biz列表文章给作者。

⚠️试用阶段为体验目的，不建议大量调用依赖～

http://whosecard.com:8081/api/wx/search/article?keyword=***&start=0&count=10

start: 文章偏移量，初始值为0，若需翻页，可使用返回结果的nextStart
count: 每页返回文章篇数，最大20
startDate: 指定搜索时间的起始日期，搜索时会包含此日期，格式如： 2019-10-01
endDate: 指定搜索时间的截止日期（如若不填则默认截止到今天），搜索时会包含此日期，格式如： 2019-12-01

当startDate与endDate不传时，表示不限制搜索时间。

⚠️同一个关键词搜索通过翻页最多能返回5000篇文章，如果总条数大于5000，建议缩小搜索日期进行遍历

请求成功会返回如下：
{
  "cost": true,
  "ok": true,
  "result": {
    "count": 10, # 本次返回的文章篇数
    "hasMore": true,  # 是否还能翻页
    "nextStart": 10, # 翻下一页的start参数
    "total": 1755,  # 全局搜索结果条数，此值为总量，作为参考使用，实际能返回的文章量由viewTotal决定
    "viewTotal": 1755,  # 通过翻页可返回的结果条数，此值最大为5000（如果全局搜索结果大于5000且需要获取全部文章，建议缩小搜索的日期范围）
    "items": [  # 文章列表
      {
        "accountId": "bukeqi168",  # 公众号id
        "accountName": "韩国彩色生活",  # 公众号昵称
        "content": "",  # 摘要
        "cover": "http://mmbiz.qpic.cn/mmbiz_jpg/51twpDgEQX7zrSLtHe1UhetAibnvDUppO5hkSwTIian3raIDDia9wGpuNRzPuSjf1lUHDFhk8YONceWE2QQJAeQeQ/0?wx_fmt=jpeg",
        "publishedDate": "2020-01-25",  # 文章发布日期
        "time": 1579957200,  # 文章发布时间戳
        "title": "LV、CHANEL大牌围巾|1月欧洲免税店最新报价",
        "url": "http://mp.weixin.qq.com/s?__biz=MzA4NzIyMzE5OA==&mid=2655280239&idx=1&sn=92b406417c90253c155fb37fae11f358&chksm=8b8c429ebcfbcb88f60cead5d9f18860d994ace660d96c49afb5cd6bb23a1b9b314acf2efcba#rd"
      }
      ...
    ]
  }
}

请求成功会返回如下：
{
  "cost": false,
  "ok": false,
  "error": "****"
}
```
