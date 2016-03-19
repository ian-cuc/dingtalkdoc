# 客户通讯录接口（暂未开放）
- category: 服务端开发文档
- order: 6---
您可以通过使用客户通讯接口，将您的CRM应用中的员工与客户的关系、客户与客户联系人的关系在钉钉客户端通讯录中展现，与钉钉有更深入的功能融合，对于用户来说客户关系与通讯录的紧密结合，更容易管理和联系核心客户

## 员工新增客户信息

##### 请求说明

Https请求方式: POST

`https://oapi.dingtalk.com/crm/customer/create?access_token=ACCESS_TOKEN&user_id=USER_ID`

##### 请求包结构体

```
{
"customer":[
{
"name":"姓名",
"address":"地址",
"description":"描述",
"telephone":"电话"
}
],
"contacts":[
{
"name":"姓名",
"mobile":"手机",
"attached":"备注"
}
],
"userIds":[
"USER_ID","USER_ID"
],
"create_by":"创建时间"
}

```

##### 参数说明

参数 | 参数类型 | 必须 | 说明
----------| ------- | ------- | ------
access_token | String | 是 | 调用接口凭证
user_id | String | 是 |  员工在企业内的userid
customer | JSONObject | 是 |  客户信息
name | String | 是 |  客户名称
address | String | 是 |  客户地址
description | String | 是 |  客户描述
telephone | String | 是 |  客户电话
contacts | JSONObject | 否 |  客户联系人信息
name | String | 否 |  客户联系人名称
mobile | String | 否 |  客户联系人手机
attached | String | 否 |  客户联系人备注
userIds | String[] | 否 |  跟进客户的员工信息
create_by | String | 是 |  创建时间

##### 返回结果

```
{
    "errcode": 0,
    "errmsg": "ok",
    "customerid": "xxxxxxxxxxxxxxxxxx"
}
```

参数 | 说明
----------  | ------
errcode | 返回码
errmsg | 对返回码的文本描述内容
customerid | 客户id

## 员工修改客户信息

##### 请求说明

Https请求方式: POST

`https://oapi.dingtalk.com/crm/customer/update?access_token=ACCESS_TOKEN&user_id=USER_ID`

##### 请求包结构体

```
{
"id":"客户id",
"name":"客户名称",
"address":"客户地址",
"description":"客户描述",
"telephone":"电话",
"modified_by":"修改时间"
}
```

##### 参数说明

参数 | 参数类型 | 必须 | 说明
----------| ------- | ------- | ------
access_token | String | 是 | 调用接口凭证
user_id | String | 是 | 员工id
id | String | 是 |  客户id
name | String | 否 | 客户名称
address  | String | 否 | 客户地址信息
description  | String | 否 | 客户描述信息
telephone  | String | 否 | 客户联系电话
modified_by  | String | 否 | 修改时间

##### 返回结果

```
{
    "errcode": 0,
    "errmsg": "ok"
}
```

参数 | 说明
----------  | ------
errcode | 返回码
errmsg | 对返回码的文本描述内容

## 员工删除客户

##### 请求说明

Https请求方式: POST

`https://oapi.dingtalk.com/crm/customer/delete?access_token=ACCESS_TOKEN&user_id=USER_ID`

##### 请求包结构体

```
{
"id[]":"客户id"
}

```

##### 参数说明

参数 | 参数类型 | 必须 | 说明
---------- | ------- | ------- | ------
access_token | String | 是 | 调用接口凭证
user_id | String | 是 | 会话id
id | String[] | 是 | 客户id

##### 返回结果

```
{
    "errcode": 0,
    "errmsg": "ok"
 }
```

参数 | 说明
---- | -----
errcode | 返回码
errmsg | 对返回码的文本描述内容


## 获取客户详细信息

##### 请求说明

Https请求方式: GET

`https://oapi.dingtalk.com/crm/customer/get?access_token=ACCESS_TOKEN&id=CUSTOMER_ID`

##### 参数说明

参数 | 参数类型 | 必须 | 说明
---------- | ------- | ------- | ------
access_token | String | 是 | 调用接口凭证
id | String | 是 | 客户id

##### 返回结果

```
{
"customer":{

"name":"客户名称",
"address":"客户地址",
"description":"客户描述",
"telephone":"客户电话"
},
"contactList":[
{
"name":"客户联系人名称",
"mobile":"客户联系人电话",
"attached":"客户联系人备注"
}
],
"userIds":[
                "USER_ID","USER_ID"
],
"create_by":"创建时间"
}
```

参数 | 说明
---- | -----
customer  |  客户信息
name |  客户名称
address  |  客户地址
description |  客户描述
telephone  |  客户电话
contacts  |  客户联系人信息
name  |  客户联系人名称
mobile  |  客户联系人手机
attached  |  客户联系人备注
userIds  |  跟进客户的员工信息
create_by  |  创建时间

## 获取客户列表

##### 请求说明

