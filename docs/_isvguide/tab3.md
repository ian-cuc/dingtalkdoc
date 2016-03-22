# Step 3 -- 开发套件（微应用）
- category: ISV接入指南
- order: 4---在您开始开发套件时，为了减少您的验收时间，建议您提供以下信息至邮件组
：open-dingtalk@list.alibaba-inc.com

- 套件所属的行业类别
- 产品功能相关说明
- 是否收费
- 产品原型稿

您将经过创建套件、创建微应用、创建测试企业、调用开放平台API开发微应用来完成您的套件开发


## 1: 创建套件
开发者可以编辑套件基本信息，创建微应用。

### 基本流程（Basic Flow）

#### 1.钉钉应用菜单-套件列表，点击“创建套件”

![createtj](https://img.alicdn.com/tps/TB1IJQRLXXXXXb0XFXXXXXXXXXX-1421-196.jpg)

#### 2．填写创建套件表单

![createtjbd](https://img.alicdn.com/tps/TB1Az_EJFXXXXb3XFXXXXXXXXXX-678-539.jpg)

#### 数据项说明：

字段  		| 属性
-----------	| -------------
名称		    | 套件的名称
套件Logo		| 上传大小不超过1M，长宽等比且范围在50px至200px之间的png格式图片
Token 		| 可任意填写，用于生成签名，校验回调请求的合法性。本套件下相关应用产生的回调消息都使用该值来解密。
数据加密密钥 	| 回调消息加解密参数，是AES密钥的Base64编码，用于解密回调消息内容对应的密文。本套件下相关应用产生的回调消息都使用该值来解密。
IP白名单		| 调用钉钉API时的合法IP列表，多个IP请以“,”隔开，如IP有变化，请立即更新
回调URL		| 以http://开头，系统将会把此套件的SuiteTicket，临时授权码以及授权变更事件推送给此URL，详细请看[<font color=red >回调接口</font>](#2-回调接口（分为五个回调类型）)
当前状态 		| 对于需要公开售卖的套件，只有处于已完成状态，才可进入售卖流程



**当您注册套件时，钉钉服务器为了避免无效推送，将会验证回调url的有效性，对回调url推送"验证回调URL有效性事件"，收到推送后您需要做正确的处理，才能成功创建套件。详细处理步骤请查看[<font color=red >回调接口</font>](#2-回调接口（分为五个回调类型）)和"验证回调URL有效性事件"。**

#### 3.点击“确定”按钮进入套件列
在这里可以查看套件详细信息，比如套件Key（suite_key），套件secret(suite_secret)


## 2: 创建微应用

### 基本流程（Basic Flow）

#### 1 查看套件基本信息

#### 2 点击“创建微应用按钮”

![createmini1](https://img.alicdn.com/tps/TB1CNZ7LXXXXXXnXpXXXXXXXXXX-1240-299.jpg)

#### 3 添加创建微应用表单，点击“确定”按钮

![createmini2](https://img.alicdn.com/tps/TB18FoZLXXXXXXqXFXXXXXXXXXX-681-673.jpg)
#### 需要提供的数据项：

字段  		| 属性
-----------	| -------------
名称 		| 应用的名称，2-16个字。
图标 		| 上传大小不超过1M，长宽等比且范围在50px至200px之间的png格式图片
应用描述 		| 描述该应用的功能与特色，4-120个字内
主页地址	 	| 以http://开头，用于接收托管企业应用的用户消息，URL支持使用$CORPID$模板参数表示corpid，用户访问应用的时候将把$CORPID$替换成用户所属企业的corpid，例如http://www.dingtalk.com/index?corpid=$CORPID$
PC主页地址 | 微应用PC端主页地址
权限设置		| 此处权限会在用户授权您的套件时进行显示告知用户您的套件所需要获取的企业员工信息，当企业用户授权后，您可以通过[<font color=red>获取部门成员（详情）</font>](#获取部门成员（详情）)接口获取员工的详细信息
接口权限		| 此处权限会在用户授权您的套件时进行显示告知用户您的套件所需要获取的企业信息，当企业用户授权后，您的套件可以钉钉开放平台提供的对应接口


#### 4  创建成功后微应用列表添加一行记录

![createmini3](https://img.alicdn.com/tps/TB1lC7QLXXXXXcJXFXXXXXXXXXX-1245-353.jpg)

## 3: 注册测试企业

钉钉套件在开发过程中，需要在钉钉移动端上登录绑定了相关企业的钉钉帐号来进行调试。在此之前，需要开发者在授权管理中对注册的测试企业"发起授权"，之后钉钉服务器会向您填写的回调url[<font color=red>推送临时授权码</font>](#2-回调接口（分为五个回调类型）)，您需要通过临时授权码一步一步到[<font color=red>激活授权套件</font>](#8-激活授权套件)，才能让测试企业的微应用列表出现您开发的微应用。

备注：[<font color=red>钉钉当前支持最多创建10个测试企业</font>]

### 基本流程（Basic Flow）

#### 1.钉钉应用菜单—开发环境列表，点击“注册测试企业”

![signintest1](https://img.alicdn.com/tps/TB1qYgPLXXXXXX.XVXXXXXXXXXX-1247-84.jpg)
#### 2.填写企业相关信息

![signintest2](https://img.alicdn.com/tps/TB1p1H3IVXXXXX8aXXXXXXXXXXX-729-447.png)

#### 3.点击“确定”后列表增加一行记录

![signintest3](https://img.alicdn.com/tps/TB1SRoPLXXXXXXIXVXXXXXXXXXX-1230-272.jpg)

#### 4.点击“授权”，对微应用进行授权

注意：只有在微应用注册的回调接口能够接收推送，才能成功开通微应用，具体详情查看[<font color=red>回调接口</font>](#5-回调接口（分为五个回调类型）)

![signintest4](https://img.alicdn.com/tps/TB1qxEULXXXXXaMXFXXXXXXXXXX-1233-341.jpg)

#### 5.点击“登录管理”跳转钉钉登录后台

![signintest5](https://img.alicdn.com/tps/TB1cHQVLXXXXXazXFXXXXXXXXXX-1220-195.jpg)

![signintest6](https://img.alicdn.com/tps/TB1snUfIVXXXXbSXpXXXXXXXXXX-866-456.png)

## 4: 开发套件

- 钉钉开放平台提供了接入一组应用接入与授权的接口，通过实现接入与授权接口您可以快速发布自己的微应用套件，并在企业客户授权开通微应用时，自动进行开通激活，企业用户可以授权后直接使用您的套件（应用），接口使用可以参考[<font color=red >ISV接入开发指南</font>](#isv接入开发指南)；该指南主要介绍了企业和ISV（服务提供商）如何接入钉钉开放平台，其中涉及到接入过程中使用的工具、与钉钉开放平台相关的概念和接入钉钉开放平台的一些实践方法，以帮助开发者快速开发自己的微应用。

- 钉钉开放平台提供了**企业通讯录管理、文件管理、发送企业会话消息**等功能，接口使用可以参考[<font color=red >服务端开发文档</font>](#服务端开发文档)；

- 我们定制了微应用专用的运行容器，提供了一组可以调用**钉钉的本地能力和业务逻辑**的JS接口，开发者可以通过这些接口使用钉钉的本地能力或者钉钉的业务逻辑，降低开发成本，提高微应用在移动客户端的体验。接口使用可以参考[<font color=red >客户端开发文档</font>](#客户端开发文档)。

- 钉钉开放平台提供了与钉钉PC版本集成的能力，接口使用可以参考[<font color=red >PC端开发文档</font>](#pc端开发文档)；

- 钉钉开放平台提供了开发过程中需要的调试工具和性能优化的建议，您可以参考[<font color=red >调试工具&性能优化</font>](#调试工具-amp-性能优化)；





