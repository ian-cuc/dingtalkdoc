# Step 2 -- 创建微应用
- category: 企业接入指南
- order: 3---
- 如果您还没有注册钉钉企业账号，您需要通过[<font color=red >Step 1 -- 注册钉钉企业</font>](#step-1-注册钉钉企业)完成钉钉企业账号注册；已注册则继续完成当前步骤您就可以在钉钉上使用微应用了
## 新增微应用
您登录钉钉管理后台后可以进入 *应用中心* 页面对添加微应用

![enter_microapp_center](https://img.alicdn.com/tps/TB1GqkTLXXXXXcsXFXXXXXXXXXX-1122-641.jpg)

点击上图中 *新增微应用* 按钮，按下图填写微应用信息，点击确定后可以新增微应用。

![add_micro_app](https://img.alicdn.com/tps/TB1Qe_XJFXXXXalXpXXXXXXXXXX-598-477.png)

*首页地址* : 以`http://`或者`https://` 开头的URL，是微应用的首页地址；在移动设备上打开微应用Tab页，点击微应用列表中的微应用将访问这个URL指向的页面。

*后台地址* : 以`http://`或者`https://` 开头的URL，是微应用的后台管理页面地址；配置后台地址后可以通过应用中心页面进入到微应用的管理后台。

<aside class="notice">
<b>首页地址</b> 的URL域名务必保证真实有效，否则会导致钉钉用户无法正常使用微应用。
</aside>

![get_micro_app_agentID](https://img.alicdn.com/tps/TB1N490JFXXXXceXFXXXXXXXXXX-602-524.png)

您在应用中心创建微应用后，如上图所示可获取到微应用的AgentID，AgentID可用于发送企业会话消息等场景。

<br />

您也可以通过调用[<font color=red >创建微应用</font>](#创建微应用)接口进行微应用创建。

创建成功之后将会在手机的工作tab上显示出来

![createMi](https://img.alicdn.com/tps/TB1xStVKpXXXXbjXFXXXXXXXXXX-361-640.jpg)


至此您已经可以在钉钉上使用微应用了，如果您需要对微应用与钉钉有进一步的融合，请进行定制开发，参考[<font color=red >开发微应用</font>](#step-3-开发微应用)

