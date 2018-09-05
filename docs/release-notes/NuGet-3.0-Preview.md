---
title: NuGet 3.0 预览版发行说明
description: 包括已知的问题、 bug 修复、 新增的功能和 Dcr NuGet 3.0 Preview 的发行说明。
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 9389639476172d05556b95d589e429ddfe0e3026
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/04/2018
ms.locfileid: "43546460"
---
# <a name="nuget-30-preview-release-notes"></a>NuGet 3.0 预览版发行说明

[NuGet 2.9 RC 发行说明](../release-notes/nuget-2.9-rc.md) | [NuGet 3.0 测试版发行说明](../release-notes/nuget-3.0-beta.md)

NuGet 3.0 预览版发布于 2014 年 11 月 12 日作为 Visual Studio 2015 预览版发布的一部分。 我们发布了 NuGet 3.0 预览版。 这是对我们很重要的版本 （尽管预览版），和我们高兴地开始获取反馈，我们更改。

## <a name="visual-studio-2012"></a>Visual Studio 2012 和更高

此 NuGet 3.0 预览版包括在 Visual Studio 2015 预览版中。 我们正在努力推出预览版删除 Visual Studio 2012 和 Visual Studio 2013 很快。 我们以前共享到我们的意图[停止更新适用于 Visual Studio 2010](http://blog.nuget.org/20141002/visual-studio-2010.html)，和我们未做出难以决定。

## <a name="brand-new-ui"></a>全新的 UI

你注意到有关 NuGet 3.0 Preview 的第一件事是我们全新的 UI。 它不再是一个模式对话框;它现在是一个完整的 Visual Studio 文档窗口。 这允许你在一次打开多个项目 （和/或解决方案） 的 UI，拉出到另一个监视器窗口中，将其固定，但您会喜欢，等等。

![新的 NuGet UI](./media/NuGet-3.0-Preview/new-ui.png)

除了可用性差异由于放弃模式对话框中，我们还在新 UI 有很多新功能。

### <a name="version-selection"></a>版本选择

可能是最常请求的 UI 功能是允许版本选择的包的安装和更新-此功能现提供。

![包版本选择](./media/NuGet-3.0-Preview/version-selection.png)

无论您是安装还是更新包，版本下拉列表中，可查看所有与提升轻松选择列表的顶部为一些值得注意版本可用于包的版本。 不再需要使用 PowerShell 控制台来获取不是最新的特定版本。

### <a name="combined-installedonlineupdates-workflows"></a>合并已安装/联机/更新工作流

我们以前的 UI 更新已安装，联机，以及有 3 个选项卡。 列出的包是特定于这些工作流，并且特定于工作流以及可用的操作。 虽然这看起来逻辑，我们听说过很多人通常会获取掣肘： 这种分离。

现在，我们有组合的体验，可以在其中安装、 更新或卸载包而不考虑如何达到选择的包。 为了帮助与特定工作流，我们现在有一个筛选器下拉列表，可以筛选包可见，但然后可用包的操作保持一致。

![卸载包](./media/NuGet-3.0-Preview/uninstall-package.png)

通过使用"已安装"筛选器，然后，您可以轻松地看到哪些功能具有可用的更新，你已安装的包，然后你可以卸载或更改版本选择以查看更新包更改可用的操作。

![更新的包](./media/NuGet-3.0-Preview/update-package.png)

### <a name="version-consolidation"></a>版本合并

它是常见的同一个包安装到您的解决方案内的多个项目。 有时安装到每个项目的版本可以偏离和需要合并中使用的版本。 NuGet 3.0 Preview 引入了新功能，可解决此类问题。

可以通过右键单击解决方案并选择为解决方案管理 NuGet 包访问解决方案级包管理窗口。 在这里，如果您选择安装到多个项目，但在使用中，不同版本的包的新的"合并"操作将变为可用。 在以下屏幕截图，`Newtonsoft.Json`安装到`SamplesClassLibrary`版本`6.0.4`且已安装到`SamplesConsoleApp`版本`5.0.4`。

![合并版本](./media/NuGet-3.0-Preview/consolidate.png)

下面是将合并到单个版本上的工作流。

1. 选择`Newtonsoft.Json`列表中的包
1. 选择`Consolidate`从`Action`下拉列表中
1. 使用`Version`下拉列表中选择要合并到的版本
1. 选中的复选框应合并到该版本 （请注意，已在所选的版本上的项目将灰显） 的项目
1. 单击`Consolidate`按钮以执行合并

### <a name="operation-previews"></a>操作预览

无论哪个操作在执行-安装/更新/卸载-新用户界面现在提供了一种方法，若要预览将会对项目所做的更改。 此预览会显示任何新的包将安装包，将被更新，并且包将被卸载，以及在操作期间将保持不变的包。

在下面的示例中，我们可以看到，安装 Microsoft.AspNet.SignalR 会导致相当多的更改到项目。

![预览版安装 SignalR](./media/NuGet-3.0-Preview/preview.png)

### <a name="installation-options"></a>安装选项

使用 PowerShell 控制台，在过去的几个值得注意的安装选项控制。 现在，我们已引入 UI 还将这些功能。 现在可以控制如何选择版本的依赖项的依赖关系解析行为。

![依赖关系行为](./media/NuGet-3.0-Preview/dependency-behavior.png)

此外可以指定当包中的内容文件与你的项目中的现有文件冲突时要执行的操作。

![文件冲突操作](./media/NuGet-3.0-Preview/file-conflict-action.png)

### <a name="infinite-scrolling"></a>无限滚动

我们用于获取大量的反馈对我们的 UI 具有这两个滚动和列出的包时分页模式。 这是相当常见的要滚动到底部的短列表，请单击下一步的页码，再然后向下滚动。 使用新的用户界面，我们已实现无限滚动包列表中，以便只需要进行滚动-没有更多的分页。

![无限滚动](./media/NuGet-3.0-Preview/infinite-scrolling.png)

### <a name="make-it-work-make-it-fast-make-it-pretty"></a>使其工作，使其快速，使其美观

我们很高兴为您尝试推出此新 UI。在此预览阶段，我们已经遵循良好老话"使其工作，使其快速、 使其美观。" 在此预览版中，我们已完成大多数的这个第一个目标-其工作原理。 我们知道它非常快速还不是，我们知道它非常非常还不是。 我们将使用这些目标现在和 RC 版本之间的信任。 在此期间，我们期待倾听您的反馈意见*可用性*的新 UI-工作流、 操作、 以及如何它*感觉*以使用新的用户界面。

有几个我们将删除与旧 UI 相比的函数。 其中一种是特意的和另一个只是未完成的时间。

#### <a name="searching-all-package-sources"></a>搜索"所有"包源

旧 UI 允许您执行针对包源的所有包的搜索。 我们在 UI 中删除了该功能，我们将不会将其返回。 此功能，用于执行搜索操作针对所有包源，归纳到一起，，结果，然后尝试基于排序所选对结果进行排序。

我们发现很难归纳到一起，搜索相关性。 可以想象得到执行针对 Google 和必应搜索，以及一起编辑结果？ 此外，此功能是速度较慢且易于*意外*使用和我们认为它很少实际上非常有用。 由于问题的功能中引入，我们收到数可能永远不会得到了修复的 bug 报告在其上。

#### <a name="update-all"></a>全部更新

我们使用旧 ui 中有新的用户界面中尚不具有"更新全部"按钮。 我们将于我们的 RC 版本恢复此功能。

## <a name="new-clientserver-api"></a>新的客户端/服务器 API

除了所有我们新的包管理 UI 中的新功能，我们也一直在 NuGet 的客户端/服务器协议一些实现细节。 我们所做的工作是为 NuGet，专为高可用性的关键方案，例如包还原和安装包创建"API v3"。 新的 API 基于 REST 和超媒体和我们所选[JSON-LD](http://json-ld.org)作为我们的资源格式。

在 NuGet 3.0 预览版位中，可以看到称为"preview.nuget.org"包源下拉列表中的新包源。 如果您选择的包源，我们将使用我们的新 API，而是要连接到 nuget.org。我们继续测试、 修订和改进的新 API 时，我们已使预览源 UI 中提供。 在 NuGet 3.0 RC 中，此新 API 基于 v3 的包源将替换基于 v2"nuget.org"包源。

尽管我们正在将它们放入 API v3 的投资，我们已使所有这些新功能也适用于我们现有的 API v2 协议，这意味着它们将与现有以外还 nuget.org 的包源。

## <a name="new-features-coming"></a>新功能

从现在到 3.0 的 RTM，我们还致力于一些基本之外的新 NuGet 功能，在 UI 中看到的内容。 下面是一个重要投资领域的简短列表：

1. 我们正与 Visual Studio 合作，并由 MSBuild 团队以获取[深入到该平台的 NuGet](http://blog.nuget.org/20141014/in-the-platform.html)。
1. 我们正在放弃安装时包约定，然后改为在打包时应用这些约定，通过引入一个新"权威"[包清单](http://blog.nuget.org/20141023/package-manifests.html)。
1. 我们正在努力 NuGet 基本代码，以使 Visual Studio 中的包管理范围之外的不同域中的客户端和服务器组件可重用的重构。
1. 我们正在研究的"专用依赖项"其中一个包可以指示它概念实现详细信息，其他包上具有依赖关系，这些依赖项不应显示为顶级依赖项。

## <a name="stay-tuned"></a>请继续关注

请密切关注[我们的博客](http://blog.nuget.org)详细进度和 NuGet 3.0 的公告 ！