# 通用
- category: 客户端开发文档
- order: 4---
## 页面引入js文件

js文件版本在添加升级功能时地址会变化，如有需要（比如要使用新增的js-api）,请随时关注地址变更。但是旧版本js文件也将一直可用。

`http://g.alicdn.com/ilw/ding/0.7.5/scripts/dingtalk.js`

或者

`https://g.alicdn.com/ilw/ding/0.7.5/scripts/dingtalk.js`

## 全局变量、命名空间

直接引入dingtalk.js会得到一个全局变量`dd`，支持amd、cmd引入方式

全局变量dd，命名空间：设备(dd.device)、业务(dd.biz)

## 权限验证配置(beta)

钉钉JS API安全验证，只有经过安全验证的微应用才能调用安全级别较高的API。

获取JS-API权限验证使用的签名的方法请参考附录-[<font color=red >JS-API权限签名算法</font>](#js-api权限签名算法)

[<font color=red >jsapi权限验证配置demo--node.js版本</font>](https://github.com/injekt/jsapi-demo)

[<font color=red >jsapi权限验证配置demo--java版本</font>](https://github.com/injekt/openapi-demo-java)

[<font color=red >jsapi权限验证配置demo--php版本</font>](https://github.com/injekt/openapi-demo-php)


```javascript
 dd.config({
    agentId: '', // 必填，微应用ID
    corpId: '',//必填，企业ID
    timeStamp: , // 必填，生成签名的时间戳
    nonceStr: '', // 必填，生成签名的随机串
    signature: '', // 必填，签名
    jsApiList: ['device.notification.alert', 'device.notification.confirm'] // 必填，需要使用的jsapi列表
});
```

#### 参数说明

参数 | 参数类型 | 必须 | 说明
------ | ----- | ------| ------
agentId | String |是 | 微应用ID，普通企业可以通过OA后台的微应用－设置查看agentID，ISV需要通过调用授权成功后的get_auth_info获取授权方的agentid
corpId | String |是 | 企业ID
timeStamp | String |是 | 生成签名的时间戳
nonceStr | String |是 | 生成签名的随机串
signature | String |是 | 签名
jsApiList | Array | 是 | 需要调用的jsapi列表

## 通过ready接口处理成功验证

dd.ready参数为回调函数，在环境准备就绪时触发，jsapi的调用需要保证在该回调函数触发后调用，否则无效。

```javascript
dd.ready(function(){
    ;
});
```

## 通过error接口处理失败验证

config信息验证失败会执行error函数，错误信息可以在返回的error参数中参看

```javascript
dd.error(function(error){
    ;
});
```

## 接口约定

* 所有接口都为异步
* 接受一个object类型的参数
* 成功回调 onSuccess(某些异步接口的成功回调，将在事件触发时被调用，具体详情请查看相关onSuccess回调时机，未做描述的即为同步接口)
* 失败回调 onFail

```javascript
dd.命名空间.功能.方法({
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

