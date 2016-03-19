# 群会话接口
- category: 服务端开发文档
- order: 5---

## 创建会话

##### 请求说明

Https请求方式: POST

`https://oapi.dingtalk.com/chat/create?access_token=ACCESS_TOKEN`

##### 请求包结构体

```
{
    "name": "群名称",
    "owner": "zhangsan",
    "useridlist": ["zhangsan","lisi"]
}
```

##### 参数说明

参数 | 参数类型 | 必须 | 说明
----------| ------- | ------- | ------
access_token | String | 是 | 调用接口凭证
name | String | 是 |  群名称。长度限制为1~20个字符
owner | String | 是 | 群主userId，员工唯一标识ID；必须为该会话useridlist的成员之一
useridlist  | String[] | 是 | 群成员列表，每次最多操作40人，群人数上限为1000

##### 返回结果

```
{
    "errcode": 0,
    "errmsg": "ok",
    "chatid": "chatxxxxxxxxxxxxxxxxxxx"
}
```

参数 | 说明
----------  | ------
errcode | 返回码
errmsg | 对返回码的文本描述内容
chatid | 群会话的id

## 修改会话

##### 请求说明

Https请求方式: POST

`https://oapi.dingtalk.com/chat/update?access_token=ACCESS_TOKEN`

##### 请求包结构体

```
{
    "chatid": "chatxxxxxxxxxxxxxxxxxxx",
    "name": "群名称",
    "owner": "zhangsan",
    "add_useridlist": ["lisi"],
    "del_useridlist": ["wangwu"]
}
```

##### 参数说明

参数 | 参数类型 | 必须 | 说明
----------| ------- | ------- | ------
access_token | String | 是 | 调用接口凭证
chatid | String | 是 | 群会话的id
name | String | 否 |  群名称。长度限制为1~20个字符，不传则不修改
owner | String | 否 | 群主userId，员工唯一标识ID；必须为该会话成员之一；不传则不修改
add_useridlist  | String[] | 否 | 添加成员列表，每次最多操作40人，群人数上限为1000
del_useridlist  | String[] | 否 | 删除成员列表，每次最多操作40人，群人数上限为1000

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

## 获取会话

##### 请求说明

Https请求方式: GET

`https://oapi.dingtalk.com/chat/get?access_token=ACCESS_TOKEN`

##### 参数说明

参数 | 参数类型 | 必须 | 说明
---------- | ------- | ------- | ------
access_token | String | 是 | 调用接口凭证
chatid | String | 是 | 群会话的id

##### 返回结果

```
{
    "errcode": 0,
    "errmsg": "ok",
    "chat_info":
        {
            "name": "群名称",
            "owner": "zhangsan",
            "useridlist": ["zhangsan","lisi"],
            "agentidlist": ["12345"]
        }
}
```

参数 | 说明
---- | -----
errcode | 返回码
errmsg | 对返回码的文本描述内容
chat_info | 群会话信息
name | 群名称
owner | 群主userid
useridlist | 群成员userId列表
agentidlist | 群绑定的微应用agentId列表


## 绑定微应用和群会话

此接口仅限ISV接入使用

##### 请求说明

Https请求方式: GET

`https://oapi.dingtalk.com/chat/bind?access_token=ACCESS_TOKEN`

##### 参数说明

参数 | 参数类型 | 必须 | 说明
---------- | ------- | ------- | ------
access_token | String | 是 | 调用接口凭证
chatid | String | 是 | 群会话的id
agentid | String | 是 | 微应用agentId，每个群最多绑定5个微应用，一个群只能被一个ISV套件绑定一次

##### 返回结果

```
{
    "errcode": 0,
    "errmsg": "ok"
}
```

参数 | 说明
---- | -----
errcode | 返回码
errmsg | 对返回码的文本描述内容

## 解绑微应用和群会话

此接口仅限ISV接入使用

##### 请求说明

Https请求方式: GET

