# JS接口API
- category: 服务端开发文档
- order: 15---
## 获取jsapi_ticket

企业在使用微应用中的JS API时，需要先从钉钉开放平台接口获取jsapi_ticket生成签名数据，并将最终签名用的部分字段及签名结果返回到H5中，JS API底层将通过这些数据判断H5是否有权限使用JS API。

##### 请求说明
Https请求方式：GET

`https://oapi.dingtalk.com/get_jsapi_ticket?access_token=ACCESS_TOKE`

##### 参数说明
参数 | 参数类型 | 必须 | 说明
---------- | ------- | ------- | ------
access_token | String | 是 | 调用接口凭证
type | String | 是 | 这里是固定值，jsapi

#####  返回结果
正确时返回示例如下：

```
{
    "errcode": 0,
    "errmsg": "ok",
    "ticket": "dsf8sdf87sd7f87sd8v8ds0vs09dvu09sd8vy87dsv87",
    "expires_in": 7200
}
```

参数 | 说明
---------- | ------
errcode | 错误码
errmsg | 错误信息
ticket | 用于JS API的临时票据
expires_in | 票据过期时间

出错时返回示例如下：

```
{
    "errcode": 45009,
    "errmsg": "接口调用超过限制"
}
```

## JS-SDK

JS-SDK 为H5页面提供了一系列原生UI控件或者服务的JS接口，文档地址如下：

[<font color=red >客户端开发文档</font>](#客户端开发文档)


<!--## 管理日历接入指南
 钉钉提供微应用接入管理日历的能力。目前处于测试阶段，为了保证接入的质量以及良好的用户体验，接入方需要与钉钉管理日历团队协商接入方案。

由于不同接入方的业务不完全一致，如果接入方希望以与本文档不同的形式接入，可以向我们提出合作邀请，我们也提供定制化接入支持。（联系邮箱：pstar.zhangp@alibaba-inc.com）

管理日历目前已接入多个微应用，例如：签到、审批、考勤、日志、拜访计划等。
    
具体接入文档查看：[管理日历接入指南](http://download.taobaocdn.com/freedom/31112/pdf/p1a6htv7hq1o3p63g9ahpq51n5q4.pdf)
-->
