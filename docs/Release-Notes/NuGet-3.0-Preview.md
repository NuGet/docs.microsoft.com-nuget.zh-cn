---
title: "NuGet 3.0 预览版发行说明 |Microsoft 文档"
author: karann-msft
ms.author: karann-msft
manager: ghogen
ms.date: 11/11/2016
ms.topic: article
ms.prod: nuget
ms.technology: 
description: "包括已知的问题、 bug 修复、 增加的功能，以及 DCRs NuGet 3.0 预览版的发行说明。"
keywords: "NuGet 3.0 预览版发行说明，bug 修复的已知问题，添加了一些功能，DCRs"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: e07bcad2bf713deee0add72663c84b9979f8c5c4
ms.sourcegitcommit: 262d026beeffd4f3b6fc47d780a2f701451663a8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/25/2018
---
# <a name="nuget-30-preview-release-notes"></a>NuGet 3.0 预览版发行说明

[NuGet 2.9 RC 发行说明](../release-notes/nuget-2.9-rc.md) | [NuGet 3.0 Beta 发行说明](../release-notes/nuget-3.0-beta.md)

NuGet 3.0 预览已于 2014 年 11 月 12 日作为 Visual Studio 2015 预览版的一部分发布。 我们发布了 NuGet 3.0 预览版。 这是为我们的大版本 （但预览版），我们非常高兴地开始获取反馈，我们更改。

## <a name="visual-studio-2012"></a>Visual Studio 2012+

