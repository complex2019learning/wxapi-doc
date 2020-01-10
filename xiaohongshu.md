# 小红书接口

url请求需带上参数key，每个用户有唯一的key。

所有接口均返回json格式，其中参数ok[true|false]表示是否请求成功.


#### 获取单个笔记详细数据
```
http://whosecard.com:8081/api/xiaohongshu/note/detail?note_id=***&key=***

返回如下：
{
  "ok": true,
  "result": {
    ... # 返回值与小红书接口一样，字段比较多，按字面意思理解即可
  }
}

当作品不存在时，则返回如下：
{
  "cost": true,
  "error": "作品不存在",
  "ok": false
}
```

#### 获取笔记的评论列表
```
http://whosecard.com:8081/api/xiaohongshu/note/comments?note_id=***&key=***

每页返回20条。
如果要翻页，需要传入cursor参数（会在前一次请求结果里返回），第一次请求不需要传此参数。
返回如下：
{
  "ok": true,
  "result": {
    'cursor': '5e16e6200000000001009400',
    'data':{...}  # 评论数据
  }
}
```

#### 获取单条评论下的回复列表
```
http://whosecard.com:8081/api/xiaohongshu/note/sub_comments?note_id=***&comment_id=***&key=***

每页返回20条。
如果要翻页，需要传入cursor参数（会在前一次请求结果里返回），第一次请求不需要传此参数。
返回如下：
{
  "ok": true,
  "result": {
    'cursor': '5e16e6200000000001009400',
    'data': []  # 评论回复列表
  }
}
```

#### 获取单个笔记关联的商品列表（当笔记存在关联商品时才需要调用此接口）
```
http://whosecard.com:8081/api/xiaohongshu/note/goods?note_id=***&key=***

如果要翻页，需要传入page参数，从1开始，每页最多10条。
返回如下：
{
  "ok": true,
  "result": {
    ... # 返回值与小红书接口一样，字段比较多，按字面意思理解即可
  }
}
```

#### 获取用户笔记列表
```
http://whosecard.com:8081/api/xiaohongshu/user/notes?user_id=***&page=1&key=***

如果要翻页，需要传入page参数，从1开始，每页最多10条。
返回如下：
{
  "ok": true,
  "result": {
    ... # 返回值与小红书接口一样
  }
}
```

#### 获取用户个人页信息
```
http://whosecard.com:8081/api/xiaohongshu/user/info?user_id=***&key=***

返回如下：
{
  "ok": true,
  "result": {
    ... # 返回值与小红书接口一样
  }
}

当用户不存在时，则返回如下：
{
  "cost": true,
  "error": "用户不存在",
  "ok": false
}
```

#### 获取商城店铺下的商品列表
```
http://whosecard.com:8081/api/xiaohongshu/store/items?store_id=***&page=1&key=***

如果要翻页，需要传入page参数，从1开始，每页最多20条。
返回如下：
{
  "ok": true,
  "result": {
    ... # 返回值与小红书接口一样
  }
}
```

#### 关键字搜索列表
```
http://whosecard.com:8081/api/xiaohongshu/search/notes?keyword=口红&key=***&page=1&sort=general

如果要翻页，需要传入page参数，从1开始，每页最多20条。
sort为搜索排序方式，可取值：general(综合) popularity_descending(最热) time_descending(最新)， 默认取general
返回如下：
{
  "ok": true,
  "result": {
    ... # 返回值与小红书接口一样
  }
}
```

#### 话题页/poi页相关接口
```
http://whosecard.com:8081/api/xiaohongshu/fe_api?pageId=***&key=***

本接口同时支持话题页与poi页
如果是话题页，pageId为话题分享页的id，如5ac48683ec9d135e560e4bc4
如果是poi页，pageId也是对应分享页id，如5a7d3969ec9d13208be64be6

如果要获取笔记列表，则传入subPath=notes参数，翻页参数为page，从1开始，默认为1，如下：
http://whosecard.com:8081/api/xiaohongshu/fe_api?pageId=***&subPath=notes&page=1&key=***

返回如下：
{
  "ok": true,
  "result": {
    ... # 返回值与小红书接口一样
  }
}
```
