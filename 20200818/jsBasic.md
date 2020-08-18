## 选择题
### 1. 输出什么？（考点：```...``` 扩展运算符）
```JavaScript
const user = { name: 'Lydia', age: 21 }
const admin = { admin: true, ...user }

console.log(admin)
``` 
错误答案：```{ admin: true, user: { name: 'Lydia', age: 21 }}```  
正确答案：```{ admin: true, name: 'Lydia', age: 21 }```  
答案解析：  
扩展运算符 ```...``` 可以复制对象的 <font style="color: rgb(227,79,140);">键值对</font>。上述 ```...user ``` 取得 ```user``` 对象的键值对后，将其加入 ```admin``` 对象中。

### 2.输出什么？（考点：数组）
```javascript
const list = [1 + 2,1 * 2,1 / 2]
console.log(list)
```
正确答案：```[3,2,0.5]```  
答案解析：  
数组元素可以包含任何值，如：数字、字符串、布尔值、对象、数组、```null```、```undefined```，以及其他表达式（日期、函数和 <font style="color: rgb(227,79,140);">计算</font>）。

### 3.输出什么？（考点：```||``` 运算符）
```javascript
const one = (false || {} || null)
const two = (null || false || '')
const three = ([] || 0 || true)

console.log(one,two,three)
```
正确答案：{} '' []  
答案解析：  
使用 ```||``` 运算符，<font style="color: rgb(227,79,140);">返回第一个真值。如果所有值都是假值，则返回最后一个值</font>。  
<font style="color: rgb(227,79,140);">！注意：</font> ```!![] => true,!!{} => true```

### 4.以下代码中后四句哪一句会导致报错？（考点：ES6 ```const```）
```javascript
const nums = [0,1,2,3]

nums.push(4)
nums.splice(0,2)
nums = [...nums,4]
nums.length = 0
```
错误答案：没有选  
正确答案：3 ```nums = [...nums,4]```  
答案解析：  
```const``` 关键字意味着不能重定义变量中的值，仅可读。但 ```nums``` 的值是一个指向数组 ```[0,1,2,3]``` 的地址，故在此处，仅限制了这个地址值不能被修改，但仍能通过这个地址值去操作其指向的数组。所以语句1、2、4都是正确的。  
而 ```nums = [...nums,4]``` 会试图将 ```nums``` 的值改变为另一新数组 ```[0,1,2,3,4]``` 在内存中的地址值，就会导致报错。

### 5.输出什么？（考点：【扩展】ES2020 ```#```）
```javascript
class Counter {
  #number = 10
  increment() {
    this.#number++
  }
  getNum() {
    return this.#number
  }
}
const counter = new Counter()
counter.increment()
console.log(counter.getNum())    //11
console.log(counter.#number)    //SyntaxError
```
答案解析：  
在 <font style="color: rgb(227,79,140);">**ES2020**</font> 中，通过 ```#``` 可以给 class 添加 <font style="color: rgb(227,79,140);">私有变量</font> 。在 class 的外部我们无法获取该值。当我们尝试输出 ```counter.#number```，语法错误（```SyntaxError```）被抛出：无法在 class Counter 外部获取它。这样就不需要使用闭包来隐藏不想暴露给外界的私有变量。