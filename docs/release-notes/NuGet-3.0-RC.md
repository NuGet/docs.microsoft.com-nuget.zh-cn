---
title: NuGet 3.0 RC 发行说明
description: NuGet 3.0 RC 的发行说明，包括已知问题、bug 修复、新增功能和 Dcr。
author: JonDouglas
ms.author: jodou
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 19bc51a278425295811db253ca3f4ba4366ccf49
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/26/2021
ms.locfileid: "98776578"
---
# <a name="nuget-30-rc-release-notes"></a>NuGet 3.0 RC 发行说明

[NuGet 3.0 Beta 发行说明](../release-notes/nuget-3.0-beta.md)  | [NuGet 3.0 RC2 发行说明](../release-notes/nuget-3.0-RC2.md)

NuGet 3.0 RC 于年4月 29 2015 日发布了 Visual Studio 2015 RC 版本。 此版本包含许多重要的 bug 修复、性能改进和更新以支持新框架。  它仅适用于 Visual Studio 2015。

### <a name="continued-focus-on-performance"></a>继续关注性能

NuGet 查询的稳定性和性能仍是我们关注的热点话题。  在此版本中，你应开始在 NuGet UI 和网站中查看非常快速的搜索操作。  我们将监视服务以及使用服务的方式，以便我们可以继续调整这些操作。

## <a name="significant-issues-resolved"></a>已解决的重要问题

为了使 NuGet 客户端稳定，我们在此版本中解决了许多问题。  下面只是一些更重要的问题已解决的简短列表：

* 在重命名 ASP.NET 5 的 K framework 的过程中，框架名字对象已更新为处理 dnx 和 dnxcore [链接](https://github.com/NuGet/Home/issues/215)
* 通过 Visual Studio UI[链接](https://github.com/NuGet/Home/issues/232)中的链接添加了帮助文档
* `.nuspec`用逗号分隔的框架引用[链接](https://github.com/NuGet/Home/issues/276)更好地处理中的复杂引用
* 固定支持日语区域性 [链接](https://github.com/NuGet/Home/issues/253)
* 更新了客户端以允许 ASP.NET 5 项目使用新的 v3 终结点 [链接](https://github.com/NuGet/Home/issues/219)
* 更新了以更好地处理包含源代码管理[链接](https://github.com/NuGet/Home/issues/56)的包文件夹
* 修复了对附属包的支持 [链接](https://github.com/NuGet/Home/issues/17)
* 更正了对框架特定内容文件[链接](https://github.com/NuGet/Home/issues/18)的支持

## <a name="github-presence-overhaul"></a>GitHub 状态检修

我们已对 [GitHub 上的源代码存储库](http://github.com/nuget/home)进行了一些更改。  如果你在 NuGet Visual Studio 客户端、Powershell 命令或命令行可执行文件中有任何问题，可以记录这些问题，并在 [GitHub Home 存储库问题列表](http://github.com/nuget/home/issues)中监视其进度。  我们正在跟踪 [GitHub NuGetGallery 存储库](http://github.com/nuget/NuGetGallery/issues)中的库问题。


## <a name="stay-tuned"></a>保持关注

有关 NuGet 3.0 的更多进度和公告，请关注 [我们的博客](http://blog.nuget.org) ！