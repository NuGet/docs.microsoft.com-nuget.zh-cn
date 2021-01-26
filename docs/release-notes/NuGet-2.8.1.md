---
title: NuGet 2.8.1 发行说明
description: NuGet 2.8.1 的发行说明，包括已知问题、bug 修复、新增功能和 Dcr。
author: JonDouglas
ms.author: jodou
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 4dcd8ab140026c39345f850ac00a7a5f26a0e62c
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/26/2021
ms.locfileid: "98776771"
---
# <a name="nuget-281-release-notes"></a>NuGet 2.8.1 发行说明

[NuGet 2.8 发行说明](../release-notes/nuget-2.8.md)  | [NuGet 2.8.2 发行说明](../release-notes/nuget-2.8.2.md)

NuGet 2.8.1 于2014年4月2日发布。

## <a name="notable-features-in-the-release"></a>版本中值得注意的功能

### <a name="support-for-windows-phone-81-projects"></a>支持 Windows Phone 8.1 项目
此版本现在支持以下新的目标框架名字对象，可用于针对 Windows Phone 8.1 项目：

* 基于 Silverlight 的 Windows Phone 项目的 WindowsPhone81/WP81 () 
* 基于 WinRT 的 Windows Phone 应用项目的 WindowsPhoneApp81/WPA81 () 

### <a name="update-of-the-nuget-webmatrix-extension"></a>NuGet WebMatrix 扩展的更新
此版本将在 WebMatrix 中找到的 NuGet 客户端更新为 [nuget.exe](https://www.nuget.org/packages/Nuget.Core/2.6.1) 2.6.1，并附带 it 功能，如 XDT 转换。 更重要的是，2.6.1 core 更新允许 WebMatrix 客户端安装包含最新版本的架构的 NuGet 包 `.nuspec` ，其中包括 ASP.NET NuGet 包。

有关 WebMatrix 扩展更新的详细信息，请参阅这些特定的 [发行说明](../release-notes/nuget-2.6.1-for-WebMatrix.md)。

### <a name="bug-fixes"></a>Bug 修复
除了这些功能以外，此版本的 NuGet 还包括其他 bug 修复。 此版本中解决了16个问题。 有关 NuGet 2.8.1 中修复的工作项的完整列表，请查看 [此版本的 NuGet 问题跟踪程序](https://nuget.codeplex.com/workitem/list/advanced?keyword=&status=All&type=All&priority=All&release=NuGet%202.8.1&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0&reasonClosed=All)。

### <a name="reshipping-with-visual-studio-14-ctp"></a>导致 with Visual Studio "14" CTP
在 Visual Studio "14" CTP 年6月 2014 3 日发布的 CTP 中，NuGet 2.8.1 随附在包装盒中。 它支持的功能与其他 2.8.1 VSIXes （例如 Visual Studio 2013 的功能）保持不变。
