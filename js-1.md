## 数组去重汇总
### 一、双层循环比较去除法
**思路：**

（1）利用内层循环中的每一个数组元素跟外层循环中的当前数组值进行比较，如果值相同，则剔除掉该数组元素，继续循环比较，直至循环完成，输出没有重复元素的数组；

（2）注意，当遇到相等数组元素时，删除数组后，内层循环的下标需要减一。
```javascript

function arrUnique(arr){
    for(let i = 0, len = arr.length ; i < len ; i++) {
        for(let j = i + 1 ; j < len ; j++) {
            //内层循环每次比较的初始位置为外层循环当前循环的第二个元素
            //数组元素空值判断，防止一直陷入递归中，内存溢出
            if(arr[j] === arr[i] && arr[i]) {
                arr.splice(j , 1);   //删除重复元素
                j--;
            }
        }
    }
    return arr;
}

let arr = [1 , 2 , 3 , 0 , false , true , null , undefined , "null" , "undefined" , {} , NaN , true , 0 , null , 1 , NaN , undefined , {}];
console.log(arrUnique(arr));
//[1, 2, 3, 0, false, true, null, undefined, "null", "undefined", {}, NaN, 0, null, NaN, undefined, {}]

```

### 二、使用`indexOf()`方法去重
**思路：**

（1）创建一个空数组`resultArr`，然后for循环原始数组`arr`，使用`resultArr.indexOf(arr[i])`判断结果数组是否存在该元素，如果存在就接着循环，不存在就`push`到新数组中。
```javascript

function arrUnique(arr){
    //Array.isArray()用于确定传递的值是否是一个Array，返回true/false，IE9以下不支持
    if(!Array.isArray(arr)){
        console.log("传入的类型错误");
        return;
    }
    let resultArr = [];
    for(let i = 0, len = arr.length ; i < len ; i++) {
        if(resultArr.indexOf(arr[i]) === -1) {
            resultArr.push(arr[i]);
        }
    }
    return resultArr;
}

let arr = [1 , 2 , 3 , 2 , 4 , 5 , 1 , 3];
console.log(arrUnique(arr));
//[1, 2, 3, 4, 5]

```

### 三、