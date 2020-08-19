## 选择题
### 1. 输出什么？（考点：事件冒泡）
```JavaScript
<div onClick="console.log('first div')">
  <div onClick="console.log('second div')">
    <button onClick="console.log('button')">
      Click!
    </button>
  </div>
</div>
``` 
错误答案：div外部  
正确答案：button  
答案解析：  
+ ```event.target``` 是当前触发点击事件的元素。上题点击在**按钮**上，所以 ```event.target``` 为 ```button``` 元素。但如果是在 ```second div``` 的区域内（button区域外），```event.target``` 为 ```second div``` 元素。
+ 导致事件的最深嵌套元素是事件的目标。即：若点击事件发生在上题中各层嵌套的“范围”内，那么，最终 ```event.target``` 指向最深嵌套层元素。但，<font style="color: rgb(227,79,140);">每一层的 ```onClick``` 事件都会触发</font>。
+ 可通过 ```event.target``` 停止冒泡。

## 2.输出什么？（考点：```import```）
```javascript
// index.js
console.log('running index.js')
import { sum } from 'sum.js'
console.log(sum(1, 2))

// sum.js
console.log('running sum.js')
export const sum = (a, b) => a + b
```
+ A. running index.js，running sum.js，3  
+ B. running sum.js，running index.js，3  
+ C. running sum.js，3，running index.js  
+ D. running index.js，undefined，running sum.js  

正确答案：B  
答案解析：  
```import``` 命令是<font style="color: rgb(227,79,140);">编译阶段</font>执行的，在代码运行之前。因此，被导入的模块会先运行，而导入模块的文件会后执行。
> 这是CommonJS中 ```require()``` 和 ```import``` 之间的区别。使用 ```require()```，您可以在运行代码时根据需要加载依赖项。如果我们使用 ```require``` 而不是 ```import```，```running index.js```、```running sum.js```、```3``` 会依次被打印。

### 3.JavaScript中的所有内容都是？（考点：JS类型）
+ A. 基本类型和对象
+ B. 函数和对象
+ C. 只有对象
+ D. 数字与对象

错误答案：C  
正确答案：A  
答案解析：  
基本类型有：```boolean,null,undefined,bigint,number,string,symbol```

### 4.输出什么？（考点：对象解构&```...```操作符）
```javascript
const value = { number: 10 }

const multiply = (x = { ...value }) => {
  console.log(x.number *= 2)
}

multiply()
multiply()
multiply(value)
multiply(value)
```
正确答案：20,20,20,40  
答案解析：  
上述例子中，将 ```value``` 进行了解构并传到一个<font style="color: rgb(227,79,140);">新对象</font>中，因此 ```x``` 的默认值为 ```{ number: 10 }```。  
<font style="color: rgb(227,79,140);">！注意：</font> ```...``` 操作符可进行浅拷贝。