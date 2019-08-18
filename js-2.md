
## 慎用slice()、concat()和assign()方法来拷贝数组
### 一、原数组里的数据不包含引用类型
```
let arr1 = [1 , 2 , 3 , "hello" , "world"];  //原数组
```

### 1、使用 slice() 方法

**拷贝数组：**
```javascript
let arr2 = arr1.slice(0);
console.log(arr2);   //打印新数组
[1 , 2 , 3 , "hello" , "world"];  //新数组
```

**修改经过 slice() 拷贝过的新数组：**
```javascript
arr2[3] = "Hello";
console.log(arr1);  //打印旧数组
[1 , 2 , 3 , "hello" , "world"]   
console.log(arr2);   //打印新数组
[1 , 2 , 3 , "Hello" , "world"]
```


<font color="red">结论：使用 slice() 方法拷贝数组，然后修改新数组，不会影响到旧数组的值。</font>

### 2、使用 concat() 方法

**拷贝数组：**
```javascript
let arr3 = [].conat(arr1);
console.log(arr3);   //打印新数组
[1 , 2 , 3 , "hello" , "world"];  //新数组
```
**修改经过 concat() 拷贝过的新数组**
```javascript
arr3[3] = "Hello";
console.log(arr1);  //打印旧数组
[1 , 2 , 3 , "hello" , "world"]   
console.log(arr3);   //打印新数组
[1 , 2 , 3 , "Hello" , "world"]
```


<font color="red">结论：使用 concat() 方法拷贝数组，然后修改新数组，不会影响到旧数组的值。</font>

### 3、使用 assign() 方法，es6中的对象方法，注意浏览器的兼容性

**拷贝数组：**
```javascript
let arr4 = Object.assign({} , arr1);
console.log(arr4);   //打印新数组
[1 , 2 , 3 , "hello" , "world"];  //新数组
```
**修改经过 assign() 拷贝过的新数组**
```javascript
arr4[3] = "Hello";
console.log(arr1);  //打印旧数组
[1 , 2 , 3 , "hello" , "world"]   
console.log(arr4);   //打印新数组
[1 , 2 , 3 , "Hello" , "world"]
```


<font color="red">结论：使用 assign() 方法拷贝数组，然后修改新数组，不会影响到旧数组的值。</font>

### 4、使用简单的数组赋值语法

**拷贝数组：**
```javascript
let arr5 = arr1;
console.log(arr5);   //打印新数组
[1 , 2 , 3 , "hello" , "world"];  //新数组
```
**修改经过简单赋值过的新数组**
```javascript
arr5[3] = "Hello";
console.log(arr1);  //打印旧数组
[1 , 2 , 3 , "Hello" , "world"]   
console.log(arr5);   //打印新数组
[1 , 2 , 3 , "Hello" , "world"]
```


<font color="red">结论：使用数组简单赋值方法拷贝数组，然后修改新数组，会影响到旧数组的值。</font>

<font color="red">原因：这种简单赋值的方法属于数组的浅拷贝，数组arr1和数组arr5共用同一块内存，其中一个数组改变，另一个数组也会跟着改变。</font>


### 二、原数组里的数据包含引用类型
```javascript
let arr1 = [1 , 2 , 3 , {"name" : "张小二"} , {"sex" : "male"}];  //原数组
```

### 1、使用 slice() 方法

**拷贝数组：**
```javascript
let arr2 = arr1.slice(0);
console.log(arr2);   //打印新数组
[1 , 2 , 3 , {"name" : "张小二"} , {"sex" : "male"}];  //新数组
```

**修改经过 slice() 拷贝过的新数组：**
```javascript
arr2[3].name = "隔壁张小二";
console.log(arr1);  //打印旧数组
[1 , 2 , 3 , {"name" : "隔壁张小二"} , {"sex" : "male"}]   
console.log(arr2);   //打印新数组
[1 , 2 , 3 , {"name" : "隔壁张小二"} , {"sex" : "male"}]
```

<font color="red">
结论：使用 slice() 方法拷贝数组，然后修改新数组，会改变旧数组的值。
</font>

### 2、使用 concat() 方法

**拷贝数组：**
```javascript
let arr3 = [].conat(arr1);
console.log(arr3);   //打印新数组
[1 , 2 , 3 , {"name" : "张小二"} , {"sex" : "male"}];  //新数组
```
**修改经过 concat() 拷贝过的新数组**
```javascript
arr3[3].name = "隔壁张小二";
console.log(arr1);  //打印旧数组
[1 , 2 , 3 , {"name" : "隔壁张小二"} , {"sex" : "male"}]   
console.log(arr3);   //打印新数组
[1 , 2 , 3 , {"name" : "隔壁张小二"} , {"sex" : "male"}]
```

<font color="red">
结论：使用 concat() 方法拷贝数组，然后修改新数组，会改变旧数组的值。
</font>

### 3、使用 assign() 方法

**拷贝数组：**
```javascript
let arr4 = Object.assign({} , arr1);
console.log(arr4);   //打印新数组
[1 , 2 , 3 , {"name" : "张小二"} , {"sex" : "male"}];  //新数组
```
**修改经过 assign() 拷贝过的新数组**
```javascript
arr4[3].name = "隔壁张小二";
console.log(arr1);  //打印旧数组
[1 , 2 , 3 , {"name" : "隔壁张小二"} , {"sex" : "male"}]   
console.log(arr4);   //打印新数组
[1 , 2 , 3 , {"name" : "隔壁张小二"} , {"sex" : "male"}]
```

<font color="red">
结论：使用 assign() 方法拷贝数组，然后修改新数组，会改变旧数组的值。
</font>

### 三、原因分析

**1、数组的浅拷贝**

（1）数组的直接赋值属于数组的浅拷贝，JS存储对象都是存内存地址的，所以浅拷贝会导致新数组和旧数组共用同一块内存地址，其中一个数组变化，另一个数组也会相应的变化。

（2）数组内部不含有引用类型，使用slice() 、concat() 和 assign() 方法都属于数组的深拷贝，一个数组变化，另一个数组不受影响。

（3）数组内部含有引用类型，使用slice() 、concat() 和 assign() 方法，非引用类型的值属于深拷贝，引入类型的值属于浅拷贝，一个数组变化，另一个也会相应的变化。

### 四、解决办法（含有引入类型的数组）

**方法一：递归**

```javascript
let cloneObj = function(obj){
    let str, newobj = obj.constructor === Array ? [] : {};
    if(typeof obj !== 'object'){
        return;
    } else if(window.JSON){
        str = JSON.stringify(obj), //系列化对象
        newobj = JSON.parse(str); //还原
    } else {
        for(var i in obj){
            newobj[i] = typeof obj[i] === 'object' ? 
            cloneObj(obj[i]) : obj[i]; 
        }
    }
    return newobj;
};

let newArr = cloneObj(oldArr);

```

**方法二：通过JSON解析解决**
```javascript
let newArr = JSON.parse(JSON.stringify(oldArr));
```
<font color="red">
注意：这种方法拷贝后的数组会丢失原数组中定义的方法和数组原型中定义的方法。
</font>