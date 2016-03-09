# Step 3 -- 开发微应用
- category: 企业接入指南
- order: 4---
- 您需要通过[<font color=red >新增微应用</font>](#新增微应用)获取微应用的AgentID，用来在微应用开发时调用开放平台的接口

钉钉开放提供丰富的接口、工具供您使用，用以降低您的开发成本：

- 钉钉开放平台提供了企业通讯录管理、文件管理、发送企业会话消息等功能，接口使用可以参考[<font color=red >服务端开发文档</font>](#服务端开发文档)；

- 钉钉开放平台提供了定制的微应用在钉钉客户端的专用运行容器，并提供了一组可以调用钉钉的本地能力和业务能力的JSApi接口，您可以通过这些接口使用钉钉的本地能力或者钉钉的业务逻辑，进行微应用与钉钉功能的结合；接口使用可以参考[<font color=red >客户端开发文档</font>](#客户端开发文档)。

- 钉钉开放平台提供了与钉钉PC版本集成的能力，接口使用可以参考[<font color=red >PC端开发文档</font>](#pc端开发文档)；

- 钉钉开放平台提供了开发过程中需要的调试工具和性能优化的建议，您可以参考[<font color=red >调试工具&性能优化</font>](#调试工具-amp-性能优化)；


## 实现免登

您的微应用接入钉钉后，通过钉钉实现免登无需让员工进行二次登录，员工在进入微应用的时可以获取当前用户的信息实现与原系统中的账户打通。详细文档请参阅[<font color=red >免登服务</font>](#免登服务)。


<br />


## 调用API接口

您在调用钉钉开放平台接口时需要附加AccessToken，AccessToken可以通过CorpID和CorpSecret获取。

### 获取CorpID和CorpSecret

CorpID是企业的唯一标识，获取CorpID和CorpSecret的步骤如下:

一、使用管理员帐号登录 [<font color=red >钉钉管理后台</font>](https://oa.dingtalk.com) ；

二、选择顶部菜单 **微应用** 进入微应用页面，在左侧菜单选择 **微应用设置** 进入微应用设置页；

三、在微应用设置页面底部点击 **获取** 按钮即可获取CorpID和CorpSecret。

![get_scecret_corpId](https://img.alicdn.com/tps/TB1xStVKpXXXXbjXFXXXXXXXXXX-361-640.jpg)

<aside class="notice">
钉钉开放平台提供了获取和修改企业(团队)的组织结构信息、人员信息等功能，所以请妥善保管CorpID和CorpSecret，避免外泄影响企业信息安全。
</aside>

### 获取AccessToken

开发者在调用开放平台接口前需要通过CorpID和CorpSecret获取AccessToken。获取AccessToken的方法是向 `https://oapi.dingtalk.com/gettoken?corpid=id&corpsecret=secrect` GET请求。

开发者获取AccessToken后便可以调用开放平台其他接口。

以获取部门列表接口为例，获取部门列表接口为：

`oapi.dingtalk.com/department/list`

在请求该接口时，需要将获取的AccessToken作为请求参数拼装到URL中：

`https://oapi.dingtalk.com/department/list?access_token=ACCESS_TOKEN`

更多关于AccessToken的信息请参考[<font color=red >《服务端开发文档-建立连接》</font>](#建立连接)一节。

<br />


## 发送企业会话消息

用户可以在企业会话中查看微应用发送的消息，开发者可以通过发送消息接口将消息发送到企业会话中。

![send_micro_app_message](https://img.alicdn.com/tps/TB1X.m6JFXXXXX0XFXXXXXXXXXX-1089-652.jpg)

调用消息发送接口时需要使用`HTTPS`协议，发送的数据包为`JSON`格式。目前钉钉开放平台支持文本、图片、声音、文件、链接、办公消息等消息类型。

## 示例程序

在[<font color=red >《Open API - 代码示例》</font>](#demo)中有发送消息的代码演示，开发者可以下载参考。

如果在使用开放平台中遇到困难请浏览[<font color=red >《常见问题》</font>](#faq)一节，若仍不能解决请按概述中的提供的反馈方式联系我们。


<!--## 服务端网段

如果您的企业无法直接访问外部域名，需要设置ip白名单，钉钉提供服务端网段，列表如下：

42.120.0.0/15

110.75.0.0/16

110.76.0.0/19

110.76.32.0/21

110.76.48.0/20

140.205.0.0/16

