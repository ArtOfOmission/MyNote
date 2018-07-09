# HTML5新特性
## 1. H5现在已经不是SGML的子集
1.1 绘画canvas
1.2 用于媒介回放的video和audio元素
1.3 本地离线存储localStorage，长期保存数据，浏览器关闭后数据不丢失
1.4 sessionStorage的数据在浏览器关闭后自动删除
1.5 语义化更好的元素
1.6 比如artical、footer、 header、nav、section
1.7 表单控件，calender、date、time、email、url、search
1.8 新的技术webworker、websocket、Geolocation

## 2. 移除的元素
2.1 纯表现的元素：basefont，big，center，font, s，strike
2.2 对可用性产生负面影响的元素：frame，frameset，noframes


## 3. 支持HTML5新标签
3.1 IE8/IE7/IE6支持通过document.createElement方法产生的标签
3.2 可以利用这一特性让这些浏览器支持HTML5新标签
3.3 浏览器支持新标签后，还需要添加标签默认的样式

## 4. 当然也可以直接使用成熟的框架、比如html5shim