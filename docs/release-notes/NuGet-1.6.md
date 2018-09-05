---
title: NuGet 1.6 版说明
description: 发行说明适用于 NuGet 1.6 包括已知的问题、 bug 修复、 新增的功能和 Dcr。
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 351303ca3ae27a37c19e59d84dfc9b4629fe0ca5
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/04/2018
ms.locfileid: "43549007"
---
 # <a name="nuget-16-release-notes"></a>NuGet 1.6 版说明

[NuGet 1.5 发行说明](../release-notes/nuget-1.5.md) | [NuGet 1.7 发行说明](../release-notes/nuget-1.7.md)

NuGet 1.6 已于 2011 年 12 月 13 日发布。

## <a name="known-installation-issue"></a>已知的安装问题
如果运行 VS 2010 SP1，你可能会遇到安装错误，尝试升级 NuGet，如果您有安装了旧版本时。

解决方法是简单地卸载 NuGet，然后从 VS 扩展库安装它。  有关详细信息，请参阅 [http://support.microsoft.com/kb/2581019](http://support.microsoft.com/kb/2581019)。

注意： 如果 Visual Studio 不会使您可以卸载的扩展 （卸载按钮被禁用），然后您可能需要重启 Visual Studio 中使用"以管理员身份运行"。

## <a name="features"></a>功能

### <a name="support-for-semantic-versioning-and-prerelease-packages"></a>对语义化版本控制和预发行包的支持
NuGet 1.6 引入了对语义化版本控制 (SemVer) 支持。 有关如何使用 SemVer 的详细信息，请阅读[版本控制文档](../create-packages/prerelease-packages.md)。

### <a name="using-nuget-without-checking-in-packages-package-restore"></a>不检查包 （包还原） 中使用 NuGet
NuGet 1.6 现在具有对工作流中的 NuGet 包不会添加到源代码管理，但改为会还原在生成时如果缺少第一类支持。 有关更多详细信息，请阅读[而包提交到源代码管理不使用 NuGet](../consume-packages/packages-and-source-control.md)主题。

### <a name="item-templates-that-install-nuget-packages"></a>安装 NuGet 包的项模板
基础上运行以支持 Visual Studio 项目模板的预安装的 NuGet 包，NuGet 1.6 还将添加对 Visual Studio 项模板的支持。 项模板可以具有关联的调用中的模板时安装的 NuGet 包。

有关如何更改要安装 NuGet 包的项目/项模板的更多详细信息，请阅读[Visual Studio 模板中的包](../visual-studio-extensibility/visual-studio-templates.md)主题。

### <a name="support-for-disabling-package-sources"></a>禁用包源的支持
当配置多个包源时，NuGet 将期间安装的包及其依赖项，查找每个包中。 已关闭的一些原因会严重降低 NuGet 包源。

在 NuGet 1.6 之前, 无法删除包的来源，但然后，必须记住的详细信息时，你想要将其添加回。

NuGet 1.6，取消选中要禁用它，但将其保留的包源。

![禁用包](./media/package-source-with-disabled-source.png)

## <a name="bug-fixes"></a>Bug 修复
NuGet 1.6 必须总共 106 个工作项已修复。 其中的 95 被分类为 bug 并且 10 的那些功能。

有关工作的完整列表项中已修复 NuGet 1.6，请查看[对于此版本的 NuGet 问题跟踪程序](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Closed&type=All&priority=All&release=NuGet%201.6&assignedTo=All&component=All&sortField=Votes&sortDirection=Descending&page=0)。
