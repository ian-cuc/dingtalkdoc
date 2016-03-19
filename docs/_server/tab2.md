# 管理通讯录
- category: 服务端开发文档
- order: 3---
## 获取部门列表

##### 请求说明

Https请求方式: GET

`https://oapi.dingtalk.com/department/list?access_token=ACCESS_TOKEN`

##### 参数说明

参数 | 参数类型 | 必须 | 说明
---------- | ------- | ------- | ------
access_token | String | 是 | 调用接口凭证

##### 返回结果

```
{
    "errcode": 0,
    "errmsg": "ok",
    "department": [
        {
           "id": 2,
            "name": "钉钉事业部",
            "parentid": 1,
            "createDeptGroup": true,
            "autoAddUser": true
        },
        {
            "id": 3,
            "name": "服务端开发组",
            "parentid": 2,
            "createDeptGroup": false,
            "autoAddUser": false
        }
    ]
}
```

参数 | 说明
---- | -----
errcode | 返回码
errmsg | 对返回码的文本描述内容
department | 部门列表数据。以部门的order字段从小到大排列
id | 部门id
name | 部门名称
parentid | 父部门id，根部门为1
createDeptGroup | 是否同步创建一个关联此部门的企业群, true表示是, false表示不是
autoAddUser | 当群已经创建后，是否有新人加入部门会自动加入该群, true表示是, false表示不是


## 获取部门详情

##### 请求说明

Https请求方式: GET

`https://oapi.dingtalk.com/department/get?access_token=ACCESS_TOKEN&id=2`

##### 参数说明

参数 | 参数类型 | 必须 | 说明
---------- | ------- | ------- | ------
access_token | String | 是 | 调用接口凭证
id | String | 是 | 部门id

##### 返回结果

```
{
    "errcode": 0,
    "errmsg": "ok",
    "id": 2,
    "name": "钉钉事业部",
    "order" : 10,
    "parentid": 1,
    "createDeptGroup": true,
    "autoAddUser": true,
    "deptHiding" : true,
    "deptPerimits" : "3|4",
    "userPerimits" : "userid1|userid2",
    "outerDept" : true,
    "outerPermitDepts" : "1|2",
    "outerPermitUsers" : "userid3|userid4",
    "orgDeptOwner" : "manager1122",
    "deptManagerUseridList" : "manager1122|manager3211"
}
```

参数 | 说明
---- | -----
errcode | 返回码
errmsg | 对返回码的文本描述内容
id | 部门id
name | 部门名称
parentid | 父部门id，根部门为1
order | 在父部门中的次序值
createDeptGroup | 是否同步创建一个关联此部门的企业群, true表示是, false表示不是
autoAddUser | 当群已经创建后，是否有新人加入部门会自动加入该群, true表示是, false表示不是
deptHiding | 是否隐藏部门, true表示隐藏, false表示显示
deptPerimits | 可以查看指定隐藏部门的其他部门列表，如果部门隐藏，则此值生效，取值为其他的部门id组成的的字符串，使用' &#124; '符号进行分割
userPerimits | 可以查看指定隐藏部门的其他人员列表，如果部门隐藏，则此值生效，取值为其他的人员userid组成的的字符串，使用' &#124; '符号进行分割
outerDept | 是否本部门的员工仅可见员工自己, 为true时，本部门员工默认只能看到员工自己
outerPermitDepts | 本部门的员工仅可见员工自己为true时，可以配置额外可见部门，值为部门id组成的的字符串，使用' &#124; '符号进行分割
outerPermitUsers | 本部门的员工仅可见员工自己为true时，可以配置额外可见人员，值为userid组成的的字符串，使用' &#124; '符号进行分割
orgDeptOwner | 企业群群主
deptManagerUseridList | 部门的主管列表,取值为由主管的userid组成的字符串，不同的userid使用' &#124; '符号进行分割


## 创建部门

##### 请求说明

Https请求方式: POST

`https://oapi.dingtalk.com/department/create?access_token=ACCESS_TOKEN`

##### 请求包结构体

```
{
    "name": "钉钉事业部",
    "parentid": "1",
    "order": "1",
    "createDeptGroup": true
}
```

##### 参数说明

参数 | 参数类型 | 必须 | 说明
----------| ------- | ------- | ------
access_token | String | 是 | 调用接口凭证
name | String | 是 |  部门名称。长度限制为1~64个字符
parentid | String | 是 | 父部门id。根部门id为1
order  | String | 否 | 在父部门中的次序值。order值小的排序靠前
createDeptGroup | Boolean | 否 | 是否创建一个关联此部门的企业群，默认为false

