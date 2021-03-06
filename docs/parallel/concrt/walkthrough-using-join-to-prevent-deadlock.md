---
title: 演练：使用 join 避免死锁
ms.date: 04/25/2019
helpviewer_keywords:
- preventing deadlock with joins [Concurrency Runtime]
- deadlock, preventing [Concurrency Runtime]
- non-greedy joins, example
- join class, example
ms.assetid: d791f697-bb93-463e-84bd-5df1651b7446
ms.openlocfilehash: 4df83e944552fd6c0d2482efa72883d87cd45f8c
ms.sourcegitcommit: a8ef52ff4a4944a1a257bdaba1a3331607fb8d0f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/11/2020
ms.locfileid: "77140658"
---
# <a name="walkthrough-using-join-to-prevent-deadlock"></a>演练：使用 join 避免死锁

本主题使用哲学家就餐问题说明如何使用[concurrency：： join](../../parallel/concrt/reference/join-class.md)类来防止应用程序中出现死锁。 在软件应用中，如果两个或多个进程分别留有资源，且相互等待另一进程释放其他资源，就会发生死锁。

哲学家就餐问题是在多个并发进程间共享一组资源时可能出现的一般问题集的一个具体示例。

## <a name="prerequisites"></a>先决条件

在开始本演练之前，请阅读以下主题：

- [异步代理](../../parallel/concrt/asynchronous-agents.md)

- [演练：创建基于代理的应用程序](../../parallel/concrt/walkthrough-creating-an-agent-based-application.md)

- [异步消息块](../../parallel/concrt/asynchronous-message-blocks.md)

- [消息传递函数](../../parallel/concrt/message-passing-functions.md)

- [同步数据结构](../../parallel/concrt/synchronization-data-structures.md)

## <a name="top"></a> 部分

本演练包含以下各节：

