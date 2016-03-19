# 微应用后台管理员免登
- category: 免登服务
- order: 4---实现微应用后台管理系统与钉钉OA后台的免登

应用场景示例如下图：

![normalcorp](https://img.alicdn.com/tps/TB1iw.4KFXXXXXoXFXXXXXXXXXX-594-302.png)

**准备工作**：

1: 配置微应用后台地址

普通企业在[<font color=red>OA后台</font>](https://oa.dingtalk.com/#/microApp/microAppList)添加微应用配置如左图，ISV在[<font color=red>开发者后台</font>](http://console.d.aliyun.com)添加微应用配置如下图

![oaback](https://img.alicdn.com/tps/TB15zWTKFXXXXcEXVXXXXXXXXXX-642-367.jpg)

2: 获取完成免登过程中验证身份的密钥（SSOSecret）

<font color=red >重要说明：企业和ISV获取的方法一致，都是通过OA后台获取，ISV开发套件微应用的管理后台，使用自己企业的SSOSecret即可完成身份认证</font>

在[<font color=red>OA后台</font>](https://oa.dingtalk.com/#/microApp/microAppSet)获取SSOSecret的方法如下：


![normalcorp](https://img.alicdn.com/tps/TB1y_xcKVXXXXa6XXXXXXXXXXXX-1084-621.jpg)



**使用方法（钉钉管理员登陆态）** 


步骤一：在OA后台，点击微应用的“进入后台”，自动跳转到准备工作1中配置的微应用后台地址，开发者从跳转的URL中解析code参数，获取CODE并保存下来，通过此CODE获取管理员的身份信息

步骤二：通过[<font color=red >获取微应用后台管理Token</font>](#获取微应用后台管理token)获取AccessToken

步骤三：使用AccessToken[<font color=red >通过步骤一获取的CODE换取微应用管理员的身份信息</font>](#通过code换取微应用管理员的身份信息)


**更多用法**

在钉钉管理员非登陆态，使用钉钉管理后台的Oauth身份认证可以通过下面方法：

在管理员访问后台地址的时候，企业在后台构造一个连接，通过HTTP 302跳转方式，让用户访问钉钉开放平台授权网址，构造的地址如下:

`https://oa.dingtalk.com/omp/api/micro_app/admin/landing?corpid=CORPID&redirect_url=REDIRECT_URL`

参数 | 说明
---------- | ------
corpid | 开发此微应用的公司corpid，ISV填写自己企业的CorpID
redirect_url | 重定向地址(需要urlencode编码)


REDIRECT_URL为微应用后台地址，首先跳转到钉钉OA管理后台登录页，登陆成功后，会再次通过HTTP 302跳转回微应用的后台地址(即REDIRECT_URL)，并在REDIRECT_URL后面追加参数code=CODE,即

`REDIRECT_URL?code=CODE`

开发者从URL中解析code参数，获取CODE并保存下来，再按照上面使用方法中的步骤二和步骤三 获得管理员信息

demo查看:[https://github.com/injekt/openapi-demo-java/tree/master/src/com/alibaba/dingtalk/openapi/servlet](https://github.com/injekt/openapi-demo-java/tree/master/src/com/alibaba/dingtalk/openapi/servlet)

