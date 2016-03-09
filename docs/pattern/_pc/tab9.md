# 企业通讯录
- category: PC端开发文档
- order: 10---
DingTalkPC.biz

## 选人

此接口只能对用户进行选择，若要同时选择部门，请使用“选人，选部门”接口。

``` javascript
DingTalkPC.biz.contact.choose({
    multiple: true, //是否多选： true多选 false单选； 默认true
    users: ['10001', '10002', ...], //默认选中的用户列表，工号；成功回调中应包含该信息
    corpId: 'dingb4ff1079f84f8d54', //企业id
    max: 10, //人数限制，当multiple为true才生效，可选范围1-1500
    onSuccess: function(data) {
    /* data结构
      [{
        "name": "张三", //姓名
        "avatar": "http://g.alicdn.com/avatar/zhangsan.png" //头像图片url，可能为空
        "emplId": '0573', //工号
       },
       ...
      ]
    */
    },
    onFail : function(err) {}
});
```

#### 参数说明

| 参数       | 参数类型          | 说明                                |
| -------- | ------------- | --------------------------------- |
| multiple | Boolean       | 是否多选： true多选，false单选； 默认true      |
| users    | Array[String] | 默认选中的用户列表，工号；成功回调中应包含该信息          |
| corpId   | String        | 企业id                              |
| max      | Number        | 人数限制，当multiple为true才生效，可选范围1-1500 |

<!--

startWithDepartmentId: Number, //-1表示从自己所在部门开始, 0表示从企业最上层开始，(其他数字表示从该部门开始:暂时不支持)

startWithDepartmentId | Number | -1表示从自己所在部门开始, 0表示从企业最上层开始，(其他数字表示从该部门开始:暂时不支持)

-->

#### 　返回说明

| 参数     | 说明           |
| ------ | ------------ |
| name   | 姓名           |
| avatar | 头像图片url，可能为空 |
| emplId | 工号           |

