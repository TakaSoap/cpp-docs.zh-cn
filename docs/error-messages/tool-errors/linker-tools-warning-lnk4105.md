---
title: 链接器工具警告 LNK4105
ms.date: 11/04/2016
f1_keywords:
- LNK4105
helpviewer_keywords:
- LNK4105
ms.assetid: 6c7bebf4-4ea6-4533-a6ed-e563d43abbd7
ms.openlocfilehash: 880c8519a530f492d0c322575a1386af8a7d0187
ms.sourcegitcommit: 0ab61bc3d2b6cfbd52a16c6ab2b97a8ea1864f12
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62310924"
---
# <a name="linker-tools-warning-lnk4105"></a>链接器工具警告 LNK4105

未指定选项 option; 使用参数忽略选项

此警告仅发生时[/LIBPATH](../../build/reference/libpath-additional-libpath.md)设置选项。 如果使用此选项时未不指定任何目录，然后链接器会忽略选项，并将生成此警告消息。

如果不需要重写现有环境库设置，请从链接器命令行删除 /LIBPATH 选项。 如果你想要用于库的其他搜索路径，指定 /LIBPATH 选项后面跟随的备用路径。

## <a name="example"></a>示例

```
link /libpath:c:\filepath\lib bar.obj
```

将直接链接器所需的库中搜索`c:\filepath\lib`之前搜索在默认位置。