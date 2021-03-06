---
title: CPictureHolder 类
ms.date: 11/04/2016
f1_keywords:
- CPictureHolder
- AFXCTL/CPictureHolder
- AFXCTL/CPictureHolder::CPictureHolder
- AFXCTL/CPictureHolder::CreateEmpty
- AFXCTL/CPictureHolder::CreateFromBitmap
- AFXCTL/CPictureHolder::CreateFromIcon
- AFXCTL/CPictureHolder::CreateFromMetafile
- AFXCTL/CPictureHolder::GetDisplayString
- AFXCTL/CPictureHolder::GetPictureDispatch
- AFXCTL/CPictureHolder::GetType
- AFXCTL/CPictureHolder::Render
- AFXCTL/CPictureHolder::SetPictureDispatch
- AFXCTL/CPictureHolder::m_pPict
helpviewer_keywords:
- CPictureHolder [MFC], CPictureHolder
- CPictureHolder [MFC], CreateEmpty
- CPictureHolder [MFC], CreateFromBitmap
- CPictureHolder [MFC], CreateFromIcon
- CPictureHolder [MFC], CreateFromMetafile
- CPictureHolder [MFC], GetDisplayString
- CPictureHolder [MFC], GetPictureDispatch
- CPictureHolder [MFC], GetType
- CPictureHolder [MFC], Render
- CPictureHolder [MFC], SetPictureDispatch
- CPictureHolder [MFC], m_pPict
ms.assetid: a4f59775-704a-41dd-b5bd-2e531c95127a
ms.openlocfilehash: 5386240114550826e4bf557b63310a91590afb55
ms.sourcegitcommit: 0ab61bc3d2b6cfbd52a16c6ab2b97a8ea1864f12
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62372876"
---
# <a name="cpictureholder-class"></a>CPictureHolder 类

实现图片属性，这样用户就可以在控件中显示的图片。

## <a name="syntax"></a>语法

```
class CPictureHolder
```

## <a name="members"></a>成员

### <a name="public-constructors"></a>公共构造函数

