---
title: NuGet 2.7.2 发行说明
description: NuGet 2.7.2 的发行说明，包括已知问题、bug 修复、新增功能和 Dcr。
author: JonDouglas
ms.author: jodou
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 7643bf930bca39684eb626fe737001bc3e3ea769
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/26/2021
ms.locfileid: "98776787"
---
# <a name="nuget-272-release-notes"></a>NuGet 2.7.2 发行说明

[NuGet 2.7.1 发行说明](../release-notes/nuget-2.7.1.md)  | [NuGet 2.8 发行说明](../release-notes/nuget-2.8.md)

NuGet 2.7.2 于2013年11月11日发布。

## <a name="noteworthy-bug-fixes-and-features"></a>值得注意的 Bug 修复和功能

### <a name="license-text"></a>许可文本
在很长一段时间内，Microsoft 在 Visual Studio 中为 Web 应用程序项目的默认模板包含了多个常用开源库的 NuGet 包。 jQuery 可能是此类型库的最常见的示例。 由于与产品一起传送的组件相关联的支持协议，包的脚本文件包含不同的许可文本，而不是公共 nuget.org 库上同一个包中的脚本文件。 这种文本差异可能会导致包更新因不同的许可证文本块而无法继续进行，导致脚本文件 (的内容哈希值，因此在项目) 中被视为已修改。

为了缓解此问题，NuGet 2.7.2 允许脚本作者将许可证文本块包含在一个特别标记的部分中，如下所示。

```
/************** NUGET: BEGIN LICENSE TEXT **************
    * The following code is licensed under the MIT license
    * Additional license information below is informational
    * only.
    ************** NUGET: END LICENSE TEXT ***************/
```

当更新包含包含此块的内容文件的包时，NuGet 不会将块的内容与 NuGet 库中的版本进行比较，因此，可以删除并更新内容文件，就像它与原始副本匹配一样。

此块由文本 "NUGET： BEGIN LICENSE TEXT" 和 "NUGET： END LICENSE TEXT" 标识，出现在开始和结束行的任何位置。  不存在其他格式设置要求，因此，无论使用何种语言，都可以在任何类型的文本文件中使用此功能。

### <a name="add-binding-redirects-for-non-framework-assemblies"></a>添加非框架程序集的绑定重定向
对于作为 .NET Framework 一部分的程序集，NuGet 将在更新包时跳过将绑定重定向添加到应用程序的配置文件中。 此修补程序解决了 NuGet 2.7 中的回归，因为没有为某些程序集添加绑定重定向，即使不将这些程序集视为 .NET Framework 的一部分。 NuGet 2.7.2 将还原以前的 NuGet 2.5 和2.6 行为，并添加绑定重定向。

### <a name="installing-portable-libraries-with-xamarin-tools-installed"></a>安装安装了 Xamarin 工具的可移植库
当 Xamarin 的开发工具安装在计算机上时，它们将修改支持的框架配置数据以指定现有目标框架组合和 Xamarin 框架之间的兼容性。 利用版本2.7.2，NuGet 现在可以识别这些隐式兼容性规则，并因此使面向 Xamarin 平台的开发人员可以轻松地安装与 Xamarin 兼容但未在包元数据本身中显式标记为这样的可移植库。

### <a name="machine-wide-configuration-settings-honored"></a>计算机范围的配置设置生效
使用分层 Nuget.Config 文件时，对于最接近于解决方案根的 Nuget.Config 文件，repositoryPath 键将不起作用。 在 Visual Studio 2013 中，NuGet 将在% ProgramData% \NuGet\Config\VisualStudio\12.0\Microsoft.VisualStudio.config 上安装一个自定义 Nuget.Config 文件，以便添加 "Microsoft 和 .NET" 包源。 因此，在解决方案中使用自定义 repositoryPath 的解决方法是删除计算机级别 Nuget.Config-这也意味着删除 "Microsoft 和 .NET" 包源。 在使用分层 Nuget.Config 文件时，NuGet 2.7.2 现在遵循 repositoryPath 的优先规则。

## <a name="all-changes"></a>所有更改
有关 NuGet 2.7.2 中修复的工作项的完整列表，请查看 [此版本的 NuGet 问题跟踪程序](https://nuget.codeplex.com/workitem/list/advanced?keyword=&status=All&type=All&priority=All&release=NuGet%202.7.2&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0&reasonClosed=Fixed)。
