# 建立连接
- category: 服务端开发文档
- order: 2---
你可以使用以下两种方式，将钉钉微应用连接到你的企业应用：

1. 企业应用服务器调用钉钉开放平台提供的接口，以钉钉微应用的身份给企业用户的钉钉账号推送消息，以下称 **主动调用模式**。

2. 钉钉用户在使用企业提供的微应用H5页面时，该页面可以调用钉钉提供的JS接口，使用钉钉开放的终端能力和业务能力，以下称 **JSAPI模式**。

3. 钉钉服务器把用户发送的消息或用户触发的事件推送给企业应用，由企业应用处理，以下称 **回调模式**。

## 主动调用

当企业应用服务器调用钉钉开放平台接口时，需使用https协议、Json数据格式、UTF8编码，访问域名为 https://oapi.dingtalk.com。
在每次主动调用钉钉开放平台接口时需要带上AccessToken参数。AccessToken参数由CorpID和CorpSecret换取。对于ISV来说，[<font color=red>获取企业授权的access_token</font>](#5-获取企业授权的access_token)

CorpID是企业在钉钉中的标识，每个企业拥有一个唯一的CorpID；

CorpSecret是企业每个应用的凭证密钥。

CorpID及CorpSecret可以在钉钉为企业提供的管理后台中找到，由钉钉自动分配。

<aside class="notice">
POST请求请在HTTP Header中设置 Content-Type:application/json，否则接口调用失败
</aside>

## 主动调用的频率限制

当你获取到AccessToken时，你的微应用后台就可以成功调用钉钉后台所提供的各种接口或访问相应企业的资源或给成员发消息。

为了防止微应用的程序错误而引发钉钉服务器负载异常，默认情况下，每个服务端调用接口都有一定的频率限制，当超过此限制时，调用对应接口会收到相应错误码。

以下是当前默认的频率限制，钉钉后台可能会根据运营情况调整此阈值：

- 每个企业调用单个接口的频率不可超过1500次/分

- 每个ISV（应用提供商）调用单个接口的频率不可超过2000次/分

- 每个ISV（应用提供商）调用单个企业的单个接口频率不可超过1500次/分

- 每个套件调用单个企业的单个接口频率不可超过1000次/分


### 获取AccessToken

AccessToken是企业访问钉钉开放平台接口的全局唯一票据，调用接口时需携带AccessToken。

AccessToken需要用CorpID和CorpSecret来换取，不同的CorpSecret会返回不同的AccessToken。正常情况下AccessToken有效期为7200秒，有效期内重复获取返回相同结果，并自动续期。

##### 请求说明

Https请求方式: GET
`https://oapi.dingtalk.com/gettoken?corpid=id&corpsecret=secrect`

##### 参数说明

参数 | 参数类型 | 必须 | 说明
---------- | ------- | ------- | ------
corpid | String | 是 | 企业Id
corpsecret | String | 是 | 企业应用的凭证密钥

##### 返回说明

a)正确的Json返回结果:

```
{
    "errcode": 0,
    "errmsg": "ok",
    "access_token": "fw8ef8we8f76e6f7s8df8s"
}
```

参数 | 说明
---- | -----
errcode | 错误码
errmsg | 错误信息
access_token | 获取到的凭证

b)错误的Json返回示例:

```
{
   "errcode": 43003,
   "errmsg": "require https"
}
```

### 获取微应用后台管理Token
本接口获取的Token和上面获取的AccessToken应用场景不一样，此token只在[<font color=red>微应用后台管理免登</font>](#oa后台调用管理员免登)服务中使用。
应用场景示例如下图：

![normalcorp](https://img.alicdn.com/tps/TB1iw.4KFXXXXXoXFXXXXXXXXXX-594-302.png)

##### 请求说明

Https请求方式: GET
`https://oapi.dingtalk.com/sso/gettoken?corpid=id&corpsecret=ssosecret`

企业在[<font color=red>OA后台</font>](https://oa.dingtalk.com/#/microApp/microAppSet)获取SSOSecret的方法如下

![normalcorp](https://img.alicdn.com/tps/TB1y_xcKVXXXXa6XXXXXXXXXXXX-1084-621.jpg)

##### 参数说明

参数 | 参数类型 | 必须 | 说明
---------- | ------- | ------- | ------
corpid | String | 是 | 企业Id
corpsecret | String | 是 | 这里必须填写专属的SSOSecret

##### 返回说明

a)正确的Json返回结果:

```
{
    "errcode": 0,
    "errmsg": "ok",
    "access_token": "fw8ef8we8f76e6f7s8df8s"
}
```

参数 | 说明
---- | -----
errcode | 错误码
errmsg | 错误信息
access_token | 获取到的凭证

b)错误的Json返回示例:

```
{
   "errcode": 43003,
   "errmsg": "require https"
}
```


