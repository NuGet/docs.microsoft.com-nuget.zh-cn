---
title: NuGet 2.0 发行说明
description: NuGet 2.0 的发行说明，包括已知问题、bug 修复、新增功能和 Dcr。
author: JonDouglas
ms.author: jodou
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: b6874cbf0404f18ab7007bec1e0f66089c790d08
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/26/2021
ms.locfileid: "98776985"
---
# <a name="nuget-20-release-notes"></a>NuGet 2.0 发行说明

[NuGet 1.8 发行说明](../release-notes/nuget-1.8.md)  | [NuGet 2.1 发行说明](../release-notes/nuget-2.1.md)

NuGet 2.0 于2012年6月19日发布。

## <a name="known-installation-issue"></a>已知安装问题
如果你运行的是 VS 2010 SP1，但如果你安装了较旧的版本，你可能会遇到安装错误。

解决方法是仅卸载 NuGet，然后从 VS 扩展库安装它。  <https://support.microsoft.com/kb/2581019>有关详细信息，请参阅，或[直接访问 VS 修补程序](http://bit.ly/vsixcertfix)。

注意：如果 Visual Studio 不允许卸载扩展 (禁用了 "卸载" 按钮) ，则可能需要使用 "以管理员身份运行" 重启 Visual Studio。

## <a name="package-restore-consent-is-now-active"></a>包还原许可现在处于活动状态

如本 [文章在包还原许可](http://blog.nuget.org/20120518/package-restore-and-consent.html)中所述，NuGet 2.0 现在要求授予许可以使包还原联机并下载包。 请确保已通过 "程序包管理器配置" 对话框或 EnableNuGetPackageRestore 环境变量提供同意。

## <a name="group-dependencies-by-target-frameworks"></a>按目标框架对依赖项进行分组

从版本2.0 开始，根据目标项目的框架配置文件，包依赖项可能会有所不同。 这是使用已更新的架构来完成的 `.nuspec` 。 `<dependencies>`元素现在可以包含一组 `<group>` 元素。 每个组都包含零个或多个 `<dependency>` 元素和一个 `targetFramework` 属性。 如果目标框架与目标项目框架配置文件兼容，则组中的所有依赖项都将一起安装。 例如：

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

请注意，一个组可以包含 **零个** 依赖项。 在上述示例中，如果将包安装到面向 Silverlight 3.0 或更高版本的项目中，则不会安装任何依赖项。 如果将包安装到面向 .NET 4.0 或更高版本的项目中，将安装两个依赖项（jQuery 和 WebActivator）。  如果将包安装到以这两个框架的早期版本为目标的项目或任何其他框架，将安装 RouteMagic 1.1.0。 组之间没有继承。 如果项目的目标框架与组的 `targetFramework` 属性匹配，则只会安装该组中的依赖关系。

包可以使用以下两种格式中的一种来指定包依赖项：元素或组的简单列表的旧格式 `<dependency>` 。 如果 `<group>` 使用格式，则包不能安装在版本早于2.0 的 NuGet 中。

请注意，不允许混合使用这两种格式。 例如，下面的代码段 **无效** 并将被 NuGet 拒绝。

```xml
<dependencies>
    <dependency id="jQuery" />
    <dependency id="WebActivator" />

    <group>
        <dependency id="RouteMagic" version="1.1.0" />
    </group>
</dependencies>
```

## <a name="grouping-content-files-and-powershell-scripts-by-target-framework"></a>按目标框架对内容文件和 PowerShell 脚本进行分组

除程序集引用外，还可以按目标框架对内容文件和 PowerShell 脚本进行分组。 现在，在用于指定目标框架的文件夹中找到的相同文件夹结构 `lib` 现在可以按与和文件夹相同的方式应用 `content` `tools` 。 例如：

```
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
```

**注意**：由于 `init.ps1` 是在解决方案级别执行的，并且不依赖于任何单个项目，因此必须将其直接放置在 `tools` 文件夹下。 如果放置在框架特定的文件夹中，则将被忽略。

此外，NuGet 2.0 中的一项新功能是框架文件夹可以是 *空* 的，在这种情况下，NuGet 不会添加程序集引用、添加内容文件或针对特定的框架版本运行 PowerShell 脚本。 在上面的示例中，该文件夹 `content\net40` 为空。

## <a name="improved-tab-completion-performance"></a>改善了选项卡完成性能
NuGet 包管理器控制台中的选项卡完成功能已更新，以显著提高性能。 按下 tab 键时，延迟时间会大大减少，直到出现建议下拉列表。

## <a name="bug-fixes"></a>Bug 修复
NuGet 2.0 包含多个 bug 修复，重点介绍包还原同意和性能。
有关 NuGet 2.0 中已修复的工作项的完整列表，请查看 [此版本的 NuGet 问题跟踪程序](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Closed&type=All&priority=All&release=NuGet%202.0&assignedTo=All&component=All&sortField=Votes&sortDirection=Descending&page=0)。