`https://oapi.dingtalk.com/chat/unbind?access_token=ACCESS_TOKEN`

##### 参数说明

参数 | 参数类型 | 必须 | 说明
---------- | ------- | ------- | ------
access_token | String | 是 | 调用接口凭证
chatid | String | 是 | 群会话的id
agentid | String | 是 | 微应用agentId

##### 返回结果

```
{
    "errcode": 0,
    "errmsg": "ok"
}
```

参数 | 说明
---- | -----
errcode | 返回码
errmsg | 对返回码的文本描述内容

## 发送消息到群会话

##### 请求说明

Https请求方式: POST

`https://oapi.dingtalk.com/chat/send?access_token=ACCESS_TOKEN`

##### 参数说明

参数 | 参数类型 | 必须 | 说明
---------- | ------- | ------- | ------
access_token |String | 是 | 调用接口凭证

##### 返回说明

```
{
    "errcode": 0,
    "errmsg": "ok"
}
```
参数 | 说明
---- | -----
errcode | 返回码
errmsg | 对返回码的文本描述内容

### 消息类型及数据格式

#### text消息

```
{
	"chatid": "chatxxxxxxxxx",
	"sender": "manager1122",
    "msgtype": "text",
    "text": {
        "content": "张三的请假申请"
    }
}
```

##### 参数说明

参数 | 参数类型 | 必须 | 说明
---------- | ------- | ------- | ------
chatid | String | 是 | 群会话的id
sender | String | 是 | 发送者的userid
msgtype |String | 是 | 消息类型，此时固定为：text

##### text消息体格式

参数 | 参数类型 | 必须 | 说明
---------- | ------- | ------- | ------
text.content |String | 是 | 消息内容

#### image消息

```
{
	"chatid": "chatxxxxxxxxx",
	"sender": "manager1122",
    "msgtype": "image",
    "image": {
        "media_id": "MEDIA_ID"
    }
}
```

##### 参数说明

参数 | 参数类型 | 必须 | 说明
---------- | ------- | ------- | ------
chatid | String | 是 | 群会话的id
sender | String | 是 | 发送者的userid
msgtype |String | 是 | 消息类型，此时固定为：image

##### image消息体格式

参数 | 参数类型 | 必须 | 说明
---------- | ------- | ------- | ------
image.media_id | String | 是 | 图片媒体文件id，可以调用上传媒体文件接口获取。建议宽600像素 x 400像素，宽高比3：2

#### voice消息

```
{
	"chatid": "chatxxxxxxxxx",
	"sender": "manager1122",
    "msgtype": "voice",
    "voice": {
       "media_id": "MEDIA_ID"
    }
}
```

##### 参数说明

参数 | 参数类型 | 必须 | 说明
---------- | ------- | ------- | ------
chatid | String | 是 | 群会话的id
sender | String | 是 | 发送者的userid
msgtype |String | 是 | 消息类型，此时固定为：voice

##### voice消息体格式

参数 | 参数类型 | 必须 | 说明
---------- | ------- | ------- | ------
voice.media_id |String | 是 | 语音媒体文件id，可以调用上传媒体文件接口获取。2MB，播放长度不超过60s，AMR格式

#### file消息

```
{
	"chatid": "chatxxxxxxxxx",
	"sender": "manager1122",
    "msgtype": "file",
    "file": {
       "media_id": "MEDIA_ID"
    }
}
```

##### 参数说明

参数 | 参数类型 | 必须 | 说明
---------- | ------- | ------- | ------
chatid | String | 是 | 群会话的id
sender | String | 是 | 发送者的userid
msgtype | String| 是 | 消息类型，此时固定为：file

##### file消息体格式

参数 | 参数类型 | 必须 | 说明
---------- | ------- | ------- | ------
file.media_id |String | 是 | 媒体文件id，可以调用上传媒体文件接口获取。10MB


#### link消息

