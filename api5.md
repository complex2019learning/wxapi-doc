# 获取搜狗 公众号/关键字 最近N天内的更新文章接口

#### 接口说明
* url请求需带上参数key，每个用户有唯一的key。
* 所有接口均返回json格式，其中参数ok[true|false]表示是否请求成功.
* retCode为返回码，详情参考[返回码说明](https://iwoods.coding.net/p/wxapi-doc/d/wxapi-doc/git/blob/master/retcode.md)
* 当返回ok=false时，可以参考返回的error字段（如果存在的话）
* 一般来说，接口只要返回cost=true，就表示请求有效，会进行收费，此时请不要再重试了，这种情况一般是请求资源已经失效。

```
接口均为GET method。

按公众号搜索： account参数为公众号账号
http://user.whosecard.com:8081/api/sogou/weixin2?account=***&start=***&key=***

如果抓取成功，会返回如下格式数据：
{
  'ok': true,
  'ts': 1518339614,  # 最近的文章更新时间
  'essay_dict': {
    '1518250915': [  # 按照文章更新时间聚合
      {
        'title': '重磅!金正恩给文在寅写了一封亲笔信',
        'url': 'http://mp.weixin.qq.com/s?src=11&timestamp=1518356594&ver=692&signature=cEA8Vk0zgwwbctG8TBXG5QoRQW*GG42p6Adme55pehpk9QuS6KOn8QzY2o6e49OZJfArY-JP6FzHj3BaQvI635jhl2b3qhtsWlFZoI6GTGk3rE71MWmebZ6sNqq-nonK&new=1',
        'summary': '“导游抢了我的救生衣,第一个跳海!”泰国快艇爆炸,25名中国游客的黑色10分钟 澎湃新闻 thepapernews',
        'accountName': '澎湃新闻',
        'ts': 1518250915
      }
    ]
  },
  'count': 1  # 总文章数量
}

按关键字搜索： keywordstr为搜索关键字
http://user.whosecard.com:8081/api/sogou/weixin2?keywordstr=***&start=***&key=***

如果抓取成功，会返回如下格式数据：
{
  'ok': true,
  'count': 2,
  'essayList': [
    {
      'title': '月亮',
      'url': 'http://mp.weixin.qq.com/s?src=11&timestamp=1518356352&ver=692&signature=ux5B9a03ULxgQMzYn8uTDywiOhqAxA9NZFSdHm3XcuDBjjXKBfmPiTZyjTEvszR5o4-g7AAfxHGDvLI2TDtqIe-mJ8SJcY4ffcBmOdzYaa*Q5IYyAnfD6f5plv2onrcF&new=1',
      'summary': '小朋友们、同学们, 前几天,你有被网络上被这条消息刷屏了:“红月亮”伴随“月全食”现身天宇.月全食+超级月亮+蓝月亮将组...',
      'accountName': '梅朵',
      'ts': 1518353188
    },
    {
      'title': '2018年重要时政汇编(五)',
      'url': 'http://mp.weixin.qq.com/s?src=11&timestamp=1518356352&ver=692&signature=Tp*8SIGsNjEB1ib3ap4aMa1fpe*wBRozVyPkFRad6gJ2OsB5jQ9LCDIGOPIB3BIfPgk3ifmEWJkc5p*Kn1w1CE34wWp6kWdCCxYW2kk2DzA21xXqyTT7pcvCYgeP8gHA&new=1',
      'summary': '公众将可以欣赏到“蓝月亮”天文景观｡巧合的是,当晚有月全食发生,一轮“红月亮”也将现身天宇添浪漫｡5. 中国“慧眼”正式开...',
      'accountName': '图图教师',
      'ts': 1518341144
    }
  ]
}

start参数为要获取最近多少天的文章，如果是最近三天，则start=3
注意，start的取值范围为  7 >= start >= 1，即可抓取最多一周以内的更新文章。
start默认值为1，即一天内的更新文章。

ps: 如果要抓7天前的文章，可以直接设置ft（起始日期）与et（终止日期）
比如 ft=2019-04-15   et=2019-04-18  （格式为%Y-%m-%d，ft不小于et，否则无效）
那么将抓取2019-04-15 - 2019-04-18之间的文章，由于一次请求最多获取10页数据，所以不要将时间间隔设置得过大，否则也只能取最多10页即100条文章，对于长时间范围的文章，可以按时间一段一段的抓。
```
