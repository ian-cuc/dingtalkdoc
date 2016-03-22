# 消息类型及数据格式
- category: 服务端开发文档
- order: 10---
## text消息

```
{
    "msgtype": "text",
    "text": {
        "content": "张三的请假申请"
    }
}
```

##### 参数说明

参数 | 参数类型 | 必须 | 说明
---------- | ------- | ------- | ------
msgtype |String | 是 | 消息类型，此时固定为：text
content |String | 是 | 消息内容

## image消息

```
{
    "msgtype": "image",
    "image": {
        "media_id": "MEDIA_ID"
    }
}
```

##### 参数说明

参数 | 参数类型 | 必须 | 说明
---------- | ------- | ------- | ------
msgtype |String | 是 | 消息类型，此时固定为：image
media_id | String | 是 | 图片媒体文件id，可以调用上传媒体文件接口获取。建议宽600像素 x 400像素，宽高比3：2

## voice消息

```
{
    "msgtype": "voice",
    "voice": {
       "media_id": "MEDIA_ID"
    }
}
```

##### 参数说明

参数 | 参数类型 | 必须 | 说明
---------- | ------- | ------- | ------
msgtype |String | 是 | 消息类型，此时固定为：voice
media_id |String | 是 | 语音媒体文件id，可以调用上传媒体文件接口获取。2MB，播放长度不超过60s，AMR格式

## file消息

```
{
    "msgtype": "file",
    "file": {
       "media_id": "MEDIA_ID"
    }
}
```

##### 参数说明

参数 | 参数类型 | 必须 | 说明
---------- | ------- | ------- | ------
msgtype | String| 是 | 消息类型，此时固定为：file
media_id |String | 是 | 媒体文件id，可以调用上传媒体文件接口获取。10MB


## link消息

```
{
    "msgtype": "link",
    "link": {
        "messageUrl": "http://s.dingtalk.com/market/dingtalk/error_code.php",
        "picUrl":"@lALOACZwe2Rk",
        "title": "测试",
        "text": "测试"
    }
}
```

##### 参数说明

参数 | 参数类型 | 必须 | 说明
---------- | ------- | ------- | ------
msgtype | String | 是 | 消息类型，此时固定为：link

#### link消息体格式

参数 | 参数类型 | 必须 | 说明
---------- | ------- | ------- | ------
link.messageUrl | String | 是 | 消息点击链接地址
link.picUrl | String | 是 | 图片媒体文件id，可以调用上传媒体文件接口获取
link.title | String | 是 | 消息标题
link.text | String | 是 | 消息描述

## OA消息

```
{
     "msgtype": "oa",
     "oa": {
        "message_url": "http://dingtalk.com",
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
msgtype |String | 是 | 消息类型，此时固定为：oa

### OA消息体内容

##### 参数说明

参数 | 参数类型 | 必须 | 说明
------ | ------- | ------- | ------
oa.message_url| String | 是 | 客户端点击消息时跳转到的H5地址
oa.pc_message_url| String | 否 | PC端点击消息时跳转到的H5地址
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

