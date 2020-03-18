---
title: RelogA
description: C++ BUILD Insights SDK RelogA 函数引用。
ms.date: 02/12/2020
helpviewer_keywords:
- C++ Build Insights
- C++ Build Insights SDK
- RelogA
- throughput analysis
- build time analysis
- vcperf.exe
ms.openlocfilehash: c4427aa0ac85e34bfb9d569913a8ccf6ab264f52
ms.sourcegitcommit: 3e8fa01f323bc5043a48a0c18b855d38af3648d4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/05/2020
ms.locfileid: "78334318"
---
# <a name="reloga"></a>RelogA

::: moniker range="<=vs-2015"

C++ BUILD Insights SDK 与 Visual Studio 2017 及更高版本兼容。 若要查看这些版本的文档，请将本文的 Visual Studio 版本选择器控件设置为 "Visual studio 2017 或 Visual Studio 2019"。

::: moniker-end
::: moniker range=">=vs-2017"

`RelogA` 函数用于从 Windows 事件跟踪（ETW）跟踪读取 MSVC 事件，并将这些事件写入新的已修改 ETW 跟踪。

## <a name="syntax"></a>语法

```cpp
enum RESULT_CODE RelogA(
    const char*             inputLogFile,
    const char*             outputLogFile,
    const RELOG_DESCRIPTOR* relogDescriptor);
```

### <a name="parameters"></a>参数

*inputLogFile*\
要从中读取事件的输入 ETW 跟踪。

*outputLogFile*\
要在其中写入新事件的文件。

*relogDescriptor*\
指向[RELOG_DESCRIPTOR](../other-types/relog-descriptor-struct.md)对象的指针。 使用此对象配置 relogging 会话。

### <a name="return-value"></a>返回值

[RESULT_CODE](../other-types/result-code-enum.md)枚举中的结果代码。

::: moniker-end