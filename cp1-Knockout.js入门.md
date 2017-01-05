# 第1章 Knockout.js入门
> Knockout.js是一个开源的JavaScript库，它被构建为允许你创建动态的富Web应用程序。它是基于 Model-View-ViewModel (MVVM) 模式进行构建的。 Knockout使得你实现一个响应用户交互的复杂用户界面变得非常简单。


我喜欢Knockout，因为它是当今最轻量级的JavaScript库之一。它也不是试图要成为一个无所不包的框架。它提供单一目的：在ViewModel与及用户界面之间进行数据绑定。


实现Knockout涉及三个不同的东西：一个包含着将要进行数据绑定的HTML和CSS元素的视图、一个包含绑定到视图中数据的ViewModel，与及告诉Knockout使用ViewModel对视图执行数据绑定。


本章中的示例演示了如何使用基本的ViewModel创建一个HTML页面。在我们回顾了基本的数据绑定语法之后，我们将探讨与视图一起使用的ViewModel的各种类型。


##数据绑定语法
数据绑定是通过将​添加一个名为data-bind的HTML属性到任何HTML元素来完成的，好让Knockout用ViewModel来替换这些信息。
某些时候这对HTML标记是不起作用的，因此Knockout允许你为以HTML注释的方式进行数据绑定，正如示例1-1所示的那样。

Example 1-1. 使用HTML注释进行Knockout绑定
``` html
<!-- ko --> 
<!-- /ko -->
```

当你想要包装一段HTML代码的绑定，通过HTML注释绑定是非常方便的，或者你不想创建一个额外的HTML对象的唯一目的只是为了容纳数据绑定。

##数据绑定示例
Knockout最常用的功能之一是使用ViewModel来动态显示文本或者HTML。
示例1-2展示了创建一个显示ViewModel中name属性的标题。

``` html
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

当在浏览器中执行这个示例，它将会在h1标记里面输出`Hello Steve Kennedy`。
span标记通过数据绑定到tagViewModel中的name属性。这是通过在data-bind HTML属性中放置`text：name`来实现的。

正如本章的介绍中提到的，实现一个Knockout应用需要三个不同的东西。 第一个是视图，在此示例中是包含h1与及标识数据绑定的span标记的HTML。 

第二个是 ViewModel, 在此示例中是一个称之为viewModel 的包含着单个变量name的JavaScript 变量/函数。
第三个是告诉Knockout在视图与及ViewModel之间执行数据绑定。这是通过调用一个带有View参数的ko.applyBindings方法来完成。

Knockout会处理视图和ViewModel。 视图中的所有数据绑定都将被ViewModel中的数据执行并动态替换。

执行此函数时，Knockout会处理视图和ViewModel。 所有绑定到视图中的数据将会被执行并动态替换来自ViewModel中的数据。

Knockout不会限制每个视图只有单个ViewModel。 大型项目或者类通常是因为重用性的原因设计精良，这也是将多个ViewModel绑定到单个视图的常见原因。 这将在第6章中进行更详细地讨论。


## 什么是MVVM
MVVM模式大部分基于MVC模式，两者共享MV部分。 ViewModel是区分两者的关键。
MVVM被设计为在 ViewModel与及View中实现数据绑定。这正是 KnockoutJS 为我们所作的，并且它做得很好。正如示例1-2，它是通过使用一些简单实现的(simple-to-implement)属性与及一个JavaScript ViewModel来实现的。


要重点记住的是，你应当以一种更为容易展现视图是如何使用数据的方式来构建ViewModel。
我们在下面的例子中探讨几种常见的情况。



## 创建一个ViewModel
一个ViewModel可以是任何类型的JavaScript变量。在示例1-3中，我们以一个简单的JavaScript结构,开始，这个结构函数着单个name属性。

Example 1-3. 基本的ViewModel
``` js
var myFirstViewModel = {
 name: 'Steve Kennedy'
};
```

上面的示例是一个完美的ViewModel场景，但通常情况下，一个数据模型并不像上面那样100%与之相关。通常，要给数据模型会将其分离为first name与last name两个单独的字段，以使得更为容易地编辑数据，然而，在一个视图中，将它们连接起来并以一个独立的字段来显示是更为有意义的。

上面的ViewModel是相关基础的。ViewModels并不限制为这么一个简单的结构，正如下面的示例所示范的那样。

## 面向对象的ViewModel
通常，当我创建ViewModelde的时候, 我通常会创建一个简单的或者复杂的JavaScript类来允许我利用一种面向对象编程风格(函数、属性、抽象等)。


### Tips: JavaScript的面向对象编程
JavaScript是一门完整的基于原型的面向对象编程语言， 它不想C++, C#或者PHP那样有class语句，然而，JavaScript 函数可以通过模拟来达到相同的行为。
它也提供了完整的OOP语言功能支持，比如命名空间、对象、属性、继承、抽象等等。
如果你是JavaScript新手或者面向对象编程新手，Mozilla Developer Network (MDN)提供了一些[很好的文章](http://mzl.la/1u0uge8).

在示例1-4中, 我创建一个基于一些面向对象特性的ViewModel，并以此为我们的视图提供更多的功能。

Example 1-4. 面向对象的ViewModel
```

var SecondViewModel = function() {
 var self = this;
 
 self.name = 'Steve Kennedy';
 
 self.getName = function() {
 return self.name;
 };
};

var mySecondViewModel = new SecondViewModel();
```

示例中，ViewModel是一个JavaScript函数，用于扮演OOP中的类。它包含一个与上一个示例中相同的name变量，但是这一次它被封装在我们的类中并扮演着一个类属性这样的角色
我也添加一个新称之为getName函数以允许我访问name属性，而无需通过在代码中的其它地方直接访问类属性。


### Tips: Self = This?
你可能会想知道为什么我的类中第一行是`var self = this;`。 通过创建一个名为self的变量，并为其分配变量this，它为我在类中提供了一个属性，这样我可以在类方法内部使用它，并且可以更为地容易得引用其它方法或者属性。

即使示例1-4和示例1-3之间的结果代码看起来完全不同，实际上，它们非常相似。 name属性可以通过任一示例完全相同的方式访问，如示例1-5所示。

尽管这导致代码1-4 与代码1-3 看起来不一样，事实上，它们是非常相同的。name属性可以在任意示例中以相同的方式进行访问，如图示例1-5所示。

Example 1-5. 访问name属性

``` javascript
alert(myFirstViewModel.name);
 
alert(mySecondViewModel.name); // 访问name属性access the property name
alert(mySecondViewModel.getName()); // 访问getName函数
```

上面所有的语句将会alert name。

##　带有参数的ViewModel
在示例示例 1-3 and 1-4, name属性的值被硬编码的，在大多数场景中，像这样的数据是通过不同的数据源进行填充的: 数据库、Ajax调用的结果等等。

在示例1-6, name将会通过ViewModel的一个输入进行填充的。

Example 1-6. 带有参数的ViewModel
``` javascript
function ViewModel(name) { 
 var self = this; 
 
 self.name = name; 
 
 self.getName = function() { 
 return self.name; 
 }; 
}; 

var myThirdViewModel = new ViewModel('Steve Kennedy');
```
在示例 1-3 和 1-4中,　 ViewModel类被直接赋值给变量。这个示例有所不同的是，ViewModel就像一个类一样，用于创建一个接受name属性的函数。然后通过为构造函数传入name属性来对它进行实例化。


在将来的示例中，我将会急需使用 JavaScript类，因为它提供了大量的灵活性，然而，如果一个简单的JavaScript变量或结构就满足你的视图，那就不觉得需要以类的形式来包装你的ViewModel。
