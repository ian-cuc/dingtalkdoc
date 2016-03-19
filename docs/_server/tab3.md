# 管理微应用
- category: 服务端开发文档
- order: 4---
## 创建微应用

##### 请求说明

Https请求方式: POST

`https://oapi.dingtalk.com/microapp/create?access_token=ACCESS_TOKEN`

##### 请求包结构体

```
{
    "appIcon": "@HIdsabikkhjsdsas",
    "appName": "测试微应用",
    "appDesc": "测试使用的微应用",
    "homepageUrl": "http://oa.dingtalk.com/?h5",
    "pcHomepageUrl": "http://oa.dingtalk.com/?pc",
    "ompLink": ""
}
```

##### 参数说明

参数 | 参数类型 | 必须 | 说明
----------| ------- | ------- | ------
access_token | String | 是 | 调用接口凭证
appIcon | String | 是 |  微应用的图标。需要调用上传接口将图标上传到钉钉服务器后获取到的mediaId
appName | String | 是 | 微应用的名称。长度限制为1~10个字符
appDesc  | String | 是 | 微应用的描述。长度限制为1~20个字符
homepageUrl | String | 是 | 微应用的移动端主页，必须以http开头或https开头
pcHomepageUrl | String | 否 | 微应用的PC端主页，必须以http开头或https开头，如果不为空则必须与homepageUrl的域名一致
ompLink | String | 否 | 微应用的OA后台管理主页，必须以http开头或https开头

##### 返回结果

```
{
    "errcode": 0,
    "errmsg": "created",
    "id": 2
}
```

参数 | 说明
----------  | ------
errcode | 返回码
errmsg | 对返回码的文本描述内容
id | 创建的微应用id



##群会话接口


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

##客户通讯录接口（暂未开放）

您可以通过使用客户通讯接口，将您的CRM应用中的员工与客户的关系、客户与客户联系人的关系在钉钉客户端通讯录中展现，与钉钉有更深入的功能融合，对于用户来说客户关系与通讯录的紧密结合，更容易管理和联系核心客户

## 员工新增客户信息

##### 请求说明

Https请求方式: POST

`https://oapi.dingtalk.com/crm/customer/create?access_token=ACCESS_TOKEN&user_id=USER_ID`

##### 请求包结构体

```
{
"customer":[
{
"name":"姓名",
"address":"地址",
"description":"描述",
"telephone":"电话"
}
],
"contacts":[
{
"name":"姓名",
"mobile":"手机",
"attached":"备注"
}
],
"userIds":[
"USER_ID","USER_ID"
],
"create_by":"创建时间"
}

```

##### 参数说明

参数 | 参数类型 | 必须 | 说明
----------| ------- | ------- | ------
access_token | String | 是 | 调用接口凭证
user_id | String | 是 |  员工在企业内的userid
customer | JSONObject | 是 |  客户信息
name | String | 是 |  客户名称
address | String | 是 |  客户地址
description | String | 是 |  客户描述
telephone | String | 是 |  客户电话
contacts | JSONObject | 否 |  客户联系人信息
name | String | 否 |  客户联系人名称
mobile | String | 否 |  客户联系人手机
attached | String | 否 |  客户联系人备注
userIds | String[] | 否 |  跟进客户的员工信息
create_by | String | 是 |  创建时间

##### 返回结果

```
{
    "errcode": 0,
    "errmsg": "ok",
    "customerid": "xxxxxxxxxxxxxxxxxx"
}
```

参数 | 说明
----------  | ------
errcode | 返回码
errmsg | 对返回码的文本描述内容
customerid | 客户id

## 员工修改客户信息

##### 请求说明

Https请求方式: POST

`https://oapi.dingtalk.com/crm/customer/update?access_token=ACCESS_TOKEN&user_id=USER_ID`

##### 请求包结构体

```
{
"id":"客户id",
"name":"客户名称",
"address":"客户地址",
"description":"客户描述",
"telephone":"电话",
"modified_by":"修改时间"
}
```

##### 参数说明

参数 | 参数类型 | 必须 | 说明
----------| ------- | ------- | ------
access_token | String | 是 | 调用接口凭证
user_id | String | 是 | 员工id
id | String | 是 |  客户id
name | String | 否 | 客户名称
address  | String | 否 | 客户地址信息
description  | String | 否 | 客户描述信息
telephone  | String | 否 | 客户联系电话
modified_by  | String | 否 | 修改时间

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

## 员工删除客户

##### 请求说明

Https请求方式: POST

`https://oapi.dingtalk.com/crm/customer/delete?access_token=ACCESS_TOKEN&user_id=USER_ID`

##### 请求包结构体

```
{
"id[]":"客户id"
}

```

##### 参数说明

参数 | 参数类型 | 必须 | 说明
---------- | ------- | ------- | ------
access_token | String | 是 | 调用接口凭证
user_id | String | 是 | 会话id
id | String[] | 是 | 客户id

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


## 获取客户详细信息

##### 请求说明

Https请求方式: GET

