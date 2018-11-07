####    dom和node(节点)的区别
        dom和node(节点)的却别
	     dom元素指的是页面的标签,通过任意一个dom元素的关系可以找到当前页面其他任意的一个dom;
	    node节点指的是页面的任意元素,标签 换行符 注释 空格  属性 标签内容等都可以被当做node节点,当然既然是节点,也是可以被js选中的

	    js可以操作dom元素,包括dom元素的属性和内容

###     任何一个标签都有class 属性 和id属性 ; 一般class用于设置样式,而id一般用于js选择
        1:id 选择器         极特殊的情况使用
        2 标签              极少,因为重复的标签很多
        3 class选择器        最常用ie6,7,8不支持! 而且ie8不支持console.log

###       api:   dom.parentNode  通过dom获取他的父类节点
          background-color 这种形式是不能做为变量或者key的
		注意: 在js中操作css中的属性,一般会把abc-xx转换为abcXx 驼峰命名法
		点击绿色盒子 使外层盒子变红
		事件的三要素 1.谁  2.什么事件  3.怎么处理



###       this指向谁?
         1  new 指向实例对象
         2  没有new,指向调用者

         兄弟节点 nextSibling 获取的是节点,可以包含空格和换行符等
	     嫡出 在ie8 可用,但是chrome是下一个空格/换行节点
		var box2 = box.nextSibling;
	     庶出  在chrome可用,在ie8是undefined
		var box2 = box.nextElementSibling;
	    兼容写法  顺序不能写错
	    var box2 = box.nextElementSibling || box.nextSibling;

        孩子节点
<ul class="lis" id="ul1">
		<li>li_1</li>
		<li>li_2</li>
		<li>li_3</li>
		<li>li_4</li>
		<li>li_5</li>
</ul>
	<script>
		var ul = document.getElementById('ul1');
		//第一个孩子节点  firstChild 嫡出
		// var li_1 = ul.firstChild;
		// firstElementChild 庶出
		// var li_1 = ul.firstElementChild;
		//兼容: 
		var li_1 = ul.firstElementChild||ul.firstChild;
		// alert(li_1);
		li_1.style.color = 'red';


	</script>


###	      获得所有孩子节点一般通过其父类
          获取所有的孩子节点
		// 嫡出
		// var lis = ul1.childNodes;  // 伪数组
		// 庶出  这里一般使用children即可,在ie8中存在兼容问题,包含注释节点.
		// var lis = ul1.children;
		// 兼容后的代码
          
####      封装方法,找到所有的文本节点 
function myChildren(pNode){
			// 通过父类元素 获取所有孩子节点,可能包括注释节点(ie8);
			var eles = pNode.children;
			var rs = [];
			for(var i = 0 ;i < eles.length ; i ++){
				// nodeType==1 标签节点
				if(eles[i].nodeType == 1){
					//找到正确的节点 插入数组
					rs.push(eles[i]);
				}
			}
			return rs;
}

###       nodeType是标签元素的属性 可以判断节点类型
            nodeType==1    指的是标签节点

###         获取：getAttribute(名称)
	        设置：setAttribute(名称, 值)
	        删除：removeAttribute(名称) 
	        // 动态给h2 标签添加class属性,且值为 danger
			h2.setAttribute("class", "danger");
			innerHTML插入可执行的标签，标签和样式会被解析，常用于动态生成页面元素


###        切换图片
<body>
	<img class="img" src="img/fbb.jpg" alt="">
	<script>
		var imgs = ['a.jpg','fbb.jpg','hulk.jpg','sjl.jpg','钢铁侠.jpg'];
		//需求:点击图片 动态改变图片 随机
		var imgEl = document.getElementsByClassName('img')[0];
		imgEl.onclick = function(){
			//随机取img  范围0~imgs.length-1;  // Math.floor(Math.random()*个数+最小值)
			var randomIndex = Math.floor(Math.random()*imgs.length);
			this.src = 'img/'+imgs[randomIndex];
		}


	</script>
</body>


####     循环绑定事件
         for(var i = 0 ; i < lis.length ;i++){
			//循环绑定事件
			lis[i].onclick = function(){
				//此处方便演示 不在处理ie8兼容
				//特别注意!!! 这里一定只能用this  lis[i]会报错,问题很深,暂时保留
				var child = this.children[0];
				//对象获取属性的形式 也可以!!!
				// var imgUrl = child.src;
				// 通过标签获取属性的方式  也可以!!!
				var imgUrl = child.getAttribute('src');
				console.log(imgUrl);
				target.src = imgUrl;
			}
		}

####    排他思想   先清除其他的同类元素样式,再给自己设置上特殊样式
        for(var j = 0 ;j < lis.length ; j ++){
					delClass(lis[j],'active');
				}
				addClass(this,'active');

###   正常情况下使用标准文档流布局
		在标准文档流处理不了的情况下使用浮动
		在浮动也处理不了的时候使用定位;小元素一般使用定位;(右边的元素一般使用定位)

		当定位的left和right同时生效的时候,left的优先级更高.
		.swiper .arr.arr-right{
			/*left回复默认*/
			left: auto;
			right: 0;
		}


		// 内部count是传递进来的值,在直接点dott的时候 需要动态修改外部计数器
			// 此时因为内部count和外部计数器count同名,根据函数内部的js变就近取值的原则,
			// 所以需要通过指定window对象的count才能取到外部count
			window.count = count;