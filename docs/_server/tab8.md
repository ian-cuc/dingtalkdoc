# 免登
- category: 服务端开发文档
- order: 9---
免登接口是关于用户无需输入用户名＋密码就可以实现登录，通过权限认证后获取用户身份的接口。

详细信息请查看[<font color=red >免登服务流程</font>](#免登服务)

## 通过CODE换取用户身份

企业应用的服务器在拿到CODE后，需要将CODE发送到钉钉开放平台接口，如果验证通过，则返回CODE对应的用户信息。**此接口只用于免登服务中用来换取用户信息**

##### 请求说明

Https请求方式: GET

`https://oapi.dingtalk.com/user/getuserinfo?access_token=ACCESS_TOKEN&code=CODE`

##### 参数说明

参数 | 参数类型 | 必须 | 说明
---------- | ------- | ------- | ------
access_token | String | 是 | 调用接口凭证
code | String | 是 | 通过Oauth认证会给URL带上CODE

##### 返回结果

正确时返回示例如下：

```
{
    "errcode": 40029,
    "errmsg": "invalid code",
    "userid": "USERID",
    "deviceId":"DEVICEID",
    "is_sys": true,
    "sys_level": 0|1|2
}
```

参数 | 说明
---------- | ------
userid | 员工在企业内的UserID
deviceId | 手机设备号,由钉钉在安装时随机产生
is_sys | 是否是管理员
sys_level | 级别，三种取值。0:非管理员 1：普通管理员 2：超级管理员


出错时返回示例如下：

```
{
    "errcode": 40029,
    "errmsg": "invalid code"
}
```

## 通过CODE换取微应用管理员的身份信息

企业应用的服务器在拿到CODE后，需要将CODE发送到钉钉开放平台接口，如果验证通过，则返回CODE对应的管理员信息。**此接口只用于微应用后台管理员免登中用来换取管理员信息**

##### 请求说明

Https请求方式: GET

`https://oapi.dingtalk.com/sso/getuserinfo?access_token=ACCESS_TOKEN&code=CODE`

##### 参数说明

参数 | 参数类型 | 必须 | 说明
---------- | ------- | ------- | ------
access_token | String | 是 | 再次强调，此token不同于一般的accesstoken，需要调用[<font color=red >获取微应用管理员免登需要的AccessToken</font>](#微应用后台管理员免登)
code | String | 是 | 通过Oauth认证给URL带上的CODE

##### 返回结果

正确时返回示例如下：

```
{
    "corp_info": {
        "corp_name": "一家公司",
        "corpid": "dingxxxxxx"
    },
    "errcode": 0,
    "errmsg": "ok",
    "is_sys": true,
    "user_info": {
        "avatar": "http://xxxxxxx.jpg",
        "email": "123456@aliyun.com",
        "name": "名称",
        "userid": "0571"
    }
}
```

参数 | 说明
---------- | ------
corp_name | 公司名字
corpid | 公司corpid
is_sys | 是否是管理员（在这里是true）
avatar | 头像地址
email | email地址",
name | 用户名字,
userid | 员工在企业内的UserID


出错时返回示例如下：

```
{
    "errcode": 40029,
    "errmsg": "invalid code"
}
```

##普通钉钉用户账号开放

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


##统计数据

##记录统计数据

用户在使用微应用的时候，企业可以通过这个接口记录微应用使用的相关信息，比如调用时间，结束时间等等。钉钉的数据分析工具会对这些数据进行汇总。

##### 请求说明

Https请求方式：POST

`https://oapi.dingtalk.com/data/record?access_token=ACCESS_TOKEN`

##### 参数说明

参数 | 参数类型 | 必须 | 说明
---------- | ------- | ------- | ------
access_token | String | 是 | 调用接口凭证
startTimeMs | String | 是 | 事件发生时间，单位为距离1970的毫秒数
endTimeMs | String | 是 | 事件结束时间（瞬间结束的，该值和发生事件一致）
module | String | 否 | 微应用提供区分内部模块的标记
originId | String | 否 | 微应用中该记录的主键索引
userid | String | 是 | 员工在企业内的UserID，企业用来唯一标识用户的字段
agentId | String | 是 | 授权方应用id
callbackUrl | String | 是 | 针对该条数据的回调url
extension | JSONObject | 否 | 扩展字段，json格式,具体的业务数据模型的定义，请参考附录二，现只开放考勤类业务数据模型

#####  返回结果

```
{
    "errcode": 0,
    "id":"$:LWCP_v1:$t3G6JuXLNr7pd0fWOQKS2w==",
    "errmsg": "ok"
}
```
参数 |  说明
---------- | -------
id      | 数据标识id
errcode | 返回码
errmsg | 对返回码的文本描述内容

##更新统计数据

isv企业可以通过这个接口更新微应用数据，所更新的数据必须是通过/data/record接口插入的，现在只能更新module，callbackUrl，extension三个字段。

##### 请求说明

Https请求方式：POST

`https://oapi.dingtalk.com/data/update?access_token=ACCESS_TOKEN`

##### 参数说明

参数 | 参数类型 | 必须 | 说明
---------- | ------- | ------- | ------
id| String| 是|使用/data/record接口插入数据时返回的id
access_token | String | 是 | 调用接口凭证
startTimeMs | String | 是 | 事件发生时间，单位为距离1970的毫秒数
endTimeMs | String | 是 | 事件结束时间（瞬间结束的，该值和发生事件一致）
module | String | 否 | 微应用提供区分内部模块的标记
originId | String | 否 | 微应用中该记录的主键索引
userid | String | 是 | 员工在企业内的UserID，企业用来唯一标识用户的字段
agentId | String | 是 | 授权方应用id
callbackUrl | String | 是 | 针对该条数据的回调url
extension | JSONObject | 否 | 扩展字段，json格式,具体的业务数据模型的定义，请参考附录二，现只开放考勤类业务数据模型
#####  返回结果

```
{
"errcode": 0,
"errmsg": "ok"
}
```
参数 |  说明
---------- | -------
errcode | 返回码
errmsg | 对返回码的文本描述内容



