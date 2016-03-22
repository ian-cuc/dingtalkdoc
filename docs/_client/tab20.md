# 附录
- category: 客户端开发文档
- order: 21---
## JS-API权限签名算法

如果开发者想使用钉钉容器开放的jsapi接口，需要经过以下流程：

- 首先需要[<font color=red >获取jsapi_ticket</font>](#获取jsapi_ticket)。

- 然后在web页面加载到钉钉容器时，通过[<font color=red >jsapi权限验证配置接口</font>](#页面引入js文件)验证可用的jsapi。这个接口使用的参数signature，在下文中有详细的说明。

### 1.获取jsapi_ticket
jsapi_ticket,是开发者调用钉钉JS接口的临时授权码，其作用主要用于生成签名，这个签名在[<font color=red >jsapi权限验证配置接口</font>](http://open.dingtalk.com/#页面引入js文件)中使用。

正常的情况下，jsapi_ticket的有效期为7200秒，通过access_token（注意，假如您是ISV开发者，这个access_token需要[<font color=red >企业授权的access_token接口</font>](#8-获取企业授权的access_token)）来获取。由于频繁刷新jsapi_ticket会导致api调用受限，影响自身业务，开发者必须在自己的服务全局缓存jsapi_ticket。
获取jsapi_ticket，具体可以[<font color=red >参考文档</font>](#js接口api)
### 2.签名生成算法
开发者在web页面使用钉钉容器提供的jsapi时，需要验证调用权限，并以参数signature标识合法性

签名生成的规则：

List keyArray = sort(noncestr,timestamp,jsapi_ticket,url);

String str = assemble(keyArray);

signature = sha1(str);

参与签名的字段包括在上文中获取的jsapi_ticket，noncestr（随机字符串，自己随便填写即可）,timestamp（当前时间戳，具体值为当前时间到1970年1月1号的秒数）,url（当前网页的URL，不包含#及其后面部分）。例如：

- noncestr=Zn4zmLFKD0wzilzM
- jsapi_ticket=mS5k98fdkdgDKxkXGEs8LORVREiweeWETE40P37wkidkfksDSKDJFD5h9nbSlYy3-Sl-HhTdfl2fzFy1AOcKIDU8l
- timestamp=1414588745
- url=http://open.dingtalk.com

步骤1. sort()含义为对所有待签名参数按照字段名的ASCII 码从小到大排序（字典序）

步骤2. assemble()含义为根据步骤1中获的参数字段的顺序，使用URL键值对的格式（即key1=value1&key2=value2…）拼接成字符串

步骤2. sha1()的含义为对在步骤2拼接好的字符串进行sha1加密。

## 图片缩放

通过JS-API获取的图片都支持缩放，比如图片：

`http://gtms02.alicdn.com/tps/i2/TB1SlYwGFXXXXXrXVXX9vKJ2XXX-2880-1560.jpg`

可通过文件名拼接的方法缩放为最大宽高为250x250的尺寸。

`http://gtms02.alicdn.com/tps/i2/TB1SlYwGFXXXXXrXVXX9vKJ2XXX-2880-1560.jpg_250x250.jpg`

拼接规则为:文件名+拼接规则；推荐使用以下拼接规则：



80x80 => _80x80.jpg

120x120 => _120x120.jpg

250x250 => _250x250.jpg

310x310 => _310x310.jpg

## 容器能力

[device.notification.alert](#alert)

[device.notification.confirm](#confirm)

[device.notification.prompt](#prompt)

[device.notification.vibrate](#vibrate)

[device.accelerometer.watchShake](#摇一摇)

[device.accelerometer.clearShake](#摇一摇)

[biz.util.open](#打开应用内页面)

[biz.util.share](#分享)

[biz.util.ut](#ut打点)

[biz.util.datepicker](#日期选择器) //android

[biz.util.timepicker](#日期选择器) //android

[biz.contact.choose](#选人)

<!--
[biz.user.get](#get)
-->

[biz.navigation.setLeft](#设置左侧导航按钮)

[biz.navigation.setRight](#设置右侧导航按钮)

[biz.navigation.setTitle](#设置标题)



// v0.0.1

[device.notification.toast](#toast)

[device.notification.showPreloader](#showpreloader)

[device.notification.hidePreloader](#hidepreloader)

[device.geolocation.get](#获取当前地理位置)

[biz.util.uploadImage](#上传图片)

[biz.util.previewImage](#图片浏览器)

//v0.0.2

[ui.input.plain](#输入框)

[device.notification.actionSheet](#actionsheet)

[device.connection.getNetworkType](#获取当前网络类型)

[runtime.info](#获取容器信息)

//v0.0.3

[biz.ding.post](#发钉)

[biz.telephone.call](#打电话)

//v0.0.4

[biz.contact.createGroup](#创建企业群聊天)

[biz.util.datetimepicker](#日期选择器)

//v0.0.5

[biz.util.chosen](#下拉控件)

[device.base.getUUID](#获取通用唯一识别码)

[device.base.getInterface](#获取热点接入信息)

[device.launcher.checkInstalledApps](#检测应用是否安装)

[device.launcher.launchApp](#启动第三方应用)

[ui.progressBar.setColors](#设置顶部进度条颜色)

[runtime.permission.requestAuthCode](#获取免登授权码)

[ui.pullToRefresh.enable](#启用下拉刷新)

[ui.pullToRefresh.stop](#收起下拉loading)

[ui.pullToRefresh.disable](#禁用下拉刷新)

[ui.webViewBounce.enable](#启用bounce)

[ui.webViewBounce.disable](#启用bounce)

[biz.navigation.close](#触发关闭)

//0.0.6

[biz.util.scan](#扫码)

[biz.contact.complexChoose](#选人，选部门)

//0.0.7

[biz.chat.pickConversation](#获取会话信息)

//0.0.8

[device.notification.modal](#modal)

[biz.util.uploadImageFromCamera](#上传图片（仅支持拍照上传）)

//0.0.11

[biz.chat.chooseConversationByCorpId](#根据corpid选择会话)

[biz.chat.toConversation](#根据chatid跳转到对应会话)



