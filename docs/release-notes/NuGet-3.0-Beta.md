---
title: NuGet 3.0 Beta 发行说明
description: NuGet 3.0 Beta 发行说明，包括已知问题、bug 修复、新增功能和 Dcr。
author: JonDouglas
ms.author: jodou
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 7970c3d81c724edc743d7b2d38c4c157237a0271
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/26/2021
ms.locfileid: "98776619"
---
# <a name="nuget-30-beta-release-notes"></a><span data-ttu-id="b3119-103">NuGet 3.0 Beta 发行说明</span><span class="sxs-lookup"><span data-stu-id="b3119-103">NuGet 3.0 Beta Release Notes</span></span>

<span data-ttu-id="b3119-104">[NuGet 3.0 预览版发行说明](../release-notes/nuget-3.0-preview.md)  | [NuGet 3.0 RC 发行说明](../release-notes/nuget-3.0-rc.md)</span><span class="sxs-lookup"><span data-stu-id="b3119-104">[NuGet 3.0 Preview Release Notes](../release-notes/nuget-3.0-preview.md) | [NuGet 3.0 RC Release Notes](../release-notes/nuget-3.0-rc.md)</span></span>

<span data-ttu-id="b3119-105">在 Visual Studio 2015 CTP 6 版本的2015上发布了 NuGet 3.0 Beta 版。</span><span class="sxs-lookup"><span data-stu-id="b3119-105">NuGet 3.0 Beta was released on February 23, 2015 for the Visual Studio 2015 CTP 6 release.</span></span> <span data-ttu-id="b3119-106">这一版本非常适用于我们的团队，因为我们有很多体系结构和性能方面的改进需要进行共享，我们非常高兴地开始优化我们的 nuget.org 服务的性能设置。</span><span class="sxs-lookup"><span data-stu-id="b3119-106">This release means a lot to our team, as we have a number of architecture and performance improvements to share, and we're excited to start tuning the performance settings on our nuget.org service.</span></span>

