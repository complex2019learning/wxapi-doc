#实时获取公众号阅读点赞接口

url请求需带上参数key，每个用户有唯一的key。

所有接口均返回json格式，其中参数ok[true|false]表示是否请求成功.

####实时获取公众号文章阅读点赞数据
```
http://whosecard.com:8081/api/msg/ext?url=***&key=***

参数中的url为urlencode后的永久链接
eg:
http://whosecard.com:8081/api/msg/ext?url=https%3a%2f%2fmp.weixin.qq.com%2fs%3f__biz%3dMjM5MzI5NTU3MQ%3d%3d%26mid%3d2651456339%26idx%3d1%26sn%3db28ead72f72decc7993d2db6a4a7f437%26scene%3d0%23wechat_redirect&key=***

返回如下：
{
	"ok": true,
	"clicksCount": 56602,
	"likeCount": 196,
	"advertisementNum": 1,
	"advertisementInfo": [
	   {
	       "hint_txt": "每天介绍新的科技玩具",  # 推荐文本
	       # url为推荐卡片外链
	       "url": "https://mp.weixin.qq.com/mp/ad_biz_info?__biz=MzU4MjAzNjkyMw==&amp;sn=6c0dcba45519d4c528756f9f5151130c&amp;weixinadkey=ebfa1f9258d2febf727ffc036131081771b42edf685d445435b51cbd21776cc2cc882dbcbff116ee6988f889a6653733&amp;ticket=2gz4o657fhrrv&amp;gdt_vid=wx0aspf7bz2og7ig00&amp;weixinadinfo=11034783.wx0aspf7bz2og7ig00.0.1#wechat_redirect",
	       "type": "0",
	       "group_id": "",
	       "aid": "11034783",  # 广告id
	       "image_url": "",
	       "ad_desc": "",
	       "biz_appid": "wx98697a2c3864ea4a",
	       "biz_info": {  # 推荐的公众号信息，如果推荐的不是公众号则没有此字段
	         "user_name": "gh_b5782da976b0",
	         "nick_name": "狂丸",
	         "is_subscribed": 0,
	         "head_img": "http://wx.qlogo.cn/mmhead/Q3auHgzwzM7z1t6Nn99nJnyAQ0nsnnCvoYNd490BhPAcXzaqm87tnw/0",
	         "biz_uin": 3582036923
	       },
	       "pos_type": 0,
	       "watermark_type": 0,
	       "logo": "",
	       "is_cpm": 0,
	       "dest_type": 0
     }
  	]
 }

advertisementNum为该文章的附带广告数量，仅开通广点通的公众号才有。
advertisementInfo为微信接口返回的广告内容，具体含义参照字面含义。
```
