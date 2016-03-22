# Demo
- category: 服务端开发文档
- order: 17---
提供了使用Java、PHP、Nodejs 接入钉钉开放平台API的代码示例，和在线调试工具

下面的代码示例展示了一些常用API的使用方式，在运行下面的示例前请先获取CorpID和CorpSecret，并按照示例下的说明配置到合适的位置。

## 调试工具

[<font color=red >钉钉服务端API调试工具</font>](https://debug.dingtalk.com)

## Java版本

```javascript
 public class Env {
  public static final String OAPI_HOST = "https://oapi.dingtalk.com";
    public static final String CORP_ID = "corpid";
    public static final String CORP_SECRET = "secret";
 }

```

1.将您的CorpID和CorpSecret配置在Env.java文件

2.启动您的服务器，如果配置正确，则会成功启动。

[<font color=red >Demo地址：</font>](https://github.com/ddtalk/HarleyCorp)
[<font color=red >https://github.com/ddtalk/HarleyCorp</font>](https://github.com/ddtalk/HarleyCorp)

## PHP版本

```javascript
 define("OAPI_HOST", "https://oapi.dingtalk.com");
 define("CORPID", "");
 define("SECRET", "");
```

1.将您的CorpID和CorpSecret配置在env.php文件

2.启动您的服务器，如果配置正确，则会成功启动。

[<font color=red >Demo地址：</font>](https://github.com/injekt/openapi-demo-php)
[<font color=red >https://github.com/injekt/openapi-demo-php</font>](https://github.com/injekt/openapi-demo-php)

## Node.js版本

```javascript
module.exports = {
    corpId: '',
    secret: ''
};
```

1.将您的CorpID和CorpSecret配置在env.js文件

2.启动您的服务器，如果配置正确，则会成功启动。

[<font color=red >Demo地址：</font>](https://github.com/injekt/openapi-demo-nodejs)
[<font color=red >https://github.com/injekt/openapi-demo-nodejs</font>](https://github.com/injekt/openapi-demo-nodejs)
