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

除了name以斜体进行展示，运行Example 2-1将会输出与示例Example 1-2相同的结果，这是因为它周围的HTML标记所引起的。

##绑定HTML属性、CSS类与及CSS Style

Knockout几乎可以绑定任何HTML属性、CSS类或者CSS style。除了一次指定多个属性，这与text绑定、HTML绑定非常相似，一次指定多个属性是通过使用花括号进行包围来完成的，正如示例 2-2与2-3.

[](ex2-2.png)

以下示例将两个自定义样式添加到p标记。 注意style属性margin-bottom和padding-bottom是CamelCase风格的而不是连字符风格。
通过在关闭的大括号之后放置逗号，我为p标签添加了第二个数据绑定。 这一次我设置了一个CSS类的myClass。添加HTML属性也是以类似的方式完成。 在示例2-3中，我们来要添加的id属性 。
 
Example 2-3. Data-binding HTML attributes
``` js
<p data-bind="attr: { id: 'myCustomId' }">
 This p tag has an id data bound to it.</p>
```
像示例2-2一样, 如果我想添加额外的HTML属性，我会在关闭的花括号之前放置一个花括号，然后添加额外的属性。


## 条件式数据绑定
When you are defining a data bind, you might want to specify a condition that when your data contains a specific value, it outputs a different class name. This can be accomplished by placing conditional statements inside your data binding.
In Example 2-4, a button is created. The text data binding contains a conditional statement that when the id is 0, the button text will say “Create.” However, when the
id is greater than 0, it will say “Update,” allowing the use of a single button tag that
dynamically changes.

Example 2-4. Conditional data binding

``` js
<!DOCTYPE html>
<html>
<head> 
 <title>Data Binding with KnockoutJS</title>
</head>
<body> 
 <button type="submit" data-bind="text: (id == 0) ? 'Create' : 'Update'"></button> 

 <script type='text/javascript' src='js/knockout-3.2.0.js'></script> 
 <script> 
 var viewModel = function() { 

 var self = this; 

 self.id = 0; 
 }; 

 ko.applyBindings(viewModel); 
 </script>
</body>
</html>
```

For this example to work, the ViewModel has been updated to include a new property called id. By setting it to 0, when this example is displayed in a web browser, the but‐
ton text will say “Create.” By updating the id to be any other positive number, the text
will change to say “Update.”



## 条件语句
When you are defining a conditional statement in your data bind‐
ing, brackets are not required; however, I find it to be much more
readable. It helps identify where the conditional statement is.

Just like when using data bindings, conditional bindings can be accomplished by
using a function instead of placing the condition inside the data binding, as shown in
Example 2-5.

Example 2-5. Condition data binding with a function
``` js
<!DOCTYPE html>
<html>
<head> 
 <title>Data Binding with KnockoutJS</title>
</head>
<body> 
 <button type="submit" data-bind="text: (isNew()) ? 'Create' : 'Update'">
 </button> 

 <script type='text/javascript' src='js/knockout-3.2.0.js'></script> 
 <script> 
 var viewModel = function() { 

 var self = this; 

 self.id = 1; 

 self.isNew = function() { 
 return id == 0; 
 }; 
 }; 

 ko.applyBindings(viewModel); 
 </script>
</body>
</html>
```

The ViewModel was updated in the example to add a new function called isNew. This contains the same conditional statement that was used in Example 2-4. The data binding was also updated to use the function inside of the condition statement.
The id was updated from 0 to 1, so running this example outputs “Update” for the button text.