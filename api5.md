#获取搜狗公众号最近N天内的更新文章接口

url请求需带上参数key，每个用户有唯一的key。

所有接口均返回json格式，其中参数ok[true|false]表示是否请求成功.


```
此接口为GET method，。


http://whosecard.com:8081/api/sogou/weixin2?account=***&start=***&key=***

如果抓取成功，会返回如下格式数据：
{
  'ok': True,
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

account参数为公众号账号
start参数为要获取最近多少天的文章，如果是最近三天，则start=3
注意，start的取值范围为  7 >= start >= 1，即可抓取最多一周以内的更新文章。
start默认值为1，即一天内的更新文章。
```