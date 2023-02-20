---
title: HTML基础
---
[toc]
# 一、基础
## 1、简单的HTML页面架构
```
<!DOCTYPE html>
<html>
			<head>
							<meta charset="utf-8">
							<title></title>
			</head>
			<body>
			</body>
</html>
```
## 2、HTML常见标签
### meta
```
meta标签
		<meta>元素可提供有关页面的元信息(meta-information),比如针对搜索引擎和更新频度的描述和关键词。
有利于网站seo
		meta name="keywords" conten="频度词,描述词" />
```
### link
```
link标签
		<link>标签定义文档与外部资源的关系。
提示和注释
		1、link元素是空元素，它仅包含属性
		2、此元素只能存在于head部分，不过它可出现任何次数。
		3、支持HTML中的全局属性(全局属性是可与所有HTML元素一起使用的属性)。
		4、支持HTNL中的事件属性(有能力让事件触发浏览器中的动作，例如当用户单元素时启动JavaScript)。
```
### script
```
<script>标签
		1、标签用于定义客户端脚本，比如Javascript。
		2、scrptt元素既可以包含脚本语句，也可以通过src属性指向外部脚本文件。
		3、必须的type属性规定脚本的MIME类型。
<script type="text/javascript">  
document.write("Hello World!")
</script>
```
### 注释
```
HTML注释
		<!-- 这是一段注释。主是不会在浏览器中显示。-->
		1、注释标签用于在源代码中插入注释。注释不会再浏览器中显示。
		2、注释对代码解释，有助于理解与后期的维护。
		3、使用注释来隐藏浏览器不支持的脚本。
		示例：
				<script type="text/javascript">
				<!--
				function displayMsg()
				{
				alert("Hello World!")
				}
				//-->
				</script>
				注释：注释结尾处的两条斜杠(//)是javascript注释符号。在浏览器可以执行脚本的时候让html的注释失效，在浏览器不支持脚本运行的时候可以注释掉脚本的内容，不至于让让本的内容显示为纯文本。  
```
### P
```
P标签
		1、标签定义的是普通的段落。
		2、p元素自动在其前后创建一些空白。浏览器会自动添加这些空间，也可以在样式表中规定。
		3、此标签支持HTML中的全局属性和事件属性。
		<p>This is some text in a very short paragraph</p>
```
### 标题标签
```
由大到小：
				<h1>这是标题 1</h1>
				<h2>这是标题 2</h2>
				<h3>这是标题 3</h3>
				<h4>这是标题 4</h4>
				<h5>这是标题 5</h5>
				<h6>这是标题 6</h6>
定义与用法：
					1、<h1>定义最大的标签，<h6>定义最小的标签。
					2、由于h元素拥有确切的语句，因此不要利用标题标签来改变同一行中的字体大小。
```
### br
```
br标签
			1、换行。
			2、<br>标签只是简单地开始新的一行。
			3、<br>标签是空标签(意味着他没有结束标签，因此这是错误的：<br></br>)。在XHTML中，把结束标签放在开始标签中也就是<br />。
			4、使用<br>来输入空行，而不是分隔符。
```
### hr
```
br标签
			1、<hr>标签在html页面中创建一条水平线。
			<h1>This is header 1</h1>
			<hr />
			<p>This is some text</p>
```
### 文本属性
```
		<strong>加粗</strong>
		<b>加粗</b>
		<i>斜体</i>
		<u>下划线</u>
		<sup>上标</sup>
		<sub>下标</sub>
		<del>删除线</del>
		<font>规定字体,字体大小，字体颜色。</font>
							<font size="3" color="red">This is some text!</font>
```
### pre
```
pre标签
			1、被包围的pre元素中的文本通常会保留空格和换行符，文本会呈现为等宽字体。
			2、一般常见应用来表示计算机的源代码。
			<pre>
			这是
			预格式文本。
			它保留了      
			和换行。
			</pre>
```
## 3、form表单和input标签
### form表单
```
from表单：规定当提交表单时向何处发送表单数据。
				1、method(规定用于发送form-date的HTTP方法)，提交的方式有两种，get和post。
						·get：是会在浏览器上显示出来。
						·post：是不会在浏览器上显示出来。
				2、action，提交的的地方。
						·为空的时候就是本页面。
				3、enctype发送之前是需要编码的。
						·application/x-www-form-urlencode 普通编码
						·multipart/form-data 上传文件时候的编码
						· text/plain 以纯文本的编码
				
```
### input
```
type属性：
				1、type="text"：创建单行文本输入框
				2、type="password"：密码输入框
				3、type="radio"：单选按钮
				4、type="checkbox"：复选框
				5、type="button"：普通按钮
				6、type="submit"：提交按钮
				7、type="reset"：重置按钮
				8、type="image"：图像按钮
				9、type="file"：文件域
				10、input type="url"：输入URL字段
				11、input type="tel" name="tel"：用来输入电话号码
				12、input type="search" name="search"：搜索字符串
				13、type="email"：该控件用来输入"email"地址
				14、input type="color" id="color"：颜色选择器
name属性 
				元素的名称；这个不需要多解释了，也就是name的取值代表为当前input元素起个名字。
size属性 
				元素的宽度；很多人都知道在HTML中，常见的宽度是用 width 表示的，而在input中 width 属性只使用与 type="image" 时使用，input元素的宽度需要通过size属性来设定，size的值为数字，数字越大input元素越长，数字越小input元素越短；
value属性
				定义input元素的默认值；
				当 input type="text"、"password"、"hidden" 时，定义输入字段的初始值；
				当 input type="button", "reset", "submit" 时，定义按钮上的显示的文本；
				当 input type="checkbox", "radio", "image" 时，定义与输入相关联的值；
				注意：input type="checkbox" 和 input type="radio" 中必须设置 value 属性；value属性无法与 input type="file" 一同使用。
maxlength属性
				定义input元素中可输入的最长字符数；如 maxlength="50" 表示最多可以输入50个字符；	
style属性 
				为input元素设定CSS样式；
width属性
				当 input type="image"时，通过width属性控制元素的宽度；
height属性
				当 input type="image"时，通过width属性控制元素的高度；
```
`示例代码`
```
<!DOCTYPE html>
<html>
	<head>
		<meta charset="UTF-8">
		<title>示范代码</title>
	</head>
	<body>
		<form method="post" action="" enctype="application/x-www-form-urlencoded">
			帐号:<input type="text" name="username" size="30" maxlength="10" value="admin"/><br/>
			密码:<input type="password" name="password" size="30" /><br />
				<input type="hidden" name="token" value="asdahiodhaohdiohaiodhoaihd"/>
			<input type="submit" value="提交"/>
			<input type="reset" value="重置"/>
		</form>
		<form method="post" action="" enctype="multipart/form-data">
			<input type="file" name="file"/>
			<input type="submit" value="提交"/>
			
		</form>
			<form method="post" action="" enctype="multipart/form-data">
			<input type="file" name="file"/>
			<input type="button" value="提交"/>
			
		</form>
		
			<form method="get" action="" enctype="multipart/form-data">
			<input type="text" name="search"/>
			<input type="submit" value="搜索"/>
			
			</form>
	</body>
</html>
```
## a标签、img标签、table标签
### a
- a标签定义超链接，用于从一张页面链接到另一张页面。
- a元素最重要的属性是href属性，它指示链接的目标。
```
<a href="指定要跳转的目标界面的链接">需要展示给用户看见的内容</a>
		1、<a href="http://www.baidu.com">百度</a>
		2、<a href="http://www.baidu.com" target="self">百度</a>
			<a href="http://www.baidu.com" target="_blank">百度</a>
				target属性就是专门控制如何跳转的
				self：在当前页面跳转。
				_back：在新的选项卡跳转，也就是新建页面跳转。
		3、<a href="http://www.baidu.com" target="_blank" title="点击会跳转到百度首页喔">百度</a>
				tiele属性是来控制鼠标悬浮时显示的提示内容。
		4、  <a href="#text">跳转</a>
    				如果某个元素含有id/name属性，那么这个元素就是网页的一个锚点
   					 利用a标签的href属性就能跳转到该锚点
    			<a href="#" name="text">跳转</a>

```
### img与area
- img元素是向网页嵌入一幅图像。从技术上来讲，不是插入到网页中来，而是链接到网页中，
```
img格式：<img src="被引用图像的地址" alt="图像的替代文本">
		1、<img src="/i/eg_tulip.jpg"  alt="图像的替代文本" />
				alt 规定图像的替代文本。
				src  规定显示图像的url
				width 规定图片的高度
				height 规定图片的宽度
```
- area标签定义图像映射中的区域。
- area标签总是嵌套在map标签中。
- img标签中的usemap属性与map元素name属性相关联，创建图像与映射之间的联系。
```
1、矩形 （左上角顶点坐标为（x1,y1）,右下角顶点坐标为（x2,y2））
		<area shape ="rect" coords ="x1,y1,x2,y2" href ="url" alt="提示" />
2、圆形（圆形坐标为（x1,y1）,半径为r）
		 <area shape ="circle" coords ="x1,y1,r" href ="url" alt="提示" />
```
- 本章综合示例
```
<html>
<body>

<p>请点击图像上的星球，把它们放大。</p>

<img
src="/i/eg_planets.jpg"
border="0" usemap="#planetmap"
alt="Planets" />

<map name="planetmap" id="planetmap">

<area
shape="circle"
coords="180,139,14"
href ="/example/html/venus.html"
target ="_blank"
alt="Venus" />

<area
shape="circle"
coords="129,161,10"
href ="/example/html/mercur.html"
target ="_blank"
alt="Mercury" />

<area
shape="rect"
coords="0,0,110,260"
href ="/example/html/sun.html"
target ="_blank"
alt="Sun" />

</map>

<p><b>注释：</b>img 元素中的 "usemap" 属性引用 map 元素中的 "id" 或 "name" 属性（根据浏览器），所以我们同时向 map 元素添加了 "id" 和 "name" 属性。</p>

</body>
</html>
```
### table
- table标签定义htnl表格。
- 简单的htnl表格是由table元素以及一个或者多个tr、th或者td元素组成。
- tr元素定义表格行、th元素定义表头、td元素定义表格单元。
- width宽度、 height高度
```
<!DOCTYPE html>
<html>
	<head>
		<meta charset="UTF-8">
		<title></title>
	</head>
	<body>
		<table border="1" cellpadding="10" cellspacing="2">
<!-- 
							border 边框
							cellpadding 单元边与内容的空白
							cellspacing 单元格的空白	
-->
			<tr><th>#</th><th>名字</th><th>年龄</th></tr>
			<tr><td>1</td><td>刘备</td><td>18</td></tr>
			<tr><td>2</td><td>张飞</td><td>19</td></tr>
			<tr><td>3</td><td>赵云</td><td>20</td></tr>
			<tr><td>总数</td><td colspan="2">3人</td></tr>
<!--
				colspan 行
-->
		</table>
		<table border="1" cellpadding="10" cellspacing="2">
			<tr><th>#</th><th>名字</th><th>年龄</th></tr>
			<tr><td>1</td><td>刘备</td><td>18</td></tr>
			<tr><td>2</td><td>张飞</td><td>19</td></tr>
			<tr><td>3</td><td>赵云</td><td rowspan="2">20</td></tr>
<!--
				rowspan 竖
-->
			<tr><td>4</td><td>马超</td></tr>
		</table>
	</body>
</html>
```
## 基础单选框、复选框，下拉选框、文本域
- 单选框radio
```
单选框语法：<input name="Fruit" type="radio" value="" />
			使用input标签、name为自定义、type类型为"radio"的表单。
示例：
			<form action="" method="get">
			您最喜欢水果？<br /><br />
			<label><input name="Fruit" type="radio" value="" />苹果 </label>
			<label><input name="Fruit" type="radio" value="" />桃子 </label>
			<label><input name="Fruit" type="radio" value="" />香蕉 </label>
			<label><input name="Fruit" type="radio" value="" />梨 </label>
			<label><input name="Fruit" type="radio" value="" />其它 </label>
			</form>
```
- 复选框checkbox
```
复选框语法：<input name="Fruit" type="checkbox" value="" />
			使用input标签、name为自定义、type类型为"checkbox"的表单。
示例：
			<form action="" method="get">
			您最喜欢水果？<br /><br />
			<label><input name="Fruit" type="checkbox" value="" />苹果 </label>
			<label><input name="Fruit" type="checkbox" value="" />桃子 </label>
			<label><input name="Fruit" type="checkbox" value="" />香蕉 </label>
			<label><input name="Fruit" type="checkbox" value="" />梨 </label>
			<label><input name="Fruit" type="checkbox" value="" />其它 </label>
			</form>
```
### 下拉选框
```
使用方法：
				<select>
								<option value='提交值'>选项</option>
				</select>
				·selected="selected"：给某一个选项加上此属性就是设置此属性为默认选项。
				
示例：
				<select name="address">
					<option value="beijing">北京</option>
					<option value="shanghai">上海</option>
					<option value="guangzhou" selected="selected">广州</option>
				</select>
```
### 文本域 textarea
- textarea标签定义多行的文本输入控件。
```
<textarea rows="10" cols="20">
		此处写文本

</textarea > 
```
### 本章综合示例
- fieldset：对表单进行分组，一个表单可以有多个fieldset。
- legend：说明每组的内容描述。
```
<!DOCTYPE html>
<html>
	<head>
		<meta charset="UTF-8">
		<title></title>
	</head>
	<body>
		<fieldset>
		 <legend>个人信息</legend>
		<form>
			<label>帐号</label><input type="text" name="username"/><br>
			<label>密码</label><input type="password" name="password" /><br>
			性别 <input type="radio" name="sex" value="1">男<input type="radio" name="sex" value="2"><br>
			喜欢的语言<input type="checkbox" name="app[]" value="php"/>php<input type="checkbox" name="app[]" value="aspx"/>aspx<input type="checkbox" name="app[]" value="asp"/>asp<br>
			地址<select name="address">
				<option value="beijing">北京</option>
				<option value="shanghai">上海</option>
				<option value="guangzhou">广州</option>
			</select>
			<br>
			个人简介<br />
			<textarea rows="10" cols="30" name="info"></textarea><br>
			<input type="submit" value="提交"/>
			<input type="reset" value="重置" />
		</form>
		</fieldset>
	</body>
</html>
```
## 列表
### 无序列表
```
	<ul type="disc">
			<li><a href="#">第一课</a></li>
			<li><a href="#">第二课</a></li>
			<li><a href="#">第三课</a></li>
			<li><a href="#">第四课</a></li>
	</ul>
```
- type的类型可以是square circle  disc
### 有序列表
```
<ol type="I">
			<li><a href="#">第一课</a></li>
			<li><a href="#">第二课</a></li>
			<li><a href="#">第三课</a></li>
			<li><a href="#">第四课</a></li>
</ol>
```
- type默认的是数字
- a 小写字母列表 
- A	大写字母列表 
- I	罗马字母列表  
- i	小写罗马字母列表 
## 补充
### frameset
- frameset 不能在body内使用
- frame 一般都是在frameset中使用
- cols 定义框架集中列的数目和尺寸
- rows 定义框架集中行的数目和尺寸
```
<!DOCTYPE html>
<html>
	<head>
		<meta charset="utf-8" />
		<title></title>
	</head>
	
	<frameset rows="20%,*">
			<frame src="top.html" />
			<frameset cols="30%,*">
				<frame src="menu.html" />
				<frame src="main.html" name="c" />
			</frameset>
	</frameset>
	
	<body>
		
	</body>
</html>
```
### 属性scrolling
- scrolling一般在iframe标签中应用。也可以在frameset标签中使用
- iframe 元素会创建包含另外一个文档的内联框架（即行内框架）。
```
<iframe scrolling="auto|yes|no">

<frameset cols="50%,50%">
  <frame src="frame_a.htm" scrolling="yes">
  <frame src="frame_b.htm">
</frameset>
```