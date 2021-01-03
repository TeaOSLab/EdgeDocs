# API认证
## 步骤1：创建AccessKey
如果你还没有AccessKey，则需要在用户平台"访问控制"页面中点击"创建AccessKey"，然后创建一个AccessKey。

## 步骤2：调用API获取AccessToken
### 接口地址
~~~
/APIAccessTokenService/GetAPIAccessToken
~~~

### 请求方法
POST。

### 请求参数
~~~json
{
    "type": "user",
    "accessKeyId": "zr9cmR42AEZxRyIV",
    "accessKey": "2w5p5NSZZuplUPsfPMzM7dFmTrI7xyja"
}
~~~
其中 `accessKeyId` 和 `accessKey` 换成你在步骤1中创建的AccessKey对应的数据。

### 响应结果
~~~
{
   "code": 200,
   "data": {
      "token": "IKNSMufZ1vDiXp5rSd9QR01m1174Oum5sah4amWFgbRb7lOKjuk62Spl7hgcazctzGhGG7jPgfmYUPojulC0FK5cLbrj8n7kxW7BtSawH9gWW14IWOzBY6UcpyXQndFu",
      "expiresAt": 1609686945
   },
   "message": "ok"
}
~~~
其中：
* `token` - 就是AccessToken，可以在别的接口中通过HTTP Header `Edge-Access-Token` 传入；
* `expiresAt` - 过期时间戳，默认为N个小时，过期后请即使重新获取。

多次调用此接口会导致先前获取的AccessToken失效。

