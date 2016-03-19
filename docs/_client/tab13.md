# Ding
- category: 客户端开发文档
- order: 14---
dd.biz

## 发钉

### 图片类型

0.0.3

```javascript
dd.biz.ding.post({
    users : ['100', '101'],//用户列表，工号
    corpId: '', //企业id
    type: 1, //钉类型 1：image  2：link
    alertType: 2,
    alertDate: {"format":"yyyy-MM-dd HH:mm","value":"2015-05-09 08:00"},
    attachment: {
        images: [''],
    }, //附件信息
    text: '', //消息
    onSuccess : function() {
    //onSuccess将在点击发送之后调用
    },
    onFail : function() {}
})
```
<img src="https://img.alicdn.com/tps/TB1h_JtKVXXXXbNXFXXXXXXXXXX-200-356.png" alt="图片名称" align=right />

#### 参数说明

参数 | 参数类型 | 说明
----- | ----- | -----
users | Array[String] | 用户列表，工号
corpId | String | 企业id
type | Number |Number为整数。钉类型 1：image，2：link
alertType |  Number |  钉提醒类型 0:电话, 1:短信, 2:应用内
alertDate |  Object  | 钉提醒时间
attachment | Object |附件信息
text | String |  消息

### Link类型

0.0.3

```javascript
dd.biz.ding.post({
    users : ['100', '101'],//用户列表，工号
    corpId: '', //企业id
    type: 2, //钉类型 1：image  2：link
    alertType: 2,
    alertDate: {"format":"yyyy-MM-dd HH:mm","value":"2015-05-09 08:00"},
    attachment: {
        title: '',
        url: '',
        image: '',
        text: ''
    }
    text: '', //消息
    onSuccess : function() {},
    onFail : function() {}
})
```
#### 参数说明

参数 | 参数类型 | 说明
----- | ----- | -----
users | Array[String] | 用户列表，工号
corpId | String | 企业id
type | Number |Number为整数。钉类型 1：image  2：link
alertType |  Number |  钉提醒类型 0:电话, 1:短信, 2:应用内
alertDate |  Object  | 钉提醒时间
attachment | Object | 附件信息
text | String |  消息

