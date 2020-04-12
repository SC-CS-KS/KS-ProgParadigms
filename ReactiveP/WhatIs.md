# What Is Reactive Programming ?
```md
是与异步数据流交互的编程范式
它的灵感来自于我们的日常生活，也即我们如何采取行动以及与他人沟通
我们在执行日常生活活动时，我们会尽可能多任务，但大脑无法处理多任务，不管我们如何努力去做。
我们人类实现多任务的唯一办法是在时间线上在任务之间切换。
	事实上，我们总是切换任务，即使我们没有意识到它。
例如
	要执行一个任务：在星巴克喝一杯咖啡饮料，你需要发出一个命令，等待它准备好，然后接受你的饮料。
	当你在等待的时候，你很可能会找到别的事情做。
		这是最简单的执行任务的反应(响应)形式，你会在你等待来自咖啡师的“响应”时做别的事情，当你的咖啡已经准备好后，会叫你的名字时。
```
```md
* 响应式编程是一种声明式编程范型。
* 响应式编程是一种非阻塞的异步编程。
* 响应式编程是一种数据流编程，关注于数据流而不是控制流。
  例如 当页面出现点击操作时产生一个click stream，然后页面会将250ms内的clickStream缓存，如此实现了一个归组过程。
  然后再进行map操作，得到每个list的长度，筛选出长度大于2的，这便可以得出多次点击操作的流。
  这种方法应用非常广泛，例如可以筛选出双击操作。
```
```md
编程的风格 非阻塞，异步，函数式
封装异步编程 提供一个优秀的异步处理框架，同时简化编写异步代码的流程，最终实现减少阻塞，提升性能的大目标。
```
* 异步事件流(asynchronous event stream)
```md
事件总线(Event Buses)或一些典型的点击事件本质上就是一个异步事件流
这样你就可以观察它的变化并使其做出一些反应(do some side effects)
```
## 传统编程模型中的某些困境
* Reactor 认为阻塞可能是浪费的
```md
阻塞导致性能瓶颈和浪费资源
增加线程可能会引起资源竞争和并发问题
并行的方式不是银弹（不能解决所有问题）
```
* Reactor 认为异步不一定能够救赎
```md
Callbacks 是解决非阻塞的方案，然而他们之间很难组合，并且快速地将代码引导至 "Callback Hell" 的不归路
Futures 相对于 Callbacks 好一点，不过还是无法组合，不过  CompletableFuture 能够提升这方面的不足
```
* Reactive Streams JVM 认为异步系统和资源消费需要特殊处理
```md
流式数据容量难以预判
异步编程复杂
数据源和消费端之间资源消费难以平衡
```
## Why
```md
响应式编程可以加深你代码抽象的程度
	让你可以更专注于定义与事件相互依赖的业务逻辑，而不是把大量精力放在实现细节上
使用响应式编程还能让你的代码变得更加简洁
特别对于现在流行的WebApps和mobile apps
	它们的 UI 事件与数据频繁地产生交互，在开发这些应用时使用响应式编程的优点将更加明显
	十年前，web页面的交互是通过提交一个很长的表单数据到后端，然后再做一些简单的前端渲染操作
	而现在的Apps则演变的更具有实时性
		仅仅修改一个单独的表单域就能自动的触发保存到后端的代码
		就像某个用户对一些内容点了赞，就能够实时反映到其他已连接的用户一样，等等。
```
## 特性
* Responsive 响应性：快速/一致的响应时间
```md
假设在有500个并发操作时，响应时间为1s，那么并发操作增长至5万时，响应时间也应控制在1s左右。
快速一致的响应时间才能给予用户信心，是系统设计的追求。
```
* Resilient 健壮性、韧性：复制/遏制/隔绝/委托
```md
当某个模块出现问题时，需要将这个问题控制在一定范围内，这便需要使用隔绝的技术，避免连锁性问题的发生。
或是将出现故障部分的任务委托给其他模块。
韧性主要是系统对错误的容忍。
```
* Elastic 弹性：无竞争点或中心瓶颈/分片/扩展
```md
如果没有状态的话，就进行水平扩展，如果存在状态，就使用分片技术，将数据分至不同的机器上。
```
* Message-driven 事件驱动性：异步/松耦合/隔绝/地址透明/错误作为消息/背压/无阻塞
```md
消息驱动是实现上述三项的技术支撑。

响应式中，错误也是一种消息，和普通消息地位一致，这和JavaScript中的Promise类似。

背压是指当上游向下游推送数据时，可能下游承受能力不足导致问题，一个经典的比喻是就像用消防水龙头解渴。
因此下游需要向上游声明每次只能接受大约多少量的数据，当接受完毕再次向上游申请数据传输。
这便转换成是下游向上游申请数据，而不是上游向下游推送数据。

无阻塞是通过no-blocking IO提供更高的多线程切换效率。
```

