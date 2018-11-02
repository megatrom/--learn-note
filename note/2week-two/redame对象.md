###         对象是封装了一些属性和方法的集合
		  js的内置对象
		     1. Date
		     2. Math
		   自定义对象
			1. 可以通过Object对象new
			2. 这里的Object是内置对象,所有对象的顶级对象
			   此时 Object() 就是构造函数对象
		       obj/obj1 是通过对象Object创建出来的两个实例对象



###		   在js中 所有的对象都是函数 所有的函数也可以称为"对象"
		   此时 这个Human为手动创建的自定义构造函数对象
		   在js中 this的指向在调用前是不确定的.

###        script 有一个整体的运行对象  window对象 
              而window对象作为网页js的默认运行环境,一般不写.
		      this在调用之前 是不知道指向谁的
		      面试: 1. 构造函数对象的this指向new出来的实例对象
		            2. 如果不通过new实例对象,那么this指向调用者!

###        通过字面量形式创建对象
           键值对   key:value        key=value

###        对象和json类型的对象都可以通过 JSON.stringify() 
           转换为字符串,
		   但是如果希望字符串转换json对象 必须用""

 
###        	// 数组
		// 1.  concat  连接
		// 2.  push  unshift   pop  shift
		// 3. join 
		var arr = [3,5,7];
		var arr2 = [10,11,1,3,5,7,9];
		console.log(arr);
		// 1.toString()  转换为字符串
		console.log(arr.toString());
		 // 2. reverse()  翻转数组
		 console.log(arr.reverse());
		arr2.sort();
		console.log(arr2);



####    indexOf 获取某个字符在字符串中的位置
        substr从想要的位置截取,比较灵活
        
