---
title: "NuGet 2.7.2 发行说明 |Microsoft 文档"
author: karann-msft
ms.author: karann-msft
manager: ghogen
ms.date: 11/11/2016
ms.topic: article
ms.prod: nuget
ms.technology: 
ms.assetid: c775d1d7-de26-476c-bf9e-0cf95986a22f
description: "发行说明，了解 NuGet 2.7.2 包括已知问题、 bug 修复、 增加的功能，以及 DCRs。"
keywords: "NuGet 2.7.2 发行说明，bug 修复的已知问题，添加了一些功能，DCRs"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 5bb1eb346666c5d5ee790fcdcd7d844bfd37b22e
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/14/2017
---
# <a name="nuget-272-release-notes"></a>NuGet 2.7.2 发行说明

[NuGet 2.7.1 发行说明](../release-notes/nuget-2.7.1.md) | [NuGet 2.8 发行说明](../release-notes/nuget-2.8.md)

NuGet 2.7.2 已于 2013 年 11 月 11 日发布。

## <a name="noteworthy-bug-fixes-and-features"></a>值得注意的 Bug 修补程序和功能

### <a name="license-text"></a>许可证文本
很长一段时间，Microsoft 具有 Visual Studio 中包含的 Web 应用程序项目的默认模板一部分的几个常用的开源库的 NuGet 包。 jQuery 可能是库的这种类型的已知示例。 由于与随产品一起传递的组件相关的支持协议，包的脚本文件包含其他许可证文本中比在公共 nuget.org 库上位于同一个包的脚本文件。 文本这种差异可以防止由于导致要具有不同的内容哈希值的脚本文件的其他许可证文本块继续包更新 （并因此被视为修改项目中）。

若要缓解此问题，NuGet 2.7.2 允许脚本作者以包括如下所示的特殊标记部分中的许可证文本块。

    /************** NUGET: BEGIN LICENSE TEXT **************
     * The following code is licensed under the MIT license
     * Additional license information below is informational
     * only.
     ************** NUGET: END LICENSE TEXT ***************/

更新包的内容时文件，其中包含此块中，NuGet 不等因素如何影响块中的内容与 NuGet 库上的版本的比较结果和可以因此删除和更新内容文件，就好像它与匹配的原始副本。

通过文本"NUGET:: 开始许可证 TEXT"和"NUGET:: 许可证文本结束"发生任何位置上开始和结束行标识此块。  没有其他格式设置要求存在，允许要在任何一种文本文件，而不考虑语言中使用此功能。

### <a name="add-binding-redirects-for-non-framework-assemblies"></a>添加绑定重定向的非 Framework 程序集
对于属于.NET Framework 的程序集，NuGet 时，跳过添加绑定重定向到应用程序的配置文件更新包。 此修补程序地址，由此绑定重定向正在添加的某些程序集，即使这些程序集不是 NuGet 2.7 中的回归被认为.NET Framework 的一部分。 NuGet 2.7.2 还原以前的 NuGet 2.5 和 2.6 行为，并将添加的绑定重定向。

### <a name="installing-portable-libraries-with-xamarin-tools-installed"></a>使用安装的 Xamarin 工具安装的可移植库
当在计算机上安装了 Xamarin 的开发工具时，他们将修改要指定现有的目标 framework 组合和 Xamarin 框架之间的兼容性的支持的框架配置数据。 使用版本 2.7.2，NuGet 目前感知这些隐式的兼容性的规则，并且因此轻松地针对 Xamarin 平台的开发人员包中的这种情况下安装 Xamarin 兼容，但未显式标记的可移植库元数据本身。

### <a name="machine-wide-configuration-settings-honored"></a>遵循的计算机范围的配置设置
使用分层 Nuget.Config 文件时，repositoryPath 密钥不被接受 Nuget.Config 文件接近解决方案根。 在 Visual Studio 2013 中，NuGet 安装自定义在 %ProgramData%\NuGet\Config\VisualStudio\12.0\Microsoft.VisualStudio.config Nuget.Config 文件以添加"Microsoft 和.NET"包源。 因此，解决办法在解决方案中使用自定义 repositoryPath 是删除计算机级别 Nuget.Config-这还意味着删除"Microsoft 和.NET"包源。 使用分层 Nuget.Config 文件时，NuGet 2.7.2 现在服从 repositoryPath 的优先顺序规则。

## <a name="all-changes"></a>所有更改
有关工作的完整列表项固定在 NuGet 2.7.2，请查看[对于此版本的 NuGet 问题跟踪程序](https://nuget.codeplex.com/workitem/list/advanced?keyword=&status=All&type=All&priority=All&release=NuGet%202.7.2&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0&reasonClosed=Fixed)。
