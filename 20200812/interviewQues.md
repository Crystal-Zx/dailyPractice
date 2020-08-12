## 选择题
### 1. 输出什么？（考点：```reduce()```）
```JavaScript
[1,2,3,4].reduce((x,y) => console.log(x,y))
```
错误答案：1 undefined and 2 undefined and 3 undefined and 4 undefined  
正确答案：1 2 and undefined 3 and undefined 4  
答案解析：  
> 主要语法：  
```arr.reduce(callback(accumulator, currentValue[, index[, array]])[, initialValue])```  
—— [MDN Array.prototype.reduce()](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Array/Reduce)   

```reduce()``` 方法对数组中的每个元素执行一个由您提供的 ```reducer``` 函数（升序执行），将其结果汇总为单个返回值，此外还接收一个可选参数```initialValue```。  
1. ```reducer``` 函数（即reduce()方法的回调函数）接收4个参数：
    + Accumulator （acc） （累计器）
    + Current Value （cur） （当前值）
    + Current Index （idx） （当前索引）
    + Source Array （src） （源数组）  
  您的 ```reducer``` 函数的返回值分配给累计器，该返回值在数组的每个迭代中被记住，并最后成为最终的单个结果值。
2. 可选参数```initialValue```：
作为第一个调用回调函数时第一个参数的值。如果没有提供，则将使用数组中第一个参数的值，<font style="color: rgb(227,79,140);">那么第一个调用时的当前值则应是数组中下标为1的值</font>。

在上述例子中  
+ 第一次调用：累加器x为1，当前值y为2，打印出累加器和当前值：1和2
+ 第二次调用：由于第一次没有返回任何值，则默认返回 ```undefined``` 作为此次调用时累加器x的值，所以打印出累加器和当前值： ```undefined``` 和 3
+ 第三次调用：同上述第二次调用，打印出： ```undefined``` 和 4

---

### 2. 输出什么？（考点：箭头函数返回值）
```JavaScript
const getList = ([x,...y]) => [x,y]
const getUser = user => { name: user.name, age: user.age }

const list = [1,2,3,4]
const user = { name: 'Lydia', age: 21 } 

console.log(getList(list))
console.log(getUser(user))
```
错误答案：```[1,[2,3,4]]``` and ```{ name: 'Lydia', age: 21 }```  
正确答案：```[1,[2,3,4]]``` and ```undefined```  
答案解析：  
对于箭头函数，如果只返回一个值，我们不必编写花括号。但如果想从一个箭头函数返回一个对象，则必须在圆括号内编写这个对象，否则不返回任何值。故打印该函数调用输出```undefined```。
1. ```getList()```方法接收一个数组参数，将 ```list``` 数组作为参数传入，等价于 ```[x,...y] = [1,2,3,4]``` （<font style="color: rgb(227,79,140);">数组解构</font>），即：```x = 1,y = [2,3,4]```。所以，打印出：```[1,[2,3,4]]```
2. ```getUser()```方法使用箭头函数，将对象变量```user```作为参数传入，创建了对象 ```{ name: 'Lydia', age: 21 }```，但由于**未加圆括号**，没有将此新对象顺利返回。

---

### 3.输出什么？（考点：JS对象）
```javaScript
let person = { name: 'Lydia' }
const members = [person]
person = null

console.log(members)
```
错误答案：```[{}]```  
正确答案：```[{ name: 'Lydia' }]```  
答案解析：```person = null``` 只是释放了变量```person```对内存中对象 ```[{ name: 'Lydia' }]```的引用！！！

---

### 4.输出什么？（考点：```String.raw```）
```javascript
console.log(String.raw`Hello\nworld`)
```
错误答案：不知String.raw用法  
正确答案：Hello\nworld  
答案解析：
> —— [MDN String.raw()](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/String/raw)  
用来获取一个模板字符串的原始字符串。比如说，占位符（例如 ${foo}）会被处理为它所代表的其他字符串，而转义字符（例如 \n）不会。

用法举例：
```javascript
const path = `C:\Documents\Projects\demo.html`
console.log(String.raw`${path}`)  // C:DocumentsProjectsdemo.html

console.log(String.raw`C:\Documents\Projects\demo.html`)  // C:\Documents\Projects\demo.html
```

---

### 5.输出什么？（考点：IIFE）
```javascript
console.log(`${(x => x)('I love')} to program`)
```
错误答案：看不懂 ```${(x => x)('I love')}```  
正确答案：I love to program  
答案解析：```${(x => x)('I love')}```是一个立即执行函数表达式（IIFE）！！！

---

### 6.输出是什么？（考点：delete操作符）
```javascript
const name = 'Lydia'
age = 21 

console.log(delete name)
console.log(delete age)
```
错误答案：true true  
正确答案：false true  
答案解析：<font style="color: rgb(227,79,140);">通过```var,const,let```声明的变量无法通过```delete```删除。</font>上述变量```name```通过```const```声明，删除失败返回```false```；而变量```age```相当于<font style="color: rgb(227,79,140);">给全局对象创建了一个属性</font>，是可以通过```delete```操作符删除的，故返回```true```。