##### 返回结果

```
{
    "errcode": 0,
    "errmsg": "created",
    "id": 2
}
```

参数 | 说明
----------  | ------
errcode | 返回码
errmsg | 对返回码的文本描述内容
id | 创建的部门id


## 更新部门

##### 请求说明

Https请求方式: POST

`https://oapi.dingtalk.com/department/update?access_token=ACCESS_TOKEN`

##### 请求包结构体

```
{
    "name": "钉钉事业部",
    "parentid": "1",
    "order": "1",
    "id": "1",
    "createDeptGroup": true,
    "autoAddUser": true,
    "deptManagerUseridList": "manager1111|2222",
    "deptHiding" : true,
    "deptPerimits" : "3|4",
    "userPerimits" : "userid1|userid2",
    "outerDept" : true,
    "outerPermitDepts" : "1|2",
    "outerPermitUsers" : "userid3|userid4",
    "orgDeptOwner": "manager1111"
}
```

##### 参数说明

参数 | 参数类型 | 必须 | 说明
----------| -------  | ------- | ------
access_token | string | 是 | 调用接口凭证
name | String | 否 | 部门名称。长度限制为1~64个字符
parentid | String | 否 | 父部门id。根部门id为1
order | String | 否 | 在父部门中的次序值。order值小的排序靠前
id | long | 是 | 部门id
createDeptGroup | Boolean | 否 | 是否创建一个关联此部门的企业群
autoAddUser | Boolean | 否 | 如果有新人加入部门是否会自动加入部门群
deptManagerUseridList | String | 否 | 部门的主管列表,取值为由主管的userid组成的字符串，不同的userid使用' &#124; '符号进行分割
deptHiding | Boolean | 否 | 是否隐藏部门, true表示隐藏, false表示显示
deptPerimits | String | 否 | 可以查看指定隐藏部门的其他部门列表，如果部门隐藏，则此值生效，取值为其他的部门id组成的的字符串，使用' &#124; '符号进行分割
userPerimits | String | 否 | 可以查看指定隐藏部门的其他人员列表，如果部门隐藏，则此值生效，取值为其他的人员userid组成的的字符串，使用' &#124; '符号进行分割
outerDept | Boolean | 否 | 是否本部门的员工仅可见员工自己, 为true时，本部门员工默认只能看到员工自己
outerPermitDepts | String | 否 | 本部门的员工仅可见员工自己为true时，可以配置额外可见部门，值为部门id组成的的字符串，使用' &#124; '符号进行分割
outerPermitUsers | String | 否 | 本部门的员工仅可见员工自己为true时，可以配置额外可见人员，值为userid组成的的字符串，使用' &#124; '符号进行分割
orgDeptOwner | String | 否 | 企业群群主


##### 返回结果

```
{
    "errcode": 0,
    "errmsg": "updated"
}
```

参数 | 说明
---------- | ------
errcode | 返回码
errmsg | 对返回码的文本描述内容

## 删除部门

##### 请求说明

Https请求方式: GET

`https://oapi.dingtalk.com/department/delete?access_token=ACCESS_TOKEN&id=ID`

##### 参数说明

参数 | 参数类型 | 必须 | 说明
----------| -------  | ------- | ------
access_token | String | 是 | 调用接口凭证
id | long | 是 | 部门id。（注：不能删除根部门；不能删除含有子部门、成员的部门）

##### 返回结果

```
{
    "errcode": 0,
    "errmsg": "deleted"
}
```

参数 | 说明
---------- | ------
errcode | 返回码
errmsg | 对返回码的文本描述内容

## 获取成员详情

##### 请求说明

Https请求方式: GET

`https://oapi.dingtalk.com/user/get?access_token=ACCESS_TOKEN&userid=zhangsan`

参数 | 参数类型 | 必须 | 说明
---------- | ------- | ------- | ------
access_token | String | 是 | 调用接口凭证
userid | String |是 | 员工在企业内的UserID，企业用来唯一标识用户的字段。

##### 返回结果

