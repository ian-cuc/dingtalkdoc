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



