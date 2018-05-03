---
title: NuGet 2.0 发行说明
description: 包括已知的问题、 bug 修复、 增加的功能，以及 DCRs NuGet 2.0 的发行说明。
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 0e637a953d9d5d10394857a352be96a7f68dc4e8
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/26/2018
---
# <a name="nuget-20-release-notes"></a>NuGet 2.0 发行说明

[NuGet 1.8 发行说明](../release-notes/nuget-1.8.md) | [NuGet 2.1 发行说明](../release-notes/nuget-2.1.md)

NuGet 2.0 已于 2012 年 6 月 19 日发布。

## <a name="known-installation-issue"></a>已知的安装问题
如果你运行的 VS 2010 SP1，你可能尝试升级 NuGet，如果安装了较旧版本时遇到安装错误。

解决方法是只需卸载 NuGet，然后从 VS 扩展库安装它。  请参阅[ http://support.microsoft.com/kb/2581019 ](http://support.microsoft.com/kb/2581019)有关详细信息，或[转到 VS 修补程序直接](http://bit.ly/vsixcertfix)。

注意： 如果 Visual Studio 不会使您可以卸载的扩展 （卸载按钮为禁用），然后你可能需要重新启动 Visual Studio 中使用"以管理员身份运行"。

## <a name="package-restore-consent-is-now-active"></a>包还原同意目前处于活动状态

在此所述[将它发布在包还原同意](http://blog.nuget.org/20120518/package-restore-and-consent.html)，NuGet 2.0 现在将需要指定同意的情况下，以便启用程序包还原以联机并下载包。 请确保你提供通过包管理器配置对话框或 EnableNuGetPackageRestore 环境变量的同意。

## <a name="group-dependencies-by-target-frameworks"></a>由目标框架的组依赖项

依赖项而异的包从版本 2.0 开始，基于目标项目的框架配置文件。 这使用更新完成`.nuspec`架构。 `<dependencies>`元素现在可以包含一套`<group>`元素。 每个组包含零个或多`<dependency>`元素和`targetFramework`属性。 如果目标框架与目标项目框架配置文件兼容，位于组内的所有依赖项是一起安装。 例如：

```xml
<dependencies>
    <group>
        <dependency id="RouteMagic" version="1.1.0" />
    </group>

    <group targetFramework="net40">
        <dependency id="jQuery" />
        <dependency id="WebActivator" />
    </group>

    <group targetFramework="sl30">
    </group>
</dependencies>
```

请注意，一个组可以包含**零**依赖关系。 在上面的示例中，如果包安装到的项目是面向 Silverlight 3.0 或更高版本，将安装没有依赖关系。 如果包安装到的项目是面向.NET 4.0 或更高版本，将安装 jQuery 和 WebActivator，两个依赖关系。  如果包安装到面向早期版本的这些 2 的框架或任何其他框架的项目后，将安装 RouteMagic 1.1.0。 组之间没有任何继承。 如果项目的目标框架与相匹配`targetFramework`将安装的一个组，只有该组内部依赖关系的属性。

包可以在两种格式之一指定包的依赖项： 的简单列表的旧格式`<dependency>`元素或组。 如果`<group>`格式时，不能将此包安装到早于 2.0 的 NuGet 版本。

请注意不允许混合使用两种格式。 例如，下面的代码段是**无效**和将拒绝的 NuGet。

```xml
<dependencies>
    <dependency id="jQuery" />
    <dependency id="WebActivator" />

    <group>
        <dependency id="RouteMagic" version="1.1.0" />
    </group>
</dependencies>
```

## <a name="grouping-content-files-and-powershell-scripts-by-target-framework"></a>由目标 framework 分组内容文件和 PowerShell 脚本

程序集引用，除了内容文件和 PowerShell 脚本也可以由目标框架分组。 在中找到的相同文件夹结构`lib`用于指定目标框架的文件夹现在可将应用到相同的方式`content`和`tools`文件夹。 例如：

    \content
        \net11
            \MyContent.txt
        \net20
            \MyContent20.txt
        \net40
        \sl40
            \MySilverlightContent.html

    \tools
        \init.ps1
        \net40
            \install.ps1
            \uninstall.ps1
        \sl40
            \install.ps1
            \uninstall.ps1

**请注意**： 因为`init.ps1`解决方案级别执行且不依赖于任何单个项目，必须将它放置在直接`tools`文件夹。 如果放置在特定于框架的文件夹内，它将被忽略。

此外，NuGet 2.0 中的新功能是框架文件夹可以是*空*，在这种情况下，NuGet 将不添加程序集引用，将内容文件添加或运行特定的框架版本的 PowerShell 脚本。 在示例中，文件夹`content\net40`为空。

## <a name="improved-tab-completion-performance"></a>改进的选项卡完成性能
已更新 NuGet 包管理器控制台中的选项卡完成功能，从而显著改善性能。 将从按下 tab 键直到建议下拉列表中出现的时间少得多延迟。

## <a name="bug-fixes"></a>Bug 修复
NuGet 2.0 包括许多主要侧重于包还原同意和性能的 bug 修补程序。
有关工作的完整列表项固定在 NuGet 2.0 中，请查看[对于此版本的 NuGet 问题跟踪程序](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Closed&type=All&priority=All&release=NuGet%202.0&assignedTo=All&component=All&sortField=Votes&sortDirection=Descending&page=0)。
