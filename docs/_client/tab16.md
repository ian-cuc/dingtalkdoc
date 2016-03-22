# 扫码
- category: 客户端开发文档
- order: 17---
dd.biz

0.0.6

```javascript
dd.biz.util.scan({
    type: String,//type为qrCode或者barCode
    onSuccess: function(data) {
    //onSuccess将在扫码成功之后回调
      /* data结构
        { 'text': String}
      */
    },
   onFail : function(err) {
   }
})
```

#### 参数说明

参数 | 参数类型 | 说明
----- | ----- | -----
type | String | type为qrCode或者barCode

####　返回说明

参数 | 说明
------|------
text | 扫码内容

