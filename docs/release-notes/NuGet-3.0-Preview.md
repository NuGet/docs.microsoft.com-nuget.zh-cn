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
# <a name="nuget-30-preview-release-notes"></a><span data-ttu-id="6b322-103">NuGet 3.0 预览版发行说明</span><span class="sxs-lookup"><span data-stu-id="6b322-103">NuGet 3.0 Preview Release Notes</span></span>

<span data-ttu-id="6b322-104">[NuGet 2.9 RC 发行说明](../release-notes/nuget-2.9-rc.md)  | [NuGet 3.0 Beta 发行说明](../release-notes/nuget-3.0-beta.md)</span><span class="sxs-lookup"><span data-stu-id="6b322-104">[NuGet 2.9 RC Release Notes](../release-notes/nuget-2.9-rc.md) | [NuGet 3.0 Beta Release Notes](../release-notes/nuget-3.0-beta.md)</span></span>

<span data-ttu-id="6b322-105">在 Visual Studio 2015 预览版中，NuGet 3.0 预览版于2014年11月12日发布。</span><span class="sxs-lookup"><span data-stu-id="6b322-105">NuGet 3.0 Preview was released on November 12, 2014 as part of the Visual Studio 2015 Preview release.</span></span> <span data-ttu-id="6b322-106">我们发布了 NuGet 3.0 预览版。</span><span class="sxs-lookup"><span data-stu-id="6b322-106">We released NuGet 3.0 Preview.</span></span> <span data-ttu-id="6b322-107">这是一个很大的版本，我们 (虽然预览) ，但我们很高兴开始收到有关我们所做的更改的反馈。</span><span class="sxs-lookup"><span data-stu-id="6b322-107">This is a big release for us (albeit a preview), and we're excited to start getting feedback on our changes.</span></span>

## <a name="visual-studio-2012"></a><span data-ttu-id="6b322-108">Visual Studio 2012 +</span><span class="sxs-lookup"><span data-stu-id="6b322-108">Visual Studio 2012+</span></span>

