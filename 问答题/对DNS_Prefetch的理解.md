<!--
 * @Description: 对DNS_Prefetch的理解
 * @Author: hetengfei
 * @Github: https://github.com/avrinfly
 * @Date: 2019-08-17 20:53:37
 * @LastEditors: hetengfei
 * @LastEditTime: 2019-08-17 20:53:58
 -->
即DNS预获取，属于前端优化的一部分。

一般来说，在前端优化中与NDS有关的有两点：
1. 减少DNS的请求次数
2. 进行DNS预获取

典型的一次DNS解析需要耗费20-120毫秒，减少DNS解析时间和次数是个很好的优化方式。
DNS Prefetching是让具有此属性的域名不需要用户点击链接就在后台解析，而域名解析和内容载入是串行的网络操作，所以该方式能减少用户等待时间，提升用户体验。