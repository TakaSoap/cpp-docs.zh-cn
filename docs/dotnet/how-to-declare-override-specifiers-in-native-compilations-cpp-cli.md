---
title: 如何：声明重写说明符 (C++/CLI)
ms.date: 11/04/2016
helpviewer_keywords:
- override specifiers in native compilation, overriding
ms.assetid: d0551836-9ac7-41eb-a6e9-a4b3ef60767d
ms.openlocfilehash: db74ef226242ec8f4f70f2769fbc8ba102a808c8
ms.sourcegitcommit: 0ab61bc3d2b6cfbd52a16c6ab2b97a8ea1864f12
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62387417"
---
# <a name="how-to-declare-override-specifiers-in-native-compilations-ccli"></a>如何：声明在本机编译中的重写说明符 (C++/CLI)

[密封](../extensions/sealed-cpp-component-extensions.md)，[抽象](../extensions/abstract-cpp-component-extensions.md)，和[重写](../extensions/override-cpp-component-extensions.md)在编译中，请勿使用可用 **/ZW**或[/clr](../build/reference/clr-common-language-runtime-compilation.md)。

> [!NOTE]
>  ISO C + + 11 标准语言具有[重写](../cpp/override-specifier.md)标识符和[最终](../cpp/final-specifier.md)标识符，并且两个支持在 Visual Studio 中使用`final`而不是`sealed`应该做的代码中编译为仅限本机的。

## <a name="example"></a>示例

### <a name="description"></a>描述

下面的示例演示`sealed`在本机编译中有效。

### <a name="code"></a>代码

```cpp
// sealed_native_keyword.cpp
#include <stdio.h>
__interface I1 {
   virtual void f();
   virtual void g();
};

class X : public I1 {
public:
   virtual void g() sealed {}
};

class Y : public X {
public:

   // the following override generates a compiler error
   virtual void g() {}   // C3248 X::g is sealed!
};
```

## <a name="example"></a>示例

### <a name="description"></a>描述

下面的示例演示`override`在本机编译中有效。

### <a name="code"></a>代码

```cpp
// override_native_keyword.cpp
#include <stdio.h>
__interface I1 {
   virtual void f();
};

class X : public I1 {
public:
   virtual void f() override {}   // OK
   virtual void g() override {}   // C3668 I1::g does not exist
};
```

## <a name="example"></a>示例

### <a name="description"></a>描述

此示例演示`abstract`在本机编译中有效。

### <a name="code"></a>代码

```cpp
// abstract_native_keyword.cpp
class X abstract {};

int main() {
   X * MyX = new X;   // C3622 cannot instantiate abstract class
}
```

## <a name="see-also"></a>请参阅

[重写说明符](../extensions/override-specifiers-cpp-component-extensions.md)
