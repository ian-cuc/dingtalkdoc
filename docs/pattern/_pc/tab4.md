# 通用
- category: PC端开发文档
- order: 5---
## 页面引入js文件

js文件版本在添加升级功能时地址会变化，如有需要（比如要使用新增的js-api）,请随时关注地址变更。但是旧版本js文件也将一直可用。

`http://g.alicdn.com/dingding/dingtalk-pc-api/2.3.1/index.js`



## 全局变量、命名空间

直接引入index.js会得到一个全局变量`DingTalkPC `，支持amd、cmd引入方式

全局变量DingTalkPC，命名空间：设备(DingTalkPC.device)、业务(DingTalkPC.biz)

## 权限验证配置(beta)

钉钉JS API安全验证，只有经过安全验证的微应用才能调用安全级别较高的API。

获取JS-API权限验证使用的签名的方法请参考附录-[<font color=red >JS-API权限签名算法</font>](#js-api权限签名算法)

[<font color=red >jsapi权限验证配置demo--node.js版本</font>](https://github.com/injekt/jsapi-demo)

[<font color=red >jsapi权限验证配置demo--java版本</font>](https://github.com/injekt/openapi-demo-java)

[<font color=red >jsapi权限验证配置demo--php版本</font>](https://github.com/injekt/openapi-demo-php)



``` javascript
 DingTalkPC.config({
    agentId: '', // 必填，微应用ID
    corpId: '',//必填，企业ID
    timeStamp: , // 必填，生成签名的时间戳
    nonceStr: '', // 必填，生成签名的随机串
    signature: '', // 必填，签名
    jsApiList: ['device.notification.alert', 'device.notification.confirm'] // 必填，需要使用的jsapi列表
});
```

#### 参数说明

| 参数        | 参数类型   | 必须   | 说明           |
| --------- | ------ | ---- | ------------ |
| agentId   | String | 是    | 微应用ID        |
| corpId    | String | 是    | 企业ID         |
| timeStamp | String | 是    | 生成签名的时间戳     |
| nonceStr  | String | 是    | 生成签名的随机串     |
| signature | String | 是    | 签名           |
| jsApiList | Array  | 是    | 需要调用的jsapi列表 |

## 通过ready接口处理成功验证

DingTalkPC.ready参数为回调函数，在环境准备就绪时触发，jsapi的调用需要保证在该回调函数触发后调用，否则无效。

``` javascript
DingTalkPC.ready(function(res){
  /*{
      authorizedAPIList: ['device.notification.alert'], //已授权API列表
      unauthorizedAPIList: [''], //未授权API列表
  }*/
  //接口操作应该在ready后才可调用
});
```

## 通过error接口处理失败验证

config信息验证失败会执行error函数，错误信息可以在返回的error参数中参看

``` javascript
DingTalkPC.error(function(error){
  /*{
      errorCode: 1001, //错误码
      errorMessage: '', //错误信息
  }*/
});
```

## 接口约定

* 所有接口都为异步
* 接受一个object类型的参数
* 成功回调 onSuccess
* 失败回调 onFail

``` javascript
DingTalkPC.命名空间.功能.方法({
    参数1: '',
    参数2: '',
    onSuccess: function(result) {
    //成功回调
    /*
    {
        //所有返回信息都输出在这里
    }*/
    },
    onFail: function(){
    //失败回调
    }
})
```



## PC版获取免登授权码



``` javascript
DingTalkPC.runtime.permission.requestAuthCode({
    corpId: "", //企业ID
    onSuccess: function(result) {
    /*{
        code: 'hYLK98jkf0m' //string authCode
    }*/
    },
    onFail : function(err) {}

})
```

#### 参数说明

| 参数     | 参数类型   | 必须   | 说明   |
| ------ | ------ | ---- | ---- |
| corpId | String | 是    | 企业ID |

#### 返回说明

| 参数   | 说明   |
| ---- | ---- |
| code | 授权码  |

