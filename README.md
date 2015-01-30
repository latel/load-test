检测浏览器对于通过 JavaScript 动态加载的资源是否完成加载事件的支持情况
=============================

>  我们经常会使用 Javascript 在 Dom 中插入一些节点，  
>  出于各种各样的目的，有时会是一些外部资源，如 图片，脚本或样式表等等。  
>  我们需要对这些资源的加载完成事件做出监听以便后续操作。  
>
>  但是我们发现 IE6、IE7和IE8在动态引入 Javascript 文件时只支持 onreadystatechange事件，  
>  不支持 onload 和 attach onload 事件。  
>
>  因此在此做出一个小测试，以便彻底弄清楚各个浏览器的支持情况。
>  以便更新和维护自己编写的 Javascript AMD 模块加载器。

___测试样本：___

>  Chrome/40.0.2214.94  
>  Firefox/35.0  
>  Safari/7.1.3

##JS脚本加载测试情况

###Chrome

在script节点插入前，设置src不会预加载

- addEventListener load
- onload

###Safari
在script节点插入前，设置src不会预加载

- addEventListener load
- onload

###Firefox
在script节点插入前，设置src不会预加载

- addEventListener load
- onload

###IE6,IE7,IE8
在script节点插入前，设置src会预加载并触发响应的事件，且readyState=loaded,节点插入后才会变为comoplete

 - onreadystatechange

###IE9,IE10
在script节点插入前，设置src会预加载并触发响应的事件，且readyState=loaded,节点插入后才会变为comoplete

- onreadystatechange
- addEventListener load
- onload

###IE11
在script节点插入前，设置src会预加载并触发响应的事件

- addEventListener load
- onload


##样式表加载测试情况

###Chrome
在link节点插入前，设置href不会预加载

- addEventListener load
- onload

###Safari
在link节点插入前，设置href不会预加载

- addEventListener load
- onload

###Firefox
在link节点插入前，设置href不会预加载

- addEventListener load
- onload

###IE6,IE7,IE8
在link节点插入前，设置href不会预加载

- onreadystatechange, 直接跳到complete
- attachEvent onload
- onload

###IE9,IE10
在link节点插入前，设置href不会预加载

- addEventListener load
- onload

###IE11
在link节点插入前，设置href不会预加载

- addEventListener load
- onload


##图片加载测试情况

###Chrome
在img节点插入前，设置src会预加载，并触发响应的事件

- addEventListener load
- onload

###Safari
在script节点插入前，设置src不会预加载

- addEventListener load
- onload

###Firefox
在img节点插入前，设置src会预加载，并触发响应的事件

- addEventListener load
- onload

###IE6,IE7,IE8
在img节点插入前，设置src会预加载，并触发响应的事件,且readyState=complete

- onreadystatechange
- attachEvent load
- onload

###IE9,IE10
在img节点插入前，设置src会预加载，并触发响应的事件,且readyState=complete

- onreadystatechange
- addEventListener load
- onload

###IE11
在img节点插入前，设置src会预加载，并触发响应的事件  

- addEventListener load
- onload


##有益的结论

+ IE11趋向于同 Chrome、 Firefox 和 Safari 保持一致，样式表，js脚本和图片都会响应 onload 和 attachEventListener load
+ IE全系列都会预加载图片和js脚本资源，而 Chrome、Safari 和 Firefox 只会预加载图片资源
+ 除了IE678在加载js脚本时不响应onload方法外，其他浏览器都会响应样式表、js脚本和图片的onload事件。IE678对js脚本的处理是个例外。