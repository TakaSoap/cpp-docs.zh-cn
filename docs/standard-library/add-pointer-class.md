---
title: add_pointer 类
ms.date: 11/04/2016
f1_keywords:
- type_traits/std::add_pointer
helpviewer_keywords:
- add_pointer class
- add_pointer
ms.assetid: d8095cb0-6578-4143-b78f-87f82485298c
ms.openlocfilehash: 759867a542aa128755ba31e090984eb5b3fe6963
ms.sourcegitcommit: 0dcab746c49f13946b0a7317fc9769130969e76d
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/24/2019
ms.locfileid: "68456548"
---
# <a name="addpointer-class"></a>add_pointer 类

从指定类型创建指向类型的指针。

## <a name="syntax"></a>语法

```cpp
template <class T>
struct add_pointer;

template <class T>
using add_pointer_t = typename add_pointer<T>::type;
```

### <a name="parameters"></a>参数

*关心*\
要修改的类型。

## <a name="remarks"></a>备注

成员**typedef** `type`将与相同的类型命名`remove_reference<T>::type*`为。 别名`add_pointer_t`是访问成员**typedef** `type`的快捷方式。

因为从引用创建指针是无效的，所以 `add_pointer` 将从指定类型中移除引用（如果有），然后再创建指向类型的指针。 因此，你可以将某一类型用于 `add_pointer`，而不必考虑该类型是否是引用。

## <a name="example"></a>示例

下面的示例演示某一类型的 `add_pointer` 与指向该类型的指针相同。

```cpp
#include <type_traits>
#include <iostream>

int main()
{
    std::add_pointer_t<int> *p = (int **)0;

    p = p;  // to quiet "unused" warning
    std::cout << "add_pointer_t<int> == "
        << typeid(*p).name() << std::endl;

    return (0);
}
```

```Output
add_pointer_t<int> == int *
```

## <a name="requirements"></a>要求

**标头：** \<type_traits>

**命名空间：** std

## <a name="see-also"></a>请参阅

[<type_traits>](../standard-library/type-traits.md)\
[remove_pointer 类](../standard-library/remove-pointer-class.md)
