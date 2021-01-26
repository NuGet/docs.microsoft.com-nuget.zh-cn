---
title: NuGet 3.0 Beta 发行说明
description: NuGet 3.0 Beta 发行说明，包括已知问题、bug 修复、新增功能和 Dcr。
author: JonDouglas
ms.author: jodou
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 7970c3d81c724edc743d7b2d38c4c157237a0271
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/26/2021
ms.locfileid: "98776619"
---
# <a name="nuget-30-beta-release-notes"></a>NuGet 3.0 Beta 发行说明

[NuGet 3.0 预览版发行说明](../release-notes/nuget-3.0-preview.md)  | [NuGet 3.0 RC 发行说明](../release-notes/nuget-3.0-rc.md)

在 Visual Studio 2015 CTP 6 版本的2015上发布了 NuGet 3.0 Beta 版。 这一版本非常适用于我们的团队，因为我们有很多体系结构和性能方面的改进需要进行共享，我们非常高兴地开始优化我们的 nuget.org 服务的性能设置。

我们强烈建议你在安装此新版本之前卸载任何以前版本的 NuGet Visual Studio 2015 扩展。  如果此版本的扩展有任何问题，我们建议您恢复到 [以前的版本](http://nuget.codeplex.com/downloads/get/909582) ，以便与 Visual Studio 2015 preview 一起使用。

## <a name="visual-studio-2012"></a>Visual Studio 2012 +

此 NuGet 3.0 Beta 版可安装在 Visual Studio 2015 CTP 6 扩展库中。 我们正在努力获取 Visual Studio 2012 的预览版，并在不久后 Visual Studio 2013。 我们之前已经分享我们的意图来 [中止 Visual Studio 2010 的更新](http://blog.nuget.org/20141002/visual-studio-2010.html)，我们确实做出了这一难题。

## <a name="new-clientserver-api"></a>新建客户端/服务器 API

我们一直在处理 NuGet 的客户端/服务器协议的一些实现细节。 我们所做的工作是创建 NuGet 的 "API v3"，这是针对关键方案（如包还原和安装包）的高可用性而设计的。 新 API 基于 REST 和超媒体，我们已选择 [JSON-LD](http://json-ld.org) 作为资源格式。

在 NuGet 3.0 Beta 版中，你会在 "包源" 下拉列表中看到一个名为 "api.nuget.org" 的新包源。   如果选择此包源，我们将使用新的 API，而不是连接到 nuget.org。在 NuGet 3.0 RC 中，这一基于 API v3 的新包源将替换基于 v2 的 "nuget.org" 包源。  建议禁用所有其他公共包源，并仅将 api.nuget.org 保留为你的唯一公共包存储库。

我们投入了大量时间来构建 v3 API，并将继续为寻找公共存储库的旧客户端维护标准 v2 API。

## <a name="updated-ui"></a>更新的 UI

我们增强了此版本中的用户界面，以包含一个组合框，使用该组合框可以选择要对包执行的操作，并将预览按钮转换为屏幕 "选项" 区域中的复选框。  选项区域不再可折叠，现在提供了描述可用选项的帮助链接。

![新 NuGet UI](./media/NuGet-3.0-Beta/updated-ui.png)


### <a name="operation-logging"></a>操作日志记录

我们删除了模式窗口，其中包含的日志记录信息会在安装或卸载时快速显示和隐藏。  如果你确实想要查看该信息或能够从它进行复制和粘贴，此窗口不会添加任何值。  相反，我们现在会将所有输出日志记录都重定向到 "输出" 窗口的 "包管理器" 窗格。  我们认为这种方式更加舒适，与要检查的典型生成报告类似。


### <a name="focus-on-performance"></a>专注于性能

我们对提高 NuGet 搜索和提取性能的名称进行了很多更改。  这是我们的客户的一项重要问题，我们希望在此版本中解决此问题。  我们已经优化了服务器，并构建了新的 CDN，并改进了查询匹配逻辑，从而为你提供了更多相关、更快的包搜索结果。

随着 NuGet 3.0 的这一阶段的发展，我们将对 nuget.org 服务进行优化和监视，以确保提供更好的体验。  我们不打算在任何故障时间内进行维护，但会在服务中添加和更改资源。  若要详细了解如何更改服务配置，请留意 [twitter 源](http://twitter.com/nuget) 。

## <a name="building-nuget-with-nuget"></a>用 NuGet 构建 NuGet

我们现在已将 NuGet 客户端重建到了多个组件，这些组件本身就内置于 NuGet 包中。 这种重复使用我们自己的库将强制构建可重复使用并且可正确打包的组件。  我们已经能够消除重复的代码，并了解了如何更好地配置开发过程，以支持在整个解决方案中构建包。  在这里，我们将讨论如何构造代码项目以及我们的生成过程如何工作的博客文章。

## <a name="stay-tuned"></a>保持关注

有关 NuGet 3.0 的更多进度和公告，请关注 [我们的博客](http://blog.nuget.org) ！
