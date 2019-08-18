
## js判断对象是否为空

**1、使用ES6提供的 Object.keys(obj) 方法**

Object.keys 返回一个数组，包括对象自身的（不含继承的）所有可枚举属性（不含 Symbol 属性）的键名。

```javascript
Object.keys(obj).length === 0 && obj.constructor === Object  //true表示为空对象，false为非空对象
```
**缺点：** 部分浏览器不支持，需要通过 babel 类插件转为 ES5

**2、遍历对象，通过对象的 hasOwnProperty() 方法判断**

```javascript
isEmpty(obj) {
    for (var prop in obj) {
        if (obj.hasOwnProperty(prop)) {
             return false;
        }
    }
    return true && JSON.stringify(obj) === JSON.stringify({});
}
//isEmpty(obj) 等于true表示为空对象，等于false表示非空对象

```

**3、使用 jquery 的 isEmptyObject(obj) 方法**

```javascript
jquery.isEmptyObject(obj)  //true表示为空对象，false为空对象
```

**4、后续方法更新中...**