# 业务
- category: 客户端开发文档
- order: 12---
dd.biz


## 打开应用内页面

```
dd.biz.util.open({
    name:String,//页面名称
    params:JSONObject,//传参
    onSuccess : function() {
        /**/
    },
    onFail : function(err) {}
});
```

参数 | 参数类型 | 说明
----- | ----- | -----
name | String | 页面名称
params | JSONObject | 传参

目前支持以下页面，具体参数看右边

a.个人资料页

```
// 页面名称：
    profile
// 传参：
    id :用户工号 String
    corpId: '' //企业id
```

b.聊天页面

```
// 页面名称：
    chat
// 传参：
    users: ['123'] 用户列表,工号
    corpId: '' //企业id
```

c.免费电话页面

```
// 页面名称：
    call
// 传参：
```

d.联系人添加页面

```
// 页面名称：
    contactAdd
// 传参：
```

f.唤起添加好友页面


```
// 页面名称：
    friendAdd
// 传参：
```


## 分享

```javascript
dd.biz.util.share({
    type: Number,//分享类型，0:全部组件 默认； 1:只能分享到钉钉；2:不能分享，只有刷新按钮
    url: String,
    title: String,
    content: String,
    image: String,
    onSuccess : function() {
        //onSuccess将在分享完成之后回调
        /**/
    },
    onFail : function(err) {}
})
```
<img src="https://img.alicdn.com/tps/TB1L6RvKVXXXXa3XFXXXXXXXXXX-200-356.jpg" alt="图片名称" align=right />

#### 参数说明

参数 | 参数类型 |  说明
----- | ----- | -----
type | Number | 分享类型，0:全部组件默认； 1:只能分享到钉钉；2:不能分享，只有刷新按钮
url | String | url地址
title | String | 分享标题
content | String | 分享内容
image | String |分享的图片


## ut数据埋点
ISV与钉钉进行数据对接的数据埋点接口，用于采集用户数据，ISV可根据微应用中关键操作进行埋点

```javascript
dd.biz.util.ut({
    key: String,//打点名
    value: String/JSONObject,//打点传值
    onSuccess : function() {
        /**/
    },
    onFail : function(err) {}
})
```
#### 参数说明

参数 | 参数类型 | 说明
----- | ----- | -----
key | String | 打点名，目前建议值open_micro_general_operat
value | String | 打点传值，必须传入’corpId':'传入corpId','agentId':'传入agentId','type':'传入type’；type(由isv自由提供的点击类型，默认可以传空)


<!--### 选取图片[暂不开放]

```javascript
dd.biz.util.chooseImage({
    multiple: false, //是否多选，默认false
    destType: String, //返回格式 DATA_URL(base64编码) FILE_URI(文件路径)，默认FILE_URI
    onSuccess : function(result) {
        /**/
    },
    onFail : function() {}
})
```
-->

## 上传图片
选择图片+上传，防止恶意上传

将在成功上传之后回调onSuccess方法，返回alicdn上的图片链接。微应用也可以调用`<input type="file" accept="image/*">`来自定义上传图片，此标签钉钉客户端版本2.5及以上支持。

```javascript
dd.biz.util.uploadImage({
    multiple: false, //是否多选，默认false
    max: 3, //最多可选个数
    onSuccess : function(result) {
    	//onSuccess将在图片上传成功之后调用
        /*
        [
          'http://gtms03.alicdn.com/tps/i3/TB1VF6uGFXXXXalaXXXmh5R_VXX-237-236.png'
        ]
        */
    },
    onFail : function() {}
})
```
<img src="https://img.alicdn.com/tps/TB1FhFlKVXXXXbNXVXXXXXXXXXX-200-356.png" alt="图片名称" align=right />

#### 参数说明

参数 | 参数类型 | 说明
----- | ----- | -----
multiple | Boolean | 是否多选，默认false
max | Number | Number为正整数，最多可选个数


## 上传图片（仅支持拍照上传）
只支持直接拍照上传，即调用这个API之后将直接调起相机界面

