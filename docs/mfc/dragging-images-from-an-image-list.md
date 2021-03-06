---
title: 从图像列表拖动图像
ms.date: 11/04/2016
helpviewer_keywords:
- CImageList class [MFC], dragging images from
- dragging images from image lists [MFC]
- image lists [MFC], dragging images from
- images [MFC], dragging from image lists
ms.assetid: af691db8-e4f0-4046-b7b9-9acc68d3713d
ms.openlocfilehash: 3035e6f21d38568b364fce02358c3baed4870bc3
ms.sourcegitcommit: fcb48824f9ca24b1f8bd37d647a4d592de1cc925
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/15/2019
ms.locfileid: "69508651"
---
# <a name="dragging-images-from-an-image-list"></a>从图像列表拖动图像

[CImageList](../mfc/reference/cimagelist-class.md)包括用于在屏幕上拖动图像的函数。 拖动函数可以流畅地拖动图像，光标没有任何闪烁。 添加了蒙板的图像和未添加蒙板的图像均可拖动。

[BeginDrag](../mfc/reference/cimagelist-class.md#begindrag)成员函数开始拖动操作。 参数包括要拖动图像的索引和图像中作用点的位置。 作用点是拖动函数识别为图像的确切屏幕位置的单一像素。 通常，应用程序将设置作用点，以便它与鼠标光标的作用点一致。 [DragMove](../mfc/reference/cimagelist-class.md#dragmove)成员函数将图像移到新位置。

[System.windows.dragdrop.dragenter>](../mfc/reference/cimagelist-class.md#dragenter)成员函数设置拖动图像在窗口中的初始位置, 并在该位置绘制图像。 参数包括一个指向绘制图像窗口的指针和一个指定窗口中初始位置的坐标的点。 坐标相对于窗口的左上角，而不是工作区。 上述情况同样适用于将坐标作为参数使用的所有图像拖动函数。 这意味着您在指定坐标时必须补偿窗口元素的宽度，如边框、标题栏和菜单栏。 如果在调用`DragEnter`时指定了**空**的窗口句柄, 则拖动函数将在与桌面窗口相关联的设备上下文中绘制图像, 并且坐标相对于屏幕的左上角。

`DragEnter` 在拖动操作期间将锁定给定窗口的所有其他更新。 如果需要在拖动操作期间执行任何绘图 (例如突出显示拖放操作的目标), 则可以使用[system.windows.dragdrop.dragleave>](../mfc/reference/cimagelist-class.md#dragleave)成员函数暂时隐藏拖动后的图像。 还可以使用[DragShowNoLock](../mfc/reference/cimagelist-class.md#dragshownolock)成员函数。

拖动完映像后, 调用[EndDrag](../mfc/reference/cimagelist-class.md#enddrag) 。

[SetDragCursorImage](../mfc/reference/cimagelist-class.md#setdragcursorimage)成员函数通过将给定图像 (通常是鼠标光标图像) 与当前拖动图像组合来创建新的拖动图像。 由于拖动函数在拖动操作期间使用新图像, 因此应在调用`SetDragCursorImage`后使用 Windows [ShowCursor](/windows/win32/api/winuser/nf-winuser-showcursor)函数隐藏实际的鼠标光标。 否则，系统在拖动操作期间可能看起来具有两个鼠标光标。

当应用程序调用 `BeginDrag` 后，系统将创建一个临时的内部图像列表并将指定拖动图像复制到内部列表中。 您可以使用[GetDragImage](../mfc/reference/cimagelist-class.md#getdragimage)成员函数来检索指向临时拖动图像列表的指针。 此函数还将检索当前拖动位置和拖动图像相对于拖动位置的偏移量。

## <a name="see-also"></a>请参阅

[使用 CImageList](../mfc/using-cimagelist.md)<br/>
[控件](../mfc/controls-mfc.md)
