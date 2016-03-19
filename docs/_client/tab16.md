# 企业通讯录
- category: 客户端开发文档
- order: 17---
dd.biz

##选人
0.0.6

corpid必须是用户所属的企业的corpid

此接口只能对用户进行选择，若要同时选择部门，请使用“选人，选部门”接口。

```javascript
dd.biz.contact.choose({
  startWithDepartmentId: Number, //-1表示打开的通讯录从自己所在部门开始展示, 0表示从企业最上层开始，(其他数字表示从该部门开始:暂时不支持)
  multiple: Boolean, //是否多选： true多选 false单选； 默认true
  users: [String, String, ...], //默认选中的用户列表，userid；成功回调中应包含该信息
  corpId: String, //企业id
  max: Number, //人数限制，当multiple为true才生效，可选范围1-1500
  onSuccess: function(data) {
  //onSuccess将在选人结束，点击确定按钮的时候被回调
  /* data结构
    [{
      "name": "张三", //姓名
      "avatar": "http://g.alicdn.com/avatar/zhangsan.png" //头像图片url，可能为空
      "emplId": '0573', //userid
     },
     ...
    ]
  */
  },
  onFail : function(err) {}
});
```
<img src="https://img.alicdn.com/tps/TB1j_JPKVXXXXXbXXXXXXXXXXXX-200-356.png" width = "200" height = "355" alt="图片名称" align=right />


#### 参数说明

参数 | 参数类型 | 说明
----- | ----- | -----
startWithDepartmentId | Number | -1表示从自己所在部门开始, 0表示从企业最上层开始，(其他数字表示从该部门开始:暂时不支持)
multiple | Boolean | 是否多选： true多选，false单选； 默认true
users | Array[String] | 默认选中的用户列表，userid；成功回调中应包含该信息
corpId | String | 企业id
max | Number | 人数限制，当multiple为true才生效，可选范围1-1500

<!--
startWithDepartmentId: Number, //-1表示从自己所在部门开始, 0表示从企业最上层开始，(其他数字表示从该部门开始:暂时不支持)
startWithDepartmentId | Number | -1表示从自己所在部门开始, 0表示从企业最上层开始，(其他数字表示从该部门开始:暂时不支持)
-->

####　返回说明

参数 | 说明
------|------
name | 姓名
avatar | 头像图片url，可能为空
emplId | userid，[<font color=red>获取成员详情接口</font>](#获取部门成员（详情）)

##选人，选部门

0.0.6

corpid必须是用户所属的企业的corpid


```javascript
dd.biz.contact.complexChoose({
  startWithDepartmentId: Number, //-1表示从自己所在部门开始, 0表示从企业最上层开始，其他数字表示从该部门开始
  selectedUsers: [String, String, ...], //预选用户
  corpId: String, //企业id
  onSuccess: function(data) {
  //onSuccess将在选人，选部门结束，点击确定按钮的时候被回调
  /* data结构
    {
      "users": [
      {
        "name": "张三", //姓名
        "avatar": "htp://g.alicdn.com/avatar/zhangsan.png" //头像图片url，可能为空
        "emplId": "0573", //userid:
      },
      ...
      ],
      "department": [
      {
        "id": 2,
        "name": "来往事业部",
      },
      ...
      ]
    }
  */
  },
  onFail : function(err) {}
});
```

<img src="https://img.alicdn.com/tps/TB1QCXuKVXXXXbWXFXXXXXXXXXX-750-1334.jpg
" width = "200" height = "355" alt="图片名称" align=right />


#### 参数说明

参数 | 参数类型 | 说明
----- | ----- | -----
startWithDepartmentId | Number | -1表示从自己所在部门开始, 0表示从企业最上层开始，其他数字表示从该部门开始
selectedUsers | Array[String] | 预选用户
corpId | String | 企业id

<!--隐藏selectedDepartments
selectedDepartments | Array | 预选部门 id必选，name可选
selectedDepartments: [{name: '', id: ''}, ...],//预选部门 id必选，name可选
-->

####　返回说明

参数 | 说明
------|------
users | 选取的用户
users.name | 姓名
users.avatar | 头像图片url，可能为空
users.emplId | userid,[<font color=red>获取成员详情接口</font>](#获取部门成员（详情）)
department | 选取的部门
department.id | 部门id
department.name | 部门名称

<!-- ### 选取

默认展示当前  业通讯录，开发中

```javascript
dd.biz.contact.choose({
    multiple: true, //是否多选： true多选 false单选； 默认true
    users: ['100','101'], //默认选中的用户列表，userid；成功回调中应包含该信息
    corpId: '', //企业id
    max: 50, //人数限制，当multiple为true才生效，可选范围1-1500
    onSuccess : function(result) {
        /*
        [{
            emplId: '0573', //userid
            name: '张三', //姓名
            nickNameCn: '三张', //花名
            mobilePhone: '****', //手机号 后续不再返回该字段
            emailAddr: '***', //邮箱  后期不再返回该字段
            pinyin: 'zhangsan', //姓名拼音
            avatar: 'htp://g.alicdn.com/avatar/zhangsan.png' //头像图片url，可能为空
        }]
        */
    },
    onFail : function(err) {}
});
```

#### 参数说明

参数 | 参数类型 | 说明
----- | ----- | -----
multiple | Boolean | 是否多选： true多选 false单选； 默认true
users | Array[String] | 默认选中的用户列表，工号；成功回调中应包含该信息
corpId | String |  企业id
max | Number| Number为正整数。人数限制，当multiple为true才生效，可选范围1-1500


####　返回说明

参数 | 说明
------|------
emplID | 是否多选： true多选 false单选； 默认true
name | 姓名
nickNameCn | 花名
mobilePhone | 手机号，后续不再返回该字段
emailAddr | 邮箱，后期不再返回该字段
pinyin | 姓名拼音
avatar | 头像图片url，可能为空 -->

## 创建企业群聊天

0.0.4

corpid必须是用户所属的企业的corpid

```javascript
dd.biz.contact.createGroup({
    corpId: '', //企业id，可选，配置该参数即在指定企业创建群聊天
    users: ['100','101'], //默认选中的用户工号列表，可选；使用此参数必须指定corpId
    onSuccess: function(result) {
        /*{
            id: 123   //企业群id
        }*/
    },
    onFail: function(err) {
    }
});
```

#### 参数说明

参数 | 参数类型 | 说明
----- | ----- | -----
corpId | String |  企业id，可选，配置该参数即在指定企业创建群聊天
users | Array[String] |  默认选中的用户列表，可选；使用此参数必须指定corpId

####　返回说明

参数 | 说明
------|------
id | 企业群id

<!--### 添加好友

```javascript
dd.biz.contact.addFriend({
    onSuccess: function(result) {
        /*{
            id: 123   //企业群id
        }*/
    },
    onFail: function(err) {
    }
})
```
-->

<!--## 用户

## 获取当前用户信息

目前只开放emplId字段

```javascript
dd.biz.user.get({
    onSuccess : function(result) {
        /*
        {
            id: '112', //id
            emplId: '0573' //工号
        }
        */
    },
    onFail : function(err) {}
});
```
-->
