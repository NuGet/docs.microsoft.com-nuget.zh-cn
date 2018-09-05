---
title: NuGet 3.0 RC 发行说明
description: 包括已知的问题、 bug 修复、 新增的功能和 Dcr NuGet 3.0 RC 的发行说明。
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 0575cb1598f259a1cf1597f67123b644d67c31b5
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/04/2018
ms.locfileid: "43551714"
---
# <a name="nuget-30-rc-release-notes"></a>NuGet 3.0 RC 发行说明

[NuGet 3.0 测试版发行说明](../release-notes/nuget-3.0-beta.md) | [NuGet 3.0 RC2 发行说明](../release-notes/nuget-3.0-RC2.md)

NuGet 3.0 RC 与 Visual Studio 2015 RC 版本发布于 2015 年 4 月 29 日。 此版本包含重要的 bug 修复、 性能改进和更新以支持新框架的数量。  它是仅适用于 Visual Studio 2015。

### <a name="continued-focus-on-performance"></a>对性能方面的不懈关注

稳定性和 NuGet 查询的性能仍是我们的重心一个热门的话题。  此版本中，您将会看到非常快速的搜索操作中的 NuGet UI 和网站。  我们正在监视服务以及如何使用该服务，以便我们可以继续调整这些操作。

## <a name="significant-issues-resolved"></a>已解决的重要问题

为了达到稳定状态的 NuGet 客户端，作为此发布的一部分解决许多问题。  下面是只是简要的一些更重要的问题已解决的列表：

* ASP.NET 5 K framework 的重命名的一部分，已更新了框架名字对象来处理 dnx 和 dnxcore[链接](https://github.com/NuGet/Home/issues/215)
* 从 Visual Studio UI 中的链接添加帮助文档[链接](https://github.com/NuGet/Home/issues/232)
* 更好地处理中的复杂引用`.nuspec`使用以逗号分隔的框架引用[链接](https://github.com/NuGet/Home/issues/276)
* 修复了对日语区域性的支持[链接](https://github.com/NuGet/Home/issues/253)
* 更新的客户端以允许 ASP.NET 5 项目使用新的 v3 终结点[链接](https://github.com/NuGet/Home/issues/219)
* 更新为更好的句柄与源代码管理的包文件夹[链接](https://github.com/NuGet/Home/issues/56)
* 修复了对附属包的支持[链接](https://github.com/NuGet/Home/issues/17)
* 更正了对特定于框架的内容文件的支持[链接](https://github.com/NuGet/Home/issues/18)

## <a name="github-presence-overhaul"></a>GitHub 存在革新

我们做出了一些更改到我们[源代码存储库在 GitHub 上的](http://github.com/nuget/home)。  如果使用 Visual Studio 的 NuGet 客户端、 Powershell 命令或命令行中有任何问题可执行文件可以记录这些问题和监视其进度上我们[主页 GitHub 存储库问题列表](http://github.com/nuget/home/issues)。  我们在跟踪中的库的问题我们[GitHub NuGetGallery 存储库](http://github.com/nuget/NuGetGallery/issues)。


## <a name="stay-tuned"></a>请继续关注

请密切关注[我们的博客](http://blog.nuget.org)详细进度和 NuGet 3.0 的公告 ！