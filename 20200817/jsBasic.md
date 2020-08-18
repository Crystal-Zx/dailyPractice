## 选择题
### 1. 输出什么？（考点：```构造函数```）
```JavaScript
function Person(firstName, lastName) {
  this.firstName = firstName
  this.lastName = lastName
}

const member = new Person('Lydia','Hallie')

Person.getFullName = () => this.firstName + this.lastName

console.log(member.getFullName())
``` 
错误答案：Lydia Hallie  
正确答案：TypeError  
答案解析：  
上述代码执行后打印以下语句：
```javascript
console.dir(Person)
console.dir(Person.prototype)
```
分别输出：
```javascript
> f Person() 
  getFullName: () => this.firstName + this.lastName
  arguments: null
  caller: null
  length: 0
  name: 'Person'
  > prototype: {constructor: f}
  > __proto__: f ()
  ...
```
```javascript
> Object
  > constructor: f Person(firstName, lastName)
  > __proto__: f ()
```
> 函数形式的构造函数下，向其添加方法后，只有构造函数本身可访问。其所有实例化对象均访问不到此方法。（除非将此方法添加到构造函数的原型对象上）  
> 以class声明的类，其中的方法若不加```static```关键字，则这个方法会被自动添加到这个类的原型对象上，反之则不会，exg:
> ```javascript
> class Person {
>   constructor() { ... }
>   drink() { console.log("drink") }
>   static eat() { console.log("eat") }
> }
> var p = new Person()
> p.drink()  // drink
> p.eat()    // TypeError: p.eat is not a function
> ```

### 2.输出什么？（考点：扩展运算符）
```javascript
function getAge(...args) {
  console.log(typeof args)
}

getAge(21)
```
错误答案："number"  
正确答案："object"  
答案解析：  
扩展运算符（```...```）返回一个带参数的数组。上述代码中： ```args = [21]```

### 3.输出什么？（考点：```Object.entries()```）
```javascript
const person = {
  name: 'Lydia',
  age: 21
}

for(const [x,y] of Object.entries(person)) {
  console.log(x,y)
}
```
错误答案：["name","age"] and undefined  
正确答案：name Lydia and age 21  
答案解析：  
```Object.entries()``` 方法返回一个给定对象<font style="color: rgb(227,79,140);">自身可枚举</font>属性的<font style="color: rgb(227,79,140);">键值对数组</font>。故上述该方法调用返回：
```javascript
[['name','Lydia'],['age','21']]
```
之后，```for-of``` 循环中声明的 ```const [x,y]``` 会对上述二维数组进行数组解构。

### 4.将会发生什么？（考点：箭头函数）★★★
```javascript
let config = {
  alert: setInterval(() => {
    console.log('Alert!')
  }, 1000)
}

config = null
```
错误答案： 我们从没调用过```config.alert()```，```config```为```null```  
正确答案：```setInterval``` 的回调仍然会被每秒钟调用  
答案解析：  
一般情况下当我们将对象赋值为 ```null```，那些对象会被进行<font style="color: rgb(227,79,140);">垃圾回收</font>。然而，```setInterval``` 的参数是一个箭头函数（所以上下文绑定到对象 ```config``` 了），回调函数仍然保持着对 ```config``` 的引用。