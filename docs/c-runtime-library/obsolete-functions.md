---
title: 已过时的函数
description: 列出已弃用并已从 Microsoft C 运行时库（CRT）中删除的过时函数。
ms.date: 12/09/2019
api_name:
- _beep
- _sleep
- _loaddll
- _getdllprocaddr
- _seterrormode
- is_wctype
- _getsystime
- _setsystime
api_location:
- msvcrt.dll
- msvcr80.dll
- msvcr90.dll
- msvcr100.dll
- msvcr100_clr0400.dll
- msvcr110.dll
- msvcr110_clr0400.dll
- msvcr120.dll
- msvcr120_clr0400.dll
- ucrtbase.dll
- api-ms-win-crt-process-l1-1-0.dll
- api-ms-win-crt-runtime-l1-1-0.dll
- api-ms-win-crt-string-l1-1-0.dll
- api-ms-win-crt-time-l1-1-0.dll
api_type:
- DLLExport
topic_type:
- apiref
f1_keywords:
- is_wctype
- _loaddll
- _unloaddll
- _getdllprocaddr
- _seterrormode
- _beep
- _sleep
- _getsystime
- corecrt_wctype/is_wctype
- process/_loaddll
- process/_unloaddll
- process/_getdllprocaddr
- stdlib/_seterrormode
- stdlib/_beep
- stdlib/_sleep
- time/_getsystime
- time/_setsystime
helpviewer_keywords:
- obsolete functions
- _beep function
- _sleep function
- _seterrormode function
ms.assetid: 8e14c2d4-1481-4240-8586-47eb43db02b0
ms.openlocfilehash: c913e44a4f0d06813e877645bd01855baa6fd4dc
ms.sourcegitcommit: 573b36b52b0de7be5cae309d45b68ac7ecf9a6d8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/10/2019
ms.locfileid: "74988783"
---
# <a name="obsolete-functions"></a>已过时的函数

某些库函数已过时，已有最新的等效函数。 建议将这些函数更改为更新后的版本。 已从 CRT 中删除其他过时函数。 本文列出了弃用的已弃用的函数，以及在 Visual Studio 的特定版本中删除的函数。

## <a name="deprecated-as-obsolete-in-visual-studio-2015"></a>在 Visual Studio 2015 中已弃用（过时）

|已过时的函数|替代项|
|-----------------------|-----------------|
|`is_wctype`|[iswctype](../c-runtime-library/reference/isctype-iswctype-isctype-l-iswctype-l.md)|
|`_loaddll`|[LoadLibrary](/windows/win32/api/libloaderapi/nf-libloaderapi-loadlibraryw)、[LoadLibraryEx](/windows/win32/api/libloaderapi/nf-libloaderapi-loadlibraryexw) 或 [LoadPackagedLibrary](/windows/win32/api/winbase/nf-winbase-loadpackagedlibrary)|
|`_unloaddll`|[FreeLibrary](/windows/win32/api/libloaderapi/nf-libloaderapi-freelibrary)|
|`_getdllprocaddr`|[GetProcAddress](../build/getprocaddress.md)|
|`_seterrormode`|[SetErrorMode](/windows/win32/api/errhandlingapi/nf-errhandlingapi-seterrormode)|
|`_beep`|[提示音](/windows/win32/api/utilapiset/nf-utilapiset-beep)|
|`_sleep`|[休眠](/windows/win32/api/synchapi/nf-synchapi-sleep)|
|`_getsystime`|[GetLocalTime](/windows/win32/api/sysinfoapi/nf-sysinfoapi-getlocaltime)|
|`_setsystime`|[SetLocalTime](/windows/win32/api/sysinfoapi/nf-sysinfoapi-setlocaltime)|

## <a name="removed-from-the-crt-in-visual-studio-2015"></a>已从 Visual Studio 2015 的 CRT 中删除

|已过时的函数|替代项|
|-----------------------|-----------------|
|[_cgets、_cgetws](../c-runtime-library/cgets-cgetws.md)|[_cgets_s、_cgetws_s](../c-runtime-library/reference/cgets-s-cgetws-s.md)|
|[gets、_getws](../c-runtime-library/gets-getws.md)|[gets_s、_getws_s](../c-runtime-library/reference/gets-s-getws-s.md)|
|[_get_output_format](../c-runtime-library/get-output-format.md)|无|
|[_heapadd](../c-runtime-library/heapadd.md)|无|
|[_heapset](../c-runtime-library/heapset.md)|无|
|[sct.inp、inpw、_inp、_inpw _inpd](../c-runtime-library/inp-inpw-inpd.md)|无|
|[outp、outpw、_outp、_outpw _outpd](../c-runtime-library/outp-outpw-outpd.md)|无|
|[_set_output_format](../c-runtime-library/set-output-format.md)|无|

## <a name="removed-from-the-crt-in-earlier-versions-of-visual-studio"></a>已从 Visual Studio 早期版本的 CRT 中删除

[_lock](../c-runtime-library/lock.md)

[_unlock](../c-runtime-library/unlock.md)
