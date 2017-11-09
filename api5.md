#获取搜狗 公众号/关键字 最近N天内的更新文章接口

url请求需带上参数key，每个用户有唯一的key。

所有接口均返回json格式，其中参数ok[true|false]表示是否请求成功.


```
接口均为GET method。

按公众号搜索： account参数为公众号账号
http://whosecard.com:8081/api/sogou/weixin2?account=***&start=***&key=***

如果抓取成功，会返回如下格式数据：
{
  'ok': true,
  'ts': 1506064145,  # 最近的文章更新时间
  'essay_dict': {
    '1506064145': [  # 按照文章更新时间聚合
      {
        'title': '从拉勾融资 1.2 亿美元说起',
        'url': 'http://mp.weixin.qq.com/s?src=11&timestamp=1506614970&ver=420&signature=xeuWyonubGMlQavMuWO9-frQy47MPgVTHaVXPQ*8z7kMu5Ue7yxTh5*A*GZZ8zi1vpp2xfX9XZVrmYtn3Uhef-q2MWBZutrIl5C*r60gfvEEzaHarU6Vl2-iHUTLRnsw&new=1',
        'ts': 1506064145
      }
    ]
  },
  'count': 1  # 总文章数量
}

按关键字搜索： keywordstr为搜索关键字
http://whosecard.com:8081/api/sogou/weixin2?keywordstr=***&start=***&key=***

如果抓取成功，会返回如下格式数据：
{
  'ok': true,
  'count': 2,
  'essayList': [
    {
      'title': '今天',
      'url': 'http://mp.weixin.qq.com/s?src=11&timestamp=1510221953&ver=504&signature=IpmkSEsJP1JilaZbfFVd7IRwT3-CLEYv7ZlLx0dl3r7Zh6mh8PAfqn7zK8KUm2hmgrs5t1dLpXM0Ul-dY9-vJynCUkHyazxDcgWqa-FcWky6M7-xMSZx4eTYGqXld0Jm&new=1',
      'ts': 1510152533
    },
    {
      'title': '今天',
      'url': 'http://mp.weixin.qq.com/s?src=11&timestamp=1510221953&ver=504&signature=nfUCrv6opADDKtIrDwVO6fpEKIUlPpsFRV-*4yPlXFi9vULbOjPHlnyWfWiFevEyYUMS8-mUwsgW4eQWgXnDhswLtdfSNtZtv6mgiwQhjKRfvbGFO3zUv-HFfSa1M4KA&new=1',
      'ts': 1510204267
    }
  ]
}

start参数为要获取最近多少天的文章，如果是最近三天，则start=3
注意，start的取值范围为  7 >= start >= 1，即可抓取最多一周以内的更新文章。
start默认值为1，即一天内的更新文章。
```