---
title: 声明摘要
ms.date: 11/04/2016
ms.assetid: 53a5e9e5-1a33-40b5-9dea-7f669b479329
ms.openlocfilehash: 88cfc78089e0efd4765a40ab0d9c6dc333deb125
ms.sourcegitcommit: a6d63c07ab9ec251c48bc003ab2933cf01263f19
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/05/2019
ms.locfileid: "74857016"
---
# <a name="summary-of-declarations"></a>声明摘要

*declaration*:<br/>
&nbsp;&nbsp;&nbsp;&nbsp;*declaration-specifiers* *attribute-seq*<sub>opt</sub> *init-declarator-list*<sub>opt</sub> **;**

*declaration-specifiers*：<br/>
&nbsp;&nbsp;&nbsp;&nbsp;*storage-class-specifier* *declaration-specifiers*<sub>opt</sub><br/>
&nbsp;&nbsp;&nbsp;&nbsp;*type-specifier* *declaration-specifiers*<sub>opt</sub><br/>
&nbsp;&nbsp;&nbsp;&nbsp;*type-qualifier* *declaration-specifiers*<sub>opt</sub>

*属性-seq* ：&nbsp;&nbsp;&nbsp;&nbsp;/\* \*/<br/>
&nbsp;&nbsp;&nbsp;&nbsp;attribute attribute-seq<sub>opt</sub>

*属性*：&nbsp;&nbsp;中的一个 &nbsp;&nbsp;/\* \*/<br/>
&nbsp;&nbsp;&nbsp;&nbsp;[__asm](../assembler/inline/asm.md) [__clrcall](../cpp/clrcall.md) [__stdcall](../cpp/stdcall.md) [__based](../cpp/based-grammar.md) [__fastcall](../cpp/fastcall.md) [__thiscall](../cpp/thiscall.md) [__cdecl](../cpp/cdecl.md) [__inline](../cpp/inline-functions-cpp.md) [__vectorcall](../cpp/vectorcall.md)

*init-declarator-list*：<br/>
&nbsp;&nbsp;&nbsp;&nbsp;*init-declarator*<br/>
&nbsp;&nbsp;&nbsp;&nbsp;*init-declarator-list*  **,**  *init-declarator*

*init-declarator*：<br/>
&nbsp;&nbsp;&nbsp;&nbsp;*declarator*<br/>
&nbsp;&nbsp;&nbsp;&nbsp;declarator  =  initializer /\* For scalar initialization \*/

*storage-class-specifier*：<br/>
&nbsp;&nbsp;&nbsp;&nbsp;**auto**<br/>
&nbsp;&nbsp;&nbsp;&nbsp;**register**<br/>
&nbsp;&nbsp;&nbsp;&nbsp;**static**<br/>
&nbsp;&nbsp;&nbsp;&nbsp;**extern**<br/>
&nbsp;&nbsp;&nbsp;&nbsp;**typedef**<br/>
&nbsp;&nbsp;&nbsp;__declspec /\* \*/ **（** *decl* **）** &nbsp;

*type-specifier*：<br/>
&nbsp;&nbsp;&nbsp;&nbsp;**void**<br/>
&nbsp;&nbsp;&nbsp;&nbsp;**char**<br/>
&nbsp;&nbsp;&nbsp;&nbsp;**short**<br/>
&nbsp;&nbsp;&nbsp;&nbsp;**int**<br/>
&nbsp;&nbsp; **&nbsp;&nbsp;__int8 /\*** \*/<br/>
&nbsp;&nbsp; **&nbsp;&nbsp;__int16 /\*** \*/<br/>
&nbsp;&nbsp; **&nbsp;&nbsp;__int32 /\*** \*/<br/>
&nbsp;&nbsp; **&nbsp;&nbsp;__int64 /\*** \*/<br/>
&nbsp;&nbsp;&nbsp;&nbsp;**long**<br/>
&nbsp;&nbsp;&nbsp;&nbsp;**float**<br/>
&nbsp;&nbsp;&nbsp;&nbsp;**double**<br/>
&nbsp;&nbsp;&nbsp;&nbsp;**signed**<br/>
&nbsp;&nbsp;&nbsp;&nbsp;**unsigned**<br/>
&nbsp;&nbsp;&nbsp;&nbsp;*struct-or-union-specifier*<br/>
&nbsp;&nbsp;&nbsp;&nbsp;*enum-specifier*<br/>
&nbsp;&nbsp;&nbsp;&nbsp;*typedef-name*

