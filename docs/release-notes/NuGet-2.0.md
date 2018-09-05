---
title: NuGet 2.0 发行说明
description: 包括已知的问题、 bug 修复、 新增的功能和 Dcr NuGet 2.0 发行说明。
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: f32eea9260ce7e307ff56b7f3e6b48c6d98e6c90
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/04/2018
ms.locfileid: "43547570"
---
# <a name="nuget-20-release-notes"></a>NuGet 2.0 发行说明

[NuGet 1.8 发行说明](../release-notes/nuget-1.8.md) | [NuGet 2.1 发行说明](../release-notes/nuget-2.1.md)

NuGet 2.0 已于 2012 年 6 月 19 日发布。

## <a name="known-installation-issue"></a>已知的安装问题
如果运行 VS 2010 SP1，你可能会遇到安装错误，尝试升级 NuGet，如果您有安装了旧版本时。

解决方法是简单地卸载 NuGet，然后从 VS 扩展库安装它。  请参阅[ http://support.microsoft.com/kb/2581019 ](http://support.microsoft.com/kb/2581019)有关详细信息，或[直接转到 VS 修补程序](http://bit.ly/vsixcertfix)。

注意： 如果 Visual Studio 不会使您可以卸载的扩展 （卸载按钮被禁用），然后您可能需要重启 Visual Studio 中使用"以管理员身份运行"。

## <a name="package-restore-consent-is-now-active"></a>包还原同意目前处于活动状态

中所述[将它发布在包还原同意](http://blog.nuget.org/20120518/package-restore-and-consent.html)，NuGet 2.0 现在要求提供同意的情况下，若要启用包还原以联机并下载包。 请确保提供了同意通过包管理器配置对话框或 EnableNuGetPackageRestore 的环境变量。

## <a name="group-dependencies-by-target-frameworks"></a>组的目标框架的依赖项

从 2.0 版开始，包依赖项而异，根据目标项目的框架配置文件。 这可以使用的已更新实现`.nuspec`架构。 `<dependencies>`元素现在可以包含一系列`<group>`元素。 每个组包含零个或更多`<dependency>`元素和一个`targetFramework`属性。 如果目标框架与目标项目框架配置文件兼容时，组内的所有依赖项是一起安装。 例如：

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

请注意，一个组可以包含**零**依赖项。 在上面的示例中，如果包已安装到的项目是面向 Silverlight 3.0 或更高版本，将安装没有依赖关系。 如果包已安装到的项目面向.NET 4.0 或更高版本，将安装 jQuery 和 WebActivator，两个依赖关系。  如果包安装到目标的早期版本的这些 2 框架或任何其他框架的项目时，将安装 RouteMagic 1.1.0。 组之间没有任何继承。 如果项目的目标框架匹配`targetFramework`将安装组，只有该组中的依赖项属性。

包可以在两种格式之一指定包的依赖项： 旧格式的平面列表`<dependency>`元素或组。 如果`<group>`使用格式时，不能将包安装到早于 2.0 的 NuGet 版本。

请注意不允许混合使用这两种格式。 例如，以下代码片段是**无效**和将拒绝的 NuGet。

```xml
<dependencies>
    <dependency id="jQuery" />
    <dependency id="WebActivator" />

    <group>
        <dependency id="RouteMagic" version="1.1.0" />
    </group>
</dependencies>
```

## <a name="grouping-content-files-and-powershell-scripts-by-target-framework"></a>按目标框架进行分组的内容文件和 PowerShell 脚本

程序集引用，除了内容文件和 PowerShell 脚本也可以由目标框架分组。 在中找到的相同文件夹结构`lib`用于指定目标框架文件夹现在可以应用到相同的方式`content`和`tools`文件夹。 例如：

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

**请注意**： 因为`init.ps1`解决方案级别执行，不依赖于任何单个项目，必须将它放置下方`tools`文件夹。 如果放置在特定于框架的文件夹中，将忽略它。

此外，NuGet 2.0 中的新功能是框架文件夹可以是*空*，在这种情况下，NuGet 将不添加程序集引用、 添加内容文件或运行特定的框架版本的 PowerShell 脚本。 在示例中的文件夹上方`content\net40`为空。

## <a name="improved-tab-completion-performance"></a>改进了选项卡完成性能
已更新 NuGet 包管理器控制台中的选项卡完成功能，以显著提高性能。 将从按下 tab 键直至建议下拉列表中显示的时间要少得多延迟。

## <a name="bug-fixes"></a>Bug 修复
NuGet 2.0 包括侧重于包还原同意和性能的许多 bug 修复。
有关工作的完整列表项中已修复 NuGet 2.0，请查看[对于此版本的 NuGet 问题跟踪程序](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Closed&type=All&priority=All&release=NuGet%202.0&assignedTo=All&component=All&sortField=Votes&sortDirection=Descending&page=0)。