|名称|描述|
|----------|-----------------|
|[CPictureHolder::CPictureHolder](#cpictureholder)|构造 `CPictureHolder` 对象。|

### <a name="public-methods"></a>公共方法

|名称|描述|
|----------|-----------------|
|[CPictureHolder::CreateEmpty](#createempty)|创建一个空的 `CPictureHolder` 对象。|
|[CPictureHolder::CreateFromBitmap](#createfrombitmap)|创建`CPictureHolder`从位图对象。|
|[CPictureHolder::CreateFromIcon](#createfromicon)|创建`CPictureHolder`对象从一个图标。|
|[CPictureHolder::CreateFromMetafile](#createfrommetafile)|创建`CPictureHolder`图元文件中的对象。|
|[CPictureHolder::GetDisplayString](#getdisplaystring)|检索控件容器的属性浏览器中显示的字符串。|
|[CPictureHolder::GetPictureDispatch](#getpicturedispatch)|返回`CPictureHolder`对象的`IDispatch`接口。|
|[CPictureHolder::GetType](#gettype)|指示是否`CPictureHolder`对象是一个位图、 图元文件，还是一个图标。|
|[CPictureHolder::Render](#render)|呈现图片。|
|[CPictureHolder::SetPictureDispatch](#setpicturedispatch)|集`CPictureHolder`对象的`IDispatch`接口。|

### <a name="public-data-members"></a>公共数据成员

|名称|描述|
|----------|-----------------|
|[CPictureHolder::m_pPict](#m_ppict)|指向图片对象的指针。|

## <a name="remarks"></a>备注

`CPictureHolder` 没有基类。

使用常用图片属性，开发人员可以指定位图、 图标或显示图元文件。

有关创建自定义图片属性的信息，请参阅文章[MFC ActiveX 控件：在 ActiveX 控件中使用图片](../../mfc/mfc-activex-controls-using-pictures-in-an-activex-control.md)。

## <a name="inheritance-hierarchy"></a>继承层次结构

`CPictureHolder`

## <a name="requirements"></a>要求

**标头：** afxctl.h

##  <a name="cpictureholder"></a>  CPictureHolder::CPictureHolder

构造 `CPictureHolder` 对象。

```
CPictureHolder();
```

##  <a name="createempty"></a>  CPictureHolder::CreateEmpty

创建一个空`CPictureHolder`对象，并将其连接到`IPicture`接口。

```
BOOL CreateEmpty();
```

### <a name="return-value"></a>返回值

已成功创建该对象; 如果非零值否则为 0。

##  <a name="createfrombitmap"></a>  CPictureHolder::CreateFromBitmap

使用一个位图来初始化中的图片对象`CPictureHolder`。

```
BOOL CreateFromBitmap(
    UINT idResource);

BOOL CreateFromBitmap(
    CBitmap* pBitmap,
    CPalette* pPal = NULL,
    BOOL bTransferOwnership = TRUE);

BOOL CreateFromBitmap(
    HBITMAP hbm,
    HPALETTE hpal = NULL,
    BOOL bTransferOwnership = FALSE);
```

### <a name="parameters"></a>参数

*idResource*<br/>
位图资源的资源 ID。

*pBitmap*<br/>
指向[CBitmap](../../mfc/reference/cbitmap-class.md)对象。

*pPal*<br/>
指向[CPalette](../../mfc/reference/cpalette-class.md)对象。

*bTransferOwnership*<br/>
指示图片对象是否将取得的位图和调色板对象的所有权。

*hbm*<br/>
从该位图的句柄`CPictureHolder`创建对象。

*hpal*<br/>
用于呈现位图的调色板的句柄。

### <a name="return-value"></a>返回值

已成功创建该对象; 如果非零值否则为 0。

### <a name="remarks"></a>备注

如果*bTransferOwnership*为 TRUE，调用方不应使用位图或以任何方式进行此调用后的面板对象返回。 如果*bTransferOwnership*为 FALSE 时，调用方负责确保的位图和调色板对象图片对象的生存期内保持有效。

##  <a name="createfromicon"></a>  CPictureHolder::CreateFromIcon

使用图标来初始化中的图片对象`CPictureHolder`。

```
BOOL CreateFromIcon(
    UINT idResource);

BOOL CreateFromIcon(
    HICON hIcon,
    BOOL bTransferOwnership = FALSE);
```

### <a name="parameters"></a>参数

*idResource*<br/>
位图资源的资源 ID。

*hIcon*<br/>
从该句柄图标`CPictureHolder`创建对象。

*bTransferOwnership*<br/>
指示图片对象是否将取得图标对象的所有权。

### <a name="return-value"></a>返回值

已成功创建该对象; 如果非零值否则为 0。

### <a name="remarks"></a>备注

如果*bTransferOwnership*为 TRUE 时，此调用返回后调用方应以任何方式使用图标对象。 如果*bTransferOwnership*为 FALSE 时，调用方负责确保图标对象图片对象的生存期内保持有效。

##  <a name="createfrommetafile"></a>  CPictureHolder::CreateFromMetafile

使用图元文件来初始化中的图片对象`CPictureHolder`。

```
BOOL CreateFromMetafile(
    HMETAFILE hmf,
    int xExt,
    int yExt,
    BOOL bTransferOwnership = FALSE);
```

### <a name="parameters"></a>参数

*hmf*<br/>
用于创建图元文件的句柄`CPictureHolder`对象。

*xExt*<br/>
X 图片的程度。

*yExt*<br/>
Y 的图片的范围。

*bTransferOwnership*<br/>
指示图片对象是否将取得图元文件对象的所有权。

### <a name="return-value"></a>返回值

已成功创建该对象; 如果非零值否则为 0。

### <a name="remarks"></a>备注

如果*bTransferOwnership*为 TRUE 时，此调用返回后调用方应以任何方式使用图元文件对象。 如果*bTransferOwnership*为 FALSE 时，调用方负责确保图元文件对象的图片对象生存期内保持有效。

##  <a name="getdisplaystring"></a>  CPictureHolder::GetDisplayString

检索容器的属性浏览器中显示的字符串。

```
BOOL GetDisplayString(CString& strValue);
```

### <a name="parameters"></a>参数

*strValue*<br/>
引用[CString](../../atl-mfc-shared/reference/cstringt-class.md)要保存的显示字符串。

### <a name="return-value"></a>返回值

已成功检索的字符串; 如果非零值否则为 0。

##  <a name="getpicturedispatch"></a>  CPictureHolder::GetPictureDispatch

此函数返回一个指向`CPictureHolder`对象的`IPictureDisp`接口。

```
LPPICTUREDISP GetPictureDispatch();
```

### <a name="return-value"></a>返回值

一个指向`CPictureHolder`对象的`IPictureDisp`接口。

### <a name="remarks"></a>备注

调用方必须调用`Release`上使用它完成操作后此指针。

##  <a name="gettype"></a>  CPictureHolder::GetType

指示图片是位图、 图元文件或图标。

```
short GetType();
```

### <a name="return-value"></a>返回值

一个值，该值的类型的图片。 可能的值及其含义如下所示：

|“值”|含义|
|-----------|-------------|
|PICTYPE_UNINITIALIZED|`CPictureHolder` unititialized 对象。|
|PICTYPE_NONE|`CPictureHolder` 对象为空。|
|PICTYPE_BITMAP|图片是一个位图。|
|PICTYPE_METAFILE|图片是图元文件。|
|PICTYPE_ICON|图片是一个图标。|

##  <a name="m_ppict"></a>  CPictureHolder::m_pPict

一个指向`CPictureHolder`对象的`IPicture`接口。

```
LPPICTURE m_pPict;
```

##  <a name="render"></a>  CPictureHolder::Render

呈现的图片中引用的矩形*rcRender*。

```
void Render(
    CDC* pDC,
    const CRect& rcRender,
    const CRect& rcWBounds);
```

### <a name="parameters"></a>参数

*pDC*<br/>
是用来呈现该图片的显示上下文的指针。

*rcRender*<br/>
是用来呈现该图片的矩形。

*rcWBounds*<br/>
表示呈现图片的对象的边框矩形。 对于控件，是此矩形*rcBounds*参数传递到的重写[COleControl::OnDraw](../../mfc/reference/colecontrol-class.md#ondraw)。

##  <a name="setpicturedispatch"></a>  CPictureHolder::SetPictureDispatch

连接`CPictureHolder`对象传递给`IPictureDisp`接口。

```
void SetPictureDispatch(LPPICTUREDISP pDisp);
```

### <a name="parameters"></a>参数

*pDisp*<br/>
指向新`IPictureDisp`接口。

## <a name="see-also"></a>请参阅

[层次结构图](../../mfc/hierarchy-chart.md)<br/>
[CFontHolder 类](../../mfc/reference/cfontholder-class.md)