## [Reactive Programming vs. Reactive Systems](https://www.oreilly.com/ideas/reactive-programming-vs-reactive-systems)
```md
响应式是一组设计原则，一种关于系统架构与设计的思考方式，一种关于在一个分布式环境下，
当实现技术、工具和设计模式都只是一个更大系统的一部分时如何设计的思考方式。
```

### 响应式系统（架构与设计）
```md
响应式系统 是一种架构风格(architectural style)，它允许许多独立的应用结合在一起成为一个单元，
共同响应它们所处的环境，同时保留着对单元内其它应用的“感知”
—— 这能够表现为它能够做到放大/缩小规模，负载平衡，甚至能够主动地执行这些步骤。
```
* 响应式系统的弹性
```md
弹性是与 错误下 的灵敏性responsiveness有关的。

构建一个弹性的、自愈self-healing系统的关键是允许错误被：容纳、具体化为消息，
发送给其他（担当监管者supervisors）的组件，从而在错误组件之外修复出一个安全环境。

消息驱动是其促成因素：远离高度耦合的、脆弱的深层嵌套的同步调用链，大家长期要么学会忍受其煎熬或直接忽略。
解决的想法是将调用链中的错误管理分离，将客户端从处理服务端错误的责任中解放出来。
```
* 响应式系统的韧性
```md
韧性 Elasticity 意味着一个系统的吞吐量在资源增加或减少时能够自动地相应增加或减少
（同样能够向内或外扩展）以满足不同的需求。

这是利用云计算承诺的特性所必需的因素：使系统利用资源更加有效，成本效益更佳，对环境友好以及实现按次付费。
```
* 响应式系统的生产效率
```md
响应式系统是我们所知的最具 生产效率 的系统架构（在多核、云及移动架构的背景下）
```
### 函数响应式编程（Functional Reactive Programming，FRP）
```md
通过函数式编程的函数为基本模块来实现响应式编程。
FRP 是 1997 年提出的概念。
```
### 响应式编程（基于声明的事件的）
```md
是异步编程下的一个子集，也是一种范式，
在这种范式下，由新信息的有效性推动逻辑的前进，而不是让一条执行线程去推动控制流。

它能够把问题分解为多个独立的步骤，这些独立的步骤可以以异步且非阻塞的方式被执行，
最后再组合在一起产生一条工作流——它的输入和输出可能是非绑定的。
```
```md
响应式编程一般是事件驱动event-driven，相比之下，响应式系统则是消息驱动message-driven的。
```
* 响应式编程库的应用程序接口（API）
> * 基于回调的Callback-based
```md
匿名的间接作用 side-effecting 回调函数被绑定在事件源 event sources 上，
当事件被放入数据流 dataflow chain 中时，回调函数被调用。
```
> * 声明式的Declarative
```md
通过函数的组合，通常是使用一些固定的函数，像 map、 filter、 fold 等等。
```
```md
大部分的库会混合这两种风格，一般还带有基于流stream-based的操作符operators，像 windowing、 counts、 triggers。
```
```md
说响应式编程跟 数据流编程dataflow programming有关是很合理的，因为它强调的是数据流而不是控制流。
```
* Futures/Promises
```md
一个值的容器，具有读共享/写独占（many-read/single-write）的语义，即使变量尚不可用也能够添加异步的值转换操作。
```
* 流streams - 响应式流
```md
无限制的数据处理流，支持异步，非阻塞式，支持多个源与目的的反压转换管道(back-pressured transformation pipelines)。
```
* 数据流变量
```md
依赖于输入、过程或者其它单元的单赋值变量 single assignment variables（存储单元），它能够自动更新值的改变。
其中一个应用例子是表格软件 —— 一个单元的值的改变会像涟漪一样荡开，影响到所有依赖于它的函数，顺流而下地使它们产生新的值。
```
* JVM 支持响应式编程的流行库
```md
Akka Streams、Ratpack、Reactor、RxJava 和 Vert.x 等等。
这些库实现了响应式编程的规范，成为 JVM 上响应式编程库之间的互通标准。
```
* 优势
```md
1. 提高多核和多 CPU 硬件的计算资源利用率；
  根据阿姆达尔定律以及引申的 Günther 的通用可伸缩性定律 Günther’s Universal Scalability Law，
  通过减少序列化点 serialization points 来提高性能。
2. 开发者生产效率
  传统的编程范式都尽力想提供一个简单直接的可持续的方法来处理异步非阻塞式计算和 I/O。
  在响应式编程中，因活动(active)组件之间通常不需要明确的协作，从而也就解决了其中大部分的挑战。
```
### 事件驱动 vs. 消息驱动
```md
1. 消息驱动有确定的目标，一定会有消息的接受者，而事件驱动是一件事情希望被观察到，观察者是谁无关紧要。
  消息驱动系统关注消息的接受者，事件驱动系统关注事件源。
2. 在一个使用响应式编程实现的响应式系统中，消息擅长于通讯，事件擅长于反应事实。
```
```md
一条消息就是一则被送往一个明确目的地的数据。一个事件则是达到某个给定状态的组件发出的一个信号。
在一个消息驱动系统中，可寻址到的接收者等待消息的到来然后响应它，否则保持休眠状态。
在一个事件驱动系统中，通知的监听者被绑定到消息源上，这样当消息被发出时它就会被调用。
这意味着一个事件驱动系统专注于可寻址的事件源，而消息驱动系统专注于可寻址的接收者。
```
```md
响应式编程专注于短时间的数据流链条上的计算，因此倾向于事件驱动。
响应式系关注于通过分布式系统的通信和协作所得到的弹性和韧性，则是消息驱动的。
```
```md
消息具有固定的导向，而事件则没有。消息会有明确的（一个）去向，而事件则只是一段等着被观察observe的信息。
```
```md
消息式messaging更适用于异步，因为消息的发送与接收和发送者和接收者是分离的。
```
```md
分布式系统需要通过消息在网络上传输进行交流，以实现其沟通基础，与之相反，事件的发出则是本地的。
在底层通过发送包裹着事件的消息来搭建跨网络的事件驱动系统的做法很常见。
这样能够维持在分布式环境下事件驱动编程模型的相对简易性，并且在某些特殊的和合理的范围内的使用案例上工作得很好。

然而，这是有利有弊的：在编程模型的抽象性和简易性上得一分，在控制上就减一分。
消息强迫我们去拥抱分布式系统的真实性和一致性——像局部错误partial failures，错误侦测failure detection，
丢弃/复制/重排序dropped/duplicated/reordered消息，
最后还有一致性，管理多个并发真实性等等——然后直面它们，去处理它们，而不是像过去无数次一样，
藏在一个蹩脚的抽象面罩后——假装网络并不存在(例如EJB、 RPC、 CORBA 和 XA)。
```
```md
在一个响应式系统中，特别是使用了响应式编程技术的，
这样的系统中就即有事件也有消息——一个是用于沟通的强大工具（消息），而另一个则呈现现实（事件）。
```
### 响应式编程与响应式系统
```md
响应式编程是一种管理内部逻辑internal logic和数据流转换dataflow transformation的好技术。
在本地的组件中，做为一种优化代码清晰度、性能以及资源利用率的方法。

响应式系统，是一组架构上的原则，旨在强调分布式信息交流并为我们提供一种处理分布式系统弹性与韧性的工具。
```
```md
单纯的响应式编程允许 时间 上的解耦decoupling，
但不允许 空间 上的（除非是如上面所述的，在底层通过网络传送消息来分发distribute数据流）。

在时间上的解耦使 并发性 成为可能，但是是空间上的解耦使 分布distribution和 移动性mobility 
（使得不仅仅静态拓扑可用，还包括了动态拓扑）成为可能的——而这些正是 韧性 所必需的要素。
```