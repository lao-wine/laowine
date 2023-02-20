---
title: DIV CSS基础
---
[toc]
## 1、DIV和CSS样式
&nbsp;&nbsp;&nbsp;&nbsp;层叠样式表是一种用来表现HTML或XML等文件样式的计算机语言。CSS不仅可以静态地修饰网页，还可以配合各种的脚本语言的动态地对网页各元素进行格式化。CSS能在像素级精确的对网页中元素位置和模型样式进行控制。支持几乎所有的字体字号样式，拥有对网页对象和模型样式编辑的能力。
`DIV是html的一个标签css是一个样式表`
## 2、样式表类型
### 2.1、嵌入样式表
```
<!DOCTYPE html>
<html>
	<head>
		<meta charset="UTF-8">
		<title></title>
		<style>
			.demol{
				color:red;
				width:100px;
				height:100px;
				background:blue;
			}
		</style>
	</head>
	<body>
		<div class="demo1">
			demo1
		</div>
	</body>
</html>
```
### 2.2、外部样式
```
<link rel="stylesheet" href="css/style.css"/>

@import url  //外部连接外部
@import url("g.css");
.demo1{
				color: red;
				width: 100px;
				height: 100px;
				background: blue;
			}

```
### 2.3、内联样式
```
<div style="color: blue;width: 100px;height: 100px; background: black;">demo2</div>
```
### 2.4、
- 元素选择器   div{属性:值}

- ID选择器  #id{属性:值}

- class选择器  .类名{属性:值}

- 子选择器    元数 空格 元素{属性:值}
  > 

- 后代选择器  元数 > 元数{属性:值}

- 属性选择器  元素[属性]{}

- 通配符选择器  *{属性:值}

- 群组选择器 
