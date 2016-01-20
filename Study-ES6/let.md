# _let_ 命令
### 1.块级作用域
_**let**_ 声明的变量只在它所在的代码块有效
```javascript
{
  let a = 1;
  var b = 1;
}
a // ReferenceError: a is not defined.
b // 1
```

### 2.不存在声明提升
_**let**_ 不像 _**var**_ 那样会发生变量声明提升现象。所以，变量一定要在声明后使用，否则报错
```javascript
console.log(foo); // 输出undefined
console.log(bar); // 报错ReferenceError
var foo = 2;
let bar = 2;
```

### 3.暂时性死区
在代码块内，使用 _**let**_ 命令声明变量之前，该变量都是不可用的
```javascript
var tmp = 123;
if (true) {
  tmp = 'abc'; // ReferenceError
  let tmp;
}
```

### 4.不允许重复声明
_**let**_ 不允许在相同作用域内，重复声明同一个变量
```javascript
function () {
  let a = 10;
  var a = 1;
}
function () {
  let a = 10;
  let a = 1;
}
```

# 块级作用域
### _let_实际上为Javascript新增了块级作用域。
```javascript
function f1() {
  let n = 5;
  if (true) {
    let n = 10;
  }
  console.log(n); // 5
}
```

### 块级作用域的出现，使得获得广泛应用的立即执行匿名函数不再必要了。
```javascript
(function () {
  var tmp = ...;
  ...
}());

{
  let tmp = ...;
  ...
}
```

### 块级作用域外部，无法调用块级作用域内部定义的函数
```javascript
{
  let a = 'secret';
  function f() {
    return a;
  }
}
f() // 报错
```

# _const_ 命令
### const也用来声明变量，但是声明的是常量。一旦声明，常量的值就不能改变。
```javascript
'use strict';
const PI = 3.1415;
PI = 3; // TypeError: "PI" is read-only
```

### const一旦声明变量，就必须立即初始化，不能留到以后赋值