```
{
    "errcode": 0,
    "errmsg": "ok",
    "userid": "zhangsan",
    "name": "张三",
    "tel" : "010-123333",
    "workPlace" :"",
    "remark" : "",
    "mobile" : "13800000000",
    "email" : "dingding@aliyun.com",
    "active" : true,
    "orderInDepts" : "{1:10, 2:20}",
    "isAdmin" : false,
    "isBoss" : false,
    "dingId" : "WsUDaq7DCVIHc6z1GAsYDSA",
    "isLeaderInDepts" : "{1:true, 2:false}",
    "isHide" : false,
    "department": [1, 2],
    "position": "工程师",
    "avatar": "dingtalk.com/abc.jpg",
    "jobnumber": "111111",
    "extattr": {
                "爱好":"旅游",
                "年龄":"24"
                }
}
```

参数 |说明
---------- | ------
errcode | 返回码
errmsg | 对返回码的文本描述内容
userid | 员工唯一标识ID（不可修改）
name | 成员名称
tel  | 分机号（ISV不可见）
workPlace | 办公地点（ISV不可见）
remark | 备注（ISV不可见）
mobile | 手机号码（ISV不可见）
email | 电子邮箱（ISV不可见）
active | 是否已经激活, true表示已激活, false表示未激活
orderInDepts | 在对应的部门中的排序, Map结构的json字符串, key是部门的Id, value是人员在这个部门的排序值
isAdmin | 是否为企业的管理员, true表示是, false表示不是
isBoss | 是否为企业的老板, true表示是, false表示不是
dingId | 钉钉Id
isLeaderInDepts | 在对应的部门中是否为主管, Map结构的json字符串, key是部门的Id, value是人员在这个部门中是否为主管, true表示是, false表示不是
isHide | 是否号码隐藏, true表示隐藏, false表示不隐藏
department | 成员所属部门id列表
position | 职位信息
avatar | 头像url
jobnumber | 员工工号
extattr | 扩展属性，可以设置多种属性(但手机上最多只能显示10个扩展属性，具体显示哪些属性，请到OA管理后台->设置->通讯录信息设置和OA管理后台->设置->手机端显示信息设置)性

## 创建成员

##### 请求说明

Https请求方式: POST

`https://oapi.dingtalk.com/user/create?access_token=ACCESS_TOKEN`

##### 请求包结构体

```
{
    "userid": "zhangsan",
    "name": "张三",
    "orderInDepts" : "{1:10, 2:20}",
    "department": [1, 2],
    "position": "产品经理",
    "mobile": "15913215421",
    "tel" : "010-123333",
    "workPlace" :"",
    "remark" : "",
    "email": "zhangsan@gzdev.com",
    "jobnumber": "111111",
    "isHide": false,
    "isSenior": false,
    "extattr": {
                "爱好":"旅游",
                "年龄":"24"
                }
}
```

##### 参数说明

参数 | 参数类型 | 必须 | 说明
---------- | -------  | ------- | ------
access_token |String | 是 | 调用接口凭证
userid | String| 否 | 员工唯一标识ID（不可修改），企业内必须唯一。长度为1~64个字符，如果不传，服务器将自动生成一个userid
name | String | 是 | 成员名称。长度为1~64个字符
orderInDepts | JSONObject | 否 | 在对应的部门中的排序, Map结构的json字符串, key是部门的Id, value是人员在这个部门的排序值
department | List | 是 |数组类型，数组里面值为整型，成员所属部门id列表
position |String | 否 | 职位信息。长度为0~64个字符
mobile | String| 是 | 手机号码。企业内必须唯一
tel  | String| 否 | 分机号，长度为0~50个字符
workPlace | String| 否 | 办公地点，长度为0~50个字符
remark | String| 否 | 备注，长度为0~1000个字符
email | String| 否 | 邮箱。长度为0~64个字符。企业内必须唯一
jobnumber | String | 否 | 员工工号。对应显示到OA后台和客户端个人资料的工号栏目。长度为0~64个字符
isHide | Boolean| 否 | 是否号码隐藏, true表示隐藏, false表示不隐藏。隐藏手机号后，手机号在个人资料页隐藏，但仍可对其发DING、发起钉钉免费商务电话。
isSenior | Boolean| 否 | 是否高管模式，true表示是，false表示不是。开启后，手机号码对所有员工隐藏。普通员工无法对其发DING、发起钉钉免费商务电话。高管之间不受影响。
extattr | JSONObject | 否 | 扩展属性，可以设置多种属性(但手机上最多只能显示10个扩展属性，具体显示哪些属性，请到OA管理后台->设置->通讯录信息设置和OA管理后台->设置->手机端显示信息设置)

