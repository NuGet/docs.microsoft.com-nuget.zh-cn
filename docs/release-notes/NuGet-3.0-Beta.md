---
title: NuGet 3.0 测试版发行说明
description: 包括已知的问题、 bug 修复、 新增的功能和 Dcr NuGet 3.0 试用版的发行说明。
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 9f9fec6a1af8dfbcfdcfa05a301ff52409521228
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/04/2018
ms.locfileid: "43550908"
---
# <a name="nuget-30-beta-release-notes"></a><span data-ttu-id="9715a-103">NuGet 3.0 测试版发行说明</span><span class="sxs-lookup"><span data-stu-id="9715a-103">NuGet 3.0 Beta Release Notes</span></span>

<span data-ttu-id="9715a-104">[NuGet 3.0 预览版发行说明](../release-notes/nuget-3.0-preview.md) | [NuGet 3.0 RC 发行说明](../release-notes/nuget-3.0-rc.md)</span><span class="sxs-lookup"><span data-stu-id="9715a-104">[NuGet 3.0 Preview Release Notes](../release-notes/nuget-3.0-preview.md) | [NuGet 3.0 RC Release Notes](../release-notes/nuget-3.0-rc.md)</span></span>

<span data-ttu-id="9715a-105">Visual Studio 2015 CTP 6 版本 2015 年 2 月 23 日发布了 NuGet 3.0 试用版。</span><span class="sxs-lookup"><span data-stu-id="9715a-105">NuGet 3.0 Beta was released on February 23, 2015 for the Visual Studio 2015 CTP 6 release.</span></span> <span data-ttu-id="9715a-106">此版本是指大量与我们的团队，我们有了大量的体系结构和性能改进，若要共享，并且我们很高兴以开始优化我们 nuget.org 的服务上的性能设置。</span><span class="sxs-lookup"><span data-stu-id="9715a-106">This release means a lot to our team, as we have a number of architecture and performance improvements to share, and we're excited to start tuning the performance settings on our nuget.org service.</span></span>

