---
title: NuGet 1.8 发行说明
description: 包括已知的问题、 bug 修复、 新增的功能和 Dcr NuGet 1.8 的发行说明。
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: ff6d12606b1bed479e63eebccd978ff9cd4a7faf
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/04/2018
ms.locfileid: "43546616"
---
# <a name="nuget-18-release-notes"></a>NuGet 1.8 发行说明

[NuGet 1.7 发行说明](../release-notes/nuget-1.7.md) | [NuGet 2.0 发行说明](../release-notes/nuget-2.0.md)

NuGet 1.8 已于 2012 年 5 月 23 日发布。

## <a name="known-installation-issue"></a>已知的安装问题
如果运行 VS 2010 SP1，你可能会遇到安装错误，尝试升级 NuGet，如果您有安装了旧版本时。

解决方法是简单地卸载 NuGet，然后从 VS 扩展库安装它。  请参阅[ http://support.microsoft.com/kb/2581019 ](http://support.microsoft.com/kb/2581019)有关详细信息，或[直接转到 VS 修补程序](http://bit.ly/vsixcertfix)。

注意： 如果 Visual Studio 不会使您可以卸载的扩展 （卸载按钮被禁用），然后您可能需要重启 Visual Studio 中使用"以管理员身份运行"。

## <a name="nuget-18-incompatible-with-windows-xp-hotfix-published"></a>NuGet 1.8 兼容 Windows XP 发布的修补程序

NuGet 1.8 发布不久后，我们了解到 1.8 中的加密更改中断用户在 Windows XP 上。

由于我们已发布，解决了此问题的修补程序。  通过更新 NuGet 通过 Visual Studio 扩展库，你收到此修补程序。

## <a name="features"></a>功能

### <a name="satellite-packages-for-localized-resources"></a>对本地化资源的附属包
NuGet 1.8 现在支持创建不同的软件包类似于.NET Framework 的附属程序集功能的本地化资源的能力。  附属包创建方式与任何其他 NuGet 包添加了几个约定相同：

* 附属包 ID 和文件名称应包含匹配的一个标准的后缀[区域性使用的.NET Framework 字符串](http://msdn.microsoft.com/goglobal/bb896001.aspx)。
* 在其`.nuspec`文件，附属包应定义一个语言元素，具有同一 ID 中使用的区域性字符串
* 附属包应定义中的依赖项及其`.nuspec`到其核心包，即只需具有相同 ID 去掉语言后缀的包文件。  要成功安装的存储库中可用的核心包要求。

若要使用的本地化资源安装包，开发人员会将本地化的包显式选择从存储库。 目前，NuGet 库不提供任何类型的特殊处理方式为附属包。

![包管理器对话框使用本地化包](./media/dlg-w-loc-packs.png)

因为附属包列出了其核心包的依赖项，是拉取到 NuGet 包文件夹和安装附属和 core 包。

![与本地化包的包文件夹](./media/fldr-loc-packs.png)

此外，同时安装附属包，NuGet 还可以识别区域性的字符串命名约定，然后将本地化的资源程序集复制到核心包中的正确子文件夹，以便它可以由.NET Framework 中选取。

![复制的资源文件夹与核心包文件夹](./media/fldr-copied-loc.png)

一个需要注意的附属包的现有 bug 是 NuGet 不会复制到的本地化的资源`bin`网站项目的文件夹。  将 NuGet 的下一个版本中修复此问题。

有关演示如何创建和使用附属包的完整示例，请参阅[ https://github.com/NuGet/SatellitePackageSample ](https://github.com/NuGet/SatellitePackageSample)。

### <a name="package-restore-consent"></a>包还原同意
在 NuGet 1.8 我们形式放置支持包还原，以保护用户隐私的一个重要约束打下基础。 此约束要求构建项目和使用包还原显式同意包还原的解决方案的开发人员现在可以联机从配置的包源下载包。

有两种方法来提供此许可。 第一个可在包管理器配置对话框，如下所示。  此方法主要针对开发人员计算机。

![包管理器配置对话框](./media/pr-consent-configdlg.png)

第二种方法是将环境变量"EnableNuGetPackageRestore"设置为值"true"。  此方法适用于无人参与的计算机，如 CI 或生成服务器。

现在，如上面所述，我们仅奠定了基础，此功能在 NuGet 1.8 中。  实际上，这意味着，尽管我们已添加的所有逻辑以启用该功能，它当前未强制执行在此版本中。 它将被启用，但是，在下一个版本的 NuGet，因此我们想要让你知道它越早越好，以便可以适当地配置您的环境并因此不会受到影响我们启动时强制执行许可约束。

有关更多详细信息，请参阅[团队博客文章](http://blog.nuget.org/20120518/package-restore-and-consent.html)有关此功能。

### <a name="nugetexe-performance-improvements"></a>nuget.exe 性能改进
通过修改安装命令下载和并行安装包，NuGet 1.8 做出了巨大的性能改进 nuget.exe – 且可由扩展包还原。  高级别测试显示 6 包安装到项目的性能提高的 35%NuGet 1.8 中。  增加到 25 的包的数量显示大约 60%的性能提升。

## <a name="bug-fixes"></a>Bug 修复
NuGet 1.8 包括的包管理器控制台和包还原工作流，这是很多 bug 修复，特别是因为它与包还原同意和集成的 Windows 8 Express。
有关工作的完整列表项中已修复 NuGet 1.8，请查看[对于此版本的 NuGet 问题跟踪程序](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Closed&type=All&priority=All&release=NuGet%201.8&assignedTo=All&component=All&sortField=Votes&sortDirection=Descending&page=0)。
