# 第3章 理解数据绑定中的上下文



## with绑定
with绑定于foreach绑定很相似，它们都会创建一个全新的子上下文(child context)。任何在这个绑定内的代码现在都会相对于那个要绑定的变量(原文: Everything within the binding is now relative to the variable to which it is bound)。主要的区别在于with是伴随着一个带有多个属性的单个对象, 而foreach会在绑定期间重复 HTML 。

Example 3-4将书籍清单扩展为单个书籍详情页并且利用with绑定来阻止变量book的重复性前缀。


Example 3-4. 使用with绑定的书籍详情

``` html
<!DOCTYPE html>
<html>
<head> 
 <title>Data Binding with KnockoutJS</title>
</head>
<body> 
 <div id="book" data-bind="with: book"> 
 <h1 data-bind="text: title"></h1> 
 <h2>Published on <span data-bind="text: $parent.formatDate(publishedDate)">
 </span></h2> 
 <p data-bind="text: synposis"></p> 
 </div> 

 <script type='text/javascript' src='js/knockout-3.2.0.js'></script> 
 <script> 
 function ViewModel(book) { 
 var self = this; 

 self.book = book; 

 self.formatDate = function(dateToFormat) { 
 var months = new Array("January", "February", "March", "April", 
 "May", "June", "July", "August", "September", "October", 
 "November", "December");

 var d = new Date(dateToFormat); 
 return months[d.getMonth()] + ' ' + d.getDate() + ', ' + 
 d.getFullYear(); 
 }; 
 }; 

 var book = { 
 title: 'Rapid Application Development With CakePHP', 
 synposis: '...', 
 isbn: '1460954394', 
 publishedDate: '2011-02-17' 
 }; 

 var viewModel = new ViewModel(book); 

 ko.applyBindings(viewModel); 
 </script>
</body>
</html>
```


在这个示例中，一个book对象包含着一些其它的属性，而不再是书籍清单，这个book对象传递给
ViewModel构造函数并且应用与with绑定。
不同于foreach绑定那样，HTML是不会重复的，这里只是显示单独一本书。

相比之下，如示例3-5所示，如果你不使用with数据绑定，则可以使用以下HTML完成相同的结果。

Example 3-5. 不使用with绑定的书籍详情页

``` html
 <div id="book"> 
 <h1 data-bind="text: book.title"></h1> 
 <h2>Published on <span data-bind="text: formatDate(book.publishedDate)">
 </span></h2> 
 <p data-bind="text: book.synposis"></p> 
 </div>
 ```

当你不使用with绑定的时候，你注意到HMTL元素中的数据绑定使用的长变量路径，比如 `book.title`这样，另外一个不同支持在于格式日期函数不再需要使用`$parent`前缀， 因为这里并没有创建一个child context,它仍然是在root context里。

在这样的情况下，使用with绑定是一个简单方便的解决方案，它可以避免在自属性变量重复这些前缀。