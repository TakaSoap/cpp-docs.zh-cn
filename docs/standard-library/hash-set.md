---
title: '&lt;hash_set&gt;'
ms.date: 11/04/2016
f1_keywords:
- <hash_set>
- std::<hash_set>
helpviewer_keywords:
- hash_set header
ms.assetid: 6b556967-c808-4869-9b4d-f9e030864435
ms.openlocfilehash: 00ca476816213d38b3c50c64e0978e65ac1a5ea1
ms.sourcegitcommit: 590e488e51389066a4da4aa06d32d4c362c23393
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/21/2019
ms.locfileid: "72687949"
---
# <a name="lthash_setgt"></a>&lt;hash_set&gt;

> [!NOTE]
> 此标头已废弃不用。 替代项为 [<unordered_set>](../standard-library/unordered-set.md)。

定义容器类模板 hash_set 和 hash_multiset 及其支持的模板。

## <a name="syntax"></a>语法

```cpp
#include <hash_set>
```

## <a name="remarks"></a>备注

### <a name="operators"></a>运算符

|Hash_set 版本|Hash_multiset 版本|描述|
|-----------------------|----------------------------|-----------------|
|[operator!= (hash_set)](../standard-library/hash-set-operators.md#op_neq)|[operator!= (hash_multiset)](../standard-library/hash-set-operators.md#op_neq)|测试运算符左侧的 hash_set 或 hash_multiset 对象是否不等于右侧的 hash_set 或 hash_multiset 对象。|
|[operator== (hash_set)](../standard-library/hash-set-operators.md#op_eq_eq)|[operator== (hash_multiset)](../standard-library/hash-set-operators.md#op_eq_eq)|测试运算符左侧的 hash_set 或 hash_multiset 对象是否等于右侧的 hash_set 或 hash_multiset 对象。|

### <a name="specialized-template-functions"></a>专用化模板函数

|Hash_set 版本|Hash_multiset 版本|描述|
|-----------------------|----------------------------|-----------------|
|[swap (hash_set)](../standard-library/hash-set-functions.md#swap)|[swap (hash_multiset)](../standard-library/hash-set-functions.md#swap_hash_multiset)|交换两个 hash_set 或 hash_multiset 的元素。|

### <a name="classes"></a>类

|实例|描述|
|-|-|
|[hash_compare 类](../standard-library/hash-compare-class.md)|描述一个对象，该对象可由任何哈希关联容器（hash_map、hash_multimap、hash_set 或 hash_multiset）用于默认 `Traits` 参数对象，以对其所包含的元素进行排序和哈希处理。|
|[hash_set 类](../standard-library/hash-set-class.md)|用于存储和快速检索集合中的数据，此集合中包含的元素值是唯一的并且用作键值。|
|[hash_multiset 类](../standard-library/hash-multiset-class.md)|用于存储和快速检索集合中的数据，此集合中包含的元素值是唯一的并且用作键值。|

## <a name="see-also"></a>请参阅

[头文件引用](../standard-library/cpp-standard-library-header-files.md)\
[C++ 标准库中的线程安全](../standard-library/thread-safety-in-the-cpp-standard-library.md)\
[C++ 标准库参考](../standard-library/cpp-standard-library-reference.md)
