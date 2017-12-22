<style type="text/css">
strong {
	 color: #f20b64;
}
</style>
<h1>javascript高级程序设计（第三版）</h1>
<h1>Professional Javascript For Web Developers 3rd Edition</h1>
<h1>在HTML里面的script元素</h1>
<p>
	<strong>内嵌在html里面的script如果给了src属性，那么里面的代码将不会被执行</strong>
<pre>
script src="your.js"
	fn() {
		your code...
	}
/script
//因为script变成标签会被解析所以没有加箭头符号
</pre>
</p>
<h2>应该做什么 - 格式</h2>
<p>
	首先不应该省略分号 ';' 虽说内置引擎可以去识别语句的结尾，但是可以避免一些输入错误，压缩代码错误。
	<strong>优化性能：解析器不用去花时间分析哪里应该插入分号</strong><br>
	if语句写在一行也许看着很酷，可是按正常写会使代码的可读性更高。
</p>
<h2>严格模式</h2>
<p>
	ECMAScript5引入了严格模式， 在顶部添加 'use strict'; 看起来像是字符串，其实是一个编译指示
</p>
<h2>申明全局变量</h2>
<pre>
var a = 'a' //在script内部第一层，未在函数作用域
a = 'a' //严格模式下会导致操作 Uncaught ReferenceError: a is not defined
window.a = 'a'
//三种申明全局变量的方式
a = 1
for( var i in window ) { // 用for in打开window对象可以发现 a 以及 i。如果变成let申明就不能获取到i，也就是一个申明全局变量以及作用域的问题
	console.log(i)
}
//用with来展开window对象
a = 1
with (window) {
	var a = 2 //if without this line, it will console 1,it means a is a property in object:window
	console.log(a)
}
</pre>
<h1>数据类型</h1>
<h2>typeof 操作符</h2>
<p>
	简单数据类型：undefined null Boolean number string <br>
	typeof返回值有：undefined Boolean number string object function <br>
	因为null被认为是空的对象的引用 <br>
	console.log(null == undefined) // true
</p>
<h2>应该做什么 - 格式</h2>
<p>
	.5 // 可行，不推荐 <br>
	0.5 // 推荐
</p>
<h2>NaN</h2>
<p>
	任意数字除以非数字都是NaN <br>
	NaN 并不等于自身 <br>
	isNaN() 判断一个值是否为NaN，是的返回true
</p>
<h2>字符串拼接 - 性能</h2>
<p>
	javascript中的字符串一旦定义就不能被修改 <br>
<pre>
var a = 'java'
a += 'script'
</pre>
上面发生的不是a直接变化，而是先创建一个10长度的字符串，在将javascript填充进去，最后销毁java以及script，不难发现字符串创建第一步是先申明长度，所以字符串不能被直接改变，同理也是为什么低级浏览器做字符串添加操作会速度很慢，不过现代浏览器已经解决了这个低效率问题
</p>
<h2>流程控制语句 - switch</h2>
<pre>
var a = '1'
switch (a) {
	case 1:
	console.log('是1');
	break;

	case '2':
	console.log('是2');
	break;
}
</pre>
<h2>函数</h2>
<p>
	函数的参数会集合在arguments对象（并不是array的实例），它是一个类数组，可以用arguments[0]去访问，也有arguments.length	
</p>
<h2>instanceof运算符</h2>
<p>
	<strong>判断该对象是</strong>
</p>
<h2>数组的方法 - 基础版</h2>
<p>
	push：将项推入数组结尾，并返回新的数组的长度 <br>
	pop：将数组最后一项去掉（弹出），返回弹出的项 <br>
	shift：将数组最开始一项去掉，返回去掉的项 <br>
	unshift：将新的项从开始填入数组，返回新的数组的长度 <br>
	sort：将数组排序，按第一项的编码来排序，返回修改后的新数组 <br>
	reverse：将数组反转，返回修改后的新数组 <br>
	<strong>上面的方法都会改变数组</strong> <br>
</p>
<h2>数组的方法 - 深入版</h2>
<p>
	join：将数组按着给定的分隔符构建字符串
<pre>
var a = ['1','2','11','1'];
var b = a.join('-') //如果没有传入参数或者传入的是undefined，则返回1,2,11,1 以逗号作为分隔符，类似toString()
console.log(b) //1-2-11-1	
</pre>
	concat：创造一个副本，然后将这个副本和传入得参数进行连接，返回新的数组，原数组不变
<pre>
var a = [1, 2, 3];
var b = a.concat(['4', '5']);
console.log(a) // [1, 2, 3]
console.log(b) //[1, 2, 3, '4', '5']
</pre>
	slice：可以传入一个或两个参数，从原数组构建新的数组
<pre>
var a = [1, 2, 3, '4', '5'];
var b = a.slice(1) // [2, 3, '4', '5'] 之传入一个参数，则返回从第几项到最后一项
//如果不传入参数默认为slice(0),即返回所有项
var c = a.slice(1,3) // [2, 3] 从第2项到第4项，不包括第4项
</pre>
	splice：数组最强大的方法，至少两个参数，个人理解：从第一个参数项开始删除几个项 <strong>该方法会修改原数组</strong> <br>
<pre>
var a = [1, 2, 3, '4', '5'];
a.splice(0,1) // [2, 3, '4', '5'] 
//<strong>如果传入的第一个参数大于数字的长度不会做任何动作</strong>
</pre>
	如果传入参数，先删除项，再添加项，第二个参数可为0，即不删除任何项
</p>
<h1>函数</h1>
<pre>
var a = function() {
	//code here..
}
//函数表达式定义函数
function a() {
	//code here..
}
//函数声明定义函数
//两种方法唯一的区别就是一个是“解析器会率先解析函数声明使其可以在执行其他表达式可以调用”
</pre>  
<h2>三种基本包装类型 String Number Boolean</h2>                                          
<p>
<pre>
var a = '11'
//在申明一个字符串，会隐式的调用String构造函数，创建完销毁，再次调用a就不会是一个对象，而是一个字符串
a.color = 'red'
console.log(a.color) // undefined
var b = new String('11')
a.color = 'red'
console.log(a.color) // red
</pre>
	再看一看Boolean构造一个布尔对象
<pre>
var a = new Boolean(false) 
console.log( a && true)
//返回的是true，因为左边的a别判定为一个对象，在布尔运算对象会被转换成true
//所以一般不用Boolean的构造，直接申明 var a = true
</pre>
</p>