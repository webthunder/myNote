你不知道的HTML
======================================

###用图片进行网速测试和数据上传


![](https://i.imgur.com/ddd0U3B.jpg)
通过服务器自动分析access日志，就可以得出结果
疑问：为什么不用AJAX统计？
解答：AJAX并发有限制，很多浏览器限制5个并发，而且成本比较高

navigator.sendBeacon() 方法可用于通过HTTP将少量数据异步传输到Web服务器。


###关于window.requsestAnimationFrame()方法

浏览器中动画有两种实现形式：通过申明元素实现（如SVG中的元素）和脚本实现。

可以通过setTimeout和setInterval方法来在脚本中实现动画，但是这样效果可能不够流畅，且会占用额外的资源。可参考《Html5 Canvas核心技术》中的论述：

它们有如下的特征：

> 1.即使向其传递毫秒为单位的参数，它们也不能达到ms的准确性。这是因为javascript是单线程的，可能会发生阻塞。

> 2、没有对调用动画的循环机制进行优化。

> 3、没有考虑到绘制动画的最佳时机，只是一味地以某个大致的事件间隔来调用循环。

其实，使用setInterval或setTimeout来实现主循环，根本错误就在于它们抽象等级不符合要求。我们想让浏览器执行的是一套可以控制各种细节的api，实现如“最优帧速率”、“选择绘制下一帧的最佳时机”等功能。但是如果使用它们的话，这些具体的细节就必须由开发者自己来完成。

requestAnimationFrame不需要使用者指定循环间隔时间，浏览器会基于当前页面是否可见、CPU的负荷情况等来自行决定最佳的帧速率，从而更合理地使用CPU


###CSS远程攻击漏洞

####XSS（跨站脚本攻击）
跨站脚本攻击(Cross Site Scripting)，为了不和层叠样式表(Cascading Style Sheets, CSS)的缩写混淆，故将跨站脚本攻击缩写为XSS。恶意攻击者往Web页面里插入恶意Script代码，当用户浏览该页之时，嵌入其中Web里面的Script代码会被执行，从而达到恶意攻击用户的目的。

####XSS的攻击方式
> （1）反射型： 发出请求时，XSS代码出现在URL中，作为输入提交到服务器端，服务器端解析后响应，XSS随响应内容一起返回给浏览器，最后浏览器解析执行XSS代码，这个过程就像一次发射，所以叫反射型XSS。

> （2）存储型: 存储型XSS和反射型的XSS差别就在于，存储型的XSS提交的代码会存储在服务器端（数据库，内存，文件系统等），下次请求目标页面时不用再提交XSS代码。

####XSS的防御措施

> （1）编码：对用户输入的数据进行HTML Entity编码 

> （2）过滤：移除用户上传的DOM属性，如onerror等，移除用户上传的style节点，script节点，iframe节点等。

> （3）校正：避免直接对HTML Entity编码，使用DOM Prase转换，校正不配对的DOM标签。

![](https://i.imgur.com/UAb1t5I.jpg)

例如以上的方式就属于XSS


###关于div和性能
> GPU负责渲染，CPU负责运算
> 
> 因为DOM包含很多方法，所以减少DIV的数量可以提升性能
> 
> 可以使用伪类来实现DIV的效果，1个DIV当十个用




