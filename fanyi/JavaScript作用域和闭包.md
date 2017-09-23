原文地址：https://css-tricks.com/javascript-scope-closures/
## 作用域
> A scope in JavaScript defines what variables you have access to. There are two kinds of scope – global scope and local scope.

JavaScript中的作用域定义了你访问的的是什么变量。作用域有两种：全局作用域和局部作用域。
###  全局作用域
> If a variable is declared outside all functions or curly braces ({}), it is said to be defined in the global scope.

如果一个变量被声明在所有的函数或者花括号之外，这个变量就可以说是在全局作用域下定义的。
> This is true only with JavaScript in web browsers. You declare global variables in Node.js differently, but we won't go into Node.js in this article.

 这个只在web浏览器下的JavaScript里有效。在Node.js里不是这么定义全局变量的，不过我们在这篇文章里面不打算对Node.js进行深入研究。
```
const globalVariable = 'some value'
```
> Once you've declared a global variable, you can use that variable anywhere in your code, even in functions.

一旦你声明了一个全局变量，你可以在你代码里的任何地方都可以使用这个变量，甚至是在函数里。
```
const hello ='Hello CSS-Tricks Reader!'
function sayHello(){
	console.log(hello);
}
console.log(hello);//Hello CSS-Tricks Reader!
sayHello();//Hello CSS-Tricks Reader!

```

> Although you can declare variables in the global scope, it is advised not to. This is because there is a chance of naming collisions, where two or more variables are named the same. If you declared your variables with const or let, you would receive an error whenever you a name collision happens. This is undesirable.

虽然你可以在全局作用域里声明变量，但是我们建议不要这么做。当两个或以上的变量使用相同的名字时可能导致命名冲突。如果你用const或者let声明你的变量，那么发生命名冲突的时候你就会收到error的警告。这是不可取的。

```
//不要这么干
let thing= 'something'
let thing = 'something else'//Error ,thing has already been declared
console.log(thing)
```
> If you declare your variables with var, your second variable overwrites the first one after it is declared. This also undesirable as you make your code hard to debug.

如果你用var声明一个变量，在你声明第二个同名变量后，你的第二个变量会覆盖第一个变量。这也是不可取的，因为这让你的代码变得难以debug。
```
// Don't do this!
var thing = 'something'
var thing = 'something else' // perhaps somewhere totally different in your code
console.log(thing) // 'something else'

```

> So, you should always declare local variables, not global variables.

所以你应该总是声明一个局部变量，而不是全局变量。
### 局部作用域
> Variables that are usable only in a specific part of your code are considered to be in a local scope. These variables are also called local variables.

> In JavaScript, there are two kinds of local scope: function scope and block scope.

> Let's talk about function scopes first.

只能在你代码的特定区域使用的的变量被认为是处于局部作用域里的。这些变量也被称为局部变量。
JavaScript里有两种局部作用域：函数作用域和块级作用域。
我们先谈一下函数作用域。

#### 函数作用域
> When you declare a variable in a function, you can access this variable only within the function. You can't get this variable once you get out of it.

当你在一个函数里面声明变量时，你只能在这个函数里使用这个变量。一旦你离开了这个函数，你就获取不到这个变量。
> In the example below, the variable hello is in the sayHello scope:

在下面的例子中，变量hello就处于sayHello的函数作用域里。
```

function sayHello(){
  const hello = 'Hello CSS-TRicks Reader!'
  console.log(hello)
}
sayHello()//Hello CSS-TRicks Reader!
console.log(hello)//Error,hello i not defined

```
#### 块级作用域
> When you declare a variable with const or let within a curly brace ({}), you can access this variable only within that curly brace.

当你用const或let在一个花括号{}里声明一个变量时，你只能在这个花括号里使用这个变量。

>  In the example below, you can see that hello is scoped to the curly brace:

在下面的例子里，你可以看到hello这个变量被限定在花括号里：

