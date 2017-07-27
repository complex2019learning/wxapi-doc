#公众号链接转换接口

url请求需带上参数key，每个用户有唯一的key。

所有接口均返回json格式，其中参数ok[true|false]表示是否请求成功.

####公众号文章临时链接转为永久链接
```
http://whosecard.com:8081/api/url/transfer/tmp2forever?url=***&key=***

参数中的url为urlencode后的临时链接（从搜狗获取的文章链接）
eg:
http://whosecard.com:8081/api/url/transfer/tmp2forever?url=https%3a%2f%2fmp.weixin.qq.com%2fs%3ftimestamp%3d1495560892%26src%3d3%26ver%3d1%26signature%3diwHBaGJJBumXB4o0dEjdFM-Tm4DoYVUBEbzMGXK9Mb3Zy8Xbv8TJuJRRYq4*XWheCnRL1ZUMtIZeqGJfFMyMlE3hKi-3*7EMlUMaEid3BV4Ip5CjG3uihOI3OSpK07dkjTLw2LXxfp103Kcq4Gkc*I0ekHo4gu*lHbiFG8qRPSg%3d&key=***

注意⚠️：
临时链接最好在失效之前转换，否则具有不稳定因素！
如果真的失效了，则必须在参数中加上biz或者account才能转换，优先传biz参数，使用account具有一定转换失败的风险， 如下：
http://whosecard.com:8081/api/url/transfer/tmp2forever?url=***&key=***&biz=***&account=***
```

####公众号文章短链接转为长链接
```
http://whosecard.com:8081/api/url/transfer/short2long?url=***&key=***

参数中的url为urlencode后的短链接
eg:
http://whosecard.com:8081/api/url/transfer/short2long?url=https%3a%2f%2fmp.weixin.qq.com%2fs%2fAuyufPtU1UeusDS6B34VZg&key=***
```