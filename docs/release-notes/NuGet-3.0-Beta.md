---
title: NuGet 3.0 测试版发行说明
description: 包括已知的问题、 bug 修复、 新增的功能和 Dcr NuGet 3.0 试用版的发行说明。
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 9f9fec6a1af8dfbcfdcfa05a301ff52409521228
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/04/2018
ms.locfileid: "43550908"
---
# <a name="nuget-30-beta-release-notes"></a>NuGet 3.0 测试版发行说明

[NuGet 3.0 预览版发行说明](../release-notes/nuget-3.0-preview.md) | [NuGet 3.0 RC 发行说明](../release-notes/nuget-3.0-rc.md)

Visual Studio 2015 CTP 6 版本 2015 年 2 月 23 日发布了 NuGet 3.0 试用版。 此版本是指大量与我们的团队，我们有了大量的体系结构和性能改进，若要共享，并且我们很高兴以开始优化我们 nuget.org 的服务上的性能设置。

我们强烈建议您在安装此新版本之前卸载任何以前版本的 Visual Studio 2015 的 NuGet 扩展。  如果有此版本的扩展中的任何问题，我们建议你还原到[早期版本](http://nuget.codeplex.com/downloads/get/909582)以用于 Visual Studio 2015 预览版。

## <a name="visual-studio-2012"></a>Visual Studio 2012 和更高

可在 Visual Studio 2015 CTP 6 扩展库中安装此 NuGet 3.0 试用版。 我们正在努力推出预览版删除 Visual Studio 2012 和 Visual Studio 2013 很快。 我们以前共享到我们的意图[停止更新适用于 Visual Studio 2010](http://blog.nuget.org/20141002/visual-studio-2010.html)，和我们未做出难以决定。

## <a name="new-clientserver-api"></a>新的客户端/服务器 API

我们一直在 NuGet 的客户端/服务器协议一些实现细节。 我们所做的工作是为 NuGet，专为高可用性的关键方案，例如包还原和安装包创建"API v3"。 新的 API 基于 REST 和超媒体和我们所选[JSON-LD](http://json-ld.org)作为我们的资源格式。

在 NuGet 3.0 试用版位中，可以看到称为"api.nuget.org"包源下拉列表中的新包源。   如果您选择的包源，我们将使用我们的新 API，而是要连接到 nuget.org。在 NuGet 3.0 RC 中，此新 API 基于 v3 的包源将替换基于 v2"nuget.org"包源。  我们建议禁用所有其他公共包源，并将仅 api.nuget.org 保留为仅对公共包存储库。

我们已投入了大量的时间构建我们的 v3 API，并将继续为旧客户端查找来访问公共存储库保持标准 v2 API。

## <a name="updated-ui"></a>更新后的 UI

我们已改进在此版本中包括的组合框，将允许您选择要与包执行的操作和转换到屏幕的选项区域中的复选框的预览按钮的用户界面。  选项区域不再可折叠，现在提供描述可用的选项的帮助链接。

![新的 NuGet UI](./media/NuGet-3.0-Beta/updated-ui.png)


### <a name="operation-logging"></a>操作日志记录

我们删除包含的日志记录信息的快速的显示效果并在安装或卸载时隐藏模式窗口。  此窗口时真正想要查看的信息，否则将无法从其复制和粘贴添加任何值。  相反，我们现在重定向所有输出记录到输出窗口的包管理器窗格中。  我们认为这是更舒适和类似于你想要检查的典型生成报表。


### <a name="focus-on-performance"></a>专注于性能

我们做了大量的更改提高性能的 NuGet 搜索和提取操作的名称。  这是从我们的客户，我们首要问题，我们希望确保我们在此版本中解决。  我们已经优化我们的服务器，构建新的 CDN，并改进了匹配逻辑为您的关系更密切希望提供的查询和更快包搜索结果。

随着我们逐步开发的 NuGet 3.0 的这个阶段，我们将优化和监视 nuget.org 服务，以确保我们提供改进的体验。  我们不要计划参与任何停机时间，但将会添加和更改服务中的资源。  请关注我们[twitter 订阅源](http://twitter.com/nuget)有关当我们更改的服务配置的详细信息。

## <a name="building-nuget-with-nuget"></a>使用 NuGet 生成 NuGet

我们现在已为多个组件内置到 NuGet 包本身被重建我们 NuGet 客户端。 此重复使用我们自己的库的迫使我们构建的是重复使用，可以正确打包的组件。  我们已能够消除重复的代码，了解到如何更好地配置我们的开发过程，以支持需要生成在我们的解决方案整个包。  查找博客文章很快我们将讨论有关代码项目的构建方式我们生成过程的工作原理。

## <a name="stay-tuned"></a>请继续关注

请密切关注[我们的博客](http://blog.nuget.org)详细进度和 NuGet 3.0 的公告 ！
