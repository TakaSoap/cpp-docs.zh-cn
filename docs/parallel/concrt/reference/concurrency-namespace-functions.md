---
title: 并发命名空间函数
ms.date: 11/04/2016
f1_keywords:
- concrt/concurrency::Alloc
- concrt/concurrency::DisableTracing
- concrt/concurrency::EnableTracing
- concrtrm/concurrency::GetExecutionContextId
- concrtrm/concurrency::GetOSVersion
- concrtrm/concurrency::GetProcessorNodeCount
- concrtrm/concurrency::GetSchedulerId
- agents/concurrency::asend
- ppltasks/concurrency::cancel_current_task
- ppltasks/concurrency::create_async
- ppltasks/concurrency::create_task
- concurrent_vector/concurrency::internal_assign_iterators
- ppl/concurrency::interruption_point
- agents/concurrency::make_choice
- agents/concurrency::make_greedy_join
- ppl/concurrency::make_task
- ppl/concurrency::parallel_buffered_sort
- ppl/concurrency::parallel_for_each
- ppl/concurrency::parallel_invoke
- ppl/concurrency::parallel_reduce
- ppl/concurrency::parallel_sort
- agents/concurrency::receive
- ppl/concurrency::run_with_cancellation_token
- pplconcrt/concurrency::set_ambient_scheduler
- concrt/concurrency::set_task_execution_resources
- ppltasks/concurrency::task_from_exception
- ppltasks/concurrency::task_from_result
- concrt/concurrency::wait
- ppltasks/concurrency::when_all
- ppltasks/concurrency::when_any
ms.assetid: 520a6dff-9324-4df2-990d-302e3050af6a
ms.openlocfilehash: 4005ae888511ec987fe83ab3d616aa0fc3675a22
ms.sourcegitcommit: a8ef52ff4a4944a1a257bdaba1a3331607fb8d0f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/11/2020
ms.locfileid: "77143261"
---
# <a name="concurrency-namespace-functions"></a>并发命名空间函数