*type-qualifier*:<br/>
&nbsp;&nbsp;&nbsp;&nbsp;const<br/>
&nbsp;&nbsp;&nbsp;&nbsp;volatile

*declarator*:<br/>
&nbsp;&nbsp;&nbsp;&nbsp;pointer<sub>opt</sub> direct-declarator

*direct-declarator*：<br/>
&nbsp;&nbsp;&nbsp;&nbsp;*identifier*<br/>
&nbsp;&nbsp;&nbsp;&nbsp;( declarator )<br/>
&nbsp;&nbsp;&nbsp;&nbsp;direct-declarator [ constant-expression<sub>opt</sub> ]<br/>
&nbsp;&nbsp;&nbsp;&nbsp;direct-declarator ( parameter-type-list ) /\* New-style declarator \*/<br/>
&nbsp;&nbsp;&nbsp;&nbsp;direct-declarator ( identifier-list<sub>opt</sub> ) /\* Obsolete-style declarator \*/

*pointer*:<br/>
&nbsp;&nbsp;&nbsp;&nbsp;<strong>\*</strong> *type-qualifier-list*<sub>opt</sub><br/>
&nbsp;&nbsp;&nbsp;&nbsp;<strong>\*</strong> *type-qualifier-list*<sub>opt</sub> *pointer*

parameter-type-list：&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;/\* 参数列表 \*/<br/>
&nbsp;&nbsp;&nbsp;&nbsp;*parameter-list*<br/>
&nbsp;&nbsp;&nbsp;&nbsp;*parameter-list* **, ...**

*parameter-list*:<br/>
&nbsp;&nbsp;&nbsp;&nbsp;*parameter-declaration*<br/>
&nbsp;&nbsp;&nbsp;&nbsp;parameter-list **,** parameter-declaration

*type-qualifier-list*:<br/>
&nbsp;&nbsp;&nbsp;&nbsp;*type-qualifier*<br/>
&nbsp;&nbsp;&nbsp;&nbsp;type-qualifier-list type-qualifier

*enum-specifier*：<br/>
&nbsp;&nbsp;&nbsp;&nbsp;**enum** *identifier*<sub>opt</sub> **{** *enumerator-list* **}**<br/>
&nbsp;&nbsp;&nbsp;&nbsp;**enum** *identifier*

*enumerator-list*：<br/>
&nbsp;&nbsp;&nbsp;&nbsp;*enumerator*<br/>
&nbsp;&nbsp;&nbsp;&nbsp;*enumerator-list* **,** *enumerator*

*enumerator*:<br/>
&nbsp;&nbsp;&nbsp;&nbsp;*enumeration-constant*<br/>
&nbsp;&nbsp;&nbsp;&nbsp;*enumeration-constant* **=** *constant-expression*

*enumeration-constant*：<br/>
&nbsp;&nbsp;&nbsp;&nbsp;*identifier*

*struct-or-union-specifier*:<br/>
&nbsp;&nbsp;&nbsp;&nbsp;*struct-or-union* *identifier*<sub>opt</sub> **{** *struct-declaration-list* **}**<br/>
&nbsp;&nbsp;&nbsp;&nbsp;*struct-or-union* *identifier*

*struct-or-union*:<br/>
&nbsp;&nbsp;&nbsp;&nbsp;**struct**<br/>
&nbsp;&nbsp;&nbsp;&nbsp;**union**

*struct-declaration-list*:<br/>
&nbsp;&nbsp;&nbsp;&nbsp;*struct-declaration*<br/>
&nbsp;&nbsp;&nbsp;&nbsp;*struct-declaration-list* *struct-declaration*

