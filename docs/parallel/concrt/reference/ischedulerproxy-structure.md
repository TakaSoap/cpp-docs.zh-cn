---
title: ISchedulerProxy 结构
ms.date: 11/04/2016
f1_keywords:
- ISchedulerProxy
- CONCRTRM/concurrency::ISchedulerProxy
- CONCRTRM/concurrency::ISchedulerProxy::ISchedulerProxy::BindContext
- CONCRTRM/concurrency::ISchedulerProxy::ISchedulerProxy::CreateOversubscriber
- CONCRTRM/concurrency::ISchedulerProxy::ISchedulerProxy::RequestInitialVirtualProcessors
- CONCRTRM/concurrency::ISchedulerProxy::ISchedulerProxy::Shutdown
- CONCRTRM/concurrency::ISchedulerProxy::ISchedulerProxy::SubscribeCurrentThread
- CONCRTRM/concurrency::ISchedulerProxy::ISchedulerProxy::UnbindContext
helpviewer_keywords:
- ISchedulerProxy structure
ms.assetid: af416973-7a1c-4c30-aa3b-4161c2aaea54
ms.openlocfilehash: 776f70f9b93eb2e38151ceb5e84b4664420cf954
ms.sourcegitcommit: a8ef52ff4a4944a1a257bdaba1a3331607fb8d0f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/11/2020
ms.locfileid: "77140336"
---
# <a name="ischedulerproxy-structure"></a>ISchedulerProxy 结构

计划程序用来与并发运行时的资源管理器进行通信以协商资源分配的接口。

## <a name="syntax"></a>语法

```cpp
struct ISchedulerProxy;
```

## <a name="members"></a>Members

### <a name="public-methods"></a>公共方法

