# 事件驱动模型
![](../_pic/ed-model.png)

### 基本组件
```md
事件队列（event queue）接收事件的入口，存储待处理事件
分发器（event mediator）将不同的事件分发到不同的业务逻辑单元
事件通道（event channel）分发器与处理器之间的联系渠道
事件处理器（event processor）实现业务逻辑，处理完成后会发出事件，触发下一步操作
```
