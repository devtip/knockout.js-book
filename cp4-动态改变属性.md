
# 第4章 动态改变属性

到目前为止，我们只是谈及到KnockoutJS框架的一小部分。在本章，我们将会利用通过用户交互来动态改变属性的优点。

Knockout称这些属性为observable(可观察的)。当你定义一个变量或者属性为observable, Knockout会跟踪它们的变化。这可以通过不同的方式来进行使用，我们将会在接下来的章节看到这些内容。


## 定义一个Observable
有3种不同类型的而又非常常用的observable。 第一个，如示例4-1所示的那样, 是一个observable变量。

Example 4-1. 创建一个observable变量

``` js
var myObservable = ko.observable();
myObservable('Hello');

alert(myObservable());
```

要创建observable，你需要将ko.observable函数分配给变量。 可以在调用该构造函数的时候指定默认值。 Knockout然后转换你的变量为一个函数，并用于跟踪值的变动发生在什么时候，以便通知与变量相关联的UI元素。


