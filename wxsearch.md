# 搜索指定关键词的文章列表

url请求需带上参数key，每个用户有唯一的key。

所有接口均返回json格式，其中参数ok[true|false]表示是否请求成功.

⚠️正式使用前可试用免费体验版[微信文章搜索工具](https://whosecard.com/wx/article/search)

⚠️如需加入指定公众号，可提交biz列表给作者。

```
http://whosecard.com:8081/api/wx/article/search?keyword=***&start=0&key=***

query参数解释：
keyword: 搜索关键词，多个关键词可用空格分开（不分开也可以，会自动分词）
accountId: 公众号ID，限定在此公众号下进行搜索，如: rmrbwx
accountName: 公众号名称，限定在此公众号下进行搜索，如: 人民日报
start: 文章偏移量，初始值为0，若需翻页，可使用返回结果的nextStart
startDate: 指定搜索时间的起始日期，搜索时会包含此日期，格式如： 2019-10-01
endDate: 指定搜索时间的截止日期（如若不填则默认截止到今天），搜索时会包含此日期，格式如： 2019-12-01
sort: 排序，目前支持三种排序，分别为：0(默认排序), 1(按发布时间倒序，最新发布的排在前面), 2(按发布时间增序，最早发布的排在前面)，默认为0
summary: 如果传1，则title,content,accountId,accountName这几个字段会将匹配到的关键词用<em>标签包裹，一般用户搜索高亮显示，默认不开启

keyword，accountId，accountName三个参数必须填一个。其中accountId，accountName参数之中只能填一个，如果填了accountId或者accountName且没有填keyword，则会返回该公众号下的所有收录文章。
当startDate与endDate不传时，表示不限制搜索时间。

此接口每次返回最多10篇文章。只要成功，不管是否有文章，都按照成功收费（比如搜了不存在的关键词）

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
