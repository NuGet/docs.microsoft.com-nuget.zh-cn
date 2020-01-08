---
title: NuGet 1.8 发行说明
description: NuGet 1.8 的发行说明，包括已知问题、bug 修复、新增功能和 Dcr。
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 973a2d010cb75eeeb383be94baf2fb17a999dd7c
ms.sourcegitcommit: 26a8eae00af2d4be581171e7a73009f94534c336
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/25/2019
ms.locfileid: "75383456"
---
# <a name="nuget-18-release-notes"></a>NuGet 1.8 发行说明

[Nuget 1.7 发行说明](../release-notes/nuget-1.7.md) | [Nuget 2.0 发行说明](../release-notes/nuget-2.0.md)

NuGet 1.8 于年5月 23 2012 日发布。

## <a name="known-installation-issue"></a>已知安装问题
如果你运行的是 VS 2010 SP1，但如果你安装了较旧的版本，你可能会遇到安装错误。

解决方法是仅卸载 NuGet，然后从 VS 扩展库安装它。  有关详细信息，请参阅 <https://support.microsoft.com/kb/2581019>，或[直接跳到 VS 修补程序](http://bit.ly/vsixcertfix)。

注意：如果 Visual Studio 不允许你卸载扩展（"卸载" 按钮已禁用），则可能需要使用 "以管理员身份运行" 重启 Visual Studio。

## <a name="nuget-18-incompatible-with-windows-xp-hotfix-published"></a>NuGet 1.8 与 Windows XP 兼容，已发布修补程序

在 NuGet 1.8 发布之后不久，我们已了解到1.8 中的密码更改在 Windows XP 上中断了用户。

我们已经发布了解决此问题的修补程序。  通过在 Visual Studio 扩展库中更新 NuGet，你会收到此修补程序。

## <a name="features"></a>特征

### <a name="satellite-packages-for-localized-resources"></a>本地化资源的附属包
NuGet 1.8 现在支持为本地化资源创建单独包的功能，类似于 .NET Framework 的附属程序集功能。  附属包的创建方式与任何其他 NuGet 包相同，只是添加了一些约定：

* 附属包 ID 和文件名应包含与[.NET Framework 使用的标准区域性字符串](https://docs.microsoft.com/openspecs/windows_protocols/ms-lcid/a9eac961-e77d-41a6-90a5-ce1a8b0cdb9c)之一匹配的后缀。
* 在其 `.nuspec` 文件中，附属包应定义一个语言元素，该元素具有在 ID 中使用的相同区域性字符串
* 附属包应将其 `.nuspec` 文件中的依赖项定义为其核心包，这只是 ID 与语言后缀相同的包。  核心包需要在存储库中可用，才能成功安装。

若要安装包含本地化资源的包，开发人员需要从存储库中显式选择本地化包。 目前，NuGet 库不会向附属包提供任何类型的特殊处理。

![带有本地化包的包管理器对话框](./media/dlg-w-loc-packs.png)

由于附属包列出了其核心包的依赖项，因此附属包和核心包都将提取到 NuGet 包文件夹中并安装。

![带有本地化包的包文件夹](./media/fldr-loc-packs.png)

此外，在安装附属包时，NuGet 还识别区域性字符串命名约定，然后将本地化的资源程序集复制到核心包内的正确子文件夹中，以便 .NET Framework 可以对其进行选取。

![包含已复制资源文件夹的核心包文件夹](./media/fldr-copied-loc.png)

附属包需要注意的一个现有 bug 是 NuGet 不会将本地化的资源复制到网站项目的 `bin` 文件夹中。  此问题将在 NuGet 的下一版本中得到解决。

有关演示如何创建和使用附属包的完整示例，请参阅[https://github.com/NuGet/SatellitePackageSample](https://github.com/NuGet/SatellitePackageSample)。

### <a name="package-restore-consent"></a>包还原许可
在 NuGet 1.8 中，我们为支持包还原中的重要约束设定了基础，以保护用户隐私。 此约束要求开发人员生成项目和解决方案，这些项目和解决方案使用包还原来显式同意包还原的联机状态，以便从配置的包源下载包。

有两种方法可提供此许可。 第一个可以在 "包管理器配置" 对话框中找到，如下所示。  此方法主要用于开发人员计算机。

![程序包管理器配置对话框](./media/pr-consent-configdlg.png)

第二种方法是将环境变量 "EnableNuGetPackageRestore" 设置为值 "true"。  此方法适用于无人参与的计算机，例如 CI 或生成服务器。

现在，如上所述，我们只在 NuGet 1.8 中为此功能奠定了基础。  实际上，这意味着虽然我们添加了所有逻辑来启用此功能，但当前未在此版本中强制执行此功能。 但在 NuGet 的下一版本中会启用此功能，因此，我们希望你尽快了解该功能，以便你可以适当地配置环境，从而在我们开始强制许可约束时不会受到影响。

有关更多详细信息，请参阅[团队博客文章](http://blog.nuget.org/20120518/package-restore-and-consent.html)此功能。

### <a name="nugetexe-performance-improvements"></a>nuget.exe 性能改进
通过修改安装命令以并行下载和安装包，NuGet 1.8 使 nuget.exe 的性能得到显著改善，并通过扩展包还原提高了性能。  高级别测试表明，将6个包安装到项目中的性能将在 NuGet 1.8 中提高大约35%。  将包数增加到25会显示大约60% 的性能提升。

## <a name="bug-fixes"></a>Bug 修复
NuGet 1.8 包含非常多的 bug 修复，其中重点介绍了包管理器控制台和包还原工作流，尤其是在它与包还原许可和 Windows 8 Express 集成相关时。
有关 NuGet 1.8 中已修复的工作项的完整列表，请查看[此版本的 NuGet 问题跟踪程序](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Closed&type=All&priority=All&release=NuGet%201.8&assignedTo=All&component=All&sortField=Votes&sortDirection=Descending&page=0)。
