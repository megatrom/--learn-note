######     style.left 与offsetLeft之间的区别
          offsetLeft 获取的是相对于父对象的左边距
			left 获取或设置相对于 具有定位属性(position定义为relative)的父对象 的左边距
			如果父div的position定义为relative,子div的position定义为absolute，那么子div的style.left的值是相对于父div的值，
         这同offsetLeft是相同的，区别在于：
			1. style.left 返回的是字符串，如28px，offsetLeft返回的是数值28，如果需要对取得的值进行计算，
			还用offsetLeft比较方便。
			2. style.left是读写的，offsetLeft是只读的，所以要改变div的位置，只能修改style.left


#####       ScrollWidth/ScrollHeight  计算的是内容的实际宽/高,不包含边框.

            //存在兼容问题
			// console.log(document.body.scrollTop);
			//兼容写法
			// window.pageYOffset 高级浏览器才有
			// document.documentElement.scrollTop ie6,7,8 
			// document.body.scrollTop 怪异模式
			// offsetLeft / pageXOffset 跟这个一样 不过在实际页面中几乎不存在

     var top= window.pageYOffset || document.documentElement.scrollTop || document.body.scrollTop || 0;

####   event 事件对象 即触发这个事件的事件本身
             // event 只能在高级浏览器获取事件对象
			// 在ie中需要通过window.event获取
			//兼容写法
			var e = event || window.event;
## scroll家族

+ scrollWidth/scrollHeight
	- 元素的宽高,不包括border,但是包括padding.
	- 元素的内容如果超出,获取的是元素内容的实际高度.
	- 即使元素overflow:hideen,依然能获取元素内容高度.

+ scrollTop / scrollLeft
	- 获取元素被卷进去的高度/left,值为number类型.
	- 读写属性. 可以被重新赋值,但是应该是number类型(不能带px).document.documentElement.scrollTop =intvalue;


+ scrollTop兼容问题
```javascript
	// 注意收集总结"代码块" , 即使是收集代码块,尽量也能看懂.
	var top= window.pageYOffset || document.documentElement.scrollTop || document.body.scrollTop || 0;
	var top= document.documentElement.scrollTop ||document.body.scrollTop;

```
+ onscroll 用于监听浏览器滚动事件,哪怕滚动1px也会触发.

+ window.scrollTo(x,y); 浏览器定位到页面的固定位置.

## 骨架标签获取

+ html  document.documentElement
+ title document.title = 'xx'
+ body  document.body
+ head  document.head


## 案例
+ 固定导航栏  
	- 页面100%高度的实现
	- element.offsetHeight 元素的高度
	- window.scrollTo(0,x);
	- document.documentElement.scrollTop = value;
	- 缓动函数的修改

+ 返回头部火箭
	- 获取被卷进去的高度
	- window.onscrll
	- window.scrollTo(0,x);
	- document.documentElement.scrollTop = value;
	- 缓动函数的修改

+ 广告跟随
	- element.offsetTop 距离上一个定位元素(body)的距离
	- 获取被卷进去的高度
	- 缓动函数修改


## offset家族
+ offsetWidth/offsetHeight
	- 获取元素的宽高,包括padding和border,指的是元素的实际大小
	- 获取的结果是number类型
	- 是一个只读属性
	- 获取的结果是四舍五入的值(即使width/height=xx.xxpx)

+ offsetLeft/offsetTop
	- 获取元素距离上一个定位元素(body)的距离
	- 结果为number类型,只读属性

+ offsetParent
	- 获取上一个定位元素
	- 如果没有定位元素,获取body对象
	- 案例(求任意元素距离body的距离)

## 案例
+ 闪现动画
+ 匀速动画
+ 匀速轮播
+ 缓动轮播
	- 缓动公式  leader = leader + (target-leader)/10;
	- offsetLeft/offsetWidth
	- setInterval/clearInterval
+ 缓动轮播的实现(多种事件的添加)
	


