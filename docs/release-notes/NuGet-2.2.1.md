---
title: NuGet 2.2.1 发行说明
description: NuGet 2.2.1 包括的发行说明的已知问题、 bug 修复、 新增的功能和 Dcr。
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: abbd3a9d9c51132477ceb236fed22cb63ccda209
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/04/2018
ms.locfileid: "43550693"
---
# <a name="nuget-221-release-notes"></a><span data-ttu-id="017a9-103">NuGet 2.2.1 发行说明</span><span class="sxs-lookup"><span data-stu-id="017a9-103">NuGet 2.2.1 Release Notes</span></span>

<span data-ttu-id="017a9-104">[NuGet 2.2 发行说明](../release-notes/nuget-2.2.md) | [NuGet 2.5 发行说明](../release-notes/nuget-2.5.md)</span><span class="sxs-lookup"><span data-stu-id="017a9-104">[NuGet 2.2 Release Notes](../release-notes/nuget-2.2.md) | [NuGet 2.5 Release Notes](../release-notes/nuget-2.5.md)</span></span>

<span data-ttu-id="017a9-105">NuGet 2.2.1 已于 2013 年 2 月 15 日发布。</span><span class="sxs-lookup"><span data-stu-id="017a9-105">NuGet 2.2.1 was released on February 15, 2013.</span></span>  <span data-ttu-id="017a9-106">在 VS 扩展版本编号是 2.2.40116.9051。</span><span class="sxs-lookup"><span data-stu-id="017a9-106">The VS Extension version number is 2.2.40116.9051.</span></span>

## <a name="localization-refresh"></a><span data-ttu-id="017a9-107">本地化刷新</span><span class="sxs-lookup"><span data-stu-id="017a9-107">Localization Refresh</span></span>
<span data-ttu-id="017a9-108">当 NuGet 作为 Visual Studio 2012 的一部分提供时，它已完全本地化为英语 + 13 种其他语言。</span><span class="sxs-lookup"><span data-stu-id="017a9-108">When NuGet shipped as part of Visual Studio 2012, it was fully localized into English + 13 other languages.</span></span>  <span data-ttu-id="017a9-109">从那时起，NuGet 2.1 和 2.2 已装运，但有未刷新本地化。</span><span class="sxs-lookup"><span data-stu-id="017a9-109">Since then, NuGet 2.1 and 2.2 have shipped but the localization had not been refreshed.</span></span>  <span data-ttu-id="017a9-110">NuGet 2.2.1 版本刷新本地化。</span><span class="sxs-lookup"><span data-stu-id="017a9-110">The NuGet 2.2.1 release refreshes our localization.</span></span>

<span data-ttu-id="017a9-111">NuGet 的 UI 和 PowerShell 控制台已本地化为以下语言版本：</span><span class="sxs-lookup"><span data-stu-id="017a9-111">NuGet's UI and PowerShell Console are localized into the following languages:</span></span>

1. <span data-ttu-id="017a9-112">中文（简体）</span><span class="sxs-lookup"><span data-stu-id="017a9-112">Chinese (Simplified)</span></span>
1. <span data-ttu-id="017a9-113">和 SharePoint 2010 显示的“中文(繁体)”</span><span class="sxs-lookup"><span data-stu-id="017a9-113">Chinese (Traditional)</span></span>
1. <span data-ttu-id="017a9-114">捷克语</span><span class="sxs-lookup"><span data-stu-id="017a9-114">Czech</span></span>
1. <span data-ttu-id="017a9-115">英语</span><span class="sxs-lookup"><span data-stu-id="017a9-115">English</span></span>
1. <span data-ttu-id="017a9-116">法语</span><span class="sxs-lookup"><span data-stu-id="017a9-116">French</span></span>
1. <span data-ttu-id="017a9-117">德语</span><span class="sxs-lookup"><span data-stu-id="017a9-117">German</span></span>
1. <span data-ttu-id="017a9-118">意大利语</span><span class="sxs-lookup"><span data-stu-id="017a9-118">Italian</span></span>
1. <span data-ttu-id="017a9-119">日语</span><span class="sxs-lookup"><span data-stu-id="017a9-119">Japanese</span></span>
1. <span data-ttu-id="017a9-120">朝鲜语</span><span class="sxs-lookup"><span data-stu-id="017a9-120">Korean</span></span>
1. <span data-ttu-id="017a9-121">波兰语</span><span class="sxs-lookup"><span data-stu-id="017a9-121">Polish</span></span>
1. <span data-ttu-id="017a9-122">葡萄牙语(巴西)</span><span class="sxs-lookup"><span data-stu-id="017a9-122">Portuguese (Brazil)</span></span>
1. <span data-ttu-id="017a9-123">俄语</span><span class="sxs-lookup"><span data-stu-id="017a9-123">Russian</span></span>
1. <span data-ttu-id="017a9-124">西班牙语</span><span class="sxs-lookup"><span data-stu-id="017a9-124">Spanish</span></span>
1. <span data-ttu-id="017a9-125">土耳其语</span><span class="sxs-lookup"><span data-stu-id="017a9-125">Turkish</span></span>

