# 自建公众号内容库相关接口

#### 本内容库收录了200w+公众号，对主流公众号发文提供近实时更新入库，平均日文章量在150w+篇左右

url请求需带上参数key，每个用户有唯一的key。

所有接口均返回json格式，其中参数ok[true|false]表示是否请求成功.

⚠️正式使用前可试用免费体验版[微信文章搜索工具](https://whosecard.com/wx/article/search)

⚠️如需加入指定公众号，可提交biz列表给作者。

### 批量查询公众号是否被收录

```
GET http://whosecard.com:8081/api/wx/gzh/includeStatus?biz=***&key=***

query参数解释：
biz: 公众号biz，如: MjM5MjAxNDM4MA==，指定多个公众号时，用半角逗号,分隔，单次最多查询100个

请求成功会返回如下：
{
  "cost": true,
  "ok": true,
  "result": {
    "MjM5MDE0Mjc4MA==": {
      "include": true,  # 是否被收录
      "invalid": false,  # 公众号是否已失效，比如被封，已转移等
      "invalidReason": null  # 公众号失效原因
    },
    "MjM5ODIyMTE0MA==": {
      "include": true,
      "invalid": false,
      "invalidReason": null
    }
  }
}

请求成功会返回如下：
{
  "cost": false,
  "ok": false,
  "error": "****"
}
```

### 搜索指定关键词的文章列表(可指定公众号范围)

```
GET http://whosecard.com:8081/api/wx/article/search?keyword=***&start=0&key=***

query参数解释：
keyword: 搜索关键词，多个关键词可用空格分开（不分开也可以，会自动分词）
biz: 公众号biz，限定在此公众号下进行搜索，如: MjM5MjAxNDM4MA==，指定多个公众号时，用半角逗号,分隔
accountId: 公众号ID，限定在此公众号下进行搜索，如: rmrbwx，指定多个公众号时，用半角逗号,分隔
accountName: 公众号名称，限定在此公众号下进行搜索，如: 人民日报，指定多个公众号时，用半角逗号,分隔
start: 文章偏移量，初始值为0，若需翻页，可使用返回结果的nextStart
startDate: 指定搜索时间的起始日期，搜索时会包含此日期，格式如： 2019-10-01
endDate: 指定搜索时间的截止日期（如若不填则默认截止到今天），搜索时会包含此日期，格式如： 2019-12-01
startTime: 指定搜索时间的起始时间戳（单位为秒）
endTime: 指定搜索时间的截止时间戳（如若不填则默认截止到当前时间戳）（单位为秒）
sort: 排序，目前支持三种排序，分别为：0(默认排序), 1(按发布时间倒序，最新发布的排在前面), 2(按发布时间增序，最早发布的排在前面)，默认为0
summary: 如果传1，则title,content会将匹配到的关键词用<em>标签包裹，一般用户搜索高亮显示，默认不开启
searchRange: 如果传1，则只对标题进行搜索。默认为0，即标题+正文搜素
searchPos: 如果传1，则只返回头条。默认为0，即不限制文章发布位置
fullMatch: 如果传1，则必须完整包含搜索词，不会进行分词处理。默认为0，即会进行适当的分词处理后再搜索
copyrightStat: 如果传1，则只返回原创文章。如果传2，则只返回转载文章。默认为0，即返回所有

keyword，biz，accountId，accountName这几个参数必须填一个。其中biz，accountId，accountName参数同一时间只能有一个生效，如果填了biz或accountId或accountName且没有填keyword，则会返回该公众号下的所有收录文章。

⚠️有时候会发现按时间排序返回的搜索结果不是最新的，那是因为命中的候选文档太多时(超过100w条)，导致最新的反而没有进入搜索候选池，这种情况下需要限制一下过滤条件，比如指定时间范围

⚠️本接口支持指定一批公众号范围内进行搜索，多个账号用逗号分隔即可，同一次请求最多指定40个公众号。

startDate/endDate与startTime/endTime都是限定时间范围的参数，所以同一时间最多只需要传其中一组，当不传时，表示不限制搜索时间。

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
