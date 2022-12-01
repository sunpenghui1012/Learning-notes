# Learning-notes
前端学习笔记 &amp; 踩坑日记 &amp; 冷知识，记录一些工作中遇到的问题，长期更新


## 1. `isNaN()` 和 `Number.isNaN()` 的区别

`Number.isNaN()` 方法确定传递的值是否为  NaN，并且检查其类型是否为  Number。它是  `isNaN()`  的更稳妥的版本。

和  `isNaN()`  相比，`Number.isNaN()` 不会自行将参数转换成数字，只有在参数是值为  NaN  的数字时，才会返回  true，否则返回 false。

```
Number.isNaN(NaN); // true
Number.isNaN(Number.NaN); // true
Number.isNaN(0 / 0); // true
```

```
Number.isNaN({}); // false
Number.isNaN('NaN'); // false
Number.isNaN('blabla'); // false
Number.isNaN(undefined); // false
```

```
isNaN({}); // true
isNaN('NaN'); // true
isNaN('blabla'); // true
isNaN(undefined); // true
```


## 2. `??` 运算符的妙用
Null 判断运算符
读取对象属性的时候，如果某个属性的值是null或undefined，有时候需要为它们指定默认值。常见做法是通过||运算符指定默认值。
```
const headerText = response.settings.headerText || 'Hello, world!';
const animationDuration = response.settings.animationDuration || 300;
const showSplashScreen = response.settings.showSplashScreen || true;
```
上面的三行代码都通过||运算符指定默认值，但是这样写是错的。开发者的原意是，只要属性的值为null或undefined，默认值就会生效，但是属性的值如果为空字符串或false或0，默认值也会生效。

为了避免这种情况，ES2020 引入了一个新的 Null 判断运算符??。它的行为类似||，但是只有运算符左侧的值为null或undefined时，才会返回右侧的值。

```
const headerText = response.settings.headerText ?? 'Hello, world!';
const animationDuration = response.settings.animationDuration ?? 300;
const showSplashScreen = response.settings.showSplashScreen ?? true;
```
上面代码中，默认值只有在左侧属性值为null或undefined时，才会生效。


## 3. 我们整天挂在嘴边的闭包到底是什么？

这里收集了不同文献中的原话，具体怎么理解看你自己：

>《JavaScript 高级程序设计》

闭包指的是那些引用了另一个函数作用域中变量的函数，通常是在嵌套函数中实现的。

>《Node 深入浅出》

在 JavaScript 中，实现外部作用域访问内部作用域中变量的方法叫做闭包（closure）。

>《JavaScript 设计模式与开发实践》

局部变量所在的环境被外界访问，这个局部变量就有了不被销毁的理由。这时就产生了一个闭包结构，在闭包中，局部变量的生命被延续了。

>《你不知道的 JavaScript（上卷）》

内部的函数持有对一个值的引用，引擎会调用这个函数，而词法作用域在这个过程中保持完整，这就是闭包。换句话说：当函数可以记住并访问所在的词法作用域，即使函数是在当前词法作用域外执行，这时就产生了闭包。
