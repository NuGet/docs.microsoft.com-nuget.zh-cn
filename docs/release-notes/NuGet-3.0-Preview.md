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
# <a name="nuget-30-preview-release-notes"></a><span data-ttu-id="0b085-103">NuGet 3.0 预览版发行说明</span><span class="sxs-lookup"><span data-stu-id="0b085-103">NuGet 3.0 Preview Release Notes</span></span>

<span data-ttu-id="0b085-104">[NuGet 2.9 RC 发行说明](../release-notes/nuget-2.9-rc.md) | [NuGet 3.0 测试版发行说明](../release-notes/nuget-3.0-beta.md)</span><span class="sxs-lookup"><span data-stu-id="0b085-104">[NuGet 2.9 RC Release Notes](../release-notes/nuget-2.9-rc.md) | [NuGet 3.0 Beta Release Notes](../release-notes/nuget-3.0-beta.md)</span></span>

<span data-ttu-id="0b085-105">NuGet 3.0 预览版发布于 2014 年 11 月 12 日作为 Visual Studio 2015 预览版发布的一部分。</span><span class="sxs-lookup"><span data-stu-id="0b085-105">NuGet 3.0 Preview was released on November 12, 2014 as part of the Visual Studio 2015 Preview release.</span></span> <span data-ttu-id="0b085-106">我们发布了 NuGet 3.0 预览版。</span><span class="sxs-lookup"><span data-stu-id="0b085-106">We released NuGet 3.0 Preview.</span></span> <span data-ttu-id="0b085-107">这是对我们很重要的版本 （尽管预览版），和我们高兴地开始获取反馈，我们更改。</span><span class="sxs-lookup"><span data-stu-id="0b085-107">This is a big release for us (albeit a preview), and we're excited to start getting feedback on our changes.</span></span>

## <a name="visual-studio-2012"></a><span data-ttu-id="0b085-108">Visual Studio 2012 和更高</span><span class="sxs-lookup"><span data-stu-id="0b085-108">Visual Studio 2012+</span></span>

