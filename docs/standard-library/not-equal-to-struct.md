---
title: not_equal_to 结构
ms.date: 11/04/2016
f1_keywords:
- functional/std::not_equal_to
helpviewer_keywords:
- not_equal_to function
- not_equal_to struct
ms.assetid: 333fce09-4f51-44e0-ba26-533bccffd485
ms.openlocfilehash: 5ee1ce120490b91a5f904109f49bf36d88e6261f
ms.sourcegitcommit: 3590dc146525807500c0477d6c9c17a4a8a2d658
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/16/2019
ms.locfileid: "68243530"
---
# <a name="notequalto-struct"></a>not_equal_to 结构

执行不等于运算的二元谓词 (`operator!=`) 对其自变量。

## <a name="syntax"></a>语法

```
template <class Type = void>
struct not_equal_to : public binary_function<Type, Type, bool>
{
    bool operator()(const Type& Left, const Type& Right) const;
};

// specialized transparent functor for operator!=
template <>
struct not_equal_to<void>
{
  template <class T, class U>
  auto operator()(T&& Left, U&& Right) const`
    -> decltype(std::forward<T>(Left) != std::forward<U>(Right));
};
```

### <a name="parameters"></a>参数

*类型*， *T*， *U*\
支持 `operator!=` 接受指定或推断类型的操作数的任何类型。

*左侧*\
不等运算的左操作数。 专用化的模板采用类型的左值引用参数*类型*。 专用化的模板可完美转移左值和右值引用参数的类型推断*T*。

*右侧*\
不等运算的右操作数。 专用化的模板采用类型的左值引用参数*类型*。 专用化的模板可完美转移左值和右值引用参数的类型推断*U*。

## <a name="return-value"></a>返回值

`Left != Right` 的结果。 专专用化模板可完美转移结果，该结果具有由 `operator!=` 返回的类型。

## <a name="remarks"></a>备注

类型的对象*类型*必须是可比较相等性的。 这要求在对象集上定义的 `operator!=` 满足等价关系的数学性质。 所有内置的数字和指针类型都满足此要求。

## <a name="example"></a>示例

```cpp
// functional_not_equal_to.cpp
// compile with: /EHsc
#include <vector>
#include <functional>
#include <algorithm>
#include <iostream>

using namespace std;

int main( )
{
   vector <double> v1, v2, v3 (6);
   vector <double>::iterator Iter1, Iter2, Iter3;

   int i;
   for ( i = 0 ; i <= 5 ; i+=2 )
   {
      v1.push_back( 2.0 *i );
      v1.push_back( 2.0 * i + 1.0 );
   }

   int j;
   for ( j = 0 ; j <= 5 ; j+=2 )
   {
      v2.push_back( - 2.0 * j );
      v2.push_back( 2.0 * j + 1.0 );
   }

   cout << "The vector v1 = ( " ;
   for ( Iter1 = v1.begin( ) ; Iter1 != v1.end( ) ; Iter1++ )
      cout << *Iter1 << " ";
   cout << ")" << endl;

   cout << "The vector v2 = ( " ;
   for ( Iter2 = v2.begin( ) ; Iter2 != v2.end( ) ; Iter2++ )
      cout << *Iter2 << " ";
   cout << ")" << endl;

   // Testing for the element-wise equality between v1 & v2
   transform ( v1.begin( ), v1.end( ), v2.begin( ), v3.begin ( ),
      not_equal_to<double>( ) );

   cout << "The result of the element-wise not_equal_to comparsion\n"
      << "between v1 & v2 is: ( " ;
   for ( Iter3 = v3.begin( ) ; Iter3 != v3.end( ) ; Iter3++ )
      cout << *Iter3 << " ";
   cout << ")" << endl;
}
```

```Output
The vector v1 = ( 0 1 4 5 8 9 )
The vector v2 = ( -0 1 -4 5 -8 9 )
The result of the element-wise not_equal_to comparsion
between v1 & v2 is: ( 0 0 1 0 1 0 )
```
