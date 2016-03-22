# 发送企业会话消息
- category: 服务端开发文档
- order: 9---
企业可以主动发消息给员工，消息量不受限制。

发送企业会话消息和发送普通会话消息的不同之处在于发送消息的主体不同
- 普通会话消息发送主体是普通员工，体现在接收方手机上的联系人是消息发送员工

- 企业会话消息发送主体是企业，体现在接收方手机上的联系人是你填写的agentid对应的微应用

调用接口时，使用Https协议、JSON数据包格式。

目前支持text、image、voice、file、link、OA消息类型。每个消息都由消息头和消息体组成，企业会话的消息头由touser,toparty,agentid组成。消息体请参见以下各种[<font color=red >消息类型</font>](#消息类型及数据格式)。

##### 参数说明

参数 | 参数类型 | 必须 | 说明
---------- | ------- | ------- | ------
touser |String | 否 | 员工ID列表（消息接收者，多个接收者用' &#124; '分隔）。特殊情况：指定为@all，则向该企业应用的全部成员发送
toparty |String | 否 | 部门id列表，多个接收者用' &#124; '分隔。当touser为@all时忽略本参数 <font color=red >touser或者toparty 二者有一个必填</font>
agentid | String | 是 |企业应用id，这个值代表以哪个应用的名义发送消息

企业会话消息样例：

![msg2](https://img.alicdn.com/tps/TB1PAQwIFXXXXXOXXXXXXXXXXXX.jpg)

## 发送企业消息接口说明

##### 请求说明

Https请求方式: POST

`https://oapi.dingtalk.com/message/send?access_token=ACCESS_TOKEN`

##### 参数说明

参数 | 参数类型 | 必须 | 说明
---------- | ------- | ------- | ------
access_token |String | 是 | 调用接口凭证

##### 返回说明

如果收件人、部门或标签不存在，发送仍然执行，但返回无效的部分。

```
{
    "errcode": 0,
    "errmsg": "ok",
    "invaliduser": "UserID1|UserID2",
    "invalidparty":"PartyID1"
}
```

