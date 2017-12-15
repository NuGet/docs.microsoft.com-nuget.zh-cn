---
title: "NuGet 3.0 Beta 发行说明 |Microsoft 文档"
author: karann-msft
ms.author: karann-msft
manager: ghogen
ms.date: 11/11/2016
ms.topic: article
ms.prod: nuget
ms.technology: 
ms.assetid: 4153ff3f-f97f-4e54-b638-e844f70edf22
description: "包括已知的问题、 bug 修复、 增加的功能，以及 DCRs NuGet 3.0 试用版的发行说明。"
keywords: "NuGet 3.0 试用版发行说明，bug 修复的已知问题，添加了一些功能，DCRs"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 46b2a81845f5ac06b8c80975c55fcfc33b86636e
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/14/2017
---
# <a name="nuget-30-beta-release-notes"></a><span data-ttu-id="da782-104">NuGet 3.0 Beta 发行说明</span><span class="sxs-lookup"><span data-stu-id="da782-104">NuGet 3.0 Beta Release Notes</span></span>

<span data-ttu-id="da782-105">[NuGet 3.0 预览版发行说明](../release-notes/nuget-3.0-preview.md) | [NuGet 3.0 RC 发行说明](../release-notes/nuget-3.0-rc.md)</span><span class="sxs-lookup"><span data-stu-id="da782-105">[NuGet 3.0 Preview Release Notes](../release-notes/nuget-3.0-preview.md) | [NuGet 3.0 RC Release Notes](../release-notes/nuget-3.0-rc.md)</span></span>

<span data-ttu-id="da782-106">为 Visual Studio 2015 CTP 6 版本情况下，NuGet 3.0 试用版已于 2015 年 2 月 23 日发布。</span><span class="sxs-lookup"><span data-stu-id="da782-106">NuGet 3.0 Beta was released on February 23, 2015 for the Visual Studio 2015 CTP 6 release.</span></span> <span data-ttu-id="da782-107">此版本对我们的团队，意味着大量，我们有大量的体系结构和性能改进，可共享，以及我们非常高兴以开始优化我们 nuget.org 的服务上的性能设置。</span><span class="sxs-lookup"><span data-stu-id="da782-107">This release means a lot to our team, as we have a number of architecture and performance improvements to share, and we're excited to start tuning the performance settings on our nuget.org service.</span></span>

