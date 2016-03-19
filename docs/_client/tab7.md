# 钉盘
- category: 客户端开发文档
- order: 8---
dd.biz

##转存文件到钉盘

```javascript
	dd.biz.cspace.saveFile({
				corpId:"dingf8b3508f3073b265",
				url:"https://ringnerippca.files.wordpress.com/20.pdf",
				name:"文件名",         
				onSuccess: function(data) {
				 /* data结构
				 {"data":
    				[
    				{
     				"corpId": "", //公司id
      				"spaceId": "" //空间id
      				"fileId": "", //文件id
      				"fileName": "", //文件名
      				"fileSize": 111111, //文件大小
      				"fileType": "", //文件类型
     				}
   					]
   				 }
 				 */
		        },
	            onFail: function(err) {
	                alert(JSON.stringify(err));
	            }
			});
```
#### 参数说明

参数 | 参数类型 | 说明
----- | ----- | -----
corpId | String | 用户当前的corpid，将只能存储到当前corpid对应企业的钉盘和个人钉盘
url | String | 文件地址
name | String | 文件保存的名字

##钉盘文件预览

```javascript
	dd.biz.cspace.preview({
				corpId:"dingf8b3508f3073b265",
				spaceId:"13557022",
				fileId:"11452819",   
				fileName:"钉盘快速入门.pdf",
				fileSize:1024,
				fileType:"pdf", 
				onSuccess: function() {
					//无，直接在native显示文件详细信息
		        },
	            onFail: function(err) {
	                // 无，直接在native页面显示具体的错误
	            }
			});
```
#### 参数说明

参数 | 参数类型 | 说明
----- | ----- | -----
corpId | String | 用户当前的corpid，此文件预览成功后只能转发或保存到此corpId对应的企业群和个人
spaceId | String | 空间ID
fileId | String | 文件ID
fileName | String | 文件名称
fileSize | long | 文件大小，字节数
fileType | String | 文件扩展名


