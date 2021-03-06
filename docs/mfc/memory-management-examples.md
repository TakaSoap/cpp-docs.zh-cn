---
title: 内存管理：示例
ms.date: 11/04/2016
helpviewer_keywords:
- objects [MFC], memory allocation
- data structures [MFC]
- arrays [MFC], allocating resources
- objects [MFC], allocating memory
- data structures [MFC], allocating memory
- examples [MFC], memory allocation
- heap allocation [MFC], examples
- memory allocation [MFC], arrays
- MFC, memory management
- struct memory allocation [MFC]
- types [MFC], memory allocation
- memory allocation [MFC], objects
- memory allocation [MFC], examples
- arrays [MFC], memory management
- frame allocation [MFC]
- memory allocation [MFC], data structures
ms.assetid: f10240f8-b698-4c83-9288-97a54318930b
ms.openlocfilehash: 5ed50bfba03f29fdd16e6f615b193109656f3ce6
ms.sourcegitcommit: 0ab61bc3d2b6cfbd52a16c6ab2b97a8ea1864f12
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62352159"
---
# <a name="memory-management-examples"></a>内存管理：示例

本文介绍了 MFC 如何为每个内存分配的三个典型执行了帧分配和堆分配：

- [一个字节数组](#_core_allocation_of_an_array_of_bytes)

- [一种数据结构](#_core_allocation_of_a_data_structure)

- [一个对象](#_core_allocation_of_an_object)

##  <a name="_core_allocation_of_an_array_of_bytes"></a> 分配的字节数组

#### <a name="to-allocate-an-array-of-bytes-on-the-frame"></a>若要分配的帧上的字节数组

1. 定义数组，如下面的代码所示。 自动删除数组和数组变量退出其作用域内时，将回收其内存。

   [!code-cpp[NVC_MFC_Utilities#1](../mfc/codesnippet/cpp/memory-management-examples_1.cpp)]

#### <a name="to-allocate-an-array-of-bytes-or-any-primitive-data-type-on-the-heap"></a>若要在堆上分配的字节数 （或任何基元数据类型） 数组

1. 使用**新**运算符与在此示例中所示的数组语法：

   [!code-cpp[NVC_MFC_Utilities#2](../mfc/codesnippet/cpp/memory-management-examples_2.cpp)]

#### <a name="to-deallocate-the-arrays-from-the-heap"></a>若要解除分配的堆中的数组

1. 使用**删除**运算符，如下所示：

   [!code-cpp[NVC_MFC_Utilities#3](../mfc/codesnippet/cpp/memory-management-examples_3.cpp)]

##  <a name="_core_allocation_of_a_data_structure"></a> 分配的数据结构

#### <a name="to-allocate-a-data-structure-on-the-frame"></a>若要分配的帧上的数据结构

1. 定义结构变量，如下所示：

   [!code-cpp[NVC_MFC_Utilities#4](../mfc/codesnippet/cpp/memory-management-examples_4.cpp)]

   退出其作用域内时回收结构占用的内存。

#### <a name="to-allocate-data-structures-on-the-heap"></a>若要分配堆上的数据结构

1. 使用**新**来分配堆上的数据结构和**删除**将其解除分配，如以下示例所示：

   [!code-cpp[NVC_MFC_Utilities#5](../mfc/codesnippet/cpp/memory-management-examples_5.cpp)]

##  <a name="_core_allocation_of_an_object"></a> 一个对象的分配

#### <a name="to-allocate-an-object-on-the-frame"></a>若要在帧上分配对象

1. 对象声明，如下所示：

   [!code-cpp[NVC_MFC_Utilities#6](../mfc/codesnippet/cpp/memory-management-examples_6.cpp)]

   该对象退出其作用域，则会自动调用对象的析构函数。

#### <a name="to-allocate-an-object-on-the-heap"></a>若要在堆上分配对象

1. 使用**新**运算符，此运算符返回指向对象的指针，以分配堆上的对象。 使用**删除**运算符将其删除。

   下面的堆和帧示例假定，`CPerson`构造函数不采用任何参数。

   [!code-cpp[NVC_MFC_Utilities#7](../mfc/codesnippet/cpp/memory-management-examples_7.cpp)]

   如果为参数`CPerson`构造函数是一个指向**char**，帧分配的语句是：

   [!code-cpp[NVC_MFC_Utilities#8](../mfc/codesnippet/cpp/memory-management-examples_8.cpp)]

   堆分配的语句为：

   [!code-cpp[NVC_MFC_Utilities#9](../mfc/codesnippet/cpp/memory-management-examples_9.cpp)]

## <a name="see-also"></a>请参阅

[内存管理：堆分配](../mfc/memory-management-heap-allocation.md)
