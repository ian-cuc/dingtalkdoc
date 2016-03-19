# 附录
- category: PC端开发文档
- order: 12---## PC UI规范

PC UI规范：[<font color=red >地址</font>](https://img.alicdn.com/tps/TB1G75xLVXXXXXjaXXXXXXXXXXX-4416-3528.jpg)

## JS-API权限签名算法

如果开发者想使用钉钉容器开放的jsapi接口，需要经过以下流程：

- 首先需要[<font color=red >获取jsapi_ticket</font>](#获取jsapi_ticket)。
- 然后在web页面加载到钉钉容器时，通过[<font color=red >jsapi权限验证配置接口</font>](#页面引入js文件)验证可用的jsapi。这个接口使用的参数signature，在下文中有详细的说明。

### 1.获取jsapi_ticket

jsapi_ticket,是开发者调用钉钉JS接口的临时授权码，其作用主要用于生成签名，这个签名在[<font color=red >jsapi权限验证配置接口</font>](http://open.dingtalk.com/#页面引入js文件)中使用。

正常的情况下，jsapi_ticket的有效期为7200秒，通过access_token来获取。由于频繁刷新jsapi_ticket会导致api调用受限，影响自身业务，开发者必须在自己的服务全局缓存jsapi_ticket。

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

<!--

## 容器能力

[runtime.permission.requestAuthCode](#获取免登授权码)

[device.notification.alert](#alert)

[device.notification.confirm](#confirm)

[device.notification.prompt](#prompt)

[device.notification.toast](#toast)

[device.notification.actionSheet](#actionSheet)

[biz.util.open](#打开应用内页面)

[biz.util.openModal](#打开模态框（modal）)

[biz.util.openSlidePanel](#打开侧边面板（SlidePanel）)

[biz.util.uploadImage](#上传图片)

[biz.util.downloadFile](#下载文件)

[biz.util.openLocalFile](#打开文件)

[biz.util.isLocalFileExist](#批量检测文件是否存在)

[biz.util.previewImage](#预览图片)

[biz.util.openLink](#在浏览器上打开链接)

[biz.navigation.quit](#触发关闭)

[biz.navigation.setTitle](#设置标题)

[biz.navigation.setLeft](#设置左侧导航按钮)

[biz.ding.post](#发钉)

[biz.contact.choose](#选人)

[biz.customContact.choose](#单选自定义联系人)

[biz.customContact.multipleChoose](#多选自定义联系人) -->