||||
|-|-|-|
|[分配](#alloc)|[CreateResourceManager](#createresourcemanager)|[DisableTracing](#disabletracing)|
|[EnableTracing](#enabletracing)|[免费](#free)|[GetExecutionContextId](#getexecutioncontextid)|
|[GetOSVersion](#getosversion)|[GetProcessorCount](#getprocessorcount)|[GetProcessorNodeCount](#getprocessornodecount)|
|[GetSchedulerId](#getschedulerid)|[Trace_agents_register_name](#trace_agents_register_name)|[asend](#asend)|
|[cancel_current_task](#cancel_current_task)|[clear](#clear)|[create_async](#create_async)|
|[create_task](#create_task)|[get_ambient_scheduler](#get_ambient_scheduler)|[internal_assign_iterators](#internal_assign_iterators)|
|[interruption_point](#interruption_point)|[is_current_task_group_canceling](#is_current_task_group_canceling)|[make_choice](#make_choice)|
|[make_greedy_join](#make_greedy_join)|[make_join](#make_join)|[make_task](#make_task)|
|[parallel_buffered_sort](#parallel_buffered_sort)|[parallel_for](#parallel_for)|[parallel_for_each](#parallel_for_each)|
|[parallel_invoke](#parallel_invoke)|[parallel_radixsort](#parallel_radixsort)|[parallel_reduce](#parallel_reduce)|
|[parallel_sort](#parallel_sort)|[parallel_transform](#parallel_transform)|[receive](#receive)|
|[run_with_cancellation_token](#run_with_cancellation_token)|[发送](#send)|[set_ambient_scheduler](#set_ambient_scheduler)|
|[set_task_execution_resources](#set_task_execution_resources)|[swap](#swap)|[task_from_exception](#task_from_exception)|
|[task_from_result](#task_from_result)|[try_receive](#try_receive)|[再](#wait)|
|[when_all](#when_all)|[when_any](#when_any)|

## <a name="alloc"></a>分配

通过并发运行时缓存子分配器分配具有指定大小的内存块。

```cpp
void* __cdecl Alloc(size_t _NumBytes);
```

### <a name="parameters"></a>参数

*_NumBytes*<br/>
要分配的内存字节数。

### <a name="return-value"></a>返回值

指向新分配的内存的指针。

### <a name="remarks"></a>备注

若要详细了解应用程序中的哪些方案可以利用缓存子分配器，请参阅[任务计划程序](../../../parallel/concrt/task-scheduler-concurrency-runtime.md)。

## <a name="asend"></a>asend

异步发送操作，计划任务以将数据传播到目标块。

```cpp
template <class T>
bool asend(
    _Inout_ ITarget<T>* _Trg,
    const T& _Data);

template <class T>
bool asend(
    ITarget<T>& _Trg,
    const T& _Data);
```

### <a name="parameters"></a>参数

*T*<br/>
要发送的数据的类型。

*_Trg*<br/>
指向向其发送数据的目标的指针或引用。

*_Data*<br/>
对要发送的数据的引用。

### <a name="return-value"></a>返回值

如果在返回方法之前接受了消息，**则为 true** ; 否则为**false** 。

### <a name="remarks"></a>备注

有关详细信息，请参阅[消息传递函数](../../../parallel/concrt/message-passing-functions.md)。

## <a name="cancel_current_task"></a>  cancel_current_task

获取当前执行的任务。 此函数可从任务主体中进行调用，以便中止任务的执行并使其进入 `canceled` 状态。

不支持从 `task` 主体外部调用此函数的情况。 这样做将导致未定义的行为，例如应用程序崩溃或挂起。

```cpp
inline __declspec(noreturn) void __cdecl cancel_current_task();
```

## <a name="clear"></a>清除

清除并发队列，销毁当前排队的任何元素。 此方法不是并发安全方法。

```cpp
template<typename T, class _Ax>
void concurrent_queue<T, _Ax>::clear();
```

### <a name="parameters"></a>参数

*T*<br/>

*_Ax*<br/>

## <a name="create_async"></a>  create_async

基于用户提供的 lambda 或函数对象创建 Windows 运行时异步构造。 `create_async` 的返回类型是基于传递给方法的 lambda 的签名的 `IAsyncAction^`、`IAsyncActionWithProgress<TProgress>^`、`IAsyncOperation<TResult>^` 或 `IAsyncOperationWithProgress<TResult, TProgress>^` 之一。

```cpp
template<typename _Function>
__declspec(noinline) auto create_async(const _Function& _Func)
    -> decltype(ref new details::_AsyncTaskGeneratorThunk<_Function>(_Func));
```

### <a name="parameters"></a>参数

*_Function*<br/>
类型。

*_Func*<br/>
从其中创建 Windows 运行时异步构造的 lambda 或函数对象。

### <a name="return-value"></a>返回值

异步构造由 IAsyncAction ^、Iasyncactionwithprogress<tprogress>\<TProgress > ^、Iasyncoperation<tresult>\<TResult > ^ 或 IAsyncOperationWithProgress\<TResult、TProgress > ^ 表示。 返回的接口依赖于传递给函数的 lambda 的签名。

### <a name="remarks"></a>备注

lambda 的返回类型确定该构造是一个行为还是一项操作。

返回 void 的 lambda 将导致创建一些行为。 返回类型为 `TResult` 的结果的 lambda 将导致创建 TResult 的操作。

lambda 可能还返回 `task<TResult>`（在自身中封装异步工作或是表示异步工作的任务链的延续）。 在此示例中，由于任务是异步执行的，所以将以内联方式执行 lambda，并且将解包 lambda 的返回类型以生成 `create_async` 返回的异步构造。 这意味着，返回 task\<void > 的 lambda 将导致创建操作，而在 TResult > 返回\<task 的 lambda 将导致创建 TResult 操作。

lambda 可采用零个、一个或两个自变量。 有效的自变量是 `progress_reporter<TProgress>` 和 `cancellation_token`（此顺序为同时使用两个自变量的顺序）。 无自变量的 lambda 将导致创建一个缺少进度报告功能的异步构造。 采用 progress_reporter\<TProgress > 的 lambda 将导致 `create_async` 返回一个异步构造，在每次调用 `report` 对象的 progress_reporter 方法时，该构造将报告 TProgress 类型的进度。 采用 cancellation_token 的 lambda 可以使用该标记来检查取消情况，或将该标记传递给它创建的任务，以便取消异步构造可导致取消这些任务。

如果 lambda 或函数对象的主体返回一个结果（而不是一个 task\<TResult >），则 lamdba 将在运行时为其隐式创建的任务上下文中以异步方式执行。 `IAsyncInfo::Cancel` 方法将导致取消隐式任务。

如果 lambda 的主体返回一个任务，则 lamba 将通过声明 lambda 采用类型为 `cancellation_token` 的自变量，以内联方式执行，你可以通过在创建任务时将此标记传入，从而触发对在 lambda 中创建的任何任务的取消。 您还可对此标记使用 `register_callback` 方法，以使运行时在您对产生的异步操作或行为调用 `IAsyncInfo::Cancel` 时调用回调。

此功能仅可用于 Windows 运行时应用。

## <a name="createresourcemanager"></a>  CreateResourceManager

返回表示并发运行时的资源管理器的单一实例的接口。 资源管理器负责将资源分配给想要相互合作的计划程序。

```cpp
IResourceManager* __cdecl CreateResourceManager();
```

### <a name="return-value"></a>返回值

一个 `IResourceManager` 接口。

### <a name="remarks"></a>备注

对此方法的多次后续调用将返回资源管理器的同一个实例。 每次调用方法都会增加资源管理器上的引用计数，并且当计划程序完成与资源管理器的通信时，必须与[IResourceManager：： Release](iresourcemanager-structure.md)方法的调用匹配。

如果并发运行时不支持操作系统，则会引发[unsupported_os](unsupported-os-class.md) 。

## <a name="create_task"></a>  create_task

创建 PPL[任务](task-class.md)对象。 在你会使用任务构造函数的任何位置都可以使用 `create_task`。 出于便利性提供该函数，因为它允许在创建任务时使用 `auto` 关键字。

```cpp
template<typename T>
__declspec(noinline) auto create_task(T _Param, const task_options& _TaskOptions = task_options())
    -> task<typename details::_TaskTypeFromParam<T>::T>;

template<typename _ReturnType>
__declspec( noinline) task<_ReturnType> create_task(const task<_ReturnType>& _Task);
```

### <a name="parameters"></a>参数

*T*<br/>
从中构造任务的参数的类型。

*_ReturnType*<br/>
类型。

*_Param*<br/>
从中构造任务的参数。 如果你在 UWP 应用中使用任务，则这可能是 lambda 或函数对象、`task_completion_event` 对象、不同的 `task` 对象或 Windows：： Foundation：： IAsyncInfo 接口。

*_TaskOptions*<br/>
任务选项。

*_Task*<br/>
要创建的任务。

### <a name="return-value"></a>返回值

`T`类型的新任务，从 `_Param`推断。

### <a name="remarks"></a>备注

第一个重载的行为类似于采用单个参数的任务构造函数。

第二个重载将所提供的取消标记与新创建的任务相关联。 如果使用此重载，则不允许将其他 `task` 对象作为第一个参数传入。

返回的任务的类型将从第一个参数推断出函数。 如果 `_Param` 是 `task_completion_event<T>`、`task<T>`或返回 `T` 或 `task<T>`类型的函子，则创建的任务的类型将为 `task<T>`。

在 UWP 应用中，如果 `_Param` 的类型为 Windows：： Foundation：： Iasyncoperation<tresult>\<T > ^ 或 Windows：： Foundation：： IAsyncOperationWithProgress\<T，P > ^，或返回这两种类型之一的函子，则创建的任务的类型将为 `task<T>`。 如果 `_Param` 的类型为 Windows：： Foundation：： IAsyncAction ^ 或 Windows：： Foundation：： Iasyncactionwithprogress<tprogress>\<P > ^，或返回这两种类型之一的函子，则创建的任务将具有类型 `task<void>`。

## <a name="disabletracing"></a>  DisableTracing

在并发运行时中禁用跟踪。 此函数被弃用，因为默认注销 ETW 跟踪。

```cpp
__declspec(deprecated("Concurrency::DisableTracing is a deprecated function.")) _CRTIMP HRESULT __cdecl DisableTracing();
```

### <a name="return-value"></a>返回值

如果已正确禁用跟踪，则返回 `S_OK`。 如果之前未启动跟踪，将返回 `E_NOT_STARTED`。

## <a name="enabletracing"></a>  EnableTracing

在并发运行时中启用跟踪。 此函数被弃用，因为现在默认启用 ETW 跟踪。

```cpp
__declspec(deprecated("Concurrency::EnableTracing is a deprecated function.")) _CRTIMP HRESULT __cdecl EnableTracing();
```

### <a name="return-value"></a>返回值

如果跟踪已正确启动，则返回 `S_OK`;否则，将返回 `E_NOT_STARTED`。

## <a name="free"></a>忙

释放先前通过 `Alloc` 方法分配给并发运行时的缓存子分配器的内存块。

```cpp
void __cdecl Free(_Pre_maybenull_ _Post_invalid_ void* _PAllocation);
```

### <a name="parameters"></a>参数

*_PAllocation*<br/>
一个指向内存的指针，该内存以前由要释放的 `Alloc` 方法分配。 如果参数 `_PAllocation` 设置为 `NULL`值，则此方法将忽略该值并立即返回。

### <a name="remarks"></a>备注

若要详细了解应用程序中的哪些方案可以利用缓存子分配器，请参阅[任务计划程序](../../../parallel/concrt/task-scheduler-concurrency-runtime.md)。

## <a name="get_ambient_scheduler"></a>  get_ambient_scheduler

```cpp
inline std::shared_ptr<::Concurrency::scheduler_interface> get_ambient_scheduler();
```

### <a name="return-value"></a>返回值

## <a name="getexecutioncontextid"></a>  GetExecutionContextId

返回可以分配给实现 `IExecutionContext` 接口的执行上下文的唯一标识符。

```cpp
unsigned int __cdecl GetExecutionContextId();
```

### <a name="return-value"></a>返回值

执行上下文的唯一标识符。

### <a name="remarks"></a>备注

使用此方法可获取执行上下文的标识符，然后将 `IExecutionContext` 接口作为参数传递给资源管理器提供的任何方法。

## <a name="getosversion"></a>  GetOSVersion

返回操作系统版本。

```cpp
IResourceManager::OSVersion __cdecl GetOSVersion();
```

### <a name="return-value"></a>返回值

表示操作系统的枚举值。

### <a name="remarks"></a>备注

如果并发运行时不支持操作系统，则会引发[unsupported_os](unsupported-os-class.md) 。

## <a name="getprocessorcount"></a>  GetProcessorCount

返回基础系统上的硬件线程数。

```cpp
unsigned int __cdecl GetProcessorCount();
```

### <a name="return-value"></a>返回值

硬件线程数。

### <a name="remarks"></a>备注

如果并发运行时不支持操作系统，则会引发[unsupported_os](unsupported-os-class.md) 。

## <a name="getprocessornodecount"></a>  GetProcessorNodeCount

返回基础系统上的 NUMA 节点数或处理器包数。

```cpp
unsigned int __cdecl GetProcessorNodeCount();
```

### <a name="return-value"></a>返回值

NUMA 节点数或处理器包数。

### <a name="remarks"></a>备注

如果系统包含的 NUMA 节点数多于处理器包数量，则返回 NUMA 节点数，否则返回处理器包的数量。

如果并发运行时不支持操作系统，则会引发[unsupported_os](unsupported-os-class.md) 。

## <a name="getschedulerid"></a>  GetSchedulerId

返回可以分配给实现 `IScheduler` 接口的计划程序的唯一标识符。

```cpp
unsigned int __cdecl GetSchedulerId();
```

### <a name="return-value"></a>返回值

计划程序的唯一标识符。

### <a name="remarks"></a>备注

使用此方法可获取计划程序的标识符，然后将 `IScheduler` 接口作为参数传递给资源管理器提供的任何方法。

## <a name="internal_assign_iterators"></a>internal_assign_iterators

```cpp
template<typename T, class _Ax>
template<class _I>
void concurrent_vector<T, _Ax>::internal_assign_iterators(
   _I first,
   _I last);
```

### <a name="parameters"></a>参数

*T*<br/>

*_Ax*<br/>

*_I*<br/>

*first*<br/>

*last*<br/>

## <a name="interruption_point"></a>  interruption_point

创建取消的中断点。 如果正在调用此函数的上下文中执行取消操作，则此函数将引发内部异常，该内部异常中止当前执行并行工作的执行。 如果没有正在执行取消操作，则函数不执行任何操作。

```cpp
inline void interruption_point();
```

### <a name="remarks"></a>备注

您不应捕捉由 `interruption_point()` 函数引发的内部取消异常。 此异常将由运行时捕捉和处理，捕捉它可能会导致程序行为异常。

## <a name="is_current_task_group_canceling"></a>  is_current_task_group_canceling

返回在当前上下文中进行内联执行的任务组是否正处于活动取消的过程中（或不久将取消）的指示。 请注意，如果当前上下文中没有当前正在进行内联执行的任务组，则将返回 `false`。

```cpp
bool __cdecl is_current_task_group_canceling();
```

### <a name="return-value"></a>返回值

如果正在取消当前正在执行的任务组，**则为 true** ; 否则为**false** 。

### <a name="remarks"></a>备注

有关详细信息，请参阅[取消](../../../parallel/concrt/exception-handling-in-the-concurrency-runtime.md#cancellation)。

## <a name="make_choice"></a>  make_choice

从可选的 `choice` 或 `Scheduler` 及两个或更多输入源构造 `ScheduleGroup` 消息块。

```cpp
template<typename T1, typename T2, typename... Ts>
choice<std::tuple<T1, T2, Ts...>> make_choice(
    Scheduler& _PScheduler,
    T1  _Item1,
    T2  _Item2,
    Ts... _Items);

template<typename T1, typename T2, typename... Ts>
choice<std::tuple<T1, T2, Ts...>> make_choice(
    ScheduleGroup& _PScheduleGroup,
    T1  _Item1,
    T2  _Item2,
    Ts... _Items);

template<typename T1, typename T2, typename... Ts>
choice<std::tuple<T1, T2, Ts...>> make_choice(
    T1  _Item1,
    T2  _Item2,
    Ts... _Items);
```

### <a name="parameters"></a>参数

T1<br/>
第一个源的消息块类型。

T2<br/>
第二个源的消息块类型。

*_PScheduler*<br/>
在其中计划了 `Scheduler` 消息块的传播任务的 `choice` 对象。

*_Item1*<br/>
第一个源。

*_Item2*<br/>
第二个源。

*_Items*<br/>
其他源。

*_PScheduleGroup*<br/>
在其中计划了 `ScheduleGroup` 消息块的传播任务的 `choice` 对象。 所用 `Scheduler` 对象由该计划组提示。

### <a name="return-value"></a>返回值

一个具有两个或更多输入源的 `choice` 消息块。

## <a name="make_greedy_join"></a>  make_greedy_join

从可选的 `greedy multitype_join` 或 `Scheduler` 及两个或更多输入源构造 `ScheduleGroup` 消息块。

```cpp
template<typename T1, typename T2, typename... Ts>
multitype_join<std::tuple<T1, T2, Ts...>,greedy> make_greedy_join(
    Scheduler& _PScheduler,
    T1 _Item1,
    T2 _Item2,
    Ts... _Items);

template<typename T1, typename T2, typename... Ts>
multitype_join<std::tuple<T1, T2, Ts...>, greedy> make_greedy_join(
    ScheduleGroup& _PScheduleGroup,
    T1 _Item1,
    T2 _Item2,
    Ts... _Items);

template<typename T1, typename T2, typename... Ts>
multitype_join<std::tuple<T1, T2, Ts...>, greedy> make_greedy_join(
    T1 _Item1,
    T2 _Items,
    Ts... _Items);
```

### <a name="parameters"></a>参数

T1<br/>
第一个源的消息块类型。

T2<br/>
第二个源的消息块类型。

*_PScheduler*<br/>
在其中计划了 `Scheduler` 消息块的传播任务的 `multitype_join` 对象。

*_Item1*<br/>
第一个源。

*_Item2*<br/>
第二个源。

*_Items*<br/>
其他源。

*_PScheduleGroup*<br/>
在其中计划了 `ScheduleGroup` 消息块的传播任务的 `multitype_join` 对象。 所用 `Scheduler` 对象由该计划组提示。

### <a name="return-value"></a>返回值

一个具有两个或更多输入源的 `greedy multitype_join` 消息块。

## <a name="make_join"></a>  make_join

从可选的 `non_greedy multitype_join` 或 `Scheduler` 及两个或更多输入源构造 `ScheduleGroup` 消息块。

```cpp
template<typename T1, typename T2, typename... Ts>
multitype_join<std::tuple<T1, T2, Ts...>>
    make_join(
Scheduler& _PScheduler,
    T1 _Item1,
    T2 _Item2,
    Ts... _Items);

template<typename T1, typename T2, typename... Ts>
multitype_join<std::tuple<T1, T2, Ts...>> make_join(
ScheduleGroup& _PScheduleGroup,
    T1 _Item1,
    T2 _Item2,
    Ts... _Items);

template<typename T1, typename T2, typename... Ts>
multitype_join<std::tuple<T1, T2, Ts...>> make_join(
    T1 _Item1,
    T2 _Item2,
    Ts... _Items);
```

### <a name="parameters"></a>参数

T1<br/>
第一个源的消息块类型。

T2<br/>
第二个源的消息块类型。

*_PScheduler*<br/>
在其中计划了 `Scheduler` 消息块的传播任务的 `multitype_join` 对象。

*_Item1*<br/>
第一个源。

*_Item2*<br/>
第二个源。

*_Items*<br/>
其他源。

*_PScheduleGroup*<br/>
在其中计划了 `ScheduleGroup` 消息块的传播任务的 `multitype_join` 对象。 所用 `Scheduler` 对象由该计划组提示。

### <a name="return-value"></a>返回值

一个具有两个或更多输入源的 `non_greedy multitype_join` 消息块。

## <a name="make_task"></a>make_task

用于创建 `task_handle` 对象的工厂方法。

```cpp
template <class _Function>
task_handle<_Function> make_task(const _Function& _Func);
```

### <a name="parameters"></a>参数

*_Function*<br/>
函数对象的类型，将调用该函数对象来执行由 `task_handle` 对象表示的工作。

*_Func*<br/>
将调用以执行 `task_handle` 对象表示的工作的函数。 这可能是 lambda 函子、指向函数的指针，或支持具有签名 `void operator()()`的函数调用运算符版本的任何对象。

### <a name="return-value"></a>返回值

`task_handle` 对象。

### <a name="remarks"></a>备注

当你需要使用 lambda 表达式创建 `task_handle` 对象时，此函数很有用，因为它允许你创建对象，而无需知道 lambda 函子的 true 类型。

## <a name="parallel_buffered_sort"></a>  parallel_buffered_sort

将指定范围中的元素按非降序顺序排列，或根据二元谓词指定的排序条件进行排列。 此函数是基于比较、不稳定的就地排序，因此它与 `std::sort` 在语义上相似，但它需要 `O(n)` 附加空间，并需要待排序的元素进行默认初始化。

```cpp
template<typename _Random_iterator>
inline void parallel_buffered_sort(
    const _Random_iterator& _Begin,
    const _Random_iterator& _End);

template<typename _Allocator,
    typename _Random_iterator>
inline void parallel_buffered_sort(
    const _Random_iterator& _Begin,
    const _Random_iterator& _End);

template<typename _Allocator,
    typename _Random_iterator>
inline void parallel_buffered_sort(
    const _Allocator& _Alloc,
    const _Random_iterator& _Begin,
    const _Random_iterator& _End);

template<typename _Random_iterator,
    typename _Function>
inline void parallel_buffered_sort(
    const _Random_iterator& _Begin,
    const _Random_iterator& _End,
    const _Function& _Func,
    const size_t _Chunk_size = 2048);

template<typename _Allocator,
    typename _Random_iterator,
    typename _Function>
inline void parallel_buffered_sort(
    const _Random_iterator& _Begin,
    const _Random_iterator& _End,
    const _Function& _Func,
    const size_t _Chunk_size = 2048);

template<typename _Allocator,
    typename _Random_iterator,
    typename _Function>
inline void parallel_buffered_sort(
    const _Allocator& _Alloc,
    const _Random_iterator& _Begin,
    const _Random_iterator& _End,
    const _Function& _Func,
    const size_t _Chunk_size = 2048);
```

### <a name="parameters"></a>参数

*_Random_iterator*<br/>
输入范围的迭代器类型。

*_Allocator*<br/>
C++标准库兼容内存分配器的类型。

*_Function*<br/>
二元比较运算符的类型。

*_Begin*<br/>
一种随机访问迭代器，用于寻址要排序的范围中第一个元素的位置。

*_End*<br/>
一种随机访问迭代器，用于定址要排序的范围中最后元素之后下一个元素的位置。

*_Alloc*<br/>
C++标准库兼容内存分配器的实例。

*_Func*<br/>
用户定义的谓词函数对象，定义排序中连续元素要满足的比较条件。 二元谓词采用两个参数并在条件满足时返回 **true** ，不满足时返回 **false**。 该比较器函数必须对序列中的元素对进行严格弱排序。

*_Chunk_size*<br/>
最小大小的区块将拆分为两个区块用于并行执行。

### <a name="remarks"></a>备注

所有重载都需要 `n * sizeof(T)` 额外的空间，其中 `n` 为要排序的元素数，`T` 为元素类型。 在大多数情况下 parallel_buffered_sort 将显示[parallel_sort](concurrency-namespace-functions.md)的性能改进，并且如果有可用内存，则应该通过 parallel_sort 使用它。

如果未提供二元比较运算符 `std::less` 将用作默认值，这需要元素类型来提供运算符 `operator<()`。

如果未提供分配器类型或实例，则使用C++标准库内存分配器 `std::allocator<T>` 来分配缓冲区。

算法将输入范围分为两个区块，然后将每个区块分成两个以并行方式执行的子区块。 可选的参数 `_Chunk_size` 可用于向算法指示它应按顺序处理 < `_Chunk_size` 的大小块。

## <a name="parallel_for"></a>parallel_for

`parallel_for` 循环访问某个索引范围，并在每次迭代时以并行方式执行用户提供的函数。

```cpp
template <typename _Index_type, typename _Function, typename _Partitioner>
void parallel_for(
    _Index_type first,
    _Index_type last,
    _Index_type _Step,
    const _Function& _Func,
    _Partitioner&& _Part);

template <typename _Index_type, typename _Function>
void parallel_for(
    _Index_type first,
    _Index_type last,
    _Index_type _Step,
    const _Function& _Func);

template <typename _Index_type, typename _Function>
void parallel_for(
    _Index_type first,
    _Index_type last,
    const _Function& _Func,
    const auto_partitioner& _Part = auto_partitioner());

template <typename _Index_type, typename _Function>
void parallel_for(
    _Index_type first,
    _Index_type last,
    const _Function& _Func,
    const static_partitioner& _Part);

template <typename _Index_type, typename _Function>
void parallel_for(
    _Index_type first,
    _Index_type last,
    const _Function& _Func,
    const simple_partitioner& _Part);

template <typename _Index_type, typename _Function>
void parallel_for(
    _Index_type first,
    _Index_type last,
    const _Function& _Func,
    affinity_partitioner& _Part);
```

### <a name="parameters"></a>参数

*_Index_type*<br/>
用于迭代的索引的类型。

*_Function*<br/>
将在每次迭代时执行的函数的类型。

*_Partitioner*<br/>
用于对提供的范围进行分区的分区程序的类型。

*first*<br/>
要包含在迭代中的第一个索引。

*last*<br/>
要包含在迭代中的最后一个索引之后的索引。

*_Step*<br/>
从 `first` 循环访问到 `last`时所依据的值。 步骤必须为正数。 如果步骤小于1，则会引发[invalid_argument](../../../standard-library/invalid-argument-class.md) 。

*_Func*<br/>
要在每次迭代时执行的函数。 这可能是 lambda 表达式、函数指针或支持 `void operator()(_Index_type)`的函数调用运算符版本的任何对象。

*_Part*<br/>
对分区程序对象的引用。 参数可以是 `const`[auto_partitioner](auto-partitioner-class.md)`&`、`const`[static_partitioner](static-partitioner-class.md)`&``const`[simple_partitioner](simple-partitioner-class.md)`&` [affinity_partitioner](affinity-partitioner-class.md) 或`&` [affinity_partitioner](affinity-partitioner-class.md) 如果使用了对象，则该引用必须是非常量的左值引用，以便算法可以存储状态以供将来循环使用。

### <a name="remarks"></a>备注

有关详细信息，请参阅[并行算法](../../../parallel/concrt/parallel-algorithms.md)。

## <a name="parallel_for_each"></a>  parallel_for_each

`parallel_for_each` 以并行方式将指定函数应用于某个范围内的每个元素。 除对元素并行执行迭代以及未指定迭代的顺序外，它在语义上等效于 `std` 命名空间中的 `for_each` 函数。 实际自变量 `_Func` 必须支持窗体 `operator()(T)` 的函数调用运算符，其中形式参数 `T` 是正在被循环访问的容器的项类型。

```cpp
template <typename _Iterator, typename _Function>
void parallel_for_each(
    _Iterator first,
    _Iterator last,
    const _Function& _Func);

template <typename _Iterator, typename _Function, typename _Partitioner>
void parallel_for_each(
    _Iterator first,
    _Iterator last,
    const _Function& _Func,
    _Partitioner&& _Part);
```

### <a name="parameters"></a>参数

*_Iterator*<br/>
用于循环访问容器的迭代器的类型。

*_Function*<br/>
将应用于范围中的每个元素的函数的类型。

*_Partitioner*<br/>
*first*<br/>
一个迭代器，用于寻址要包含在并行迭代中的第一个元素的位置。

*last*<br/>
一种迭代器，用于寻址要包含在并行迭代中的最后一个元素之后的位置。

*_Func*<br/>
应用于范围中的每个元素的用户定义函数对象。

*_Part*<br/>
对分区程序对象的引用。 参数可以是 `const`[auto_partitioner](auto-partitioner-class.md)`&`、`const`[static_partitioner](static-partitioner-class.md)`&``const`[simple_partitioner](simple-partitioner-class.md)`&` [affinity_partitioner](affinity-partitioner-class.md) 或`&` [affinity_partitioner](affinity-partitioner-class.md) 如果使用了对象，则该引用必须是非常量的左值引用，以便算法可以存储状态以供将来循环使用。

### <a name="remarks"></a>备注

[auto_partitioner](auto-partitioner-class.md)将用于无显式分区程序的重载。

对于不支持随机访问的迭代器，仅支持[auto_partitioner](auto-partitioner-class.md) 。

有关详细信息，请参阅[并行算法](../../../parallel/concrt/parallel-algorithms.md)。

## <a name="parallel_invoke"></a>parallel_invoke

执行作为参数并行提供的函数对象，并在它们完成执行后进行阻止。 每个函数对象都可以是 lambda 表达式、函数指针或支持具有签名 `void operator()()` 的函数调用运算符的任何对象。

```cpp
template <typename _Function1, typename _Function2>
void parallel_invoke(
    const _Function1& _Func1,
    const _Function2& _Func2);

template <typename _Function1, typename _Function2, typename _Function3>
void parallel_invoke(
    const _Function1& _Func1,
    const _Function2& _Func2,
    const _Function3& _Func3);

template <typename _Function1,
    typename _Function2,
    typename _Function3,
    typename _Function4>
void parallel_invoke(
    const _Function1& _Func1,
    const _Function2& _Func2,
    const _Function3& _Func3,
    const _Function4& _Func4);

template <typename _Function1,
    typename _Function2,
    typename _Function3,
    typename _Function4,
    typename _Function5>
void parallel_invoke(
    const _Function1& _Func1,
    const _Function2& _Func2,
    const _Function3& _Func3,
    const _Function4& _Func4,
    const _Function5& _Func5);

template <typename _Function1,
    typename _Function2,
    typename _Function3,
    typename _Function4,
    typename _Function5,
    typename _Function6>
void parallel_invoke(
    const _Function1& _Func1,
    const _Function2& _Func2,
    const _Function3& _Func3,
    const _Function4& _Func4,
    const _Function5& _Func5,
    const _Function6& _Func6);

template <typename _Function1,
    typename _Function2,
    typename _Function3,
    typename _Function4,
    typename _Function5,
    typename _Function6,
    typename _Function7>
void parallel_invoke(
    const _Function1& _Func1,
    const _Function2& _Func2,
    const _Function3& _Func3,
    const _Function4& _Func4,
    const _Function5& _Func5,
    const _Function6& _Func6,
    const _Function7& _Func7);

template <typename _Function1,
    typename _Function2,
    typename _Function3,
    typename _Function4,
    typename _Function5,
    typename _Function6,
    typename _Function7,
    typename _Function8>
void parallel_invoke(
    const _Function1& _Func1,
    const _Function2& _Func2,
    const _Function3& _Func3,
    const _Function4& _Func4,
    const _Function5& _Func5,
    const _Function6& _Func6,
    const _Function7& _Func7,
    const _Function8& _Func8);

template <typename _Function1,
    typename _Function2,
    typename _Function3,
    typename _Function4,
    typename _Function5,
    typename _Function6,
    typename _Function7,
    typename _Function8,
    typename _Function9>
void parallel_invoke(
    const _Function1& _Func1,
    const _Function2& _Func2,
    const _Function3& _Func3,
    const _Function4& _Func4,
    const _Function5& _Func5,
    const _Function6& _Func6,
    const _Function7& _Func7,
    const _Function8& _Func8,
    const _Function9& _Func9);

template <typename _Function1,
    typename _Function2,
    typename _Function3,
    typename _Function4,
    typename _Function5,
    typename _Function6,
    typename _Function7,
    typename _Function8,
    typename _Function9,
    typename _Function10>
void parallel_invoke(
    const _Function1& _Func1,
    const _Function2& _Func2,
    const _Function3& _Func3,
    const _Function4& _Func4,
    const _Function5& _Func5,
    const _Function6& _Func6,
    const _Function7& _Func7,
    const _Function8& _Func8,
    const _Function9& _Func9,
    const _Function10& _Func10);
```

### <a name="parameters"></a>参数

*_Function1*<br/>
要并行执行的第一个函数对象的类型。

*_Function2*<br/>
要并行执行的第二个函数对象的类型。

*_Function3*<br/>
要并行执行的第三个函数对象的类型。

*_Function4*<br/>
要并行执行的第四个函数对象的类型。

*_Function5*<br/>
要并行执行的第五个函数对象的类型。

*_Function6*<br/>
要并行执行的第六个函数对象的类型。

*_Function7*<br/>
要并行执行的第七个函数对象的类型。

*_Function8*<br/>
要并行执行的第8个函数对象的类型。

*_Function9*<br/>
要并行执行的第九个函数对象的类型。

*_Function10*<br/>
要并行执行的第十个函数对象的类型。

*_Func1*<br/>
要并行执行的第一个函数对象。

*_Func2*<br/>
要并行执行的第二个函数对象。

*_Func3*<br/>
要并行执行的第三个函数对象。

*_Func4*<br/>
要并行执行的第四个函数对象。

*_Func5*<br/>
要并行执行的第五个函数对象。

*_Func6*<br/>
要并行执行的第六个函数对象。

*_Func7*<br/>
要并行执行的第七个函数对象。

*_Func8*<br/>
要并行执行的第8个函数对象。

*_Func9*<br/>
要并行执行的第九个函数对象。

*_Func10*<br/>
要并行执行的第十个函数对象。

### <a name="remarks"></a>备注

请注意，作为参数提供的一个或多个函数对象可能在调用上下文上内联执行。

如果作为参数传递给此函数的一个或多个函数对象引发了异常，则运行时将选择一个此类异常，并将其传播到 `parallel_invoke`调用。

有关详细信息，请参阅[并行算法](../../../parallel/concrt/parallel-algorithms.md)。

## <a name="parallel_radixsort"></a>  parallel_radixsort

使用基数排序算法将指定范围中的元素按非降序顺序排列。 这是一个稳定排序函数，它需要可以投影要按无符号整数键排序的元素的投影函数。 默认初始化对于待排序的元素是必须的。

```cpp
template<typename _Random_iterator>
inline void parallel_radixsort(
    const _Random_iterator& _Begin,
    const _Random_iterator& _End);

template<typename _Allocator, typename _Random_iterator>
inline void parallel_radixsort(
    const _Random_iterator& _Begin,
    const _Random_iterator& _End);

template<typename _Allocator, typename _Random_iterator>
inline void parallel_radixsort(
    const _Allocator& _Alloc,
    const _Random_iterator& _Begin,
    const _Random_iterator& _End);

template<typename _Random_iterator, typename _Function>
inline void parallel_radixsort(
    const _Random_iterator& _Begin,
    const _Random_iterator& _End,
    const _Function& _Proj_func,
    const size_t _Chunk_size = 256* 256);

template<typename _Allocator, typename _Random_iterator,
    typename _Function>
inline void parallel_radixsort(
    const _Random_iterator& _Begin,
    const _Random_iterator& _End,
    const _Function& _Proj_func,
    const size_t _Chunk_size = 256* 256);

template<typename _Allocator,
    typename _Random_iterator,
    typename _Function>
inline void parallel_radixsort(
    const _Allocator& _Alloc,
    const _Random_iterator& _Begin,
    const _Random_iterator& _End,
    const _Function& _Proj_func,
    const size_t _Chunk_size = 256* 256);
```

### <a name="parameters"></a>参数

*_Random_iterator*<br/>
输入范围的迭代器类型。

*_Allocator*<br/>
C++标准库兼容内存分配器的类型。

*_Function*<br/>
投影函数的类型。

*_Begin*<br/>
一种随机访问迭代器，用于寻址要排序的范围中第一个元素的位置。

*_End*<br/>
一种随机访问迭代器，用于定址要排序的范围中最后元素之后下一个元素的位置。

*_Alloc*<br/>
C++标准库兼容内存分配器的实例。

*_Proj_func*<br/>
将元素转换为整数值的用户定义的投影函数对象。

*_Chunk_size*<br/>
最小大小的区块将拆分为两个区块用于并行执行。

### <a name="remarks"></a>备注

所有重载都需要 `n * sizeof(T)` 额外的空间，其中 `n` 为要排序的元素数，`T` 为元素类型。 给定元素时，需要使用带有签名 `I _Proj_func(T)` 的一元投影函子返回密钥，其中 `T` 为元素类型，`I` 是无符号整数类型。

如果未提供投影函数，则仅返回元素的默认投影函数将用于整型类型。 如果在缺少投影函数时元素不是整数类型，则函数将无法进行编译。

如果未提供分配器类型或实例，则使用C++标准库内存分配器 `std::allocator<T>` 来分配缓冲区。

算法将输入范围分为两个区块，然后将每个区块分成两个以并行方式执行的子区块。 可选的参数 `_Chunk_size` 可用于向算法指示它应按顺序处理 < `_Chunk_size` 的大小块。

## <a name="parallel_reduce"></a>  parallel_reduce

通过计算连续部分和来计算指定范围中所有元素的和，或计算类似的通过指定的二元运算（而不是求和运算）获得的连续部分结果的结果（以并行方式）。 `parallel_reduce` 与 `std::accumulate` 在语义上相似，但它需要二元运算是关联的，并需要标识值（而不是初始值）。

```cpp
template<typename _Forward_iterator>
inline typename std::iterator_traits<_Forward_iterator>::value_type parallel_reduce(
    _Forward_iterator _Begin,
    _Forward_iterator _End,
    const typename std::iterator_traits<_Forward_iterator>::value_type& _Identity);

template<typename _Forward_iterator, typename _Sym_reduce_fun>
inline typename std::iterator_traits<_Forward_iterator>::value_type parallel_reduce(
    _Forward_iterator _Begin,
    _Forward_iterator _End,
    const typename std::iterator_traits<_Forward_iterator>::value_type& _Identity,
    _Sym_reduce_fun _Sym_fun);

template<typename _Reduce_type,
    typename _Forward_iterator,
    typename _Range_reduce_fun,
    typename _Sym_reduce_fun>
inline _Reduce_type parallel_reduce(
    _Forward_iterator _Begin,
    _Forward_iterator _End,
    const _Reduce_type& _Identity,
    const _Range_reduce_fun& _Range_fun,
    const _Sym_reduce_fun& _Sym_fun);
```

### <a name="parameters"></a>参数

*_Forward_iterator*<br/>
输入范围的迭代器类型。

*_Sym_reduce_fun*<br/>
对称缩减函数的类型。 这必须是带有签名 `_Reduce_type _Sym_fun(_Reduce_type, _Reduce_type)`的函数类型，其中 _Reduce_type 与缩减的标识类型和结果类型相同。 对于第三个重载，这应该与 `_Range_reduce_fun`的输出类型一致。

*_Reduce_type*<br/>
输入将减少到的类型，可不同于输入元素类型。 返回值和标识值将具有此类型。

*_Range_reduce_fun*<br/>
范围缩减函数的类型。 这必须是签名 `_Reduce_type _Range_fun(_Forward_iterator, _Forward_iterator, _Reduce_type)`的函数类型，_Reduce_type 与缩减的标识类型和结果类型相同。

*_Begin*<br/>
一种输入迭代器，用于寻址要减少的范围内的第一个元素。

*_End*<br/>
一种输入迭代器，用于寻址元素，该元素在要减少的范围内的最后一个元素之外。

*_Identity*<br/>
`_Identity` 的标识值与减少的结果类型和第一个和第二个重载的迭代器的 `value_type` 的类型相同。 对于第三个重载，标识值必须与缩减的结果类型具有相同的类型，但可以不同于迭代器的 `value_type`。 它必须具有适当的值，以便范围缩减运算符 `_Range_fun`（当应用于 `value_type` 类型的单个元素的范围和标识值时）的行为类似于类型 `value_type` 到标识类型的值的类型转换。

*_Sym_fun*<br/>
将在减少的第二个中使用的对称函数。 有关详细信息，请参阅 "备注"。

*_Range_fun*<br/>
将在减少的第一个阶段使用的函数。 有关详细信息，请参阅 "备注"。

### <a name="return-value"></a>返回值

减少的结果。

### <a name="remarks"></a>备注

若要执行并行缩减，函数会根据可用于基础计划程序的工作线程数将范围划分为块区。 减少分两个阶段，第一个阶段在每个区块内进行缩减，第二个阶段在每个区块的部分结果之间进行缩减。

第一个重载要求迭代器的 `value_type``T`与标识值类型以及缩减结果类型相同。 元素类型 T 必须提供运算符 `T T::operator + (T)` 来减小每个块区中的元素。 在第二阶段也使用同一运算符。

第二个重载还要求迭代器的 `value_type` 与标识值类型以及缩减结果类型相同。 提供的二元运算符 `_Sym_fun` 用于两个减少阶段，其中标识值为第一个阶段的初始值。

对于第三个重载，标识值类型必须与缩减结果类型相同，但迭代器的 `value_type` 可能不同于两者。 范围缩减函数 `_Range_fun` 在第一阶段中使用，其标识值为初始值，而二元函数 `_Sym_reduce_fun` 应用于第二个阶段中的子结果。

## <a name="parallel_sort"></a>  parallel_sort

将指定范围中的元素按非降序顺序排列，或根据二元谓词指定的排序条件进行排列。 此函数是基于比较、不稳定的就地排序，因此它与 `std::sort` 在语义上相似。

```cpp
template<typename _Random_iterator>
inline void parallel_sort(
    const _Random_iterator& _Begin,
    const _Random_iterator& _End);

template<typename _Random_iterator,typename _Function>
inline void parallel_sort(
    const _Random_iterator& _Begin,
    const _Random_iterator& _End,
    const _Function& _Func,
    const size_t _Chunk_size = 2048);
```

### <a name="parameters"></a>参数

*_Random_iterator*<br/>
输入范围的迭代器类型。

*_Function*<br/>
二元比较函子的类型。

*_Begin*<br/>
一种随机访问迭代器，用于寻址要排序的范围中第一个元素的位置。

*_End*<br/>
一种随机访问迭代器，用于定址要排序的范围中最后元素之后下一个元素的位置。

*_Func*<br/>
用户定义的谓词函数对象，定义排序中连续元素要满足的比较条件。 二元谓词采用两个参数并在条件满足时返回 **true** ，不满足时返回 **false**。 该比较器函数必须对序列中的元素对进行严格弱排序。

*_Chunk_size*<br/>
要拆分为两个以并行执行的块区的最小大小。

### <a name="remarks"></a>备注

第一个重载使用二进制比较运算符 `std::less`。

第二个重载使用提供的应具有签名 `bool _Func(T, T)`（其中 `T` 是输入范围中元素的类型）的二进制比较器。

算法将输入范围分为两个区块，然后将每个区块分成两个以并行方式执行的子区块。 可选的参数 `_Chunk_size` 可用于向算法指示它应按顺序处理 < `_Chunk_size` 的大小块。

## <a name="parallel_transform"></a>parallel_transform

将指定的函数对象应用于源范围中的每个元素或两个源范围中的一对元素，并将函数对象的返回值复制到目标范围（以并行方式）。 此函数在语义上等效于 `std::transform`。

```cpp
template <typename _Input_iterator1,
    typename _Output_iterator,
    typename _Unary_operator>
_Output_iterator parallel_transform(
    _Input_iterator1 first1,
    _Input_iterator1 last1,
    _Output_iterator _Result,
    const _Unary_operator& _Unary_op,
    const auto_partitioner& _Part = auto_partitioner());

template <typename _Input_iterator1,
    typename _Output_iterator,
    typename _Unary_operator>
_Output_iterator parallel_transform(
    _Input_iterator1 first1,
    _Input_iterator1 last1,
    _Output_iterator _Result,
    const _Unary_operator& _Unary_op,
    const static_partitioner& _Part);

template <typename _Input_iterator1,
    typename _Output_iterator,
    typename _Unary_operator>
_Output_iterator parallel_transform(
    _Input_iterator1 first1,
    _Input_iterator1 last1,
    _Output_iterator _Result,
    const _Unary_operator& _Unary_op,
    const simple_partitioner& _Part);

template <typename _Input_iterator1,
    typename _Output_iterator,
    typename _Unary_operator>
_Output_iterator parallel_transform(
    _Input_iterator1 first1,
    _Input_iterator1 last1,
    _Output_iterator _Result,
    const _Unary_operator& _Unary_op,
    affinity_partitioner& _Part);

template <typename _Input_iterator1,
    typename _Input_iterator2,
    typename _Output_iterator,
    typename _Binary_operator,
    typename _Partitioner>
_Output_iterator parallel_transform(
    _Input_iterator1 first1,
    _Input_iterator1 last1,
    _Input_iterator2
first2,
    _Output_iterator _Result,
    const _Binary_operator& _Binary_op,
    _Partitioner&& _Part);

template <typename _Input_iterator1,
    typename _Input_iterator2,
    typename _Output_iterator,
    typename _Binary_operator>
_Output_iterator parallel_transform(
    _Input_iterator1 first1,
    _Input_iterator1 last1,
    _Input_iterator2
first2,
    _Output_iterator _Result,
    const _Binary_operator& _Binary_op);
```

### <a name="parameters"></a>参数

*_Input_iterator1*<br/>
第一个或唯一输入迭代器的类型。

*_Output_iterator*<br/>
输出迭代器的类型。

*_Unary_operator*<br/>
在输入范围内每个元素上执行的一元函子的类型。

*_Input_iterator2*<br/>
第二个输入迭代器的类型。

*_Binary_operator*<br/>
在两个源范围的元素上成对执行的二元函子的类型。

*_Partitioner*<br/>
*first1*<br/>
一种输入迭代器，用于定址所操作的第一个或唯一的源范围内第一个元素的位置。

*last1*<br/>
一种输入迭代器，用于定址所操作的第一个或唯一的源范围内最后元素之后下一个元素的位置。

*_Result*<br/>
一种输出迭代器，用于定址目标范围内第一个元素的位置。

*_Unary_op*<br/>
用户定义的应用于源范围内每个元素的一元函数对象。

*_Part*<br/>
对分区程序对象的引用。 参数可以是 `const`[auto_partitioner](auto-partitioner-class.md)`&`、`const`[static_partitioner](static-partitioner-class.md)`&``const`[simple_partitioner](simple-partitioner-class.md)`&` [affinity_partitioner](affinity-partitioner-class.md) 或`&` [affinity_partitioner](affinity-partitioner-class.md) 如果使用了对象，则该引用必须是非常量的左值引用，以便算法可以存储状态以供将来循环使用。

*first2*<br/>
一种输入迭代器，用于定址所操作的第二个源范围内第一个元素的位置。

*_Binary_op*<br/>
用户定义的按向前顺序成对应用于两个源范围的二元函数对象。

### <a name="return-value"></a>返回值

一种输出迭代器，用于寻址接收通过函数对象转换的输出元素的目标范围内最后元素之后下一个元素的位置。

### <a name="remarks"></a>备注

[auto_partitioner](auto-partitioner-class.md)将用于无显式分区程序参数的重载。

对于不支持随机访问的迭代器，仅支持[auto_partitioner](auto-partitioner-class.md) 。

采用参数 `_Unary_op` 的重载将一元函子应用于输入范围内的每个元素，从而将输入范围转换为输出范围。 `_Unary_op` 必须支持带有签名 `operator()(T)` 的函数调用运算符，签名中的 `T` 是要循环访问的范围的值类型。

采用参数 `_Binary_op` 的重载将二元函子分别应用于第一个输入范围内的一个元素和第二个输入范围内的一个元素，从而将两个输入范围转换为输出范围。 `_Binary_op` 必须支持具有签名 `operator()(T, U)` 的函数调用运算符，签名中的 `T`, `U` 是两个输入迭代器的值类型。

有关详细信息，请参阅[并行算法](../../../parallel/concrt/parallel-algorithms.md)。

## <a name="receive"></a>收

常规接收实现，允许上下文仅等待来自一个源的数据并筛选所接受的值。

```cpp
template <class T>
T receive(
    _Inout_ ISource<T>* _Src,
    unsigned int _Timeout = COOPERATIVE_TIMEOUT_INFINITE);

template <class T>
T receive(
    _Inout_ ISource<T>* _Src,
    typename ITarget<T>::filter_method const& _Filter_proc,
    unsigned int _Timeout = COOPERATIVE_TIMEOUT_INFINITE);

template <class T>
T receive(
    ISource<T>& _Src,
    unsigned int _Timeout = COOPERATIVE_TIMEOUT_INFINITE);

template <class T>
T receive(
    ISource<T>& _Src,
    typename ITarget<T>::filter_method const& _Filter_proc,
    unsigned int _Timeout = COOPERATIVE_TIMEOUT_INFINITE);
```

### <a name="parameters"></a>参数

*T*<br/>
负载类型。

*_Src*<br/>
指向需要数据的源的指针或引用。

*_Timeout*<br/>
此方法应为的数据的最大时间（以毫秒为单位）。

*_Filter_proc*<br/>
确定是否应接受消息的筛选器函数。

### <a name="return-value"></a>返回值

负载类型的源中的值。

### <a name="remarks"></a>备注

如果参数 `_Timeout` 的值不是常量 `COOPERATIVE_TIMEOUT_INFINITE`，则在收到消息之前指定的时间长度过期时，将引发异常[operation_timed_out](operation-timed-out-class.md) 。 如果要使零长度超时，则应使用[try_receive](concurrency-namespace-functions.md)函数，而不是使用 `0` （零）的超时值调用 `receive`，因为这样会更有效，且不会引发超时异常。

有关详细信息，请参阅[消息传递函数](../../../parallel/concrt/message-passing-functions.md)。

## <a name="run_with_cancellation_token"></a>run_with_cancellation_token

在给定取消标记的上下文中立即同步执行函数对象。

```cpp
template<typename _Function>
void run_with_cancellation_token(
    const _Function& _Func,
    cancellation_token _Ct);
```

### <a name="parameters"></a>参数

*_Function*<br/>
将会调用的函数对象的类型。

*_Func*<br/>
将会执行的函数对象。 此对象必须支持具有 void(void) 签名的函数调用运算符。

*_Ct*<br/>
将控制函数对象隐式取消的取消标记。 如果希望避免执行的函数被要取消的父任务组隐式取消，请使用 `cancellation_token::none()`。

### <a name="remarks"></a>备注

取消 `cancellation_token` 时，将触发函数对象中的任何中断点。 如果父任务具有不同的标记或没有标记，则显式标记 `_Ct` 会将此 `_Func` 从父任务取消中隔离出来。

## <a name="send"></a>发送

同步发送操作，它会一直等待，直到目标接受或拒绝消息。

```cpp
template <class T>
bool send(_Inout_ ITarget<T>* _Trg, const T& _Data);

template <class T>
bool send(ITarget<T>& _Trg, const T& _Data);
```

### <a name="parameters"></a>参数

*T*<br/>
负载类型。

*_Trg*<br/>
指向向其发送数据的目标的指针或引用。

*_Data*<br/>
对要发送的数据的引用。

### <a name="return-value"></a>返回值

如果接受消息，**则为 true** ; 否则为**false** 。

### <a name="remarks"></a>备注

有关详细信息，请参阅[消息传递函数](../../../parallel/concrt/message-passing-functions.md)。

## <a name="set_ambient_scheduler"></a>  set_ambient_scheduler

```cpp
inline void set_ambient_scheduler(std::shared_ptr<::Concurrency::scheduler_interface> _Scheduler);
```

### <a name="parameters"></a>参数

*_Scheduler*<br/>
要设置的环境计划程序。

## <a name="set_task_execution_resources"></a>  set_task_execution_resources

将并发运行时内部工作线程使用的执行资源限制为指定的关联集。

仅在创建资源管理器之前，或在两个资源管理器生存期之间调用此方法才是有效的。 只要资源管理器在调用时不存在，就可以多次调用它。 设置关联限制后，它仍然有效，直到对 `set_task_execution_resources` 方法的下一次有效调用。

提供的关联掩码不需要是进程关联掩码的子集。 如果需要，将更新过程关联。

```cpp
void __cdecl set_task_execution_resources(
    DWORD_PTR _ProcessAffinityMask);

void __cdecl set_task_execution_resources(
    unsigned short count,
    PGROUP_AFFINITY _PGroupAffinity);
```

### <a name="parameters"></a>参数

*_ProcessAffinityMask*<br/>
限于并发运行时辅助线程使用的关联掩码。 仅在想要将并发运行时限制为当前处理器组的一部分时，在具有 64 个以上硬件线程的系统上使用此方法。 通常，应使用接受将组关联的数组作为参数的方法版本，以限制具有 64 个以上硬件线程的计算机上的关联。

*计数*<br/>
数组中参数 `GROUP_AFFINITY` 指定的 `_PGroupAffinity` 项的数目。

*_PGroupAffinity*<br/>
`GROUP_AFFINITY` 项的数组。

### <a name="remarks"></a>备注

如果资源管理器在调用时存在，则方法会引发[invalid_operation](invalid-operation-class.md)异常，如果指定的关联导致一组空的资源，则会引发[invalid_argument](../../../standard-library/invalid-argument-class.md)异常。

应仅在具有 Windows 7 或更高版本的操作系统上使用接受组关联作为参数的方法版本。 否则，会引发[invalid_operation](invalid-operation-class.md)异常。

在调用此方法后以编程方式修改进程关联将不会导致资源管理器重新计算其限制的相关性。 因此，对进程关联的所有更改都应在调用此方法之前进行。

## <a name="swap"></a>  swap

交换两个 `concurrent_vector` 对象的元素。

```cpp
template<typename T, class _Ax>
inline void swap(
    concurrent_vector<T, _Ax>& _A,
    concurrent_vector<T, _Ax>& _B);
```

### <a name="parameters"></a>参数

*T*<br/>
并发向量中存储的元素的数据类型。

*_Ax*<br/>
并发向量的分配器类型。

*_A*<br/>
要与并发向量 `_B`的元素进行交换的并发向量。

*_B*<br/>
提供要交换的元素的并发向量，或其元素将与并发向量 `_A`的元素进行交换的向量。

### <a name="remarks"></a>备注

模板函数是容器类 `concurrent_vector` 的算法，用于执行成员函数 `_A`。 [concurrent_vector：： swap](concurrent-vector-class.md#swap)（`_B`）。 这些是由编译器进行的函数模板部分排序的实例。 模板函数以此种方式重载时，模板与函数调用的匹配并不唯一，随后编译器会选择此模板函数的最专用化版本。 算法类中的模板函数 `template <class T> void swap(T&, T&)`的常规版本按赋值方式工作，并且是一项慢速操作。 每个容器中的专用化版本速度快很多，因为专用化版本可适用于容器类的内部表示形式。

此方法不是并发安全方法。 在调用此方法时，必须确保没有其他线程在任一并发矢量上执行操作。

## <a name="task_from_exception"></a>  task_from_exception

```cpp
template<typename _TaskType, typename _ExType>
task<_TaskType> task_from_exception(
    _ExType _Exception,
    const task_options& _TaskOptions = task_options());
```

### <a name="parameters"></a>参数

*_TaskType*<br/>

*_ExType*<br/>

*_Exception*<br/>

*_TaskOptions*<br/>

### <a name="return-value"></a>返回值

## <a name="task_from_result"></a>  task_from_result

```cpp
template<typename T>
task<T> task_from_result(
    T _Param,
    const task_options& _TaskOptions = task_options());

inline task<bool> task_from_result(ool _Param);

inline task<void> task_from_result(
    const task_options& _TaskOptions = task_options());
```

### <a name="parameters"></a>参数

*T*<br/>

*_Param*<br/>

*_TaskOptions*<br/>

### <a name="return-value"></a>返回值

## <a name="trace_agents_register_name"></a>  Trace_agents_register_name

在 ETW 跟踪中将给定名称关联到消息块或代理。

```cpp
template <class T>
void Trace_agents_register_name(
    _Inout_ T* _PObject,
    _In_z_ const wchar_t* _Name);
```

### <a name="parameters"></a>参数

*T*<br/>
对象的类型。 这通常是消息块或代理。

*_PObject*<br/>
指向在跟踪中命名的消息块或代理的指针。

*_Name*<br/>
给定对象的名称。

## <a name="try_receive"></a>  try_receive

常规尝试-接收实现，允许上下文仅查找来自一个源的数据并筛选所接受的值。 如果数据未就绪，则方法将返回**false**。

```cpp
template <class T>
bool try_receive(_Inout_ ISource<T>* _Src, T& _value);

template <class T>
bool try_receive(
    _Inout_ ISource<T>* _Src,
    T& _value,
    typename ITarget<T>::filter_method const& _Filter_proc);

template <class T>
bool try_receive(ISource<T>& _Src, T& _value);

template <class T>
bool try_receive(
    ISource<T>& _Src,
    T& _value,
    typename ITarget<T>::filter_method const& _Filter_proc);
```

### <a name="parameters"></a>参数

*T*<br/>
负载类型

*_Src*<br/>
指向需要数据的源的指针或引用。

*_value*<br/>
对将放置结果的位置的引用。

*_Filter_proc*<br/>
确定是否应接受消息的筛选器函数。

### <a name="return-value"></a>返回值

一个 `bool` 值，该值指示是否将有效负载置于 `_value`。

### <a name="remarks"></a>备注

有关详细信息，请参阅[消息传递函数](../../../parallel/concrt/message-passing-functions.md)。

## <a name="wait"></a>再

将当前上下文暂停指定的一段时间。

```cpp
void __cdecl wait(unsigned int _Milliseconds);
```

### <a name="parameters"></a>参数

*_Milliseconds*<br/>
当前上下文应该暂停的毫秒数。 如果 `_Milliseconds` 参数设置为值 `0`，则当前上下文应在继续之前执行其他可运行的上下文。

### <a name="remarks"></a>备注

如果在并发运行时计划程序上下文中调用此方法，则计划程序将查找要在基础资源上运行的其他上下文。 由于计划程序在本质上是合作的，此上下文不会正好在指定的毫秒数后继续。 如果计划程序正忙于执行不协作产生计划程序的其他任务，那么等待时间可能是无限期。

## <a name="when_all"></a>when_all

创建一个任务，在作为自变量提供的所有任务成功完成后，此任务将成功完成。

```cpp
template <typename _Iterator>
auto when_all(
    _Iterator _Begin,
    _Iterator _End,
    const task_options& _TaskOptions = task_options()) ->
    decltype (details::_WhenAllImpl<typename std::iterator_traits<_Iterator>::value_type::result_type,
    _Iterator>::_Perform(_TaskOptions, _Begin,  _End));
```

### <a name="parameters"></a>参数

*_Iterator*<br/>
输入迭代器的类型。

*_Begin*<br/>
要合并到结果任务的元素范围中第一个元素的位置。

*_End*<br/>
超出要合并到结果任务的元素范围的第一个元素的位置。

*_TaskOptions*<br/>
`task_options` 对象。

### <a name="return-value"></a>返回值

在所有输入任务成功完成后成功完成的任务。 如果输入任务的类型为 `T`，则此函数的输出将为 `task<std::vector<T>>`。 如果输入任务的类型为 `void`，则输出任务也将是 `task<void>`。

### <a name="remarks"></a>备注

`when_all` 是生成 `task` 作为其结果的的非阻止函数。 与[任务：： wait](task-class.md#wait)不同，在 ASTA （应用程序 STA）线程上的 UWP 应用中调用此函数是安全的。

如果其中一个任务被取消或引发异常，则返回的任务将在 "已取消" 状态下提前完成，如果发生这种情况，则会在对该任务调用[task：： get](task-class.md#get)或 `task::wait` 时引发异常。

有关详细信息，请参阅[任务并行](../../../parallel/concrt/task-parallelism-concurrency-runtime.md)。

## <a name="when_any"></a>  when_any

创建一个任务，在作为参数提供的任何任务成功完成后，此任务将成功完成。

```cpp
template<typename _Iterator>
auto when_any(
    _Iterator _Begin,
    _Iterator _End,
    const task_options& _TaskOptions = task_options())
    -> decltype (
        details::_WhenAnyImpl<
            typename std::iterator_traits<_Iterator>::value_type::result_type,
            _Iterator>::_Perform(_TaskOptions, _Begin, _End));

template<typename _Iterator>
auto when_any(
    _Iterator _Begin,
    _Iterator _End,
    cancellation_token _CancellationToken)
       -> decltype (
           details::_WhenAnyImpl<
               typename std::iterator_traits<_Iterator>::value_type::result_type,
               _Iterator>::_Perform(_CancellationToken._GetImplValue(), _Begin, _End));
```

### <a name="parameters"></a>参数

*_Iterator*<br/>
输入迭代器的类型。

*_Begin*<br/>
要合并到结果任务的元素范围中第一个元素的位置。

*_End*<br/>
超出要合并到结果任务的元素范围的第一个元素的位置。

*_TaskOptions*<br/>
*_CancellationToken*<br/>
控制返回的任务的取消的取消标记。 如果未提供取消标记，则结果任务将接收到导致任务完成的任务取消标记。

### <a name="return-value"></a>返回值

在任意输入任务成功完成后成功完成的任务。 如果输入任务的类型为 `T`，则此函数的输出将为 `task<std::pair<T, size_t>>>`，其中的 pair 的第一个元素是正在完成的任务的结果，第二个元素是已完成的任务的索引。 如果输入任务的类型为 `void`，则输出为 `task<size_t>`，其中的结果是正在完成的任务的索引。

### <a name="remarks"></a>备注

`when_any` 是生成 `task` 作为其结果的的非阻止函数。 与[任务：： wait](task-class.md#wait)不同，在 ASTA （应用程序 STA）线程上的 UWP 应用中调用此函数是安全的。

有关详细信息，请参阅[任务并行](../../../parallel/concrt/task-parallelism-concurrency-runtime.md)。

## <a name="see-also"></a>请参阅

[并发命名空间](concurrency-namespace.md)
