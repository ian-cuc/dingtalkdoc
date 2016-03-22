# 通讯录及群会话变更事件回调接口
- category: 服务端开发文档
- order: 7---
在使用回调接口之前您需要了解的是，

首先您需要准备好，

- URL:[<font color=red>注册事件回调接口</font>](#注册事件回调接口)填写的接收推送的地址

- Token:[<font color=red>注册事件回调接口</font>](#注册事件回调接口)中任意填写的，用来生成signature，用来和回调参数中的signature比对，校验消息的合法性

- 数据加密密钥(ENCODING_AES_KEY):[<font color=red>注册事件回调接口</font>](#注册事件回调接口)中填写的数据加密密钥。用于回调数据的加解密，长度固定为43个字符，从a-z, A-Z, 0-9共62个字符中选取,您可以随机生成。

钉钉服务器会向回调url推送事件变更。

假设您提供的回调URL是

`https://127.0.0.1/suite/receive`

那么在钉钉服务器每一次访问回调URL的时候
将请求(下面链接中的signature,timestamp,nonce的值只是示例，并不代表真实返回的值):

`https://127.0.0.1/suite/receive?signature=111108bb8e6dbce3c9671d6fdb69d15066227608
&timestamp=1783610513&nonce=380320111`

```
{
    "encrypt":"1ojQf0NSvw2WPvW7LijxS8UvISr8pdDP+rXpPbcLGOmIBNbWetRg7IP0vdhVgkVwSoZBJeQwY2zhROsJq/HJ+q6tp1qhl9L1+ccC9ZjKs1wV5bmA9NoAWQiZ+7MpzQVq+j74rJQljdVyBdI/dGOvsnBSCxCVW0ISWX0vn9lYTuuHSoaxwCGylH9xRhYHL9bRDskBc7bO0FseHQQasdfghjkl"
}
```

回调数据的格式如右所示：

其中的encrypt字段是经过加密的消息体，encrypt经过一系列解密步骤后，才能产生下面所说的“POST数据解密后示例”，服务提供商可以直接使用钉钉提供的库进行解密的处理。

除此之外，在接收到推送之后，**需要返回字符串success（代表了你收到了推送），返回的数据也需要做加密处理**，如果不返回，钉钉服务器将持续推送下去，达到一定阈值后将不再推送。

"Talk is cheap, show me the code."所以我们也为开发者提供了加解密的demo，目前提供Java/PHP等语言版本。
加解密库和demo的下载：[<font color=red >加解密库和demo下载</font>](#加解密库和demo下载)

如有需要，可以查看具体加解密步骤：[<font color=red >查看</font>](#12-加解密方案)

## 通讯录事件回调

当企业通讯录发生变化，并且事件类型包含在注册时填写的"call_back_tag"中时，比如call_back_tag字段为"["user_add_org","user_modify_org"]"，那么企业通讯录发生了"通讯录用户增加"和"讯录用户更改"，钉钉服务器会向url推送事件。

目前可以监听的事件类型分别为:

- user_add_org : 通讯录用户增加
- user_modify_org : 通讯录用户更改
- user_leave_org : 通讯录用户离职
- org_admin_add ：通讯录用户被设为管理员
- org_admin_remove ：通讯录用户被取消设置管理员
- org_dept_create ： 通讯录企业部门创建
- org_dept_modify ： 通讯录企业部门修改
- org_dept_remove ： 通讯录企业部门删除
- org_remove ： 企业被解散

POST数据解密后示例
接收到推送之后请务必返回经过加密的字符串"success"的json数据

```
{
    "EventType": "user_add_org",
    "TimeStamp": 43535463645,
    "UserId": ["efefef" , "111111"],
    "CorpId": "corpid"
}
```

##### 参数说明

参数 | 说明
----------  | ------
EventType | 事件类型，有八种，"user_add_org", "user_modify_org", "user_leave_org","org_admin_add", "org_admin_remove", "org_dept_create", "org_dept_modify", "org_dept_remove", "org_remove"
TimeStamp | 时间戳
UserId | 用户发生变更的userid列表
DeptId | 部门发生变更的userid列表
CorpId | 发生通讯录变更的企业

#### 返回说明

服务提供商在收到此事件推送后务必返回包含经过加密的字符串"success"的json数据

只有返回了对应的json数据，钉钉才会判断此事件推送成功，套件才能创建成功。

```

{
  "msg_signature":"111108bb8e6dbce3c9671d6fdb69d15066227608",
  "timeStamp":"1783610513",
  "nonce":"123456",
  "encrypt":"1ojQf0NSvw2WPvW7LijxS8UvISr8pdDP+rXpPbcLGOmIBNbWetRg7IP0vdhVgkVwSoZBJeQwY2zhROsJq/HJ+q6tp1qhl9L1+ccC9ZjKs1wV5bmA9NoAWQiZ+7MpzQVq+j74rJQljdVyBdI/dGOvsnBSCxCVW0ISWX0vn9lYTuuHSoaxwCGylH9xRhYHL9bRDskBc7bO0FseHQQasdfghjkl"
 }

```

参数      | 说明
-------   | -------------
msg_signature  | 消息体签名
timeStamp | 时间戳
nonce  | 随机字符串
encrypt  | "success"加密字符串

## 群会话事件回调

当企业群会话发生变化，并且事件类型包含在注册时填写的"call_back_tag"中时，比如call_back_tag字段为"["chat_add_member","chat_remove_member"]"，那么企业群会话发生了"群会话添加人员"和"群会话删除人员"，钉钉服务器会向url推送事件。

目前可以监听的事件类型分别为:

- chat_add_member : 群会话添加人员
- chat_remove_member : 群会话删除人员
- chat_quit : 群会话用户主动退群
- chat_update_owner ：群会话更换群主
- chat_update_title ：群会话更换群名称
- chat_disband ： 群会话解散群
- chat_disband_microapp ： 绑定了微应用的群会话，在解散时回调

POST数据解密后示例
接收到推送之后请务必返回经过加密的字符串"success"的json数据

```
{
    "EventType": "chat_add_member",
    "TimeStamp": 43535463645,
    "CorpId": "corpid",
    "ChatId": "chat90f29b737b56dc179df8w86t83d5f0f8",
    "UserId": ["efefef" , "111111"],
    "Operator": "manager0112",
}
```

##### 参数说明

参数 | 说明明
----------  | ------
EventType | 事件类型，有七种，"chat_add_member", "chat_remove_member", "chat_quit", "chat_update_owner", "chat_update_title", "chat_disband","chat_disband_microapp"
TimeStamp | 时间戳
CorpId | 发生群会话变更的企业
ChatId | 会话的ID
UserId | 用户发生变更的userid列表
Owner  | 已经更新的新的群主的userid
Title  | 已经更新的新的群标题
Operator | 操作人员的userid
agentId  | 群会话绑定的微应用agentId

#### 返回说明

服务提供商在收到此事件推送后务必返回包含经过加密的字符串"success"的json数据

只有返回了对应的json数据，钉钉才会判断此事件推送成功，套件才能创建成功。

```

{
  "msg_signature":"111108bb8e6dbce3c9671d6fdb69d15066227608",
  "timeStamp":"1783610513",
  "nonce":"123456",
  "encrypt":"1ojQf0NSvw2WPvW7LijxS8UvISr8pdDP+rXpPbcLGOmIBNbWetRg7IP0vdhVgkVwSoZBJeQwY2zhROsJq/HJ+q6tp1qhl9L1+ccC9ZjKs1wV5bmA9NoAWQiZ+7MpzQVq+j74rJQljdVyBdI/dGOvsnBSCxCVW0ISWX0vn9lYTuuHSoaxwCGylH9xRhYHL9bRDskBc7bO0FseHQQasdfghjkl"
 }

```

参数      | 说明
-------   | -------------
msg_signature  | 消息体签名
timeStamp | 时间戳
nonce  | 随机字符串
encrypt  | "success"加密字符串

##注册事件回调接口

注册回调接口的时候，钉钉服务器会回调[<font color=red>测试回调url</font>](#测试回调url)，来验证填写的url的合法性，需要您再接收到回调之后返回加密字符串"success"的json数据,才能完成注册。

<img src="https://img.alicdn.com/tps/TB10MOOJFXXXXbdXpXXXXXXXXXX-373-351.png" width = "373" height = "351" alt="图片名称" align=center />


##### 请求说明

Https请求方式: POST

`https://oapi.dingtalk.com/call_back/register_call_back?access_token=ACCESS_TOKEN`

##### 请求包结构体

```
{
    "call_back_tag": ["user_add_org", "user_modify_org", "user_leave_org"],
    "token": "123456",
    "aes_key": "1",
    "url":"www.dingtalk.com"
}
```
##### 参数说明

参数 | 参数类型 | 必须 | 说明
----------| ------- | ------- | ------
access_token | String | 是 | 调用接口凭证
call_back_tag | Array[String] | 是 |  需要监听的事件类型，有16种，"user_add_org", "user_modify_org", "user_leave_org","org_admin_add", "org_admin_remove", "org_dept_create", "org_dept_modify", "org_dept_remove", "org_remove", "chat_add_member", "chat_remove_member", "chat_quit", "chat_update_owner", "chat_update_title", "chat_disband", "chat_disband_microapp"
token | String | 是 | 加解密需要用到的token，ISV(服务提供商)推荐使用注册套件时填写的token，普通企业可以随机填写
aes_key  | String | 是 | 数据加密密钥。用于回调数据的加密，长度固定为43个字符，从a-z, A-Z, 0-9共62个字符中选取,您可以随机生成，ISV(服务提供商)推荐使用注册套件时填写的EncodingAESKey
url  | String | 是 | 接收事件回调的url

##### 返回结果

```
{
    "errcode": 0,
    "errmsg": "ok"
}
```

参数 | 说明
----------  | ------
errcode | 返回码
errmsg | 对返回码的文本描述内容



##查询事件回调接口

##### 请求说明

Https请求方式: get

`https://oapi.dingtalk.com/call_back/get_call_back?access_token=ACCESS_TOKEN`

##### 参数说明

参数 | 参数类型 | 必须 | 说明
----------| ------- | ------- | ------
access_token | String | 是 | 调用接口凭证

##### 返回结果

```
{   
    "errcode": 0,
    "errmsg": "ok",
    "call_back_tag": ["user_add_org", "user_modify_org", "user_leave_org"],
    "token": "123456",
    "aes_key": "",
    "url":"www.dingtalk.com"

}
```

参数 | 说明
----------  | ------
errcode | 返回码
errmsg | 对返回码的文本描述内容
access_token  | 调用接口凭证
call_back_tag |  需要监听的事件类型，有16种，"user_add_org", "user_modify_org", "user_leave_org","org_admin_add", "org_admin_remove", "org_dept_create", "org_dept_modify", "org_dept_remove", "org_remove", "chat_add_member", "chat_remove_member", "chat_quit", "chat_update_owner", "chat_update_title", "chat_disband", "chat_disband_microapp"
token | 加解密需要用到的token，ISV(服务提供商)推荐使用注册套件时填写的token，普通企业可以随机填写
aes_key  | 数据加密密钥。用于回调数据的加密，长度固定为43个字符，从a-z, A-Z, 0-9共62个字符中选取,您可以随机生成，ISV(服务提供商)推荐使用注册套件时填写的EncodingAESKey
url   | 接收事件回调的url



##更新事件回调接口

##### 请求说明

Https请求方式: POST

`https://oapi.dingtalk.com/call_back/update_call_back?access_token=ACCESS_TOKEN`

##### 请求包结构体

```
{
    "call_back_tag": ["user_add_org", "user_modify_org", "user_leave_org","org_admin_add", "org_admin_remove", "org_dept_create", "org_dept_modify", "org_dept_remove", "org_remove"],
    "token": "123456",
    "aes_key": "11111111lvdhntotr3x9qhlbytb18zyz5z111111111",
    "url": "www.dingtalk.com"
}
```
##### 参数说明

参数 | 参数类型 | 必须 | 说明
----------| ------- | ------- | ------
access_token | String | 是 | 调用接口凭证
call_back_tag | Array[String] | 是 |  需要监听的事件类型，有16种，"user_add_org", "user_modify_org", "user_leave_org","org_admin_add", "org_admin_remove", "org_dept_create", "org_dept_modify", "org_dept_remove", "org_remove", "chat_add_member", "chat_remove_member", "chat_quit", "chat_update_owner", "chat_update_title", "chat_disband","chat_disband_microapp"
token | String | 是 | 加解密需要用到的token，ISV(服务提供商)推荐使用注册套件时填写的token，普通企业可以随机填写
aes_key  | String | 是 | 数据加密密钥。用于回调数据的加密，长度固定为43个字符，从a-z, A-Z, 0-9共62个字符中选取,您可以随机生成，ISV(服务提供商)推荐使用注册套件时填写的EncodingAESKey
url  | String | 是 | 接收事件回调的url

##### 返回结果

```
{
    "errcode": 0,
    "errmsg": "ok"
}
```

参数 | 说明
----------  | ------
errcode | 返回码
errmsg | 对返回码的文本描述内容




##删除事件回调接口

##### 请求说明

Https请求方式: get

`https://oapi.dingtalk.com/call_back/delete_call_back?access_token=ACCESS_TOKEN`

##### 参数说明

参数 | 参数类型 | 必须 | 说明
----------| ------- | ------- | ------
access_token | String | 是 | 调用接口凭证

##### 返回结果
```
{
   "errcode": 0,
   "errmsg": "ok"

}
```

参数 | 说明
----------  | ------
errcode | 返回码
errmsg | 对返回码的文本描述内容



## 获取回调失败的结果

钉钉服务器给回调接口推送 通讯录变更事件的时候，有可能因为各种原因推送失败(比如网络异常)，此时钉钉服务器将保留此次变更事件。

用户可以通过此回调接口获取推送失败的变更事件。

##### 请求说明

Https请求方式: get

`https://oapi.dingtalk.com/call_back/get_call_back_failed_result?access_token=ACCESS_TOKEN`

##### 参数说明

参数 | 参数类型 | 必须 | 说明
----------| ------- | ------- | ------
access_token | String | 是 | 调用接口凭证


##### 返回结果
```
{
   "errcode": 0,
   "errmsg": "ok",
   "has_more": false,
   "failed_list": [
        {
            "event_time" : 32112412,
            "call_back_tag" : "user_add_org",
            "userid" : ["",""],
            "corpid" : ""
        },
        {
            "event_time" : 24431231,
            "call_back_tag" : "user_add_org",
            "userid" : ["",""],
            "corpid" : ""
        }
   ]

}
```

参数 | 说明
----------  | ------
errcode | 返回码
errmsg | 对返回码的文本描述内容
has_more | 是否还有推送失败的变更事件，若为true,则表示还有未回调的事件
failed_list | 事件列表，一次最多200个
event_time | 事件的时间戳
call_back_tag | 事件类型，有16种，"user_add_org", "user_modify_org", "user_leave_org","org_admin_add", "org_admin_remove", "org_dept_create", "org_dept_modify", "org_dept_remove", "org_remove", "chat_add_member", "chat_remove_member", "chat_quit", "chat_update_owner", "chat_update_title", "chat_disband","chat_disband_microapp"
userid | 相关员工列表
deptid | 相关部门列表
corpid | 相关企业id

## 测试回调url

在您注册事件回调接口的时候，钉钉服务器会向您”注册回调接口“时候上传的url(接收回调的url)推送一条消息，用来测试url的合法性。

收到消息需要返回经过加密后的字符串"success"的json数据，否则钉钉服务器将认为url不合法，从而不予推送。

POST数据解密后示例

```
{
    "EventType" : "check_url"
}
```
参数 | 说明
----------  | ------
EventType | "check_url"

#### 返回说明

服务提供商在收到此事件推送后务必返回包含经过加密的字符串"success"的json数据

只有返回了对应的json数据，钉钉才会判断此事件推送成功，套件才能创建成功。

```

{
  "msg_signature":"111108bb8e6dbce3c9671d6fdb69d15066227608",
  "timeStamp":"1783610513",
  "nonce":"123456",
  "encrypt":"1ojQf0NSvw2WPvW7LijxS8UvISr8pdDP+rXpPbcLGOmIBNbWetRg7IP0vdhVgkVwSoZBJeQwY2zhROsJq/HJ+q6tp1qhl9L1+ccC9ZjKs1wV5bmA9NoAWQiZ+7MpzQVq+j74rJQljdVyBdI/dGOvsnBSCxCVW0ISWX0vn9lYTuuHSoaxwCGylH9xRhYHL9bRDskBc7bO0FseHQQasdfghjkl"
  }

```

参数      | 说明
-------   | -------------
msg_signature  | 消息体签名
timeStamp | 时间戳
nonce  | 随机字符串
encrypt  | "success"加密字符串




