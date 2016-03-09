# ISV接入开发指南
- category: ISV接入指南
- order: 6---
## 1: ISV接口调用整体流程
欢迎成为钉钉套件（微应用）的服务提供商！
通过接入钉钉ISV的应用授权接口，可以快速发布自己的微应用套件，并在企业客户授权开通微应用时，自动进行开通激活，企业用户可以授权后直接使用您的套件（应用）！

钉钉的应用授权接口包含以下两个阶段：

### ISV注册套件（微应用）

当前您经过[<font color=red >注册钉钉开发者</font>](#注册钉钉开发者)
和[<font color=red >创建套件&微应用</font>](#创建套件&微应用)之后，
已经注册成为钉钉开发者，并在开发者平台中创建好了套件及应用，您需要实现钉钉回调接口，实现[<font color=red >回调接口</font>](#2-回调接口（分为五个回调类型）)中的验证url有效性和定时推送Ticket，实现这俩个回调之后您就可以开发您的套件（微应用）了。

### 企业管理员授权套件（微应用）

当您开发好套件之后，您需要[<font color=red >注册测试企业</font>](#3-注册测试企业)进行管理员授权应用模拟，
您可以在『授权管理』中进行授权操作，授权成功后，您需要立即激活套件，确保测试企业可以正常使用套件中的功能。

当您的套件发布后，当企业管理员通过钉钉提供的 微应用的第三方授权页面 确认授权内容后，**<font color=red>ISV需要立即激活套件，从用户授权至套件激活整体应在5s内完成</font>**,授权以及激活完成之后，企业就可使用ISV服务提供商所提供的应用服务了。

以下是套件从开发到企业开始使用套件的详细的接口调用时序图
![Mou icon](https://img.alicdn.com/tps/TB1b1fdLXXXXXXTXVXXXXXXXXXX-896-702.jpg)

## 2: 回调接口（分为五个回调类型）
### 使用场景
使用回调接口主要用来实现2个场景：
- 创建套件（微应用）后将其注册至钉钉，与之关联的回调接口为a.验证回调URL有效性事件；b: 定时推送Ticket
- 企业用户在使用您的套件（微应用）之前，需要通过钉钉进行授权与激活，与之关联的回调接口为 c:回调向ISV推送临时授权码；d:回调向ISV推送授权变更消息；e."套件信息更新"事件；f."解除授权"事件；g."校验序列号"事件

### 调用说明
在使用回调接口之前您需要了解的是，
首先要拿到您创建套件时填写的"回调URL"，"Token"，"数据加密密钥(ENCODING_AES_KEY)"，

- 回调URL:服务提供商接收推送请求的协议和地址

- Token:服务提供商在注册时任意填写的，用来生成signature，用来和回调参数中的signature比对，校验消息的合法性

- 数据加密密钥(ENCODING_AES_KEY):用于消息体的加解密。

钉钉服务器会向服务提供商申请时填写的套件回调URL定时推送SuiteTicket，以及临时授权码和授权设置变更。

以[服务端demo java版本](http://ddtalk.github.io/dingTalkDoc/?spm=a3140.7785475.0.0.Ju6sXi#加解密库和demo下载)做示例，您提供的回调URL是

`http://您服务端部署的IP:您的端口/demo/isvreceive`

那么在钉钉服务器每一次访问回调URL的时候
将请求(下面链接中的signature,timestamp,nonce的值只是示例，并不代表真实返回的值):

`http://您服务端部署的IP:您的端口/demo/isvreceive?signature=111108bb8e6dbce3c9671d6fdb69d15066227608
&timestamp=1783610513&nonce=380320111`

```
{
	"encrypt":"1ojQf0NSvw2WPvW7LijxS8UvISr8pdDP+rXpPbcLGOmIBNbWetRg7IP0vdhVgkVwSoZBJeQwY2zhROsJq/HJ+q6tp1qhl9L1+ccC9ZjKs1wV5bmA9NoAWQiZ+7MpzQVq+j74rJQljdVyBdI/dGOvsnBSCxCVW0ISWX0vn9lYTuuHSoaxwCGylH9xRhYHL9bRDskBc7bO0FseHQQasdfghjkl"
}
```

回调数据的格式如右所示：

其中的encrypt字段是经过加密的消息体，encrypt经过一系列解密步骤后，才能产生下面所说的“POST数据解密后示例”，服务提供商可以直接使用钉钉提供的库进行解密的处理。

除此之外，在接收到推送之后，**需要返回相应的加密字符串（代表了你收到了推送）**，如果ISV未能成功返回，钉钉服务器将持续推送下去，达到100次后将不再推送。

"Talk is cheap, show me the code."所以我们也为开发者提供了加解密的demo，目前提供Java/PHP等语言版本。
加解密库和demo的下载：[<font color=red >加解密库和demo下载</font>](#加解密库和demo下载)

本地调试：[<font color=red >如何本地进行调试？</font>](#调试工具)

如有需要，可以查看具体加解密步骤：[<font color=red >加解密方案说明</font>](#加解密方案说明)


### 接口说明

### a.<font color=red >验证回调URL有效性事件</font>

此事件的推送会发生在注册套件，点击下图按钮之时。注意，若未能成功验证回调URL有效性，套件将不能被创建。

![verifyurl](https://img.alicdn.com/tps/TB1RuHzJFXXXXahXVXXXXXXXXXX-615-100.jpg)

```
dingTalkEncryptor = new DingTalkEncryptor(Env.TOKEN, Env.ENCODING_AES_KEY, Env.CREATE_SUITE_KEY);//套件在创建中，使用默认的SUITE_KEY进行加解密

```

此时，由于套件尚未创建成功，还未生成套件的SUITE_KEY，所以在解密post数据的时候，需要使用默认的Env.CREATE_SUITE_KEY（默认值为"suite4xxxxxxxxxxxxxxx"）来解密，以java-demo代码为例（Env为Demo中配置文件），如右，服务端demo已经做了配置。

同时，Demo的配置文件（Env.java）中还需要根据套件创建时填写的TOKEN 和 ENCODING_AES_KEY做相应的更改。

![verifyurl](https://img.alicdn.com/tps/TB1LK2kLXXXXXasXFXXXXXXXXXX-1338-1072.png)


待成功处理『验证回调URL有效性事件』事件，套件创建成功之后，就不能再使用默认的SUITE_KEY了，需要使用套件本身的SUITE_KEY，所以需要在Env.java中配置SUITE_KEY，同时将新创建套件中的SUITE_SECRET配置到Env.java中，然后重新部署代码，此时将用下面的语句进行加解密。因为推送ticket是二十分钟推送一次，再次部署也需要等待二十分钟服务端才会推送，后续会优化该逻辑，保证即时推送，提高推送效率。


`dingTalkEncryptor = new DingTalkEncryptor(Env.TOKEN, Env.ENCODING_AES_KEY, Env.SUITE_KEY);//套件创建成功后，使用套件本身的SUITE_KEY进行加解密`



POST数据解密后示例

```

{

  "EventType":"check_create_suite_url",
  "Random":"brdkKLMW",
  "TestSuiteKey":"suite4xxxxxxxxxxxxxxx"

}

```


参数      | 说明
-------   | -------------
Random  | 随机字符串
EventType | check_create_suite_url
TestSuiteKey  | 校验的SuiteKey

#### 返回说明

服务提供商在收到此事件推送后务必返回包含经过加密后"Random"字段的json数据，比如对于上面的示例，需要返回的即是加密后的"brdkKLMW"字符串。

只有返回了对应的json数据，钉钉才会判断此事件推送成功，套件才能创建成功。

```

{
  "msg_signature":"111108bb8e6dbce3c9671d6fdb69d15066227608",
  "timeStamp":"1783610513",
  "nonce":"123456",
  "encrypt":"1ojQf0NSvw2WPvW7LijxS8UvISr8pdDP+rXpPbcLGOmIBNbWetRg7IP0vdhVgkVwSoZBJeQwY2zhROsJq/HJ+q6tp1qhl9L1+ccC9ZjKs1wV5bmA9NoAWQiZ+7MpzQVq+j74rJQljdVyBdI/dGOvsnBSCxCVW0ISWX0vn9lYTuuHSoaxwCGylH9xRhYHL9bRDskBc7bO0FseHQQasdfghjkl" // "Random"字段的加密数据
}

```

参数      | 说明
-------   | -------------
msg_signature  | 消息体签名
timeStamp | 时间戳
nonce  | 随机字符串
encrypt  | "Random"字段的加密字符串

### b: 定时推送Ticket

服务器会向服务提供商申请时填写的套件事件接收 URL定时（二十分钟）推送ticket：


服务提供商在收到ticket推送后务必返回经过加密的字符串"success"的json数据，同时，如果该套件下没有任何的微应用，定时推送的ticket也不会成功，需要保证至少有一个ticket。


如果不返回，钉钉服务器将连续推送，直到推送次数超过100次，就不再推送。倘若您希望钉钉服务器重新推送，需要进入[<font color=red>开发者后台</font>](http://console.d.aliyun.com)，进入套件管理页面，点击『重新推送』按钮，即可重新推送。
![repush](https://img.alicdn.com/tps/TB15j7OJFXXXXckXXXXXXXXXXXX-1121-124.jpg)

以[服务端demo java版本](http://ddtalk.github.io/dingTalkDoc/?spm=a3140.7785475.0.0.Ju6sXi#加解密库和demo下载)做示例，每二十分钟服务端会向服务商提供的接口进行一次回调，可以在IsvReceiveServlet.java文件中，打印并获取Env.suiteTicket。在[debug平台](https://debug.dingtalk.com/isv.html)获取套件的SuiteAccessToken。

POST数据解密后示例

```
{
  "SuiteKey": "suitexxxxxx",
  "EventType": "suite_ticket ",
  "TimeStamp": 1234456,
  "SuiteTicket": "adsadsad"
}
```

参数			| 说明
-------		| -------------
SuiteKey	| 应用套件的SuiteKey
EventType	| suite_ticket
TimeStamp	| 时间戳
SuiteTicket	| Ticket内容

#### 返回说明

服务提供商在收到此事件推送后务必返回包含经过加密的字符串"success"的json数据

只有返回了对应的json数据，钉钉才会判断此事件推送成功，套件才能创建成功。

```

{
  "msg_signature":"111108bb8e6dbce3c9671d6fdb69d15066227608",
  "timeStamp":"1783610513",
  "nonce":"123456",
  "encrypt":"1ojQf0NSvw2WPvW7LijxS8UvISr8pdDP+rXpPbcLGOmIBNbWetRg7IP0vdhVgkVwSoZBJeQwY2zhROsJq/HJ+q6tp1qhl9L1+ccC9ZjKs1wV5bmA9NoAWQiZ+7MpzQVq+j74rJQljdVyBdI/dGOvsnBSCxCVW0ISWX0vn9lYTuuHSoaxwCGylH9xRhYHL9bRDskBc7bO0FseHQQasdfghjkl" // "Random"字段的加密数据
}

```

参数      | 说明
-------   | -------------
msg_signature  | 消息体签名
timeStamp | 时间戳
nonce  | 随机字符串
encrypt  | "success"加密字符串


### c:回调向ISV推送临时授权码

当授权方（即授权企业）在微应用管理端的授权管理中，向服务提供商的应用套件授权了访问权限，钉钉服务器会向服务提供商的套件事件接收 URL（创建套件时填写）推送临时授权码，

比如在[<font color=red>钉钉开发者后台</font>](http://console.d.aliyun.com)中，模拟测试企业发起授权，钉钉服务器就会向回调url推送测试企业的临时授权码

![shouqun](https://img.alicdn.com/tps/TB1rZerKpXXXXX8XXXXXXXXXXXX-720-124.jpg)


以[服务端demo java版本](http://ddtalk.github.io/dingTalkDoc/?spm=a3140.7785475.0.0.Ju6sXi#加解密库和demo下载)做示例，可以在IsvReceiveServlet.java文件中，打印并获取Env.authCode。在[debug平台](https://debug.dingtalk.com/isv.html)获取套件的永久授权码，请将永久授权码保存下来，目前永久授权码丢失之后没法再次获取，只能创建套件重新来，后续会优化该逻辑，解决临时授权码只能获取一次永久授权码的问题。

POST数据解密后示例

```
{
  "SuiteKey": "suitexxxxxx",
  "EventType": " tmp_auth_code",
  "TimeStamp": 1234456,
  "AuthCode": "adads"
}
```

字段说明

参数			| 说明
-------		| -------------
SuiteKey	| 应用套件的SuiteKey
EventType	| tmp_auth_code
TimeStamp	| 时间戳
AuthCode	| 临时授权码

#### 返回说明

服务提供商在收到此事件推送后务必返回包含经过加密的字符串"success"的json数据

只有返回了对应的json数据，钉钉才会判断此事件推送成功，套件才能创建成功。

```

{
  "msg_signature":"111108bb8e6dbce3c9671d6fdb69d15066227608",
  "timeStamp":"1783610513",
  "nonce":"123456",
  "encrypt":"1ojQf0NSvw2WPvW7LijxS8UvISr8pdDP+rXpPbcLGOmIBNbWetRg7IP0vdhVgkVwSoZBJeQwY2zhROsJq/HJ+q6tp1qhl9L1+ccC9ZjKs1wV5bmA9NoAWQiZ+7MpzQVq+j74rJQljdVyBdI/dGOvsnBSCxCVW0ISWX0vn9lYTuuHSoaxwCGylH9xRhYHL9bRDskBc7bO0FseHQQasdfghjkl" // "Random"字段的加密数据
}

```

参数      | 说明
-------   | -------------
msg_signature  | 消息体签名
timeStamp | 时间戳
nonce  | 随机字符串
encrypt  | "success"加密字符串


### d:回调向ISV推送授权变更消息

当授权方（即授权企业）在微应用管理端中，修改了对套件的授权托管后，钉钉服务器会向服务提供商的套件事件接收 URL（创建套件时填写）推送授权变更消息。注意，推送的授权变更信息并不包括企业用户具体做了什么修改，所以收到推送之后,

**ISV需要通过调用[<font color=red >获取企业的应用信息</font>](#7-获取企业的应用信息)接口**，获取接口返回值其中的"close"参数，才能得知微应用在企业用户做了授权变更之后的状态，有三种状态码，分别为0，1，2.含义如下：

- 0:禁用（例如企业用户在OA后台禁用了微应用）
- 1:正常 (例如企业用户在禁用之后又启用了微应用)
- 2:待激活 (企业已经进行了授权，但是ISV还未为企业激活应用)

再根据具体状态做具体操作。比如状态为2，就需要ISV为企业进行激活授权套件的操作。

POST数据解密后示例

```
{
  "SuiteKey": "suitexxxxxx",
  "EventType": " change_auth",
  "TimeStamp": 1234456,
  "AuthCorpId": "xxxxx"
}
```

字段说明

参数			| 说明
-------		| -------------
SuiteKey	| 应用套件的SuiteKey
EventType	| change_auth
TimeStamp	| 时间戳
AuthCorpId	| 授权方企业的corpid

#### 返回说明

服务提供商在收到此事件推送后务必返回包含经过加密的字符串"success"的json数据

只有返回了对应的json数据，钉钉才会判断此事件推送成功，套件才能创建成功。

```

{
  "msg_signature":"111108bb8e6dbce3c9671d6fdb69d15066227608",
  "timeStamp":"1783610513",
  "nonce":"123456",
  "encrypt":"1ojQf0NSvw2WPvW7LijxS8UvISr8pdDP+rXpPbcLGOmIBNbWetRg7IP0vdhVgkVwSoZBJeQwY2zhROsJq/HJ+q6tp1qhl9L1+ccC9ZjKs1wV5bmA9NoAWQiZ+7MpzQVq+j74rJQljdVyBdI/dGOvsnBSCxCVW0ISWX0vn9lYTuuHSoaxwCGylH9xRhYHL9bRDskBc7bO0FseHQQasdfghjkl" // "Random"字段的加密数据
}

```

参数      | 说明
-------   | -------------
msg_signature  | 消息体签名
timeStamp | 时间戳
nonce  | 随机字符串
encrypt  | "success"加密字符串



### e."套件信息更新"事件

此事件的推送会发生在更新套件信息的时候。

POST数据解密后示例

```

{
  "EventType":"check_update_suite_url",
  "Random":"Aedr5LMW",
  "TestSuiteKey":"suited6db0pze8yao1b1y"

}

```

服务提供商在收到"套件信息更新"事件推送后务必返回经过加密后"Random"字段，比如对于右边的示例，需要返回的即是加密后的"Aedr5LMW"字符串。


参数			| 说明
-------		| -------------
Random	| 随机字符串
EventType	| check_update_suite_url
TestSuiteKey	| 校验的SuiteKey(此处为套件的SuiteKey)

#### 返回说明

服务提供商在收到此事件推送后务必返回包含经过加密后"Random"字段的json数据，比如对于上面的示例，需要返回的即是加密后的"Aedr5LMW"字符串。

只有返回了对应的json数据，钉钉才会判断此事件推送成功，套件才能创建成功。

```

{
  "msg_signature":"111108bb8e6dbce3c9671d6fdb69d15066227608",
  "timeStamp":"1783610513",
  "nonce":"123456",
  "encrypt":"1ojQf0NSvw2WPvW7LijxS8UvISr8pdDP+rXpPbcLGOmIBNbWetRg7IP0vdhVgkVwSoZBJeQwY2zhROsJq/HJ+q6tp1qhl9L1+ccC9ZjKs1wV5bmA9NoAWQiZ+7MpzQVq+j74rJQljdVyBdI/dGOvsnBSCxCVW0ISWX0vn9lYTuuHSoaxwCGylH9xRhYHL9bRDskBc7bO0FseHQQasdfghjkl" // "Random"字段的加密数据
}

```

参数      | 说明
-------   | -------------
msg_signature  | 消息体签名
timeStamp | 时间戳
nonce  | 随机字符串
encrypt  | "Random"字段的加密字符串


### f."解除授权"事件

此事件的推送会发生在企业解除套件授权的时候。

**发生了"解除授权"事件之后，原来的永久授权码将立即失效**，假设企业用户又重新发起授权，ISV将收到临时授权码换取以换取新的永久授权码

POST数据解密后示例

```

{
  "EventType":"suite_relieve",
  "SuiteKey":"suited6db0pze8yao1b1y",
  "TimeStamp":"12351458245",
  "AuthCorpId":"ding4583267d28sd61"
}

```

服务提供商在收到"解除授权"事件推送后务必返回包含经过加密的字符串"success"的json数据。


参数			| 说明
-------		| -------------
SuiteKey	| 应用套件的SuiteKey
EventType	| suite_relieve
TimeStamp	| 时间戳
AuthCorpId	|授权方企业的corpid

#### 返回说明

服务提供商在收到"解除授权"事件推送后务必返回包含经过加密的字符串"success"的json数据。

只有返回了对应的json数据，钉钉才会判断此事件推送成功。

```

{
  "msg_signature":"111108bb8e6dbce3c9671d6fdb69d15066227608",
  "timeStamp":"1783610513",
  "nonce":"123456",
  "encrypt":"1ojQf0NSvw2WPvW7LijxS8UvISr8pdDP+rXpPbcLGOmIBNbWetRg7IP0vdhVgkVwSoZBJeQwY2zhROsJq/HJ+q6tp1qhl9L1+ccC9ZjKs1wV5bmA9NoAWQiZ+7MpzQVq+j74rJQljdVyBdI/dGOvsnBSCxCVW0ISWX0vn9lYTuuHSoaxwCGylH9xRhYHL9bRDskBc7bO0FseHQQasdfghjkl" // "Random"字段的加密数据
}

```

参数      | 说明
-------   | -------------
msg_signature  | 消息体签名
timeStamp | 时间戳
nonce  | 随机字符串
encrypt  | "success"字段的加密字符串


### g."校验序列号"事件

此事件的推送会发生在企业开通套件输入序列号的时候,要求请求立即返回。

POST数据解密后示例

```

{
  "EventType":"check_suite_license_code",
  "TimeStamp":15481221,
  "SuiteKey":"suited6db0pze8yao1b1y"
  "AuthCorpId":"dingxxxxxxxx"
  "LicenseCode":"xxxxxxxx"
}

```

服务提供商在收到"校验序列号"事件推送后,判断该LicenseCode是否合法,如果合法则返回加密"success"。返回其它值或者不返回视为LicenseCode不合法


参数			| 说明
-------		| -------------
TimeStamp	| 时间戳
EventType	| check_suite_license_code
SuiteKey	| 校验的SuiteKey(此处为套件的SuiteKey)
AuthCorpId	| 使用该套件企业的corpid
LicenseCode	| 企业使用套件输入的序列号
#### 返回说明

服务提供商在收到"校验序列号"事件推送后,判断该LicenseCode是否合法,如果合法返回加密"success"。返回其它值或者不返回作为不合法处理


```

{
  "msg_signature":"111108bb8e6dbce3c9671d6fdb69d15066227608",
  "timeStamp":"1783610513",
  "nonce":"123456",
  "encrypt":"1ojQf0NSvw2WPvW7LijxS8UvISr8pdDP+rXpPbcLGOmIBNbWetRg7IP0vdhVgkVwSoZBJeQwY2zhROsJq/HJ+q6tp1qhl9L1+ccC9ZjKs1wV5bmA9NoAWQiZ+7MpzQVq+j74rJQljdVyBdI/dGOvsnBSCxCVW0ISWX0vn9lYTuuHSoaxwCGylH9xRhYHL9bRDskBc7bO0FseHQQasdfghjkl" // "Random"字段的加密数据
}

```

参数      | 说明
-------   | -------------
msg_signature  | 消息体签名
timeStamp | 时间戳
nonce  | 随机字符串
encrypt  | 加密字符串


## 3: 获取套件访问Token（suite_access_token）
### 使用场景

该API用于获取应用套件令牌（suite_access_token）
### 接口说明

接口调用请求说明
https请求方式: POST
https://oapi.dingtalk.com/service/get_suite_token

POST数据示例

```
{
	"suite_key":"key_value",
 	"suite_secret": "secret_value",
	"suite_ticket": "ticket_value"
}
```

请求参数说明

参数				| 说明
-------			| -------------
suite_key		| 应用套件的key
suite_secret	| 应用套件secret
suite_ticket	| 钉钉后台推送的ticket


返回结果示例

```
{
	"suite_access_token":"61W3mEpU66027wgNZ_MhGHNQDHnFATkDa9-2llqrMBjUwxRSNPbVsMmyD-yq8wZETSoE5NQgecigDrSHkPtIYA", 	"expires_in":7200
}
```

结果参数说明

参数		| 说明
-------	| -------------
suite_access_token	| 应用套件access_token
expires_in			| 有效期


## 4: 获取企业的永久授权码
### 使用场景

该API用于使用临时授权码换取授权方的永久授权码，并换取授权信息、企业access_token。得到永久授权码之后请将永久授权码存储下来。

注：临时授权码使用一次后即失效
### 接口说明

接口调用请求说明
https请求方式: POST
https://oapi.dingtalk.com/service/get_permanent_code?suite_access_token=xxxx

POST数据示例

```
{
	"tmp_auth_code": " value"
}
```

请求参数说明

参数		| 说明
-------	| -------------
tmp_auth_code | 回调接口（tmp_auth_code）获取的临时授权码

返回结果示例

```
{
	"permanent_code": "xxxx",
	"auth_corp_info":
	{
		"corpid": "xxxx",
		"corp_name": "name"
    }
}
```

结果参数说明

参数		| 说明
-------	| -------------
permanent_code | 永久授权码
auth_corp_info | 授权方企业信息
corpid | 授权方企业id
corp_name | 授权方企业名称

## 5:获取企业授权的access_token
### 使用场景

服务提供商在取得企业的永久授权码并完成对企业应用的设置之后，便可以开始通过调用企业接口来运营这些应用。其中，调用企业接口所需的access_token获取方法如下接口说明。
### 接口说明

接口调用请求说明

https请求方式: POST
https://oapi.dingtalk.com/service/get_corp_token?suite_access_token=xxxx

POST数据示例

```
{
	"auth_corpid": "auth_corpid_value",
	"permanent_code": "code_value"
}
```

请求参数说明

参数		| 说明
-------	| -------------
auth_corpid	| 授权方corpid
permanent_code | 永久授权码，通过get_permanent_code获取

返回结果示例

```
{
	"access_token": "xxxxxx",
	"expires_in": 7200
}
```

结果参数说明

参数 | 说明
-------	| -------------
access_token | 授权方（企业）access_token
expires_in | 授权方（企业）access_token超时时间

## 6: 获取企业授权的授权数据
### 使用场景

该API用于通过永久授权码换取授权信息。 永久授权码的获取，是通过临时授权码使用get_permanent_code 接口获取到的permanent_code。
### 接口说明

接口调用请求说明

https请求方式: POST

https://oapi.dingtalk.com/service/get_auth_info?suite_access_token=xxxx

//注意，是suite_access_token，不是授权方（企业）的access_token

POST数据示例

```
{
	"auth_corpid":"auth_corpid_value",
	"permanent_code":"code_value",
	"suite_key":"key_value"
}
```

请求参数说明

参数					| 说明
-------				| -------------
suite_key			| 应用套件key
auth_corpid			| 授权方corpid
permanent_code		| 永久授权码，通过get_permanent_code获取

返回结果示例

```
{
   "auth_corp_info":{
	  "corp_logo_url":"http://xxxx.png",
	  "corp_name":"corpid",
	  "corpid":"auth_corpid_value",
	  "industry":"互联网",
	  "invite_code" : "1001",
	  "license_code": "xxxxx",
	  "is_authenticated":true,
	  "invite_url":"invite_url:https://yfm.dingtalk.com/invite/index?code=xxxx"
	},
	"auth_user_info":
    {
    	"userId":""
	},
    "auth_info":{
	"agent":[{
			"agent_name":"aaaa",
			"agentid":1,
			"appid":-3,
			"logo_url":"http://aaaaaa.com"
	}
	,{
			"agent_name":"bbbb",
			"agentid":4,
			"appid":-2,
			"logo_url":"http://vvvvvv.com"
	}]
	},
		  "errcode":0,
		  "errmsg":"ok"
}
```

结果参数说明

参数					| 说明
-------				| -------------
auth_corp_info		| 授权方企业信息
corpid				| 授权方企业id
invite_code         | 表示邀请码，只有填写过且是ISV自己邀请码的数据才会返回,否则值为空字符串
industry			| 表示企业所属行业
corp_name			| 授权方企业名称
license_code		| 序列号
is_authenticated	| 企业是否认证
invite_url			| 企业邀请链接
auth_user_info      | 授权方管理员信息
corp_logo_url		| 企业logo
auth_info			| 授权信息
agent				| 授权的应用信息
agentid				| 授权方应用id
agent_name			| 授权方应用名字
logo_url			| 授权方应用头像
appid				| 服务商套件中的对应应用id


## 7:获取企业的应用信息
### 使用场景
该API用于获取已授权开通的企业的某个应用的基本信息，包括LOGO,名称，描述等,信息接口调用请求说明
### 接口说明

https请求方式: POST

https://oapi.dingtalk.com/service/get_agent?suite_access_token=xxxx

POST数据示例

```
{	"suite_key":"key_value",
	"auth_corpid":"auth_corpid_value",
	"permanent_code":"code_value",
	"agentid":541
}
```

请求参数说明

参数					| 说明
-------				| -------------
suite_key			| 应用套件key
auth_corpid			| 授权方corpid
permanent_code		| 永久授权码，从get_permanent_code接口中获取
agentid				| 授权方应用id

返回结果示例

```
{
	"agentid":541,
	"name":"公告",	
	"logo_url":"http://xxxxxxx/png",
	"description":"企业重要消息",
	"close":1,
	"errcode":0,
	"errmsg":"ok"
}
```

结果参数说明

参数			| 说明
-------		| -------------
agentid		| 授权方企业应用id
name		| 授权方企业应用名称
logo_url	| 授权方企业应用头像
description	| 授权方企业应用详情
close		| 授权方企业应用是否被禁用（0:禁用  1:正常  2:待激活 ）

## 8:激活授权套件
### 使用场景
该API适用于当企业用户授权开通套件时ISV套件进行调用，用于激活授权方企业的套件微应用。如果ISV未调用此接口，则企业用户无法使用ISV套件
### 接口说明
信息接口调用请求说明

https请求方式: POST

https://oapi.dingtalk.com/service/activate_suite?suite_access_token=xxxx

POST数据示例

```
{
	"suite_key":"key_value",
	"auth_corpid":"auth_corpid_value",
	"permanent_code":"permanent_code"
}
```

请求参数说明

参数				| 说明
-------			| -------------
suite_key		| 应用套件key
auth_corpid		| 授权方corpid
permanent_code	| 永久授权码，从get_permanent_code接口中获取

返回结果示例

```
{
	"errcode":0,
	"errmsg":"ok"
}
```
## 9: 解除授权套件
### 使用场景

当ISV想重新模拟测试企业发起授权套件，需要先进行解除对套件的授权。

### 操作说明

解除授权需要进入进入测试企业OA后台--微应用进行操作，如图：

![deleteSuite](https://img.alicdn.com/tps/TB1GpUAKVXXXXckaXXXXXXXXXXX-858-302.jpg)


## 10: ISV为授权方的企业单独设置IP白名单
### 使用场景

该API用于ISV为企业独立部署场景，在ISV为企业进行独立部署软件系统时，由于是独立机房环境，每套系统是不同的IP地址，ISV可以通过此API为授权套件企业设置IP白名单,设置成功后，套件中的微应用可以调用钉钉开放平台接口服务。
### 接口说明

https请求方式: POST

https://oapi.dingtalk.com/service/set_corp_ipwhitelist?suite_access_token=xxxx

POST数据示例

```
{	
	"auth_corpid":"dingabcdefgxxx",
	"ip_whitelist":["1.2.3.4","5.6.*.*"]
}
```

请求参数说明

参数					| 说明
-------				| -------------
auth_corpid			| 授权方corpid
ip_whitelist		| 要为其设置的IP白名单,格式支持IP段,用星号表示,如【5.6.\*.\*】,代表从【5.6.0.\*】到【5.6.255.\*】的任意IP,在第三段设为星号时,将忽略第四段的值,注意:仅支持后两段设置为星号

返回结果示例

```
{
	"errcode":0,
	"errmsg":"ok"
}
```
## 消息体签名

为了验证调用者的合法性，钉钉在回调url中增加了消息签名，以参数signature标识，企业需要验证此参数的正确性后再解密。

验证步骤：

1.  企业计算签名：dev_msg_signature=sha1(sort(token、timestamp、nonce、msg_encrypt))。sort的含义是将参数按照字母字典排序，然后从小到大拼接成一个字符串

2. 比较dev_msg_signature和回调接口中推送的字段signature是否相等，相等则表示验证通过


#### 加解密方案说明

开启回调模式时，有以下术语需要了解：

1. signature是签名，用于验证调用者的合法性。具体算法见以下'消息体签名'章节

2. EncodingAESKey：注册套件提供的数据加密密钥。用于消息体的加密，长度固定为43个字符，从a-z, A-Z, 0-9共62个字符中选取，是AESKey的Base64编码。解码后即为32字节长的AESKey

3. AESKey=Base64_Decode(EncodingAESKey + “=”)，是AES算法的密钥，长度为32字节。AES采用CBC模式，数据采用PKCS#7填充；IV初始向量大小为16字节，取AESKey前16字节。具体详见：http://tools.ietf.org/html/rfc2315

4. msg为消息体明文，格式为JSON

5. 钉钉服务器会把msg消息体明文编码成encrypt，encrypt = Base64_Encode(AES_Encrypt[random(16B) + msg_len(4B) + msg + $key])，是对明文消息msg加密处理后的Base64编码。其中random为16字节的随机字符串；msg_len为4字节的msg长度，网络字节序；msg为消息体明文；$key对于ISV开发来说，填写对应的suitekey，$key对于普通企业开发，填写企业的Corpid。
最终传给回调者的是encrypt，字段名为encrypt。

#####	对明文msg加密的过程如下：

msg_encrypt = Base64_Encode( AES_Encrypt[random(16B) + msg_len(4B) + msg + $key] )
AES加密的buf由16个字节的随机字符串、4个字节的msg长度、明文msg和$key组成。其中msg_len为msg的字节数，网络字节序；

* $key对于ISV来说，填写对应的suitekey
* $key对于普通企业开发，填写企业的Corpid

#### 对应于加密方案，解密方案如下：

* 取出返回的JSON中的encrypt字段。
* 对密文BASE64解码：aes_msg=Base64_Decode(encrypt)
* 使用AESKey做AES解密：rand_msg=AES_Decrypt(aes_msg)
* 验证解密后$key、msg_len
* 去掉rand_msg头部的16个随机字节，4个字节的msg_len,和尾部的$CorpID即为最终的消息体原文msg

## 加解密库和demo下载

ISV开发demo地址：[https://github.com/injekt/openapi-demo-java](https://github.com/injekt/openapi-demo-java)

### 加解密库-Java库和demo
首先，您需要做以下准备工作

1.请开发者使用jdk1.6或以上版本，针对加解密包中使用的org.apache.commons.codec.binary.Base64，须导入jar包commons-codec-1.10(或comm ons-codec-1.9等其他版本)，在java-demo的WebContent/WEB_INF/lib目录中我们也提供了commons-codec-1.10.jar。

官方下载地址：[http://commons.apache.org/proper/commons-codec/download_codec.cgi](http://commons.apache.org/proper/commons-codec/download_codec.cgi)

2.异常java.security.InvalidKeyException:illegal Key Size和『计算解密文字错误』的解决方案：

在官方网站下载JCE无限制权限策略文件
JDK6的下载地址：[http://www.oracle.com/technetwork/java/javase/downloads/jce-6-download-429243.html](http://www.oracle.com/technetwork/java/javase/downloads/jce-6-download-429243.html)

JDK7的下载地址：[http://www.oracle.com/technetwork/java/javase/downloads/jce-7-download-432124.html](http://www.oracle.com/technetwork/java/javase/downloads/jce-7-download-432124.html)

下载后解压，可以看到local_policy.jar和US_export_policy.jar以及readme.txt。如果安装的是JRE，将两个jar文件放到%JRE_HOME% \lib\security目录下覆盖原来的文件，如果安装的是JDK，将两个jar文件放到%JDK_HOME%\jre\lib\security目录下覆盖原来文件。

库地址：[https://github.com/injekt/openapi-demo-java/tree/master/src/com/alibaba/dingtalk/openapi/demo/utils/aes](https://github.com/injekt/openapi-demo-java/tree/master/src/com/alibaba/dingtalk/openapi/demo/utils/aes)

demo地址：[https://github.com/injekt/openapi-demo-java/blob/master/src/com/alibaba/dingtalk/openapi/servlet](https://github.com/injekt/openapi-demo-java/blob/master/src/com/alibaba/dingtalk/openapi/servlet)

### php库和demo
库地址：[https://github.com/injekt/openapi-demo-php/tree/master/crypto](https://github.com/injekt/openapi-demo-php/tree/master/crypto)

demo地址：[https://github.com/injekt/openapi-demo-php/blob/master/receive.php](https://github.com/injekt/openapi-demo-php/blob/master/receive.php)

### C#库和demo
库地址：[https://github.com/ian-cuc/suite-demo-c-/tree/master/API](https://github.com/ian-cuc/suite-demo-c-/tree/master/API)

demo地址：[https://github.com/ian-cuc/suite-demo-c-/blob/master/receive.ashx.cs](https://github.com/ian-cuc/suite-demo-c-/blob/master/receive.ashx.cs)

##调试工具

回调接口本地调试方案：由于回调接口需要在外网环境接收钉钉服务器的推送，假如开发者暂时没有外网地址，需要在本地调试回调接口的加解密方案，可以在本地环境构造推送。具体构造参数示例：

URL后面带的参数：signature=5a65ceeef9aab2d149439f82dc191dd6c5cbe2c0&timestamp=1445827045067&nonce=nEXhMP4r

Post参数：
```
{"encrypt":"1a3NBxmCFwkCJvfoQ7WhJHB+iX3qHPsc9JbaDznE1i03peOk1LaOQoRz3+nlyGNhwmwJ3vDMG+OzrHMeiZI7gTRWVdUBmfxjZ8Ej23JVYa9VrYeJ5as7XM/ZpulX8NEQis44w53h1qAgnC3PRzM7Zc/D6Ibr0rgUathB6zRHP8PYrfgnNOS9PhSBdHlegK+AGGanfwjXuQ9+0pZcy0w9lQ=="
}
```
Token：123456

数据加密密钥(ENCODING_AES_KEY)：4g5j64qlyl3zvetqxz5jiocdr586fn2zvjpa8zls3ij

suitekey：suite4xxxxxxxxxxxxxxx


ISV接入相关接口调试：[<font color=red >ISV接入调试工具</font>](https://debug.dingtalk.com/isv.html)

