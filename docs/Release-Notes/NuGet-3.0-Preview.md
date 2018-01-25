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
# <a name="nuget-30-preview-release-notes"></a><span data-ttu-id="2d9a7-104">NuGet 3.0 预览版发行说明</span><span class="sxs-lookup"><span data-stu-id="2d9a7-104">NuGet 3.0 Preview Release Notes</span></span>

<span data-ttu-id="2d9a7-105">[NuGet 2.9 RC 发行说明](../release-notes/nuget-2.9-rc.md) | [NuGet 3.0 Beta 发行说明](../release-notes/nuget-3.0-beta.md)</span><span class="sxs-lookup"><span data-stu-id="2d9a7-105">[NuGet 2.9 RC Release Notes](../release-notes/nuget-2.9-rc.md) | [NuGet 3.0 Beta Release Notes](../release-notes/nuget-3.0-beta.md)</span></span>

<span data-ttu-id="2d9a7-106">NuGet 3.0 预览已于 2014 年 11 月 12 日作为 Visual Studio 2015 预览版的一部分发布。</span><span class="sxs-lookup"><span data-stu-id="2d9a7-106">NuGet 3.0 Preview was released on November 12, 2014 as part of the Visual Studio 2015 Preview release.</span></span> <span data-ttu-id="2d9a7-107">我们发布了 NuGet 3.0 预览版。</span><span class="sxs-lookup"><span data-stu-id="2d9a7-107">We released NuGet 3.0 Preview.</span></span> <span data-ttu-id="2d9a7-108">这是为我们的大版本 （但预览版），我们非常高兴地开始获取反馈，我们更改。</span><span class="sxs-lookup"><span data-stu-id="2d9a7-108">This is a big release for us (albeit a preview), and we're excited to start getting feedback on our changes.</span></span>

## <a name="visual-studio-2012"></a><span data-ttu-id="2d9a7-109">Visual Studio 2012+</span><span class="sxs-lookup"><span data-stu-id="2d9a7-109">Visual Studio 2012+</span></span>

