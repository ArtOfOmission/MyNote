# display: none;与visibility: hidden;的区别

- 联系:都能让元素不可见
- 区别
    - display: none;会让元素完全从DOM树中消失,渲染的时候完全不占据任何空间<br> 
    visibility: hidden;不会让元素从渲染树消失,渲染时元素继续占据空间,只是内容不可见
    - display: none;是非继承属性，子孙节点消失由于元素从渲染树消失造成，通过修改子孙节点属性无法显示;<br>
    visibility: hidden;是继承属性,子孙节点消失由于继承了hidden,通过设置visibility: visible;可以让子孙节点显示
    - 修改常规流中元素的display通常会造成文档重排。修改visibility属性只会造成本元素的重绘。
    - 读屏器不会读取display: none;元素内容；会读取visibility: hidden;元素内容