```
{
	const hello = 'Hello CSS-Tricks Reader!'
    console.log(hello) // 'Hello CSS-Tricks Reader!'
}
console.log(hello) // Error, hello is not defined
```
> The block scope is a subset of a function scope since functions need to be declared with curly braces (unless you're using arrow functions with an implicit return).

块级作用域（{}）是函数作用域的子集，因为函数都是需要用花括号声明的（除非你使用带有隐式返回的箭头函数）
#### 函数提升和作用域

> Functions, when declared with a function declaration, are always hoisted to the top of the current scope. So, these two are equivalent:

使用函数声明的函数总是会被提升到当前作用域的顶部。所以，这两个例子是等价的：
```

// This is the same as the one below
sayHello()
function sayHello () {
  console.log('Hello CSS-Tricks Reader!')
}
// This is the same as the code above
function sayHello () {
   console.log('Hello CSS-Tricks Reader!')
}
sayHello()
```
> When declared with a function expression, functions are not hoisted to the top of the current scope.

当你使用函数表达式来声明函数的时候，函数不会被提升到当前作用域的顶部。
```
sayHello() // Error, sayHello is not defined
const sayHello = function () {
  console.log(aFunction)
}
```

> Because of these two variations, function hoisting can potentially be confusing, and should not be used. Always declare your functions before you use them.

因为这两种不同，函数提升让人感到迷惑，所以是不应该使用的。你应该总是在你使用函数之前声明他们。
####  函数不能访问彼此的作用域

> Functions do not have access to each other's scopes when you define them separately, even though one function may be used in another.

> In this example below, second does not have access to firstFunctionVariable.

当你分开的声明函数的时候，函数是不能访问彼此的作用域的。虽然一个函数可能在另一个函数里面使用。
在下面这个例子中，second函数不能访问 firstFunctionVariable这个变量。

```
function first () {  
     const firstFunctionVariable = `I'm part of first`
}
function second () {  
     first()  
     console.log(firstFunctionVariable) // Error, firstFunctionVariable is not defined
}
```
####  嵌套作用域
 > When a function is defined in another function, the inner function has access to the outer function's variables. This behavior is called lexical scoping.

> However, the outer function does not have access to the inner function's variables.

当一个函数里面定义另一个函数，内部函数可以访问外部函数的变量。这种行为被称为词法作用域（静态作用域/词法闭包）。
然而外部函数不能访问内部函数的变量。

```

function outerFunction () {
     const outer = `I'm the outer function!`
function innerFunction() {
     const inner = `I'm the inner function!`
     console.log(outer) // I'm the outer function!
}
     console.log(inner) // Error, inner is not defined
}