Https请求方式: GET

`https://oapi.dingtalk.com/crm/customer/get?access_token=ACCESS_TOKEN`

##### 参数说明

参数 | 参数类型 | 必须 | 说明
---------- | ------- | ------- | ------
access_token | String | 是 | 调用接口凭证

##### 返回结果

```
{
"customerlist":[
{
"name":"客户名称",
"address":"客户地址",
"description":"客户描述",
"telephone":"客户电话"
}
]
}
```

参数 | 说明
---- | -----
customerlist  |  客户列表信息
name |  客户名称
address  |  客户地址
description |  客户描述
telephone  |  客户电话

## 员工新增客户联系人

##### 请求说明

Https请求方式: POST

`https://oapi.dingtalk.com/crm/contact/create?access_token=ACCESS_TOKEN&user_id=USER_ID`

##### 请求包结构体

```
{
"customerid":"客户id",
"name":"客户联系人名称",
"mobile":"客户联系人手机",
"attached":"客户联系人备注",
"create_by":"创建时间"
}

```

##### 参数说明

参数 | 参数类型 | 必须 | 说明
---------- | ------- | ------- | ------
access_token |String | 是 | 调用接口凭证
user_id |String | 是 | 员工id
customerid  |  客户id
name  |  客户联系人名称
mobile  |  客户联系人手机
attached  |  客户联系人备注
create_by  |  创建时间

##### 返回说明

```
{
    "errcode": 0,
    "errmsg": "ok"
}
```
参数 | 说明
---- | -----
errcode | 返回码
errmsg | 对返回码的文本描述内容

## 员工修改客户联系人

##### 请求说明

Https请求方式: POST

`https://oapi.dingtalk.com/crm/contact/create?access_token=ACCESS_TOKEN&user_id=USER_ID`

##### 请求包结构体

```
{
"contactid":"客户联系人id",
"name":"客户联系人名称",
"mobile":"客户联系人手机",
"attached":"客户联系人备注",
"modified_by":"修改时间"	  
}

```

##### 参数说明

参数 | 参数类型 | 必须 | 说明
---------- | ------- | ------- | ------
access_token |String | 是 | 调用接口凭证
user_id |String | 是 | 员工id
contactid |String | 是  |  客户id
name |String | 是  |  客户联系人名称
mobile  |String | 是 |  客户联系人手机
attached |String | 是   |  客户联系人备注
modified_by |String | 是   |  修改时间

##### 返回说明

```
{
    "errcode": 0,
    "errmsg": "ok"
}
```
参数 | 说明
---- | -----
errcode | 返回码
errmsg | 对返回码的文本描述内容

## 员工删除客户联系人

##### 请求说明

Https请求方式: POST

`https://oapi.dingtalk.com/crm/contact/delete?access_token=ACCESS_TOKEN&user_id=USER_ID`

##### 请求包结构体

```
{
"contactid[]":"客户联系人id1"
}

```

##### 参数说明

参数 | 参数类型 | 必须 | 说明
---------- | ------- | ------- | ------
access_token |String | 是 | 调用接口凭证
user_id |String | 是 | 员工id
contactid  |String[] | 是  |  客户id
##### 返回说明

```
{
    "errcode": 0,
    "errmsg": "ok"
}
```
参数 | 说明
---- | -----
errcode | 返回码
errmsg | 对返回码的文本描述内容

## 员工客户关系新增

##### 请求说明

Https请求方式: POST

`https://oapi.dingtalk.com/crm/empcustomer/create?access_token=ACCESS_TOKEN`

##### 请求包结构体

```
{
    "customerId":"客户id",
    "userId":"员工id",
    "create_by":"创建时间"
}

```

##### 参数说明

参数 | 参数类型 | 必须 | 说明
---------- | ------- | ------- | ------
access_token |String | 是 | 调用接口凭证
customerId |String | 是 | 客户id
userId  |String | 是  |  员工id
create_by  |String | 是  |  创建时间

##### 返回说明

```
{
    "errcode": 0,
    "errmsg": "ok"
}
```
参数 | 说明
---- | -----
errcode | 返回码
errmsg | 对返回码的文本描述内容

## 员工客户关系删除

##### 请求说明

Https请求方式: POST

`https://oapi.dingtalk.com/crm/empcustomer/delete?access_token=ACCESS_TOKEN`

##### 请求包结构体

```
{
"customerId":"客户id",
"userId":"员工id",
"modified_by":"修改时间"
}

```

##### 参数说明

参数 | 参数类型 | 必须 | 说明
---------- | ------- | ------- | ------
access_token |String | 是 | 调用接口凭证
customerId |String | 是 | 客户id
userId  |String | 是  |  员工id
modified_by  |String | 是  |  修改时间

##### 返回说明

```
{
    "errcode": 0,
    "errmsg": "ok"
}
```
参数 | 说明
---- | -----
errcode | 返回码
errmsg | 对返回码的文本描述内容

