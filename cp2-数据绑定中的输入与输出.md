# 第2章 数据绑定中的输入与输出

在Example 1-1中, text被数据绑定到span标记。就像text一样，数据绑定到包含HTML数据的内容，这是非常普遍的。
在Example 2-1中, getName函数通过扩展以包装为一个进行数据绑定到一些HTML代码的name的输出。

## Tips: HTML绑定 VS 文本绑定
HTML绑定的工作原理类似于text绑定，它的例外之处在于它们会渲染任何HTML标记。如果你在HTML内容中适用text binding，HTML内容将会被转义，HTML内容会以文本的形式进行展示。

在Example 2-1中，我对代码更新了两样东西。首先，data-bind属性从span标记转移到h1标记，其次，它绑定到getName函数，它已经被更新为包含一些HTML代码的代码。 

Example 2-1. 带有HTML绑定的h1标记

``` html
<h1 data-bind="text: getName()"></h1>

<!-- Scripts -->
<script src="js/knockout-3.2.0.js"></script>
<script>
var ViewModel = function(){
	var self = this;
	
	self.name = 'Steve Kennedy';

	self.getName = function(){
		return 'Hello <em>' + self.name + '</em>!';
	};
};

var viewModel = new ViewModel();
ko.applyBindings(viewModel);
```