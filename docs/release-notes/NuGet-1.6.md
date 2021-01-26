---
title: NuGet 1.6 发行说明
description: NuGet 1.6 的发行说明，包括已知问题、bug 修复、新增功能和 Dcr。
author: JonDouglas
ms.author: jodou
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 08b1cb3736e645d6efcc33f920f521c9c0fc7507
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/26/2021
ms.locfileid: "98777015"
---
 # <a name="nuget-16-release-notes"></a>NuGet 1.6 发行说明

[NuGet 1.5 发行说明](../release-notes/nuget-1.5.md)  | [NuGet 1.7 发行说明](../release-notes/nuget-1.7.md)

NuGet 1.6 于2011年12月13日发布。

## <a name="known-installation-issue"></a>已知安装问题
如果你运行的是 VS 2010 SP1，但如果你安装了较旧的版本，你可能会遇到安装错误。

解决方法是仅卸载 NuGet，然后从 VS 扩展库安装它。  有关更多信息，请参见<https://support.microsoft.com/kb/2581019>。

注意：如果 Visual Studio 不允许卸载扩展 (禁用了 "卸载" 按钮) ，则可能需要使用 "以管理员身份运行" 重启 Visual Studio。

## <a name="features"></a>功能

### <a name="support-for-semantic-versioning-and-prerelease-packages"></a>支持语义版本控制和预发行包
NuGet 1.6 引入 (SemVer) 的语义版本控制支持。 有关如何使用 SemVer 的更多详细信息，请参阅 [版本控制文档](../create-packages/prerelease-packages.md)。

### <a name="using-nuget-without-checking-in-packages-package-restore"></a>使用 NuGet 但不签入包 (包还原) 
NuGet 1.6 现在提供对工作流的第一类支持，其中 NuGet 包未添加到源代码管理中，但在生成时将在缺少时还原。 有关更多详细信息，请阅读 [使用 NuGet 但不将包提交到源代码管理](../consume-packages/packages-and-source-control.md) 主题。

### <a name="item-templates-that-install-nuget-packages"></a>安装 NuGet 包的项模板
基于支持预安装 NuGet 包的工作以支持 Visual Studio 项目模板，NuGet 1.6 还添加了对 Visual Studio 项模板的支持。 项模板可以具有在调用模板时安装的关联 NuGet 包。

有关如何更改项目/项模板以安装 NuGet 包的详细信息，请阅读 [Visual Studio 模板中的包](../visual-studio-extensibility/visual-studio-templates.md) 主题。

### <a name="support-for-disabling-package-sources"></a>支持禁用包源
当配置了多个包源时，NuGet 将在包及其依赖项的安装过程中为包查找每个源。 出于某种原因关闭的包源可能严重降低了 NuGet 速度。

在 NuGet 1.6 之前，你可以删除包源，但当你想要将其重新添加时，必须记住的详细信息。

NuGet 1.6 允许不选中包源来禁用它，但要进行保留。

![禁用包](./media/package-source-with-disabled-source.png)

## <a name="bug-fixes"></a>Bug 修复
NuGet 1.6 总共修复了106个工作项。 其中的95归类为 bug，其中10个是功能。

有关 NuGet 1.6 中已修复的工作项的完整列表，请查看 [此版本的 NuGet 问题跟踪程序](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Closed&type=All&priority=All&release=NuGet%201.6&assignedTo=All&component=All&sortField=Votes&sortDirection=Descending&page=0)。
