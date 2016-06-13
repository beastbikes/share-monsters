在js中，window表示全局作用域，是一个很重要的对象，但是因为可以省略不写，例如`alert('test')`等同于`window.alert('test')`,所以经常被忽略。
下面介绍一下window对象下的一些主要的对象与方法。未特殊提及的表示各个浏览器兼容良好，IE不在考虑范围之内。

###对象
---
1. `window.innerWidth` & `window.innerHeight`
这两个对象是只读的，表示窗口内可用于显示页面的宽度与高度。
![innerWidth与innerHeight的范围](http://upload-images.jianshu.io/upload_images/1748822-72c6728a34e7927e.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

2. `window.outerWidth` & `window.outerHeight`
这两个对象是只读的，表示浏览器窗口大小，包括标签栏、地址栏、工具栏、滚动条、状态栏等部分。
![outerWidth与outerHeight的范围](http://upload-images.jianshu.io/upload_images/1748822-ca97ed810491103d.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

3. `window.screenX` & `window.screenY`
`window.screenLeft` & `window.screenTop`(FF不支持)
上面这两组对象都是只读的，表示浏览器窗口的左上角到屏幕左上角之间的距离，目前我知道的区别是浏览器兼容性。
![screenX与screenY的值](http://upload-images.jianshu.io/upload_images/1748822-239a0b18a54f5acd.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

4. `window.pageXOffset` & `window.pageYOffset`
`window.scrollX` & `window.scrollY`
这两组对象是等价的并且都是只读的，表示页面内容滚动的距离。
`window.pageXOffset == window.scrollX; // always true`
![显示窗口外，已滚动的部分](http://upload-images.jianshu.io/upload_images/1748822-f2a10df50837e832.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

5. `window.history`
`history`表示浏览器的浏览记录，可以理解为一个栈。每一次url的变化（包括跳转或者通过锚点跳转）就是一次入栈，后退可以理解为出栈，不过这边的出栈并不是记录就没了，而是保存在栈外的某一个地方，因此还可以前进，不过如果有一次新的入栈，则栈外的纪录丢失。
[出于安全方面的考虑，浏览记录是不允许被代码读取到具体的url的，只能通过索引index在记录之间跳转。](https://developer.mozilla.org/en-US/docs/Web/API/Window/history)
`history`提供了一个属性与三个方法:
 - length //栈的大小，只读
 - back()  //相当于浏览器的后退
 - forward() //相当于浏览器的前进
 - go() //跳转到栈中的相对于当前的位置，参数为-1、1之类正负整数，如果数字超出范围，则方法无效

6. `window.screen`
`screen`是一个只读参数，存储着一些关于显示器的数据。
 - width & height // 屏幕的宽 & 高度
 - availWidth & availHeight //屏幕的有效宽&高度（以windows系统为例，为扣除了任务栏的部分）

7. `window.location`
`location`对象中存储关于当前URL的相关信息。
 - href //完整的URL, 可读写，赋值后跳转
 - origin //协议+端口＋域名，只读
 - protocol //协议，只读
 - host //当前端口与域名，只读
 - port //端口，只读
 - hostname //域名，只读
 - pathname //当前页面的路径,只读，例：/newspaper/today.html
 - hash //URL中的锚信息，可读写
 - search //参数（包含?），只读
 - reload() //等同于刷新，参数为true时为强制刷新（刷新缓存）
 - assign() //参数为url地址，表示跳转到制定url
 - replace() //与assign用法一样，区别是新页面不会入栈，而是取代当前页面在栈里的位置，无法通过后退按钮回到原页面

8. `window.document`
`document`对象应该是最常用的对象之一，表示当前页面的HTML文档，可以用来访问页面内的元素，属性与方法有下。
部分通用属性与方法具体会在**JS对象之Element**(还没写)一章中提及。
 - head //表示`<head>`，可以进行DOM操作
 - title //表示`<title>`的文本内容，可读写
 - body //表示`<body>`，可以进行DOM操作
 - cookie //页面的cookie, 可读写
 - inputEncoding //返回页面编码的字符集
 - activeElement() //返回当前focus的元素，默认为body
 - createElement() //创建一个元素，参数为标签名
 - createTextNode() //创建一个文本节点，参数为文本内容
 - getElementById() //通过Id获取一个元素
 - getElementsByClassName() //通过class获取一群元素
 - getElementsByName() //通过name属性获取一群元素
 - getElementsByTagName() //通过标签名获取一群元素

9. `window.navigator`
`navigator`对象原来是用来存放一些浏览器相关的信息，例如`navigator.userAgent`，后来又添加的许多属性与对象进来，`navigator.connection`（网络连接状态）、`navigator.battery`（电池信息）、`navigator.geolocation`（定位信息），但是许多新特性都还未成为w3c标准，兼容性并不好（后续补充）。
 - userAgent //存放浏览器信息


###方法
---
1. `window.alert()`
`alert()`提示框，这个没啥好介绍的

2. `window.setTimeout()`
`setTimeout()`是一个定时器方法，作用是在一定时间(毫秒)后执行相关代码，return 一个id表示当前定时器。
eg1: `setTimeout(function(){alert(1)}, 5000)`//5000毫秒后执行alert(1)
eg2: `setTimeout('alert(1)', 5000)`

3. `window.clearTimeout()`
`clearTimeout()`的作用是取消定时器。
eg: 
```
var t = setTimeout(function(){alert(1)}, 5000);
clearTimeout(t);
```

4. `window.setInterval()`
`setInterval()`可以理解为一个循环定时器(setTimeout)，它会按照设定时间段循环执行代码，用法与setTimeout类似。
eg: `setTimeout(function(){alert(1)}, 5000)` //每5000毫秒alert(1)

5. `window.clearInterval()`
`clearInterval()`与`clearTimeout()`效果类似，用于取消`setInterval()`
eg: 
```
var t = setInterval(function(){alert(1)}, 5000);
clearInterval(t);
```

6. `window.open()`
`open`方法用来打开一个窗口，参数有四个，都是可选的。
第一个参数：url  //字符串，窗口打开的页面
第二个参数：name  //字符串，目前不知道干啥用的
第三个参数：features //字符串，窗口的一些参数，逗号隔开
第四个参数：replace //bool, 表示新开窗口是否存入历史纪录
eg:`window.open('https://www.baidu.com/','','width=200,height=200');`
features可选值：
 - channelmode=yes|no|1|0   //是否使用剧院模式显示窗口。默认为 no。
 - directories=yes|no|1|0	 //是否添加目录按钮。默认为 yes。
 - fullscreen=yes|no|1|0	 //是否使用全屏模式显示浏览器。默认是 no。处于全屏模式的窗口必须同时处于剧院模式。
 - height=pixels	 //窗口文档显示区的高度。以像素计。
 - left=pixels	 //窗口的 x 坐标。以像素计。
 - location=yes|no|1|0	 //是否显示地址字段。默认是 yes。
 - menubar=yes|no|1|0	 //是否显示菜单栏。默认是 yes。
 - resizable=yes|no|1|0	 //窗口是否可调节尺寸。默认是 yes。
 - scrollbars=yes|no|1|0	 //是否显示滚动条。默认是 yes。
 - status=yes|no|1|0	 //是否添加状态栏。默认是 yes。
 - titlebar=yes|no|1|0	 //是否显示标题栏。默认是 yes。
 - toolbar=yes|no|1|0	 //是否显示浏览器的工具栏。默认是 yes。
 - top=pixels	 //窗口的 y 坐标。
 - width=pixels  //窗口的文档显示区的宽度。以像素计。
7. `window.close()`
`close()`用来关闭`open()`窗口。
eg:
```
var w = window.open('https://www.baidu.com/','','width=200,height=200');
w.close();
```

目前整理如上，当然不止这些。少的一部分是未成为标准，兼容性不好的，另一部分是我觉得不是那么重要的，还有一部分是我不知道的。huan ying