比如可以应用在，需要用户上传即时照片的场景。成功上传之后回调onSuccess方法，返回图片链接
```javascript
dd.biz.util.uploadImageFromCamera({
    compression:true,//(是否压缩，默认为true)
    onSuccess : function(result) {
    	 //onSuccess将在图片上传成功之后调用
        /*
        [
          'http://gtms03.alicdn.com/tps/i3/TB1VF6uGFXXXXalaXXXmh5R_VXX-237-236.png'
        ]
        */
    },
    onFail : function() {}
})
```
#### 参数说明

参数 | 参数类型 |说明
----- | ----- | -----
compression | Boolean | 图片地址列表


## 图片浏览器

调用此api，将显示一个图片浏览器

```javascript
dd.biz.util.previewImage({
    urls: [String],//图片地址列表
    current: String,//当前显示的图片链接
    onSuccess : function(result) {
        /**/
    },
    onFail : function() {}
})
```

<img src="https://img.alicdn.com/tps/TB1UjhmKVXXXXboXVXXXXXXXXXX-200-356.jpg" alt="图片名称" align=right />

#### 参数说明

参数 | 参数类型 |说明
----- | ----- | -----
urls | Array[String] | 图片地址列表
current | String | 当前显示的图片链接

<!-- ### 扫码

```javascript
dd.biz.util.qrcode({
    onSuccess : function(result) {
        /*
        {
            text: String
        }
        */
    },
    onFail : function(err) {}
})
```
#### 返回说明
参数 | 说明
----- | ------
text | 扫码的内容 -->


## 日期选择器

日期

注意：format只支持android系统规范，即2015-03-31格式为yyyy-MM-dd

```javascript
dd.biz.util.datepicker({
    format: 'yyyy-MM-dd',
    value: '2015-04-17', //默认显示日期
    onSuccess : function(result) {
        //onSuccess将在点击完成之后回调
        /*{
            value: "2015-02-10"
        }
        */
    },
    onFail : function() {}
})
```
<img src="https://img.alicdn.com/tps/TB1bcRLKVXXXXb8XXXXXXXXXXXX-200-356.png" width = "200" height = "355" alt="图片名称" align=right />

#### 参数说明

参数 | 参数类型 | 说明
----- | ----- | -----
format | String | format只支持android系统规范，即2015-03-31格式为yyyy-MM-dd
value | String | 默认显示日期

####　返回说明
参数 | 说明
----- | ------
value | 返回选择的日期

时间

```javascript
dd.biz.util.timepicker({
    format: 'HH:mm',
    value: '14:00', //默认显示时间  0.0.3
    onSuccess : function(result) {
        //onSuccess将在点击完成之后回调
        /*{
            value: "10:00"
        }
        */
    },
    onFail : function() {}
})
```
#### 参数说明

参数 | 参数类型 | 说明
----- | ----- | -----
format | String | 时间格式
value | String | 默认显示时间

####　返回说明
参数 | 说明
----- | ------
value | 返回选择的时间

日期+时间

0.0.4

```javascript
dd.biz.util.datetimepicker({
    format: 'yyyy-MM-dd HH:mm',
    value: '2015-04-17 08:00', //默认显示
    onSuccess : function(result) {
        //onSuccess将在点击完成之后回调
        /*{
            value: "2015-06-10 09:50"
        }
        */
    },
    onFail : function() {}
})
```
#### 参数说明

参数 | 参数类型 | 说明
----- | ----- | -----
format |String | 日期和时间的格式
value | String | 默认显示的日期和时间

####　返回说明
参数 | 说明
----- | ------
value | 返回选择的日期和时间

## 下拉控件

0.0.5

```javascript
dd.biz.util.chosen({
    source:[{
        key: '选项1', //显示文本
        value: '123' //值，
    },{
        key: '选项2',
        value: '234'
    }],
    onSuccess : function(result) {
    //onSuccess将在点击完成之后回调
        /*
        {
            key: '选项2',
            value: '234'
        }
        */
    },
    onFail : function() {}
})
```
<img src="https://img.alicdn.com/tps/TB177sWJpXXXXbeXFXXXXXXXXXX-750-1334.jpg" width = "200" height = "355" alt="图片名称" align=right />

#### 参数说明

参数 | 参数类型 |  说明
----- | ----- | -----
source | Array[String] | 下拉控件的内容
key | String | 显示文本
value | String | 文本对应的值

####　返回说明
参数 | 说明
----- | ------
key | 返回选择的文本
value | 返回选择的值

