
## canvas在H5中的绘图总结

### 一、canvas使用场景介绍
需求：用户在H5里面答题，然后根据得分情况生成一个奖状，奖状上会显示用户的个人信息（微信昵称、答题时间），奖状可以保存，实际效果如下图所示。

![](https://user-gold-cdn.xitu.io/2019/2/25/169241a97e26d9a1?w=727&h=705&f=png&s=379326)

### 二、项目中遇到的坑
**1、把奖状背景图绘制到canvas上，会出现图片和文字模糊问题；**

**2、用户微信昵称绘制到奖状上的红线位置，需要在红线区域居中，但是用户昵称千奇百怪，较难处理；**

**3、奖状上的绘制的文字字体大小在移动端需要自适应。**

### 三、解决方案
**1、问题1解决方案：**

（1）canvas中存在两种尺寸：

     canvas 的 width/height 是画布的宽/高，用来确定这个画布的内容大小，类似于 img 标签中的图片的宽高属性；
     canvas 的 样式表里的 width/height 代表的是最终绘制到浏览器上的尺寸，是 canvas 的物理宽度，
     类似于 img 标签中 样式表中设置的宽高属性。
（2）图片和文字模糊原因

     canvas 中属性的宽高并不代表实际的宽度，所以在高分辨率设备下（高清屏），浏览器就会放大 canvas，导致模糊；
     canvas 的最小单位是像素，通常情况下，设备的一个像素可以绘制一个点，
     但是当 window.ddevicePixelRatio > 1 |的时候，设备就会用大于1的像素个数绘制 canvas
     上的一个点，这时候如果还按照原始的画布大小去绘制图片或者文字时，看到的线条就比较粗，出现模糊的现象。
（3）根据 devicePixelRatio 的值，放大 canvas 的内容大小，去掉模糊效果
```javascript
const canvasBg = new Image(); //省略奖状图片地址
let canvas = document.getElementById("myCanvas");
canvasBg.onload = () => {
    let ctx = canvas.getContext("2d");
    let getPixelRatio = function (context) {
          let backingStore = context.backingStorePixelRatio ||
            context.webkitBackingStorePixelRatio ||
            context.mozBackingStorePixelRatio ||
            context.msBackingStorePixelRatio ||
            context.oBackingStorePixelRatio ||
            context.backingStorePixelRatio || 1;
            
          return (window.devicePixelRatio || 1) / backingStore;
        };
}
let ratio = getPixelRatio(ctx);  //获取设备物理像素与设备独立像素的比例
let imgW = canvasBg.width;
var imgH = canvasBg.height;
canvas.width = $(window).width() * ratio;  //放大画布内容的宽度
canvas.height = imgH * $(window).width() / imgW * ratio;  //放大画布内容的高度
let cW = $('#myCanvas').width();
let cH = $('#myCanvas').height();
canvas.style.width = "100%";
ctx.drawImage(canvasBg, 0, 0, cW, imgH * cW / imgW);  //把奖状模板绘制到canvas上，自适应奖状背景图，不拉伸或压缩图片
```
**2、问题2解决方案：**

（1）解决思路：

     先计算奖状上红线的宽度，然后在计算出用户昵称的宽度，对于超过红线宽度的用户昵称做特殊处理，
     截断超过红线的字符串，用省略号替代
 ```javascript
     //截取字符串方法，参数1为传入的用户昵称，参数2为要截取的字符串长度
     function cutstr(str, len) {
      var str_length = 0,
        str_cut = new String(),
        str_len = str.length;
      var charAtStr;
      for (var i = 0; i < str_len; i++) {
        //获取str字符串指定位置的字符
        charAtStr = str.charAt(i);
        str_length++;
        //中文字符的长度经编码之后大于4，其他字符小于4，因此中文字符占两位，其他字符占一位
        if (escape(charAtStr).length > 4) {
          str_length++;
        }
        str_cut = str_cut.concat(charAtStr);
        if (str_length >= len) {
          str_cut = str_cut.concat("..");
          return str_cut;
        }
      }
      //如果给定字符串小于指定长度，则返回源字符串；
      if (str_length < len) {
        return str;
      }
    }
  }
  let userInfo = {
      userName: "xxx张小二xxx"
  };
  let paddingLeft = 0;  //居中的字符串距离 canvas 左边界的距离
  //ctx.measureText(userInfo.userName).width 为字符串的宽度
  //146 * $('#myCanvas').width() / 727 * ratio 根据比例算出红线的宽度
  if (ctx.measureText(userInfo.userName).width > 146 * $('#myCanvas').width() / 727 * ratio) {
      userInfo.userName = cutstr(userInfo.userName, 8);
   }
   //魔鬼数字为固定尺寸奖状上的某些元素的宽度，然后在根据比例求出
   paddingLeft = 68 * $('#myCanvas').width() / 360 * ratio + (146 * $('#myCanvas').width() / 727 * ratio - ctx.measureText(userInfo.userName).width) / 2;
    //绘制用户昵称到奖状上
   ctx.fillText(userInfo.userName, paddingLeft, 210 * $('#myCanvas').height() / 640 * ratio);
 ```
 **3、问题3解决方案：**
 
（1）解决思路

     利用rem设置字体大小，使用淘宝的 flexible 插件计算出移动设备根节点的font-size，
     然后在某一固定分辨率的设备上计算出当前用户昵称对应的字体大小，然后根据比例求出其他设备对应的字体大小
    
```javascript
    ctx.fillStyle = "red";
    let fontSize = getComputedStyle(window.document.documentElement)['font-size'];
    //0.41 为在某个确定分辨率下调试出的字体rem值
    ctx.font = fontSize.replace(/px/, "") * 0.41 * ratio + "px Arial";
    
```
    
### 四、H5体验地址，做的不够完美，希望大家多多指导，谢谢！


![](https://user-gold-cdn.xitu.io/2019/2/26/16928fd70ed5788b?w=200&h=200&f=png&s=3829)
