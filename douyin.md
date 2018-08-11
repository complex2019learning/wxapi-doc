#实时抖音接口

url请求需带上参数key，每个用户有唯一的key。

所有接口均返回json格式，其中参数ok[true|false]表示是否请求成功.

####1. 实时获取抖音视频detail信息（不包含播放量）
```
http://whosecard.com:8081/api/douyin/aweme/detail?key=***&aweme_id=6580087189395213581

返回如下：
{
  "ok": true,
  "result": {
    "statistics": {
        "forward_count": 0,
        "digg_count": 1,  # 有效点赞数
        "play_count": 0,  # 此字段目前不返回真实数据
        "comment_count": 0,  # 有效评论数
        "aweme_id": "6572756298830449927",
        "share_count": 0
      },
    ... # 其它字段按字面意思理解
  }
}

result包含了抖音返回的所有字段数据，除了statistics字段外还会返回其它字段，按照字面意思理解即可。

划重点：请传入有效的aweme_id
```
