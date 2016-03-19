# 弹窗
- category: PC端开发文档
- order: 6---
DingTalkPC.device

## alert

``` javascript
DingTalkPC.device.notification.alert({
    message: "亲爱的",
    title: "提示",//可传空
    buttonName: "收到",
    onSuccess : function() {
        /*回调*/
    },
    onFail : function(err) {}
});
```

<img src="http://gtms04.alicdn.com/tps/i4/TB1mXnaKFXXXXbvXVXXV8PWOVXX-1792-1200.png" width = "350" height = "" alt="图片名称" align=right />

#### 参数说明

| 参数         | 参数类型   | 说明   |
| ---------- | ------ | ---- |
| message    | String | 消息内容 |
| title      | String | 弹窗标题 |
| buttonName | String | 按钮名称 |

## confirm



``` javascript
DingTalkPC.device.notification.confirm({
    message: "你爱我吗",
    title: "提示",
    buttonLabels: ['爱', '不爱'],
    onSuccess : function(result) {
        /*
        {
            buttonIndex: 0 //被点击按钮的索引值，Number类型，从0开始
        }
        */
    },
    onFail : function(err) {}
});
```

<img src="http://gtms01.alicdn.com/tps/i1/TB1I4jbKFXXXXbBXVXX._qIYpXX-1794-1198.png" width = "350" height = "" alt="图片名称" align=right />

#### 参数说明

| 参数           | 参数类型          | 说明   |
| ------------ | ------------- | ---- |
| message      | String        | 消息说明 |
| title        | String        | 标题   |
| buttonLabels | Array[String] | 按钮名称 |

#### 返回说明

| 参数          | 说明                      |
| ----------- | ----------------------- |
| buttonIndex | 被点击按钮的索引值，Number类型，从0开始 |

## prompt

``` javascript
DingTalkPC.device.notification.prompt({
    message: "再说一遍？",
    title: "提示",
    buttonLabels: ['继续', '不玩了'],
    onSuccess : function(result) {
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

<img src="http://gtms02.alicdn.com/tps/i2/TB1iwLlKFXXXXbgXFXXFvH2OVXX-1792-1194.png" width = "350" height = "" alt="图片名称" align=right />

#### 参数说明

| 参数           | 参数类型          | 说明   |
| ------------ | ------------- | ---- |
| message      | String        | 消息内容 |
| title        | String        | 标题   |
| buttonLabels | Array[String] | 按钮名称 |

#### 返回说明

| 参数          | 说明                      |
| ----------- | ----------------------- |
| buttonIndex | 被点击按钮的索引值，Number类型，从0开始 |
| value       | 输入的值                    |

## toast

``` javascript
DingTalkPC.device.notification.toast({
    type: "information", //toast的类型 alert, success, error, warning, information, confirm
    text: '这里是个toast', //提示信息
    duration: 3, //显示持续时间，单位秒，最短2秒，最长5秒
    delay: 0, //延迟显示，单位秒，默认0, 最大限制为10
    onSuccess : function(result) {
        /*{}*/
    },
    onFail : function(err) {}
})
```

<img src="http://gtms03.alicdn.com/tps/i3/TB18p6hKFXXXXXBXVXXrQ409pXX-1786-1198.png" width ="350" height = "" alt="图片名称"  align=right />

#### 参数说明

| 参数       | 参数类型   | 说明                                       |
| -------- | ------ | ---------------------------------------- |
| type     | String | toast的类型 alert, success, error, warning, information, confirm，默认information |
| text     | String | 提示信息                                     |
| duration | Number | 显示持续时间，单位秒，最小2，最大限制为5                    |
| delay    | Number | 延迟显示，单位秒，默认0，最大限制为10                     |

## actionsheet

单选列表

``` javascript
DingTalkPC.device.notification.actionSheet({
    title: "谁是最棒哒？", //标题
    cancelButton: '取消', //取消按钮文本
    otherButtons: ["孙悟空","猪八戒","唐僧","沙和尚"],
    onSuccess : function(result) {
        /*{
            buttonIndex: 0 //被点击按钮的索引值，Number，从0开始, 取消按钮为-1
        }*/
    },
    onFail : function(err) {}
})
```

<img src="http://gtms04.alicdn.com/tps/i4/TB1mSvwKFXXXXX7XFXXpXX.QFXX-1886-1278.png" width = "350" height = "" alt="图片名称" align=right />

#### 参数说明

| 参数           | 参数类型          | 说明     |
| ------------ | ------------- | ------ |
| title        | String        | 标题     |
| cancelButton | String        | 取消按钮文本 |
| otherButtons | Array[String] | 其他按钮列表 |

#### 返回说明

| 参数          | 说明                             |
| ----------- | ------------------------------ |
| buttonIndex | 被点击按钮的索引值，Number，从0开始, 取消按钮为-1 |

