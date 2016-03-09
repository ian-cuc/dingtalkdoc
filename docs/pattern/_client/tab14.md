# 电话
- category: 客户端开发文档
- order: 15---
dd.biz

## 打电话

0.0.3

```javascript
dd.biz.telephone.call({
    users: ['101', '102'], //用户列表，工号
    corpId: '', //企业id
    onSuccess : function() {},
    onFail : function() {}
})
```
#### 参数说明

参数 | 参数类型 |说明
----- | ----- | -----
users | Array[String] | 用户列表，工号
corpId | String | 企业id


