# 设备
- category: 客户端开发文档
- order: 6---
dd.device

## 基础信息

## 获取通用唯一识别码

0.0.5

```javascript
dd.device.base.getUUID({
    onSuccess : function(data) {
        /*
        {
            uuid: '3udbhg98ddlljokkkl' //
        }
        */
    },
    onFail : function(err) {}
});
```

#### 返回说明

参数 | 说明
---- | -----
uuid | 通用唯一识别码

## 获取热点接入信息

0.0.5

```javascript
dd.device.base.getInterface({
    onSuccess : function(data) {
        /*
        {
            ssid: 'alibaba-inc',
            macIp: '3c:12:aa:09'
        }
        */
    },
    onFail : function(err) {}
});
```

#### 返回说明

参数 | 说明
---- | -----
ssid | 热点ssid
macIp | 热点mac地址