<span data-ttu-id="9715a-107">我们强烈建议您在安装此新版本之前卸载任何以前版本的 Visual Studio 2015 的 NuGet 扩展。</span><span class="sxs-lookup"><span data-stu-id="9715a-107">We strongly recommend that you uninstall any prior version of the NuGet Visual Studio 2015 extension before installing this new version.</span></span>  <span data-ttu-id="9715a-108">如果有此版本的扩展中的任何问题，我们建议你还原到[早期版本](http://nuget.codeplex.com/downloads/get/909582)以用于 Visual Studio 2015 预览版。</span><span class="sxs-lookup"><span data-stu-id="9715a-108">If you have any problems with this version of the extension, we recommend you revert to the [prior version](http://nuget.codeplex.com/downloads/get/909582) for use with Visual Studio 2015 preview.</span></span>

## <a name="visual-studio-2012"></a><span data-ttu-id="9715a-109">Visual Studio 2012 和更高</span><span class="sxs-lookup"><span data-stu-id="9715a-109">Visual Studio 2012+</span></span>

<span data-ttu-id="9715a-110">可在 Visual Studio 2015 CTP 6 扩展库中安装此 NuGet 3.0 试用版。</span><span class="sxs-lookup"><span data-stu-id="9715a-110">This NuGet 3.0 Beta is available to install in the Visual Studio 2015 CTP 6 Extension Gallery.</span></span> <span data-ttu-id="9715a-111">我们正在努力推出预览版删除 Visual Studio 2012 和 Visual Studio 2013 很快。</span><span class="sxs-lookup"><span data-stu-id="9715a-111">We are working to get preview drops out for Visual Studio 2012 and Visual Studio 2013 very soon.</span></span> <span data-ttu-id="9715a-112">我们以前共享到我们的意图[停止更新适用于 Visual Studio 2010](http://blog.nuget.org/20141002/visual-studio-2010.html)，和我们未做出难以决定。</span><span class="sxs-lookup"><span data-stu-id="9715a-112">We previously shared our intent to [discontinue updates for Visual Studio 2010](http://blog.nuget.org/20141002/visual-studio-2010.html), and we did make that difficult decision.</span></span>

## <a name="new-clientserver-api"></a><span data-ttu-id="9715a-113">新的客户端/服务器 API</span><span class="sxs-lookup"><span data-stu-id="9715a-113">New Client/Server API</span></span>

<span data-ttu-id="9715a-114">我们一直在 NuGet 的客户端/服务器协议一些实现细节。</span><span class="sxs-lookup"><span data-stu-id="9715a-114">We've been working on some implementation details for NuGet's client/server protocol.</span></span> <span data-ttu-id="9715a-115">我们所做的工作是为 NuGet，专为高可用性的关键方案，例如包还原和安装包创建"API v3"。</span><span class="sxs-lookup"><span data-stu-id="9715a-115">The work we've done is to create "API v3" for NuGet, which is designed around high availability for critical scenarios such as package restore and installing packages.</span></span> <span data-ttu-id="9715a-116">新的 API 基于 REST 和超媒体和我们所选[JSON-LD](http://json-ld.org)作为我们的资源格式。</span><span class="sxs-lookup"><span data-stu-id="9715a-116">The new API is based on REST and Hypermedia and we've selected [JSON-LD](http://json-ld.org) as our resource format.</span></span>

<span data-ttu-id="9715a-117">在 NuGet 3.0 试用版位中，可以看到称为"api.nuget.org"包源下拉列表中的新包源。</span><span class="sxs-lookup"><span data-stu-id="9715a-117">In the NuGet 3.0 Beta bits, you see a new package source called "api.nuget.org" in the package source dropdown.</span></span>   <span data-ttu-id="9715a-118">如果您选择的包源，我们将使用我们的新 API，而是要连接到 nuget.org。在 NuGet 3.0 RC 中，此新 API 基于 v3 的包源将替换基于 v2"nuget.org"包源。</span><span class="sxs-lookup"><span data-stu-id="9715a-118">If you select that package source, we'll use our new API rather to connect to nuget.org. In NuGet 3.0 RC, this new API v3-based package source will replace the v2-based "nuget.org" package source.</span></span>  <span data-ttu-id="9715a-119">我们建议禁用所有其他公共包源，并将仅 api.nuget.org 保留为仅对公共包存储库。</span><span class="sxs-lookup"><span data-stu-id="9715a-119">We recommend disabling all of the other public package sources and leave only api.nuget.org as your only public package repository.</span></span>

<span data-ttu-id="9715a-120">我们已投入了大量的时间构建我们的 v3 API，并将继续为旧客户端查找来访问公共存储库保持标准 v2 API。</span><span class="sxs-lookup"><span data-stu-id="9715a-120">We've put a lot of time into building our v3 API and will continue to maintain the standard v2 API for old clients seeking to access the public repository.</span></span>

## <a name="updated-ui"></a><span data-ttu-id="9715a-121">更新后的 UI</span><span class="sxs-lookup"><span data-stu-id="9715a-121">Updated UI</span></span>

<span data-ttu-id="9715a-122">我们已改进在此版本中包括的组合框，将允许您选择要与包执行的操作和转换到屏幕的选项区域中的复选框的预览按钮的用户界面。</span><span class="sxs-lookup"><span data-stu-id="9715a-122">We've enhanced the user-interface in this release to include a combobox that will allow you to choose an action to take with the package and transitioned the preview button into a checkbox in the options area of the screen.</span></span>  <span data-ttu-id="9715a-123">选项区域不再可折叠，现在提供描述可用的选项的帮助链接。</span><span class="sxs-lookup"><span data-stu-id="9715a-123">The options area is no longer collapsible and now provides a help link describing the options available.</span></span>

![新的 NuGet UI](./media/NuGet-3.0-Beta/updated-ui.png)


### <a name="operation-logging"></a><span data-ttu-id="9715a-125">操作日志记录</span><span class="sxs-lookup"><span data-stu-id="9715a-125">Operation Logging</span></span>

<span data-ttu-id="9715a-126">我们删除包含的日志记录信息的快速的显示效果并在安装或卸载时隐藏模式窗口。</span><span class="sxs-lookup"><span data-stu-id="9715a-126">We removed the modal window with logging information that would quickly appear and hide while installing or uninstalling.</span></span>  <span data-ttu-id="9715a-127">此窗口时真正想要查看的信息，否则将无法从其复制和粘贴添加任何值。</span><span class="sxs-lookup"><span data-stu-id="9715a-127">This window added no value when you would really want to see the information or be able to copy and paste from it.</span></span>  <span data-ttu-id="9715a-128">相反，我们现在重定向所有输出记录到输出窗口的包管理器窗格中。</span><span class="sxs-lookup"><span data-stu-id="9715a-128">Instead, we are now redirecting all of the output logging to the Package Manager pane of the Output window.</span></span>  <span data-ttu-id="9715a-129">我们认为这是更舒适和类似于你想要检查的典型生成报表。</span><span class="sxs-lookup"><span data-stu-id="9715a-129">We think this is more comfortable and similar to a typical build report that you would want to inspect.</span></span>


### <a name="focus-on-performance"></a><span data-ttu-id="9715a-130">专注于性能</span><span class="sxs-lookup"><span data-stu-id="9715a-130">Focus on Performance</span></span>

<span data-ttu-id="9715a-131">我们做了大量的更改提高性能的 NuGet 搜索和提取操作的名称。</span><span class="sxs-lookup"><span data-stu-id="9715a-131">We made a lot of changes in the name of improving performance of NuGet searches, and fetches.</span></span>  <span data-ttu-id="9715a-132">这是从我们的客户，我们首要问题，我们希望确保我们在此版本中解决。</span><span class="sxs-lookup"><span data-stu-id="9715a-132">This was our number one concern from our customers, and we wanted to be sure we addressed it in this release.</span></span>  <span data-ttu-id="9715a-133">我们已经优化我们的服务器，构建新的 CDN，并改进了匹配逻辑为您的关系更密切希望提供的查询和更快包搜索结果。</span><span class="sxs-lookup"><span data-stu-id="9715a-133">We've tuned our servers, built out a new CDN, and improved the query matching logic to hopefully deliver to you more relevant and faster package search results.</span></span>

<span data-ttu-id="9715a-134">随着我们逐步开发的 NuGet 3.0 的这个阶段，我们将优化和监视 nuget.org 服务，以确保我们提供改进的体验。</span><span class="sxs-lookup"><span data-stu-id="9715a-134">As we proceed through this phase of the development of NuGet 3.0, we will be tuning and monitoring the nuget.org service to ensure that we deliver an improved experience.</span></span>  <span data-ttu-id="9715a-135">我们不要计划参与任何停机时间，但将会添加和更改服务中的资源。</span><span class="sxs-lookup"><span data-stu-id="9715a-135">We do not plan to engage in any downtime, but will be adding and changing resources in the service.</span></span>  <span data-ttu-id="9715a-136">请关注我们[twitter 订阅源](http://twitter.com/nuget)有关当我们更改的服务配置的详细信息。</span><span class="sxs-lookup"><span data-stu-id="9715a-136">Keep an eye on our [twitter feed](http://twitter.com/nuget) for details on when we change the service configuration.</span></span>

## <a name="building-nuget-with-nuget"></a><span data-ttu-id="9715a-137">使用 NuGet 生成 NuGet</span><span class="sxs-lookup"><span data-stu-id="9715a-137">Building NuGet with NuGet</span></span>

<span data-ttu-id="9715a-138">我们现在已为多个组件内置到 NuGet 包本身被重建我们 NuGet 客户端。</span><span class="sxs-lookup"><span data-stu-id="9715a-138">We have now rearchitected our NuGet clients into several components that are themselves being built into NuGet packages.</span></span> <span data-ttu-id="9715a-139">此重复使用我们自己的库的迫使我们构建的是重复使用，可以正确打包的组件。</span><span class="sxs-lookup"><span data-stu-id="9715a-139">This re-use of our own libraries forces us to build components that are re-usable and that can be packaged properly.</span></span>  <span data-ttu-id="9715a-140">我们已能够消除重复的代码，了解到如何更好地配置我们的开发过程，以支持需要生成在我们的解决方案整个包。</span><span class="sxs-lookup"><span data-stu-id="9715a-140">We have been able to eliminate duplicated code and have learned how to better configure our development process to support the need to build packages throughout our solutions.</span></span>  <span data-ttu-id="9715a-141">查找博客文章很快我们将讨论有关代码项目的构建方式我们生成过程的工作原理。</span><span class="sxs-lookup"><span data-stu-id="9715a-141">Look for a blog post soon where we will talk about how the code projects are structured and how our build process works.</span></span>

## <a name="stay-tuned"></a><span data-ttu-id="9715a-142">请继续关注</span><span class="sxs-lookup"><span data-stu-id="9715a-142">Stay Tuned</span></span>

<span data-ttu-id="9715a-143">请密切关注[我们的博客](http://blog.nuget.org)详细进度和 NuGet 3.0 的公告 ！</span><span class="sxs-lookup"><span data-stu-id="9715a-143">Please keep an eye on [our blog](http://blog.nuget.org) for more progress and announcements for NuGet 3.0!</span></span>