`https://oapi.dingtalk.com/crm/customer/get?access_token=ACCESS_TOKEN&id=CUSTOMER_ID`

##### 参数说明

参数 | 参数类型 | 必须 | 说明
---------- | ------- | ------- | ------
access_token | String | 是 | 调用接口凭证
id | String | 是 | 客户id

##### 返回结果

```
{
"customer":{

"name":"客户名称",
"address":"客户地址",
"description":"客户描述",
"telephone":"客户电话"
},
"contactList":[
{
"name":"客户联系人名称",
"mobile":"客户联系人电话",
"attached":"客户联系人备注"
}
],
"userIds":[
                "USER_ID","USER_ID"
],
"create_by":"创建时间"
}
```

参数 | 说明
---- | -----
customer  |  客户信息
name |  客户名称
address  |  客户地址
description |  客户描述
telephone  |  客户电话
contacts  |  客户联系人信息
name  |  客户联系人名称
mobile  |  客户联系人手机
attached  |  客户联系人备注
userIds  |  跟进客户的员工信息
create_by  |  创建时间

## 获取客户列表

##### 请求说明

Https请求方式: GET

`https://oapi.dingtalk.com/crm/customer/get?access_token=ACCESS_TOKEN`

##### 参数说明

参数 | 参数类型 | 必须 | 说明
---------- | ------- | ------- | ------
access_token | String | 是 | 调用接口凭证

##### 返回结果

```
{
"customerlist":[
{
"name":"客户名称",
"address":"客户地址",
"description":"客户描述",
"telephone":"客户电话"
}
]
}
```

参数 | 说明
---- | -----
customerlist  |  客户列表信息
name |  客户名称
address  |  客户地址
description |  客户描述
telephone  |  客户电话

## 员工新增客户联系人

##### 请求说明

Https请求方式: POST

`https://oapi.dingtalk.com/crm/contact/create?access_token=ACCESS_TOKEN&user_id=USER_ID`

##### 请求包结构体

```
{
"customerid":"客户id",
"name":"客户联系人名称",
"mobile":"客户联系人手机",
"attached":"客户联系人备注",
"create_by":"创建时间"
}

```

##### 参数说明

参数 | 参数类型 | 必须 | 说明
---------- | ------- | ------- | ------
access_token |String | 是 | 调用接口凭证
user_id |String | 是 | 员工id
customerid  |  客户id
name  |  客户联系人名称
mobile  |  客户联系人手机
attached  |  客户联系人备注
create_by  |  创建时间

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

## 员工修改客户联系人

##### 请求说明

Https请求方式: POST

`https://oapi.dingtalk.com/crm/contact/create?access_token=ACCESS_TOKEN&user_id=USER_ID`

##### 请求包结构体

```
{
"contactid":"客户联系人id",
"name":"客户联系人名称",
"mobile":"客户联系人手机",
"attached":"客户联系人备注",
"modified_by":"修改时间"	  
}

```

##### 参数说明

参数 | 参数类型 | 必须 | 说明
---------- | ------- | ------- | ------
access_token |String | 是 | 调用接口凭证
user_id |String | 是 | 员工id
contactid |String | 是  |  客户id
name |String | 是  |  客户联系人名称
mobile  |String | 是 |  客户联系人手机
attached |String | 是   |  客户联系人备注
modified_by |String | 是   |  修改时间

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

## 员工删除客户联系人

##### 请求说明

Https请求方式: POST

`https://oapi.dingtalk.com/crm/contact/delete?access_token=ACCESS_TOKEN&user_id=USER_ID`

##### 请求包结构体

```
{
"contactid[]":"客户联系人id1"
}

```

##### 参数说明

参数 | 参数类型 | 必须 | 说明
---------- | ------- | ------- | ------
access_token |String | 是 | 调用接口凭证
user_id |String | 是 | 员工id
contactid  |String[] | 是  |  客户id
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

## 员工客户关系新增

##### 请求说明

Https请求方式: POST

`https://oapi.dingtalk.com/crm/empcustomer/create?access_token=ACCESS_TOKEN`

##### 请求包结构体

```
{
    "customerId":"客户id",
    "userId":"员工id",
    "create_by":"创建时间"
}

```

##### 参数说明

参数 | 参数类型 | 必须 | 说明
---------- | ------- | ------- | ------
access_token |String | 是 | 调用接口凭证
customerId |String | 是 | 客户id
userId  |String | 是  |  员工id
create_by  |String | 是  |  创建时间

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

## 员工客户关系删除

##### 请求说明

Https请求方式: POST

`https://oapi.dingtalk.com/crm/empcustomer/delete?access_token=ACCESS_TOKEN`

##### 请求包结构体

```
{
"customerId":"客户id",
"userId":"员工id",
"modified_by":"修改时间"
}

```

##### 参数说明

参数 | 参数类型 | 必须 | 说明
---------- | ------- | ------- | ------
access_token |String | 是 | 调用接口凭证
customerId |String | 是 | 客户id
userId  |String | 是  |  员工id
modified_by  |String | 是  |  修改时间

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

##通讯录及群会话变更事件回调接口

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