<span data-ttu-id="b3119-107">我们强烈建议你在安装此新版本之前卸载任何以前版本的 NuGet Visual Studio 2015 扩展。</span><span class="sxs-lookup"><span data-stu-id="b3119-107">We strongly recommend that you uninstall any prior version of the NuGet Visual Studio 2015 extension before installing this new version.</span></span>  <span data-ttu-id="b3119-108">如果此版本的扩展有任何问题，我们建议您恢复到 [以前的版本](http://nuget.codeplex.com/downloads/get/909582) ，以便与 Visual Studio 2015 preview 一起使用。</span><span class="sxs-lookup"><span data-stu-id="b3119-108">If you have any problems with this version of the extension, we recommend you revert to the [prior version](http://nuget.codeplex.com/downloads/get/909582) for use with Visual Studio 2015 preview.</span></span>

## <a name="visual-studio-2012"></a><span data-ttu-id="b3119-109">Visual Studio 2012 +</span><span class="sxs-lookup"><span data-stu-id="b3119-109">Visual Studio 2012+</span></span>

<span data-ttu-id="b3119-110">此 NuGet 3.0 Beta 版可安装在 Visual Studio 2015 CTP 6 扩展库中。</span><span class="sxs-lookup"><span data-stu-id="b3119-110">This NuGet 3.0 Beta is available to install in the Visual Studio 2015 CTP 6 Extension Gallery.</span></span> <span data-ttu-id="b3119-111">我们正在努力获取 Visual Studio 2012 的预览版，并在不久后 Visual Studio 2013。</span><span class="sxs-lookup"><span data-stu-id="b3119-111">We are working to get preview drops out for Visual Studio 2012 and Visual Studio 2013 very soon.</span></span> <span data-ttu-id="b3119-112">我们之前已经分享我们的意图来 [中止 Visual Studio 2010 的更新](http://blog.nuget.org/20141002/visual-studio-2010.html)，我们确实做出了这一难题。</span><span class="sxs-lookup"><span data-stu-id="b3119-112">We previously shared our intent to [discontinue updates for Visual Studio 2010](http://blog.nuget.org/20141002/visual-studio-2010.html), and we did make that difficult decision.</span></span>

## <a name="new-clientserver-api"></a><span data-ttu-id="b3119-113">新建客户端/服务器 API</span><span class="sxs-lookup"><span data-stu-id="b3119-113">New Client/Server API</span></span>

<span data-ttu-id="b3119-114">我们一直在处理 NuGet 的客户端/服务器协议的一些实现细节。</span><span class="sxs-lookup"><span data-stu-id="b3119-114">We've been working on some implementation details for NuGet's client/server protocol.</span></span> <span data-ttu-id="b3119-115">我们所做的工作是创建 NuGet 的 "API v3"，这是针对关键方案（如包还原和安装包）的高可用性而设计的。</span><span class="sxs-lookup"><span data-stu-id="b3119-115">The work we've done is to create "API v3" for NuGet, which is designed around high availability for critical scenarios such as package restore and installing packages.</span></span> <span data-ttu-id="b3119-116">新 API 基于 REST 和超媒体，我们已选择 [JSON-LD](http://json-ld.org) 作为资源格式。</span><span class="sxs-lookup"><span data-stu-id="b3119-116">The new API is based on REST and Hypermedia and we've selected [JSON-LD](http://json-ld.org) as our resource format.</span></span>

<span data-ttu-id="b3119-117">在 NuGet 3.0 Beta 版中，你会在 "包源" 下拉列表中看到一个名为 "api.nuget.org" 的新包源。</span><span class="sxs-lookup"><span data-stu-id="b3119-117">In the NuGet 3.0 Beta bits, you see a new package source called "api.nuget.org" in the package source dropdown.</span></span>   <span data-ttu-id="b3119-118">如果选择此包源，我们将使用新的 API，而不是连接到 nuget.org。在 NuGet 3.0 RC 中，这一基于 API v3 的新包源将替换基于 v2 的 "nuget.org" 包源。</span><span class="sxs-lookup"><span data-stu-id="b3119-118">If you select that package source, we'll use our new API rather to connect to nuget.org. In NuGet 3.0 RC, this new API v3-based package source will replace the v2-based "nuget.org" package source.</span></span>  <span data-ttu-id="b3119-119">建议禁用所有其他公共包源，并仅将 api.nuget.org 保留为你的唯一公共包存储库。</span><span class="sxs-lookup"><span data-stu-id="b3119-119">We recommend disabling all of the other public package sources and leave only api.nuget.org as your only public package repository.</span></span>

<span data-ttu-id="b3119-120">我们投入了大量时间来构建 v3 API，并将继续为寻找公共存储库的旧客户端维护标准 v2 API。</span><span class="sxs-lookup"><span data-stu-id="b3119-120">We've put a lot of time into building our v3 API and will continue to maintain the standard v2 API for old clients seeking to access the public repository.</span></span>

## <a name="updated-ui"></a><span data-ttu-id="b3119-121">更新的 UI</span><span class="sxs-lookup"><span data-stu-id="b3119-121">Updated UI</span></span>

<span data-ttu-id="b3119-122">我们增强了此版本中的用户界面，以包含一个组合框，使用该组合框可以选择要对包执行的操作，并将预览按钮转换为屏幕 "选项" 区域中的复选框。</span><span class="sxs-lookup"><span data-stu-id="b3119-122">We've enhanced the user-interface in this release to include a combobox that will allow you to choose an action to take with the package and transitioned the preview button into a checkbox in the options area of the screen.</span></span>  <span data-ttu-id="b3119-123">选项区域不再可折叠，现在提供了描述可用选项的帮助链接。</span><span class="sxs-lookup"><span data-stu-id="b3119-123">The options area is no longer collapsible and now provides a help link describing the options available.</span></span>

![新 NuGet UI](./media/NuGet-3.0-Beta/updated-ui.png)


### <a name="operation-logging"></a><span data-ttu-id="b3119-125">操作日志记录</span><span class="sxs-lookup"><span data-stu-id="b3119-125">Operation Logging</span></span>

<span data-ttu-id="b3119-126">我们删除了模式窗口，其中包含的日志记录信息会在安装或卸载时快速显示和隐藏。</span><span class="sxs-lookup"><span data-stu-id="b3119-126">We removed the modal window with logging information that would quickly appear and hide while installing or uninstalling.</span></span>  <span data-ttu-id="b3119-127">如果你确实想要查看该信息或能够从它进行复制和粘贴，此窗口不会添加任何值。</span><span class="sxs-lookup"><span data-stu-id="b3119-127">This window added no value when you would really want to see the information or be able to copy and paste from it.</span></span>  <span data-ttu-id="b3119-128">相反，我们现在会将所有输出日志记录都重定向到 "输出" 窗口的 "包管理器" 窗格。</span><span class="sxs-lookup"><span data-stu-id="b3119-128">Instead, we are now redirecting all of the output logging to the Package Manager pane of the Output window.</span></span>  <span data-ttu-id="b3119-129">我们认为这种方式更加舒适，与要检查的典型生成报告类似。</span><span class="sxs-lookup"><span data-stu-id="b3119-129">We think this is more comfortable and similar to a typical build report that you would want to inspect.</span></span>


### <a name="focus-on-performance"></a><span data-ttu-id="b3119-130">专注于性能</span><span class="sxs-lookup"><span data-stu-id="b3119-130">Focus on Performance</span></span>

<span data-ttu-id="b3119-131">我们对提高 NuGet 搜索和提取性能的名称进行了很多更改。</span><span class="sxs-lookup"><span data-stu-id="b3119-131">We made a lot of changes in the name of improving performance of NuGet searches, and fetches.</span></span>  <span data-ttu-id="b3119-132">这是我们的客户的一项重要问题，我们希望在此版本中解决此问题。</span><span class="sxs-lookup"><span data-stu-id="b3119-132">This was our number one concern from our customers, and we wanted to be sure we addressed it in this release.</span></span>  <span data-ttu-id="b3119-133">我们已经优化了服务器，并构建了新的 CDN，并改进了查询匹配逻辑，从而为你提供了更多相关、更快的包搜索结果。</span><span class="sxs-lookup"><span data-stu-id="b3119-133">We've tuned our servers, built out a new CDN, and improved the query matching logic to hopefully deliver to you more relevant and faster package search results.</span></span>

<span data-ttu-id="b3119-134">随着 NuGet 3.0 的这一阶段的发展，我们将对 nuget.org 服务进行优化和监视，以确保提供更好的体验。</span><span class="sxs-lookup"><span data-stu-id="b3119-134">As we proceed through this phase of the development of NuGet 3.0, we will be tuning and monitoring the nuget.org service to ensure that we deliver an improved experience.</span></span>  <span data-ttu-id="b3119-135">我们不打算在任何故障时间内进行维护，但会在服务中添加和更改资源。</span><span class="sxs-lookup"><span data-stu-id="b3119-135">We do not plan to engage in any downtime, but will be adding and changing resources in the service.</span></span>  <span data-ttu-id="b3119-136">若要详细了解如何更改服务配置，请留意 [twitter 源](http://twitter.com/nuget) 。</span><span class="sxs-lookup"><span data-stu-id="b3119-136">Keep an eye on our [twitter feed](http://twitter.com/nuget) for details on when we change the service configuration.</span></span>

## <a name="building-nuget-with-nuget"></a><span data-ttu-id="b3119-137">用 NuGet 构建 NuGet</span><span class="sxs-lookup"><span data-stu-id="b3119-137">Building NuGet with NuGet</span></span>

<span data-ttu-id="b3119-138">我们现在已将 NuGet 客户端重建到了多个组件，这些组件本身就内置于 NuGet 包中。</span><span class="sxs-lookup"><span data-stu-id="b3119-138">We have now rearchitected our NuGet clients into several components that are themselves being built into NuGet packages.</span></span> <span data-ttu-id="b3119-139">这种重复使用我们自己的库将强制构建可重复使用并且可正确打包的组件。</span><span class="sxs-lookup"><span data-stu-id="b3119-139">This re-use of our own libraries forces us to build components that are re-usable and that can be packaged properly.</span></span>  <span data-ttu-id="b3119-140">我们已经能够消除重复的代码，并了解了如何更好地配置开发过程，以支持在整个解决方案中构建包。</span><span class="sxs-lookup"><span data-stu-id="b3119-140">We have been able to eliminate duplicated code and have learned how to better configure our development process to support the need to build packages throughout our solutions.</span></span>  <span data-ttu-id="b3119-141">在这里，我们将讨论如何构造代码项目以及我们的生成过程如何工作的博客文章。</span><span class="sxs-lookup"><span data-stu-id="b3119-141">Look for a blog post soon where we will talk about how the code projects are structured and how our build process works.</span></span>

## <a name="stay-tuned"></a><span data-ttu-id="b3119-142">保持关注</span><span class="sxs-lookup"><span data-stu-id="b3119-142">Stay Tuned</span></span>

<span data-ttu-id="b3119-143">有关 NuGet 3.0 的更多进度和公告，请关注 [我们的博客](http://blog.nuget.org) ！</span><span class="sxs-lookup"><span data-stu-id="b3119-143">Please keep an eye on [our blog](http://blog.nuget.org) for more progress and announcements for NuGet 3.0!</span></span>