<span data-ttu-id="0b085-109">此 NuGet 3.0 预览版包括在 Visual Studio 2015 预览版中。</span><span class="sxs-lookup"><span data-stu-id="0b085-109">This NuGet 3.0 Preview is included in Visual Studio 2015 Preview.</span></span> <span data-ttu-id="0b085-110">我们正在努力推出预览版删除 Visual Studio 2012 和 Visual Studio 2013 很快。</span><span class="sxs-lookup"><span data-stu-id="0b085-110">We are working to get preview drops out for Visual Studio 2012 and Visual Studio 2013 very soon.</span></span> <span data-ttu-id="0b085-111">我们以前共享到我们的意图[停止更新适用于 Visual Studio 2010](http://blog.nuget.org/20141002/visual-studio-2010.html)，和我们未做出难以决定。</span><span class="sxs-lookup"><span data-stu-id="0b085-111">We previously shared our intent to [discontinue updates for Visual Studio 2010](http://blog.nuget.org/20141002/visual-studio-2010.html), and we did make that difficult decision.</span></span>

## <a name="brand-new-ui"></a><span data-ttu-id="0b085-112">全新的 UI</span><span class="sxs-lookup"><span data-stu-id="0b085-112">Brand New UI</span></span>

<span data-ttu-id="0b085-113">你注意到有关 NuGet 3.0 Preview 的第一件事是我们全新的 UI。</span><span class="sxs-lookup"><span data-stu-id="0b085-113">The first thing you notice about NuGet 3.0 Preview is our brand new UI.</span></span> <span data-ttu-id="0b085-114">它不再是一个模式对话框;它现在是一个完整的 Visual Studio 文档窗口。</span><span class="sxs-lookup"><span data-stu-id="0b085-114">It's no longer a modal dialog; it's now a full Visual Studio document window.</span></span> <span data-ttu-id="0b085-115">这允许你在一次打开多个项目 （和/或解决方案） 的 UI，拉出到另一个监视器窗口中，将其固定，但您会喜欢，等等。</span><span class="sxs-lookup"><span data-stu-id="0b085-115">This allows you to open the UI for multiple projects (and/or the solution) at once, tear the window off to another monitor, dock it however you'd like, etc.</span></span>

![新的 NuGet UI](./media/NuGet-3.0-Preview/new-ui.png)

<span data-ttu-id="0b085-117">除了可用性差异由于放弃模式对话框中，我们还在新 UI 有很多新功能。</span><span class="sxs-lookup"><span data-stu-id="0b085-117">Beyond the usability differences because of abandoning the modal dialog, we also have lots of new features in the new UI.</span></span>

### <a name="version-selection"></a><span data-ttu-id="0b085-118">版本选择</span><span class="sxs-lookup"><span data-stu-id="0b085-118">Version Selection</span></span>

<span data-ttu-id="0b085-119">可能是最常请求的 UI 功能是允许版本选择的包的安装和更新-此功能现提供。</span><span class="sxs-lookup"><span data-stu-id="0b085-119">Perhaps the most requested UI feature is to allow version selection for package installation and update--this is now available.</span></span>

![包版本选择](./media/NuGet-3.0-Preview/version-selection.png)

<span data-ttu-id="0b085-121">无论您是安装还是更新包，版本下拉列表中，可查看所有与提升轻松选择列表的顶部为一些值得注意版本可用于包的版本。</span><span class="sxs-lookup"><span data-stu-id="0b085-121">Whether you are installing or updating a package, the version dropdown allows you to see all of the versions available for the package, with some notable versions promoted to the top of the list for easy selection.</span></span> <span data-ttu-id="0b085-122">不再需要使用 PowerShell 控制台来获取不是最新的特定版本。</span><span class="sxs-lookup"><span data-stu-id="0b085-122">You no longer need to use the PowerShell Console to get specific versions that are not the latest.</span></span>

### <a name="combined-installedonlineupdates-workflows"></a><span data-ttu-id="0b085-123">合并已安装/联机/更新工作流</span><span class="sxs-lookup"><span data-stu-id="0b085-123">Combined Installed/Online/Updates Workflows</span></span>

<span data-ttu-id="0b085-124">我们以前的 UI 更新已安装，联机，以及有 3 个选项卡。</span><span class="sxs-lookup"><span data-stu-id="0b085-124">Our previous UI had 3 tabs for Installed, Online, and Updates.</span></span> <span data-ttu-id="0b085-125">列出的包是特定于这些工作流，并且特定于工作流以及可用的操作。</span><span class="sxs-lookup"><span data-stu-id="0b085-125">The packages listed were specific to those workflows and the actions available were specific to the workflows as well.</span></span> <span data-ttu-id="0b085-126">虽然这看起来逻辑，我们听说过很多人通常会获取掣肘： 这种分离。</span><span class="sxs-lookup"><span data-stu-id="0b085-126">While that seemed logical, we heard that many of you would often get tripped up by this separation.</span></span>

<span data-ttu-id="0b085-127">现在，我们有组合的体验，可以在其中安装、 更新或卸载包而不考虑如何达到选择的包。</span><span class="sxs-lookup"><span data-stu-id="0b085-127">We now have a combined experience, where you can install, update, or uninstall a package regardless of how you got the package selected.</span></span> <span data-ttu-id="0b085-128">为了帮助与特定工作流，我们现在有一个筛选器下拉列表，可以筛选包可见，但然后可用包的操作保持一致。</span><span class="sxs-lookup"><span data-stu-id="0b085-128">To assist with the specific workflows, we now have a Filter dropdown that lets you filter the packages visible, but then the actions available for the package are consistent.</span></span>

![卸载包](./media/NuGet-3.0-Preview/uninstall-package.png)

<span data-ttu-id="0b085-130">通过使用"已安装"筛选器，然后，您可以轻松地看到哪些功能具有可用的更新，你已安装的包，然后你可以卸载或更改版本选择以查看更新包更改可用的操作。</span><span class="sxs-lookup"><span data-stu-id="0b085-130">By using the "Installed" filter, you can then easily see your installed packages, which ones have updates available, and then you can either uninstall or update the package by changing the version selection to see change the action available.</span></span>

![更新的包](./media/NuGet-3.0-Preview/update-package.png)

### <a name="version-consolidation"></a><span data-ttu-id="0b085-132">版本合并</span><span class="sxs-lookup"><span data-stu-id="0b085-132">Version Consolidation</span></span>

<span data-ttu-id="0b085-133">它是常见的同一个包安装到您的解决方案内的多个项目。</span><span class="sxs-lookup"><span data-stu-id="0b085-133">It's common to have the same package installed into multiple projects within your solution.</span></span> <span data-ttu-id="0b085-134">有时安装到每个项目的版本可以偏离和需要合并中使用的版本。</span><span class="sxs-lookup"><span data-stu-id="0b085-134">Sometimes the versions installed into each project can drift apart and it's necessary to consolidate the versions in use.</span></span> <span data-ttu-id="0b085-135">NuGet 3.0 Preview 引入了新功能，可解决此类问题。</span><span class="sxs-lookup"><span data-stu-id="0b085-135">NuGet 3.0 Preview introduces a new feature for just this scenario.</span></span>

<span data-ttu-id="0b085-136">可以通过右键单击解决方案并选择为解决方案管理 NuGet 包访问解决方案级包管理窗口。</span><span class="sxs-lookup"><span data-stu-id="0b085-136">The solution-level package management window can be accessed by right-clicking on the solution and choosing Manage NuGet Packages for Solution.</span></span> <span data-ttu-id="0b085-137">在这里，如果您选择安装到多个项目，但在使用中，不同版本的包的新的"合并"操作将变为可用。</span><span class="sxs-lookup"><span data-stu-id="0b085-137">From there, if you select a package that is installed into multiple projects, but with different versions in use, a new "Consolidate" action becomes available.</span></span> <span data-ttu-id="0b085-138">在以下屏幕截图，`Newtonsoft.Json`安装到`SamplesClassLibrary`版本`6.0.4`且已安装到`SamplesConsoleApp`版本`5.0.4`。</span><span class="sxs-lookup"><span data-stu-id="0b085-138">In the screen shot below, `Newtonsoft.Json` was installed into the `SamplesClassLibrary` with version `6.0.4` and installed into `SamplesConsoleApp` with version `5.0.4`.</span></span>

![合并版本](./media/NuGet-3.0-Preview/consolidate.png)

<span data-ttu-id="0b085-140">下面是将合并到单个版本上的工作流。</span><span class="sxs-lookup"><span data-stu-id="0b085-140">Here's the workflow for consolidating onto a single version.</span></span>

1. <span data-ttu-id="0b085-141">选择`Newtonsoft.Json`列表中的包</span><span class="sxs-lookup"><span data-stu-id="0b085-141">Select the `Newtonsoft.Json` package in the list</span></span>
1. <span data-ttu-id="0b085-142">选择`Consolidate`从`Action`下拉列表中</span><span class="sxs-lookup"><span data-stu-id="0b085-142">Choose `Consolidate` from the `Action` dropdown</span></span>
1. <span data-ttu-id="0b085-143">使用`Version`下拉列表中选择要合并到的版本</span><span class="sxs-lookup"><span data-stu-id="0b085-143">Use the `Version` dropdown to select the version to be consolidated onto</span></span>
1. <span data-ttu-id="0b085-144">选中的复选框应合并到该版本 （请注意，已在所选的版本上的项目将灰显） 的项目</span><span class="sxs-lookup"><span data-stu-id="0b085-144">Check the boxes for the projects that should be consolidated onto that version (note that projects already on the selected version will be greyed out)</span></span>
1. <span data-ttu-id="0b085-145">单击`Consolidate`按钮以执行合并</span><span class="sxs-lookup"><span data-stu-id="0b085-145">Click the `Consolidate` button to perform the consolidation</span></span>

### <a name="operation-previews"></a><span data-ttu-id="0b085-146">操作预览</span><span class="sxs-lookup"><span data-stu-id="0b085-146">Operation Previews</span></span>

<span data-ttu-id="0b085-147">无论哪个操作在执行-安装/更新/卸载-新用户界面现在提供了一种方法，若要预览将会对项目所做的更改。</span><span class="sxs-lookup"><span data-stu-id="0b085-147">Regardless of which operation you're performing--install/update/uninstall--the new UI now offers a way to preview the changes that will be made to your project.</span></span> <span data-ttu-id="0b085-148">此预览会显示任何新的包将安装包，将被更新，并且包将被卸载，以及在操作期间将保持不变的包。</span><span class="sxs-lookup"><span data-stu-id="0b085-148">This preview will show any new packages that will be installed, packages that will be updated, and packages that will be uninstalled, along with packages that will be unchanged during the operation.</span></span>

<span data-ttu-id="0b085-149">在下面的示例中，我们可以看到，安装 Microsoft.AspNet.SignalR 会导致相当多的更改到项目。</span><span class="sxs-lookup"><span data-stu-id="0b085-149">In the example below, we can see that installing Microsoft.AspNet.SignalR will result in quite a few changes to the project.</span></span>

![预览版安装 SignalR](./media/NuGet-3.0-Preview/preview.png)

### <a name="installation-options"></a><span data-ttu-id="0b085-151">安装选项</span><span class="sxs-lookup"><span data-stu-id="0b085-151">Installation Options</span></span>

<span data-ttu-id="0b085-152">使用 PowerShell 控制台，在过去的几个值得注意的安装选项控制。</span><span class="sxs-lookup"><span data-stu-id="0b085-152">Using the PowerShell Console, you've had control over a couple of notable installation options.</span></span> <span data-ttu-id="0b085-153">现在，我们已引入 UI 还将这些功能。</span><span class="sxs-lookup"><span data-stu-id="0b085-153">We've now brought those features into the UI as well.</span></span> <span data-ttu-id="0b085-154">现在可以控制如何选择版本的依赖项的依赖关系解析行为。</span><span class="sxs-lookup"><span data-stu-id="0b085-154">You can now control the dependency resolution behavior for how versions of the dependencies are selected.</span></span>

![依赖关系行为](./media/NuGet-3.0-Preview/dependency-behavior.png)

<span data-ttu-id="0b085-156">此外可以指定当包中的内容文件与你的项目中的现有文件冲突时要执行的操作。</span><span class="sxs-lookup"><span data-stu-id="0b085-156">You can also specify the action to take when content files from packages conflict with files already in your project.</span></span>

![文件冲突操作](./media/NuGet-3.0-Preview/file-conflict-action.png)

### <a name="infinite-scrolling"></a><span data-ttu-id="0b085-158">无限滚动</span><span class="sxs-lookup"><span data-stu-id="0b085-158">Infinite Scrolling</span></span>

<span data-ttu-id="0b085-159">我们用于获取大量的反馈对我们的 UI 具有这两个滚动和列出的包时分页模式。</span><span class="sxs-lookup"><span data-stu-id="0b085-159">We used to get quite a bit of feedback on our UI having both the scrolling and paging paradigms when listing packages.</span></span> <span data-ttu-id="0b085-160">这是相当常见的要滚动到底部的短列表，请单击下一步的页码，再然后向下滚动。</span><span class="sxs-lookup"><span data-stu-id="0b085-160">It was pretty common to have to scroll to the bottom of the short list, click the next page number, and then scroll again.</span></span> <span data-ttu-id="0b085-161">使用新的用户界面，我们已实现无限滚动包列表中，以便只需要进行滚动-没有更多的分页。</span><span class="sxs-lookup"><span data-stu-id="0b085-161">With the new UI, we've implemented infinite scrolling in the package list so that you only need to scroll--no more paging.</span></span>

![无限滚动](./media/NuGet-3.0-Preview/infinite-scrolling.png)

### <a name="make-it-work-make-it-fast-make-it-pretty"></a><span data-ttu-id="0b085-163">使其工作，使其快速，使其美观</span><span class="sxs-lookup"><span data-stu-id="0b085-163">Make it Work, Make it Fast, Make it Pretty</span></span>

<span data-ttu-id="0b085-164">我们很高兴为您尝试推出此新 UI。在此预览阶段，我们已经遵循良好老话"使其工作，使其快速、 使其美观。"</span><span class="sxs-lookup"><span data-stu-id="0b085-164">We are excited to get this new UI out for you to try out. During this Preview milestone, we've been following the good old adage of "Make it work, make it fast, make it pretty."</span></span> <span data-ttu-id="0b085-165">在此预览版中，我们已完成大多数的这个第一个目标-其工作原理。</span><span class="sxs-lookup"><span data-stu-id="0b085-165">In this preview, we've accomplished most of that first goal--it works.</span></span> <span data-ttu-id="0b085-166">我们知道它非常快速还不是，我们知道它非常非常还不是。</span><span class="sxs-lookup"><span data-stu-id="0b085-166">We know it's not quite fast yet, and we know it's not quite pretty yet.</span></span> <span data-ttu-id="0b085-167">我们将使用这些目标现在和 RC 版本之间的信任。</span><span class="sxs-lookup"><span data-stu-id="0b085-167">Trust that we'll be working on those goals between now and the RC release.</span></span> <span data-ttu-id="0b085-168">在此期间，我们期待倾听您的反馈意见*可用性*的新 UI-工作流、 操作、 以及如何它*感觉*以使用新的用户界面。</span><span class="sxs-lookup"><span data-stu-id="0b085-168">In the meantime, we would love to hear your feedback about the *usability* of the new UI--the workflows, operations, and how it *feels* to use the new UI.</span></span>

<span data-ttu-id="0b085-169">有几个我们将删除与旧 UI 相比的函数。</span><span class="sxs-lookup"><span data-stu-id="0b085-169">There are a couple of functions that we've removed when compared to the old UI.</span></span> <span data-ttu-id="0b085-170">其中一种是特意的和另一个只是未完成的时间。</span><span class="sxs-lookup"><span data-stu-id="0b085-170">One of these was intentional, and the other one just didn't get done in time.</span></span>

#### <a name="searching-all-package-sources"></a><span data-ttu-id="0b085-171">搜索"所有"包源</span><span class="sxs-lookup"><span data-stu-id="0b085-171">Searching "All" Package Sources</span></span>

<span data-ttu-id="0b085-172">旧 UI 允许您执行针对包源的所有包的搜索。</span><span class="sxs-lookup"><span data-stu-id="0b085-172">The old UI allowed you to perform a package search against all of your package sources.</span></span> <span data-ttu-id="0b085-173">我们在 UI 中删除了该功能，我们将不会将其返回。</span><span class="sxs-lookup"><span data-stu-id="0b085-173">We've removed that feature in the UI and we won't be bringing it back.</span></span> <span data-ttu-id="0b085-174">此功能，用于执行搜索操作针对所有包源，归纳到一起，，结果，然后尝试基于排序所选对结果进行排序。</span><span class="sxs-lookup"><span data-stu-id="0b085-174">This feature used to perform search operations against all of your package sources, weave the results together, and attempt to order the results based on your sorting selection.</span></span>

<span data-ttu-id="0b085-175">我们发现很难归纳到一起，搜索相关性。</span><span class="sxs-lookup"><span data-stu-id="0b085-175">We found that search relevance is really hard to weave together.</span></span> <span data-ttu-id="0b085-176">可以想象得到执行针对 Google 和必应搜索，以及一起编辑结果？</span><span class="sxs-lookup"><span data-stu-id="0b085-176">Could you imagine performing a search against Google and Bing and weaving the results together?</span></span> <span data-ttu-id="0b085-177">此外，此功能是速度较慢且易于*意外*使用和我们认为它很少实际上非常有用。</span><span class="sxs-lookup"><span data-stu-id="0b085-177">Additionally, this feature was slow, easy to *accidentally* use, and we believe it was rarely actually useful.</span></span> <span data-ttu-id="0b085-178">由于问题的功能中引入，我们收到数可能永远不会得到了修复的 bug 报告在其上。</span><span class="sxs-lookup"><span data-stu-id="0b085-178">Because of the problems the feature introduced, we received a number of bug reports on it that could never have been fixed.</span></span>

#### <a name="update-all"></a><span data-ttu-id="0b085-179">全部更新</span><span class="sxs-lookup"><span data-stu-id="0b085-179">Update All</span></span>

<span data-ttu-id="0b085-180">我们使用旧 ui 中有新的用户界面中尚不具有"更新全部"按钮。</span><span class="sxs-lookup"><span data-stu-id="0b085-180">We used to have an "Update All" button in the old UI that isn't there in the new UI yet.</span></span> <span data-ttu-id="0b085-181">我们将于我们的 RC 版本恢复此功能。</span><span class="sxs-lookup"><span data-stu-id="0b085-181">We will resurrect this feature for our RC release.</span></span>

## <a name="new-clientserver-api"></a><span data-ttu-id="0b085-182">新的客户端/服务器 API</span><span class="sxs-lookup"><span data-stu-id="0b085-182">New Client/Server API</span></span>

<span data-ttu-id="0b085-183">除了所有我们新的包管理 UI 中的新功能，我们也一直在 NuGet 的客户端/服务器协议一些实现细节。</span><span class="sxs-lookup"><span data-stu-id="0b085-183">In addition to all of the new features in our new package management UI, we've also been working on some implementation details for NuGet's client/server protocol.</span></span> <span data-ttu-id="0b085-184">我们所做的工作是为 NuGet，专为高可用性的关键方案，例如包还原和安装包创建"API v3"。</span><span class="sxs-lookup"><span data-stu-id="0b085-184">The work we've done is to create "API v3" for NuGet, which is designed around high availability for critical scenarios such as package restore and installing packages.</span></span> <span data-ttu-id="0b085-185">新的 API 基于 REST 和超媒体和我们所选[JSON-LD](http://json-ld.org)作为我们的资源格式。</span><span class="sxs-lookup"><span data-stu-id="0b085-185">The new API is based on REST and Hypermedia and we've selected [JSON-LD](http://json-ld.org) as our resource format.</span></span>

<span data-ttu-id="0b085-186">在 NuGet 3.0 预览版位中，可以看到称为"preview.nuget.org"包源下拉列表中的新包源。</span><span class="sxs-lookup"><span data-stu-id="0b085-186">In the NuGet 3.0 Preview bits, you see a new package source called "preview.nuget.org" in the package source dropdown.</span></span> <span data-ttu-id="0b085-187">如果您选择的包源，我们将使用我们的新 API，而是要连接到 nuget.org。我们继续测试、 修订和改进的新 API 时，我们已使预览源 UI 中提供。</span><span class="sxs-lookup"><span data-stu-id="0b085-187">If you select that package source, we'll use our new API rather to connect to nuget.org. We've made the preview source available in the UI while we continue to test, revise, and improve the new API.</span></span> <span data-ttu-id="0b085-188">在 NuGet 3.0 RC 中，此新 API 基于 v3 的包源将替换基于 v2"nuget.org"包源。</span><span class="sxs-lookup"><span data-stu-id="0b085-188">In NuGet 3.0 RC, this new API v3-based package source will replace the v2-based "nuget.org" package source.</span></span>

<span data-ttu-id="0b085-189">尽管我们正在将它们放入 API v3 的投资，我们已使所有这些新功能也适用于我们现有的 API v2 协议，这意味着它们将与现有以外还 nuget.org 的包源。</span><span class="sxs-lookup"><span data-stu-id="0b085-189">Despite the investment we're putting into API v3, we've made all of these new features also work with our existing API v2 protocol, which means they will work with existing package sources other than nuget.org as well.</span></span>

## <a name="new-features-coming"></a><span data-ttu-id="0b085-190">新功能</span><span class="sxs-lookup"><span data-stu-id="0b085-190">New Features Coming</span></span>

<span data-ttu-id="0b085-191">从现在到 3.0 的 RTM，我们还致力于一些基本之外的新 NuGet 功能，在 UI 中看到的内容。</span><span class="sxs-lookup"><span data-stu-id="0b085-191">Between now and 3.0 RTM, we are also working on some fundamental new NuGet features, beyond what you see in the UI.</span></span> <span data-ttu-id="0b085-192">下面是一个重要投资领域的简短列表：</span><span class="sxs-lookup"><span data-stu-id="0b085-192">Here's a short list of salient investment areas:</span></span>

1. <span data-ttu-id="0b085-193">我们正与 Visual Studio 合作，并由 MSBuild 团队以获取[深入到该平台的 NuGet](http://blog.nuget.org/20141014/in-the-platform.html)。</span><span class="sxs-lookup"><span data-stu-id="0b085-193">We're partnering with the Visual Studio and MSBuild teams to get [NuGet deeper into the platform](http://blog.nuget.org/20141014/in-the-platform.html).</span></span>
1. <span data-ttu-id="0b085-194">我们正在放弃安装时包约定，然后改为在打包时应用这些约定，通过引入一个新"权威"[包清单](http://blog.nuget.org/20141023/package-manifests.html)。</span><span class="sxs-lookup"><span data-stu-id="0b085-194">We're working to abandon installation-time package conventions and instead apply those conventions at packaging time by introducing a new "authoritative" [package manifest](http://blog.nuget.org/20141023/package-manifests.html).</span></span>
1. <span data-ttu-id="0b085-195">我们正在努力 NuGet 基本代码，以使 Visual Studio 中的包管理范围之外的不同域中的客户端和服务器组件可重用的重构。</span><span class="sxs-lookup"><span data-stu-id="0b085-195">We're working to refactor the NuGet codebase to make the client and server components reusable in different domains beyond package management in Visual Studio.</span></span>
1. <span data-ttu-id="0b085-196">我们正在研究的"专用依赖项"其中一个包可以指示它概念实现详细信息，其他包上具有依赖关系，这些依赖项不应显示为顶级依赖项。</span><span class="sxs-lookup"><span data-stu-id="0b085-196">We're investigating the notion of "private dependencies" where a package can indicate that it has dependencies on other packages for implementation details only, and those dependencies shouldn't be surfaced as top-level dependencies.</span></span>

## <a name="stay-tuned"></a><span data-ttu-id="0b085-197">请继续关注</span><span class="sxs-lookup"><span data-stu-id="0b085-197">Stay Tuned</span></span>

<span data-ttu-id="0b085-198">请密切关注[我们的博客](http://blog.nuget.org)详细进度和 NuGet 3.0 的公告 ！</span><span class="sxs-lookup"><span data-stu-id="0b085-198">Please keep an eye on [our blog](http://blog.nuget.org) for more progress and announcements for NuGet 3.0!</span></span>