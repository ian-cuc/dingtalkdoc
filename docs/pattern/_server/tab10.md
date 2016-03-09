# 管理多媒体文件
- category: 服务端开发文档
- order: 11---
企业在使用接口时，对多媒体文件、多媒体消息的获取和调用等操作，是通过media_id来进行的。通过本接口，企业可以上传或下载多媒体文件。

## 上传媒体文件

用于上传图片、语音等媒体资源文件以及普通文件（如doc，ppt），接口返回媒体资源标识ID：media_id。请注意，media_id是可复用的，同一个media_id可用于消息的多次发送。

##### 请求说明

Https请求方式: POST

`https://oapi.dingtalk.com/media/upload?access_token=ACCESS_TOKEN&type=TYPE`

##### 参数说明

参数 | 参数类型 | 必须 | 说明
---------- | ------- | ------- | ------
access_token | String | 是 | 调用接口凭证
type |String | 是 | 媒体文件类型，分别有图片（image）、语音（voice）、普通文件(file)
media |String | 是 | form-data中媒体文件标识，有filename、filelength、content-type等信息

##### 返回结果

```
{
    "errcode": 0,
    "errmsg": "ok",
    "type": "image",
    "media_id": "@dsa8d87y7c8d8c"
}
```

参数 |说明
---------- | ------
errcode | 错误码
errmsg | 错误信息
type | 媒体文件类型，分别有图片（image）、语音（voice）、普通文件(file)
media_id | 媒体文件上传后获取的唯一标识
created_at | 媒体文件上传时间戳

##### 上传的媒体文件限制

* 图片（image）:1MB，支持JPG格式
* 语音（voice）：2MB，播放长度不超过60s，AMR格式
* 普通文件（file）：10MB

## 获取媒体文件

通过media_id获取图片、语音等文件。



##### 请求说明

Https请求方式: GET

`https://oapi.dingtalk.com/media/get?access_token=ACCESS_TOKEN&media_id=MEDIA_ID`


##### 参数说明

```
  HTTP/1.1 200: OK
  Connection: close
  Content-Type: image/jpeg
  Content-disposition: attachment; filename="MEDIA_ID.jpg"
  Date: Sun, 04 Jan 2015 12:00:00 GMT
  Cache-Control: no-cache, must-revalidate
  Content-Length: 1234567
  ...
```

参数 |参数类型 | 必须 | 说明
---------- | ------- | ------- | ------
access_token |String | 是 | 调用接口凭证
media_id |String | 是 | 媒体文件的唯一标示


##### 返回说明


和普通的http下载相同，请根据http头做相应的处理。


a)正确时返回：

```
{
    "errcode": 40004,
    "errmsg": "invalid media_id"
}
```

b)错误时返回（这里省略了HTTP首部）：

