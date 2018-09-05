---
title: NuGet 1.3 的发行说明
description: 包括已知的问题、 bug 修复、 新增的功能和 Dcr NuGet 1.3 的发行说明。
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: fa89af100096356c2ffb4d6c501c4a34296ad0ea
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/04/2018
ms.locfileid: "43551346"
---
# <a name="nuget-13-release-notes"></a>NuGet 1.3 的发行说明

[NuGet 1.2 发行说明](../release-notes/nuget-1.2.md) | [NuGet 1.4 发行说明](../release-notes/nuget-1.4.md)

NuGet 1.3 已于 2011 年 4 月 25 日发布。

## <a name="new-features"></a>新增功能

### <a name="streamlined-package-creation-with-symbol-server-integration"></a>简化了的创建符号服务器集成包

NuGet 团队的人员也与合作[SymbolSource.org](http://www.symbolsource.org/)提供您的包以及发布你的源和 PDB 的真正简单的方法。 这允许使用者在包的单步执行您在调试器中的包源。 有关更多详细信息，请阅读[创建和发布符号包](../create-packages/symbol-packages.md)发布具有源的 NuGet 包的简单方法。 此外可观看实时演示此功能的深度中的 NuGet 的一部分在 Mix11 通信。 此功能完全进行了演示视频的 20 分钟标记处开始。

### <a name="open-packagepage-command"></a>`Open-PackagePage` 命令

此命令让可以轻松获得到从包管理器控制台中的包的项目页。 它还提供了选项，若要打开许可证 URL 和包报告滥用行为页。
该命令的语法是：

    Open-PackagePage -Id <string> [-Version] [-Source] [-License] [-ReportAbuse] [-PassThru]

`-PassThru`选项用来返回指定的 URL 的值。

示例：

    PM> Open-PackagePage Ninject

将打开到 Ninject 包中指定的项目 URL 的浏览器。

    PM> Open-PackagePage Ninject -License

许可证 URL Ninject 包中指定浏览器中打开。

    PM> Open-PackagePage Ninject -ReportAbuse

报告滥用行为用于指定包的当前包源中的 URL 浏览器中打开。

    PM> $url = Open-PackagePage Ninject -License -WhatIf -PassThru

分配给变量，$url，而无需在浏览器中打开 URL 许可证 URL。

### <a name="performance-improvements"></a>性能改进

NuGet 1.3 引入了大量性能改进。 NuGet 1.3 可避免通过包括每个用户本地缓存多次下载相同版本的包。 可以访问和通过包管理器设置对话框中清除缓存：

![NuGet 包缓存设置的选项对话框](./media/nuget-options.png)

其他性能改进包括添加支持 HTTP 压缩和改进 Visual Studio 中的包安装速度。

### <a name="visual-studio-and-nugetexe-uses-the-same-list-of-package-sources"></a>Visual Studio 和 nuget.exe 使用相同的包源列表

在 NuGet 1.3 之前的使用并由 nuget.exe 和 NuGet Visual Studio 外接程序的包源列表没有存储在相同的位置。 NuGet 1.3 现在，在这两个位置中使用相同的列表。 列表存储在`NuGet.Config`并存储在应用程序数据文件夹中。

### <a name="nugetexe-ignores-files-and-folders-that-start-with--by-default"></a>nuget.exe 会忽略文件和文件夹以开头的。 默认情况下

为了使 NuGet 很好地配合源代码管理系统，此类 Subversion 和 Mercurial，nuget.exe 忽略文件夹和文件开头的。 ' 字符创建包时。 这可以使用重写两个新标记：

* __-NoDefaultExcludes__用于替代此设置，包括所有文件。
* __-排除__用于添加要使用的模式中排除其他文件/文件夹。 例如，若要排除具有 '.bak' 文件扩展名的所有文件

```
nuget Pack MyPackage.nuspec -Exclude **\*.bak
```  

_注意： 模式不是默认情况下的递归。_

### <a name="support-for-wix-projects-and-the-net-micro-framework"></a>对 WiX 项目和.NET Micro Framework 的支持

由于社区贡献，NuGet 还 WiX 项目类型，以及.NET Micro Framework 的支持。

## <a name="bug-fixes"></a>Bug 修复

Bug 修复的完整列表，请查看[对于此版本的 NuGet 问题跟踪程序](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=All&type=All&priority=All&release=NuGet%201.3&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0)。

## <a name="bug-fixes-worth-noting"></a>值得注意的 bug 修复

* 带有源文件的包工作在两个网站和 Web 应用程序项目中。
对于网站，请将源文件复制到`App_Code`文件夹
