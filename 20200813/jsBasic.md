## 选择题
### 1. 以下哪一项会对对象```person```有副作用？（考点：```Object.freeze()```）
```JavaScript
const person = {
  name: 'Lydia Hallie',
  address: {
    street: '100 Main St'
  }
}
Object.freeze(person)
```
+ A. ```person.name = 'Evan Bacon'```
+ B. ```delete person.address```
+ C. ```person.address.street = '101 Main St'```
+ D. ```person.pet = { name: 'Mara' }```
 
正确答案：C  
答案解析：  
使用 ```Object.freeze()``` 对一个对象进行冻结，就不能对属性进行添加、删除、修改。但这都是<font style="color: rgb(227,79,140);">浅冻结</font>。

### 2.输出什么？（考点：数组&对象）
```javascript
const food = ['apple','pizza','banana','orange']
const info = { favoriteFood: food[0] }

info.favoriteFood = 'milk'

console.log(food)
```
错误答案：```['milk','pizza','banana','orange']```  
正确答案：```['apple','pizza','banana','orange']```  
答案解析：  
虽然 ```food``` 为引用类型的值，但 ```food[0] => 'apple'``` 为字符串，是基础类型的值，按值传递。故此，```info.favoriteFood```只是拿到了字符串```'apple'```，与原数组```food```没有任何关系。

### 3.输出什么？（考点：ES6剩余参数）
```javascript
function getItems(fruitList,...args,favoriteFruit) {
  return [...fruitList,...args,favoriteFruit]
}

getItems(['banana','apple'],'pear','orange')
```
错误答案： ```['banana','apple','pear','orange']```  
正确答案： ```SyntaxError```  
答案解析：  
```...args``` 剩余参数的值是一个包含所有剩余参数的数组，并且<font style="color: rgb(227,79,140);">只能作为最后一个参数</font>。  
```javascript
function getItems(fruitList,favoriteFruit,...args) {
  return [...fruitList,...args,favoriteFruit]
}

getItems(['banana','apple'],'pear','orange')
```
上述改正后的代码会正常返回：```['banana','apple','orange','pear']```

### 4.输出什么？（考点：对象）
```javascript
const person = {
  name: 'Lydia',
  age: 21
}

let city = person.city
city = 'Amsterdam'

console.log(person)
```
错误答案： ```{ name: 'Lydia', age: 21, city: undefined }```  
正确答案： ```{ name: 'Lydia', age: 21 }```  
答案解析：  
```person``` 对象上没有 ```city``` 属性，所以 ```city``` 变量执行赋值操作后值为 ```undefined``` 。  
<font style="color: rgb(227,79,140);">！注意：</font> 我们没有引用 ```person``` 对象本身，只是将变量 ```city``` 设置为 ```person.city``` 的当前值，而这一步并不会在对象 ```person``` 上添加属性 ```city``` 。因此，打印 ```person``` 对象时，会返回未修改的对象。

### 5.输出什么？（考点：```try...catch()```）
```javascript
(() => {
  let x,y
  try {
    throw new Error()
  } catch(x) {
    x = 1,y = 2
    console.log(x)
  }
  console.log(x)
  console.log(y)
})
```
正确答案： 1 undefined 2  
答案解析：  
+ ```catch``` 块接收参数 ```x``` ，这与变量 ```x``` 不同。这个参数 ```x``` 是属于 ```catch``` 作用域的。  
+ 在 ```catch``` 作用域内分别对参数 ```x``` 和 变量 ```y``` 赋值。此时的两者的赋值有些差异：
  - x是 ```catch``` 作用域内的局部变量（可想象成是函数的形参）
  - 而 ```y``` 由于没有被作为参数传入 ```catch``` ，所以会LHS查询到上一层的 ```y``` ，即此处的全局变量 ```y``` 。对y的赋值也是基于此全局变量 ```y``` 的（即赋值操作之后，全局的 ```x = undefined```，全局的 ```y = 2```）
+ 此时，打印参数 ```x``` 的值为1（若打印变量 ```y``` 的值应为2）。  
+ 在 ```catch``` 块之外， ```x``` 仍然是 ```undefined``` ，而 ```y = 2```。

### 6.输出什么？（考点：对象）
```javascript
const myFunc = ({x,y,z}) => {
  console.log(x,y,z)
}

myFunc(1,2,3)
```
错误答案： 1 2 3  
正确答案： undefined undefined undefined  
答案解析：  
```myFunc``` 方法接收一个包含 ```x,y,z``` 属性的对象作为它的参数。但调用时仅传入了三个单独的数字值1，2，3，而非一个含有 ```x,y,z``` 属性的对象 ```{x: 1,y: 2,z: 3}``` ，故返回 ```x,y,z``` 的默认值 ```undefiend``` 。