---
title: '&lt;iomanip&gt; 函数'
ms.date: 11/04/2016
f1_keywords:
- iomanip/std::get_money
- iomanip/std::get_time
- iomanip/std::put_money
- iomanip/std::put_time
- iomanip/std::quoted
- iomanip/std::resetiosflags
- iomanip/std::setbase
- iomanip/std::setfill
- iomanip/std::setiosflags
- iomanip/std::setprecision
- iomanip/std::setw
ms.assetid: 3ddde610-70cc-4cfa-8a89-3e83d1d356a8
helpviewer_keywords:
- std::get_money [C++]
- std::get_time [C++]
- std::put_money [C++]
- std::put_time [C++]
- std::quoted [C++]
- std::resetiosflags [C++]
- std::setbase [C++]
- std::setfill [C++]
- std::setiosflags [C++]
- std::setprecision [C++]
- std::setw [C++]
ms.openlocfilehash: 944834e40a399622b5c85d95100d4ca3c3c2da93
ms.sourcegitcommit: a930a9b47bd95599265d6ba83bb87e46ae748949
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/22/2020
ms.locfileid: "76518460"
---
# <a name="ltiomanipgt-functions"></a>&lt;iomanip&gt; 函数

||||
|-|-|-|
|[get_money](#iomanip_get_money)|[get_time](#iomanip_get_time)|[put_money](#iomanip_put_money)|
|[put_time](#iomanip_put_time)|[quoted](#quoted)|[resetiosflags](#resetiosflags)|
|[setbase](#setbase)|[setfill](#setfill)|[setiosflags](#setiosflags)|
|[setprecision](#setprecision)|[setw](#setw)|

## <a name="iomanip_get_money"></a>get_money

使用所需格式从流中提取货币值，然后在参数中返回值。

```cpp
template <class Money>
T7 get_money(Money& amount, bool use_intl);
```

### <a name="parameters"></a>参数

\*量*
提取的货币值。

*use_intl*\
如果**为 true**，则使用国际格式。 默认值为“false”。

### <a name="remarks"></a>备注

操控器会返回一个对象，该对象在从流 `str`中提取时，将充当 `formatted input function`，该对象调用与 `str`关联的区域设置 facet `money_get` `get`，并使用*use_intl*来指示国际格式。 如果成功，则调用将按提取的货币值存储*量*。 此操控器随后返回 `str`。

`Money` 必须为 `long double` 类型，或者是具有与 `str` 相同的元素和特征参数的 `basic_string` 的实例化。

## <a name="iomanip_get_time"></a>get_time

使用所需格式从流中提取时间值。 在参数中返回值作为时间结构。

```cpp
template <class Elem>
T10 put_time(struct tm *time_ptr, const Elem *time_format);
```

### <a name="parameters"></a>参数

*time_ptr*\
时间结构形式的时间。

*time_format*\
要用于获取时间值的所需格式。

### <a name="remarks"></a>备注

此操控器会返回一个对象，该对象在从流 `str` 中提取时会表现为 `formatted input function`，它为与 `str` 关联的区域设置 Facet `time_get` 调用成员函数 `get`，其使用 `tptr` 来指示时间结构，使用 `fmt` 来指示 null 终止格式字符串的开头。 如果成功，则调用会将与任何提取时间字段关联的值存储在时间结构中。 此操控器随后返回 `str`。

## <a name="iomanip_put_money"></a>put_money

使用所需格式将货币金额插入流中。

```cpp
template <class Money>
T8 put_money(const Money& amount, bool use_intl);
```

### <a name="parameters"></a>参数

\*量*
要插入到流中的货币金额。

*use_intl*\
如果操控器应使用国际格式，则设置为**true** ，否则设置为**false** 。

### <a name="return-value"></a>返回值

返回 `str`。

### <a name="remarks"></a>备注

此操控器会返回一个对象，该对象在插入到流 `str` 中时会表现为一个格式化输出函数，该函数会对与 `str` 关联的区域设置 Facet `money_put` 调用成员函数 `put`。 如果成功，则调用插入 `amount` 的格式正确，使用*use_intl*指示国际格式并 `str.fill()`，作为填充元素。 此操控器随后返回 `str`。

`Money` 必须为 `long double` 类型，或者是具有与 `str` 相同的元素和特征参数的 `basic_string` 的实例化。

## <a name="iomanip_put_time"></a>put_time

使用指定格式将时间值从时间结构写入流中。

```cpp
template <class Elem>
T10 put_time(struct tm* time_ptr, const Elem* time_format);
```

### <a name="parameters"></a>参数

*time_ptr*\
时间结构中提供的要写入到流中的时间值。

*time_format*\
用来写入时间值的所需格式。

### <a name="remarks"></a>备注

操控器返回一个对象，该对象在插入到流 `str` 中时会表现为 `formatted output function`。 此输出函数会对与 `str` 关联的区域设置 Facet `time_put` 调用成员函数 `put`。 Output 函数使用*time_ptr*来指示时间结构，并*time_format*以指示以 null 结尾的格式字符串的开头。 如果成功，则调用会从格式字符串插入文字文本，从时间结构插入转换的值。 此操控器随后返回 `str`。

## <a name="quoted"></a>quoted

**（C++14 中的新增功能）** 一个 iostream 操控程序，它使用 >> and << 运算符，使字符串能方便地往返进出流。

```cpp
quoted(std::string str) // or wstring
quoted(const char* str) //or wchar_t*
quoted(std::string str, char delimiter, char escape) // or wide versions
quoted(const char* str, char delimiter, char escape) // or wide versions
```

### <a name="parameters"></a>参数

*str*\
Std：： string、char\*、字符串文本或原始字符串文本或其中任何一个的宽版本（例如 std：： wstring、wchar_t\*）。

*分隔符*\
一个用户指定的字符或宽字符，用作字符串开头和结尾的分隔符。

*转义*\
一个用户指定的字符或宽字符，用作字符串内转义序列的转义字符。

### <a name="remarks"></a>备注

请参阅[使用插入运算符并控制格式](../standard-library/using-insertion-operators-and-controlling-format.md)。

### <a name="example"></a>示例

此示例显示如何通过窄字符串将 `quoted` 与默认分隔符和转义字符一起使用。 同样支持宽字符串。

```cpp
#include <iostream>
#include <iomanip>
#include <sstream>

using namespace std;

void show_quoted_v_nonquoted()
{
    // Results are identical regardless of input string type:
    // string inserted { R"(This is a "sentence".)" }; // raw string literal
    // string inserted { "This is a \"sentence\"." };  // regular string literal
    const char* inserted = "This is a \"sentence\".";  // const char*
    stringstream ss, ss_quoted;
    string extracted, extracted_quoted;

    ss << inserted;
    ss_quoted << quoted(inserted);

    cout << "ss.str() is storing       : " << ss.str() << endl;
    cout << "ss_quoted.str() is storing: " << ss_quoted.str() << endl << endl;

    // Round-trip the strings
    ss >> extracted;
    ss_quoted >> quoted(extracted_quoted);

    cout << "After round trip: " << endl;
    cout << "Non-quoted      : " << extracted << endl;
    cout << "Quoted          : " << extracted_quoted << endl;
}

int main(int argc, char* argv[])
{
    show_quoted_v_nonquoted();

    // Keep console window open in debug mode.
    cout << endl << "Press Enter to exit" << endl;
    string input{};
    getline(cin, input);
}

/* Output:
ss.str() is storing       : This is a "sentence".
ss_quoted.str() is storing: "This is a \"sentence\"."

After round trip:
Non-quoted      : This
Quoted          : This is a "sentence".

Press Enter to exit
*/
```

### <a name="example"></a>示例

以下示例显示如何提供自定义分隔符和/或转义字符：

```cpp
#include <iostream>
#include <iomanip>
#include <sstream>

using namespace std;

void show_custom_delimiter()
{
    string inserted{ R"("This" "is" "a" "heavily-quoted" "sentence".)" };
    // string inserted{ "\"This\" \"is\" \"a\" \"heavily-quoted\" \"sentence\"" };
    // const char* inserted{ "\"This\" \"is\" \"a\" \"heavily-quoted\" \"sentence\"" };
    stringstream ss, ss_quoted;
    string extracted;

    ss_quoted << quoted(inserted, '*');
    ss << inserted;
    cout << "ss_quoted.str() is storing: " << ss_quoted.str() << endl;
    cout << "ss.str() is storing       : " << ss.str() << endl << endl;

    // Use the same quoted arguments as on insertion.
    ss_quoted >> quoted(extracted, '*');

    cout << "After round trip: " << endl;
    cout << "Quoted          : " << extracted << endl;

    extracted = {};
    ss >> extracted;
    cout << "Non-quoted      : " << extracted << endl << endl;
}

void show_custom_escape()
{
    string inserted{ R"(\\root\trunk\branch\nest\egg\yolk)" };
    // string inserted{ "\\\\root\\trunk\\branch\\nest\\egg\\yolk" };
    stringstream ss, ss_quoted, ss_quoted_custom;
    string extracted;

    // Use '"' as delimiter and '~' as escape character.
    ss_quoted_custom << quoted(inserted, '"', '~');
    ss_quoted << quoted(inserted);
    ss << inserted;
    cout << "ss_quoted_custom.str(): " << ss_quoted_custom.str() << endl;
    cout << "ss_quoted.str()       : " << ss_quoted.str() << endl;
    cout << "ss.str()              : " << ss.str() << endl << endl;

    // No spaces in this string, so non-quoted behaves same as quoted
    // after round-tripping.
}

int main(int argc, char* argv[])
{
    cout << "Custom delimiter:" << endl;
    show_custom_delimiter();
    cout << "Custom escape character:" << endl;
    show_custom_escape();

    // Keep console window open in debug mode.
    cout << endl << "Press Enter to exit" << endl;
    string input{};
    getline(cin, input);
}
/* Output:
Custom delimiter:
ss_quoted.str() is storing: *"This" "is" "a" "heavily-quoted" "sentence".*
ss.str() is storing       : "This" "is" "a" "heavily-quoted" "sentence".

After round trip:
Quoted          : "This" "is" "a" "heavily-quoted" "sentence".
Non-quoted      : "This"

Custom escape character:
ss_quoted_custom.str(): "\\root\trunk\branch\nest\egg\yolk"
ss_quoted.str()       : "\\\\root\\trunk\\branch\\nest\\egg\\yolk"
ss.str()              : \\root\trunk\branch\nest\egg\yolk

Press Enter to exit
*/
```

## <a name="resetiosflags"></a>resetiosflags

清除指定标志。

```cpp
T1 resetiosflags(ios_base::fmtflags mask);
```

### <a name="parameters"></a>参数

*掩码*\
要清除的标志。

### <a name="return-value"></a>返回值

操控器返回一个对象，该对象在从流中提取或插入到流 `str`时，将调用 `str.`[setf](../standard-library/ios-base-class.md#setf)`(ios_base::`[fmtflags](../standard-library/ios-base-class.md#fmtflags)`, mask)`，然后返回 `str`。

### <a name="example"></a>示例

有关使用 `resetiosflags` 的示例，请参阅 [setw](../standard-library/iomanip-functions.md#setw)。

## <a name="setbase"></a>setbase

为整数设置基数。

```cpp
T3 setbase(int base);
```

### <a name="parameters"></a>参数

*base*\
数基。

### <a name="return-value"></a>返回值

操控器返回一个对象，该对象在从流中提取或插入到流 `str`时，调用 `str.setf(mask, `[ios_base：： basefield](../standard-library/ios-base-class.md#fmtflags)`)`，然后返回 `str`。 此处 `mask` 确定如下：

- 如果*基数*为8，则 `mask` `ios_base::`[oct](../standard-library/ios-functions.md#oct)。

- 如果*base*是10，则 mask `ios_base::`[dec](../standard-library/ios-functions.md#dec)。

- 如果*base*为16，则 `mask` `ios_base::`[十六进制](../standard-library/ios-functions.md#hex)。

- 如果*底数*为其他任何值，则 mask `ios_base::`[fmtflags](../standard-library/ios-base-class.md#fmtflags)`(0)`。

### <a name="example"></a>示例

有关使用 `setbase` 的示例，请参阅 [setw](../standard-library/iomanip-functions.md#setw)。

## <a name="setfill"></a>setfill

设置用于在右对齐显示中填充空格的字符。

```cpp
template <class Elem>
T4 setfill(Elem Ch);
```

### <a name="parameters"></a>参数

*Ch*\
用于在右对齐显示中填充空格的字符。

### <a name="return-value"></a>返回值

模板操控器返回一个对象，该对象在从流中提取或插入到流 `str`时，将调用 `str.`[fill](../standard-library/basic-ios-class.md#fill)`(Ch)`，然后返回 `str`。 类型 `Elem` 必须与流 `str`的元素类型相同。

### <a name="example"></a>示例

有关使用 `setfill` 的示例，请参阅 [setw](../standard-library/iomanip-functions.md#setw)。

## <a name="setiosflags"></a>setiosflags

设置指定标志。

```cpp
T2 setiosflags(ios_base::fmtflags mask);
```

### <a name="parameters"></a>参数

*掩码*\
要设置的标志。

### <a name="return-value"></a>返回值

操控器返回一个对象，该对象在从流中提取或插入到流 `str`时，将调用 `str.`[setf](../standard-library/ios-base-class.md#setf)`(mask)`，然后返回 `str`。

### <a name="example"></a>示例

有关使用 `setiosflags` 的示例，请参阅 [setw](../standard-library/iomanip-functions.md#setw)。

## <a name="setprecision"></a>setprecision

为浮点值设置精度。

```cpp
T5 setprecision(streamsize Prec);
```

### <a name="parameters"></a>参数

*Prec*\
浮点值的精度。

### <a name="return-value"></a>返回值

操控器返回一个对象，该对象在从流中提取或插入到流 `str`时，调用 `str.`[precision](../standard-library/ios-base-class.md#precision)`(Prec)`，然后返回 `str`。

### <a name="example"></a>示例

有关使用 `setprecision` 的示例，请参阅 [setw](../standard-library/iomanip-functions.md#setw)。

## <a name="setw"></a>setw

为流中下一元素指定显示字段的宽度。

```cpp
T6 setw(streamsize Wide);
```

### <a name="parameters"></a>参数

*宽*\
显示字段的宽度。

### <a name="return-value"></a>返回值

操控器返回一个对象，该对象在从流中提取或插入到流 `str`时，将调用 `str.`[width](../standard-library/ios-base-class.md#width)`(Wide)`，然后返回 `str`。

### <a name="remarks"></a>备注

setw 仅设置流中下一元素的宽度，并且必须插入在要对其指定宽度的每个元素之前。

### <a name="example"></a>示例

```cpp
// iomanip_setw.cpp
// compile with: /EHsc
// Defines the entry point for the console application.
//
// Sample use of the following manipulators:
//   resetiosflags
//   setiosflags
//   setbase
//   setfill
//   setprecision
//   setw

#include <iostream>
#include <iomanip>

using namespace std;

const double   d1 = 1.23456789;
const double   d2 = 12.3456789;
const double   d3 = 123.456789;
const double   d4 = 1234.56789;
const double   d5 = 12345.6789;
const long      l1 = 16;
const long      l2 = 256;
const long      l3 = 1024;
const long      l4 = 4096;
const long      l5 = 65536;
int         base = 10;

void DisplayDefault( )
{
   cout << endl << "default display" << endl;
   cout << "d1 = " << d1 << endl;
   cout << "d2 = " << d2 << endl;
   cout << "d3 = " << d3 << endl;
   cout << "d4 = " << d4 << endl;
   cout << "d5 = " << d5 << endl;
}

void DisplayWidth( int n )
{
   cout << endl << "fixed width display set to " << n << ".\n";
   cout << "d1 = " << setw(n) << d1 << endl;
   cout << "d2 = " << setw(n) << d2 << endl;
   cout << "d3 = " << setw(n) << d3 << endl;
   cout << "d4 = " << setw(n) << d4 << endl;
   cout << "d5 = " << setw(n) << d5 << endl;
}

void DisplayLongs( )
{
   cout << setbase(10);
   cout << endl << "setbase(" << base << ")" << endl;
   cout << setbase(base);
   cout << "l1 = " << l1 << endl;
   cout << "l2 = " << l2 << endl;
   cout << "l3 = " << l3 << endl;
   cout << "l4 = " << l4 << endl;
   cout << "l5 = " << l5 << endl;
}

int main( int argc, char* argv[] )
{
   DisplayDefault( );

   cout << endl << "setprecision(" << 3 << ")" << setprecision(3);
   DisplayDefault( );

   cout << endl << "setprecision(" << 12 << ")" << setprecision(12);
   DisplayDefault( );

   cout << setiosflags(ios_base::scientific);
   cout << endl << "setiosflags(" << ios_base::scientific << ")";
   DisplayDefault( );

   cout << resetiosflags(ios_base::scientific);
   cout << endl << "resetiosflags(" << ios_base::scientific << ")";
   DisplayDefault( );

   cout << endl << "setfill('" << 'S' << "')" << setfill('S');
   DisplayWidth(15);
   DisplayDefault( );

   cout << endl << "setfill('" << ' ' << "')" << setfill(' ');
   DisplayWidth(15);
   DisplayDefault( );

   cout << endl << "setprecision(" << 8 << ")" << setprecision(8);
   DisplayWidth(10);
   DisplayDefault( );

   base = 16;
   DisplayLongs( );

   base = 8;
   DisplayLongs( );

   base = 10;
   DisplayLongs( );

   return   0;
}
```

```Output

default display
d1 = 1.23457
d2 = 12.3457
d3 = 123.457
d4 = 1234.57
d5 = 12345.7

setprecision(3)
default display
d1 = 1.23
d2 = 12.3
d3 = 123
d4 = 1.23e+003
d5 = 1.23e+004

setprecision(12)
default display
d1 = 1.23456789
d2 = 12.3456789
d3 = 123.456789
d4 = 1234.56789
d5 = 12345.6789

setiosflags(4096)
default display
d1 = 1.234567890000e+000
d2 = 1.234567890000e+001
d3 = 1.234567890000e+002
d4 = 1.234567890000e+003
d5 = 1.234567890000e+004

resetiosflags(4096)
default display
d1 = 1.23456789
d2 = 12.3456789
d3 = 123.456789
d4 = 1234.56789
d5 = 12345.6789

setfill('S')
fixed width display set to 15.
d1 = SSSSS1.23456789
d2 = SSSSS12.3456789
d3 = SSSSS123.456789
d4 = SSSSS1234.56789
d5 = SSSSS12345.6789

default display
d1 = 1.23456789
d2 = 12.3456789
d3 = 123.456789
d4 = 1234.56789
d5 = 12345.6789

setfill(' ')
fixed width display set to 15.
d1 =      1.23456789
d2 =      12.3456789
d3 =      123.456789
d4 =      1234.56789
d5 =      12345.6789

default display
d1 = 1.23456789
d2 = 12.3456789
d3 = 123.456789
d4 = 1234.56789
d5 = 12345.6789

setprecision(8)
fixed width display set to 10.
d1 =  1.2345679
d2 =  12.345679
d3 =  123.45679
d4 =  1234.5679
d5 =  12345.679

default display
d1 = 1.2345679
d2 = 12.345679
d3 = 123.45679
d4 = 1234.5679
d5 = 12345.679

setbase(16)
l1 = 10
l2 = 100
l3 = 400
l4 = 1000
l5 = 10000

setbase(8)
l1 = 20
l2 = 400
l3 = 2000
l4 = 10000
l5 = 200000

setbase(10)
l1 = 16
l2 = 256
l3 = 1024
l4 = 4096
l5 = 65536
```

## <a name="see-also"></a>另请参阅

[\<iomanip>](../standard-library/iomanip.md)
