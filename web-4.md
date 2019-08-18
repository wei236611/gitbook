
## 移动端调试方法汇总

**背景：**
随着移动端的不断推进，`redZZ移动端`的调试也成为前端开发者不得不面临的问题，在PC端的时代，我们直接打开
chrome的检查元素面板，就可以解决大部分的问题了。但是到了移动端，明明在电脑上模拟好的元素，在手机上就会
乱掉。下面我们就来一起聊一聊移动端调试的那些问题，让真机调试不在那么困难。

#### 1、浏览器模拟手机调试

**1.1 如何使用？**

chrome作为一款浏览器，给开发者带来的便捷也是为人所称道的。在PC端，只需要F12，打开开发者工具，就可以开始调试了，这点就不用我多说了。而其开发者工具中加入的模拟手机调试选项更是强大。只需要点击**切换设备**工具，如图1.1.1所示。

![](https://user-gold-cdn.xitu.io/2018/6/4/163ca10d04496972?w=1136&h=611&f=png&s=124374)

**1.2 何时使用？**

建议在日常的开发过程中，尽量使用chrome模拟进行开发，因为其容易使用与速度快（电脑的性能与网速还是比手机强不少的）。使用模拟功能，我们能快速先把功能与布局调试出来。据笔者经验，使用chrome模拟开发出来的网页，一般在真机上都没什么问题。

**1.3 注意事项**

使用chrome模拟调试的同学可能有时候会碰到touchstart，touchend等事件无法触发的情况。先不要着急担心是自己代码的问题，因为chrome模拟调试。目前还有一点问题，我们在进行过一些操作后，模拟状态会丢失。chrome虽然窗口大小还在模拟移动端，鼠标事件已经变成PC端的模拟了。所以需要再触发两次模拟，就会恢复模拟移动端。如图1.1.2所示

![](https://user-gold-cdn.xitu.io/2018/6/4/163ca11b9cc86608?w=157&h=77&f=png&s=4536)

#### 2、Android手机 + chrome（真机调试）

**2.1 有什么用？**

虽然使用PC端浏览器模拟开发很强大，但是我们在chrome上模拟的移动端网页，在真机运行的时候，总会遇到一些样式错乱的问题，这时，我们就需要使用真机来进行调试；
**建议：**使用模拟开发完后，如果在真机上测试遇到了问题（无论什么浏览器），首先应该用chrome来检查一下，如果在手机chrome上也遇到了同样的问题，那么使用chrome的调试是非常方便的，应该首选其调试。

**2.2 如何使用？**

你需要有：一台Android手机，一台电脑，一根Android数据线

**操作步骤：**
1、首先需要在Android手机上安装chrome浏览器；
2、然后打开手机的开发者模式，一般Android手机都是通过以下路径打开开发者模式，设置->关于手机->版本号连按5次，之后设置菜单里会多出一个开发人员选项，进入将其中的“USB调试”打开即可，如图2.2.1


![](https://user-gold-cdn.xitu.io/2018/6/4/163ca1219c6a4a6c?w=344&h=616&f=png&s=92456)

3、将手机与电脑通过USB线连接，弹出对话框“是否允许USB调试”，选择确定，如图2.2.2


![](https://user-gold-cdn.xitu.io/2018/6/4/163ca1259d0dc291?w=350&h=409&f=png&s=178698)

4、打开手机上的chrome，并进入需要调试的页面，如图2.2.3

![](https://user-gold-cdn.xitu.io/2018/6/4/163ca128b2e26c36?w=360&h=640&f=png&s=113658)

5、打开PC端chrome，在地址栏中输入chrome://inspect/，进入调试页面，此时，我们发现，chrome检测到了我们的手机，如图2.2.4

![](https://user-gold-cdn.xitu.io/2018/6/4/163ca130d94ec11d?w=962&h=410&f=png&s=37362)

6、点击inspect弹出chrome调试工具，然后就可以在电脑上调试真机了，如图2.2.5

![](https://user-gold-cdn.xitu.io/2018/6/4/163ca1333287ce08?w=800&h=340&f=png&s=91671)

**2.3 注意事项**

在上面第6步的时候，点击inspect后，弹出的面板可能是一片空白，这是因为，首次使用该功能时，需要连接外网（翻墙），初始化后，成功显示了调试工具的面板后，以后就不需要翻墙了。

#### 3、iPhone手机 + Safari浏览器

**3.1 有什么用？**

如果模拟器没有问题，iPhone手机上运行时出现了问题，首先使用iPhone自带的Safari浏览器查看一下网页，如果浏览器中出现了同样的问题，则建议配合Mac上的Safari进行调试，找出问题所在。

**3.2 如何使用**

你需要有：一部iPhone，一台Mac，一根iPhone数据线

**操作步骤：**

1、打开手机上的Safari调试，具体步骤为，设置->Safari->高级->web检查器（打开），如图3.2.1

![](https://user-gold-cdn.xitu.io/2018/6/4/163ca13782e66c46?w=375&h=667&f=png&s=52956)

2、打开Safari，并打开需要调试的网页，如图3.2.2

![](https://user-gold-cdn.xitu.io/2018/6/4/163ca139d4b75522?w=375&h=667&f=png&s=261649)

3、打开Mac上的Safari，选择开发->账户名-右侧需要测试的网页URl，如图3.2.3

![](https://user-gold-cdn.xitu.io/2018/6/4/163ca13f288b06bc?w=2642&h=1446&f=jpeg&s=460609)

4、利用检查器进行调试，如图3.2.4

![](https://user-gold-cdn.xitu.io/2018/6/4/163ca147b55cd8c5)

#### 4、微信内置浏览器调试

**4.1 有什么用**

使用微信团队提供的微信调试工具，可以调试在微信中访问的页面。

**4.2 如何使用**

**操作步骤：**

1、首先，下载微信调试工具，并安装。[微信调试工具下载](http://dldir1.qq.com/WechatWebDev/release/0.7.0/wechat_web_devtools_0.7.0_x64.exe)
2、使用USB线，将手机与电脑连接，扫描二维码，勾选 信息->TBS setting->是否打开TBS内核inspector调试功能。点击“提交” 如图4.2.1、4.2.2

![](https://user-gold-cdn.xitu.io/2018/6/4/163ca14d706b47d4?w=145&h=140&f=png&s=4319)

![](https://user-gold-cdn.xitu.io/2018/6/4/163ca150e91f632b?w=800&h=381&f=png&s=64769)

3、使用微信，打开网页，之后点击“开始调试”（如图4.2.3），弹出如图4.2.4的调试列表。点击需要调试的页面下方的inspect进行调试，弹出调试工具，如图4.2.5

![](https://user-gold-cdn.xitu.io/2018/6/4/163ca158f97bcea0?w=292&h=136&f=png&s=3160)
图4.2.3

![](https://user-gold-cdn.xitu.io/2018/6/4/163ca15c5005833b?w=454&h=243&f=png&s=20895)
图4.2.4

![](https://user-gold-cdn.xitu.io/2018/6/4/163ca15e2a5a9d12?w=640&h=640&f=png&s=113966)
图4.2.5

#### 5、使用weinre调试

**5.1 有什么用**

如果上述所说的所有浏览器均没有出问题，但是偏偏有些浏览器下，自己的网页发生了问题，可是这个浏览器又没有解决方案的话。我们的秘密武器weinre就要登场了。

**它可以调试所有浏览器。其原理是在要调试的页面上加上一段js，再由这段js，支持电脑与手机的调试与调用。由于weinre的原理是注入js，微信等内置浏览器也可以使用weinre进行调试。**

**5.2 如何使用**

如果是一个人调试的话，可以在自己的机器上使用个人的解决方案。

**操作步骤**

1、在自己的电脑上使用npm（或cnpm）安装weinre，安装命令及结果如图5.2.1所示

![](https://user-gold-cdn.xitu.io/2018/6/4/163ca16d75d7b622?w=939&h=495&f=png&s=61049)

2、启动weinre服务，绑定到localhost，端口可以自己选一个，不要与其他服务端口重启就行，如图5.2.2所示，开启8081端口

![](https://user-gold-cdn.xitu.io/2018/6/4/163ca170b780395f?w=802&h=104&f=png&s=8146)

3、按照提示打开 [http://localhost:8081](http://localhost:8081) ，发现服务已经启动了，如图5.2.3所示

![](https://user-gold-cdn.xitu.io/2018/6/4/163ca17455876018?w=1281&h=977&f=png&s=86115)

4、将生成的js，引入自己将要调试的页面中去，如图5.2.4所示，生成的js在图5.2.3中箭头标识

![](https://user-gold-cdn.xitu.io/2018/6/4/163ca177a82c6f7e?w=1157&h=388&f=png&s=48508)

5、然后使用任意手机端浏览器打开这个页面，进行调试，如图5.2.5所示

![](https://user-gold-cdn.xitu.io/2018/6/4/163ca17ab38f8635?w=419&h=768&f=png&s=19302)

6、在http://localhost:8081上，点击第一个连接，进入调试页面，如图5.2.6所示

![](https://user-gold-cdn.xitu.io/2018/6/4/163ca17c5ab48840?w=1103&h=702&f=png&s=60190)

7、在调试页面中，发现有一个客户端连接了本weinre服务，如图5.2.7，点击上方最新连接的客户端，然后点击element进行调试，如图5.2.8所示

![](https://user-gold-cdn.xitu.io/2018/6/4/163ca17e56fac698?w=854&h=488&f=png&s=44076)
图5.2.7

![](https://user-gold-cdn.xitu.io/2018/6/4/163ca18051c9feee?w=804&h=277&f=png&s=28132)
图5.2.8

8、团队调试
如果希望搭建一个服务，团队公用的话，也是可以的，只需要找一台服务器，在其上运行weinre，并让所有团队成员，调试时，均引用这台服务器上生成的js，调试页面是可以选择调试哪个接入的手机的，如图5.2.9，只要团队成员，调试的时候，自己选择自己的访问就可以了。

![](https://user-gold-cdn.xitu.io/2018/6/4/163ca182f1040bff?w=830&h=42&f=png&s=6588)

#### 6、使用spy-debugger方法调试（[github介绍](https://github.com/wuchangming/spy-debugger)）

**6.1 介绍及特性**

**1、介绍**

（1）站式页面调试、抓包工具。远程调试任何手机浏览器页面，任何手机移动端webview（如：微信，HybirdApp等）。支持HTTP/HTTPS，无需USB连接设备。
（2）spy-debugger原理是集成了weinre，简化了weinre需要给每个调试的页面添加js代码。spy-debugger原理是拦截所有html页面请求注入weinre所需要的js代码。让页面调试更加方便。

**2、特性**

（1）页面调试＋抓包
（2）操作简单，无需USB连接设备
（3）支持HTTPS。
（4）spy-debugger内部集成了weinre、node-mitmproxy、AnyProxy。
（5）自动忽略原生App发起的https请求，只拦截webview发起的https请求。对使用了SSL pinning技术的原生App不造成任何影响。
（6）可以配合其它代理工具一起使用(默认使用AnyProxy) (设置外部代理)

**6.2 使用步骤**

1、安装插件
window下：
``` javascript
npm install spy-debugger -g
```
Mac下：
```javascript
sudo npm install spy-debugger -g
```
2、使手机和PC保持在同一网络下（比如同时连在一个WiFi下）；
3、打开cmd，输入spy-debugger，按命令行提示用浏览器打开相应地址；
4、设置手机的HTTP代理，代理IP地址设置为PC端的IP地址，端口为spy-debugger的启动端口（默认端口：9888），如下图所示；

![](https://user-gold-cdn.xitu.io/2018/6/4/163ca18b8d938751?w=735&h=161&f=png&s=16491)

（1）Android设置代理步骤：
>设置 -> WLAN -> 长按选中网络 -> 修改网络 -> 高级 -> 代理设置 - 手动

（2）IOS设置代理步骤：
>设置 -> 无线局域网 -> 选中网络 -> HTTP代理 -> 手动

5、手机安装证书。注：手机必须先设置完代理后再通过（非微信）手机浏览器访问 http://s.xxx（可直接扫码访问，如图6.2.2）安装证书（手机首次调试需要安装证书，已安装了证书的手机无需重复安装）。[问题：IOS10.3.1以上版本证书安装问题](https://github.com/wuchangming/spy-debugger/issues/42)；

6、用手机浏览器访问你要调试的页面即可

**6.3 自定义选项**

（1）端口设置（默认端口为9888）：
```bash
spy-debugger -p 8888
```
（2）设置外部代理（默认使用AnyProxy）：
```bash
spy-debugger -e http://127.0.0.1:8888
```
spy-debugger内置AnyProxy提供抓包功能，但是也可通过设置外部代理和其它抓包代理工具一起使用，如：Charles、Fiddler。

（3）设置内容页面为可编辑模式（默认false）
```bash
spy-debugger -w true
```
内部使用原理：在需要调试的页面内注入代码：document.body.contentEditable = true；暂不支持使用了iscroll框架的页面。

（4）是否允许weinre监控iframe加载的页面（默认false）
```bash
spy-debugger -i true
```
（5）是否只拦截浏览器发起的https请求（默认true）
```bash
spy-debugger -b false
```
有些浏览器发出的connect请求没有正确的携带userAgent，这个判断有时候会出错，如UC浏览器。这个时候需要设置为false。大多数情况建议启用默认配置：true，由于目前大量App应用自身（非WebView）发出的请求会使用到SSL pinning技术，自定义的证书将不能通过app的证书校验。

（6）是否允许HTTP缓存（默认false）
```bash
spy-debugger -c true
```