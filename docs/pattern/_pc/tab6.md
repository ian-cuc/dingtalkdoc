# 业务
- category: PC端开发文档
- order: 7---
DingTalkPC.biz



## 打开应用内页面

``` javascript
DingTalkPC.biz.util.open({
    name:'profile',//页面名称
    params:{
        id: '123456',// String 必选 用户工号
        corpId:'dingb4ff1079f84f8d54' //String 必选 企业id
    },//传参
    onSuccess : function() {
        /**/
    },
    onFail : function(err) {}
});
```

| 参数     | 参数类型       | 说明   |
| ------ | ---------- | ---- |
| name   | String     | 页面名称 |
| params | JSONObject | 传参   |

目前支持以下页面，具体参数看右边

1. 个人资料页

传参例子(右旁代码区)以及参数说明

``` 
{
    "name": "profile",
    "params":{
        "id": "123456",
        "corpId":"dingb4ff1079f84f8d54"
    },
    "onSuccess":function() {

    },
    "onFail":function(err) {}
}

```

| 参数            | 参数类型   | 必须   | 说明            |
| ------------- | ------ | ---- | ------------- |
| name          | String | 是    | 固定为 "profile" |
| params.id     | String | 是    | 用户工号          |
| params.corpId | String | 是    | 企业ID          |

<!--

b.聊天页面

``` javascript
// 页面名称：
    chat
// 传参：
    users: ['123'] 用户列表,工号
    corpId: '' //企业id
```

c.免费电话页面

``` javascript
// 页面名称：
    call
// 传参：
```

d.联系人添加页面

``` javascript
// 页面名称：
    contactAdd
// 传参：
```

f.唤起添加好友页面



``` 
// 页面名称：
    friendAdd
// 传参：
​``` -->

## 打开模态框（modal）

打开一个模态框

​```javascript
DingTalkPC.biz.util.openModal({
    size:'middle',  // modal的尺寸
    url: 'https://test.dingtalk.com/modal.html', //打开modal的内容的url
    title: 'modal title', //顶部标题
    onSuccess : function(result) {
        /*

        */
    },
    onFail : function() {}
})
```

<img src="http://gtms02.alicdn.com/tps/i2/TB1PqPwKFXXXXa8XFXXsaR5YpXX-1880-1276.png" width = "350" height = "" alt="图片名称" align=right />

#### 参数说明

| 参数    | 参数类型   | 说明                  |
| ----- | ------ | ------------------- |
| size  | String | 模态框的尺寸大小 三种选择 具体看下表 |
| url   | String | 模态框内部显示内容的url       |
| title | String | 模态框标题               |

#### 尺寸选择详情：

| 名称       | size输入   | 尺寸长宽               |
| -------- | -------- | ------------------ |
| （默认）大模态框 |          | 包括标题 676px * 545px |
| 中模态框     | "middle" | 包括标题 440px * 300px |
| 小模态框     | "mini"   | 包括标题 366px * 120px |

## 打开侧边面板（SlidePanel）

打开侧边面板

``` javascript
DingTalkPC.biz.util.openSlidePanel({
    url: 'about:blank', //打开侧边栏的url
    title: 'title', //侧边栏顶部标题
    onSuccess : function(result) {
        /*
        */
    },
    onFail : function() {}
})
```

<img src="http://gtms02.alicdn.com/tps/i2/TB1mzDBKFXXXXcTXpXXhMAQZVXX-1888-1278.png" width = "350" height = "" alt="图片名称" align=right />

#### 参数说明

| 参数    | 参数类型   | 说明             |
| ----- | ------ | -------------- |
| title | String | 侧边面板顶部显示标题     |
| url   | String | 侧边面板内部显示内容的url |

## 上传图片

选择图片+上传，防止恶意上传

``` javascript
DingTalkPC.biz.util.uploadImage({
    multiple: false, //是否多选，默认false
    max: 3, //最多可选个数
    onSuccess : function(result) {
        /*
        [
          'https://static.dingtalk.com/media/lADOA9bQH8zIzMg_200_200.jpg'
        ]
        */
    },
    onFail : function() {}
})
```

#### 参数说明

| 参数       | 参数类型    | 说明                |
| -------- | ------- | ----------------- |
| multiple | Boolean | 是否多选，默认false      |
| max      | Number  | Number为正整数，最多可选个数 |

## 下载文件

下载一个文件

``` javascript
DingTalkPC.biz.util.downloadFile({
    url: '//static.dingtalk.com/media/lADOADTWJM0C2M0C7A_748_728.jpg_60x60q90.jpg', //要下载的文件的url
    name: '一个图片.jpg', //定义下载文件名字
    onProgress: function(msg){
      // 文件下载进度回调
    },
    onSuccess : function(result) {
        /*
          true
        */
    },
    onFail : function() {}
})
```

<img src="http://gtms02.alicdn.com/tps/i2/TB1TfjCKFXXXXXwXFXXDZsQZVXX-1888-1280.png" width = "350" height = "" alt="图片名称" align=right />

#### 参数说明

| 参数         | 参数类型     | 说明                           |
| ---------- | -------- | ---------------------------- |
| url        | String   | 要下载文件的url                    |
| name       | String   | 定义下载文件的名字，记得添加文件扩展名，默认无文件扩展名 |
| onProgress | Function | 文件下载进度回调                     |

## 打开本地文件

打开本地文件接口

``` javascript
DingTalkPC.biz.util.openLocalFile({
    url: '', //本地文件的url
    onSuccess : function(result) {
        /*
          true
        */
    },
    onFail : function() {}
})
```

#### 参数说明

| 参数   | 参数类型   | 说明           |
| ---- | ------ | ------------ |
| url  | String | url是缓存文件的key |

## 批量检测本地文件是否存在

批量检测本地文件是否存在

``` javascript
DingTalkPC.biz.util.isLocalFileExist({
    params: [{
        url: '', //本地文件的url
      },{
        url: ''
      }
    ],
    onSuccess : function(result) {
        /*
          [{
              url: '', //本地文件的url
              path: '', // 文件的path
              isExist: true //根据你输入的文件的url检测出的结果，true:存在，false：不存在
          }]
        */
    },
    onFail : function() {}
})
```

#### 参数说明

| 参数   | 参数类型   | 说明           |
| ---- | ------ | ------------ |
| url  | String | url是缓存文件的key |

## 预览图片

``` javascript
DingTalkPC.biz.util.previewImage({
    urls: ['//static.dingtalk.com/media/1.jpg', '//static.dingtalk.com/media/2.jpg'],//图片地址列表
    current: '//static.dingtalk.com/media/1.jpg',//当前显示的图片链接
    onSuccess : function(result) {
        /**/
    },
    onFail : function() {}
})
```

<img src="http://gtms02.alicdn.com/tps/i2/TB1SaYsKFXXXXaIXVXXkOgK6FXX-1882-1276.png" width = "350" height = "" alt="图片名称" align=right />

#### 参数说明

| 参数      | 参数类型          | 说明        |
| ------- | ------------- | --------- |
| urls    | Array[String] | 图片地址列表    |
| current | String        | 当前显示的图片链接 |

## 在浏览器上打开链接

``` javascript
DingTalkPC.biz.util.openLink({
    url: "http://www.dingtalk.com",//要打开链接的地址
    onSuccess : function(result) {
        /**/
    },
    onFail : function() {}
})
```

| 参数   | 参数类型   | 说明       |
| ---- | ------ | -------- |
| url  | String | 要打开链接的地址 |

