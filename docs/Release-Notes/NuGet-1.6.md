---
title: "NuGet 1.6 发行说明 |Microsoft 文档"
author: karann-msft
ms.author: karann-msft
manager: ghogen
ms.date: 11/11/2016
ms.topic: article
ms.prod: nuget
ms.technology: 
description: "包括已知的问题、 bug 修复、 增加的功能，以及 DCRs NuGet 1.6 的发行说明。"
keywords: "NuGet 1.6 发行说明，bug 修复的已知问题，添加了一些功能，DCRs"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 114b03cede24dee520ace1d8aa920a648ad16af1
ms.sourcegitcommit: 4651b16a3a08f6711669fc4577f5d63b600f8f58
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/02/2018
---
 # <a name="nuget-16-release-notes"></a>NuGet 1.6 发行说明

[NuGet 1.5 发行说明](../release-notes/nuget-1.5.md) | [NuGet 1.7 发行说明](../release-notes/nuget-1.7.md)

NuGet 1.6 已于 2011 年 12 月 13 日发布。

## <a name="known-installation-issue"></a>已知的安装问题
如果你运行的 VS 2010 SP1，你可能尝试升级 NuGet，如果安装了较旧版本时遇到安装错误。

解决方法是只需卸载 NuGet，然后从 VS 扩展库安装它。  有关详细信息，请参阅 [http://support.microsoft.com/kb/2581019](http://support.microsoft.com/kb/2581019)。

注意： 如果 Visual Studio 不会使您可以卸载的扩展 （卸载按钮为禁用），然后你可能需要重新启动 Visual Studio 中使用"以管理员身份运行"。

## <a name="features"></a>功能

### <a name="support-for-semantic-versioning-and-prerelease-packages"></a>支持语义版本控制和预发行程序包
NuGet 1.6 引入了对语义版本控制 (SemVer) 支持。 关于如何使用 SemVer 的详细信息，请参阅[版本控制文档](../create-packages/prerelease-packages.md)。

### <a name="using-nuget-without-checking-in-packages-package-restore"></a>使用 NuGet，而无需签入包 （包还原）
NuGet 1.6 现在具有工作流中的 NuGet 包不会添加到源代码管理，但改为会还原在生成时如果缺少第一类支持。 有关详细信息，请阅读[不提交到源代码管理包的情况下使用 NuGet](../consume-packages/packages-and-source-control.md)主题。

### <a name="item-templates-that-install-nuget-packages"></a>安装 NuGet 包的项模板
生成的工作以支持 Visual Studio 项目模板的预安装的 NuGet 程序包，NuGet 1.6 还将添加对 Visual Studio 项模板的支持。 项模板可以具有关联中的模板调用时安装的 NuGet 包。

有关如何更改要安装 NuGet 包的项目服务/项目模板的详细信息，请参阅[Visual Studio 模板中的包](../visual-studio-extensibility/visual-studio-templates.md)主题。

### <a name="support-for-disabling-package-sources"></a>禁用包源的支持
当配置多个包源时，NuGet 将查找每个包的包及其依赖项的安装过程。 已关闭的某种原因会严重降低 NuGet 包源。

在 NuGet 1.6 之前无法删除包源，但然后必须要记住的详细信息时，你想要将其添加回。

NuGet 1.6 允许取消选中的程序包源中禁用它，但保留它。

![禁用包](./media/package-source-with-disabled-source.png)

## <a name="bug-fixes"></a>Bug 修复
NuGet 1.6 具有总共 106 工作固定的项。 95 的那些已被归类为 bug 和 10 的那些功能。

有关工作的完整列表项固定在 NuGet 1.6，请查看[对于此版本的 NuGet 问题跟踪程序](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Closed&type=All&priority=All&release=NuGet%201.6&assignedTo=All&component=All&sortField=Votes&sortDirection=Descending&page=0)。