<span data-ttu-id="2d9a7-110">Visual Studio 2015 预览版中包括此 NuGet 3.0 预览。</span><span class="sxs-lookup"><span data-stu-id="2d9a7-110">This NuGet 3.0 Preview is included in Visual Studio 2015 Preview.</span></span> <span data-ttu-id="2d9a7-111">我们正在努力获取预览谷的 Visual Studio 2012 和 Visual Studio 2013 很快。</span><span class="sxs-lookup"><span data-stu-id="2d9a7-111">We are working to get preview drops out for Visual Studio 2012 and Visual Studio 2013 very soon.</span></span> <span data-ttu-id="2d9a7-112">我们先前共享到我们的目的[for Visual Studio 2010 停止更新](http://blog.nuget.org/20141002/visual-studio-2010.html)，我们未作出此困难的决策。</span><span class="sxs-lookup"><span data-stu-id="2d9a7-112">We previously shared our intent to [discontinue updates for Visual Studio 2010](http://blog.nuget.org/20141002/visual-studio-2010.html), and we did make that difficult decision.</span></span>

## <a name="brand-new-ui"></a><span data-ttu-id="2d9a7-113">全新 UI</span><span class="sxs-lookup"><span data-stu-id="2d9a7-113">Brand New UI</span></span>

<span data-ttu-id="2d9a7-114">你会注意到有关 NuGet 3.0 预览版的第一件事是我们全新的 UI。</span><span class="sxs-lookup"><span data-stu-id="2d9a7-114">The first thing you'll notice about NuGet 3.0 Preview is our brand new UI.</span></span> <span data-ttu-id="2d9a7-115">它不再是一个模式对话框;现在，这是一个完整的 Visual Studio 文档窗口。</span><span class="sxs-lookup"><span data-stu-id="2d9a7-115">It's no longer a modal dialog; it's now a full Visual Studio document window.</span></span> <span data-ttu-id="2d9a7-116">这允许你在一次打开多个项目 （和/或解决方案） 的 UI，拉出到另一个监视器窗口，将其固定，但是会喜欢，等。</span><span class="sxs-lookup"><span data-stu-id="2d9a7-116">This allows you to open the UI for multiple projects (and/or the solution) at once, tear the window off to another monitor, dock it however you'd like, etc.</span></span>

![新的 NuGet UI](./media/NuGet-3.0-Preview/new-ui.png)

<span data-ttu-id="2d9a7-118">超出由于放弃模式对话框的可用性差异，我们还必须在新的用户界面中大量新功能。</span><span class="sxs-lookup"><span data-stu-id="2d9a7-118">Beyond the usability differences because of abandoning the modal dialog, we also have lots of new features in the new UI.</span></span>

### <a name="version-selection"></a><span data-ttu-id="2d9a7-119">版本选择</span><span class="sxs-lookup"><span data-stu-id="2d9a7-119">Version Selection</span></span>

<span data-ttu-id="2d9a7-120">可能是最常请求的用户界面功能是允许版本选择的包安装和更新-这是现在可用。</span><span class="sxs-lookup"><span data-stu-id="2d9a7-120">Perhaps the most requested UI feature is to allow version selection for package installation and update--this is now available.</span></span>

![包版本选择](./media/NuGet-3.0-Preview/version-selection.png)

<span data-ttu-id="2d9a7-122">是否要安装或更新包，则版本下拉列表中，可查看所有可用的版本的包，对于某些值得注意的版本升级为轻松选择列表的顶部。</span><span class="sxs-lookup"><span data-stu-id="2d9a7-122">Whether you are installing or updating a package, the version dropdown allows you to see all of the versions available for the package, with some notable versions promoted to the top of the list for easy selection.</span></span> <span data-ttu-id="2d9a7-123">你不再需要使用 PowerShell 控制台来获取不是最新的特定版本。</span><span class="sxs-lookup"><span data-stu-id="2d9a7-123">You no longer need to use the PowerShell Console to get specific versions that are not the latest.</span></span>

### <a name="combined-installedonlineupdates-workflows"></a><span data-ttu-id="2d9a7-124">组合的安装/联机/更新工作流</span><span class="sxs-lookup"><span data-stu-id="2d9a7-124">Combined Installed/Online/Updates Workflows</span></span>

<span data-ttu-id="2d9a7-125">我们以前 UI 更新已安装，联机，以及具有三个选项卡。</span><span class="sxs-lookup"><span data-stu-id="2d9a7-125">Our previous UI had 3 tabs for Installed, Online, and Updates.</span></span> <span data-ttu-id="2d9a7-126">列出的包是特定于这些工作流以及特定于工作流以及可用的操作。</span><span class="sxs-lookup"><span data-stu-id="2d9a7-126">The packages listed were specific to those workflows and the actions available were specific to the workflows as well.</span></span> <span data-ttu-id="2d9a7-127">通过这种分离情况下时，看起来逻辑，我们听说你们中的许多通常会获取触发。</span><span class="sxs-lookup"><span data-stu-id="2d9a7-127">While that seemed logical, we heard that many of you would often get tripped up by this separation.</span></span>

<span data-ttu-id="2d9a7-128">我们现在有组合的体验，其中可以安装、 更新或卸载无论你如何选择的包的包。</span><span class="sxs-lookup"><span data-stu-id="2d9a7-128">We now have a combined experience, where you can install, update, or uninstall a package regardless of how you got the package selected.</span></span> <span data-ttu-id="2d9a7-129">为了帮助的特定工作流，我们现在有筛选器下拉列表中，你可以筛选包可见，但适用于包的操作都是一致。</span><span class="sxs-lookup"><span data-stu-id="2d9a7-129">To assist with the specific workflows, we now have a Filter dropdown that lets you filter the packages visible, but then the actions available for the package are consistent.</span></span>

![卸载包](./media/NuGet-3.0-Preview/uninstall-package.png)

<span data-ttu-id="2d9a7-131">通过使用"已安装"筛选器，你就可以轻松看到哪些功能具有可用的更新，你已安装的程序包，然后你可以卸载或者通过更改版本选择以查看更新的包更改可用的操作。</span><span class="sxs-lookup"><span data-stu-id="2d9a7-131">By using the "Installed" filter, you can then easily see your installed packages, which ones have updates available, and then you can either uninstall or update the package by changing the version selection to see change the action available.</span></span>

![更新的包](./media/NuGet-3.0-Preview/update-package.png)

### <a name="version-consolidation"></a><span data-ttu-id="2d9a7-133">版本合并</span><span class="sxs-lookup"><span data-stu-id="2d9a7-133">Version Consolidation</span></span>

<span data-ttu-id="2d9a7-134">它很常见同一个包安装到您的解决方案内的多个项目。</span><span class="sxs-lookup"><span data-stu-id="2d9a7-134">It's common to have the same package installed into multiple projects within your solution.</span></span> <span data-ttu-id="2d9a7-135">有时安装到每个项目的版本可以偏离，并且有必要整合中使用的版本。</span><span class="sxs-lookup"><span data-stu-id="2d9a7-135">Sometimes the versions installed into each project can drift apart and it's necessary to consolidate the versions in use.</span></span> <span data-ttu-id="2d9a7-136">NuGet 3.0 Preview 引入了一个新功能，只是这种情况。</span><span class="sxs-lookup"><span data-stu-id="2d9a7-136">NuGet 3.0 Preview introduces a new feature for just this scenario.</span></span>

<span data-ttu-id="2d9a7-137">可以通过右键单击解决方案并选择管理解决方案的 NuGet 包访问解决方案级包管理窗口。</span><span class="sxs-lookup"><span data-stu-id="2d9a7-137">The solution-level package management window can be accessed by right-clicking on the solution and choosing Manage NuGet Packages for Solution.</span></span> <span data-ttu-id="2d9a7-138">在这里，如果您选择安装到多个项目，但使用不同版本中使用，包的新的"合并"操作可用。</span><span class="sxs-lookup"><span data-stu-id="2d9a7-138">From there, if you select a package that is installed into multiple projects, but with different versions in use, a new "Consolidate" action becomes available.</span></span> <span data-ttu-id="2d9a7-139">在以下屏幕截图，`Newtonsoft.Json`安装到`SamplesClassLibrary`版本`6.0.4`且已安装到`SamplesConsoleApp`版本`5.0.4`。</span><span class="sxs-lookup"><span data-stu-id="2d9a7-139">In the screen shot below, `Newtonsoft.Json` was installed into the `SamplesClassLibrary` with version `6.0.4` and installed into `SamplesConsoleApp` with version `5.0.4`.</span></span>

![合并版本](./media/NuGet-3.0-Preview/consolidate.png)

<span data-ttu-id="2d9a7-141">下面是将合并到单个版本的工作流。</span><span class="sxs-lookup"><span data-stu-id="2d9a7-141">Here's the workflow for consolidating onto a single version.</span></span>

1. <span data-ttu-id="2d9a7-142">选择`Newtonsoft.Json`列表中的包</span><span class="sxs-lookup"><span data-stu-id="2d9a7-142">Select the `Newtonsoft.Json` package in the list</span></span>
1. <span data-ttu-id="2d9a7-143">选择`Consolidate`从`Action`下拉列表中</span><span class="sxs-lookup"><span data-stu-id="2d9a7-143">Choose `Consolidate` from the `Action` dropdown</span></span>
1. <span data-ttu-id="2d9a7-144">使用`Version`下拉列表中选择要合并到的版本</span><span class="sxs-lookup"><span data-stu-id="2d9a7-144">Use the `Version` dropdown to select the version to be consolidated onto</span></span>
1. <span data-ttu-id="2d9a7-145">选中的复选框应整合到该版本 （请注意，已在所选版本的项目将灰显） 的项目</span><span class="sxs-lookup"><span data-stu-id="2d9a7-145">Check the boxes for the projects that should be consolidated onto that version (note that projects already on the selected version will be greyed out)</span></span>
1. <span data-ttu-id="2d9a7-146">单击`Consolidate`按钮来执行合并</span><span class="sxs-lookup"><span data-stu-id="2d9a7-146">Click the `Consolidate` button to perform the consolidation</span></span>

### <a name="operation-previews"></a><span data-ttu-id="2d9a7-147">操作预览</span><span class="sxs-lookup"><span data-stu-id="2d9a7-147">Operation Previews</span></span>

<span data-ttu-id="2d9a7-148">无论哪个操作当前正在执行-安装/更新/卸载-新的用户界面现在提供预览将向你的项目所做的更改的方法。</span><span class="sxs-lookup"><span data-stu-id="2d9a7-148">Regardless of which operation you're performing--install/update/uninstall--the new UI now offers a way to preview the changes that will be made to your project.</span></span> <span data-ttu-id="2d9a7-149">此预览版将显示的任何新包将安装包，将会更新，并且包将卸载，以及在操作期间将保持不变的包。</span><span class="sxs-lookup"><span data-stu-id="2d9a7-149">This preview will show any new packages that will be installed, packages that will be updated, and packages that will be uninstalled, along with packages that will be unchanged during the operation.</span></span>

<span data-ttu-id="2d9a7-150">在下面的示例中，我们可以看到，安装 Microsoft.AspNet.SignalR 将导致相当多的更改到项目。</span><span class="sxs-lookup"><span data-stu-id="2d9a7-150">In the example below, we can see that installing Microsoft.AspNet.SignalR will result in quite a few changes to the project.</span></span>

![安装 SignalR 的预览](./media/NuGet-3.0-Preview/preview.png)

### <a name="installation-options"></a><span data-ttu-id="2d9a7-152">安装选项</span><span class="sxs-lookup"><span data-stu-id="2d9a7-152">Installation Options</span></span>

<span data-ttu-id="2d9a7-153">使用 PowerShell 控制台，你已经有几个值得注意的安装选项控制。</span><span class="sxs-lookup"><span data-stu-id="2d9a7-153">Using the PowerShell Console, you've had control over a couple of notable installation options.</span></span> <span data-ttu-id="2d9a7-154">现在，我们已将这些功能也在 ui。</span><span class="sxs-lookup"><span data-stu-id="2d9a7-154">We've now brought those features into the UI as well.</span></span> <span data-ttu-id="2d9a7-155">你现可控制如何选择依赖项的版本的依赖项解析行为。</span><span class="sxs-lookup"><span data-stu-id="2d9a7-155">You can now control the dependency resolution behavior for how versions of the dependencies are selected.</span></span>

![依赖项行为](./media/NuGet-3.0-Preview/dependency-behavior.png)

<span data-ttu-id="2d9a7-157">你还可以指定当从包的内容文件与已在你的项目的文件发生冲突时要执行的操作。</span><span class="sxs-lookup"><span data-stu-id="2d9a7-157">You can also specify the action to take when content files from packages conflict with files already in your project.</span></span>

![文件冲突操作](./media/NuGet-3.0-Preview/file-conflict-action.png)

### <a name="infinite-scrolling"></a><span data-ttu-id="2d9a7-159">无限滚动</span><span class="sxs-lookup"><span data-stu-id="2d9a7-159">Infinite Scrolling</span></span>

<span data-ttu-id="2d9a7-160">我们用于获取很多有关我们的 UI 的反馈具有这两个滚动和分页范例，列出包时。</span><span class="sxs-lookup"><span data-stu-id="2d9a7-160">We used to get quite a bit of feedback on our UI having both the scrolling and paging paradigms when listing packages.</span></span> <span data-ttu-id="2d9a7-161">常见的做法是非常必须滚动到底部的短列表，请单击下一步的页号，然后再次然后向下滚动。</span><span class="sxs-lookup"><span data-stu-id="2d9a7-161">It was pretty common to have to scroll to the bottom of the short list, click the next page number, and then scroll again.</span></span> <span data-ttu-id="2d9a7-162">与新的 UI 中，我们已经实现无限滚动在包列表中，以便仅需要进行滚动-没有更多的分页。</span><span class="sxs-lookup"><span data-stu-id="2d9a7-162">With the new UI, we've implemented infinite scrolling in the package list so that you only need to scroll--no more paging.</span></span>

![无限滚动](./media/NuGet-3.0-Preview/infinite-scrolling.png)

### <a name="make-it-work-make-it-fast-make-it-pretty"></a><span data-ttu-id="2d9a7-164">使其工作，请使其快速，使其优质</span><span class="sxs-lookup"><span data-stu-id="2d9a7-164">Make it Work, Make it Fast, Make it Pretty</span></span>

<span data-ttu-id="2d9a7-165">我们很高兴获取此新的用户界面，供你试用。在此预览版的里程碑，我们已经遵循良好旧句箴言，而且的"使其工作，使其快速，使其非常。"</span><span class="sxs-lookup"><span data-stu-id="2d9a7-165">We are excited to get this new UI out for you to try out. During this Preview milestone, we've been following the good old adage of "Make it work, make it fast, make it pretty."</span></span> <span data-ttu-id="2d9a7-166">在此预览版中，我们已完成大多数的此第一个目标就其工作原理。</span><span class="sxs-lookup"><span data-stu-id="2d9a7-166">In this preview, we've accomplished most of that first goal--it works.</span></span> <span data-ttu-id="2d9a7-167">我们知道它不是相当快速尚未和我们知道它尚不可相当相当。</span><span class="sxs-lookup"><span data-stu-id="2d9a7-167">We know it's not quite fast yet, and we know it's not quite pretty yet.</span></span> <span data-ttu-id="2d9a7-168">我们会处理这些目标现在的 RC 版本之间的信任。</span><span class="sxs-lookup"><span data-stu-id="2d9a7-168">Trust that we'll be working on those goals between now and the RC release.</span></span> <span data-ttu-id="2d9a7-169">在此期间，我们很乐意倾听你的反馈有关*可用性*的新 UI-工作流、 操作，以及它*外观*以使用新的用户界面。</span><span class="sxs-lookup"><span data-stu-id="2d9a7-169">In the meantime, we would love to hear your feedback about the *usability* of the new UI--the workflows, operations, and how it *feels* to use the new UI.</span></span>

<span data-ttu-id="2d9a7-170">有几个我们将删除与旧 UI 相比的函数。</span><span class="sxs-lookup"><span data-stu-id="2d9a7-170">There are a couple of functions that we've removed when compared to the old UI.</span></span> <span data-ttu-id="2d9a7-171">以下方法之一是特意的和另一个只是未在时间内完成。</span><span class="sxs-lookup"><span data-stu-id="2d9a7-171">One of these was intentional, and the other one just didn't get done in time.</span></span>

#### <a name="searching-all-package-sources"></a><span data-ttu-id="2d9a7-172">搜索的"所有"包源</span><span class="sxs-lookup"><span data-stu-id="2d9a7-172">Searching "All" Package Sources</span></span>

<span data-ttu-id="2d9a7-173">旧 UI 允许你执行针对你的包源的所有包的搜索。</span><span class="sxs-lookup"><span data-stu-id="2d9a7-173">The old UI allowed you to perform a package search against all of your package sources.</span></span> <span data-ttu-id="2d9a7-174">我们在 UI 中将删除该功能，我们将不会使其返回。</span><span class="sxs-lookup"><span data-stu-id="2d9a7-174">We've removed that feature in the UI and we won't be bringing it back.</span></span> <span data-ttu-id="2d9a7-175">用于执行搜索操作针对所有包源，此功能 weave 配合使用，结果在一起，并尝试根据排序的选择对结果进行排序。</span><span class="sxs-lookup"><span data-stu-id="2d9a7-175">This feature used to perform search operations against all of your package sources, weave the results together, and attempt to order the results based on your sorting selection.</span></span>

<span data-ttu-id="2d9a7-176">我们找到搜索相关性很难 weave 配合使用，在一起。</span><span class="sxs-lookup"><span data-stu-id="2d9a7-176">We found that search relevance is really hard to weave together.</span></span> <span data-ttu-id="2d9a7-177">可以想象得到执行针对 Google 和必应搜索，并在一起种结果编制方法？</span><span class="sxs-lookup"><span data-stu-id="2d9a7-177">Could you imagine performing a search against Google and Bing and weaving the results together?</span></span> <span data-ttu-id="2d9a7-178">此外，此功能已速度慢、 易于*意外*使用和我们认为它是很少确实有用。</span><span class="sxs-lookup"><span data-stu-id="2d9a7-178">Additionally, this feature was slow, easy to *accidentally* use, and we believe it was rarely actually useful.</span></span> <span data-ttu-id="2d9a7-179">由于问题中引入的功能我们已收到大量的无法从不已修复的 bug 报告在其上。</span><span class="sxs-lookup"><span data-stu-id="2d9a7-179">Because of the problems the feature introduced, we received a number of bug reports on it that could never have been fixed.</span></span>

#### <a name="update-all"></a><span data-ttu-id="2d9a7-180">更新所有</span><span class="sxs-lookup"><span data-stu-id="2d9a7-180">Update All</span></span>

<span data-ttu-id="2d9a7-181">我们用于旧 ui 中不存在新的用户界面中尚未具有一个"全部更新"按钮。</span><span class="sxs-lookup"><span data-stu-id="2d9a7-181">We used to have an "Update All" button in the old UI that isn't there in the new UI yet.</span></span> <span data-ttu-id="2d9a7-182">我们将使此功能重新起用对于我们的 RC 版本。</span><span class="sxs-lookup"><span data-stu-id="2d9a7-182">We will resurrect this feature for our RC release.</span></span>

## <a name="new-clientserver-api"></a><span data-ttu-id="2d9a7-183">新的客户端/服务器 API</span><span class="sxs-lookup"><span data-stu-id="2d9a7-183">New Client/Server API</span></span>

<span data-ttu-id="2d9a7-184">除了所有我们新的程序包管理 UI 中的新功能，我们还整理 NuGet 的客户端/服务器协议某些实现详细信息。</span><span class="sxs-lookup"><span data-stu-id="2d9a7-184">In addition to all of the new features in our new package management UI, we've also been working on some implementation details for NuGet's client/server protocol.</span></span> <span data-ttu-id="2d9a7-185">我们已完成的工作是创建"API v3"nuget，围绕关键方案，如程序包还原和安装包的高可用性而设计。</span><span class="sxs-lookup"><span data-stu-id="2d9a7-185">The work we've done is to create "API v3" for NuGet, which is designed around high availability for critical scenarios such as package restore and installing packages.</span></span> <span data-ttu-id="2d9a7-186">新的 API 基于 REST 并且超媒体，我们已选择[JSON LD](http://json-ld.org)作为我们资源格式。</span><span class="sxs-lookup"><span data-stu-id="2d9a7-186">The new API is based on REST and Hypermedia and we've selected [JSON-LD](http://json-ld.org) as our resource format.</span></span>

<span data-ttu-id="2d9a7-187">以 NuGet 3.0 预览位为单位，你将看到在程序包源下拉列表中称为"preview.nuget.org"的新包源。</span><span class="sxs-lookup"><span data-stu-id="2d9a7-187">In the NuGet 3.0 Preview bits, you'll see a new package source called "preview.nuget.org" in the package source dropdown.</span></span> <span data-ttu-id="2d9a7-188">如果你选择该包源，我们将使用我们新的 API 而是要连接到 nuget.org。我们继续测试、 修订和提高新的 API 时，我们已简化预览源在 UI 中可用。</span><span class="sxs-lookup"><span data-stu-id="2d9a7-188">If you select that package source, we'll use our new API rather to connect to nuget.org. We've made the preview source available in the UI while we continue to test, revise, and improve the new API.</span></span> <span data-ttu-id="2d9a7-189">在 NuGet 3.0 RC 中，此新的 API 基于 v3 的包源将替换 v2 基于"nuget.org"包源。</span><span class="sxs-lookup"><span data-stu-id="2d9a7-189">In NuGet 3.0 RC, this new API v3-based package source will replace the v2-based "nuget.org" package source.</span></span>

<span data-ttu-id="2d9a7-190">尽管我们正在将放入 API v3 的投资，我们进行了所有这些新功能与我们现有的 API v2 协议，这意味着它们将使用 nuget.org 以及以外的现有包源一同使用。</span><span class="sxs-lookup"><span data-stu-id="2d9a7-190">Despite the investment we're putting into API v3, we've made all of these new features also work with our existing API v2 protocol, which means they will work with existing package sources other than nuget.org as well.</span></span>

## <a name="new-features-coming"></a><span data-ttu-id="2d9a7-191">新的多功能即将推出</span><span class="sxs-lookup"><span data-stu-id="2d9a7-191">New Features Coming</span></span>

<span data-ttu-id="2d9a7-192">现在，3.0 RTM，我们还致力于一些基本 NuGet 之外新功能，将在 UI 中看到的内容。</span><span class="sxs-lookup"><span data-stu-id="2d9a7-192">Between now and 3.0 RTM, we are also working on some fundamental new NuGet features, beyond what you'll see in the UI.</span></span> <span data-ttu-id="2d9a7-193">下面是一个突出投资领域的简短列表：</span><span class="sxs-lookup"><span data-stu-id="2d9a7-193">Here's a short list of salient investment areas:</span></span>

1. <span data-ttu-id="2d9a7-194">我们正在合作使用 Visual Studio 和 MSBuild 团队以获取[NuGet 深入到平台](http://blog.nuget.org/20141014/in-the-platform.html)。</span><span class="sxs-lookup"><span data-stu-id="2d9a7-194">We're partnering with the Visual Studio and MSBuild teams to get [NuGet deeper into the platform](http://blog.nuget.org/20141014/in-the-platform.html).</span></span>
1. <span data-ttu-id="2d9a7-195">我们正在努力放弃安装时间包约定并改为在打包时应用这些约定，通过引入了一个新"具有权威"[包清单](http://blog.nuget.org/20141023/package-manifests.html)。</span><span class="sxs-lookup"><span data-stu-id="2d9a7-195">We're working to abandon installation-time package conventions and instead apply those conventions at packaging time by introducing a new "authoritative" [package manifest](http://blog.nuget.org/20141023/package-manifests.html).</span></span>
1. <span data-ttu-id="2d9a7-196">我们正在努力 NuGet 基本代码，以使局限于 Visual Studio 中的包管理的不同域中的客户端和服务器组件可重用的重构。</span><span class="sxs-lookup"><span data-stu-id="2d9a7-196">We're working to refactor the NuGet codebase to make the client and server components reusable in different domains beyond package management in Visual Studio.</span></span>
1. <span data-ttu-id="2d9a7-197">我们正在调查的概念"专用依赖关系"其中一个包可以指示它是实现详细信息仅，其他包上具有依赖关系，这些依赖关系不应显示为顶级依赖项。</span><span class="sxs-lookup"><span data-stu-id="2d9a7-197">We're investigating the notion of "private dependencies" where a package can indicate that it has dependencies on other packages for implementation details only, and those dependencies shouldn't be surfaced as top-level dependencies.</span></span>

## <a name="stay-tuned"></a><span data-ttu-id="2d9a7-198">请继续关注</span><span class="sxs-lookup"><span data-stu-id="2d9a7-198">Stay Tuned</span></span>

<span data-ttu-id="2d9a7-199">请留意[我们的博客](http://blog.nuget.org)了解详细的进度和公告 NuGet 3.0 ！</span><span class="sxs-lookup"><span data-stu-id="2d9a7-199">Please keep an eye on [our blog](http://blog.nuget.org) for more progress and announcements for NuGet 3.0!</span></span>