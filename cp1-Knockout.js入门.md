# Knockout.js入门
> Knockout.js是一个开源的JavaScript库，它被构建为允许你创建动态和丰富的Web应用程序。它是基于 Model-View-ViewModel (MVVM) 模式进行构建的。 Knockout使得你实现一个响应用户交互的复杂用户界面变得非常简单。


我喜欢Knockout，因为它是当今最轻量级的JavaScript库之一。它也不是试图要成为一个无所不包的框架。它提供单一目的：在ViewModle与及用户界面进行数据绑定。


实现Knockout涉及三个不同的东西：一个包含着将要进行数据绑定的HTML和CSS元素的视图、一个包含绑定到视图中数据的ViewModel，与及告诉Knockout使用ViewModel对视图执行数据绑定。


本章中的示例演示了如何使用基本的ViewModel创建一个HTML页面。在我们回顾了基本的数据绑定语法之后，我们将探讨与视图一起使用的ViewModel的各种类型。


##数据绑定语法
数据绑定是通过将​添加一个名为data-bind的HTML属性到任何HTML元素来完成的，好让Knockout用ViewModel来替换这些信息。
某些时候HTML标记不起作用，因此Knockout允许你为以HTML注释的方式进行数据绑定，正如示例1-1所示的那样。

Example 1-1. 使用HTML注释进行Knockout绑定
``` html
<!-- ko --> 
<!-- /ko -->
```

当你想要包装一段HTML代码的绑定，通过HTML注释绑定是非常方便的，或者你不想创建一个额外的HTML对象的唯一目的只是为了容纳数据绑定。

##数据绑定示例
Knockout最常用的功能之一是使用ViewModel来动态显示文本或者HTML。
示例1-2展示了创建一个使用ViewModel来显示中name属性的标题。

```
<!DOCTYPE html>
<html lang="en">
<head>
	<meta charset="UTF-8">
	<title>Data Binding With Knockout.js</title>
</head>
<body>
	<h1>Hello <span data-bind="text: name"></span></h1>

	<!-- Scripts -->
	<script src="js/knockout-3.2.0.js"></script>
	<script>
	var viewModel = function(){
		this.name = 'Steve Kennedy'
	};

	ko.applyBindings(viewModel);
	</script>
</body>
</html>
```