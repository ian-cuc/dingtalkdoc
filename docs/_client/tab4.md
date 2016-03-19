# 容器
- category: 客户端开发文档
- order: 5---
dd.runtime

## 获取容器信息

```javascript
dd.runtime.info({
    onSuccess: function(result) {
    /*{
        ability: '0.0.2' //容器版本，用来标识JSAPI能力，可根据该版本来决定能否使用jsapi
    }*/
    }
    onFail : function(err) {}

})
```

#### 返回说明

参数 | 说明
---- | -----
ability | 容器版本，用来标识JSAPI能力，可根据该版本来决定能否使用jsapi

## 获取免登授权码

0.0.5

```javascript
dd.runtime.permission.requestAuthCode({
	corpId: "corpid",
    onSuccess: function(result) {
    /*{
        code: 'hYLK98jkf0m' //string authCode
    }*/
    },
    onFail : function(err) {}

})
```
#### 参数说明

参数 | 参数类型 | 必须 | 说明
----- | ------- | ------- | ------
corpId | String | 是 | 企业ID

#### 返回说明

参数 | 说明
---- | -----
code | 授权码


<!--### 请求jsapi

0.0.5

```javascript
dd.runtime.permission.requestJsApis({
    corpId: '', //企业ID
    timeStamp: '', //生成签名的时间戳
    nonceStr: '', //生成签名的随机串
    signature: '', //签名
    jsApiList: [], //需要调用的jsapi列表
    onSuccess: function(result) {
    /*{
        jsApilist: [] //array[string] authJsApiList
    }*/
    }
})
```
#### 参数说明

参数 | 参数类型 | 必须 | 说明
----- | ------- | ------- | ------
corpId | String | 是 | 企业ID
timeStamp | String | 是 | 生成签名的时间戳
nonceStr | String | 是 | 生成签名的随机串
signature | String | 是 | 签名
jsApiList | array[string] | 是 | 需要调用的jsapi列表

#### 返回说明

参数 | 说明
---- | -----
jsApilist | 授权的JsApi列表
-->