*struct-declaration*:<br/>
&nbsp;&nbsp;&nbsp;&nbsp;*specifier-qualifier-list* *struct-declarator-list* **;**

*specifier-qualifier-list*:<br/>
&nbsp;&nbsp;&nbsp;&nbsp;*type-specifier* *specifier-qualifier-list*<sub>opt</sub><br/>
&nbsp;&nbsp;&nbsp;&nbsp;*type-qualifier* *specifier-qualifier-list*<sub>opt</sub>

*struct-declarator-list*:<br/>
&nbsp;&nbsp;&nbsp;&nbsp;*struct-declarator* *struct-declarator-list* **,** *struct-declarator*

*struct-declarator*:<br/>
&nbsp;&nbsp;&nbsp;&nbsp;*declarator*<br/>
&nbsp;&nbsp;&nbsp;&nbsp;*type-specifier* *declarator*<sub>opt</sub> **:** *constant-expression*

*parameter-declaration*:<br/>
&nbsp;&nbsp;&nbsp;&nbsp;declaration-specifiers declarator /\* 已命名的声明符 \*/<br/>
&nbsp;&nbsp;&nbsp;&nbsp;declaration-specifiers abstract-declarator<sub>opt</sub> /\* 匿名声明符 \*/

identifier-list：/\*用于旧式声明符\*/<br/>
&nbsp;&nbsp;&nbsp;&nbsp;*identifier*<br/>
&nbsp;&nbsp;&nbsp;&nbsp;identifier-list , identifier

abstract-declarator：/\* 用于匿名声明符 \*/<br/>
&nbsp;&nbsp;&nbsp;&nbsp;pointer<br/>
&nbsp;&nbsp;&nbsp;&nbsp;pointer<sub>opt</sub> direct-abstract-declarator

*direct-abstract-declarator*：<br/>
&nbsp;&nbsp;&nbsp;&nbsp;( abstract-declarator )<br/>
&nbsp;&nbsp;&nbsp;&nbsp;direct-abstract-declarator<sub>opt</sub> [ constant-expression<sub>opt</sub> ]<br/>
&nbsp;&nbsp;&nbsp;&nbsp;direct-abstract-declarator<sub>opt</sub> ( parameter-type-list<sub>opt</sub>)

*initializer*：<br/>
&nbsp;&nbsp;&nbsp;&nbsp;*assignment-expression*<br/>
&nbsp;&nbsp;&nbsp;&nbsp;{ initializer-list} /\* 用于聚合初始化 \*/<br/>
&nbsp;&nbsp;&nbsp;&nbsp;{initializer-list , }

*initializer-list*：<br/>
&nbsp;&nbsp;&nbsp;&nbsp;*initializer*<br/>
&nbsp;&nbsp;&nbsp;&nbsp;initializer-list, initializer

*type-name*：<br/>
&nbsp;&nbsp;&nbsp;&nbsp;specifier-qualifier-list abstract-declarator<sub>opt</sub>

*typedef-name*：<br/>
&nbsp;&nbsp;&nbsp;&nbsp;*identifier*

*decl*&nbsp;&nbsp;&nbsp;&nbsp;/\* 特定于 Microsoft 的 \*/<br/>
&nbsp;&nbsp;&nbsp;&nbsp;*extended-decl-modifier*<sub>opt</sub><br/>
&nbsp;&nbsp;&nbsp;&nbsp;*extended-decl-modifier-seq* *extended-decl-modifier*

*decl-修饰符*：&nbsp;&nbsp;&nbsp;&nbsp;/\* \*/<br/>
&nbsp;&nbsp;&nbsp;&nbsp;**thread**<br/>
&nbsp;&nbsp;&nbsp;&nbsp;**naked**<br/>
&nbsp;&nbsp;&nbsp;&nbsp;**dllimport**<br/>
&nbsp;&nbsp;&nbsp;&nbsp;**dllexport**

## <a name="see-also"></a>另请参阅

[调用约定](../cpp/calling-conventions.md)<br/>
[短语结构语法](../c-language/phrase-structure-grammar.md)<br/>
[已过时调用约定](../cpp/obsolete-calling-conventions.md)