## 选择题
### 1. 输出什么？（考点：```ES6 Proxy```）
```JavaScript
const handler = {
  set: () => console.log('Added a new property!')
  get: () => console.log('Accessed a property!')
}

const person = new Proxy({}, handler)

person.name = 'Lydia'
person.name
``` 
正确答案：Added a new property! Accessed a property!  
答案解析：  
> <font style="color: rgb(227,79,140);">**关于proxy**</font>：Proxy 用于修改某些操作的默认行为，等同于在语言层面做出修改，所以属于一种“元编程”（meta programming），即对编程语言进行编程。  
Proxy 可以理解成，在目标对象之前架设一层“拦截”，外界对该对象的访问，都必须先通过这层拦截，因此提供了一种机制，可以对外界的访问进行过滤和改写。  
—— [ECMAScript 6入门——阮一峰](https://es6.ruanyifeng.com/#docs/proxy)  

故，在上述代码中：  
第一个参数是一个空对象 ```{}```，作为 ```person``` 的值。对于这个对象，自定义行为被定义在对象 ```handler```。如果我们想对象 ```person``` 添加属性，```set``` 将被调用；如果我们获取 ```person``` 的属性，```get``` 被调用。

### 2. 输出什么？（考点：```ES6 Generator函数```）
```javascript
function* generator(i) {
  yield i;
  yield i * 2
}

const gen = generator(10)

console.log(gen.next().value)
console.log(gen.next().value)
```
+ A. [0,10],[10,20]
+ B. 20,20
+ C. 10,20
+ D. 0,10 and 10,20

错误答案：D
正确答案：C  
答案解析： 
> —— [ECMAScript 6入门——阮一峰_generator生成器](https://es6.ruanyifeng.com/?search=yield&x=0&y=0#docs/generator)  

+ 一般的函数在执行之后是不能中途停下的。但是，生成器函数却可以中途“停下”，之后可以再从停下的地方继续。  
+ 当生成器遇到 ```yield``` 关键字的时候，会生成 ```yield``` 后面的值。<font style="color: rgb(227,79,140);">！注意：生成器在这种情况下不返回（```return```）值，而是生成（```yield```）值。</font>  
+ ```next()``` 方法一步步执行生成器。  

上述代码的执行流程如下：  
+ 首先，初始化生成器函数并将值 ```10``` 传入，作为参数 ```i``` 的值。
+ 然后使用 ```next()``` 方法一步步执行生成器。第一次执行生成器的时候，```i``` 的值为 ```10```，遇到第一个 ```yield``` 关键字，它要生成 ```i``` 的值。此时，生成器<font style="color: rgb(227,79,140);">“暂停”</font>，生成了 ```10```。
+ 下一次的打印语句执行流程同上述步骤二。

### 3.补全空缺代码（考点：```ES6 Generator函数```）
```javascript
const teams = [
  { name: 'Team 1', members: ['Paul','Lisa'] },
  { name: 'Team 2', members: ['Laura','Tim'] }
]

function* getMembers(members) {
  for(let i = 0; i < members.length; i++) {
    yield members[i]
  }
}

function* getTeams(teams) {
  for(let i = 0; i < teams.length; i++) {
    // → Something is Missing here ←
  }
}

const obj = getTeams(teams)
obj.next()
obj.next()
```
错误答案：return yield getMembers(teams[i].members)  
正确答案：yield* getMembers(teams[i].members)  
答案解析：  
不能加 ```return``` 的原因见题2解析。
> 如果yield表达式后面跟的是一个遍历器对象，需要在yield表达式后面加上星号，表明它返回的是一个遍历器对象。这被称为yield*表达式。
—— [ECMAScript 6入门——阮一峰_yield表达式](https://es6.ruanyifeng.com/?search=yield&x=0&y=0#docs/generator#yield--%E8%A1%A8%E8%BE%BE%E5%BC%8F)  

### 4.下面代码的输出是什么？（考点：等于/全等于）
```javascript
let a = 3
let b = new Number(3)
let c = 3

console.log(a == b)
console.log(a === b)
console.log(b === c)
```
正确答案：true false false  
答案解析：  
```Number()```是一个内置的构造函数，通过它实例化出来的变量是一个对象，具有很多额外的API，并不是基础类型值。  
```==```只检查值，不检查类型。而```===```会额外检查类型。  
<font style="color: rgb(227,79,140);">！注意：</font> ```==```会引发隐式类型转换，右侧的对象类型会自动拆箱为Number基础类型。

### 5.输出什么？（考点：```Number()、Boolean()、Symbol()```）
```javascript
console.log(Number(2) === Number(2))
console.log(Boolean(false) === Boolean(false))
console.log(Symbol('foo') === Symbol('foo'))
```
正确答案：true，true，false  
答案解析：  
+ ```new Number(2) === new Number(2)``` 为 ```false```（用 ```==``` 也是 ```false```）。```Boolean```同理
+ 但 ```Symbol``` 不同。每个 ```Symbol``` 都是完全唯一的。传递给 ```Symbol``` 的参数只是给 ```Symbol``` 的一个描述。 ```Symbol``` 的值不依赖于传递的参数。上述测试相等的代码中，实际上是创建了两个全新的符号。

### 6.输出什么？（考点：类型转换）
```javascript
const a = {}
const b = { key: 'b' }
const c = { key: 'c' }

a[b] = 123
a[c] = 456

console.log(a[b])
```
错误答案：123  
正确答案：456  
答案解析：  
+ ```a[b] = 123``` 试图将对象 ```b``` 作为对象 ```a``` 的键，其值为 ```123```。此时对象 ```b``` 会被隐式转换为字符串，即调用：```b.toString()```，其结果为 ```'[object Object]'```。  
+ ```a[b] = 123``` 的结果是：```a['object Object'] = 123```
+ 同理：```a[c] = 123``` 的结果是：```a['object Object'] = 456```。相当于修改了对象 ```a```下同一属性的值。

### 7.当我们这样做时会发生什么？（考点：函数）
```javascript
function bark() {
  console.log('Woof!')
}

bark.animal = 'dog'
```
+ A. Nothing,this is totally fine!
+ B. SyntaxError.You cannot add properties to a function this way
+ C. undefined
+ D. ReferenceError

错误答案：B  
正确答案：A  
答案解析：  
JS中除基础类型之外皆对象。（想象一下构造函数）  
```console.dir(bark)``` 会打印出如下内容：
```javascript
> f bark() 
  animal: 'dog'
  arguments: null
  caller: null
  length: 0
  name: 'bark'
  > prototype: {constructor: f}
  > __proto__: f ()
  ...
```
