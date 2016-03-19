# Ding
- category: PC端开发文档
- order: 9---
DingTalkPC.biz

## 发钉

### 图片类型



``` javascript
DingTalkPC.biz.ding.post({
    users : ['100', '101'],//用户列表，工号
    corpId: 'dingb4ff1079f84f8d54', //加密的企业id
    type: 1, //钉类型 1：image  2：link
    alertType: 2,
    alertDate: {"format":"yyyy-MM-dd HH:mm","value":"2015-05-09 08:00"},
    attachment: {
        images: [''], //只取第一个image
    }, //附件信息
    text: '', //消息体
    onSuccess : function() {},
    onFail : function() {}
})
```

#### 参数说明

| 参数         | 参数类型          | 说明                           |
| ---------- | ------------- | ---------------------------- |
| users      | Array[String] | 用户列表，工号                      |
| corpId     | String        | 企业id                         |
| type       | Number        | Number为整数。钉类型 1：image，2：link |
| alertType  | Number        | 钉提醒类型 0：电话, 1：短信, 2：应用内      |
| alertDate  | Object        | 钉提醒时间                        |
| attachment | Object        | 附件信息                         |
| text       | String        | 消息体                          |

### Link类型



``` javascript
DingTalkPC.biz.ding.post({
    users : ['100', '101'],//用户列表，工号
    corpId: 'dingb4ff1079f84f8d54', //企业id
    type: 2, //钉类型 1：image  2：link
    alertType: 2,
    alertDate: {"format":"yyyy-MM-dd HH:mm","value":"2015-05-09 08:00"},
    attachment: {
        title: '', //附件的标题
        url: '', //附件点击后跳转url
        image: '', //附件显示时的图片 【可选】
        text: '' //附件显示时的消息体 【可选】
    }
    text: '', //消息体
    onSuccess : function() {},
    onFail : function() {}
})
```

#### 参数说明

| 参数         | 参数类型          | 说明                            |
| ---------- | ------------- | ----------------------------- |
| users      | Array[String] | 用户列表，工号                       |
| corpId     | String        | 企业id                          |
| type       | Number        | Number为整数。钉类型 1：image  2：link |
| alertType  | Number        | 钉提醒类型 0：电话, 1：短信, 2：应用内       |
| alertDate  | Object        | 钉提醒时间                         |
| attachment | Object        | 附件信息                          |
| text       | String        | 消息体                           |

