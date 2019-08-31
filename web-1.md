
## H5页面实现滑动控制音频播放

### 一、业务场景
微信中打开H5页面，滑动页面，滑动到指定位置区间，播放对应的音频，上下滑动页面，可快速切到对应的音频，然后播放。

### 二、实现方法 
**1、原理介绍**

首先计算出设计图的总高度，然后标注设计图上的音频切换点，算出切点所在的高度在整个设计图高度中所占的比例，最后根据比例算出实际页面中切点的高度。
```javascript
//切点配置信息
let scrollConfigInfo = [{
    top: 0,
    bottom: 0.12,
    audioUrl: "1.mp3",
    pageNum: 1
},{
    top: 0.12,
    bottom: 0.167,
    audioUrl: "2.mp3",
    pageNum: 2
},{
    top: 0.167,
    bottom: 0.26,
    audioUrl: "3.mp3",
    pageNum: 3
},{
    top: 0.26,
    bottom: 0.428,
    audioUrl: "4.mp3",
    pageNum: 4
},{
    top: 0.428,
    bottom: 0.57,
    audioUrl: "5.mp3",
    pageNum: 5
}]

//滑动页面控制音频播放
const audio = new Audio();
let scrollY = 0;
let currentPage = 1;  //初始化处于第一屏
let realPageAllHeight = 9221;   //设计图的页面总高度
let realFirstPageHeight = 1317;  //设计图第一屏的高度
let pageHeight = $(".page-1").height();  //设备上第一屏页面的高度
let pageAllHeight = pageHeight * realPageAllHeight / realFirstPageHeight;  //设备上页面总高度
$(window).scroll(() => {
    scrollY = $(document).scrollTop(); //获取当前滚动的高度
    for (let i = 0 , len = scrollConfigInfo.length; i < len; i++) {
    //当用户划到某个位置时，计算当前位置处于哪一个区间内，如果进入某个区间，就播放当前区间内的音频
    //currentPage !== (i + 1) 用来控制在一个区间内来回滑动不会来回重新播放该区间内的音频
    if (scrollY >= Math.floor(scrollConfigInfo[i].top * pageAllHeight) && scrollY < Math.floor(scrollConfigInfo[i].bottom * pageAllHeight) && currentPage !== (i + 1)) {
        audio.src = scrollConfigInfo[i].audioUrl;
        this.currentPage = scrollConfigInfo[i].pageNum;
        audio.play();
        break;
        }
      }
    });
```
## 三、H5效果展示

![](https://user-gold-cdn.xitu.io/2019/2/26/16928fd70ed5788b?w=200&h=200&f=png&s=3829)