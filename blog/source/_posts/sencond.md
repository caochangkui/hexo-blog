---
title: JavaScript浅拷贝和深拷贝
categories: JS
---
在JavaScript中，以对象为例，浅拷贝只会复制对象的第一层数据；深拷贝不仅仅会复制第一层的数据，如果里面还有对象，会继续进行复制，直到复制到全是基本数据类型为止。


<!-- more -->


 - 浅拷贝：只会复制对象的第一层数据
 - 深拷贝：不仅仅会复制第一层的数据，如果里面还有对象，会继续进行复制，直到复制到全是基本数据类型为止
**简单来说，浅拷贝是都指向同一块内存区块，而深拷贝则是另外开辟了一块区域**

例如，浅拷贝：
```

let arr = [1,2,3,4];
let arr2 = arr;

arr2.push(5);

console.log(arr); // [1, 2, 3, 4, 5]
console.log(arr2); // [1, 2, 3, 4, 5]
```


----------
对深拷贝来说，有以下的方法：

### 1. 深拷贝的简单方法:

 - 对数组来说：

```
let arr = [1,2,3,4];

let arr2 = [];

for(let i=0;i<arr.length;i++){
    arr2[i] = arr[i];
}

arr2.push(5);

console.log(arr); // [1, 2, 3, 4]
console.log(arr2); // [1, 2, 3, 4, 5]
```

 - 对对象来说（for..in）:

```
let obj = {
    name:"haha",
    age:18
}

let obj2 = {};

for(var attr in obj){
    obj2[attr] = obj[attr]
}

obj2.name = 'hehe';

console.log(obj); // {name: "haha", age: 18}
console.log(obj2); // {name: "hehe", age: 18}
```
### 2. 深拷贝的es6方法：[Object.assign()][1]

```
let obj = {
    name:"haha",
    age:18
}

let obj2 = {};

Object.assign(obj2,obj);

obj2.name = 'hehe';

console.log(obj); // {name: "haha", age: 18}
console.log(obj2); // {name: "hehe", age: 18}
```

### 3. 深拷贝的方法封装:

但是，对于下面的例子(包含多层对象)，不能用Object.assign()
```
let arr = [1,2,3,4,[5],{}];

let arr2 = Object.assign([],arr);

arr2[4].push(6);

console.log(arr) // [1, 2, 3, 4, [5,6], {…}]
console.log(arr2) // [1, 2, 3, 4, [5,6], {…}]
```

所以，这里封装了一个深拷贝函数**deepClone**

```
let arr = [1,2,3,4,[5],{}];

let arr2 = deepClone(arr);

arr2[4].push(6);

function deepClone(obj){ //深度克隆
let o = obj.push?[]:{};
for(let attr in obj){
    //值为复合类型
    if(typeof obj[attr] === 'object' && obj[attr]!=null){
        o[attr] = deepClone(obj[attr]);
    }else{
        o[attr] = obj[attr];
    }
}
return o;
}

console.log(arr) // [1, 2, 3, 4, [5], {…}]
console.log(arr2) // [1, 2, 3, 4, [5,6], {…}]
```

  [1]: https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Object/assign