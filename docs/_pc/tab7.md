# 导航
- category: PC端开发文档
- order: 8---
DingTalkPC.biz

## 触发关闭

注意：只在SlidePanel和Modal里起作用

``` javascript
DingTalkPC.biz.navigation.quit({
    message: "quit message",//退出信息，传递给openModal或者openSlidePanel的onSuccess函数的result参数
    onSuccess : function(result) {
        /**/
    },
    onFail : function() {}
})
```

| 参数      | 参数类型   | 说明                                       |
| ------- | ------ | ---------------------------------------- |
| message | String | 退出信息，传递给openModal或者openSlidePanel的onSuccess函数的result参数 |

## 设置标题

注意：只在SlidePanel和Modal里起作用

``` javascript
DingTalkPC.biz.navigation.setTitle({
    title: "lalala",//标题
    onSuccess : function(result) {
        /**/
    },
    onFail : function() {}
})
```

| 参数    | 参数类型   | 说明   |
| ----- | ------ | ---- |
| title | String | 标题   |

## 设置左侧导航按钮

注意：只在SlidePanel里起作用

``` javascript
DingTalkPC.biz.navigation.setLeft({
    text: "lalala",//显示文字信息
    onSuccess : function(result) {
        /**/
    },
    onFail : function() {}
})
```

| 参数   | 参数类型   | 说明     |
| ---- | ------ | ------ |
| text | String | 显示文字信息 |

### 设置左侧按钮点击后的回调

DingTalkPC.addEventListener('leftBtnClick', handleFn);

``` javascript
//添加监听回调函数
DingTalkPC.addEventListener('leftBtnClick', handleFn);

//移除相应handleFn的监听回调函数
DingTalkPC.removeEventListener('leftBtnClick', handleFn);

```



