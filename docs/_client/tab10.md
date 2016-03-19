# 加速器
- category: 客户端开发文档
- order: 11---
dd.device

## 摇一摇

开启监听

```javascript
dd.device.accelerometer.watchShake({
    sensitivity: 20,//振动幅度，Number类型，加速度变化超过这个值后触发shake
    frequency: 150,//采样间隔(毫秒)，Number类型，指每隔多长时间对加速度进行一次采样， 然后对比前后变化，判断是否触发shake
    callbackDelay: 3000,//触发『摇一摇』后的等待时间(毫秒)，Number类型，防止频繁调用
    onSuccess : function(result) {
        /*
        {}
        */
    },
    onFail : function(err) {}
});
```
#### 参数说明

参数 | 参数类型 | 说明
----- | ----- | -----
sensitivity | Number |振动幅度，Number类型，加速度变化超过这个值后触发shake
frequency | Number | 采样间隔(毫秒)，Number类型，指每隔多长时间对加速度进行一次采样， 然后对比前后变化，判断是否触发shake
callbackDelay| Number |触发『摇一摇』后的等待时间(毫秒)，Number类型，防止频繁调用


清除监听

```javascript
dd.device.accelerometer.clearShake({
    onSuccess : function(result) {
        /* 调用成功
        */
    },
    onFail : function(err) {}
});
```


