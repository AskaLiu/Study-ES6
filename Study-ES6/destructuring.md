### ES6允许按照一定模式，从数组和对象中提取值，对变量进行赋值，这被称为解构（Destructuring）。
# 数组的解构赋值
### 如果解构不成功，变量的值就等于undefined
```javascript
let [foo] = []; // undefined
let [bar, foo] = [1]; // foo undefined
```

### 不完全解构
等号左边的模式，只匹配一部分的等号右边的数组。这种情况下，解构依然可以成功。
```javascript
let [x, y] = [1, 2, 3];
x // 1
y // 2

let [a, [b], d] = [1, [2, 3], 4];
a // 1
b // 2
d // 4
```

### 只要某种数据结构具有Iterator接口，都可以采用数组形式的解构赋值,f否者报错

# 解构赋值允许指定默认值
只有数组元素严格等于(===)undefined时，默认值才生效
```javascript
let [foo = true] = [];
foo // true

let [x, y = 'b'] = ['a'] // x='a', y='b'
let [x, y = 'b'] = ['a', undefined] // x='a', y='b'
```

# 对象的解构赋值
对象的解构与数组有一个重要的不同。数组的元素是按次序排列的，变量的取值由它的位置决定；而对象的属性没有次序，变量必须与属性同名，才能取到正确的值。
```javascript
let { bar, foo } = { foo: "aaa", bar: "bbb" };
foo // "aaa"
bar // "bbb"

let { baz } = { foo: "aaa", bar: "bbb" };
baz // undefined
```

### 如果变量名与属性名不一致，必须写成下面这样。
实际上,对象的解构赋值是下面形式的简写
```javascript
let { foo: foo, bar: bar } = { foo: "aaa", bar: "bbb" };
```
也就是说，对象的解构赋值的内部机制，是先找到同名属性，然后再赋给对应的变量。真正被赋值的是后者，而不是前者。

### 如果要将一个已经声明的变量用于解构赋值，必须非常小心。

```javascript
// 错误的写法
var x;
{x} = {x: 1}; // SyntaxError: syntax error

//上面代码的写法会报错，因为JavaScript引擎会将{x}理解成一个代码块，从而发生语法错误。只有不将大括号写在行首，避免JavaScript将其解释为代码块，才能解决这个问题
({x} = {x: 1}); // 正确的写法
```

# 用途
### 交换变量的值
```javascript
let [x, y] = [1, 2];
```

### 从函数返回多个值
```javascript
function func() {
    return {
        x: 1,
        y: 2
    };
}
let {x, y} = func();
```

### 函数参数的定义
```javascript
function func([x, y, z]) {}
func([1, 2, 3]);
function func({x, y, z}) {}
func({x: 1, y: 2, z: 3});
```

### 提取JSON
```javascript
var jsonData = {
  id: 42,
  status: "OK",
  data: [867, 5309]
}
let { id, status, data: number } = jsonData;
```

### 函数参数的默认值
```javascript
function func(a,
    {
        b = false, 
        c = function() {}
    }
) {
    // do something
}
func(a,{b: true});
```

### 遍历Map数据
任何部署了Iterator接口的对象，都可以用for...of循环遍历。Map结构原生支持Iterator接口，配合变量的解构赋值，获取键名和键值就非常方便。
```javascript
var map = new Map();
map.set('first', 'hello');
map.set('second', 'world');

for (let [key, value] of map) {
  console.log(key + " is " + value);
}
// first is hello
// second is world
```

### 输入模块的指定方法
加载模块时，往往需要指定输入那些方法。解构赋值使得输入语句非常清晰。
```javascript
const { SourceMapConsumer, SourceNode } = require("source-map");
```