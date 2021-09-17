# 事件循环系统

## 参考资料

- [WHATWG](https://html.spec.whatwg.org)
- [ECMA262](https://tc39.es/ecma262)
- [RFC](https://zh.wikipedia.org/wiki/RFC)

## PPT

1. 示例展示
2. WHATWG 标准
3. task（macrotask）- 宏任务
4. microtask - 微任务
5. Event loops - 事件循环
   1. Definitions - 定义
   2. Processing model - 处理模型
   3. Generic task sources - 通用的任务源
6. setTimeout
7. XMLHttpRequest
8. Promise
9. async/await

### 示例展示

start.html

### WHATWG 标准

1. WHATWG 是什么
   WHATWG（Web Hypertext Application Technology Working Group）即网页超文本应用技术工作小组，是一个以推动网络`HTML5`标准为目的而成立的组织。在 2004 年，由 Opera、Mozilla 基金会和苹果这些浏览器厂商组成。WHATWG 成立的原因是 W3C 意图放弃 HTML，而力图发展 XML（可扩展标记记语言下的一个子集）技术。WHATWG 邮件列表公布于 2004 年 6 月 4 日，否决了由 W3C 成员在 W3C 工作室的 Web 标准，组织中浏览器厂商建议 W3C 跟随 WHATWG 的 HTML5，将新的 HTML（标准通用标记语言下的一个应用）命名为 HTML5，后来 W ３ C 采纳了他们的建议。比如：Event loops、The elements of HTML、Web workers
2. ECMAScript 是什么
   ECMAScript 是一种由 Ecma 国际（前身为欧洲计算机制造商协会）在标准 ECMA-262 中定义的脚本语言规范。这种语言在万维网上应用广泛，它往往被称为 JavaScript 或 JScript，但实际上后两者是 ECMA-262 标准的实现和扩展。比如：Data Types and Values、Functions and Classes、IsLooselyEqual(x, y)
3. RFC 是什么
   RFC 文档也称请求注解文档（Requests for Comments，RFC），这是用于发布 Internet 标准和 Internet 其他正式出版物的一种网络文件或工作报告，内容和 Internet 相关。草案讨论了计算机通讯的方方面面，重点在网络协议、过程、程序，以及一些会议注解、意见、风格方面的概念。一个 RFC 文件在成为官方标准前一般至少要经历三个阶段：建议标准、草案标准、因特网标准。在 Internet 上，任何一个用户都可以对 Internet 某一领域的问题提出自己的解决方案或规范，作为 Internet 草案提交给 Internet 工程任务组（IETF）。草案存放在美国、欧洲和亚太地区的工作文件站点上，供世界多国自愿参加的 IETF 成员进行讨论、测试和审查。最后，由 Internet 工程指导组确定该草案是否能成为 Internet 的标准。RFC 文档必须被分配 RFC 编号后才能在网络上发布。例如，RFC2026 的内容是“Internet 标准进程-修订版 3”、RFC1543 的内容为“RFC 作者指导”等等。比如：UDP、TCP、HTTP/1.1、HTTP/2

### task（macrotask）- 宏任务

task 也被称为 macrotask，task 队列还是比较好理解的，就是一个先进先出的队列，由指定的任务源去提供任务。

1. 一个 event loop 有一个或者多个 task 队列。
2. 当用户代理安排一个任务，必须将该任务增加到相应的 event loop 的一个 task 队列中。
3. 每一个 task 都来源于指定的任务源，比如可以为鼠标、键盘事件提供一个 task 队列，其他事件又是一个单独的队列。

task 任务源非常宽泛，比如 ajax 的 onload，click 事件，基本上我们经常绑定的各种事件都是 task 任务源，还有数据库操作（IndexedDB），需要注意的是 setTimeout、setInterval、setImmediate 也是 task 任务源。总结来说 task 任务源：

- setTimeout
- setInterval
- setImmediate(Node.js)
- I/O
- UI rendering

### microtask - 微任务

每一个 event loop 都有一个 microtask 队列

HTML Standard 没有具体指明哪些是 microtask 任务源，通常认为是 microtask 任务源有：

- process.nextTick
- promise
- Object.observe
- MutationObserver
