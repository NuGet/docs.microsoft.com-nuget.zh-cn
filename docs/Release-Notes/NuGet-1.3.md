---
title: NuGet 1.3 的发行说明
description: 包括已知的问题、 bug 修复、 增加的功能，以及 DCRs NuGet 1.3 的发行说明。
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: c0284fe0afb11bf6465897132cccd160674ea3e1
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/26/2018
---
# <a name="nuget-13-release-notes"></a>NuGet 1.3 的发行说明

[NuGet 1.2 发行说明](../release-notes/nuget-1.2.md) | [NuGet 1.4 的发行说明](../release-notes/nuget-1.4.md)

NuGet 1.3 已于 2011 年 4 月 25 日发布。

## <a name="new-features"></a>新增功能

### <a name="streamlined-package-creation-with-symbol-server-integration"></a>简化的创建符号服务器集成包

NuGet 团队的整个过程的人员合作[SymbolSource.org](http://www.symbolsource.org/)以提供了非常简单的方法，以及你的包中发布你的源和 PDB。 这允许你的包的使用者单步执行你在调试器中的包的源。 有关详细信息，请阅读[创建和发布符号包](../create-packages/symbol-packages.md)发布 NuGet 包与源的简单方法。 你也可以观看实时演示此功能的深度 NuGet 的一部分在 Mix11 对话。 此功能完全进行了演示视频的 20 分钟标记处开始。

### <a name="open-packagepage-command"></a>`Open-PackagePage` 命令

此命令可以轻松获取到从程序包管理器控制台中的包的项目页。 它还提供了选项，若要打开的许可证 URL 和包的报告滥用行为页。
该命令的语法是：

    Open-PackagePage -Id <string> [-Version] [-Source] [-License] [-ReportAbuse] [-PassThru]

`-PassThru`选项用于返回指定的 URL 的值。

示例：

    PM> Open-PackagePage Ninject

将打开 Ninject 程序包中指定的项目 URL 在浏览器。

    PM> Open-PackagePage Ninject -License

将打开 Ninject 程序包中指定的许可证 URL 在浏览器。

    PM> Open-PackagePage Ninject -ReportAbuse

打开浏览器中用于指定包的报告滥用行为的当前程序包源的 URL。

    PM> $url = Open-PackagePage Ninject -License -WhatIf -PassThru

将许可证 URL 分配给变量，$url，，而无需在浏览器打开 URL。

### <a name="performance-improvements"></a>性能改进

NuGet 1.3 引入了大量的性能改进。 NuGet 1.3 可避免通过包括每用户本地缓存多次下载相同版本的包。 可以访问缓存，并将其清除通过程序包管理器设置对话框：

![使用包缓存设置的 NuGet 选项对话框](./media/nuget-options.png)

其他性能改进包括添加对 HTTP 压缩的支持和改进 Visual Studio 中的包安装速度。

### <a name="visual-studio-and-nugetexe-uses-the-same-list-of-package-sources"></a>Visual Studio 和 nuget.exe 使用相同的包源列表

在 NuGet 1.3 之前 nuget.exe 和 NuGet Visual Studio 外接程序使用的包源的列表未存储在同一位置。 NuGet 1.3 现在使用这两个位置中的相同列表。 列表存储在`NuGet.Config`并且存储在应用程序数据文件夹。

### <a name="nugetexe-ignores-files-and-folders-that-start-with--by-default"></a>nuget.exe 忽略文件和文件夹以开头的。 默认情况下

为了进行很好地配合源代码管理系统，此类子版本号和 Mercurial 的 NuGet，nuget.exe 忽略文件夹和开头的文件。 ' 字符创建包时。 这可以重写使用两个新的标志：

* __-NoDefaultExcludes__用于重写此设置，并包括所有文件。
* __-排除__用于添加要使用的模式中排除其他文件/文件夹。 例如，若要排除具有 '.bak' 文件扩展名的所有文件

```
nuget Pack MyPackage.nuspec -Exclude **\*.bak
```  

_注意： 的模式不是默认情况下的递归。_

### <a name="support-for-wix-projects-and-the-net-micro-framework"></a>WiX 项目和.NET Micro Framework 的支持

感谢社区贡献 NuGet 包括对 WiX 项目类型，以及.NET Micro Framework 支持。

## <a name="bug-fixes"></a>Bug 修复

Bug 修复的完整列表，请查看[对于此版本的 NuGet 问题跟踪程序](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=All&type=All&priority=All&release=NuGet%201.3&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0)。

## <a name="bug-fixes-worth-noting"></a>值得注意的 bug 修复

* 源文件的包可以使用这两个网站和 Web 应用程序项目中。
对于网站，将源文件复制到`App_Code`文件夹
