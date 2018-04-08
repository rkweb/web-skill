# skrollr

用于移动端和PC端的独立视差滚动库

[http://test.go.163.com/go/2017/0530/sxproject_three/js/skrollr.js](http://test.go.163.com/go/2017/0530/sxproject_three/js/skrollr.js)


## Dome

[Demo1][demo1]（wap）

![](../../images/skrollr-eqCode1.png) 

-----------

[Demo2][demo2]（wap）

![](../../images/skrollr-eqCode2.png)

----------
  
[Demo3][demo3]（PC）


## 使用说明

### HTML

```html
<div id="slides-container">
	//data值从0-1200-1800-2400中每段间隔执行不同动画
	<div id="rect" 
		data-0="top:0%;left:0%" 
		data-1200='top:50%;left:50%' 
		data-1800='top:50%;left:100%' 
		data-2400='top:90%;left:0%'>
	</div>
</div>
```

### CSS

```css
*{
    margin: 0;
    padding: 0;
}
    			
html,body{
    width: 100%;
    height: 100%;
}
    			
#slides-container {
    width: 100%;
    height: 100%;
}
    			
#rect {
    position: absolute;
    width: 100px;
    height: 100px;
    background: red;
}
```

### JavaScript

```javascript
<script src="js/skrollr.js" type="text/javascript" charset="utf-8"></script>
<script type="text/javascript">
	window.onload = function() {
		var s = skrollr.init({
 			// 实时的data位置
			// 建议根据实时的data值写动画，而不是滑动的距离
			render: function(data) {
				console.log(data.curTop);
			}
		});
	}
</script>
```

## 注意事项
1. `data-0` 为初始直，`data-max（max代表一个数值）` 为div中出现的最大值，最终位置以 `data-max` 的值为准，无论是在哪个div的data值，值的大小必须依次增加。

2. 如果想让页面保持不动的执行动画，例如data-1200到data-1800之间停止垂直动画，开始水平动画，代码如下：

	```html
	<div id="rect" 
		data-0="top:0%;left:0%" 
		// 上下的位置一样，左右可变值
		data-1200='top:50%;left:50%' 
		data-1800='top:50%;left:100%' 
		data-2400='top:90%;left:0%'>
	</div>
	```

3. 不建议在单页面出现大量的动画，在移动端可能会有卡顿的现象

------

关于一些API方法以及data的各类属性：
[https://github.com/Prinzhorn/skrollr](https://github.com/Prinzhorn/skrollr)

[demo1]:http://test.go.163.com/go/2017/0530/sxproject_three/
[demo2]:http://test.go.163.com/go/2017/0530/glgs/
[demo3]:http://test.go.163.com/go/2017/0530/sx/