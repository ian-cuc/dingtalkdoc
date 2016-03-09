# 发送普通会话消息
- category: 服务端开发文档
- order: 8---
员工可以在微应用中把消息发送到同企业的人或群。

调用接口时，使用Https协议、JSON数据包格式。

目前支持文本、图片、语音、普通文件、OA消息以及link等消息类型，每个消息都由消息头和消息体组成，普通会话的消息头由sender,cid组成。消息体请参见以下各种[<font color=red >消息类型</font>](#消息类型及数据格式)。

##### 参数说明

参数 | 参数类型 | 必须 | 说明
---------- | ------- | ------- | ------
sender | String | 是 | 消息发送者员工ID
cid | String | 是 | 群消息或者个人聊天会话Id，(通过[<font color=red>JSAPI之pickConversation接口</font>](#获取会话信息)唤起联系人界面选择之后即可拿到会话ID，之后您可以使用获取到的cid调用此接口）

普通会话消息样例：

![msg1](https://img.alicdn.com/tps/TB1FVMvIFXXXXcnXXXXXXXXXXXX.jpg)

## 发送普通会话消息接口说明

##### 请求说明

Https请求方式: POST

`https://oapi.dingtalk.com/message/send_to_conversation?access_token=ACCESS_TOKEN`

##### 参数说明

参数 | 参数类型 | 必须 | 说明
---------- | ------- | ------- | ------
access_token |String | 是 | 调用接口凭证

##### 返回说明

如果是群，返回跟发送者同一家企业的一组工号；如果是个人聊天，只返回发送者同一家企业的一个工号；不在同一家企业，发送失败

```
{
    "errcode": 0,
    "errmsg": "ok",
    "receiver": "UserID1|UserID2"
}
```