- [哲学家就餐问题](#problem)

- [简单实现](#deadlock)

- [使用 join 避免死锁](#solution)

## <a name="problem"></a>哲学家就餐问题

哲学家就餐问题说明了应用程序中出现死锁的情况。 在此问题中，有五个哲学家坐在一个圆桌上。 每个哲学家在思考与吃间都有不同之处。 每个哲学家都必须与左侧的邻居共享 chopstick，并将另一个 chopstick 与右侧的邻居共享。 下图显示了此布局。

![哲学家就餐问题](../../parallel/concrt/media/dining_philosophersproblem.png "哲学家就餐问题")

若要吃吃，哲学家必须包含两个筷子。 如果每个哲学家都只包含一个 chopstick 并等待另一个，则哲学家不会吃和所有枯竭。

[[返回页首](#top)]

## <a name="deadlock"></a>简单实现

下面的示例演示了哲学家就餐问题的简单实现。 从[concurrency：： agent](../../parallel/concrt/reference/agent-class.md)派生的 `philosopher` 类使每个哲学家可以独立操作。 该示例使用一个[并发的 concurrency：： critical_section](../../parallel/concrt/reference/critical-section-class.md)对象数组向每个 `philosopher` 对象授予对一对筷子的独占访问权限。

为了使实现与插图相关，`philosopher` 类表示一个哲学家。 `int` 变量表示每个 chopstick。 `critical_section` 对象充当筷子的对象。 `run` 方法模拟哲学家的生存期。 `think` 方法模拟思考的行为，而 `eat` 方法模拟吃的行为。

`philosopher` 对象会锁定 `critical_section` 对象，以便在调用 `eat` 方法之前模拟从持有者中删除筷子。 调用 `eat`后，`philosopher` 对象通过将 `critical_section` 对象设置回未锁定状态来将筷子返回给持有者。

`pickup_chopsticks` 方法说明了可能发生死锁的情况。 如果每个 `philosopher` 对象均获得对其中一个锁定的访问权限，则没有 `philosopher` 对象可以继续，因为另一个锁由另一个 `philosopher` 对象控制。

### <a name="example"></a>示例

[!code-cpp[concrt-philosophers-deadlock#1](../../parallel/concrt/codesnippet/cpp/walkthrough-using-join-to-prevent-deadlock_1.cpp)]

### <a name="compiling-the-code"></a>编译代码

复制代码示例并将其粘贴到 Visual Studio 项目中，或粘贴到一个名为 `philosophers-deadlock.cpp` 的文件中，然后在 Visual Studio 命令提示符窗口中运行以下命令。

> **cl/EHsc philosophers-deadlock**

[[返回页首](#top)]

## <a name="solution"></a>使用 join 避免死锁

本部分演示如何使用消息缓冲区和消息传递函数来消除死锁的可能性。

为了使此示例与前面的示例相关，`philosopher` 类将使用[concurrency：： unbounded_buffer](reference/unbounded-buffer-class.md)对象和 `join` 对象替换每个 `critical_section` 对象。 `join` 对象充当向哲学家提供筷子的仲裁器。

此示例使用 `unbounded_buffer` 类，因为当目标接收来自 `unbounded_buffer` 对象的消息时，将从消息队列中删除该消息。 这将启用保存消息的 `unbounded_buffer` 对象，以指示 chopstick 可用。 不包含任何消息的 `unbounded_buffer` 对象指示正在使用 chopstick。

此示例使用非贪婪 `join` 对象，因为非贪婪联接仅在两个 `unbounded_buffer` 对象都包含一条消息时，使每个 `philosopher` 对象都可以访问这两个筷子。 贪婪联接不会阻止死锁，因为贪婪联接会在消息可用时立即接受消息。 如果所有贪婪 `join` 对象均收到其中一条消息但一直等待另一消息变为可用，则会发生死锁。

有关贪婪和非贪婪联接的详细信息以及各种消息缓冲区类型之间的差异，请参阅[异步消息块](../../parallel/concrt/asynchronous-message-blocks.md)。

### <a name="to-prevent-deadlock-in-this-example"></a>在此示例中防止死锁

1. 从示例中删除以下代码。

[!code-cpp[concrt-philosophers-deadlock#2](../../parallel/concrt/codesnippet/cpp/walkthrough-using-join-to-prevent-deadlock_2.cpp)]

1. 将 `philosopher` 类的 `_left` 和 `_right` 数据成员的类型更改为 `unbounded_buffer`。

[!code-cpp[concrt-philosophers-join#2](../../parallel/concrt/codesnippet/cpp/walkthrough-using-join-to-prevent-deadlock_3.cpp)]

1. 修改 `philosopher` 构造函数以采用 `unbounded_buffer` 对象作为其参数。

[!code-cpp[concrt-philosophers-join#3](../../parallel/concrt/codesnippet/cpp/walkthrough-using-join-to-prevent-deadlock_4.cpp)]

1. 将 `pickup_chopsticks` 方法修改为使用非贪婪 `join` 对象从消息缓冲区中为这两个筷子接收消息。

[!code-cpp[concrt-philosophers-join#4](../../parallel/concrt/codesnippet/cpp/walkthrough-using-join-to-prevent-deadlock_5.cpp)]

1. 修改 `putdown_chopsticks` 方法，以释放对这两个筷子的消息缓冲区的消息的访问权限。

[!code-cpp[concrt-philosophers-join#5](../../parallel/concrt/codesnippet/cpp/walkthrough-using-join-to-prevent-deadlock_6.cpp)]

1. 修改 `run` 方法以保存 `pickup_chopsticks` 方法的结果并将这些结果传递到 `putdown_chopsticks` 方法。

[!code-cpp[concrt-philosophers-join#6](../../parallel/concrt/codesnippet/cpp/walkthrough-using-join-to-prevent-deadlock_7.cpp)]

1. 修改 `wmain` 函数中 `chopsticks` 变量的声明，使其成为每个 `unbounded_buffer` 对象的数组，每个对象都包含一条消息。

[!code-cpp[concrt-philosophers-join#7](../../parallel/concrt/codesnippet/cpp/walkthrough-using-join-to-prevent-deadlock_8.cpp)]

### <a name="description"></a>说明

下面显示了使用非贪婪 `join` 对象的示例，消除了死锁风险。

### <a name="example"></a>示例

[!code-cpp[concrt-philosophers-join#1](../../parallel/concrt/codesnippet/cpp/walkthrough-using-join-to-prevent-deadlock_9.cpp)]

本示例生成以下输出。

```Output
aristotle ate 50 times.
descartes ate 50 times.
hobbes ate 50 times.
socrates ate 50 times.
plato ate 50 times.
```

### <a name="compiling-the-code"></a>编译代码

复制代码示例并将其粘贴到 Visual Studio 项目中，或粘贴到一个名为 `philosophers-join.cpp` 的文件中，然后在 Visual Studio 命令提示符窗口中运行以下命令。

> **cl/EHsc philosophers-join**

[[返回页首](#top)]

## <a name="see-also"></a>另请参阅

[并发运行时演练](../../parallel/concrt/concurrency-runtime-walkthroughs.md)<br/>
[异步代理库](../../parallel/concrt/asynchronous-agents-library.md)<br/>
[异步代理](../../parallel/concrt/asynchronous-agents.md)<br/>
[异步消息块](../../parallel/concrt/asynchronous-message-blocks.md)<br/>
[消息传递函数](../../parallel/concrt/message-passing-functions.md)<br/>
[同步数据结构](../../parallel/concrt/synchronization-data-structures.md)
