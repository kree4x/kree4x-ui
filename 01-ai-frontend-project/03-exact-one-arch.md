# 同一架构：AI动态生成是基底，预定义是瞬间快照

> Created By [RV](mailto:rodney.vin@gmail.com), and licensed with Creative Commons "[CC BY-NC-ND 4.0](https://creativecommons.org/licenses/by-nc-nd/4.0/)"

当前基于Catalog的AI动态生成式UI，单纯从技术层面来看，毫无新意。

本质来看，其不过是传统的WinForm技术方案的一个变种：

- Component：一个组件库，定义可组合的UI元素全集
- Layout：使用某种语法，描述页面静态布局
- Event：为按钮等UI元件，定义响应事件
- Data Binding：使用数据驱动UI更新

重大的创新，实际只有AI——AI Native与AI驱动。

从架构层面来看，AI的引入，现实中带来的是一场前端的颠覆性革命。

- 传统的WinForm路线，是人类在开发期拖曳摆放、手动定义、编译后固定发行。
- AI动态生成的本质，是将上述过程在运行时自动化、智能化

这种变革，本质是一种框架、方法不变，引入AI后，速度极致提升，以致支持实时生成，从而量变引发质变的过程。

当然，这种说法，是一种断言式的暴论，只是一种忽略细节，直击本质的化繁为简。

在实际的工程层面，两者的差异，类似于现代坦克与古代骑兵的差异。非要说坦克就是现代化的骑兵，它不错，但不准确。

### 当前前端

在[两种交付：预置式UI与生成式UI的二元困境](https://zhuanlan.zhihu.com/p/2061466214581416097)中我们展开讨论过前端预置式UI与生成式UI的问题。

预置式UI方面，当前现实中，我们讲到前端时，它基本是React、Vue、Angular之类重型框架的代名词。当然还存在SDUI之类的一些小众、边缘的技术选择。

一方面，React、Vue、Angular基本是前端面向人类编程、工程化、体系化的极致，另一方面，伴随它们所带来的争论从未停息。

**现代前端的复杂性：本质还是偶然？**

参见 2026-04-18：[Modern Frontend Complexity: essential or accidental?](https://binaryigor.com/modern-frontend-complexity.html)

及其在Hacker News引发的讨论：[Modern Front end Complexity: essential or accidental?](https://news.ycombinator.com/item?id=47824051)

以及Redis之父Antirez，在这场争论中所持的立场：“***The web is terrible now.***”

**不要选边**

去趟争论的浑水，毫无意义。

你的应用场景，需要什么，什么合适，就采用什么。

我们面对的场景是：**面对AI编程，需要一个AI Native的前端架构。**

在这个场景约束下，我们其实真的不需要选边，因为两边都可抛弃：不论是Modern的极端工程化，还是极致简单化的HTMX，都不是AI Coding的合适之选。

**任何编译型的方案都不适合AI动态生成UI**

这个道理，很浅显。

如果AI生成后，需要编译，才能部署到前端，那它天生就是不适用于AI生成的。

**纯声明式的HTMX也不适合AI动态生成UI**

这个道理，也很浅显。

不论是HTML还是HTMX，这是渲染，这是在要求AI去执行How，而不是去声明What。

### 动态生成：A2UI为代表的AI实时生成

**Agent-2-Agent** 这一系列协议，代表了Google在AI时代，搭建完整AI Native生态的野望之心。

A2UI本身并不复杂，去除A2A部分后，仅与UI相关的部分更为精简。

本质上，它就是开篇我们所言的：一个现代化的WinForm方案。

- Catalog划定AI的能力范围，提供组件库
- 扁平邻接表，提供了描述UI布局的语法
- Function Call，定义了组件内可调用的响应事件
- Data Binding，使用JSON Pointer定义数据与组件属性的映射关系
- Render，提供跨平台的前端渲染能力
- 流式消息，提供了使用数据驱动前端UI增量更新的能力

整个方案，声明式的描述What，而不是编程式的定义How。整个架构，干净、纯粹、轻量、职责分离。

很好！确实，极好！

“***The web is terrible now.***”，其所有罪魁全部消失。

BTW：

- 前端Render，最佳实践是使用Lit，实质是原生Web Component。
- 前端无（重型）框架，曙光可见。

### 预置式UI：开发期引入AI，基于同一个技术架构生成

如果，您的应用中，涉及到AI的部分，您采用了类似A2UI的生成式方案，那么一个问题就会自然复现：

**在预置式UI部分，我们可以采取同一个技术方案么？**

为什么不呢？

工程上，我们看不到任何的障碍。

- 为AI提供设计图稿，AI基于多模态能力，识别为扁平邻接表
- 识别结果，保存为预置的JSON
- 系统启动时，发送一个预置的JSON，则前端渲染一个完整的UI界面

如此：

- 预置式UI就仅仅是生成式UI在时间维度上的一个瞬时快照。
- 人类工程师，可以对这个瞬间快照进行微调。
- 运行时，实际所有UI都是动态生成，任何页面AI都可实时调整

技术同源，架构同一，运行同态。

完美。

当然，工程上会有很多的细节需要处理。

这就是后续一众轻量的AI Native UI框架要解决的细节技术问题了：

- 框架提供运行时支持
- 提供工具，支持可视化编辑AI生成的UI描述数据文件
- 新的打包、构建、发行工具
- ……
