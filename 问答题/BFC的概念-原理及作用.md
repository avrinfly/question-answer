<!--
 * @Description: BFC的概念、原理及作用
 * @Author: hetengfei
 * @Github: https://github.com/avrinfly
 * @Date: 2019-08-17 23:39:53
 * @LastEditors: hetengfei
 * @LastEditTime: 2019-08-17 23:40:51
 -->
1. 什么是bfc？
   1. BFC(block formatting context)直译为“块级格式化上下文”。它是一个独立的渲染区域，只有block-level box(块元素)参与，它规定了内部的块元素如何布局，切与外部毫不相干。
    2. 可理解为创建了BFC的元素就是一个独立的盒子，里边的子元素不会影响到外部，**仍属于文档中的普通流**。
    3. 也不是所有的元素、模式都能产生BFC，w3c规范：display属性为block，list-item，table的元素会产生bfc。
2. bfc的原理是什么？
    1. 内部的box会在垂直方向，一个接一个地放置。
    2. Box垂直方向的距离由margin决定。属于同一个BFC的两个相邻Box的margin会发生**重叠**。
    3. 每个元素的margin box的左边与包含块border box的左边相接触(对于从左向右，否则相反)。即使存在浮动也如此
    4. BFC区域不会与float元素重叠。
    5. 计算BFC高度时，浮动元素也参与计算
3. 如何创建BFC？
    1. 根元素
    2. float属性不为none
    3. position不为static和relative
    4. overflow不为hidden
    5. display为inline-block，table-cell，table-caption，flex
4. bfc的作用是什么？
    1. 防止外边距重叠。
    bfc导致同属于一个bfc的子元素的margin会重叠（元素垂直方向的距离由margin决定。属于同一个BFC的两个相邻元素的margin会发生重叠）
    2. 清除浮动的影响
    块级子元素浮动，如果块级的父元素未设置高度，会出现高度塌陷的情况。  
    原因是：**子元素浮动后均开启了BFC，父元素不会被子元素撑开**
    
    解决方法：由原理中的第五条可知，浮动元素也参与计算。故只要将父容器设置为bfc就可以把子元素也包含进去；这个容器将包含浮动的子元素，高度也将扩展到可以包含它的子元素，在这个bfc里，这些元素将会回到页面的正常文档流
    3. 防止文字环绕