Visual Studio 2015 预览版中包括此 NuGet 3.0 预览。 我们正在努力获取预览谷的 Visual Studio 2012 和 Visual Studio 2013 很快。 我们先前共享到我们的目的[for Visual Studio 2010 停止更新](http://blog.nuget.org/20141002/visual-studio-2010.html)，我们未作出此困难的决策。

## <a name="brand-new-ui"></a>全新 UI

你会注意到有关 NuGet 3.0 预览版的第一件事是我们全新的 UI。 它不再是一个模式对话框;现在，这是一个完整的 Visual Studio 文档窗口。 这允许你在一次打开多个项目 （和/或解决方案） 的 UI，拉出到另一个监视器窗口，将其固定，但是会喜欢，等。

![新的 NuGet UI](./media/NuGet-3.0-Preview/new-ui.png)

超出由于放弃模式对话框的可用性差异，我们还必须在新的用户界面中大量新功能。

### <a name="version-selection"></a>版本选择

可能是最常请求的用户界面功能是允许版本选择的包安装和更新-这是现在可用。

![包版本选择](./media/NuGet-3.0-Preview/version-selection.png)

是否要安装或更新包，则版本下拉列表中，可查看所有可用的版本的包，对于某些值得注意的版本升级为轻松选择列表的顶部。 你不再需要使用 PowerShell 控制台来获取不是最新的特定版本。

### <a name="combined-installedonlineupdates-workflows"></a>组合的安装/联机/更新工作流

我们以前 UI 更新已安装，联机，以及具有三个选项卡。 列出的包是特定于这些工作流以及特定于工作流以及可用的操作。 通过这种分离情况下时，看起来逻辑，我们听说你们中的许多通常会获取触发。

我们现在有组合的体验，其中可以安装、 更新或卸载无论你如何选择的包的包。 为了帮助的特定工作流，我们现在有筛选器下拉列表中，你可以筛选包可见，但适用于包的操作都是一致。

![卸载包](./media/NuGet-3.0-Preview/uninstall-package.png)

通过使用"已安装"筛选器，你就可以轻松看到哪些功能具有可用的更新，你已安装的程序包，然后你可以卸载或者通过更改版本选择以查看更新的包更改可用的操作。

![更新的包](./media/NuGet-3.0-Preview/update-package.png)

### <a name="version-consolidation"></a>版本合并

它很常见同一个包安装到您的解决方案内的多个项目。 有时安装到每个项目的版本可以偏离，并且有必要整合中使用的版本。 NuGet 3.0 Preview 引入了一个新功能，只是这种情况。

可以通过右键单击解决方案并选择管理解决方案的 NuGet 包访问解决方案级包管理窗口。 在这里，如果您选择安装到多个项目，但使用不同版本中使用，包的新的"合并"操作可用。 在以下屏幕截图，`Newtonsoft.Json`安装到`SamplesClassLibrary`版本`6.0.4`且已安装到`SamplesConsoleApp`版本`5.0.4`。

![合并版本](./media/NuGet-3.0-Preview/consolidate.png)

下面是将合并到单个版本的工作流。

1. 选择`Newtonsoft.Json`列表中的包
1. 选择`Consolidate`从`Action`下拉列表中
1. 使用`Version`下拉列表中选择要合并到的版本
1. 选中的复选框应整合到该版本 （请注意，已在所选版本的项目将灰显） 的项目
1. 单击`Consolidate`按钮来执行合并

### <a name="operation-previews"></a>操作预览

无论哪个操作当前正在执行-安装/更新/卸载-新的用户界面现在提供预览将向你的项目所做的更改的方法。 此预览版将显示的任何新包将安装包，将会更新，并且包将卸载，以及在操作期间将保持不变的包。

在下面的示例中，我们可以看到，安装 Microsoft.AspNet.SignalR 将导致相当多的更改到项目。

![安装 SignalR 的预览](./media/NuGet-3.0-Preview/preview.png)

### <a name="installation-options"></a>安装选项

使用 PowerShell 控制台，你已经有几个值得注意的安装选项控制。 现在，我们已将这些功能也在 ui。 你现可控制如何选择依赖项的版本的依赖项解析行为。

![依赖项行为](./media/NuGet-3.0-Preview/dependency-behavior.png)

你还可以指定当从包的内容文件与已在你的项目的文件发生冲突时要执行的操作。

![文件冲突操作](./media/NuGet-3.0-Preview/file-conflict-action.png)

### <a name="infinite-scrolling"></a>无限滚动

我们用于获取很多有关我们的 UI 的反馈具有这两个滚动和分页范例，列出包时。 常见的做法是非常必须滚动到底部的短列表，请单击下一步的页号，然后再次然后向下滚动。 与新的 UI 中，我们已经实现无限滚动在包列表中，以便仅需要进行滚动-没有更多的分页。

![无限滚动](./media/NuGet-3.0-Preview/infinite-scrolling.png)

### <a name="make-it-work-make-it-fast-make-it-pretty"></a>使其工作，请使其快速，使其优质

我们很高兴获取此新的用户界面，供你试用。在此预览版的里程碑，我们已经遵循良好旧句箴言，而且的"使其工作，使其快速，使其非常。" 在此预览版中，我们已完成大多数的此第一个目标就其工作原理。 我们知道它不是相当快速尚未和我们知道它尚不可相当相当。 我们会处理这些目标现在的 RC 版本之间的信任。 在此期间，我们很乐意倾听你的反馈有关*可用性*的新 UI-工作流、 操作，以及它*外观*以使用新的用户界面。

有几个我们将删除与旧 UI 相比的函数。 以下方法之一是特意的和另一个只是未在时间内完成。

#### <a name="searching-all-package-sources"></a>搜索的"所有"包源

旧 UI 允许你执行针对你的包源的所有包的搜索。 我们在 UI 中将删除该功能，我们将不会使其返回。 用于执行搜索操作针对所有包源，此功能 weave 配合使用，结果在一起，并尝试根据排序的选择对结果进行排序。

我们找到搜索相关性很难 weave 配合使用，在一起。 可以想象得到执行针对 Google 和必应搜索，并在一起种结果编制方法？ 此外，此功能已速度慢、 易于*意外*使用和我们认为它是很少确实有用。 由于问题中引入的功能我们已收到大量的无法从不已修复的 bug 报告在其上。

#### <a name="update-all"></a>更新所有

我们用于旧 ui 中不存在新的用户界面中尚未具有一个"全部更新"按钮。 我们将使此功能重新起用对于我们的 RC 版本。

## <a name="new-clientserver-api"></a>新的客户端/服务器 API

除了所有我们新的程序包管理 UI 中的新功能，我们还整理 NuGet 的客户端/服务器协议某些实现详细信息。 我们已完成的工作是创建"API v3"nuget，围绕关键方案，如程序包还原和安装包的高可用性而设计。 新的 API 基于 REST 并且超媒体，我们已选择[JSON LD](http://json-ld.org)作为我们资源格式。

以 NuGet 3.0 预览位为单位，你将看到在程序包源下拉列表中称为"preview.nuget.org"的新包源。 如果你选择该包源，我们将使用我们新的 API 而是要连接到 nuget.org。我们继续测试、 修订和提高新的 API 时，我们已简化预览源在 UI 中可用。 在 NuGet 3.0 RC 中，此新的 API 基于 v3 的包源将替换 v2 基于"nuget.org"包源。

尽管我们正在将放入 API v3 的投资，我们进行了所有这些新功能与我们现有的 API v2 协议，这意味着它们将使用 nuget.org 以及以外的现有包源一同使用。

## <a name="new-features-coming"></a>新的多功能即将推出

现在，3.0 RTM，我们还致力于一些基本 NuGet 之外新功能，将在 UI 中看到的内容。 下面是一个突出投资领域的简短列表：

1. 我们正在合作使用 Visual Studio 和 MSBuild 团队以获取[NuGet 深入到平台](http://blog.nuget.org/20141014/in-the-platform.html)。
1. 我们正在努力放弃安装时间包约定并改为在打包时应用这些约定，通过引入了一个新"具有权威"[包清单](http://blog.nuget.org/20141023/package-manifests.html)。
1. 我们正在努力 NuGet 基本代码，以使局限于 Visual Studio 中的包管理的不同域中的客户端和服务器组件可重用的重构。
1. 我们正在调查的概念"专用依赖关系"其中一个包可以指示它是实现详细信息仅，其他包上具有依赖关系，这些依赖关系不应显示为顶级依赖项。

## <a name="stay-tuned"></a>请继续关注

请留意[我们的博客](http://blog.nuget.org)了解详细的进度和公告 NuGet 3.0 ！