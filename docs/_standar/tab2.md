# 产品标准
- category: 标准规范
- order: 3---
## 命名规范
套件／微应用命名规范：#### 1.不能使用通用名词命名，包括拼音谐音，如墨迹天气、滴滴打车，不能命名为天气，打车#### 2.不能带有钉钉，阿里，淘宝，等阿里巴巴关联产品和企业文字#### 3.应用不得包含虚假、欺骗或误导的陈述，或是使用的名称与其他应用类似#### 4.命名必须符合开发者相关协议条款,不得带有影射竞争对手，触犯法律和道德的文字#### 5.命名不能重名，一旦应用审核通过，则不允许同名应用提交申请#### 6.应用的名字、描述和截图与应用内容相关#### 7.应用不得包括符号，和任何“beta”、“demo”、“trial”或“test”版本的应用#### 8.建议不超过6个汉字
### 9.更名：线上商品更名，不允许自行更名，现阶段必须进行邮件审核，发送邮箱至open-dingtalk@list.alibaba-inc.com申请，审核通过后才可更名

## 套件规范
### 市场上展示的套件，原则上不允许，相同微应用出现在不同的套件中，比如a应用已经独立组成套件A，不允许a应用组成套件B（线下快速部署的除外），运营审核套件和微应用的从属关系，不通过，则退回修改

## 场景规范

### 场景化与钉钉统一通讯能力结合，比如消息，会话，钉，通讯录，群等如：

![product_scene1](https://img.alicdn.com/tps/TB1FUmiLXXXXXauXFXXXXXXXXXX-431-613.png)
![product_scene2](https://img.alicdn.com/tps/TB1EgabLXXXXXXIXVXXXXXXXXXX-467-556.png)

## 功能规范 

### 需要在钉钉上形成完整的业务闭环，用户可以在钉钉手机端上解决完整的业务刚需

### 如果已有原生APP， 建议ISV在钉钉版本上保留原生APP的核心价值，并积极实现和原生APP相同或更好的用户体验

## UI规范 
需要按照钉钉UI规范进行产品设计，[<font color=red >请下载</font>](http://download.taobaocdn.com/freedom/30563/compress/p1a5tl8v1d1fk91l9l15cu1vnp54l4.zip)
![product_UI](https://img.alicdn.com/tps/TB18eWkLXXXXXcnXpXXXXXXXXXX-528-223.png)

## 免登及注册 
降低用户使用门槛，原则上不出现任何注册功能，必须实现移动端应用无需注册，直接开通使用和免登，如有PC版，需要实现PC端的免登，但此功能非开始共创和灰度的必要条件，可以后续迭代完善
![product_use](https://img.alicdn.com/tps/TB1ZNx3LXXXXXaIaXXXXXXXXXXX-644-575.png)

## 用户引导 
钉钉不会以任何方式提供客户的联系方式（包括手机，固定电话等），ISV产品设计上也不能误导客户提供联系方式，如业务需要，则必须向客户明确说明，联系方式的真实使用目的，范围和场景，并让客户自行选择是否提供联系方式

![product_ feedback](https://img.alicdn.com/tps/TB17mSwLXXXXXXeXXXXXXXXXXXX-419-505.png)

## 迭代计划 
商品上架前，提供产品的下一阶段的迭代计划；例如：
![product_plan](https://img.alicdn.com/tps/TB17mSwLXXXXXXeXXXXXXXXXXXX-419-505.png)

## PC桌面版
ISV在10家企业共创阶段，如提供PC版，必须完成钉钉桌面版免登接入，并且需要按照以下标准进行产品验收
### 1.全部页面嵌入钉钉桌面版，如审批和通达应用
![product_PC1](https://img.alicdn.com/tps/TB1WAkELpXXXXXjXFXXXXXXXXXX-865-588.png)
### 2.跳出钉钉桌面版，新开浏览器窗口，免登进入ISV web版页面
- 在保持较好体验前提下，建议ISV web版页面，全部嵌入钉钉桌面版，并实现免登，如果嵌入体验较差，可以点击具体功能后，跳出到浏览器- 从钉钉桌面跳出，必须从对用户有业务意义的页面，点击具体功能后，无缝跳出，不能有业务断点，比如可以嵌入报表导航页面，在进行查询/新增/编辑/删除时，跳出到浏览器，不允许通过只有登录按钮的空页面，进行跳出

![product_PC2](https://img.alicdn.com/tps/TB1nJcCLpXXXXamXFXXXXXXXXXX-865-588.png)

