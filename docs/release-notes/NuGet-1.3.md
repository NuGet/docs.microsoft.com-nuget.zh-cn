---
title: NuGet 1.3 发行说明
description: NuGet 1.3 的发行说明，包括已知问题、bug 修复、新增功能和 Dcr。
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 45d5caa46d532670e370b81f675663b3c5aaaa95
ms.sourcegitcommit: fe34b1fc79d6a9b2943a951f70b820037d2dd72d
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/04/2019
ms.locfileid: "74825260"
---
# <a name="nuget-13-release-notes"></a>NuGet 1.3 发行说明

[Nuget 1.2 发行说明](../release-notes/nuget-1.2.md) | [Nuget 1.4 发行说明](../release-notes/nuget-1.4.md)

NuGet 1.3 于2011年4月25日发布。

## <a name="new-features"></a>新增功能

### <a name="streamlined-package-creation-with-symbol-server-integration"></a>通过符号服务器集成简化包创建

NuGet 团队与[SymbolSource.org](http://www.symbolsource.org/)的用户进行了合作，提供了一种非常简单的方式来将源和 PDB 与包一起发布。 这允许你的包的使用者在调试器中单步执行包的源。 有关更多详细信息，请参阅[创建和发布符号包](../create-packages/symbol-packages.md)使用源发布 NuGet 包的简单方法。 你还可以观看此功能的实时演示，作为 NuGet 深入了解 Mix11。 此功能在视频的20分钟标记处开始完全演示。

### <a name="open-packagepage-command"></a>`Open-PackagePage` 命令

使用此命令可以轻松地从包管理器控制台中访问包的项目页。 它还提供了用于打开包的 "许可证 URL" 和 "报表滥用" 页的选项。
命令的语法为：

    Open-PackagePage -Id <string> [-Version] [-Source] [-License] [-ReportAbuse] [-PassThru]

`-PassThru` 选项用于返回指定 URL 的值。

例如：

    PM> Open-PackagePage Ninject

打开浏览器，指向在 Ninject 包中指定的项目 URL。

    PM> Open-PackagePage Ninject -License

打开浏览器，指向在 Ninject 包中指定的许可证 URL。

    PM> Open-PackagePage Ninject -ReportAbuse

打开浏览器，指向当前包源中用于报告指定包的滥用的 URL。

    PM> $url = Open-PackagePage Ninject -License -WhatIf -PassThru

将许可证 URL 分配给变量 $url，而无需在浏览器中打开该 URL。

### <a name="performance-improvements"></a>性能改进

NuGet 1.3 引入了大量性能改进。 NuGet 1.3 通过包含本地的每用户缓存避免多次下载包的同一版本。 可以通过 "包管理器设置" 对话框访问和清除缓存：

![包含包缓存设置的 NuGet 选项对话框](./media/nuget-options.png)

其他性能改进包括添加对 HTTP 压缩的支持和在 Visual Studio 中提高包的安装速度。

### <a name="visual-studio-and-nugetexe-uses-the-same-list-of-package-sources"></a>Visual Studio 和 nuget.exe 使用相同的包源列表

在 NuGet 1.3 之前，nuget.exe 和 NuGet Visual Studio 外接程序使用的包源列表未存储在同一位置。 NuGet 1.3 现在同时在这两个位置使用同一列表。 该列表存储在 `NuGet.Config` 中并存储在 AppData 文件夹中。

### <a name="nugetexe-ignores-files-and-folders-that-start-with--by-default"></a>默认情况下，nuget.exe 忽略以 "." 开头的文件和文件夹

为了使 NuGet 适用于源控制系统（如 Subversion 和 Mercurial），nuget.exe 会忽略在创建包时以 "." 字符开头的文件夹和文件。 这可以使用两个新标志进行重写：

* __-NoDefaultExcludes__用于覆盖此设置并包括所有文件。
* __-Exclude__用于使用模式添加要排除的其他文件/文件夹。 例如，若要排除文件扩展名为 ".bak" 的所有文件

```cli
nuget Pack MyPackage.nuspec -Exclude **\*.bak
```  

_注意：默认情况下，该模式不是递归的。_

### <a name="support-for-wix-projects-and-the-net-micro-framework"></a>对 WiX 项目和 .NET 微框架的支持

由于社区贡献，NuGet 包含对 WiX 项目类型和 .NET 微框架的支持。

## <a name="bug-fixes"></a>Bug 修复

有关 bug 修复的完整列表，请查看[此版本的 NuGet 问题跟踪](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=All&type=All&priority=All&release=NuGet%201.3&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0)程序。

## <a name="bug-fixes-worth-noting"></a>Bug 修复值得注意

* 包含源文件的包可在网站和 Web 应用程序项目中使用。
对于网站，源文件将复制到 `App_Code` 文件夹中
