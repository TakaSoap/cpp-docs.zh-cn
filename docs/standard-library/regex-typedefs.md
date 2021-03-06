---
title: '&lt;regex&gt; typedefs'
ms.date: 11/04/2016
f1_keywords:
- regex/std::cmatch
- regex/std::cregex_iterator
- regex/std::cregex_token_iterator
- regex/std::csub_match
- regex/std::regex
- regex/std::smatch
- regex/std::sregex_iterator
- regex/std::sregex_token_iterator
- regex/std::ssub_match
- regex/std::wcmatch
- regex/std::wcregex_iterator
- regex/std::wcregex_token_iterator
- regex/std::wcsub_match
- regex/std::wregex
- regex/std::wsmatch
- regex/std::wsregex_iterator
- regex/std::wsregex_token_iterator
- regex/std::wssub_match
ms.assetid: e6a69067-106c-4a24-9e08-7c867a3a2260
ms.openlocfilehash: 4321d9ea6fd9ba57074b25e084553fe1f0846213
ms.sourcegitcommit: 590e488e51389066a4da4aa06d32d4c362c23393
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/21/2019
ms.locfileid: "72689029"
---
# <a name="ltregexgt-typedefs"></a>&lt;regex&gt; typedefs

||||
|-|-|-|
|[cmatch](#cmatch)|[cregex_iterator](#cregex_iterator)|[cregex_token_iterator](#cregex_token_iterator)|
|[csub_match](#csub_match)|[regex](#regex)|[smatch](#smatch)|
|[sregex_iterator](#sregex_iterator)|[sregex_token_iterator](#sregex_token_iterator)|[ssub_match](#ssub_match)|
|[wcmatch](#wcmatch)|[wcregex_iterator](#wcregex_iterator)|[wcregex_token_iterator](#wcregex_token_iterator)|
|[wcsub_match](#wcsub_match)|[wregex](#wregex)|[wsmatch](#wsmatch)|
|[wsregex_iterator](#wsregex_iterator)|[wsregex_token_iterator](#wsregex_token_iterator)|[wssub_match](#wssub_match)|

## <a name="cmatch"></a>  cmatch Typedef

char match_results 的类型定义。

```cpp
typedef match_results<const char*> cmatch;
```

### <a name="remarks"></a>备注

该类型描述 `const char*` 类型的迭代器的类模板[Match_results 类](../standard-library/match-results-class.md)的专用化。

## <a name="cregex_iterator"></a>  cregex_iterator Typedef

char regex_iterator 的类型定义。

```cpp
typedef regex_iterator<const char*> cregex_iterator;
```

### <a name="remarks"></a>备注

该类型描述 `const char*` 类型的迭代器的类模板[Regex_iterator 类](../standard-library/regex-iterator-class.md)的专用化。

## <a name="cregex_token_iterator"></a>  cregex_token_iterator Typedef

char regex_token_iterator 的类型定义

```cpp
typedef regex_token_iterator<const char*> cregex_token_iterator;
```

### <a name="remarks"></a>备注

该类型描述 `const char*` 类型的迭代器的类模板[Regex_token_iterator 类](../standard-library/regex-token-iterator-class.md)的专用化。

## <a name="csub_match"></a>  csub_match Typedef

char sub_match 的类型定义。

```cpp
typedef sub_match<const char*> csub_match;
```

### <a name="remarks"></a>备注

该类型描述 `const char*` 类型的迭代器的类模板[Sub_match 类](../standard-library/sub-match-class.md)的专用化。

## <a name="regex"></a>  regex Typedef

char basic_regex 的类型定义。

```cpp
typedef basic_regex<char> regex;
```

### <a name="remarks"></a>备注

该类型描述了类模板[Basic_regex 类](../standard-library/basic-regex-class.md)的专用化，该类用于**char**类型的元素。

> [!NOTE]
> 用于 `regex` 时，高位字符的结果不可预测。 0 到 127 范围之外的值可能会导致未定义的行为。

## <a name="smatch"></a>  smatch Typedef

字符串 match_results 的类型定义。

```cpp
typedef match_results<string::const_iterator> smatch;
```

### <a name="remarks"></a>备注

该类型描述 `string::const_iterator` 类型的迭代器的类模板[Match_results 类](../standard-library/match-results-class.md)的专用化。

## <a name="sregex_iterator"></a>  sregex_iterator Typedef

字符串 regex_iterator. 的类型定义。

```cpp
typedef regex_iterator<string::const_iterator> sregex_iterator;
```

### <a name="remarks"></a>备注

该类型描述 `string::const_iterator` 类型的迭代器的类模板[Regex_iterator 类](../standard-library/regex-iterator-class.md)的专用化。

## <a name="sregex_token_iterator"></a>  sregex_token_iterator Typedef

字符串 regex_token_iterator 的类型定义。

```cpp
typedef regex_token_iterator<string::const_iterator> sregex_token_iterator;
```

### <a name="remarks"></a>备注

该类型描述 `string::const_iterator` 类型的迭代器的类模板[Regex_token_iterator 类](../standard-library/regex-token-iterator-class.md)的专用化。

## <a name="ssub_match"></a>ssub_match Typedef

字符串 sub_match 的类型定义。

```cpp
typedef sub_match<string::const_iterator> ssub_match;
```

### <a name="remarks"></a>备注

该类型描述 `string::const_iterator` 类型的迭代器的类模板[Sub_match 类](../standard-library/sub-match-class.md)的专用化。

## <a name="wcmatch"></a>wcmatch Typedef

wchar_t match_results 的类型定义。

```cpp
typedef match_results<const wchar_t *> wcmatch;
```

### <a name="remarks"></a>备注

该类型描述 `const wchar_t*` 类型的迭代器的类模板[Match_results 类](../standard-library/match-results-class.md)的专用化。

## <a name="wcregex_iterator"></a>  wcregex_iterator Typedef

wchar_t regex_iterator 的类型定义。

```cpp
typedef regex_iterator<const wchar_t*> wcregex_iterator;
```

### <a name="remarks"></a>备注

该类型描述 `const wchar_t*` 类型的迭代器的类模板[Regex_iterator 类](../standard-library/regex-iterator-class.md)的专用化。

## <a name="wcregex_token_iterator"></a>  wcregex_token_iterator Typedef

wchar_t regex_token_iterator. 的类型定义。

```cpp
typedef regex_token_iterator<const wchar_t*> wcregex_token_iterator;
```

### <a name="remarks"></a>备注

该类型描述 `const wchar_t*` 类型的迭代器的类模板[Regex_token_iterator 类](../standard-library/regex-token-iterator-class.md)的专用化。

## <a name="wcsub_match"></a>wcsub_match Typedef

wchar_t sub_match 的类型定义。

```cpp
typedef sub_match<const wchar_t*> wcsub_match;
```

### <a name="remarks"></a>备注

该类型描述 `const wchar_t*` 类型的迭代器的类模板[Sub_match 类](../standard-library/sub-match-class.md)的专用化。

## <a name="wregex"></a>wregex Typedef

wchar_t basic_regex 的类型定义。

```cpp
typedef basic_regex<wchar_t> wregex;
```

### <a name="remarks"></a>备注

该类型描述了类型为**wchar_t**的元素的类模板[basic_regex 类](../standard-library/basic-regex-class.md)的专用化。

## <a name="wsmatch"></a>  wsmatch Typedef

wstring match_results 的类型定义。

```cpp
typedef match_results<wstring::const_iterator> wsmatch;
```

### <a name="remarks"></a>备注

该类型描述 `wstring::const_iterator` 类型的迭代器的类模板[Match_results 类](../standard-library/match-results-class.md)的专用化。

## <a name="wsregex_iterator"></a>  wsregex_iterator Typedef

wstring regex_iterator 的类型定义。

```cpp
typedef regex_iterator<wstring::const_iterator> wsregex_iterator;
```

### <a name="remarks"></a>备注

该类型描述 `wstring::const_iterator` 类型的迭代器的类模板[Regex_iterator 类](../standard-library/regex-iterator-class.md)的专用化。

## <a name="wsregex_token_iterator"></a>  wsregex_token_iterator Typedef

wstring regex_token_iterator 的类型定义。

```cpp
typedef regex_token_iterator<wstring::const_iterator> wsregex_token_iterator;
```

### <a name="remarks"></a>备注

该类型描述 `wstring::const_iterator` 类型的迭代器的类模板[Regex_token_iterator 类](../standard-library/regex-token-iterator-class.md)的专用化。

## <a name="wssub_match"></a>  wssub_match Typedef

wstring sub_match 的类型定义。

```cpp
typedef sub_match<wstring::const_iterator> wssub_match;
```

### <a name="remarks"></a>备注

该类型描述 `wstring::const_iterator` 类型的迭代器的类模板[Sub_match 类](../standard-library/sub-match-class.md)的专用化。

## <a name="see-also"></a>请参阅

[\<regex>](../standard-library/regex.md)\
[Regex_constants 类](../standard-library/regex-constants-class.md)\
[Regex_error 类](../standard-library/regex-error-class.md)\
[\<regex > 函数](../standard-library/regex-functions.md)\
[Regex_iterator 类](../standard-library/regex-iterator-class.md)\
[\<regex > 运算符](../standard-library/regex-operators.md)\
[Regex_token_iterator 类](../standard-library/regex-token-iterator-class.md)\
[regex_traits 类](../standard-library/regex-traits-class.md)
