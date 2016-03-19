# 弹窗
- category: 客户端开发文档
- order: 9---
dd.device

## alert

```javascript
dd.device.notification.alert({
    message: "亲爱的",
    title: "提示",//可传空
    buttonName: "收到",
    onSuccess : function() {
    	//onSuccess将在点击button之后回调
        /*回调*/
    },
    onFail : function(err) {}
});
```
<img src="https://gw.alicdn.com/tps/TB1.3UPJpXXXXbEXVXXXXXXXXXX-750-1334.jpg" width = "200" height = "355" alt="图片名称" align=right />

#### 参数说明

参数 | 参数类型 | 说明
----- | ----- | -----
message | String | 消息内容
title | String | 弹窗标题
buttonName | String |按钮名称



## confirm


```javascript
dd.device.notification.confirm({
    message: "你爱我吗",
    title: "提示",
    buttonLabels: ['爱', '不爱'],
    onSuccess : function(result) {
    	//onSuccess将在点击button之后回调
        /*
        {
            buttonIndex: 0 //被点击按钮的索引值，Number类型，从0开始
        }
        */
    },
    onFail : function(err) {}
});
```
<img src="https://img.alicdn.com/tps/TB1cL.KJpXXXXXJaXXXXXXXXXXX-750-1334.jpg" width = "200" height = "355" alt="图片名称" align=right />

#### 参数说明

参数 | 参数类型 | 说明
----- | ----- | -----
message | String | 消息说明
title | String |标题
buttonLabels | Array[String]| 按钮名称

#### 返回说明

参数 | 说明
---- | -----
buttonIndex | 被点击按钮的索引值，Number类型，从0开始

## prompt

```javascript
dd.device.notification.prompt({
    message: "再说一遍？",
    title: "提示",
    buttonLabels: ['继续', '不玩了'],
    onSuccess : function(result) {
        //onSuccess将在点击button之后回调
        /*
        {
            buttonIndex: 0, //被点击按钮的索引值，Number类型，从0开始
            value: '' //输入的值
        }
        */
    },
    onFail : function(err) {}
});
```
<img src="https://img.alicdn.com/tps/TB1lZZJJpXXXXazaXXXXXXXXXXX-750-1334.jpg" width = "200" height = "355" alt="图片名称" align=right />

#### 参数说明

参数 | 参数类型 | 说明
----- | ----- | -----
message | String |消息内容
title | String |标题
buttonLabels | Array[String] | 按钮名称

#### 返回说明

参数 | 说明
---- | -----
buttonIndex | 被点击按钮的索引值，Number类型，从0开始
value | 输入的值

## vibrate
震动

```javascript
dd.device.notification.vibrate({
    duration: 300, //震动时间，android可配置 iOS忽略
    onSuccess : function(result) {
        /*
        {}
        */
    },
    onFail : function(err) {}
})
```
#### 参数说明

参数 | 参数类型 | 说明
----- | ----- | -----
duration | Number | 震动时间，android可配置 iOS忽略

## showPreloader
（显示浮层，请和hidePreloader配对使用）

```javascript
dd.device.notification.showPreloader({
    text: "使劲加载中..", //loading显示的字符，空表示不显示文字
    showIcon: true, //是否显示icon，默认true
    onSuccess : function(result) {
        /*{}*/
    },
    onFail : function(err) {}
})
```
<img src="https://img.alicdn.com/tps/TB17bBXJFXXXXb3XXXXXXXXXXXX-750-1334.jpg" width = "200" height = "355" alt="图片名称" align=right />

#### 参数说明

参数 | 参数类型 | 说明
----- | ----- | -----
text | String | loading显示的字符，空表示不显示文字
showIcon | Boolean | 是否显示icon，默认true

## hidePreloader

```javascript
dd.device.notification.hidePreloader({
    onSuccess : function(result) {
        /*{}*/
    },
    onFail : function(err) {}
})
```

## toast

```javascript
dd.device.notification.toast({
    icon: '', //icon样式，有success和error，默认为空 0.0.2
    text: String, //提示信息
    duration: Number, //显示持续时间，单位秒，默认按系统规范[android只有两种(<=2s >2s)]
    delay: Number, //延迟显示，单位秒，默认0
    onSuccess : function(result) {
        /*{}*/
    },
    onFail : function(err) {}
})
```

<img src="https://img.alicdn.com/tps/TB1jjdJKVXXXXXbXpXXXXXXXXXX-200-356.jpg" alt="图片名称" align=right />

#### 参数说明

参数 | 参数类型 | 说明
----- | ----- | -----
icon | Boolean | icon样式，有success和error，默认为空 0.0.2
text | String | 提示信息
duration |  Number |显示持续时间，单位秒，默认按系统规范[android只有两种(<=2s >2s)]
delay | Number | 延迟显示，单位秒，默认0


## actionsheet
单选列表

0.0.2

```javascript
dd.device.notification.actionSheet({
    title: "谁是最棒哒？", //标题
    cancelButton: '取消', //取消按钮文本
    otherButtons: ["孙悟空","猪八戒","唐僧","沙和尚"],
    onSuccess : function(result) {
        //onSuccess将在点击button之后回调
        /*{
            buttonIndex: 0 //被点击按钮的索引值，Number，从0开始, 取消按钮为-1
        }*/
    },
    onFail : function(err) {}
})
```
<img src="https://img.alicdn.com/tps/TB1jn70JpXXXXXEXFXXXXXXXXXX-750-1334.jpg" width = "200" height = "355" alt="图片名称" align=right />

#### 参数说明

参数 | 参数类型 | 说明
----- | ----- | -----
title | String | 标题
cancelButton | String |取消按钮文本
otherButtons | Array[String] | 其他按钮列表

#### 返回说明

参数 | 说明
----- | -----
buttonIndex | 被点击按钮的索引值，Number，从0开始, 取消按钮为-1


## modal

modal弹浮层

```javascript
dd.device.notification.modal({
    image:"http://gw.alicdn.com/tps/i2/TB1SlYwGFXXXXXrXVXX9vKJ2XXX-2880-1560.jpg_200x200.jpg", // 标题图片地址
    title:"2.4版本更新", //标题
    content:"1.功能更新2.功能更新;", //文本内容
    buttonLabels:["了解更多","知道了"],// 最多两个按钮，至少有一个按钮。
    onSuccess : function(result) {
        //onSuccess将在点击button之后回调
        /*{
            buttonIndex: 0 //被点击按钮的索引值，Number，从0开始
        }*/
    },
    onFail : function(err) {}
})
```
<img src="https://img.alicdn.com/tps/TB1M1MKJpXXXXadaXXXXXXXXXXX-720-1280.jpg" width = "200" height = "355" alt="图片名称" align=right />

#### 参数说明

参数 | 参数类型 | 说明
----- | ----- | -----
image | String | 图片地址
title | String | 标题
content | String | 文本内容
buttonLabels | Array[String] | 其他按钮列表

#### 返回说明

参数 | 说明
----- | -----
buttonIndex | 被点击按钮的索引值，Number，从0开始


