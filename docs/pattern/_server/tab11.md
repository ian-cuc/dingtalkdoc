# 免登
- category: 服务端开发文档
- order: 12---
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

