###		1. $(document).ready(function(){});
		2. $(function(){}); 推荐使用

		jQuery 就是$  ,  $代表了jQuery
		源码:window.jQuery = window.$ = jQuery;

		jq对象  .css('attr','value')

		jq对象具有的css方法能够方便的设置样式
		例如: $('#h1').css('color','green');

####		>子代选择器,选择所有的子代元素,不包含孙子
		    +紧邻选择器,选择紧挨着的下一个元素
		    ~ 兄弟选择器,选择后面的所有的兄弟元素


		    find()  查找指定元素得所有后代元素(子子孙孙)
		    children() 查找指定元素的直接子元素(亲儿子元素)
		    siblings()查找所有兄弟元素(不包括自己)
		    parent() 查找父元素(亲的)
		    eq(index)  查看指定元素的第index个元素,index是索引号,从0开始.
		    :eq(index)选择器只匹配一个元素,:eq()选择器中要写变量，即index是动态变化的，则需要用+  +连接

####		addClass() - 向被选元素添加一个或多个类
		    removeClass() - 从被选元素删除一个或多个类
		    hasClass()- 判断是否存在类,如果不写参数
		    toggleClass() - 对被选元素进行添加/删除类的切换操作

		    siblings()  除了自己以外的所有的兄弟节点
		    next()	下一个兄弟
		    nextAll()	后面所有的兄弟
		    nextUntil()	后面所有的兄弟直到
		    prev()	    前面的兄弟
		    prevAll()		前面所有的兄弟


####      on绑定事件的运用  
   <script>
		//监听的形式绑定
		// 可以同时添加多个事件  "然并卵"
		$('.d1').on('click mouseenter',function () {
			// alert('fff');
			console.log('fff');
		})
		$('.btn1').click(function () {
			//解绑事件
			$('.d1').off('click');
		})
	</script>

###   append() 方法在被选元素的结尾（仍然在内部）插入指定内容
    $("button").click(function(){
      $("p").append(" <b>Hello world!</b>");
    });


###    触发事件
   <script>
		$('.d1').click(function () {
			alert('d1');
		})
		$('.btn1').click(function(){
			// 1.通过表单获取事件名称
			var eventName = $('.eventName').val();
			// 通过传递字符串 触发事件
			// 用的很少
			// $('.d1').trigger(eventName);
			$('.d1').triggerHandler(eventName);
		})

	</script>

     event.data 			传递给事件处理程序的额外数据
     event.currentTarget 	等同于this，当前DOM对象
     event.pageX 			鼠标相对于文档左部边缘的位置
     event.target 			触发事件源，不一定===this
   <script>
		$('.d1').click(function (event) {
			// event触发的对象是谁
			// currentTarget   this
			// target  实际触发的对象
			console.log(event.currentTarget);
			// srcElement  target
			// 可以用于实现委托
			console.log(event.target);
		})

	</script>


###    阻止冒泡
       event.stopPropagation()；	阻止事件冒泡
       event.preventDefault(); 	阻止默认行为

###    隐式迭代
   <script>
		// jq会对选择到的元素(集合)进行迭代(看不到),给每一个元素添加事件或者修改样式
		$('.box').click(function () {
			alert('fff');
		})

		console.log($('.box').text());
	</script>

###3
   <script>
		// 1.$(document).ready(function(){});
		// 2.2.$(function(){});  推荐
		// jquery 就是 $  , $ 就是代表了jquery	
		// 源码: window.jQuery = window.$ = jQuery;
		// 变量: 字母数字下划线 还有 $
		// $(document).ready(function(){
		// 	alert('abc');
		// })
		$(function(){

			alert('abc');
		})
	</script>

####   样式操作
   <script>
		$(function() {
			// d1是一个jquery对象 
			var d1 = $('.d1');
			console.log(d1);
			// jq对象 .css('attr','value')  jq对象具有的css方法能够方便的是设置样式
			d1.css('background-color','red');
			$('#h1').css('color','green');
			$('.d1 .p1').css('color','yellow');
			$('.d1 .p2').css('fontSize','30px');
		})
	</script>

   <script>
		$('li').eq(1).css('color','red');
		$('.li3').siblings().css('backgroundColor','green');
		//children 只能选择直接孩子节点
		// children/find 如果不写具体类型,则选中所有的孩子节点
		// $('.box').children().css('width','250px');
		$('.box').children('div').css('width','250px');
		//find 从所有的后代元素中找到符合条件的 
		$('.box').find('div').css('opacity','.5');
		// 注意: 原生的js选择关系都用属性,而jq都是封装的方法
		$('.p1').parent().css('border','20px solid red');
	</script>

   <script>
		//jq绑定方法 不需要on,而且click接受的参数为 函数类型
		$('.d1').click(function () {
			// alert('fff');
			// 注意: 如果事件是 $('.d1').click = fn 那么this指的是$('.d1'),
			// 但这里是在回调函数里,this一般会发生变化
			//在jq的事件里,this指向绑定该事件的dom元素本身
			// console.log(this);
			//css() 是jq对象的方法,这里需要把this变为jq对象才能使用
			$(this).css('background-color','red');
		})
		// $('.d1').click(function () {
		// 	alert('ffdddf');
		// })

	</script>	

###   jq对象和dom的相互转换
   <script>
		//jq和原生js写法 可以共存!
		// window.onload = function () {
		// 	$('.d1').css('background','pink')
		// }
		// d1 原生的dom元素
		var d1 = document.getElementsByClassName('d1')[0];
		//  css() 这个方法 是jq对象特有的方法
		// 原生对象要转换为jq对象 
		$(d1).css('background','pink');
		$('.d1').click(function () {
			//点击事件里的this指向 原生对象
			console.log(this);
			console.log($(this));
			console.log($('.d1'));
			//通过jq对象可以取到原生对象
			console.log($('.d1')[0]);
		})
	</script>