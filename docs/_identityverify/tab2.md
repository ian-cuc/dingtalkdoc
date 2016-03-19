# 钉钉PC版微应用中调用免登
- category: 免登服务
- order: 3---
## 使用JS-API

步骤一：首先需要获取当前用户的corpid。ISV开发者请在微应用主页地址使用$CORPID$模板参数表示corpid，用户访问微应用的时候钉钉服务器将把$CORPID$替换成用户所属企业的corpid，例如原本的主页地址是http://www.dingtalk.com/index，则能获取用户corpid的主页地址为http://www.dingtalk.com/index?corpid=$CORPID$

步骤二：使用钉钉js-api提供的[<font color=red >PC版获取免登授权码</font>](#pc版获取免登授权码)接口获取CODE

步骤二：[<font color=red >通过CODE换取身份</font>](#通过code换取用户身份)

demo： 可参考手机客户端免登demo，但全局变量dd替换成DingTalkPC



