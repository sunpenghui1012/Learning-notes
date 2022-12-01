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

