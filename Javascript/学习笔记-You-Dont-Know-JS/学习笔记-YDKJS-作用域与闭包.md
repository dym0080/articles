# 你不懂JS：作用域与闭包
# 第一章：什么是作用域？

# 第二章：词法作用域

词法作用域意味着作用域是由编写时函数被声明的位置的决策定义的。编译器的词法分析阶段实质上可以知道所有的标识符是在哪里和如何声明的，并如此在执行期间预测它们将如何被查询。

在 JavaScript 中有两种机制可以“欺骗”词法作用域：`eval(..) `和 `with`。前者可以通过对一个拥有一个或多个声明的“代码”字符串进行求值，来（在运行时）修改现存的词法作用域。后者实质上是通过将一个对象引用看作一个“作用域”，并将这个对象的属性看作作用域中的标识符，（同样，也是在运行时）创建一个全新的词法作用域。

这些机制的缺点是，它压制了 引擎 在作用域查询上进行编译期优化的能力，因为 引擎 不得不悲观地假定这样的优化是无效的。这两种特性的结果就是代码 将 会运行的更慢。**不要使用它们**。

# 第三章：函数与块儿作用域

## 块儿作为作用域

### `with`

我们在第二章中学习了 `with`。虽然它是一个使人皱眉头的结构，但它确实是一个（一种形式的）块儿作用域的例子，它从对象中创建的作用域仅存在于这个 `with` 语句的生命周期中，而不在外围作用域中。

### `try/catch`

一个鲜为人知的事实是，JavaScript 在 ES3 中明确指出在 `try/catch` 的 `catch` 子句中声明的变量，是属于 `catch` 块儿的块儿作用域的。例如：

```js
try {
	undefined(); //用非法的操作强制产生一个异常！
}
catch (err) {
	console.log( err ); // 好用！
}

console.log( err ); // ReferenceError: `err` not found
```
如你所见，`err` 仅存在于 `catch` 子句中，并且在你试着从其他地方引用它时抛出一个错误。

### `let`

然而，使用 `let` 做出的声明将 *不会* 在它们所出现的整个块儿的作用域中提升。如此，直到声明语句为止，声明将不会“存在”于块儿中。

```js
{
   console.log( bar ); // ReferenceError!
   let bar = 2;
}
```
# 第四章：提升

## 编译器再次袭来

函数表达式的变量提升：

```js
foo(); // TypeError
bar(); // ReferenceError

var foo = function bar() {
	// ...
};
```
这个代码段可以（使用提升）更准确地解释为：
```js
var foo;

foo(); // TypeError
bar(); // ReferenceError

foo = function() {
	var bar = ...self...
	// ...
}
```
函数申明式的变量提升：
```js
foo(); // 1

function foo(){
    console.log(1);
}
```
这个代码段可以（使用提升）更准确地解释为：
```js
function foo(){
    console.log(1);
}

foo();
```

## 复习

我们可能被诱导而将 `var a = 2` 看作是一个语句，但是 JavaScript *引擎* 可不这么看。它将 `var a` 和 `a = 2` 看作两个分离的语句，第一个是编译期的任务，而第二个是执行时的任务。

这将导致在一个作用域内的所有声明，不论它们出现在何处，都会在代码本身被执行前 *首先* 被处理。你可以将它可视化为声明（变量与函数）被“移动”到它们各自的作用域顶部，这就是我们所说的“提升”。

声明本身会被提升，但不是赋值，即便是函数表达式的赋值，也 *不会* 被提升。

要小心重复声明，特别是将一般的变量声明和函数声明混在一起 —— 如果你这么做的话，危险就在眼前！

# 第五章：作用域闭包

## 模块

```js
function CoolModule() {
	var something = "cool";
	var another = [1, 2, 3];

	function doSomething() {
		console.log( something );
	}

	function doAnother() {
		console.log( another.join( " ! " ) );
	}

	return {
		doSomething: doSomething,
		doAnother: doAnother
	};
}

var foo = CoolModule();

foo.doSomething(); // cool
foo.doAnother(); // 1 ! 2 ! 3
```
在 JavaScript 中我们称这种模式为 *模块*。实现模块模式的最常见方法经常被称为“揭示模块”，它是我们在这里展示的方式的变种。

让我们检视关于这段代码的一些事情。

首先，`CoolModule()` 只是一个函数，但它 *必须被调用* 才能成为一个被创建的模块实例。没有外部函数的执行，内部作用域的创建和闭包都不会发生。

