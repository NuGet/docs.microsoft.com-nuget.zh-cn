---
title: NuGet 3.0 RC 发行说明
description: 包括已知的问题、 bug 修复、 增加的功能，以及 DCRs NuGet 3.0 RC 的发行说明。
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 28ac49d9e9071d16d20b24808abb0acaab214ffd
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/26/2018
ms.locfileid: "31819593"
---
# <a name="nuget-30-rc-release-notes"></a>NuGet 3.0 RC 发行说明

[NuGet 3.0 Beta 发行说明](../release-notes/nuget-3.0-beta.md) | [NuGet 3.0 RC2 发行说明](../release-notes/nuget-3.0-RC2.md)

随 Visual Studio 2015 RC 版本于 2015 年 4 月 29 日发布 NuGet 3.0 RC。 此版本有大量的重要的 bug 修复、 性能改进和更新以支持新的框架。  它才可用于 Visual Studio 2015。

### <a name="continued-focus-on-performance"></a>一贯的关注性能

稳定性和性能的 NuGet 查询仍是我们关注的热门话题。  此版本中，你将会看到在 NuGet UI 和网站的非常快速搜索操作。  我们正在监视的服务以及如何使用服务，以便我们可以继续优化这些操作。

## <a name="significant-issues-resolved"></a>解决的重要问题

为了保持稳定，NuGet 客户端，我们解决许多问题作为此版本的一部分。  下面是只需要的一些更重要的问题已解决的简短列表：

* 作为 ASP.NET 5 K framework 的重命名的一部分，已更新了框架名字对象来处理 dnx 和 dnxcore[链接](https://github.com/NuGet/Home/issues/215)
* 从 Visual Studio UI 中的链接添加帮助文档[链接](https://github.com/NuGet/Home/issues/232)
* 更好地处理中的复杂引用`.nuspec`与以逗号分隔 framework 引用[链接](https://github.com/NuGet/Home/issues/276)
* 修复了对日语区域性的支持[链接](https://github.com/NuGet/Home/issues/253)
* 更新的客户端，以允许 ASP.NET 5 项目以使用新的 v3 终结点[链接](https://github.com/NuGet/Home/issues/219)
* 更新为更好的句柄与源代码管理的包文件夹[链接](https://github.com/NuGet/Home/issues/56)
* 固定附属包支持[链接](https://github.com/NuGet/Home/issues/17)
* 更正的特定于框架的内容文件的支持[链接](https://github.com/NuGet/Home/issues/18)

## <a name="github-presence-overhaul"></a>GitHub 状态检查

我们已对一些更改我们[源在 GitHub 上的代码存储库](http://github.com/nuget/home)。  如果你有任何问题，NuGet Visual Studio 客户端、 Powershell 命令或命令行可执行你可以记录这些问题和上监视其进度我们[GitHub 主页存储库问题列表](http://github.com/nuget/home/issues)。  我们在跟踪中的库的问题我们[GitHub NuGetGallery 存储库](http://github.com/nuget/NuGetGallery/issues)。


## <a name="stay-tuned"></a>请继续关注

请留意[我们的博客](http://blog.nuget.org)了解详细的进度和公告 NuGet 3.0 ！