##### 返回结果

```
{
    "errcode": 0,
    "errmsg": "created",
    "userid": "dedwefewfwe1231"
}
```

参数 | 说明
---------- | ------
errcode | 返回码
errmsg | 对返回码的文本描述内容
userid | 员工唯一标识

## 更新成员

##### 请求说明

Https请求方式: POST

`https://oapi.dingtalk.com/user/update?access_token=ACCESS_TOKEN`

##### 请求包结构体

```
{
    "userid": "zhangsan",
    "name": "张三",
    "department": [1, 2],
    "orderInDepts": "{1:10}", 
    "position": "产品经理",
    "mobile": "15913215421",
    "tel" : "010-123333",
    "workPlace" :"",
    "remark" : "",
    "email": "zhangsan@gzdev.com",
    "jobnumber": "111111",
    "isHide": false,
    "isSenior": false,
    "extattr": {
                "爱好":"旅游",
                "年龄":"24"
                }
}
```

##### 参数说明（如果非必须的字段未指定，则钉钉后台不改变该字段之前设置好的值）

参数 | 参数类型 | 必须 | 说明
---------- | ------- | ------- | ------
access_token |String | 是 | 调用接口凭证
userid |String | 是 | 员工唯一标识ID（不可修改），企业内必须唯一。长度为1~64个字符
name |String | 是 | 成员名称。长度为1~64个字符
department |List | 否 | 成员所属部门id列表
orderInDepts | JSONObject | 否 | 实际是Map的序列化字符串，Map的Key是deptId，表示部门id，Map的Value是order，表示排序的值，列表是按order的倒序排列输出的，即从大到小排列输出的
position | String| 否 | 职位信息。长度为0~64个字符
mobile |String | 否 | 手机号码。企业内必须唯一
tel  | String| 否 | 分机号，长度为0~50个字符
workPlace | String| 否 | 办公地点，长度为0~50个字符
remark | String| 否 | 备注，长度为0~1000个字符
email |String | 否 | 邮箱。长度为0~64个字符。企业内必须唯一
jobnumber | String | 否 | 员工工号，对应显示到OA后台和客户端个人资料的工号栏目。长度为0~64个字符
isHide | Boolean| 否 | 是否号码隐藏, true表示隐藏, false表示不隐藏。隐藏手机号后，手机号在个人资料页隐藏，但仍可对其发DING、发起钉钉免费商务电话。
isSenior | Boolean| 否 | 是否高管模式，true表示是，false表示不是。开启后，手机号码对所有员工隐藏。普通员工无法对其发DING、发起钉钉免费商务电话。高管之间不受影响。
extattr |JSONObject | 否 | 扩展属性，可以设置多种属性(但手机上最多只能显示10个扩展属性，具体显示哪些属性，请到OA管理后台->设置->通讯录信息设置和OA管理后台->设置->手机端显示信息设置)

##### 返回结果

```
{
    "errcode": 0,
    "errmsg": "updated"
}
```

参数 | 说明
---------- | ------
errcode | 返回码
errmsg | 对返回码的文本描述内容

## 删除成员

##### 请求说明

Https请求方式: GET

`https://oapi.dingtalk.com/user/delete?access_token=ACCESS_TOKEN&userid=ID`


##### 参数说明

参数 | 参数类型 | 必须 | 说明
---------- | ------- | ------- | ------
access_token | String | 是 | 调用接口凭证
userid | String | 是 | 员工唯一标识ID（不可修改）

##### 返回结果

```
{
    "errcode": 0,
    "errmsg": "deleted"
}
```

参数 | 说明
---------- | ------
errcode | 返回码
errmsg | 对返回码的文本描述内容

## 批量删除成员

##### 请求说明
Https请求方式: POST

`https://oapi.dingtalk.com/user/batchdelete?access_token=ACCESS_TOKEN`

##### 请求包结构
```
{
   "useridlist":["zhangsan","lisi"]
}
```

##### 参数说明

参数 | 参数类型 | 必须 | 说明
----------| -------  | ------- | ------
access_token | String| 是 | 调用接口凭证
useridlist | List | 是 | 员工UserID列表。列表长度在1到20之间

##### 返回结果

```
{
    "errcode": 0,
    "errmsg": "deleted"
}
```

参数 | 说明
---------- | ------
errcode | 返回码
errmsg | 对返回码的文本描述内容

## 获取部门成员

##### 请求说明