|名称|说明|
|----------|-----------------|
|[ISchedulerProxy：： BindContext](#bindcontext)|将执行上下文与线程代理关联（如果它尚未与其中的关联）。|
|[ISchedulerProxy：： CreateOversubscriber](#createoversubscriber)|在与现有执行资源关联的硬件线程上创建新的虚拟处理器根。|
|[ISchedulerProxy：： RequestInitialVirtualProcessors](#requestinitialvirtualprocessors)|请求虚拟处理器根的初始分配。 每个虚拟处理器根都代表执行一个线程来执行计划程序的能力。|
|[ISchedulerProxy：： Shutdown](#shutdown)|通知资源管理器计划程序正在关闭。 这将导致资源管理器立即回收授予计划程序的所有资源。|
|[ISchedulerProxy：： SubscribeCurrentThread](#subscribecurrentthread)|将当前线程注册到资源管理器，并将它与此计划程序关联。|
|[ISchedulerProxy：： UnbindContext](#unbindcontext)|取消线程代理与 `pContext` 参数指定的执行上下文之间的相关操作，并将其返回给线程代理工厂的可用池。 此方法只能在通过[ISchedulerProxy：： BindContext](#bindcontext)方法绑定的执行上下文上调用，并且尚未通过[IThreadProxy：： SwitchTo](ithreadproxy-structure.md#switchto)方法调用的 `pContext` 参数启动。|

## <a name="remarks"></a>备注

资源管理器使用[IResourceManager：： RegisterScheduler](iresourcemanager-structure.md#registerscheduler)方法为注册到它的每个计划程序提供 `ISchedulerProxy` 接口。

## <a name="inheritance-hierarchy"></a>继承层次结构

`ISchedulerProxy`

## <a name="requirements"></a>要求

**标头：** concrtrm。h

**命名空间：** 并发

## <a name="bindcontext"></a>ISchedulerProxy：： BindContext 方法

将执行上下文与线程代理关联（如果它尚未与其中的关联）。

```cpp
virtual void BindContext(_Inout_ IExecutionContext* pContext) = 0;
```

### <a name="parameters"></a>参数

*pContext*<br/>
要与线程代理关联的执行上下文的接口。

### <a name="remarks"></a>备注

通常， [IThreadProxy：： SwitchTo](ithreadproxy-structure.md#switchto)方法会按需将线程代理绑定到执行上下文。 但在某些情况下，需要事先绑定上下文以确保 `SwitchTo` 方法切换到已绑定的上下文。 这种情况在 UMS 计划上下文上，因为它不能调用分配内存的方法，如果线程代理在线程代理工厂的可用池中不能轻松地使用，则绑定线程代理可能会涉及内存分配。

如果参数 `pContext` 具有值 `NULL`，则会引发 `invalid_argument`。

## <a name="createoversubscriber"></a>ISchedulerProxy：： CreateOversubscriber 方法

在与现有执行资源关联的硬件线程上创建新的虚拟处理器根。

```cpp
virtual IVirtualProcessorRoot* CreateOversubscriber(_Inout_ IExecutionResource* pExecutionResource) = 0;
```

### <a name="parameters"></a>参数

*pExecutionResource*<br/>
一个 `IExecutionResource` 接口，该接口表示你要订阅的硬件线程。

### <a name="return-value"></a>返回值

一个 `IVirtualProcessorRoot` 接口。

### <a name="remarks"></a>备注

当您的计划程序要在有限的时间内超额订阅特定的硬件线程时，可使用此方法。 完成虚拟处理器根后，应通过对 `IVirtualProcessorRoot` 接口调用[Remove](iexecutionresource-structure.md#remove)方法，将其返回给资源管理器。

您甚至可以过度订阅现有虚拟处理器根，因为 `IVirtualProcessorRoot` 接口继承自 `IExecutionResource` 接口。

## <a name="requestinitialvirtualprocessors"></a>ISchedulerProxy：： RequestInitialVirtualProcessors 方法

请求虚拟处理器根的初始分配。 每个虚拟处理器根都代表执行一个线程来执行计划程序的能力。

```cpp
virtual IExecutionResource* RequestInitialVirtualProcessors(bool doSubscribeCurrentThread) = 0;
```

### <a name="parameters"></a>参数

*doSubscribeCurrentThread*<br/>
是否在资源分配过程中订阅当前线程并为其提供帐户。

### <a name="return-value"></a>返回值

如果参数 `doSubscribeCurrentThread` 的值**为 true**，则为当前线程的 `IExecutionResource` 接口。 如果该值为**false**，则该方法返回 NULL。

### <a name="remarks"></a>备注

在计划程序执行任何工作之前，应使用此方法从资源管理器请求虚拟处理器根。 资源管理器将使用[IScheduler：： GetPolicy](ischeduler-structure.md#getpolicy)访问计划程序的策略，并使用策略密钥 `MinConcurrency`、`MaxConcurrency` 和 `TargetOversubscriptionFactor` 的值来确定要为计划程序分配多少个硬件线程以及为每个硬件线程创建多少个虚拟处理器根。 有关如何使用计划程序策略来确定计划程序初始分配的详细信息，请参阅[PolicyElementKey](concurrency-namespace-enums.md)。

资源管理器通过使用虚拟处理器根的列表调用方法[IScheduler：： AddVirtualProcessors](ischeduler-structure.md#addvirtualprocessors)来向计划程序授予资源。 在此方法返回之前，方法将作为回调调用到计划程序中。

如果计划程序通过将参数 `doSubscribeCurrentThread` 设置为**true**，请求当前线程的订阅，则该方法将返回 `IExecutionResource` 接口。 使用[IExecutionResource：： Remove](iexecutionresource-structure.md#remove)方法，必须在稍后终止订阅。

确定选择了哪些硬件线程时，资源管理器会尝试优化处理器节点相关性。 如果为当前线程请求了订阅，则指示当前线程打算参与分配给此计划程序的工作。 在这种情况下，分配的虚拟处理器根位于当前线程正在执行的处理器节点上（如果可能）。

订阅线程的操作会将基础硬件线程的订阅级别增加1。 终止订阅后，订阅级别将减少1。 有关订阅级别的详细信息，请参阅[IExecutionResource：： CurrentSubscriptionLevel](iexecutionresource-structure.md#currentsubscriptionlevel)。

## <a name="shutdown"></a>ISchedulerProxy：： Shutdown 方法

通知资源管理器计划程序正在关闭。 这将导致资源管理器立即回收授予计划程序的所有资源。

```cpp
virtual void Shutdown() = 0;
```

### <a name="remarks"></a>备注

由于使用 `ISchedulerProxy::RequestInitialVirtualProcessors` 或 `ISchedulerProxy::SubscribeCurrentThread` 在计划程序自行关闭之前，必须使用 `IExecutionResource::Remove` 将或返回到资源管理器，因此，计划程序收到的所有 `IExecutionContext` 接口都将作为订阅外部线程的结果。

如果你的计划程序具有任何已停用的虚拟处理器根，则必须使用[IVirtualProcessorRoot：： activate](ivirtualprocessorroot-structure.md#activate)激活这些根，并在这些根上执行线程代理，在调用计划程序代理上的 `Shutdown` 之前，保留它们正在分派的执行上下文的 `Dispatch` 方法。

计划程序不需要通过调用 `Remove` 方法分别返回资源管理器授予它的所有虚拟处理器根，因为关机时所有虚拟处理器根都将返回到资源管理器。

## <a name="subscribecurrentthread"></a>ISchedulerProxy：： SubscribeCurrentThread 方法

将当前线程注册到资源管理器，并将它与此计划程序关联。

```cpp
virtual IExecutionResource* SubscribeCurrentThread() = 0;
```

### <a name="return-value"></a>返回值

表示运行时中当前线程的 `IExecutionResource` 接口。

### <a name="remarks"></a>备注

如果希望资源管理器在将资源分配给计划程序和其他计划程序时考虑当前线程，请使用此方法。 当线程计划参与到计划程序中的工作时，它特别有用，计划程序将其从资源管理器接收的虚拟处理器根。 资源管理器使用信息来防止系统上的硬件线程的过度订阅。

通过此方法接收的执行资源应该使用[IExecutionResource：： Remove](iexecutionresource-structure.md#remove)方法返回到资源管理器。 调用 `Remove` 方法的线程必须与之前称为 `SubscribeCurrentThread` 方法的线程相同。

订阅线程的操作会将基础硬件线程的订阅级别增加1。 终止订阅后，订阅级别将减少1。 有关订阅级别的详细信息，请参阅[IExecutionResource：： CurrentSubscriptionLevel](iexecutionresource-structure.md#currentsubscriptionlevel)。

## <a name="unbindcontext"></a>ISchedulerProxy：： UnbindContext 方法

取消线程代理与 `pContext` 参数指定的执行上下文之间的相关操作，并将其返回给线程代理工厂的可用池。 此方法只能在通过[ISchedulerProxy：： BindContext](#bindcontext)方法绑定的执行上下文上调用，并且尚未通过[IThreadProxy：： SwitchTo](ithreadproxy-structure.md#switchto)方法调用的 `pContext` 参数启动。

```cpp
virtual void UnbindContext(_Inout_ IExecutionContext* pContext) = 0;
```

### <a name="parameters"></a>参数

*pContext*<br/>
要与其线程代理解除关联的执行上下文。

## <a name="see-also"></a>另请参阅

[并发命名空间](concurrency-namespace.md)<br/>
[IScheduler 结构](ischeduler-structure.md)<br/>
[IThreadProxy 结构](ithreadproxy-structure.md)<br/>
[IVirtualProcessorRoot 结构](ivirtualprocessorroot-structure.md)<br/>
[IResourceManager 结构](iresourcemanager-structure.md)
