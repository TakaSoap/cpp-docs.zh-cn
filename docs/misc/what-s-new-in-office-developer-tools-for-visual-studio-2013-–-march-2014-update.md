---
title: "Visual Studio 2013 的 Office 开发工具的新增功能 – 2014 年 3 月版更新 | Microsoft Docs"
ms.custom: ""
ms.date: "10/29/2016"
ms.prod: "visual-studio-dev14"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-csharp"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: e701c650-2a2b-4b18-9f7b-04d4fc59a05d
caps.latest.revision: 2
caps.handback.revision: 2
author: "stevehoag"
ms.author: "shoag"
manager: "wpickett"
---
# Visual Studio 2013 的 Office 开发工具的新增功能 – 2014 年 3 月版更新
**“Visual Studio 2013 的 Office 开发人员工具 – 2014 年 3 月版更新”**包括很多新功能，这些功能改进了用于云企业应用的 Visual Studio 2013 附带的工具和 Office\/SharePoint 开发应用。  它还允许你生成在 Office 2013 SP1 和 Office 365 中启用的 Office 相关应用程序的新类型。  
  
-   [云企业应用程序的新增功能](#cba)  
  
-   [Office 相关应用程序开发的新增功能](#office)  
  
-   [SharePoint 相关应用程序开发的新增功能](#sharepoint)  
  
##  <a name="cba"></a> 云企业应用程序的新增功能  
 Visual Studio 2013 引入了云企业应用程序项目模板，可使用此模板快速生成现代企业应用程序，这些应用程序将与 Office 365 平台体验集成并对其进行扩展。  在此版本中，添加了一些新功能，旨在更好地支持连接到企业数据并集成文档库，以及更好地支持快速应用程序开发。  
  
### 附加到企业数据  
 **新的 SAP 数据源**  
  
 企业数据在很多企业应用程序中起着重要作用。  现在，许多不同类型的企业数据源已上市。  除了数据库、SharePoint、OData 服务和 WCF RIA 服务数据源之外，2014 年 3 月版更新工具还提供对 SAP Netweaver 网关的一流支持。  在连接到 SAP 后，你的云企业应用程序现在将遵循 Phone、WebAddress 和 Email 的 SAP 批注，从而简化 SAP Netweaver 网关中使用的实体配置。  
  
 **连接数据源向导改进**  
  
 很多企业数据源存储大量数据实体，云企业应用程序可能需要仅与其中一些数据实体进行交互。  为了使你能够轻松找到要连接到的实体，**“连接数据源向导”**现在允许你基于名称搜索实体并按不同的类别筛选实体。  它还显示数据源中实体的关系。  
  
 **连接到大型数据集时的性能改进**  
  
 如果你的云企业应用程序需要连接到大型数据集，你将注意到**“连接数据源向导”**中的性能改进。  已针对大型数据集改进实体设计器的布局，因此，你可以轻松浏览实体之间的关系。  此外，它现在允许你更改实体中的属性顺序。  
  
 **业务类型改进**  
  
 除了大量实体外，很多企业数据源还包含复杂的业务类型，如复杂类型。  2014 年 3 月版更新包含新的针对复杂数据类型的支持。  
  
 如果你的云企业应用程序连接到包含**“人员”**类型列的 SharePoint 列表，则在运行此应用程序时，这些列将作为联系人自动亮起。  例如，如果你在计算机上安装了 Lync，并且它连接到 SharePoint 站点使用的相同 Active Directory，则人员类型列会将值显示为 Lync 联系人并自动激活云企业应用程序中的 Lync 功能。  
  
### 集成文档  
 文档存储和检索是针对许多企业应用程序的常见要求。  例如，当用户查看某个产品的详细信息时，你可能需要提供对与该产品相关的文档列表的访问权。  你还可能需要允许你的用户管理应用程序中的文档。  现在，利用云企业应用程序，你可以连接到 SharePoint 文档库列表并建立列表实体和另一个数据实体之间的关系。  利用此功能，你可以快速生成显示与某个特定数据字段相关的文档的应用程序。  
  
 此外，在将你的应用程序连接到 SharePoint 主机 Web 文档库时，此应用程序屏幕将与一组新的文档控件集成，这将允许你的用户创建新的 Office 文档（空白文档或从连接的文档库中提供的文档模板），在 Office Web 应用或 Office 客户端中打开文档以及上载现有文档。  这些工具提供的所有功能都不要求你执行任何额外操作。  
  
### 快速应用程序开发改进  
 **增强的摘要控件**  
  
 为了更好地使用不同的数据类型，已更新摘要控件来显示基础语义类型的默认控件。  利用此支持，如果摘要控件与**“人员”**类型关联，则摘要控件将使用**“人员查看器”**控件，后者将显示与人员有关的其他信息（例如，人员的姓名、标题和显示图像）。  
  
> [!NOTE]
>  摘要控件的 `contentItem.value` 属性现在将返回摘要属性值，而不是整个数据实体。  如果你已将 `contentItem.value` 用于摘要控件来获取用于访问实体中的其他属性的实体，则需要更新你的代码以改用 `contentItem.data`。  
  
 **用于在屏幕上筛选大型数据集的内置逻辑**  
  
 2014 年 3 月版更新包含内置的数据筛选支持。  云企业应用程序生成移动优化的屏幕，这不需要你执行任何新的操作，并且允许你的用户搜索数据表并使用表标题对表进行排序。  
  
 **创建屏幕集**  
  
 为了帮助你快速生成常用屏幕以便用户在你的应用程序中浏览、查看和编辑数据，此版本中引入了常见屏幕集。  你现在不需要依次创建浏览、查看和新建\/编辑屏幕，而只需选择创建常见屏幕集即可立即生成所有这三种类型的屏幕。  此常见屏幕集还将自动为你连接屏幕之间的数据表、导航和关系。  
  
 **应用书签**  
  
 用户经常需要为应用程序中的某个页面加入书签以便快速返回该页面。  此版本中的云企业应用程序现在支持加入书签，而无需你编写任何代码。  它允许用户为应用程序中的任何页面加入书签。  用户还可以将某个页面固定到其移动设备上的开始屏幕。  
  
##  <a name="office"></a> Office 相关应用程序开发的新增功能  
 **Office 相关应用程序的新类型**  
  
 Office 2013 SP1 和 Office 365 支持 PowerPoint 内容应用和 Access Web App 内容应用，并允许在撰写窗体中激活你的邮件应用（例如，当用户撰写新的电子邮件或创建新的约会时）。  2014 年 3 月版更新在整个开发周期（从项目创建、清单编辑、编程、调试到发布）中都支持所有这些新应用类型。  还更新了 Napa 以支持这些新的应用类型。  
  
 **已更新的项目模板**  
  
 已更新 Office 开发人员工具中的 Office 相关应用程序项目创建向导，以便为应用程序创建提供更有条理的选项。  尤其是对于内容应用，此版本引入了两个项目模板。  一个项目模板仅用于创建基本应用（包含最小代码示例），另一个项目模板包含多个示例代码以演示如何实现 Excel 相关应用程序和 Access Web App 应用程序来可视化数据。  你可以在项目创建向导中选择这两个项目模板之一以快速开始操作你的应用。  
  
 **用于激活应用的更多选项**  
  
 除了新的应用类型之外，Office 2013 SP1 和 Office 365 还为你提供了一种新的方法来指定何时可激活应用。  除了可在其中激活应用（Word、Excel、PowerPoint 等）的应用主机外，它还定义了 API 集的列表，其中每个集均表示一组带相同语义（Selection、TableBindings 等）的 Office JSOM API。对于应用的关键功能中调用的 Office API，你可以将相应的 API 集添加到应用清单中，以避免在不支持这些 API 的 Office 主机中激活此应用。  通过执行这些操作，你可以跨不同版本在尽可能多的主机上激活你的应用，而无需添加复杂的编程逻辑。  
  
 为了支持此类激活，Office 相关应用程序工具在任务窗格应用和内容应用清单编辑器中引入了一个“激活”页。  它不仅允许你更新应用的 API 集，还根据 API 集以及你选择的应用主机显示将在何处激活此应用。  
  
 **更好的 IntelliSense 支持**  
  
 为了提供针对新应用类型和新应用激活模型的更佳编程体验，IntelliSense 也得到了改进。  IntelliSense 只显示对目标应用主机有效的 API。  例如，如果你生成仅面向 Access Web App 的内容应用，则 Access Web App 中支持的 API 将显示在 IntelliSense 中而非任何其他位置。  如果你仅为撰写窗体生成邮件应用，则将在 IntelliSense 中隐藏读取窗体邮件应用 API，以使你绝不会误用 API。  此外，任务窗格应用\/内容应用清单编辑器中的“激活”页面包含一个选项，可以选择该选项以仅显示带属于清单中指定的 API 集的 API 的 IntelliSense。  
  
 **调试改进**  
  
 2014 年 3 月版更新还提供了更多的调试选项。  对于 Excel 任务窗格和内容应用，你可以在 Office Web App 和桌面客户端中对其进行调试。  你可以通过应用项目属性窗口在 IE、Chrome 和 Firefox（如果它们安装在计算机上）之间进行选择，以启动 Office Web App 进行调试。  
  
 除了 Office Web App 调试支持之外，新工具还使你能够调试 Office 相关应用程序和 SharePoint 相关应用程序的“仅我的代码”。  启用此选项后，你将不再担忧与你的代码无关的 JavaScript 异常。  
  
##  <a name="sharepoint"></a> SharePoint 相关应用程序开发的新增功能  
 **面向不同版本的 SharePoint**  
  
 现在，利用 SharePoint 相关应用程序工具，你可以使你的应用面向与 SharePoint Online 兼容的 SharePoint Server 2013 或仅面向 SharePoint Online。  借助 SharePoint 相关应用程序项目属性页中的简单开关，这些工具将相应地更新项目中使用的 SharePoint 版本号和 SharePoint 客户端组件程序集引用。  
  
 **客户端 Web 部件的 MVS 支持**  
  
 为了增强对 MVC Web 应用程序的支持，此版本中添加了对客户端 Web 部件页的 MVC 支持。  只要 SharePoint 相关应用程序项目与 MVC 应用程序关联，当你添加客户端 Web 部件并选择在客户端 Web 部件创建向导中创建新的部件页时，就会将一个客户端 Web 部件控制器以及该控制器要附带的默认视图添加到 MVC 应用程序而不是 .aspx 页面中。  
  
 **远程事件接收器的列表实例支持**  
  
 在 Visual Studio 2013 中，远程事件接收器创建向导仅允许你选取列表模板。  现在，此向导还为你显示项目中的所有列表实例以供你选择并用来创建远程事件接收器。  这些工具将基于你的选择创建正确的清单。  
  
 **改进的列表模板生成**  
  
 此版本还包括 SharePoint 列表模板项的修复。  利用 2014 年 3 月版更新，在创建 SharePoint 列表模板时，列表模板清单中的 Type 特性将设置为其父模板的类型（而不是像以前一样的默认值“10000”）。  利用此修复，你的新列表模板将免费从其父模板继承所有属性。  对于包含大量自定义功能的复杂列表模板类型（如文档库），这特别有用。