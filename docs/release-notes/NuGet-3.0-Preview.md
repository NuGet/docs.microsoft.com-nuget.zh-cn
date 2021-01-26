---
title: NuGet 3.0 预览版发行说明
description: NuGet 3.0 预览版的发行说明，包括已知问题、bug 修复、新增功能和 Dcr。
author: JonDouglas
ms.author: jodou
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: ecaed21c5e689a488e033404f8042cd1f17eed0d
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/26/2021
ms.locfileid: "98780333"
---
# <a name="nuget-30-preview-release-notes"></a>NuGet 3.0 预览版发行说明

[NuGet 2.9 RC 发行说明](../release-notes/nuget-2.9-rc.md)  | [NuGet 3.0 Beta 发行说明](../release-notes/nuget-3.0-beta.md)

在 Visual Studio 2015 预览版中，NuGet 3.0 预览版于2014年11月12日发布。 我们发布了 NuGet 3.0 预览版。 这是一个很大的版本，我们 (虽然预览) ，但我们很高兴开始收到有关我们所做的更改的反馈。

## <a name="visual-studio-2012"></a>Visual Studio 2012 +

此 NuGet 3.0 预览版包含在 Visual Studio 2015 预览版中。 我们正在努力获取 Visual Studio 2012 的预览版，并在不久后 Visual Studio 2013。 我们之前已经分享我们的意图来 [中止 Visual Studio 2010 的更新](http://blog.nuget.org/20141002/visual-studio-2010.html)，我们确实做出了这一难题。

## <a name="brand-new-ui"></a>全新 UI

有关 NuGet 3.0 预览版的第一件事是我们全新的 UI。 它不再是模式对话框;它现在是一个完整的 Visual Studio 文档窗口。 这样一来，您就可以同时打开多个项目的 UI (和/或解决方案) ，将窗口移出到另一个监视器，并将其停靠在您喜欢的位置等等。

![新 NuGet UI](./media/NuGet-3.0-Preview/new-ui.png)

除了因放弃模式对话框以外的可用性不同之外，我们还在新的 UI 中提供了许多新功能。

### <a name="version-selection"></a>版本选择

可能是最常请求的 UI 功能是允许对包安装和更新进行版本选择-这现在可用。

![选择包版本](./media/NuGet-3.0-Preview/version-selection.png)

不管是安装还是更新包，"版本" 下拉列表都允许您查看包的所有可用版本，其中有一些值得注意的版本升级到列表的顶部以便于选择。 不再需要使用 PowerShell 控制台来获取不是最新版本的特定版本。

### <a name="combined-installedonlineupdates-workflows"></a>组合安装/联机/更新工作流

以前的 UI 有3个选项卡用于安装、联机和更新。 列出的包特定于这些工作流，而可用的操作也是特定于工作流的。 虽然这种情况看似合乎逻辑，但我们听说，你们中的许多人通常会获得这种分离。

现在我们有了组合体验，你可以在其中安装、更新或卸载包，而不考虑选择包的方式。 为了帮助特定工作流，现在提供了一个筛选器下拉列表，使你可以筛选出可查看的包，但之后包的操作是一致的。

![卸载包](./media/NuGet-3.0-Preview/uninstall-package.png)

通过使用 "已安装" 筛选器，你可以轻松地查看已安装的包（其中有更新可用），然后可以通过更改版本选择来卸载或更新包，以查看更改操作可用。

![更新包](./media/NuGet-3.0-Preview/update-package.png)

### <a name="version-consolidation"></a>版本合并

在解决方案中将同一包安装到多个项目中是很常见的。 有时，安装在每个项目中的版本可能会偏离，并且需要合并所使用的版本。 NuGet 3.0 预览版为此方案引入了一项新功能。

可以通过右键单击解决方案并选择 "管理解决方案的 NuGet 包" 来访问解决方案级包管理窗口。 在该版本中，如果选择安装到多个项目中的包，但使用不同的版本，则新的 "合并" 操作将可用。 在下面的屏幕截图中， `Newtonsoft.Json` 已安装到 `SamplesClassLibrary` with 版本中， `6.0.4` 并已安装到 `SamplesConsoleApp` 版本中 `5.0.4` 。

![合并版本](./media/NuGet-3.0-Preview/consolidate.png)

下面是用于合并到单个版本的工作流。

1. `Newtonsoft.Json`在列表中选择包
1. `Consolidate`从 `Action` 下拉列表中选择
1. 使用 `Version` 下拉列表选择要合并到的版本
1. 选中应合并到该版本上的项目的复选框 (请注意，所选版本中已有的项目将灰显) 
1. 单击 " `Consolidate` 执行合并" 按钮

### <a name="operation-previews"></a>操作预览

无论执行哪个操作（安装/更新/卸载），新的 UI 现在提供了一种方法来预览将对项目进行的更改。 此预览将显示要安装的任何新包、将更新的包、将卸载的包以及在操作过程中不会发生更改的包。

在下面的示例中，我们可以看到，安装 SignalR 会导致对项目进行很多更改。

![预览安装 SignalR](./media/NuGet-3.0-Preview/preview.png)

### <a name="installation-options"></a>安装选项

使用 PowerShell 控制台，可以控制几个值得注意的安装选项。 现在，我们还将这些功能引入了 UI 中。 你现在可以控制如何选择依赖项版本的依赖关系解析行为。

![依赖项行为](./media/NuGet-3.0-Preview/dependency-behavior.png)

你还可以指定当包中的内容文件与你的项目中已有的文件发生冲突时要执行的操作。

![文件冲突操作](./media/NuGet-3.0-Preview/file-conflict-action.png)

### <a name="infinite-scrolling"></a>无限滚动

我们使用了在列出包时具有滚动和分页模式的 UI 上，可以获得相当多的反馈。 必须滚动到简短列表的底部，单击下一个页码，然后再次滚动，这相当常见。 利用新的 UI，我们在包列表中实现了无限滚动，只需滚动即可实现，而无需进行更多分页。

![无限滚动](./media/NuGet-3.0-Preview/infinite-scrolling.png)

### <a name="make-it-work-make-it-fast-make-it-pretty"></a>使其正常工作，使其更快，使其变得漂亮

我们很高兴能让你试用这个新的 UI。在此预览里程碑期间，我们已遵循了 "使其正常工作，使其变得更快，使其变得漂亮" 这一良好的言弃。 在此预览版中，我们已完成了上述第一个目标--它的工作原理。 我们知道，这并不是很快，而且我们还知道它并未太好。 相信，我们将在现在和 RC 版本之间处理这些目标。 同时，我们将很乐意倾听您对新 UI 的 *可用性*（工作流、操作和使用新 ui 的方式）的反馈。 

与旧的 UI 相比，我们已经删除了一些函数。 其中一项是有意的，而另一个则不是及时完成。

#### <a name="searching-all-package-sources"></a>搜索 "所有" 包源

旧 UI 允许您对所有包源执行包搜索。 我们已在 UI 中删除该功能，我们不会将其返回。 此功能用于对所有包源执行搜索操作，将结果与组合在一起，并尝试根据排序选择对结果进行排序。

我们发现，搜索相关性确实很难组合在一起。 您是否可以设想对 Google 和 Bing 执行搜索，并将结果结合在一起？ 此外，此功能的速度较慢，很容易 *意外* 使用，我们认为它很少真正有用。 由于此功能存在问题，我们在其上收到了大量可能从未修复的 bug 报告。

#### <a name="update-all"></a>全部更新

过去，我们在旧 UI 中使用了 "全部更新" 按钮。 我们将为 RC 版本恢复此功能。

## <a name="new-clientserver-api"></a>新建客户端/服务器 API

除了新的包管理 UI 中的所有新功能，我们还在处理 NuGet 的客户端/服务器协议的一些实现细节。 我们所做的工作是创建 NuGet 的 "API v3"，这是针对关键方案（如包还原和安装包）的高可用性而设计的。 新 API 基于 REST 和超媒体，我们已选择 [JSON-LD](http://json-ld.org) 作为资源格式。

在 NuGet 3.0 预览位中，你会在 "包源" 下拉列表中看到一个名为 "preview.nuget.org" 的新包源。 如果选择此包源，我们将使用新的 API，而不是连接到 nuget.org。我们使预览源在 UI 中可用，同时我们继续测试、修改和改进新的 API。 在 NuGet 3.0 RC 中，这一基于 API v3 的新包源将替换基于 v2 的 "nuget.org" 包源。

尽管我们将投入使用 API v3，但我们已将所有这些新功能也用于我们的现有 API v2 协议，这意味着它们将适用于除 nuget.org 以外的现有包源。

## <a name="new-features-coming"></a>新功能即将推出

在现在和 3.0 RTM 之间，我们还将处理一些基本的新 NuGet 功能，而不仅仅是在 UI 中看到的内容。 下面是重要投资领域的简短列表：

1. 我们与 Visual Studio 和 MSBuild 团队合作，使 [NuGet 更深入地进入平台](http://blog.nuget.org/20141014/in-the-platform.html)。
1. 我们正在努力放弃安装时包约定，改为在打包时通过引入新的 "权威" [包清单](http://blog.nuget.org/20141023/package-manifests.html)来应用这些约定。
1. 我们正在努力重构 NuGet 基本代码，使客户端和服务器组件可在不同的域中重复使用，而不是在 Visual Studio 中的包管理。
1. 我们将调查 "专用依赖项" 的概念，其中包可以指示它在其他包上仅有依赖实现详细信息，不应将这些依赖项视为顶级依赖项。

## <a name="stay-tuned"></a>保持关注

有关 NuGet 3.0 的更多进度和公告，请关注 [我们的博客](http://blog.nuget.org) ！