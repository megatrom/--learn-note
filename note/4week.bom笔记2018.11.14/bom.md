####    包含边框+padding,指的是元素的实际大小
		 1.offsetWith
		2.offsetHeight
		3.offsetLeft/offsetTop和定位的absolute属性的表现形式一样,如果父类(父类的父类..)有定位元素,则找父类,如果都没有,找body
		4. offset获取的结果是number类型
		5. style获取的结果是字符串类型

		// 通过dom节点属性的形式获取width
		console.log(d1El.style.width);

		注意:obj.style.xx只能获取行内样式!!!

#####   匀速动画
   <script>
		var btn1 = document.getElementsByClassName('btn1')[0];
		var btn2 = document.getElementsByClassName('btn2')[0];
		var d1El = document.getElementsByClassName('d1')[0];
		var target = 405;
		var target2 = 800;
		//连续动作形成动画 24帧
		// 1s钟连续播放24张图片,那么图片会形成动画
		// 游戏: 60fps 
		//步长为30px
		// var step = 10;
		btn1.onclick = function() {
		 var timer = setInterval(function(){
		 		var step = target>d1El.offsetLeft?10:-10;
				//循环给d1的left添加步长
				d1El.style.left = (d1El.offsetLeft+step)+'px';
				//获取剩余距离
				var cha = target-d1El.offsetLeft; // -400
				//停止循环
				//如果cha值小于步长,直接定位到结果,并且停止定时器
				if(Math.abs(cha)<Math.abs(step)){
					d1El.style.left = target+'px';
					//清除定时器
					clearInterval(timer);
				}
			}, 17);
		}
		btn2.onclick = function() {
		 var timer = setInterval(function(){
		 		var step = target2>d1El.offsetLeft?10:-10;
				//循环给d1的left添加步长
				d1El.style.left = (d1El.offsetLeft+step)+'px';
				//获取剩余距离
				var cha = target2-d1El.offsetLeft;
				//停止循环
				//如果cha值小于步长,直接定位到结果,并且停止定时器
				if(Math.abs(cha)<Math.abs(step)){
					d1El.style.left = target2+'px';
					//清除定时器
					clearInterval(timer);
				}
			}, 17);
		}
	</script>

#####    // 轮播
   <script>
		var targetEl = document.getElementsByClassName('imgs')[0];
		var btn1 = document.getElementsByClassName('btn1')[0];
		//一个图片的宽度
		var liW = targetEl.children[0].offsetWidth;
		var lis = targetEl.children;
		// //目标位置 
		// var target = -1*liW*(targetEl.children.length-1);
		var timer = null;
		var count = 0;
		btn1.onclick = function () {
			setInterval(function(){
				count ++;
				if(count == lis.length){
					count = 0;
					targetEl.style.left = 0;
				}else{
					var target = -1* count * liW;
					animate(targetEl,target);
				
				}
				console.log(count+'次开始...'+new Date().getSeconds());
			},3000);
		}

		// el 谁动画
		// target 往哪动
		function animate(el,target) {
			// 开始前 应该清楚之前的定时器
			clearInterval(timer);
			timer = setInterval(function(){
				var step = target>el.offsetLeft?5:-5;
				//增加步长
				el.style.left = (el.offsetLeft+step)+'px';
				//计算距离目标的差值
				var cha = target-el.offsetLeft;
				//判断停止条件
				if(Math.abs(cha)<Math.abs(step)){
					//剩下的差值还不够一个步长 直接结束
					el.style.left = target+'px';
					//停止定时器
					clearInterval(timer);
					console.log('移动到'+target+'结束...');
				}

			},17)	
		}
	</script>
 

 #####          el.offsetParent永远为真   offsetLeft只能取到整数
 ####             缓动公式
 <script>
		var timer = null;
		
		var boxEl = document.getElementsByClassName('box')[0];
		var btn1 = document.getElementsByClassName('btn1')[0];
		var btn2 = document.getElementsByClassName('btn2')[0];
		var target = 400;
		var target2 = 800;
		btn1.onclick = function  () {
			clearInterval(timer);
			// leader=leader+(target-leader)/10;
			timer = setInterval(function(){
				// offsetLeft只能取到整数 
				var leader = boxEl.offsetLeft;
				// console.log('offset==>'+leader);
				// 步长 分正副
				var step = (target - leader )/10;
				//最后10像素 修正step永远=1;
				
				if(step<1&&step>0){
					step = 1;
				}else if(step>-1&&step<0){
					step = -1;
				}

				//修改元素位置
				boxEl.style.left = (leader + step) + 'px';
				// console.log('left==>'+(leader+step));
				//终止条件
				if(target==leader){
					//恢复位置
					boxEl.style.left = target+'px';
					clearInterval(timer);
					console.log('结束了...');
				}

			},17);
		}

		btn2.onclick = function  () {
			clearInterval(timer);
			// leader=leader+(target-leader)/10;
			timer = setInterval(function(){
				// offsetLeft只能取到整数 
				var leader = boxEl.offsetLeft;
				// console.log('offset==>'+leader);
				// 步长  
				var step = (target2 - leader )/10;
				//最后10像素 修正step永远=1;
				if(step<1){
					step = 1;
				}
				//修改元素位置
				boxEl.style.left = (leader + step) + 'px';
				// console.log('left==>'+(leader+step));
				//终止条件
				if(target2==leader){
					//恢复位置
					boxEl.style.left = target2+'px';
					clearInterval(timer);
					console.log('结束了...');
				}

			},17);
		}
</script>