<span data-ttu-id="da782-108">我们强烈建议你在安装此新版本之前卸载任何以前版本的 NuGet Visual Studio 2015 扩展。</span><span class="sxs-lookup"><span data-stu-id="da782-108">We strongly recommend that you uninstall any prior version of the NuGet Visual Studio 2015 extension before installing this new version.</span></span>  <span data-ttu-id="da782-109">如果你有与此版本的扩展的任何问题，我们建议你还原到[以前的版本](http://nuget.codeplex.com/downloads/get/909582)用于 Visual Studio 2015 预览版。</span><span class="sxs-lookup"><span data-stu-id="da782-109">If you have any problems with this version of the extension, we recommend you revert to the [prior version](http://nuget.codeplex.com/downloads/get/909582) for use with Visual Studio 2015 preview.</span></span>

## <a name="visual-studio-2012"></a><span data-ttu-id="da782-110">Visual Studio 2012 +</span><span class="sxs-lookup"><span data-stu-id="da782-110">Visual Studio 2012+</span></span>

<span data-ttu-id="da782-111">此 NuGet 3.0 试用版，可在 Visual Studio 2015 CTP 6 扩展库中安装。</span><span class="sxs-lookup"><span data-stu-id="da782-111">This NuGet 3.0 Beta is available to install in the Visual Studio 2015 CTP 6 Extension Gallery.</span></span> <span data-ttu-id="da782-112">我们正在努力获取预览谷的 Visual Studio 2012 和 Visual Studio 2013 很快。</span><span class="sxs-lookup"><span data-stu-id="da782-112">We are working to get preview drops out for Visual Studio 2012 and Visual Studio 2013 very soon.</span></span> <span data-ttu-id="da782-113">我们先前共享到我们的目的[for Visual Studio 2010 停止更新](http://blog.nuget.org/20141002/visual-studio-2010.html)，我们未作出此困难的决策。</span><span class="sxs-lookup"><span data-stu-id="da782-113">We previously shared our intent to [discontinue updates for Visual Studio 2010](http://blog.nuget.org/20141002/visual-studio-2010.html), and we did make that difficult decision.</span></span>

## <a name="new-clientserver-api"></a><span data-ttu-id="da782-114">新的客户端/服务器 API</span><span class="sxs-lookup"><span data-stu-id="da782-114">New Client/Server API</span></span>

<span data-ttu-id="da782-115">我们一直在 NuGet 的客户端/服务器协议某些实现详细信息。</span><span class="sxs-lookup"><span data-stu-id="da782-115">We've been working on some implementation details for NuGet's client/server protocol.</span></span> <span data-ttu-id="da782-116">我们已完成的工作是创建"API v3"nuget，围绕关键方案，如程序包还原和安装包的高可用性而设计。</span><span class="sxs-lookup"><span data-stu-id="da782-116">The work we've done is to create "API v3" for NuGet, which is designed around high availability for critical scenarios such as package restore and installing packages.</span></span> <span data-ttu-id="da782-117">新的 API 基于 REST 并且超媒体，我们已选择[JSON LD](http://json-ld.org)作为我们资源格式。</span><span class="sxs-lookup"><span data-stu-id="da782-117">The new API is based on REST and Hypermedia and we've selected [JSON-LD](http://json-ld.org) as our resource format.</span></span>

<span data-ttu-id="da782-118">以 NuGet 3.0 试用版位为单位，你将看到在程序包源下拉列表中称为"api.nuget.org"的新包源。</span><span class="sxs-lookup"><span data-stu-id="da782-118">In the NuGet 3.0 Beta bits, you'll see a new package source called "api.nuget.org" in the package source dropdown.</span></span>   <span data-ttu-id="da782-119">如果你选择该包源，我们将使用我们新的 API 而是要连接到 nuget.org。在 NuGet 3.0 RC 中，此新的 API 基于 v3 的包源将替换 v2 基于"nuget.org"包源。</span><span class="sxs-lookup"><span data-stu-id="da782-119">If you select that package source, we'll use our new API rather to connect to nuget.org. In NuGet 3.0 RC, this new API v3-based package source will replace the v2-based "nuget.org" package source.</span></span>  <span data-ttu-id="da782-120">我们建议禁用所有其他公共包源，并且将仅 api.nuget.org 保留为仅对公共包存储库。</span><span class="sxs-lookup"><span data-stu-id="da782-120">We recommend disabling all of the other public package sources and leave only api.nuget.org as your only public package repository.</span></span>

<span data-ttu-id="da782-121">我们已投入了大量的时间生成我们 v3 的 API，并将继续保持标准 v2 API 以访问公共存储库寻求的旧客户端的。</span><span class="sxs-lookup"><span data-stu-id="da782-121">We've put a lot of time into building our v3 API and will continue to maintain the standard v2 API for old clients seeking to access the public repository.</span></span>

## <a name="updated-ui"></a><span data-ttu-id="da782-122">更新的 UI</span><span class="sxs-lookup"><span data-stu-id="da782-122">Updated UI</span></span>

<span data-ttu-id="da782-123">我们已增强，此版本中，以包括让您选择要与包执行的操作，然后转换到屏幕的选项区域中的复选框的预览按钮的组合框中的用户界面。</span><span class="sxs-lookup"><span data-stu-id="da782-123">We've enhanced the user-interface in this release to include a combobox that will allow you to choose an action to take with the package and transitioned the preview button into a checkbox in the options area of the screen.</span></span>  <span data-ttu-id="da782-124">选项区域不再可折叠，并且现在提供描述可用的选项的帮助链接。</span><span class="sxs-lookup"><span data-stu-id="da782-124">The options area is no longer collapsible and now provides a help link describing the options available.</span></span>

![新的 NuGet UI](./media/NuGet-3.0-Beta/updated-ui.png)


### <a name="operation-logging"></a><span data-ttu-id="da782-126">操作日志记录</span><span class="sxs-lookup"><span data-stu-id="da782-126">Operation Logging</span></span>

<span data-ttu-id="da782-127">我们删除了日志记录信息，将快速显示和隐藏，同时安装或卸载模式窗口。</span><span class="sxs-lookup"><span data-stu-id="da782-127">We removed the modal window with logging information that would quickly appear and hide while installing or uninstalling.</span></span>  <span data-ttu-id="da782-128">确实要查看的信息或能够从其复制并粘贴时，此窗口将添加任何值。</span><span class="sxs-lookup"><span data-stu-id="da782-128">This window added no value when you would really want to see the information or be able to copy and paste from it.</span></span>  <span data-ttu-id="da782-129">相反，我们现在将重定向所有日志记录到输出窗口的包管理器窗格中的输出。</span><span class="sxs-lookup"><span data-stu-id="da782-129">Instead, we are now redirecting all of the output logging to the Package Manager pane of the Output window.</span></span>  <span data-ttu-id="da782-130">我们认为这是更舒适，类似于你想要检查的典型生成报表。</span><span class="sxs-lookup"><span data-stu-id="da782-130">We think this is more comfortable and similar to a typical build report that you would want to inspect.</span></span>


### <a name="focus-on-performance"></a><span data-ttu-id="da782-131">重点放在性能</span><span class="sxs-lookup"><span data-stu-id="da782-131">Focus on Performance</span></span>

<span data-ttu-id="da782-132">我们做了大量的名称提高性能的 NuGet 搜索和读取的更改。</span><span class="sxs-lookup"><span data-stu-id="da782-132">We made a lot of changes in the name of improving performance of NuGet searches, and fetches.</span></span>  <span data-ttu-id="da782-133">这是从我们的客户，我们第一问题，我们想要确保我们在此版本中解决。</span><span class="sxs-lookup"><span data-stu-id="da782-133">This was our number one concern from our customers, and we wanted to be sure we addressed it in this release.</span></span>  <span data-ttu-id="da782-134">我们已优化我们的服务器，构建新的 CDN，并改进匹配逻辑为更具相关性您希望提供查询和更快的包搜索结果。</span><span class="sxs-lookup"><span data-stu-id="da782-134">We've tuned our servers, built out a new CDN, and improved the query matching logic to hopefully deliver to you more relevant and faster package search results.</span></span>

<span data-ttu-id="da782-135">我们继续通过 NuGet 3.0 开发此阶段操作，我们将优化和监视该 nuget.org 服务以确保我们提供改进的体验。</span><span class="sxs-lookup"><span data-stu-id="da782-135">As we proceed through this phase of the development of NuGet 3.0, we will be tuning and monitoring the nuget.org service to ensure that we deliver an improved experience.</span></span>  <span data-ttu-id="da782-136">我们不计划进行的任何停机时间，但将被添加并更改服务中的资源。</span><span class="sxs-lookup"><span data-stu-id="da782-136">We do not plan to engage in any downtime, but will be adding and changing resources in the service.</span></span>  <span data-ttu-id="da782-137">关注我们[twitter 订阅源](http://twitter.com/nuget)有关当我们更改服务配置的详细信息。</span><span class="sxs-lookup"><span data-stu-id="da782-137">Keep an eye on our [twitter feed](http://twitter.com/nuget) for details on when we change the service configuration.</span></span>

## <a name="building-nuget-with-nuget"></a><span data-ttu-id="da782-138">使用 NuGet 构建 NuGet</span><span class="sxs-lookup"><span data-stu-id="da782-138">Building NuGet with NuGet</span></span>

<span data-ttu-id="da782-139">我们现在具有到它们本身内置于 NuGet 包的多个组件重新构建我们 NuGet 客户端。</span><span class="sxs-lookup"><span data-stu-id="da782-139">We have now rearchitected our NuGet clients into several components that are themselves being built into NuGet packages.</span></span> <span data-ttu-id="da782-140">此重复使用我们自己的库的强制我们构建组件重复使用以及可以正确打包的。</span><span class="sxs-lookup"><span data-stu-id="da782-140">This re-use of our own libraries forces us to build components that are re-usable and that can be packaged properly.</span></span>  <span data-ttu-id="da782-141">我们已经能够消除重复的代码，并已了解如何更好地配置我们的开发过程，以支持需要生成在我们的解决方案整个包。</span><span class="sxs-lookup"><span data-stu-id="da782-141">We have been able to eliminate duplicated code and have learned how to better configure our development process to support the need to build packages throughout our solutions.</span></span>  <span data-ttu-id="da782-142">查找博客文章很快我们将讨论有关如何构造代码项目和我们生成过程的工作原理。</span><span class="sxs-lookup"><span data-stu-id="da782-142">Look for a blog post soon where we will talk about how the code projects are structured and how our build process works.</span></span>

## <a name="stay-tuned"></a><span data-ttu-id="da782-143">请继续关注</span><span class="sxs-lookup"><span data-stu-id="da782-143">Stay Tuned</span></span>

<span data-ttu-id="da782-144">请留意[我们的博客](http://blog.nuget.org)了解详细的进度和公告 NuGet 3.0 ！</span><span class="sxs-lookup"><span data-stu-id="da782-144">Please keep an eye on [our blog](http://blog.nuget.org) for more progress and announcements for NuGet 3.0!</span></span>
