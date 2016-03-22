# 普通钉钉用户账号开放
- category: 服务端开发文档
- order: 13---
##获取钉钉开放应用的ACCESS_TOKEN

第三方web服务提供商取得钉钉开放应用的appid及appsecret后，可以获取开放应用的ACCESS_TOKEN

##### 请求说明


Https请求方式: GET

`https://oapi.dingtalk.com/sns/gettoken?appid=APPID&appsecret=APPSECRET`


##### 参数说明

参数 | 参数类型 | 必须 | 说明
---------- | ------- | ------- | ------
appid | String | 是 | 由钉钉开放平台提供给开放应用的唯一标识
appsecret | String | 是 | 由钉钉开放平台提供的密钥

##### 返回结果

正确时返回示例如下

```
{
    "access_token": "070c171a26d633d1b631dxxxxxxxx", 
    "errcode": 0, 
    "errmsg": "ok"
}
```

参数 | 说明
---------- | ------
access_token | token的值


##获取用户授权的持久授权码

##### 请求说明

Https请求方式: POST

`https://oapi.dingtalk.com/sns/get_persistent_code?access_token=ACCESS_TOKEN`

POST 正文

```
{
    "tmp_auth_code": "23152698ea18304da4d0ce1xxxxx"
}
```

##### 参数说明

参数 | 参数类型 | 必须 | 说明
---------- | ------- | ------- | ------
access_token | String | 是 | 开放应用的token
tmp_auth_code | String | 是 | 用户授权给钉钉开放应用的临时授权码

##### 返回结果

正确时返回示例如下

```
{
    "errcode": 0, 
    "errmsg": "ok", 
    "openid": "liSii8KCxxxxx", 
    "persistent_code": "dsa-d-asdasdadHIBIinoninINIn-ssdasd", 
    "unionid": "7Huu46kk"
}
```

参数 | 说明
---------- | ------
openid | 用户在当前开放应用内的唯一标识
unionid | 用户在当前钉钉开放平台账号范围内的唯一标识，同一个钉钉开放平台账号可以包含多个开放应用，同时也包含ISV的套件应用及企业应用
persistent_code | 用户给开放应用授权的持久授权码，此码目前无过期时间


##获取用户授权的SNS_TOKEN

##### 请求说明

Https请求方式: POST

`https://oapi.dingtalk.com/sns/get_sns_token?access_token=ACCESS_TOKEN`

POST 正文

```
{
    "openid": "liSii8KCxxxxx", 
    "persistent_code": "dsa-d-asdasdadHIBIinoninINIn-ssdasd"
}
```

##### 参数说明

参数 | 参数类型 | 必须 | 说明
---------- | ------- | ------- | ------
access_token | String | 是 | 开放应用的token
openid | String | 是 | 用户的openid
persistent_code | String | 是 | 用户授权给钉钉开放应用的持久授权码

##### 返回结果

正确时返回示例如下

```
{
    "errcode": 0, 
    "errmsg": "ok", 
    "expires_in": 7200, 
    "sns_token": "c76dsc87ds6c876sd87csdcxxxxx"
}
```

参数 | 说明
---------- | ------
expires_in | sns_token的过期时间
sns_token | 用户授权的token

##获取用户授权的个人信息

##### 请求说明

Https请求方式: GET

`https://oapi.dingtalk.com/sns/getuserinfo?sns_token=SNS_TOKEN`

##### 参数说明

参数 | 参数类型 | 必须 | 说明
---------- | ------- | ------- | ------
sns_token | String | 是 | 用户授权给开放应用的token

##### 返回结果

正确时返回示例如下

```
{
    "corp_info": [
        {
            "corp_name": "阿里巴巴", 
            "is_auth": true, 
            "is_manager": false, 
            "rights_level": 100
        }, 
        {
            "corp_name": "DingTalk", 
            "is_auth": true, 
            "is_manager": false, 
            "rights_level": 200
        }
    ], 
    "errcode": 0, 
    "errmsg": "ok", 
    "user_info": {
        "maskedMobile": "130****1234", 
        "nick": "张三", 
        "openid": "liSii8KCxxxxx", 
        "unionid": "7Huu46kk"
    }
}
```

参数 | 说明
---------- | ------
corp_info | 企业信息
is_auth | 企业是否经过钉钉认证
is_manager | 当前用户是否为该企业的管理人员
rights_level | 该企业的权益等级
corp_name | 企业名称
maskedMobile | 经过处理的手机号
nick | 用户在钉钉上面的昵称

openid | 用户在当前开放应用内的唯一标识
unionid | 用户在当前开放应用所属的钉钉开放平台账号内的唯一标识


