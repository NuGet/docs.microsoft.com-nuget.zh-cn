---
title: NuGet 2.8.1 发行说明
description: 发行说明，了解 NuGet 2.8.1 包括已知问题、 bug 修复、 增加的功能，以及 DCRs。
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 8787aee36d31ed5d8071b35a8c243823029d135f
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/26/2018
ms.locfileid: "31820516"
---
# <a name="nuget-281-release-notes"></a>NuGet 2.8.1 发行说明

[NuGet 2.8 发行说明](../release-notes/nuget-2.8.md) | [NuGet 2.8.2 发行说明](../release-notes/nuget-2.8.2.md)

NuGet 2.8.1 已于 2014 年 4 月 2 日发布。

## <a name="notable-features-in-the-release"></a>发行版中的值得注意的功能

### <a name="support-for-windows-phone-81-projects"></a>对 Windows Phone 8.1 项目的支持
此版本现在支持以下新目标框架名字对象可以用于记录的目标 Windows Phone 8.1 项目：

* WindowsPhone81 / WP81 （对于基于 Silverlight 的 Windows Phone 项目）
* WindowsPhoneApp81 / WPA81 （对于基于 WinRT 的 Windows Phone 应用程序项目）

### <a name="update-of-the-nuget-webmatrix-extension"></a>更新 NuGet WebMatrix 扩展
此版本更新到 WebMatrix 中找到 NuGet 客户端[NuGet.Core](https://www.nuget.org/packages/Nuget.Core/2.6.1) 2.6.1，并使它如 XDT 转换使用的功能。 更重要的是，2.6.1 核心更新使 WebMatrix 客户端安装包含较新版本的 NuGet 包`.nuspec`架构，包括 ASP.NET NuGet 包。

有关 WebMatrix 扩展更新的详细信息，请参阅这些特定[发行说明](../release-notes/nuget-2.6.1-for-WebMatrix.md)。

### <a name="bug-fixes"></a>Bug 修复
除了这些功能，此版本的 NuGet 包括其他 bug 修复。 出现了 16 的总问题在版本中解决。 有关工作的完整列表项固定在 NuGet 2.8.1，请查看[对于此版本的 NuGet 问题跟踪程序](https://nuget.codeplex.com/workitem/list/advanced?keyword=&status=All&type=All&priority=All&release=NuGet%202.8.1&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0&reasonClosed=All)。

### <a name="reshipping-with-visual-studio-14-ctp"></a>使用 Visual Studio"14"CTP reshipping
在 Visual Studio"14"CTP 中发布了第三 2014 年 6 月，NuGet 2.8.1 包装盒中。 它支持这些功能仍保持在 par 与其他 2.8.1 VSIXes 如 Visual Studio 2013 的一个。
