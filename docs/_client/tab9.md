# 地图
- category: 客户端开发文档
- order: 10---
dd.device

## 获取当前地理位置

钉钉Android2.1及之前版本返回的数据会多嵌套一层location字段,2.2版本会改成和钉钉iOS客户端一致，请注意，建议对返回的数据先判断存在location，做向后兼容处理。

目前androidJSAPI返回的坐标是高德坐标，ios是标准坐标，如果服务端调用的是高德API，则需要对ios返回的经纬度做下处理，详细请见[<font color=red >http://lbsbbs.amap.com/forum.php?mod=viewthread&tid=724&page=2</font>](http://lbsbbs.amap.com/forum.php?mod=viewthread&tid=724&page=2)。坐标转换API [<font color=red >http://lbs.amap.com/api/javascript-api/example/p/1602-2/</font>](http://lbs.amap.com/api/javascript-api/example/p/1602-2/)

```javascript
dd.device.geolocation.get({
	targetAccuracy : Number,
    onSuccess : function(result) {
        /*
        {
            longitude : Number,
            latitude : Number,
            accuracy : Number,
            isWifiEnabled : Boolean,
            isGpsEnabled : Boolean,
            isFromMock : Boolean,
            provider : wifi|lbs|gps,
            accuracy : Number,
            isMobileEnabled : Boolean,
            errorMessage : String,
			errorCode : Number
        }
        */
    },
    onFail : function(err) {}
});
```

#### 参数说明

参数 | 参数类型 | 说明
----- | ----- | -----
targetAccuracy | Number | 期望定位精度半径（单位米），定位结果尽量满足该参数要求，但是不一定能保证小于该误差


#### 返回说明

参数 | 说明
----- | -----
longitude | 经度
latitude | 纬度
accuracy | 实际的定位精度半径（单位米）
isWifiEnabled | wifi设置是否开启，不保证已连接上
isGpsEnabled | gps设置是否开启，不保证已经连接上
isFromMock | 定位返回的经纬度是否是模拟的结果
provider | 我们使用的是混合定位，具体定位提供者有wifi/lbs/gps" 这三种
isMobileEnabled | 移动网络是设置是否开启，不保证已经连接上
errorMessage | 对错误码的描述
errorCode | 错误码
<!--

## 搜索
0.0.6

```javascript
dd.biz.map.search({
  scope: Number, //定位范围
  extraInfo: {
	  prompt: "提示信息"
  }
  onSuccess: function(data) {
  /* data结构
	  {
	  "province": ""//省
	  "provinceCode": "" //省份编码
	  "city": "" //城市
	  "cityCode": "" //城市编码
	  "adCode": "" // POI的行政区划代码
	  "adName": "" // POI的行政区划名称
	  "distance": "" //获取POI距离中心点的距离
	  "postCode": "" //返回POI的邮编
	  "title": "" //POI的名称
	  "snippet": "" //POI的地址
	  "longitude": 11.11, //该点经度
	  "latitude": 11.11, //该点纬度
	  }
  */
  },
  onFail : function(err) {
  }
})
```
#### 参数说明

参数 | 参数类型 | 说明
----- | ----- | -----
scope | Number | 定位范围
extraInfo.prompt | String | 提示信息

#### 返回说明

参数 | 说明
----- | -----
province | 省份
provinceCode | 省份编码
city | 城市
cityCode | 城市编码
adCode | POI的行政区划代码
adName | POI的行政区划名称
distance | 获取POI距离中心点的距离
postCode | 返回POI的邮编
title | POI的名称
snippet | POI的地址
longitude | 该点经度
latitude | 该点纬度

##定位
0.0.6

```javascript
dd.biz.map.locate({
  onSuccess: function(data) {
   /* data结构
	  {
	  "province": ""//省
	  "provinceCode": "" //省份编码
	  "city": "" //城市
	  "cityCode": "" //城市编码
	  "adCode": "" // POI的行政区划代码
	  "adName": "" // POI的行政区划名称
	  "distance": "" //获取POI距离中心点的距离
	  "postCode": "" //返回POI的邮编
	  "title": "" //POI的名称
	  "snippet": "" //POI的地址
	  "longitude": 11.11, //该点经度
	  "latitude": 11.11, //该点纬度
	  }
  */
  },
  onFail : function(err) {
  }
})
```

#### 返回说明

参数 | 说明
----- | -----
province | 省份
provinceCode | 省份编码
city | 城市
cityCode | 城市编码
adCode | POI的行政区划代码
adName | POI的行政区划名称
distance | 获取POI距离中心点的距离
postCode | 返回POI的邮编
title | POI的名称
snippet | POI的地址
longitude | 该点经度
latitude | 该点纬度

-->

