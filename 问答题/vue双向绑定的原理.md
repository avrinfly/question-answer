<!--
 * @Description: 对于vue双向绑定原理的答案
 * @Author: hetengfei
 * @Github: https://github.com/avrinfly
 * @Date: 2019-08-17 20:53:08
 * @LastEditors: hetengfei
 * @LastEditTime: 2019-08-17 20:53:34
 -->
回答：vue是采用数据劫持结合发布-订阅者模式的方法 通过object.defineProperty()来劫持各个属性的setter、getter，在数据变动时发布消息给订阅者，触发相应的监听回调

**具体谈一谈：**

1. observe对数据对象进行递归遍历，包括子属性对象的属性，都加上setter和getter。如果对该对象的某个值赋值，就会触发setter，就能监听到数据变化（DOM diff算法来进行递归遍历）
2. compile解析模板指令，将模板中的变量替换成数据，然后初始化渲染页面视图，并将每个指令对应的节点绑定更新函数，添加监听数据的订阅者，一旦数据有变动，收到通知，更新视图。
3. Watcher订阅者是Observe和compile的桥梁，自身有一个update方法，当属性变动时，调用自身的update方法，并触发compile中绑定的回调
4. 简而言之：MVVM模式整合Observe、Compile和Watcher三者，通过compile解析编译模板指令，最终利用Watcher搭起Observe和Compile之间的通信桥梁，达到数据变化->视图更新；视图更新->数据model变更的双向绑定效果。