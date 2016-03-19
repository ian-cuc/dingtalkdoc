# 普通钉钉用户账号开放及免登(暂未开放，敬请期待)
- category: 免登服务
- order: 5---第三方web服务提供者，通过此项服务，可以使用普通钉钉用户账号登录自有的系统，并可将自有系统的账号与钉钉账号进行绑定，同时还能够获取钉钉用户的个人及企业数据，如姓名、手机号、对应企业的名称、企业是否认证过、企业的权益等级、其在企业内是否为管理人员等信息(取决于用户最终授权)。

<font color=red >注:此功能与ISV没有关系，任何外部系统都可以使用。</font>

1: 获取完成免登过程中验证身份的appId及appSecret。

<font color=red >暂未开放，敬请期待</font>

2: 使用appid及appSecret访问如下接口，获取accesstoken，此处获取的token有效期为2小时，有效期内重复获取，返回相同值，并自动续期，如果在有效期外获取会获得新的token值，建议定时获取本token，不需要用户登录时再获取。

[<font color=red >https://oapi.dingtalk.com/sns/gettoken?appid=APPID&appsecret=APPSECRET</font>](#获取钉钉开放应用的access_token)

3: 在钉钉用户访问你的Web系统时，如果用户选择使用钉钉账号登录，则需要由你构造并引导用户跳转到如下链接。

https://oapi.dingtalk.com/connect/oauth2/sns_authorize?appid=APPID&response_type=code&scope=snsapi_login&state=STATE&redirect_uri=REDIRECT_URI

参数 | 说明
---------- | ------
appid | 需要在第1步获取,代表了你提供的服务，必填
redirect_uri | 重定向地址(需要urlencode编码),该地址所在域名需要配置为appid对应的安全域名，必填
state | 用于防止重放攻击，选填
response_type | 固定为code，必填
scope | 固定为snsapi_login，必填

4:在钉钉用户登录钉钉系统后，会302到你指定的redirect_uri，并向url参数中追加code及state两个参数。

5:在你的web系统获取到代表用户的code之后，使用第2步获取的AccessToken及code获取当前钉钉用户授权给你的持久授权码，此授权码目前无过期时间，可反复使用，参数code只能使用一次。

[<font color=red >https://oapi.dingtalk.com/sns/get_persistent_code?access_token=ACCESS_TOKEN</font>](#获取用户授权的持久授权码)

6:在获得钉钉用户的持久授权码后，通过以下接口获取该用户授权的SNS_TOKEN，此token的有效时间为2小时，重复获取不会续期。

[<font color=red >https://oapi.dingtalk.com/sns/get_sns_token?access_token=ACCESS_TOKEN</font>](#获取用户授权的sns_token)

7:在获得钉钉用户的SNS_TOKEN后，通过以下接口获取该用户的个人信息。

[<font color=red >https://oapi.dingtalk.com/sns/getuserinfo?sns_token=SNS_TOKEN</font>](#获取用户授权的个人信息)