## <a name="visual-studio-templates-support-multiple-preinstalled-package-repositories"></a><span data-ttu-id="017a9-126">Visual Studio 模板支持多个预安装的包存储库</span><span class="sxs-lookup"><span data-stu-id="017a9-126">Visual Studio Templates Support Multiple Preinstalled Package Repositories</span></span>
<span data-ttu-id="017a9-127">如果生成 Visual Studio 模板，则可以使用 NuGet[预安装包](../visual-studio-extensibility/visual-studio-templates.md)作为模板的一部分。</span><span class="sxs-lookup"><span data-stu-id="017a9-127">If you produce Visual Studio templates, you can use NuGet to [preinstall packages](../visual-studio-extensibility/visual-studio-templates.md) as part of the template.</span></span>  <span data-ttu-id="017a9-128">到目前为止，此功能有限制的所有包需要来自同一源。</span><span class="sxs-lookup"><span data-stu-id="017a9-128">Until now, this feature had a limitation that all of the packages needed to come from the same source.</span></span>  <span data-ttu-id="017a9-129">使用 NuGet 2.2.1 不过，您可以从多个存储库 （在模板中，VSIX 或在注册表中定义的磁盘上的文件夹） 安装的包。</span><span class="sxs-lookup"><span data-stu-id="017a9-129">With NuGet 2.2.1 though, you can have packages installed from multiple repositories (within the template, a VSIX, or a folder on disk defined in the registry).</span></span>

<span data-ttu-id="017a9-130">此功能的主要方案是自定义 ASP.NET 项目模板。</span><span class="sxs-lookup"><span data-stu-id="017a9-130">The main scenario for this feature is custom ASP.NET project templates.</span></span>  <span data-ttu-id="017a9-131">内置的 ASP.NET 模板使用预安装的包，提取程序包从本地磁盘。</span><span class="sxs-lookup"><span data-stu-id="017a9-131">The built-in ASP.NET templates use preinstalled packages, pulling packages from local disk.</span></span>  <span data-ttu-id="017a9-132">现在，您可以创建使用 ASP.NET 所安装的现有包的自定义 ASP.NET 项目模板，但将额外的 NuGet 包添加到你的模板。</span><span class="sxs-lookup"><span data-stu-id="017a9-132">You can now create a custom ASP.NET project template that uses the existing packages installed by ASP.NET but add extra NuGet packages into your template.</span></span>

## <a name="bug-fixes"></a><span data-ttu-id="017a9-133">Bug 修复</span><span class="sxs-lookup"><span data-stu-id="017a9-133">Bug Fixes</span></span>
<span data-ttu-id="017a9-134">NuGet 2.2.1 包含几个目标的 bug 修补程序。</span><span class="sxs-lookup"><span data-stu-id="017a9-134">NuGet 2.2.1 includes a few targeted bug fixes.</span></span> <span data-ttu-id="017a9-135">有关工作的列表项中已修复 NuGet 2.2.1，请查看[对于此版本的 NuGet 问题跟踪程序](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Closed&type=All&priority=All&release=NuGet%202.2.1&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0)。</span><span class="sxs-lookup"><span data-stu-id="017a9-135">For a list of work items fixed in NuGet 2.2.1, please view the [NuGet Issue Tracker for this release](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Closed&type=All&priority=All&release=NuGet%202.2.1&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0).</span></span>


## <a name="known-issues"></a><span data-ttu-id="017a9-136">已知问题</span><span class="sxs-lookup"><span data-stu-id="017a9-136">Known Issues</span></span>

<span data-ttu-id="017a9-137">当扩展 ASP.NET 项目模板，所有预安装的包存储库必须使用相同的值为`isPreunzipped`属性。</span><span class="sxs-lookup"><span data-stu-id="017a9-137">If you are extending ASP.NET project templates, all preinstalled package repositories must use the same value for the `isPreunzipped` attribute.</span></span>
