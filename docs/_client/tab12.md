# 会话
- category: 客户端开发文档
- order: 13---
dd.biz

## 获取会话信息

0.0.7

corpid必须是用户所属的企业的corpid


```javascript
dd.biz.chat.pickConversation({
    corpId: '', //企业id
    isConfirm:'true', //是否弹出确认窗口，默认为true
    onSuccess : function() {
    	//onSuccess将在选择结束之后调用
        /*{
            cid: 'xxxx',
            title:'xxx'
        }*/
},
    onFail : function() {}
})
```
<img src="https://img.alicdn.com/tps/TB1cXJPKVXXXXXFXXXXXXXXXXXX-200-356.png" width = "200" height = "355" alt="图片名称" align=right />

#### 参数说明

参数 | 参数类型 | 说明
----- | ----- | -----
corpId | String | 企业ID
isConfirm | Boolean | 是否弹出确认窗口，默认为true

#### 返回说明
参数 | 说明
----- | -----
cid | 会话id
title | 会话标题

## 根据corpid选择会话

0.0.11

corpid必须是用户所属的企业的corpid

2.6版本新增

```javascript
dd.biz.chat.chooseConversationByCorpId({
    corpId: 'xxx', //企业id
    onSuccess : function() {
        	//onSuccess将在选择结束之后调用
        /*{
            chatId: 'xxxx',
            title:'xxx'
        }*/
},
    onFail : function() {}
})
```
#### 参数说明

参数 | 参数类型 | 说明
----- | ----- | -----
corpId | String | 企业ID

#### 返回说明
参数 | 说明
----- | -----
chatId | 会话id
title | 会话标题


## 根据chatid跳转到对应会话

0.0.11

corpid必须是用户所属的企业的corpid

2.6版本新增

```javascript
dd.biz.chat.toConversation({
    corpId: 'xxx', //企业id
    chatId:'xxx',//会话Id
    onSuccess : function() {},
    onFail : function() {}
})
```
#### 参数说明

参数 | 参数类型 | 说明
----- | ----- | -----
corpId | String | 企业ID
chatId | String | 会话ID

#### 返回说明（无）



<!--### 发送消息

```javascript
dd.biz.chat.sendMessage({
    users : ['100', '101'],//用户列表，工号
    corpId: '', //企业id
    type: 1,//消息类型 1：image  2：link  [暂定和发钉保持一致]
    attachment: {
        images: [''],
    },
    text: String,
    onSuccess : function() {},
    onFail : function() {}
})
```

## 选择会话(群)

类似分享到钉钉的选取页面，只能选一个回话 0.0.3

```javascript
dd.biz.chat.chooseConversation({
    onSuccess : function(data) {
    /*
    {
        id: '123' //会话id
    }
    */
    },
    onFail : function() {}
})
```
####　返回说明
参数 | 说明
----- | ------
id | 会话id

##获取会话信息

0.0.6

```javascript
dd.biz.chat.getConversationInfo ({
  cid: String, //会话ID
  onSuccess: function(data) {
  /* data结构
	  "cid": "1111", //会话ID
	  "title": '123', //会话标题
	  "avatarIcons": ["http://", ...], //会话的头像数组
	  "memberCount": 11, //群聊成员总数
	  }
  */
  },
  onFail : function(err) {
  }
})
```
#### 参数说明

参数 | 参数类型 | 说明
----- | ----- | -----
cid | String | 会话ID

#### 返回说明
参数 | 说明
----- | -----
cid | 会话ID
title | 会话标题
avatarIcons | 会话的头像数组
memberCount | 群聊成员总数
-->

