# 自定义联系人
- category: 客户端开发文档
- order: 19---
dd.biz

## 单选自定义联系人

选取单个自定义联系人

```javascript
dd.biz.customContact.choose({
    title: '选人的标题', //标题
    users: ['10001', '10002', ...],//一组员工工号
    corpId: 'dingb4ff1079f84f8d54',//加密的企业 ID，
    isShowCompanyName: true,   //true|false，默认为 false
    onSuccess: function(data) {
    /* data结构
      [{
        "name": "张三", //姓名
        "avatar": "http://g.alicdn.com/avatar/zhangsan.png" //头像图片url，可能为空
        "emplId": '0573', //工号
       },
       ...
      ]
    */
    },
    onFail : function(err) {}
});
```

#### 参数说明

参数 | 参数类型 | 说明
----- | ----- | -----
corpId | String | 企业ID
users | Array[String] | 一组员工工号
isShowCompanyName | Boolean | 是否显示公司名称
title | String | 标题

####　返回说明

参数 | 说明
------|------
name | 姓名
avatar | 头像图片url，可能为空
emplId | 工号


## 多选自定义联系人

选取多个自定义联系人

```javascript
dd.biz.customContact.multipleChoose({
    title: '多选人的标题', //标题
    users: ['10001', '10002', ...],//一组员工工号
    corpId: 'dingb4ff1079f84f8d54',//企业 ID，
    isShowCompanyName: false,   //true|false，默认为 false
    selectedUsers: ["18658"], //默认选中的人
    disabledUsers: ["78308"], //不能选的人
    max: 10, //人数限制
    onSuccess: function(data) {
    /* data结构
      [{
        "name": "张三", //姓名
        "avatar": "http://g.alicdn.com/avatar/zhangsan.png" //头像图片url，可能为空
        "emplId": '0573', //工号
       },
       ...
      ]
    */
    },
    onFail : function(err) {}
});
```

#### 参数说明

参数 | 参数类型 | 说明
----- | ----- | -----
corpId | String | 企业ID
users | Array[String] | 是否多选： true多选，false单选； 默认true
isShowCompanyName | Boolean | 默认选中的用户列表，工号；成功回调中应包含该信息
title | String | 选择窗口的标题
selectedUsers | Array[String] | 默认选中的人
disabledUsers | Array[String] | 不能选的人
max | Number | 人数限制


####　返回说明

参数 | 说明
------|------
name | 姓名
avatar | 头像图片url，可能为空
emplId | 工号




