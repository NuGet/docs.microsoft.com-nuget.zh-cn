---
title: NuGet 2.7.2 发行说明
description: NuGet 2.7.2，它包括的发行说明的已知问题、 bug 修复、 新增的功能和 Dcr。
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 3e63944a05f66d5dadf17c5d4b91d3bc4478bb33
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/04/2018
ms.locfileid: "43550065"
---
# <a name="nuget-272-release-notes"></a>NuGet 2.7.2 发行说明

[NuGet 2.7.1 发行说明](../release-notes/nuget-2.7.1.md) | [NuGet 2.8 发行说明](../release-notes/nuget-2.8.md)

NuGet 2.7.2，它已于 2013 年 11 月 11 日发布。

## <a name="noteworthy-bug-fixes-and-features"></a>值得注意的 Bug 修复和功能

### <a name="license-text"></a>许可证文本
一段时间，Microsoft 已包含在 Visual Studio 为 Web 应用程序项目的默认模板的一部分的几个常用的开源库的 NuGet 包。 jQuery 可能是库的这种类型的最常见示例。 由于与产品一起提供的组件关联的支持协议，包的脚本文件包含不同的许可证文本中比在同一个包中找到公共 nuget.org 库上的脚本文件。 这种文本的差异可以防止由于导致要具有不同的内容哈希值的脚本文件的其他许可证文本块继续包更新 （并因此被视为在项目中修改）。

若要缓解此问题，NuGet 2.7.2，它允许脚本作者以包括如下所示的特殊标记部分中的许可证文本块。

    /************** NUGET: BEGIN LICENSE TEXT **************
     * The following code is licensed under the MIT license
     * Additional license information below is informational
     * only.
     ************** NUGET: END LICENSE TEXT ***************/

当更新包的内容文件，其中包含此块中，NuGet 不会不块的内容，应考虑使用 NuGet 库上的版本比较和可以因此删除和更新内容文件，就好像它匹配的原始副本。

由文本"NUGET:: BEGIN 许可证 TEXT"和"NUGET:: 结束许可证 TEXT"发生任意位置上开始和结束行标识此块。  没有其他格式设置要求存在，可让在任何类型的文本与语言无关的文件中使用此功能。

### <a name="add-binding-redirects-for-non-framework-assemblies"></a>添加绑定重定向为非 Framework 程序集
对于属于.NET Framework 的程序集，NuGet 将跳过添加绑定重定向到应用程序的配置文件更新包时。 此修补程序地址，由此绑定重定向不添加对于某些程序集，即使这些程序集不是 NuGet 2.7 中的回归视为.NET Framework 的一部分。 NuGet 2.7.2，它将还原以前的 NuGet 2.5 和 2.6 行为，并将添加绑定重定向。

### <a name="installing-portable-libraries-with-xamarin-tools-installed"></a>使用安装了 Xamarin 工具安装可移植库
当在计算机上安装 Xamarin 的开发工具时，它们修改要指定现有的目标框架组合和 Xamarin 框架之间的兼容性的支持的框架配置数据。 2.7.2，它在版本，NuGet 会了解这样的隐式的兼容性规则，并因此可以轻松面向 Xamarin 平台的开发人员能够在包中这种情况下安装 Xamarin 兼容，但未显式标记的可移植库元数据本身。

### <a name="machine-wide-configuration-settings-honored"></a>接受的计算机范围的配置设置
使用分层 Nuget.Config 文件时，repositoryPath 密钥不被接受 Nuget.Config 文件接近解决方案根目录。 在 Visual Studio 2013 中，NuGet 安装自定义在 %ProgramData%\NuGet\Config\VisualStudio\12.0\Microsoft.VisualStudio.config Nuget.Config 文件以添加"Microsoft 和.NET"包源。 因此，解决在解决方案中使用自定义 repositoryPath 是删除计算机级别 Nuget.Config-这也意味着删除"Microsoft 和.NET"包源。 使用分层 Nuget.Config 文件时，NuGet 2.7.2，它现在遵循 repositoryPath 的优先顺序规则。

## <a name="all-changes"></a>所有更改
有关完整列表的工作项中已修复 NuGet 2.7.2，它，请查看[对于此版本的 NuGet 问题跟踪程序](https://nuget.codeplex.com/workitem/list/advanced?keyword=&status=All&type=All&priority=All&release=NuGet%202.7.2&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0&reasonClosed=Fixed)。