```
{
	"chatid": "chatxxxxxxxxx",
	"sender": "manager1122",
    "msgtype": "link",
    "link": {
        "title": "测试",
        "text": "测试",
        "pic_url":"https://gw.alicdn.com/tps/TB1FN16LFXXXXXJXpXXXXXXXXXX-256-130.png",
        "message_url": "http://www.dingtalk.com"
    }
}
```

##### 参数说明

参数 | 参数类型 | 必须 | 说明
---------- | ------- | ------- | ------
chatid | String | 是 | 群会话的id
sender | String | 是 | 发送者的userid
msgtype | String | 是 | 消息类型，此时固定为：link

##### link消息体格式

参数 | 参数类型 | 必须 | 说明
---------- | ------- | ------- | ------
link.title | String | 是 | 消息标题
link.text | String | 是 | 消息描述
link.pic_url | String | 是 | 图片媒体文件id，可以调用上传媒体文件接口获取
link.message_url | String | 是 | 消息点击链接地址

#### OA消息

```
{
	 "chatid": "chatxxxxxxxxx",
	 "sender": "manager1122",
	 "msgtype": "oa",
     "oa": {
        "message_url": "https://www.dingtalk.com",
        "pc_message_url": "https://oa.dingtalk.com",
        "head": {
            "bgcolor": "FFBBBBBB",
            "text": "头部标题"
        },
        "body": {
            "title": "正文标题",
            "form": [
                {
                    "key": "姓名:",
                    "value": "张三"
                },
                {
                    "key": "年龄:",
                    "value": "20"
                },
                {
                    "key": "身高:",
                    "value": "1.8米"
                },
                {
                    "key": "体重:",
                    "value": "130斤"
                },
                {
                    "key": "学历:",
                    "value": "本科"
                },
                {
                    "key": "爱好:",
                    "value": "打球、听音乐"
                }
            ],
            "rich": {
                "num": "15.6",
                "unit": "元"
            },
            "content": "大段文本大段文本大段文本大段文本大段文本大段文本大段文本大段文本大段文本大段文本大段文本大段文本",
            "image": "@lADOADmaWMzazQKA",
            "file_count": "3",
            "author": "李四 "
        }
    }
}
```

##### 参数说明

参数 | 参数类型 | 必须 | 说明
----- | ------- | ------- | ------
chatid | String | 是 | 群会话的id
sender | String | 是 | 发送者的userid
msgtype |String | 是 | 消息类型，此时固定为：oa

##### OA消息体格式

参数 | 参数类型 | 必须 | 说明
------ | ------- | ------- | ------
oa.message_url| String | 是 | 客户端点击消息时跳转到的H5地址
oa.pc_message_url| String | 否 | PC端点击消息时跳转到的URL地址
oa.head | String | 是 | 消息头部内容
oa.head.bgcolor | String | 是 | 消息头部的背景颜色。长度限制为8个英文字符，其中前2为表示透明度，后6位表示颜色值。不要添加0x
oa.head.text | String | 是 | 消息的头部标题
oa.body | Array[JSON Object] | 是 | 消息体
oa.body.title | String | 否 | 消息体的标题
oa.body.form | Array[JSON Object] | 否 | 消息体的表单，最多显示6个，超过会被隐藏
oa.body.form.key | String | 否 | 消息体的关键字
oa.body.form.value | String | 否 | 消息体的关键字对应的值
oa.body.rich | JSON Object | 否 | 单行富文本信息
oa.body.rich.num | String | 否 | 单行富文本信息的数目
oa.body.rich.unit | String | 否| 单行富文本信息的单位
oa.body.content | String | 否 | 消息体的内容，最多显示3行
oa.body.image | String | 否 | 消息体中的图片media_id
oa.body.file_count | String | 否 | 自定义的附件数目。此数字仅供显示，钉钉不作验证
oa.body.author | String | 否 | 自定义的作者名字

### OA消息截图

![oames](https://img.alicdn.com/tps/TB1gVcFIFXXXXcGXXXXXXXXXXXX.jpg)

