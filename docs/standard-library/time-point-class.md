---
title: time_point 类
ms.date: 03/27/2019
f1_keywords:
- chrono/std::chrono::time_point
- chrono/std::chrono::time_point::time_point
- chrono/std::chrono::time_point::max
- chrono/std::chrono::time_point::min
- chrono/std::chrono::time_point::time_since_epoch
ms.assetid: 18be1e52-57b9-489a-8a9b-f58894f0aaad
helpviewer_keywords:
- std::chrono [C++], time_point
ms.openlocfilehash: 4511c7b2d8629f1a052137c7997daf5913c976ab
ms.sourcegitcommit: 0dcab746c49f13946b0a7317fc9769130969e76d
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/24/2019
ms.locfileid: "68459992"
---
# <a name="timepoint-class"></a>time_point 类

一个 `time_point`，描述表示时间点的类型。 它包含类型为 [duration](../standard-library/duration-class.md) 的对象，用于存储运行时间，因为由模板参数 `Clock` 表示 epoch。

## <a name="syntax"></a>语法

```cpp
template <class Clock,
    class Duration = typename Clock::duration>
class time_point;
```

## <a name="members"></a>成员

### <a name="public-typedefs"></a>公共 Typedef

|name|描述|
|----------|-----------------|
|`time_point::clock`|模板参数 `Clock` 的同义词。|
|`time_point::duration`|模板参数 `Duration` 的同义词。|
|`time_point::period`|嵌套类型名 `duration::period` 的同义词。|
|`time_point::rep`|嵌套类型名 `duration::rep` 的同义词。|

### <a name="public-constructors"></a>公共构造函数

|名称|描述|
|----------|-----------------|
|[time_point](#time_point)|构造 `time_point` 对象。|

### <a name="public-methods"></a>公共方法

|名称|描述|
|----------|-----------------|
|[max](#max)|指定 `time_point::ref` 的上限值。|
|[min](#min)|指定 `time_point::ref` 的下限值。|
|[time_since_epoch](#time_since_epoch)|返回存储的 `duration` 值。|

### <a name="public-operators"></a>公共运算符

|名称|描述|
|----------|-----------------|
|[time_point::operator+=](#op_add_eq)|将指定的值添加到存储持续时间。|
|[time_point::operator-=](#operator-_eq)|从存储的持续时间减去指定的值。|

## <a name="requirements"></a>要求

**标头:** \<chrono >

**命名空间：** std::chrono

## <a name="max"></a>  time_point::max

返回类型 `time_point::ref` 的值上限的静态方法。

```cpp
static constexpr time_point max();
```

### <a name="return-value"></a>返回值

实际上，返回 `time_point(duration::max())`。

## <a name="min"></a>  time_point::min

返回类型值下限的静态方法`time_point::ref`。

```cpp
static constexpr time_point min();
```

### <a name="return-value"></a>返回值

实际上，返回 `time_point(duration::min())`。

## <a name="op_add_eq"></a>  time_point::operator+=

将指定的值添加到存储[持续时间](../standard-library/duration-class.md)值。

```cpp
time_point& operator+=(const duration& Dur);
```

### <a name="parameters"></a>参数

*工期*\
一个 `duration` 对象。

### <a name="return-value"></a>返回值

相加后执行 `time_point` 对象。

## <a name="operator-_eq"></a>  time_point::operator-=

从存储[持续时间](../standard-library/duration-class.md)值减去指定的值。

```cpp
time_point& operator-=(const duration& Dur);
```

### <a name="parameters"></a>参数

*工期*\
一个 `duration` 对象。

### <a name="return-value"></a>返回值

相减后执行 `time_point` 对象。

## <a name="time_point"></a>  time_point::time_point 构造函数

构造 `time_point` 对象。

```cpp
constexpr time_point();

constexpr explicit time_point(const duration& Dur);

template <class Duration2>
constexpr time_point(const time_point<clock, Duration2>& Tp);
```

### <a name="parameters"></a>参数

*工期*\
[duration](../standard-library/duration-class.md) 对象。

*Tp*\
一个 `time_point` 对象。

### <a name="remarks"></a>备注

第一个构造函数构造一个对象，该对象的存储 `duration` 值等于 [duration::zero](../standard-library/duration-class.md#zero)。

第二个构造函数将构造一个其存储的 duration 值等于 "*工期*" 的对象。 除非`is_convertible<Duration2, duration>`保留为 true, 否则第二个构造函数不参与重载决策。 有关详细信息，请参阅 [<type_traits>](../standard-library/type-traits.md)。

第三个构造函数使用 `Tp.time_since_epoch()` 来初始化其`duration` 值。

## <a name="time_since_epoch"></a>  time_point::time_since_epoch

检索存储[持续时间](../standard-library/duration-class.md)值。

```cpp
constexpr duration time_since_epoch() const;
```

## <a name="see-also"></a>请参阅

[头文件引用](../standard-library/cpp-standard-library-header-files.md)\
[\<chrono>](../standard-library/chrono.md)
