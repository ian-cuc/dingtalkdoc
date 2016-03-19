# UI控件
- category: 客户端开发文档
- order: 16---
dd.ui

## 输入框

0.0.2

```javascript
dd.ui.input.plain({
    placeholder: '说点什么吧', //占位符
    text: '', //默认填充文本
    onSuccess: function(data) {
    	//onSuccess将在点击发送之后调用
        /*{
            text: String
        }*/
    },
    onFail: function() {

    }
})
```
<img src="https://img.alicdn.com/tps/TB1ju0BKVXXXXcrXpXXXXXXXXXX-200-356.png" width = "200" height = "355" alt="图片名称" align=right />

#### 参数说明

参数 | 参数类型 | 说明
----- | ----- | -----
placeholder | String | 占位符
text | String | 默认填充文本

#### 返回说明
参数 | 说明
----- | ------
text | 返回文本

## 设置顶部进度条颜色

0.0.5

```javascript
dd.ui.progressBar.setColors({
    colors: [], //array[number] 进度条变化颜色，最多支持4个颜色
    onSuccess: function(data) {
        /*
            true:成功  false:失败
        */
    },
    onFail: function() {
    }
})
```
#### 参数说明

参数 | 参数类型 | 说明
----- | ----- | -----
colors | array[number] | 进度条变化颜色，最多支持4个颜色



## 启用下拉刷新

0.0.5

```javascript
dd.ui.pullToRefresh.enable({
    onSuccess: function() {
    },
    onFail: function() {
    }
})
```

## 收起下拉loading

0.0.5

```javascript
dd.ui.pullToRefresh.stop()
```

## 禁用下拉刷新

0.0.5

```javascript
dd.ui.pullToRefresh.disable()
```

## 启用bounce

启用iOS webview弹性效果(仅iOS支持) 0.0.5

```javascript
dd.ui.webViewBounce.enable()
```

## 禁用bounce

禁用iOS webview弹性效果(仅iOS支持) 0.0.5

```javascript
dd.ui.webViewBounce.disable()
```

##扫码

dd.biz

0.0.6

```javascript
dd.biz.util.scan({
    type: String,//type为qrCode或者barCode
    onSuccess: function(data) {
    //onSuccess将在扫码成功之后回调
      /* data结构
        { 'text': String}
      */
    },
   onFail : function(err) {
   }
})
```

#### 参数说明

参数 | 参数类型 | 说明
----- | ----- | -----
type | String | type为qrCode或者barCode

####　返回说明

参数 | 说明
------|------
text | 扫码内容