<span data-ttu-id="6b322-109">此 NuGet 3.0 预览版包含在 Visual Studio 2015 预览版中。</span><span class="sxs-lookup"><span data-stu-id="6b322-109">This NuGet 3.0 Preview is included in Visual Studio 2015 Preview.</span></span> <span data-ttu-id="6b322-110">我们正在努力获取 Visual Studio 2012 的预览版，并在不久后 Visual Studio 2013。</span><span class="sxs-lookup"><span data-stu-id="6b322-110">We are working to get preview drops out for Visual Studio 2012 and Visual Studio 2013 very soon.</span></span> <span data-ttu-id="6b322-111">我们之前已经分享我们的意图来 [中止 Visual Studio 2010 的更新](http://blog.nuget.org/20141002/visual-studio-2010.html)，我们确实做出了这一难题。</span><span class="sxs-lookup"><span data-stu-id="6b322-111">We previously shared our intent to [discontinue updates for Visual Studio 2010](http://blog.nuget.org/20141002/visual-studio-2010.html), and we did make that difficult decision.</span></span>

## <a name="brand-new-ui"></a><span data-ttu-id="6b322-112">全新 UI</span><span class="sxs-lookup"><span data-stu-id="6b322-112">Brand New UI</span></span>

<span data-ttu-id="6b322-113">有关 NuGet 3.0 预览版的第一件事是我们全新的 UI。</span><span class="sxs-lookup"><span data-stu-id="6b322-113">The first thing you notice about NuGet 3.0 Preview is our brand new UI.</span></span> <span data-ttu-id="6b322-114">它不再是模式对话框;它现在是一个完整的 Visual Studio 文档窗口。</span><span class="sxs-lookup"><span data-stu-id="6b322-114">It's no longer a modal dialog; it's now a full Visual Studio document window.</span></span> <span data-ttu-id="6b322-115">这样一来，您就可以同时打开多个项目的 UI (和/或解决方案) ，将窗口移出到另一个监视器，并将其停靠在您喜欢的位置等等。</span><span class="sxs-lookup"><span data-stu-id="6b322-115">This allows you to open the UI for multiple projects (and/or the solution) at once, tear the window off to another monitor, dock it however you'd like, etc.</span></span>

![新 NuGet UI](./media/NuGet-3.0-Preview/new-ui.png)

<span data-ttu-id="6b322-117">除了因放弃模式对话框以外的可用性不同之外，我们还在新的 UI 中提供了许多新功能。</span><span class="sxs-lookup"><span data-stu-id="6b322-117">Beyond the usability differences because of abandoning the modal dialog, we also have lots of new features in the new UI.</span></span>

### <a name="version-selection"></a><span data-ttu-id="6b322-118">版本选择</span><span class="sxs-lookup"><span data-stu-id="6b322-118">Version Selection</span></span>

<span data-ttu-id="6b322-119">可能是最常请求的 UI 功能是允许对包安装和更新进行版本选择-这现在可用。</span><span class="sxs-lookup"><span data-stu-id="6b322-119">Perhaps the most requested UI feature is to allow version selection for package installation and update--this is now available.</span></span>

![选择包版本](./media/NuGet-3.0-Preview/version-selection.png)

<span data-ttu-id="6b322-121">不管是安装还是更新包，"版本" 下拉列表都允许您查看包的所有可用版本，其中有一些值得注意的版本升级到列表的顶部以便于选择。</span><span class="sxs-lookup"><span data-stu-id="6b322-121">Whether you are installing or updating a package, the version dropdown allows you to see all of the versions available for the package, with some notable versions promoted to the top of the list for easy selection.</span></span> <span data-ttu-id="6b322-122">不再需要使用 PowerShell 控制台来获取不是最新版本的特定版本。</span><span class="sxs-lookup"><span data-stu-id="6b322-122">You no longer need to use the PowerShell Console to get specific versions that are not the latest.</span></span>

### <a name="combined-installedonlineupdates-workflows"></a><span data-ttu-id="6b322-123">组合安装/联机/更新工作流</span><span class="sxs-lookup"><span data-stu-id="6b322-123">Combined Installed/Online/Updates Workflows</span></span>

<span data-ttu-id="6b322-124">以前的 UI 有3个选项卡用于安装、联机和更新。</span><span class="sxs-lookup"><span data-stu-id="6b322-124">Our previous UI had 3 tabs for Installed, Online, and Updates.</span></span> <span data-ttu-id="6b322-125">列出的包特定于这些工作流，而可用的操作也是特定于工作流的。</span><span class="sxs-lookup"><span data-stu-id="6b322-125">The packages listed were specific to those workflows and the actions available were specific to the workflows as well.</span></span> <span data-ttu-id="6b322-126">虽然这种情况看似合乎逻辑，但我们听说，你们中的许多人通常会获得这种分离。</span><span class="sxs-lookup"><span data-stu-id="6b322-126">While that seemed logical, we heard that many of you would often get tripped up by this separation.</span></span>

<span data-ttu-id="6b322-127">现在我们有了组合体验，你可以在其中安装、更新或卸载包，而不考虑选择包的方式。</span><span class="sxs-lookup"><span data-stu-id="6b322-127">We now have a combined experience, where you can install, update, or uninstall a package regardless of how you got the package selected.</span></span> <span data-ttu-id="6b322-128">为了帮助特定工作流，现在提供了一个筛选器下拉列表，使你可以筛选出可查看的包，但之后包的操作是一致的。</span><span class="sxs-lookup"><span data-stu-id="6b322-128">To assist with the specific workflows, we now have a Filter dropdown that lets you filter the packages visible, but then the actions available for the package are consistent.</span></span>

![卸载包](./media/NuGet-3.0-Preview/uninstall-package.png)

<span data-ttu-id="6b322-130">通过使用 "已安装" 筛选器，你可以轻松地查看已安装的包（其中有更新可用），然后可以通过更改版本选择来卸载或更新包，以查看更改操作可用。</span><span class="sxs-lookup"><span data-stu-id="6b322-130">By using the "Installed" filter, you can then easily see your installed packages, which ones have updates available, and then you can either uninstall or update the package by changing the version selection to see change the action available.</span></span>

![更新包](./media/NuGet-3.0-Preview/update-package.png)

### <a name="version-consolidation"></a><span data-ttu-id="6b322-132">版本合并</span><span class="sxs-lookup"><span data-stu-id="6b322-132">Version Consolidation</span></span>

<span data-ttu-id="6b322-133">在解决方案中将同一包安装到多个项目中是很常见的。</span><span class="sxs-lookup"><span data-stu-id="6b322-133">It's common to have the same package installed into multiple projects within your solution.</span></span> <span data-ttu-id="6b322-134">有时，安装在每个项目中的版本可能会偏离，并且需要合并所使用的版本。</span><span class="sxs-lookup"><span data-stu-id="6b322-134">Sometimes the versions installed into each project can drift apart and it's necessary to consolidate the versions in use.</span></span> <span data-ttu-id="6b322-135">NuGet 3.0 预览版为此方案引入了一项新功能。</span><span class="sxs-lookup"><span data-stu-id="6b322-135">NuGet 3.0 Preview introduces a new feature for just this scenario.</span></span>

<span data-ttu-id="6b322-136">可以通过右键单击解决方案并选择 "管理解决方案的 NuGet 包" 来访问解决方案级包管理窗口。</span><span class="sxs-lookup"><span data-stu-id="6b322-136">The solution-level package management window can be accessed by right-clicking on the solution and choosing Manage NuGet Packages for Solution.</span></span> <span data-ttu-id="6b322-137">在该版本中，如果选择安装到多个项目中的包，但使用不同的版本，则新的 "合并" 操作将可用。</span><span class="sxs-lookup"><span data-stu-id="6b322-137">From there, if you select a package that is installed into multiple projects, but with different versions in use, a new "Consolidate" action becomes available.</span></span> <span data-ttu-id="6b322-138">在下面的屏幕截图中， `Newtonsoft.Json` 已安装到 `SamplesClassLibrary` with 版本中， `6.0.4` 并已安装到 `SamplesConsoleApp` 版本中 `5.0.4` 。</span><span class="sxs-lookup"><span data-stu-id="6b322-138">In the screen shot below, `Newtonsoft.Json` was installed into the `SamplesClassLibrary` with version `6.0.4` and installed into `SamplesConsoleApp` with version `5.0.4`.</span></span>

![合并版本](./media/NuGet-3.0-Preview/consolidate.png)

<span data-ttu-id="6b322-140">下面是用于合并到单个版本的工作流。</span><span class="sxs-lookup"><span data-stu-id="6b322-140">Here's the workflow for consolidating onto a single version.</span></span>

1. <span data-ttu-id="6b322-141">`Newtonsoft.Json`在列表中选择包</span><span class="sxs-lookup"><span data-stu-id="6b322-141">Select the `Newtonsoft.Json` package in the list</span></span>
1. <span data-ttu-id="6b322-142">`Consolidate`从 `Action` 下拉列表中选择</span><span class="sxs-lookup"><span data-stu-id="6b322-142">Choose `Consolidate` from the `Action` dropdown</span></span>
1. <span data-ttu-id="6b322-143">使用 `Version` 下拉列表选择要合并到的版本</span><span class="sxs-lookup"><span data-stu-id="6b322-143">Use the `Version` dropdown to select the version to be consolidated onto</span></span>
1. <span data-ttu-id="6b322-144">选中应合并到该版本上的项目的复选框 (请注意，所选版本中已有的项目将灰显) </span><span class="sxs-lookup"><span data-stu-id="6b322-144">Check the boxes for the projects that should be consolidated onto that version (note that projects already on the selected version will be greyed out)</span></span>
1. <span data-ttu-id="6b322-145">单击 " `Consolidate` 执行合并" 按钮</span><span class="sxs-lookup"><span data-stu-id="6b322-145">Click the `Consolidate` button to perform the consolidation</span></span>

### <a name="operation-previews"></a><span data-ttu-id="6b322-146">操作预览</span><span class="sxs-lookup"><span data-stu-id="6b322-146">Operation Previews</span></span>

<span data-ttu-id="6b322-147">无论执行哪个操作（安装/更新/卸载），新的 UI 现在提供了一种方法来预览将对项目进行的更改。</span><span class="sxs-lookup"><span data-stu-id="6b322-147">Regardless of which operation you're performing--install/update/uninstall--the new UI now offers a way to preview the changes that will be made to your project.</span></span> <span data-ttu-id="6b322-148">此预览将显示要安装的任何新包、将更新的包、将卸载的包以及在操作过程中不会发生更改的包。</span><span class="sxs-lookup"><span data-stu-id="6b322-148">This preview will show any new packages that will be installed, packages that will be updated, and packages that will be uninstalled, along with packages that will be unchanged during the operation.</span></span>

<span data-ttu-id="6b322-149">在下面的示例中，我们可以看到，安装 SignalR 会导致对项目进行很多更改。</span><span class="sxs-lookup"><span data-stu-id="6b322-149">In the example below, we can see that installing Microsoft.AspNet.SignalR will result in quite a few changes to the project.</span></span>

![预览安装 SignalR](./media/NuGet-3.0-Preview/preview.png)

### <a name="installation-options"></a><span data-ttu-id="6b322-151">安装选项</span><span class="sxs-lookup"><span data-stu-id="6b322-151">Installation Options</span></span>

<span data-ttu-id="6b322-152">使用 PowerShell 控制台，可以控制几个值得注意的安装选项。</span><span class="sxs-lookup"><span data-stu-id="6b322-152">Using the PowerShell Console, you've had control over a couple of notable installation options.</span></span> <span data-ttu-id="6b322-153">现在，我们还将这些功能引入了 UI 中。</span><span class="sxs-lookup"><span data-stu-id="6b322-153">We've now brought those features into the UI as well.</span></span> <span data-ttu-id="6b322-154">你现在可以控制如何选择依赖项版本的依赖关系解析行为。</span><span class="sxs-lookup"><span data-stu-id="6b322-154">You can now control the dependency resolution behavior for how versions of the dependencies are selected.</span></span>

![依赖项行为](./media/NuGet-3.0-Preview/dependency-behavior.png)

<span data-ttu-id="6b322-156">你还可以指定当包中的内容文件与你的项目中已有的文件发生冲突时要执行的操作。</span><span class="sxs-lookup"><span data-stu-id="6b322-156">You can also specify the action to take when content files from packages conflict with files already in your project.</span></span>

![文件冲突操作](./media/NuGet-3.0-Preview/file-conflict-action.png)

### <a name="infinite-scrolling"></a><span data-ttu-id="6b322-158">无限滚动</span><span class="sxs-lookup"><span data-stu-id="6b322-158">Infinite Scrolling</span></span>

<span data-ttu-id="6b322-159">我们使用了在列出包时具有滚动和分页模式的 UI 上，可以获得相当多的反馈。</span><span class="sxs-lookup"><span data-stu-id="6b322-159">We used to get quite a bit of feedback on our UI having both the scrolling and paging paradigms when listing packages.</span></span> <span data-ttu-id="6b322-160">必须滚动到简短列表的底部，单击下一个页码，然后再次滚动，这相当常见。</span><span class="sxs-lookup"><span data-stu-id="6b322-160">It was pretty common to have to scroll to the bottom of the short list, click the next page number, and then scroll again.</span></span> <span data-ttu-id="6b322-161">利用新的 UI，我们在包列表中实现了无限滚动，只需滚动即可实现，而无需进行更多分页。</span><span class="sxs-lookup"><span data-stu-id="6b322-161">With the new UI, we've implemented infinite scrolling in the package list so that you only need to scroll--no more paging.</span></span>

![无限滚动](./media/NuGet-3.0-Preview/infinite-scrolling.png)

### <a name="make-it-work-make-it-fast-make-it-pretty"></a><span data-ttu-id="6b322-163">使其正常工作，使其更快，使其变得漂亮</span><span class="sxs-lookup"><span data-stu-id="6b322-163">Make it Work, Make it Fast, Make it Pretty</span></span>

<span data-ttu-id="6b322-164">我们很高兴能让你试用这个新的 UI。在此预览里程碑期间，我们已遵循了 "使其正常工作，使其变得更快，使其变得漂亮" 这一良好的言弃。</span><span class="sxs-lookup"><span data-stu-id="6b322-164">We are excited to get this new UI out for you to try out. During this Preview milestone, we've been following the good old adage of "Make it work, make it fast, make it pretty."</span></span> <span data-ttu-id="6b322-165">在此预览版中，我们已完成了上述第一个目标--它的工作原理。</span><span class="sxs-lookup"><span data-stu-id="6b322-165">In this preview, we've accomplished most of that first goal--it works.</span></span> <span data-ttu-id="6b322-166">我们知道，这并不是很快，而且我们还知道它并未太好。</span><span class="sxs-lookup"><span data-stu-id="6b322-166">We know it's not quite fast yet, and we know it's not quite pretty yet.</span></span> <span data-ttu-id="6b322-167">相信，我们将在现在和 RC 版本之间处理这些目标。</span><span class="sxs-lookup"><span data-stu-id="6b322-167">Trust that we'll be working on those goals between now and the RC release.</span></span> <span data-ttu-id="6b322-168">同时，我们将很乐意倾听您对新 UI 的 *可用性*（工作流、操作和使用新 ui 的方式）的反馈。 </span><span class="sxs-lookup"><span data-stu-id="6b322-168">In the meantime, we would love to hear your feedback about the *usability* of the new UI--the workflows, operations, and how it *feels* to use the new UI.</span></span>

<span data-ttu-id="6b322-169">与旧的 UI 相比，我们已经删除了一些函数。</span><span class="sxs-lookup"><span data-stu-id="6b322-169">There are a couple of functions that we've removed when compared to the old UI.</span></span> <span data-ttu-id="6b322-170">其中一项是有意的，而另一个则不是及时完成。</span><span class="sxs-lookup"><span data-stu-id="6b322-170">One of these was intentional, and the other one just didn't get done in time.</span></span>

#### <a name="searching-all-package-sources"></a><span data-ttu-id="6b322-171">搜索 "所有" 包源</span><span class="sxs-lookup"><span data-stu-id="6b322-171">Searching "All" Package Sources</span></span>

<span data-ttu-id="6b322-172">旧 UI 允许您对所有包源执行包搜索。</span><span class="sxs-lookup"><span data-stu-id="6b322-172">The old UI allowed you to perform a package search against all of your package sources.</span></span> <span data-ttu-id="6b322-173">我们已在 UI 中删除该功能，我们不会将其返回。</span><span class="sxs-lookup"><span data-stu-id="6b322-173">We've removed that feature in the UI and we won't be bringing it back.</span></span> <span data-ttu-id="6b322-174">此功能用于对所有包源执行搜索操作，将结果与组合在一起，并尝试根据排序选择对结果进行排序。</span><span class="sxs-lookup"><span data-stu-id="6b322-174">This feature used to perform search operations against all of your package sources, weave the results together, and attempt to order the results based on your sorting selection.</span></span>

<span data-ttu-id="6b322-175">我们发现，搜索相关性确实很难组合在一起。</span><span class="sxs-lookup"><span data-stu-id="6b322-175">We found that search relevance is really hard to weave together.</span></span> <span data-ttu-id="6b322-176">您是否可以设想对 Google 和 Bing 执行搜索，并将结果结合在一起？</span><span class="sxs-lookup"><span data-stu-id="6b322-176">Could you imagine performing a search against Google and Bing and weaving the results together?</span></span> <span data-ttu-id="6b322-177">此外，此功能的速度较慢，很容易 *意外* 使用，我们认为它很少真正有用。</span><span class="sxs-lookup"><span data-stu-id="6b322-177">Additionally, this feature was slow, easy to *accidentally* use, and we believe it was rarely actually useful.</span></span> <span data-ttu-id="6b322-178">由于此功能存在问题，我们在其上收到了大量可能从未修复的 bug 报告。</span><span class="sxs-lookup"><span data-stu-id="6b322-178">Because of the problems the feature introduced, we received a number of bug reports on it that could never have been fixed.</span></span>

#### <a name="update-all"></a><span data-ttu-id="6b322-179">全部更新</span><span class="sxs-lookup"><span data-stu-id="6b322-179">Update All</span></span>

<span data-ttu-id="6b322-180">过去，我们在旧 UI 中使用了 "全部更新" 按钮。</span><span class="sxs-lookup"><span data-stu-id="6b322-180">We used to have an "Update All" button in the old UI that isn't there in the new UI yet.</span></span> <span data-ttu-id="6b322-181">我们将为 RC 版本恢复此功能。</span><span class="sxs-lookup"><span data-stu-id="6b322-181">We will resurrect this feature for our RC release.</span></span>

## <a name="new-clientserver-api"></a><span data-ttu-id="6b322-182">新建客户端/服务器 API</span><span class="sxs-lookup"><span data-stu-id="6b322-182">New Client/Server API</span></span>

<span data-ttu-id="6b322-183">除了新的包管理 UI 中的所有新功能，我们还在处理 NuGet 的客户端/服务器协议的一些实现细节。</span><span class="sxs-lookup"><span data-stu-id="6b322-183">In addition to all of the new features in our new package management UI, we've also been working on some implementation details for NuGet's client/server protocol.</span></span> <span data-ttu-id="6b322-184">我们所做的工作是创建 NuGet 的 "API v3"，这是针对关键方案（如包还原和安装包）的高可用性而设计的。</span><span class="sxs-lookup"><span data-stu-id="6b322-184">The work we've done is to create "API v3" for NuGet, which is designed around high availability for critical scenarios such as package restore and installing packages.</span></span> <span data-ttu-id="6b322-185">新 API 基于 REST 和超媒体，我们已选择 [JSON-LD](http://json-ld.org) 作为资源格式。</span><span class="sxs-lookup"><span data-stu-id="6b322-185">The new API is based on REST and Hypermedia and we've selected [JSON-LD](http://json-ld.org) as our resource format.</span></span>

<span data-ttu-id="6b322-186">在 NuGet 3.0 预览位中，你会在 "包源" 下拉列表中看到一个名为 "preview.nuget.org" 的新包源。</span><span class="sxs-lookup"><span data-stu-id="6b322-186">In the NuGet 3.0 Preview bits, you see a new package source called "preview.nuget.org" in the package source dropdown.</span></span> <span data-ttu-id="6b322-187">如果选择此包源，我们将使用新的 API，而不是连接到 nuget.org。我们使预览源在 UI 中可用，同时我们继续测试、修改和改进新的 API。</span><span class="sxs-lookup"><span data-stu-id="6b322-187">If you select that package source, we'll use our new API rather to connect to nuget.org. We've made the preview source available in the UI while we continue to test, revise, and improve the new API.</span></span> <span data-ttu-id="6b322-188">在 NuGet 3.0 RC 中，这一基于 API v3 的新包源将替换基于 v2 的 "nuget.org" 包源。</span><span class="sxs-lookup"><span data-stu-id="6b322-188">In NuGet 3.0 RC, this new API v3-based package source will replace the v2-based "nuget.org" package source.</span></span>

<span data-ttu-id="6b322-189">尽管我们将投入使用 API v3，但我们已将所有这些新功能也用于我们的现有 API v2 协议，这意味着它们将适用于除 nuget.org 以外的现有包源。</span><span class="sxs-lookup"><span data-stu-id="6b322-189">Despite the investment we're putting into API v3, we've made all of these new features also work with our existing API v2 protocol, which means they will work with existing package sources other than nuget.org as well.</span></span>

## <a name="new-features-coming"></a><span data-ttu-id="6b322-190">新功能即将推出</span><span class="sxs-lookup"><span data-stu-id="6b322-190">New Features Coming</span></span>

<span data-ttu-id="6b322-191">在现在和 3.0 RTM 之间，我们还将处理一些基本的新 NuGet 功能，而不仅仅是在 UI 中看到的内容。</span><span class="sxs-lookup"><span data-stu-id="6b322-191">Between now and 3.0 RTM, we are also working on some fundamental new NuGet features, beyond what you see in the UI.</span></span> <span data-ttu-id="6b322-192">下面是重要投资领域的简短列表：</span><span class="sxs-lookup"><span data-stu-id="6b322-192">Here's a short list of salient investment areas:</span></span>

1. <span data-ttu-id="6b322-193">我们与 Visual Studio 和 MSBuild 团队合作，使 [NuGet 更深入地进入平台](http://blog.nuget.org/20141014/in-the-platform.html)。</span><span class="sxs-lookup"><span data-stu-id="6b322-193">We're partnering with the Visual Studio and MSBuild teams to get [NuGet deeper into the platform](http://blog.nuget.org/20141014/in-the-platform.html).</span></span>
1. <span data-ttu-id="6b322-194">我们正在努力放弃安装时包约定，改为在打包时通过引入新的 "权威" [包清单](http://blog.nuget.org/20141023/package-manifests.html)来应用这些约定。</span><span class="sxs-lookup"><span data-stu-id="6b322-194">We're working to abandon installation-time package conventions and instead apply those conventions at packaging time by introducing a new "authoritative" [package manifest](http://blog.nuget.org/20141023/package-manifests.html).</span></span>
1. <span data-ttu-id="6b322-195">我们正在努力重构 NuGet 基本代码，使客户端和服务器组件可在不同的域中重复使用，而不是在 Visual Studio 中的包管理。</span><span class="sxs-lookup"><span data-stu-id="6b322-195">We're working to refactor the NuGet codebase to make the client and server components reusable in different domains beyond package management in Visual Studio.</span></span>
1. <span data-ttu-id="6b322-196">我们将调查 "专用依赖项" 的概念，其中包可以指示它在其他包上仅有依赖实现详细信息，不应将这些依赖项视为顶级依赖项。</span><span class="sxs-lookup"><span data-stu-id="6b322-196">We're investigating the notion of "private dependencies" where a package can indicate that it has dependencies on other packages for implementation details only, and those dependencies shouldn't be surfaced as top-level dependencies.</span></span>

## <a name="stay-tuned"></a><span data-ttu-id="6b322-197">保持关注</span><span class="sxs-lookup"><span data-stu-id="6b322-197">Stay Tuned</span></span>

<span data-ttu-id="6b322-198">有关 NuGet 3.0 的更多进度和公告，请关注 [我们的博客](http://blog.nuget.org) ！</span><span class="sxs-lookup"><span data-stu-id="6b322-198">Please keep an eye on [our blog](http://blog.nuget.org) for more progress and announcements for NuGet 3.0!</span></span>