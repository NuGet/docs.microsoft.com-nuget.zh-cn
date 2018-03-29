---
title: NuGet 3.0 Beta 发行说明 |Microsoft 文档
author: karann-msft
ms.author: karann-msft
manager: ghogen
ms.date: 11/11/2016
ms.topic: article
ms.prod: nuget
ms.technology: ''
description: 包括已知的问题、 bug 修复、 增加的功能，以及 DCRs NuGet 3.0 试用版的发行说明。
keywords: NuGet 3.0 试用版发行说明，bug 修复的已知问题，添加了一些功能，DCRs
ms.reviewer:
- karann-msft
- unniravindranathan
ms.workload:
- dotnet
- aspnet
ms.openlocfilehash: bb64cbce4f26d84e1ba12930578382f887bb85f8
ms.sourcegitcommit: beb229893559824e8abd6ab16707fd5fe1c6ac26
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/28/2018
---
# <a name="nuget-30-beta-release-notes"></a>NuGet 3.0 Beta 发行说明

[NuGet 3.0 预览版发行说明](../release-notes/nuget-3.0-preview.md) | [NuGet 3.0 RC 发行说明](../release-notes/nuget-3.0-rc.md)

为 Visual Studio 2015 CTP 6 版本情况下，NuGet 3.0 试用版已于 2015 年 2 月 23 日发布。 此版本对我们的团队，意味着大量，我们有大量的体系结构和性能改进，可共享，以及我们非常高兴以开始优化我们 nuget.org 的服务上的性能设置。

我们强烈建议你在安装此新版本之前卸载任何以前版本的 NuGet Visual Studio 2015 扩展。  如果你有与此版本的扩展的任何问题，我们建议你还原到[以前的版本](http://nuget.codeplex.com/downloads/get/909582)用于 Visual Studio 2015 预览版。

## <a name="visual-studio-2012"></a>Visual Studio 2012+

此 NuGet 3.0 试用版，可在 Visual Studio 2015 CTP 6 扩展库中安装。 我们正在努力获取预览谷的 Visual Studio 2012 和 Visual Studio 2013 很快。 我们先前共享到我们的目的[for Visual Studio 2010 停止更新](http://blog.nuget.org/20141002/visual-studio-2010.html)，我们未作出此困难的决策。

## <a name="new-clientserver-api"></a>新的客户端/服务器 API

我们一直在 NuGet 的客户端/服务器协议某些实现详细信息。 我们已完成的工作是创建"API v3"nuget，围绕关键方案，如程序包还原和安装包的高可用性而设计。 新的 API 基于 REST 并且超媒体，我们已选择[JSON LD](http://json-ld.org)作为我们资源格式。

在 NuGet 3.0 试用版位为单位，可以看到在程序包源下拉列表中称为"api.nuget.org"的新包源。   如果你选择该包源，我们将使用我们新的 API 而是要连接到 nuget.org。在 NuGet 3.0 RC 中，此新的 API 基于 v3 的包源将替换 v2 基于"nuget.org"包源。  我们建议禁用所有其他公共包源，并且将仅 api.nuget.org 保留为仅对公共包存储库。

我们已投入了大量的时间生成我们 v3 的 API，并将继续保持标准 v2 API 以访问公共存储库寻求的旧客户端的。

## <a name="updated-ui"></a>更新的 UI

我们已增强，此版本中，以包括让您选择要与包执行的操作，然后转换到屏幕的选项区域中的复选框的预览按钮的组合框中的用户界面。  选项区域不再可折叠，并且现在提供描述可用的选项的帮助链接。

![新的 NuGet UI](./media/NuGet-3.0-Beta/updated-ui.png)


### <a name="operation-logging"></a>操作日志记录

我们删除了日志记录信息，将快速显示和隐藏，同时安装或卸载模式窗口。  确实要查看的信息或能够从其复制并粘贴时，此窗口将添加任何值。  相反，我们现在将重定向所有日志记录到输出窗口的包管理器窗格中的输出。  我们认为这是更舒适，类似于你想要检查的典型生成报表。


### <a name="focus-on-performance"></a>重点放在性能

我们做了大量的名称提高性能的 NuGet 搜索和读取的更改。  这是从我们的客户，我们第一问题，我们想要确保我们在此版本中解决。  我们已优化我们的服务器，构建新的 CDN，并改进匹配逻辑为更具相关性您希望提供查询和更快的包搜索结果。

我们继续通过 NuGet 3.0 开发此阶段操作，我们将优化和监视该 nuget.org 服务以确保我们提供改进的体验。  我们不计划进行的任何停机时间，但将被添加并更改服务中的资源。  关注我们[twitter 订阅源](http://twitter.com/nuget)有关当我们更改服务配置的详细信息。

## <a name="building-nuget-with-nuget"></a>使用 NuGet 构建 NuGet

我们现在具有到它们本身内置于 NuGet 包的多个组件重新构建我们 NuGet 客户端。 此重复使用我们自己的库的强制我们构建组件重复使用以及可以正确打包的。  我们已经能够消除重复的代码，并已了解如何更好地配置我们的开发过程，以支持需要生成在我们的解决方案整个包。  查找博客文章很快我们将讨论有关如何构造代码项目和我们生成过程的工作原理。

## <a name="stay-tuned"></a>请继续关注

请留意[我们的博客](http://blog.nuget.org)了解详细的进度和公告 NuGet 3.0 ！
