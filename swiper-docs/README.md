## 初始化swiper ##
- 定义swiper时, 定义成全局变量

#### HTML布局 ####
	<!-- Slider main container -->
	<div class="swiper-container">
	    <!-- Additional required wrapper -->
	    <div class="swiper-wrapper">
	        <!-- Slides -->
	        <div class="swiper-slide">Slide 1</div>
	        <div class="swiper-slide">Slide 2</div>
	        <div class="swiper-slide">Slide 3</div>
	    </div>
	    <!-- If we need pagination -->
	    <div class="swiper-pagination"></div>
	    
	    <!-- If we need navigation buttons -->
	    <div class="swiper-button-prev"></div>
	    <div class="swiper-button-next"></div>
	    
	    <!-- If we need scrollbar -->
	    <div class="swiper-scrollbar"></div>
	</div>

## 常用参数 ##
#### 1. 全屏滚动swiper常用参数 ####
	swiper = new Swiper('.swiper-container-main',{
	    //全屏滚动常用参数
	    initialSlide: 0,
	    direction: 'vertical',
	    onlyExternal: true,  //只能外部触发翻页

		//翻页的方式, 常用'fade'
		//注意: 当使用'fade'时, 翻页后, 上一页互动会与当前页冲突, 例如上一页如果有擦一擦效果等
		//解决办法: 翻页后, 其他页设置point-events: none;
		effect:'fade', 

	    //当外部swiper使用默认的class 'swiper-no-swiping'时, 会影响内部的swiper的翻动
		//所以当嵌套使用swiper时, 建议自定义noSwipingClass名称
		noSwipingClass: 'outer-no-swiping', 
		
		//以下三个属性在当前slide,前一个slide和后一个slide多加class sel, 用于分屏加载
	    slideActiveClass: 'swiper-slide-active sel', 
	    slideNextClass: 'swiper-slide-next sel',
	    slidePrevClass: 'swiper-slide-prev sel',

	    onInit:function(e){}, //swiper初始化时的动作
	    onTransitionEnd:function(swiper){ //整屏滑动时用onTransitionEnd不要用onSlideChangeEnd
			//每次翻页时, 加锁swiperLock = true; 防止多次翻页导致页面错误 当翻页结束时恢复swiperLock = false;
	        swipeLock = false;
	    }
	});
#### 2. 常规swiper常用参数 ####
	swiper = new Swiper('.swiper-container-main',{
	    autoplay: 2000, //自动轮播相隔的时间
	    loop: true, //是否可循环
	    spaceBetween: 20, //两个slide之间的距离
	    slidesPerView: 3, //每页slide页数
	    prevButton: '.swiper-button-prev', //向上按钮的class名
	    nextButton: '.swiper-button-next', //向下按钮的class名
	    pagination: '.swiper-pagination', //分页器class名
	    paginationClickable: false //分页器是否可点击
	});
#### 3. 长页面自由滚动swiper常用参数 (常用于评论区加载评论时) ####
	swiper = new Swiper('.swiper-container-main',{
	    freeMode: true,
	    slidesPerView: 'auto',
	    scrollbar: '.swiper-scrollbar', //scrollbar的class名
	    scrollbarHide: false //要不要隐藏scrollbar
	    //长页面的时候只创建一个swiper-slide, 所有内容都放进swiper-slide, 要设置swiper-slide的高度
	    //如果是动态的内容, 也要动态更改swiper-slide的高度, 并且更改之后执行swiper.update()
	});

## 常用属性和方法 ##
#### 属性 ####
	swiper.activeIndex //当前页的index
	swiper.isEnd //swiper是否滑到底, 常用于freemode模式
#### 方法 ####
	swiper.update(); //当改变swiper内部slide内容时, 要用swiper.update();
	swiper.slideTo(index, speed, runCallbacks);

## 常见问题 ##

1. 当有嵌套swiper时, 内层swiper设置了动效, 与内层swiper同级的dom元素的z-index失效.

	解决办法: 内层swiper设置transform: translate3d(0,0,0);
2. 当swiper内是视频时, 翻页后前页视频会继续播放, 并且Android端视频位置会错乱.

	解决办法: 翻页时删除其他页所有video标签, 动态加当前页video标签
