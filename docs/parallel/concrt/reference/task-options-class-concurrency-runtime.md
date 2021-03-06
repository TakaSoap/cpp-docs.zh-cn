---
title: task_options 类（并发运行时）
ms.date: 11/04/2016
f1_keywords:
- ppltasks/concurrency::task_options
ms.assetid: f93d146b-70f7-46ec-8c2f-c33b8bb0af69
ms.openlocfilehash: 5f60a07d709a79f3ce4845c8fbd1c40cb2ee7328
ms.sourcegitcommit: a8ef52ff4a4944a1a257bdaba1a3331607fb8d0f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/11/2020
ms.locfileid: "77142536"
---
# <a name="task_options-class-concurrency-runtime"></a>task_options 类（并发运行时）

表示可用于创建任务的选项

## <a name="syntax"></a>语法

```cpp
class task_options;
```

## <a name="members"></a>Members

### <a name="public-constructors"></a>公共构造函数

|名称|说明|
|----------|-----------------|
|[task_options：： task_options 构造函数（并发运行时）](#ctor)|已重载。 任务创建选项的默认列表|

### <a name="public-methods"></a>公共方法

|名称|说明|
|----------|-----------------|
|[task_options：： get_cancellation_token 方法（并发运行时）](#get_cancellation_token)|返回取消标记|
|[task_options：： get_continuation_context 方法（并发运行时）](#get_continuation_context)|返回持续上下文|
|[task_options：： get_scheduler 方法（并发运行时）](#get_scheduler)|返回计划程序|
|[task_options：： has_cancellation_token 方法（并发运行时）](#has_cancellation_token)|指示用户是否指定了取消标记|
|[task_options：： has_scheduler 方法（并发运行时）](#has_scheduler)|指示用户是否指定了计划程序|
|[task_options：： set_cancellation_token 方法（并发运行时）](#set_cancellation_token)|在选项中设置给定的标记|
|[task_options：： set_continuation_context 方法（并发运行时）](#set_continuation_context)|在选项中设置给定的持续上下文|

## <a name="inheritance-hierarchy"></a>继承层次结构

`task_options`

## <a name="requirements"></a>要求

**标头：** ppltasks。h

**命名空间：** 并发

## <a name="get_cancellation_token"></a>task_options：： get_cancellation_token 方法（并发运行时）

返回取消标记

```cpp
cancellation_token get_cancellation_token() const;
```

### <a name="return-value"></a>返回值

## <a name="get_continuation_context"></a>task_options：： get_continuation_context 方法（并发运行时）

返回持续上下文

```cpp
task_continuation_context get_continuation_context() const;
```

### <a name="return-value"></a>返回值

## <a name="get_scheduler"></a>task_options：： get_scheduler 方法（并发运行时）

返回计划程序

```cpp
scheduler_ptr get_scheduler() const;
```

### <a name="return-value"></a>返回值

## <a name="has_cancellation_token"></a>task_options：： has_cancellation_token 方法（并发运行时）

指示用户是否指定了取消标记

```cpp
bool has_cancellation_token() const;
```

### <a name="return-value"></a>返回值

## <a name="has_scheduler"></a>task_options：： has_scheduler 方法（并发运行时）

指示用户是否指定了计划程序

```cpp
bool has_scheduler() const;
```

### <a name="return-value"></a>返回值

## <a name="set_cancellation_token"></a>task_options：： set_cancellation_token 方法（并发运行时）

在选项中设置给定的标记

```cpp
void set_cancellation_token(cancellation_token _Token);
```

### <a name="parameters"></a>参数

`_Token`

## <a name="set_continuation_context"></a>task_options：： set_continuation_context 方法（并发运行时）

在选项中设置给定的持续上下文

```cpp
void set_continuation_context(task_continuation_context _ContinuationContext);
```

### <a name="parameters"></a>参数

`_ContinuationContext`

## <a name="ctor"></a>task_options：： task_options 构造函数（并发运行时）

任务创建选项的默认列表

```cpp
task_options();

task_options(
    cancellation_token _Token);

task_options(
    task_continuation_context _ContinuationContext);

task_options(
    cancellation_token _Token,
    task_continuation_context _ContinuationContext);

template<typename _SchedType>
task_options(
    std::shared_ptr<_SchedType> _Scheduler);

task_options(
    scheduler_interface& _Scheduler);

task_options(
    scheduler_ptr _Scheduler);

task_options(
    const task_options& _TaskOptions);
```

### <a name="parameters"></a>参数

`_SchedType`

`_Token`

`_ContinuationContext`

`_Scheduler`

`_TaskOptions`

## <a name="see-also"></a>另请参阅

[并发命名空间](concurrency-namespace.md)
