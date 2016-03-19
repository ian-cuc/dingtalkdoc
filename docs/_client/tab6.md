# 启动器
- category: 客户端开发文档
- order: 7---
dd.device

## 检测应用是否安装

0.0.5

iOS平台仅对iOS9之前的系统有效

```javascript
dd.device.launcher.checkInstalledApps({
    apps: ['taobao', 'tmall'], //iOS:应用scheme;Android:应用包名
    onSuccess : function(data) {
        /*
        {
            installed: ['taobao', 'tmall'] //iOS:应用scheme;Android:应用包名
        }
        */
    },
    onFail : function(err) {}
});
```

#### 参数说明

参数 | 参数类型 | 说明
----- | ------- | ------
apps | Array[String] | iOS:应用scheme;Android:应用包名

#### 返回说明

参数 | 说明
---- | -----
installed | 安装过的应用列表

## 启动第三方应用

0.0.5

```javascript
dd.device.launcher.launchApp({
    app: 'taobao', //iOS:应用scheme;Android:应用包名
    activity :'DetailActivity', //仅限Android，打开指定Activity，可不传。如果为空，就打开App的Main入口Activity
    onSuccess : function(data) {
        /*
        {
            result: true //true 唤起成功 false 唤起失败
        }
        */
    },
    onFail : function(err) {}
});
```
#### 参数说明

参数 | 参数类型 | 说明
----- | ------- | -------
app | String | iOS:应用scheme;Android:应用包名

#### 返回说明

参数 | 说明
---- | -----
result | 值为true说明唤起成功，值为false说明唤起失败


## 获取当前网络类型

0.0.2

```javascript
dd.device.connection.getNetworkType({
    onSuccess : function(data) {
        /*
        {
            result: 'wifi' // result值: wifi 2g 3g 4g unknown none   none表示离线
        }
        */
    },
    onFail : function(err) {}
});
```
#### 返回说明

参数 | 说明
---- | -----
result | result值: wifi、2g、3g、4g、unknown、none，none表示离线


## 事件

支持事件： pause、resume、backbutton(android)


```
//退到后台(webview)
document.addEventListener('pause', function(e) {
    e.preventDefault();
    console.log('事件：pause')
}, false);

//唤醒(webview)
document.addEventListener('resume', function(e) {
    e.preventDefault();
    console.log('事件：resume')
}, false);


//返回按钮(android)
document.addEventListener('backbutton', function(e) {
    e.preventDefault();
    dd.device.notification.alert({
        message: '哎呀，你不小心点到返回键啦!',
        title: '...警告...'
    });
}, false);
```


