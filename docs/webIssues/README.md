# 移动端常见问题 #
移动端开发常见问题汇总

## 目录
- [需要长按但不选中文本的方法](#需要长按但不选中文本的方法)
- [微信客户端二维码长按识别注意事项](#微信客户端二维码长按识别注意事项)
- [安卓输入框弹出键盘遮盖住文本框的解决办法](#安卓输入框弹出键盘遮盖住文本框的解决办法)
- [网易新闻客户端长按保存图片问题](#网易新闻客户端长按保存图片问题)



### 需要长按但不选中文本的方法

```css
//css
-webkit-touch-callout: none; /* disables the callout */
-webkit-user-select:none;
```

### 微信客户端二维码长按识别注意事项

```html
//html 用img标签
<img class="qr" src="img/s4/qr.png" alt="">
```

//css 不要用绝对定位 定位时只能用padding
```css
.qr {
    padding: 327px 0 0 144px;
}
```

### 安卓输入框弹出键盘遮盖住文本框的解决办法

```javascript
if(/Android [4-6]/.test(navigator.appVersion)) {
	window.addEventListener("resize", function() {
		if(document.activeElement.tagName=="INPUT" || document.activeElement.tagName=="TEXTAREA") {
			window.setTimeout(function() {
				document.activeElement.scrollIntoViewIfNeeded();
			},0);
		}
	})
}
```

### 网易新闻客户端长按保存图片问题

```

如果在body里面加了 -webkit-touch-callout: none; 在网易新闻客户端下无法长按保存图片(微信下可以)

需要在长按保存的元素或者它的父级加 -webkit-touch-callout: default;
```


