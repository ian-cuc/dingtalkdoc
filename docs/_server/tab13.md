# 统计数据
- category: 服务端开发文档
- order: 14---
## 记录统计数据

用户在使用微应用的时候，企业可以通过这个接口记录微应用使用的相关信息，比如调用时间，结束时间等等。钉钉的数据分析工具会对这些数据进行汇总。

##### 请求说明

Https请求方式：POST

`https://oapi.dingtalk.com/data/record?access_token=ACCESS_TOKEN`

##### 参数说明

参数 | 参数类型 | 必须 | 说明
---------- | ------- | ------- | ------
access_token | String | 是 | 调用接口凭证
startTimeMs | String | 是 | 事件发生时间，单位为距离1970的毫秒数
endTimeMs | String | 是 | 事件结束时间（瞬间结束的，该值和发生事件一致）
module | String | 否 | 微应用提供区分内部模块的标记
originId | String | 否 | 微应用中该记录的主键索引
userid | String | 是 | 员工在企业内的UserID，企业用来唯一标识用户的字段
agentId | String | 是 | 授权方应用id
callbackUrl | String | 是 | 针对该条数据的回调url
extension | JSONObject | 否 | 扩展字段，json格式,具体的业务数据模型的定义，请参考附录二，现只开放考勤类业务数据模型

#####  返回结果

```
{
    "errcode": 0,
    "id":"$:LWCP_v1:$t3G6JuXLNr7pd0fWOQKS2w==",
    "errmsg": "ok"
}
```
参数 |  说明
---------- | -------
id      | 数据标识id
errcode | 返回码
errmsg | 对返回码的文本描述内容

##更新统计数据

isv企业可以通过这个接口更新微应用数据，所更新的数据必须是通过/data/record接口插入的，现在只能更新module，callbackUrl，extension三个字段。

##### 请求说明

Https请求方式：POST

`https://oapi.dingtalk.com/data/update?access_token=ACCESS_TOKEN`

##### 参数说明

参数 | 参数类型 | 必须 | 说明
---------- | ------- | ------- | ------
id| String| 是|使用/data/record接口插入数据时返回的id
access_token | String | 是 | 调用接口凭证
startTimeMs | String | 是 | 事件发生时间，单位为距离1970的毫秒数
endTimeMs | String | 是 | 事件结束时间（瞬间结束的，该值和发生事件一致）
module | String | 否 | 微应用提供区分内部模块的标记
originId | String | 否 | 微应用中该记录的主键索引
userid | String | 是 | 员工在企业内的UserID，企业用来唯一标识用户的字段
agentId | String | 是 | 授权方应用id
callbackUrl | String | 是 | 针对该条数据的回调url
extension | JSONObject | 否 | 扩展字段，json格式,具体的业务数据模型的定义，请参考附录二，现只开放考勤类业务数据模型
#####  返回结果

```
{
"errcode": 0,
"errmsg": "ok"
}
```
参数 |  说明
---------- | -------
errcode | 返回码
errmsg | 对返回码的文本描述内容