```
> To visualize how scopes work, you can imagine one-way glass. You can see the outside, but people from the outside cannot see you.

为了形象的解释作用域是怎么工作的，你可以想象一面单面的玻璃。你可以看到外面，但是外面的人看不到你。

![](http://g.mdcdn.cn/h5/img/act/fy/1.png)

> If you have scopes within scopes, visualize multiple layers of one-way glass.

如果作用域里嵌套着作用域，可以形象化的表现为多层单面玻璃的叠加。

![](http://g.mdcdn.cn/h5/img/act/fy/2.png)
### 闭包

>  Whenever you create a function within another function, you have created a closure. The inner function is the closure. This closure is usually returned so you can use the outer function's variables at a later time.

当你在一个函数里面创建另一个函数的时候，你就创建了闭包。里面的函数就是闭包。闭包通常会被返回，所以你可以访问外部函数的变量。
```
function outerFunction () {
     const outer = `I see the outer variable!`
function innerFunction() {
     console.log(outer)
}
      return innerFunction
}
outerFunction()() // I see the outer variable!
```
>  Since the inner function is returned, you can also shorten the code a little by writing a return statement while declaring the function.

既然这个内部函数是要被返回的，那么你可以通过声明函数的时候写一个返回语句来稍微缩短你的代码。
```
function outerFunction () {
const outer = `I see the outer variable!`
     return function innerFunction() {
     console.log(outer)
}
}
outerFunction()() // I see the outer variable!
```
> Since closures have access to the variables in the outer function, they are usually used for two things:

>  1.To control side effects

>  2.To create private variables

因为闭包能够获取外部函数的变量，所以闭包通常用来做两件事：
1. 控制副作用
2. 创建私有变量

#### 用闭包控制副作用
>   Many things can be side effects, like an Ajax request, a timeout or even a console.log statement:

很多事情都会导致副作用，像ajax请求，一个超时（？？）甚至一个console.log()语句：

```
function (x) {
	console.log('A console.log is a side effect!')
}
```
> When you use closures to control side effects, you're usually concerned with ones that can mess up your code flow like Ajax or timeouts.

当你利用闭包来控制副作用的时候，你通常需要关注一些点。比如ajax或timeouts会破坏你的程序的运行顺序。
>  Let's go through this with an example to make things clearer.


让我们通过一个例子来更清晰地学习这一知识点。

> Let's say you want to make a cake for your friend's birthday. This cake would take a second to make, so you wrote a function that logs made a cake after one second.

打个比方说，你想为了你朋友的生日做一个蛋糕。这个蛋糕需要花一些时间来制作，所以你写了一个函数：一秒后打印“制作蛋糕“。

```
function makeCake() {
  setTimeout(_ => console.log(`Made a cake`), 1000)
}
```
> As you can see, this cake making function has a side effect: a timeout.

所以你可以看到，这个制作蛋糕的函数有一个副作用：一个定时器。
> Let's further say you want your friend to choose a flavor for the cake. To do so, you can write add a flavor to your makeCake function.

更进一步的说，你想让你的朋友给蛋糕选一个口味。为了加上这个功能，你可以在你的makecake这个函数里加上‘添加口味’。

```
function makeCake(flavor) {
  setTimeout(_ => console.log(`Made a ${flavor} cake!`, 1000))
}
```
> When you run the function, notice the cake gets made immediately after one second.

```
makeCake('banana')
// Made a banana cake!
```
> The problem here is that you don't want to make the cake immediately after knowing the flavor. You want to make it later when the time is right.

问题在于你并不想在知道蛋糕口味之后就马上制作蛋糕。你想在晚点时间合适的时候再开始做蛋糕。

> To solve this problem, you can write a prepareCake function that stores your flavor. Then, return the makeCake closure within prepareCake.

为了解决这个问题，你可以写一个prepareCake函数来保存口味这个变量。然后prepareCake这个函数里面返回makeCake这个闭包。

> From this point on, you can call the returned function whenever you want to, and the cake will be made within a second.

从这个点出发，你可以在任何时候调用返回的函数，并且蛋糕会在函数被调用一秒后制作。
```
function prepareCake (flavor) {
	return function () {
     	setTimeout(_ => console.log(`Made a ${fla			vor} cake!`, 1000))
	}
}
const makeCakeLater = prepareCake('banana') // And later in your code...
makeCakeLater() // Made a banana cake!
```
### 闭包和私有变量

>  As you know by now, variables created in a function cannot be accessed outside the function. Since they can't be accessed, they are also called private variables.

到目前为止你也知道了，在一个函数里创建的变量是不能被外部函数访问的。因为他们不能被外部访问，所以他们也被称为私有变量。

> However, sometimes you need to access such a private variable. You can do so with the help of closures.

然而，有时候你也需要访问一个私有变量。你可以借助闭包来获取私有变量。

```
function secret (secretCode) {
	return {
		saySecretCode () {
    	 	console.log(secretCode)
		}
	}
}
const theSecret = secret('CSS Tricks is amazing')
theSecret.saySecretCode() // 'CSS Tricks is amazing'
```
> saySecretCode in this example above is the only function (a closure) that exposes the secretCode outside the original secret function. As such, it is also called a privileged function.

saySecretCode在上面这个例子中是唯一一个除了原始的 secret函数外暴露了 secretCode的函数。所以也被叫私有函数。

#### 用devTools来debug作用域
> Chrome and Firefox's DevTools make it simple for you to debug variables you can access in the current scope. There are two ways to use this functionality.

chrome和火狐的 devTools让你可以很容易的debug那些你可以在当前作用域获取的变量。这里有两种方式来使用这个功能。
> The first way is to add the debugger keyword in your code. This causes JavaScript execution in browsers to pause so you can debug.

第一种方式是在你的代码里面添加'debuggger'关键字。这会导致javascript在浏览器里暂停执行，所以你可以debug。

> Here's an example with the prepareCake:

这儿有个prepareCake的例子。
```
function prepareCake (flavor) {
  // Adding debugger
  debugger
  return function () {
    setTimeout(_ => console.log(`Made a ${flavor} cake!`, 1000))
  }
}

const makeCakeLater = prepareCake('banana')
```
> If you open your DevTools and navigate to the Sources tab in Chrome (or Debugger tab in Firefox), you would see the variables available to you.

如果你打开你的devTools，并且打开sources这个tab，你就可以看到你可以使用的变量。

![](http://g.mdcdn.cn/h5/img/act/fy/3.png)

> The second way to use this debugging functionality is to add a breakpoint to your code directly in the sources (or debugger) tab by clicking on the line number.

第二种方式是利用debug这个功能来直接给代码打断点。
在sources（或debugger）tab里通过点击行数来给代码加断点。

![](http://g.mdcdn.cn/h5/img/act/fy/4.png)

### 总结

> Scopes and closures aren't incredibly hard to understand. They're pretty simple once you know how to see them through a one-way glass.

函数作用域和闭包也不是很难理解。当你知道怎么从单面玻璃这个例子理解他们的时就会觉得很简单了。
> When you declare a variable in a function, you can only access it in the function. These variables are said to be scoped to the function.

当你在一个函数里声明一个变量的时候，你只能在这个函数里面获取你的变量。这些变量就被局限在这个函数里。

> If you define any inner function within another function, this inner function is called a closure. It retains access to the variables created in the outer function.

如果你在另一个函数里定义一个函数的时候，内部的这个函数就被称为闭包。它可以获取外部函数的变量。
