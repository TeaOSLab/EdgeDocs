# API调用概述
除了 `/APIAccessTokenService/GetAPIAccessToken` 接口外，其他的所有接口都需要：
1. 在HTTP Header中传递`Edge-Access-Token`令牌数据，以便于我们认证用户是否有接口访问的权限，此令牌通过 `/APIAccessTokenService/GetAPIAccessToken` 接口获取
2. 所有请求数据需要以 `POST` 方法上传一个完整的JSON数据，接口响应数据也是JSON数据

比如：
~~~
POST /HTTPAccessLogService/ListHTTPAccessLogs
...
Edge-Access-Token: n8adDybtPCAGdbORkXjfpJgL28EGkOLz
...

{
	"serverId": 23,
	"day": "20210101",
	"size": 100,
	"reverse": true
}
~~~

可以在[这里](Auth.md)查看令牌获取方法。

## 格式化输出
可以在HTTP Header中增加 `Edge-Response-Pretty: on` 来让输出的JSON更加可读。