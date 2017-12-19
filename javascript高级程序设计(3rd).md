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