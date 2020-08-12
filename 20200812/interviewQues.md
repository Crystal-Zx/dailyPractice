## 选择题
1.输出什么？
```
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
作为第一个调用回调函数时第一个参数的值。如果没有提供，则将使用数组中第一个参数的值，<span style="color: rgb(227,79,140);">那么第一个调用时的当前值则应是数组中下标为1的值</span>。

在上述例子中 
+ 第一次调用：累加器x为1，当前值y为2，打印出累加器和当前值：1和2
+ 第二次调用：由于第一次没有返回任何值，则默认返回 ```undefined``` 作为此次调用时累加器x的值，所以打印出累加器和当前值： ```undefined``` 和 3
+ 第三次调用：同上述第二次调用，打印出： ```undefined``` 和 4