Https请求方式: GET

`https://oapi.dingtalk.com/user/simplelist?access_token=ACCESS_TOKEN&department_id=1`

##### 参数说明

参数 | 参数类型 | 必须 | 说明
---------- | ------- | ------- | ------
access_token | String | 是 | 调用接口凭证
department_id | long | 是 | 获取的部门id
offset | long | 否 | 支持分页查询，与size参数同时设置时才生效，此参数代表偏移量
size | int | 否 | 支持分页查询，与offset参数同时设置时才生效，此参数代表分页大小，最大100
order | String | 否 | 支持分页查询，部门成员的排序规则，默认不传是按自定义排序；entry_asc代表按照进入部门的时间升序，entry_desc代表按照进入部门的时间降序，modify_asc代表按照部门信息修改时间升序，modify_desc代表按照部门信息修改时间降序，custom代表用户定义(未定义时按照拼音)排序

##### 返回结果

```
{
    "errcode": 0,
    "errmsg": "ok",
    "hasMore": false,
    "userlist": [
        {
            "userid": "zhangsan",
            "name": "张三"
        }
    ]
}
```

参数 | 说明
---------- | ------
errcode | 返回码
errmsg | 对返回码的文本描述内容
hasMore | 在分页查询时返回，代表是否还有下一页更多数据
userlist | 成员列表
userid | 员工唯一标识ID（不可修改）
name | 成员名称

## 获取部门成员（详情）

##### 请求说明

Https请求方式: GET

`https://oapi.dingtalk.com/user/list?access_token=ACCESS_TOKEN&department_id=1`

参数 | 参数类型 | 必须 | 说明
---------- | -------  | ------- | ------
access_token |String | 是 | 调用接口凭证
department_id | long | 是 | 获取的部门id
offset | long | 否 | 支持分页查询，与size参数同时设置时才生效，此参数代表偏移量
size | int | 否 | 支持分页查询，与offset参数同时设置时才生效，此参数代表分页大小，最大100
order | String | 否 | 支持分页查询，部门成员的排序规则，默认不传是按自定义排序；entry_asc代表按照进入部门的时间升序，entry_desc代表按照进入部门的时间降序，modify_asc代表按照部门信息修改时间升序，modify_desc代表按照部门信息修改时间降序，custom代表用户定义(未定义时按照拼音)排序

##### 返回结果

```
{
    "errcode": 0,
    "errmsg": "ok",
    "hasMore": false,
    "userlist":[
        {
            "userid": "zhangsan",
            "dingId": "dwdded",
            "mobile": "13122222222",
            "tel" : "010-123333",
            "workPlace" :"",
            "remark" : "",
            "order" : 1,
            "isAdmin": true,
            "isBoss": false,
            "isHide": true,
            "isLeader": true,
            "name": "张三",
            "active": true,
            "department": [1, 2],
            "position": "工程师",
            "email": "zhangsan@alibaba-inc.com",
            "avatar":  "./dingtalk/abc.jpg",
            "jobnumber": "111111",
            "extattr": {
                "爱好":"旅游",
                "年龄":"24"
                }
        }
    ]
}
```

参数 | 说明
---------- | ------
errcode | 返回码
errmsg | 对返回码的文本描述内容
hasMore | 在分页查询时返回，代表是否还有下一页更多数据
userlist | 成员列表
userid | 员工唯一标识ID（不可修改）
order | 表示人员在此部门中的排序，列表是按order的倒序排列输出的，即从大到小排列输出的
dingId | 钉钉ID
mobile | 手机号（ISV不可见）
tel  | 分机号（ISV不可见）
workPlace | 办公地点（ISV不可见）
remark | 备注（ISV不可见）
isAdmin | 是否是企业的管理员, true表示是, false表示不是
isBoss | 是否为企业的老板, true表示是, false表示不是
isHide | 是否隐藏号码, true表示是, false表示不是
isLeader | 是否是部门的主管, true表示是, false表示不是
name | 成员名称
active | 表示该用户是否激活了钉钉
department | 成员所属部门id列表
position |  职位信息
email | 邮箱
avatar  | 头像url
jobnumber | 员工工号
extattr |  扩展属性，可以设置多种属性(但手机上最多只能显示10个扩展属性，具体显示哪些属性，请到OA管理后台->设置->通讯录信息设置和OA管理后台->设置->手机端显示信息设置)

<!--
"mobile": "15913215421",
mobile | 手机号码
-->

