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
  "ok": false,
  "result": {
    "msg": "",
    "result": -1,
    "success": false
  }
}
```

#### 获取用户笔记列表
```
http://whosecard.com:8081/api/xiaohongshu/user/notes?user_id=***&page=1&key=***

如果要翻页，需要传入page参数，从1开始，每页最多15条。
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
http://whosecard.com:8081/api/xiaohongshu/search/notes?keyword=口红&key=***&page=1

如果要翻页，需要传入page参数，从1开始，每页最多20条。
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
