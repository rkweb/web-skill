# elCanvas #
Canvas移动端绘图（支持导出base64）
demo:[http://test.go.163.com/go/2015/public/team/liwenhui/elCanvas/](http://test.go.163.com/go/2015/public/team/liwenhui/elCanvas/)

## 引用js ##
（首先引用Zepto：http://go.163.com/2015/public/common/js/zepto.min.js）
  
http://test.go.163.com/go/2015/public/team/liwenhui/elCanvas/js/elCanvas.js

## 接口说明 ##
1. 调用(传入参数)
     
		var elCanvas = new ElCanvas( {		
			obj: '#canvas',  画布
			color: '#000',   画笔颜色( 默认值 '#000' )
			width: '5'		 画笔大小( 默认值 '10' )	
		} );

2. 清除画布

		elCanvas.clear();
		

3. 获取返回的base64

		elCanvas.base64();


4. 用swiper时，锁定画布当前页