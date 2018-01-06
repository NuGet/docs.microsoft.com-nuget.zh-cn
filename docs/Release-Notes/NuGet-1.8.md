---
title: "NuGet 1.8 发行说明 |Microsoft 文档"
author: karann-msft
ms.author: karann-msft
manager: ghogen
ms.date: 11/11/2016
ms.topic: article
ms.prod: nuget
ms.technology: 
ms.assetid: e694ee1a-fe4c-4397-8d0a-7336be4dfebe
description: "包括已知的问题、 bug 修复、 增加的功能，以及 DCRs NuGet 1.8 的发行说明。"
keywords: "NuGet 1.8 发行说明，bug 修复的已知问题，添加了一些功能，DCRs"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 350f0d9590c1e0ef1a843fd783203b158059efa7
ms.sourcegitcommit: a40c1c1cc05a46410f317a72f695ad1d80f39fa2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/05/2018
---
# <a name="nuget-18-release-notes"></a>NuGet 1.8 发行说明

[NuGet 1.7 发行说明](../release-notes/nuget-1.7.md) | [NuGet 2.0 发行说明](../release-notes/nuget-2.0.md)

NuGet 1.8 已于 2012 年 5 月 23 日发布。

## <a name="known-installation-issue"></a>已知的安装问题
如果你运行的 VS 2010 SP1，你可能尝试升级 NuGet，如果安装了较旧版本时遇到安装错误。

解决方法是只需卸载 NuGet，然后从 VS 扩展库安装它。  请参阅[http://support.microsoft.com/kb/2581019](http://support.microsoft.com/kb/2581019)有关详细信息，或[转到 VS 修补程序直接](http://bit.ly/vsixcertfix)。

注意： 如果 Visual Studio 不会使您可以卸载的扩展 （卸载按钮为禁用），然后你可能需要重新启动 Visual Studio 中使用"以管理员身份运行"。

## <a name="nuget-18-incompatible-with-windows-xp-hotfix-published"></a>NuGet 1.8 兼容 Windows XP 中，发布的修补程序

很快发布 NuGet 1.8 后，我们已了解 1.8 中的加密更改在 Windows XP 上中断用户。

由于我们已发布的修补程序来解决该问题。  通过更新通过 Visual Studio 扩展库的 NuGet，您将收到此修补程序。

## <a name="features"></a>功能

### <a name="satellite-packages-for-localized-resources"></a>本地化资源的附属包
NuGet 1.8 现在支持创建单独的包的本地化资源，类似于.NET framework 的附属程序集功能的能力。  为通过添加少量的约定的任何其他 NuGet 包相同的方式创建一个附属包：

* 附属包 ID 和文件名称应包含匹配的标准之一后缀[区域性使用的.NET Framework 字符串](http://msdn.microsoft.com/goglobal/bb896001.aspx)。
* 在其`.nuspec`文件，附属包应定义一个语言元素，具有相同 ID 中使用的区域性字符串
* 附属包应定义中的依赖项其`.nuspec`到其核心包中，只需具有相同 ID 的语言后缀减包文件。  要成功安装的存储库中可用的核心程序包要求。

若要安装包使用本地化的资源，开发人员显式选择的本地化的程序包从存储库。 目前，NuGet 库未提供任何类型的附属包的特殊处理。

![与本地化包的包管理器对话框](./media/dlg-w-loc-packs.png)

由于附属包会列出对其核心包的依赖性，附属和核心包都已拉入 NuGet 包文件夹，并且安装。

![具有本地化包的包文件夹](./media/fldr-loc-packs.png)

此外，时安装附属包，NuGet 还可识别的区域性字符串命名约定，然后将本地化的资源程序集复制到核心包内正确的子文件夹，以便它可以由.NET Framework 中选取。

![核心包文件夹与复制的资源文件夹](./media/fldr-copied-loc.png)

一个现有的 bug，需要注意的附属包是 NuGet 不会复制到的本地化的资源`bin`适用于网站项目的文件夹。  将在下一个版本的 NuGet 中修复此问题。

有关演示如何创建和使用附属包的完整示例，请参阅[https://github.com/NuGet/SatellitePackageSample](https://github.com/NuGet/SatellitePackageSample)。

### <a name="package-restore-consent"></a>包还原同意
在 NuGet 1.8，我们放置支持包还原，以保护用户个人信息的一个重要约束奠定基础。 此约束要求开发人员生成项目和使用程序包还原显式同意程序包还原的解决方案的联机从配置的包源中下载的程序包。

有两种方法提供此许可。 第一个可在包管理器配置对话框如下所示。  此方法主要用于开发人员计算机。

![包管理器配置对话框](./media/pr-consent-configdlg.png)

第二种方法是将环境变量"EnableNuGetPackageRestore"设置为"true"的值。  此方法适用于无人参与的计算机，如 CI 或生成服务器。

现在，如上面所述，我们仅具有在 NuGet 1.8 中排列此功能的基础工作。  实际上，这意味着，虽然我们已添加所有启用的功能的逻辑，但是它当前不强制执行在此版本中。 它将被启用，但是，在下一个版本的 NuGet，因此我们想要让你知道它越早越好，以便你可以相应地配置你的环境，并因此不会影响我们启动时强制实施同意约束。

有关更多详细信息，请参阅[团队博客文章](http://blog.nuget.org/20120518/package-restore-and-consent.html)有关此功能。

### <a name="nugetexe-performance-improvements"></a>nuget.exe 性能改进
通过修改将下载并在并行中安装包的安装命令，NuGet 1.8 会极大地提高性能 nuget.exe – 并且，通过扩展包还原。  高级别测试显示 6 包安装到项目的性能可以减少大约 35%NuGet 1.8 中。  增加到 25 的包数目显示大约 60%的性能有所提高。

## <a name="bug-fixes"></a>Bug 修复
NuGet 1.8 包括相当多的 bug 修复，主要侧重于的包管理器控制台和包恢复工作流，尤其当它与包还原同意和 Windows 8 Express 集成。
有关工作的完整列表项固定在 NuGet 1.8，请查看[对于此版本的 NuGet 问题跟踪程序](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Closed&type=All&priority=All&release=NuGet%201.8&assignedTo=All&component=All&sortField=Votes&sortDirection=Descending&page=0)。