第二，`CoolModule()` 函数返回一个对象，通过对象字面量语法 `{ key: value, ... }` 标记。这个我们返回的对象拥有指向我们内部函数的引用，但是 *没有* 指向我们内部数据变量的引用。我们可以将它们保持为隐藏和私有的。可以很恰当地认为这个返回值对象实质上是一个 **我们模块的公有API**。

这个返回值对象最终被赋值给外部变量 `foo`，然后我们可以在这个API上访问那些属性，比如 `foo.doSomething()`。

更简单地说，行使模块模式有两个“必要条件”：

1. 必须有一个外部的外围函数，而且它必须至少被调用一次（每次创建一个新的模块实例）。

2. 外围的函数必须至少返回一个内部函数，这样这个内部函数才拥有私有作用域的闭包，并且可以访问和/或修改这个私有状态。

上面的代码段展示了一个称为 CoolModule() 独立的模块创建器，它可以被调用任意多次，每次创建一个新的模块实例。这种模式的一个稍稍的变化是当你只想要一个实例的时候，某种“单例”：

```js
var foo = (function CoolModule() {
	var something = "cool";
	var another = [1, 2, 3];

	function doSomething() {
		console.log( something );
	}

	function doAnother() {
		console.log( another.join( " ! " ) );
	}

	return {
		doSomething: doSomething,
		doAnother: doAnother
	};
})();

foo.doSomething(); // cool
foo.doAnother(); // 1 ! 2 ! 3
```
### 现代的模块

各种模块依赖加载器/消息机制实质上都是将这种模块定义包装进一个友好的API。与其检视任意一个特定的库，不如让我 **（仅）为了说明的目的** 展示一个 *非常简单* 的概念证明：

```js
var MyModules = (function Manager() {
	var modules = {};

	function define(name, deps, impl) {
		for (var i=0; i<deps.length; i++) {
			deps[i] = modules[deps[i]];
		}
		modules[name] = impl.apply( impl, deps );
	}

	function get(name) {
		return modules[name];
	}

	return {
		define: define,
		get: get
	};
})();
```

这段代码的关键部分是 `modules[name] = impl.apply(impl, deps)`。这为一个模块调用了它的定义的包装函数（传入所有依赖），并将返回值，也就是模块的API，存储到一个用名称追踪的内部模块列表中。

这里是我可能如何使用它来定义一个模块：

```js
MyModules.define( "bar", [], function(){
	function hello(who) {
		return "Let me introduce: " + who;
	}

	return {
		hello: hello
	};
} );

MyModules.define( "foo", ["bar"], function(bar){
	var hungry = "hippo";

	function awesome() {
		console.log( bar.hello( hungry ).toUpperCase() );
	}

	return {
		awesome: awesome
	};
} );

var bar = MyModules.get( "bar" );
var foo = MyModules.get( "foo" );

console.log(
	bar.hello( "hippo" )
); // Let me introduce: hippo

foo.awesome(); // LET ME INTRODUCE: HIPPO
```

模块“foo”和“bar”都使用一个返回公有API的函数来定义。“foo”甚至接收一个“bar”的实例作为依赖参数，并且可以因此使用它。

花些时间检视这些代码段，来完全理解将闭包的力量付诸实践给我们带来的好处。关键之处在于，对于模块管理器来说真的没有什么特殊的“魔法”。它们只是满足了我在上面列出的模块模式的两个性质：调用一个函数定义包装器，并将它的返回值作为这个模块的API保存下来。

换句话说，模块就是模块，即便你在它们上面放了一个友好的包装工具。

## 复习

对于那些还蒙在鼓里的人来说，闭包就像在 JavaScript 内部被隔离开的魔法世界，只有很少一些最勇敢的灵魂才能到达。但是它实际上只是一个标准的，而且几乎明显的事实 —— 我们如何在函数即是值，而且可以被随意传递的词法作用域环境中编写代码，

**闭包就是当一个函数即使是在它的词法作用域之外被调用时，也可以记住并访问它的词法作用域。**

如果我们不能小心地识别它们和它们的工作方式，闭包可能会绊住我们，例如在循环中。但它们也是一种极其强大的工具，以各种形式开启了像 *模块* 这样的模式。

模块要求两个关键性质：1）一个被调用的外部包装函数，来创建外围作用域。2）这个包装函数的返回值必须包含至少一个内部函数的引用，这个函数才拥有包装函数内部作用域的闭包。

现在我们看到了闭包在我们的代码中无处不在，而且我们有能力识别它们，并为了我们自己的利益利用它们！


## 注明

以下这几个章节没有去看

* 附录A：动态作用域
* 附录B：填补块儿作用域
* 附录C：词法 this
* 附录D：鸣谢