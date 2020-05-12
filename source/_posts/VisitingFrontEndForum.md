---
title: 我看前端技术交流论坛
date: 2018-05-15 00:00:00
---
上周六去苏宁总部参加了前端技术交流论坛，有关于Node.js、React16、WebRTC等方面的内容，在此记录一下自己感兴趣的主题。
### Node.js项目优化
项目中使用了ejs模版引擎，为了提升TPS，根据Chome Devtools-JavaScript CPU Profile查找渲染html时的瓶颈，发现问题根源在ejs模版引擎内部，通过修改ejs源码，实现了较大的提升。（现场提问环节有人提出另一种解决ejs的include指令消耗性能的方案，即用webpack预处理把include指令的相对路径处理为绝对路径）
项目中有大量静态路由（即固定的字符串的路由表达式），原来是express框架默认采用正则表达式逐条匹配，为了提升路由匹配效率，使用HashMap把这些固定字符串通过键值对映射进行匹配，将匹配时间从O(n)降低到O(1)。
### React16新特性
司徒正美概括了React的优化思路，由于神奇的口音，聆听时需要很费力地理解他在表达什么，不过说的内容还是很有干货的。
- React15 减少变化
    - 单向数据流
    - 分离可变的state与不可变的props
    - 虚拟DOM做缓冲
    - 单层比较，相类比较，key
    - SCU

- 迷你React 减少移动
    - 双向同时比较
    - 最短编辑距离，最长公共序列，最长上升序列
- React16 限量更新 异步渲染
    - requestIdleback：闲时更新，时间分片
    - DFS遍历，每次只展开一层
    - batchedUpdates：合并更新

### Web Component、WebRTC
Web Components用于在web应用中创建可重用的定制元素，目前浏览器的支持还比较有限，应用范围也不广。
WebRTC是由Google主导的实现视频实时通讯的标准，目前Chrome、Firefox、Opera等浏览器均已支持，并被各大厂商广泛使用。