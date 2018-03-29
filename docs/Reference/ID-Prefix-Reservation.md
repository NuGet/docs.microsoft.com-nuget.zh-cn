---
title: ID 前缀保留引用 |Microsoft 文档
author: diverdan92
ms.author: diverdan92
manager: unniravindranathan
ms.date: 10/09/2017
ms.topic: reference
ms.prod: nuget
ms.technology: ''
description: 包 ID 前缀保留功能说明和作者指南。
keywords: NuGet 包 ID、 前缀、 保留
ms.reviewer:
- ananguar
- karann-msft
- unniravindranathan
ms.workload:
- dotnet
- aspnet
ms.openlocfilehash: 7b1956612bd48a1c59503418f1a4d7d9dee900f5
ms.sourcegitcommit: beb229893559824e8abd6ab16707fd5fe1c6ac26
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/28/2018
---
# <a name="package-id-prefix-reservation"></a><span data-ttu-id="47b83-104">包 ID 前缀保留</span><span class="sxs-lookup"><span data-stu-id="47b83-104">Package ID prefix reservation</span></span>

<span data-ttu-id="47b83-105">包所有者可以保留，并通过保留 ID 前缀来保护其标识。</span><span class="sxs-lookup"><span data-stu-id="47b83-105">Package owners can reserve and protect their identity by reserving ID prefixes.</span></span> <span data-ttu-id="47b83-106">包使用者会提供其他信息时使用包，它们使用的包不在其标识属性欺骗性。</span><span class="sxs-lookup"><span data-stu-id="47b83-106">Package consumers are provided with additional information when consuming packages that the package they are consuming are not deceptive in their identifying properties.</span></span> 

<span data-ttu-id="47b83-107">[nuget.org](https://www.nuget.org/)和 Visual Studio 2017 15.4 或更高版本的包，只要包与匹配的保留的 ID 提交由所有者具有保留的包 ID 前缀，前缀的命名模式显示可视的指示器。</span><span class="sxs-lookup"><span data-stu-id="47b83-107">[nuget.org](https://www.nuget.org/) and Visual Studio 2017 version 15.4 or later show a visual indicator for packages that are submitted by owners with a reserved package ID prefix, as long as the package matches the reserved ID prefix naming pattern.</span></span> <span data-ttu-id="47b83-108">下引用介绍 ID 前缀保留的需要，以及如何所有者可以将应用 ID 前缀。</span><span class="sxs-lookup"><span data-stu-id="47b83-108">The below reference explains what the ID prefix reservation entails, and how an owner can apply for an ID prefix.</span></span>

## <a name="id-prefix-reservation-details"></a><span data-ttu-id="47b83-109">ID 前缀保留详细信息</span><span class="sxs-lookup"><span data-stu-id="47b83-109">ID prefix reservation details</span></span>

<span data-ttu-id="47b83-110">保留包 ID 前缀后，将在发生下列情况[nuget.org](https://www.nuget.org/)库，以及如 Visual Studio 中所示。</span><span class="sxs-lookup"><span data-stu-id="47b83-110">When a package ID prefix is reserved, several things happen on the [nuget.org](https://www.nuget.org/) gallery, as well as in Visual Studio.</span></span> <span data-ttu-id="47b83-111">此外，一些高级支持由 ID 前缀保留项，如设置为 'public' 前缀将前缀子集委托给多个所有者的方案。</span><span class="sxs-lookup"><span data-stu-id="47b83-111">In addition, there are advanced scenarios that are supported by ID prefix reservations, such as setting a prefix as 'public', delegating prefix subsets to multiple owners.</span></span>

### <a name="id-prefix-reservation-on-nugetorg"></a><span data-ttu-id="47b83-112">在 nuget.org 上的 ID 前缀保留</span><span class="sxs-lookup"><span data-stu-id="47b83-112">ID prefix reservation on nuget.org</span></span>

<span data-ttu-id="47b83-113">当前缀会保留在[nuget.org](https://www.nuget.org/)，将发生以下情况：</span><span class="sxs-lookup"><span data-stu-id="47b83-113">When a prefix is reserved on [nuget.org](https://www.nuget.org/), the following will happen:</span></span>

1. <span data-ttu-id="47b83-114">前缀保留关联的所有者或所有者的组上[nuget.org](https://www.nuget.org/)。</span><span class="sxs-lookup"><span data-stu-id="47b83-114">A prefix reservation is associated with an owner or set of owners on [nuget.org](https://www.nuget.org/).</span></span>

1. <span data-ttu-id="47b83-115">每当包提交到[nuget.org](https://www.nuget.org/) id 相匹配的保留的 ID 前缀，包被拒绝，除非它来自所有者保留 ID 前缀。</span><span class="sxs-lookup"><span data-stu-id="47b83-115">Whenever a package is submitted to [nuget.org](https://www.nuget.org/) with an ID that matches the reserved ID prefix, the package is rejected unless it originates from the owner(s) that reserved the ID prefix.</span></span>

1. <span data-ttu-id="47b83-116">与匹配的保留的 ID 前缀，并源自保留 ID 前缀所有者的任何包将具有的可视指示器，在 Visual Studio 2017 版本 15.4 或更高版本，和上[nuget.org](https://www.nuget.org/) ，该值指示包正在保留的 ID 前缀。</span><span class="sxs-lookup"><span data-stu-id="47b83-116">Any package that matches the reserved ID prefix and originates from the owner(s) that reserved the ID prefix will have a visual indicator in Visual Studio 2017 version 15.4 or later, and on [nuget.org](https://www.nuget.org/) indicating that the package is under a reserved ID prefix.</span></span> <span data-ttu-id="47b83-117">这适用于新的包提交以及在所有者下的现有包。</span><span class="sxs-lookup"><span data-stu-id="47b83-117">This is true for both new package submissions as well as existing packages under the owner(s).</span></span> <span data-ttu-id="47b83-118">**注意：**仅当单个源选择作为包源，将显示在 Visual Studio 中的指示器。</span><span class="sxs-lookup"><span data-stu-id="47b83-118">**Note:** The indicator in Visual Studio appears only if a single feed is selected as the package source.</span></span>

1. <span data-ttu-id="47b83-119">所有先前存在的包与匹配的保留的 ID 前缀，但都*不*拥有保留的所有者的前缀将保持不变 （它们不会未列出，但它们还将不具有可视的指示器）。</span><span class="sxs-lookup"><span data-stu-id="47b83-119">All previously existing packages that match the reserved ID prefix, but are *not* owned by the owner of the reserved prefix will remain unchanged (they will not be unlisted, but they will also not have the visual indicator).</span></span> <span data-ttu-id="47b83-120">此外，这些包的所有者将仍能够提交到包的新版本。</span><span class="sxs-lookup"><span data-stu-id="47b83-120">In addition, owners of these packages will still be able to submit new versions to the package.</span></span>

<span data-ttu-id="47b83-121">这些更改基于以下条件，并且有多个附加限制：</span><span class="sxs-lookup"><span data-stu-id="47b83-121">These changes are based on the following conditions and impose several additional restrictions:</span></span>

- <span data-ttu-id="47b83-122">只有一个所有者的包需要具有可视的指示器，显示 （对于与多个所有者的包） 的保留的前缀。</span><span class="sxs-lookup"><span data-stu-id="47b83-122">Only one owner of a package needs to have the reserved prefix for the visual indicator to appear (for packages with multiple-owners).</span></span>

- <span data-ttu-id="47b83-123">如果没有的包其中一个或多个所有者具有保留的前缀和一个或多个所有者不具有保留的前缀的多个所有者，仅保留前缀与所有者可以删除以保留前缀其他所有者。</span><span class="sxs-lookup"><span data-stu-id="47b83-123">If there is more than one owner of a package where one or more owners has the reserved prefix and one or more owners does not have the reserved prefix, then only the owner(s) with the reserved prefix can remove other owner(s) with a reserved prefix.</span></span> <span data-ttu-id="47b83-124">而在不具有保留的前缀的所有者不能删除以保留前缀的所有者。</span><span class="sxs-lookup"><span data-stu-id="47b83-124">The owners who do not have the prefix reserved cannot remove owners with the prefix reserved.</span></span> <span data-ttu-id="47b83-125">他们仍可以删除还没有保留的前缀其他所有者。</span><span class="sxs-lookup"><span data-stu-id="47b83-125">They can still remove other owners that also do not have the prefix reserved.</span></span>

- <span data-ttu-id="47b83-126">可视的指示器包后，它应*始终*具有可视的指示器 （保留前缀与该至少一个所有者，从而保证始终将保留所有者）</span><span class="sxs-lookup"><span data-stu-id="47b83-126">Once a package has the visual indicator, it should *always* have the visual indicator (guaranteeing that at least one owner with the reserved prefix will always remain an owner)</span></span>

### <a name="advanced-prefix-reservation-scenarios"></a><span data-ttu-id="47b83-127">高级的前缀保留方案</span><span class="sxs-lookup"><span data-stu-id="47b83-127">Advanced prefix reservation scenarios</span></span>

<span data-ttu-id="47b83-128">有更高级的几种前缀保留方案下面所述，包括 subprefix 委派，并为公共的标记前缀。</span><span class="sxs-lookup"><span data-stu-id="47b83-128">There are several more advanced prefix reservation scenarios described below, including subprefix delegation, and marking prefixes as public.</span></span> <span data-ttu-id="47b83-129">以下是可以进行更高级的前缀保留。</span><span class="sxs-lookup"><span data-stu-id="47b83-129">Below are the more advanced prefix reservations that can be made.</span></span> 

- <span data-ttu-id="47b83-130">在前缀保留过程所有者可以请求的前缀子集委派 （或前缀） 到其他所有者。</span><span class="sxs-lookup"><span data-stu-id="47b83-130">During prefix reservation, the owner can request delegation of prefix subsets (or the prefix) to other owners.</span></span> <span data-ttu-id="47b83-131">例如，如果[Microsoft](https://www.nuget.org/profiles/microsoft)拥有 Microsoft。\*，但[aspnet](https://www.nuget.org/profiles/aspnet)想要保留 Microsoft.AspNet。\*'，'[Microsoft](https://www.nuget.org/profiles/microsoft)可以选择委派 Microsoft.AspNet。\*到[aspnet](https://www.nuget.org/profiles/aspnet)帐户。</span><span class="sxs-lookup"><span data-stu-id="47b83-131">For example, if '[Microsoft](https://www.nuget.org/profiles/microsoft)' owns 'Microsoft.\*', but '[aspnet](https://www.nuget.org/profiles/aspnet)' wants to reserve 'Microsoft.AspNet.\*', '[Microsoft](https://www.nuget.org/profiles/microsoft)' can choose to delegate 'Microsoft.AspNet.\*' to the [aspnet](https://www.nuget.org/profiles/aspnet) account.</span></span>

- <span data-ttu-id="47b83-132">在前缀保留所有者可以选择公开一个前缀。</span><span class="sxs-lookup"><span data-stu-id="47b83-132">During prefix reservation, the owner can choose to make a prefix public.</span></span> <span data-ttu-id="47b83-133">这将仍为它们可视的指示器显示包源自保留前缀，但它将**不**阻止任何所有者提交的将来的软件包时根据的前缀。</span><span class="sxs-lookup"><span data-stu-id="47b83-133">This will still give them the visual indicator showing that the package originates from a reserved prefix, but it will **not** block future package submissions on the prefix for any owner.</span></span> <span data-ttu-id="47b83-134">这可用于具有很多参与者的开放源代码项目-顶部或核心参与者都可以具有前缀保留，但它仍可以打开到所有 contributors （参与者）。</span><span class="sxs-lookup"><span data-stu-id="47b83-134">This is useful for open source projects with many contributors - the top or core contributors can have the prefix reserved, but it can still be open to all contributors.</span></span> 

### <a name="prefix-reservation-visual-indicator"></a><span data-ttu-id="47b83-135">前缀保留可视的指示器</span><span class="sxs-lookup"><span data-stu-id="47b83-135">Prefix reservation visual indicator</span></span>

<span data-ttu-id="47b83-136">当包来自保留前缀时，你会看到下面直观的指示器上, [nuget.org](https://www.nuget.org/)库和 Visual Studio 2017 15.4 或更高版本中：</span><span class="sxs-lookup"><span data-stu-id="47b83-136">When a package comes from a reserved prefix, you see the below visual indicators on the [nuget.org](https://www.nuget.org/) gallery and in Visual Studio 2017 version 15.4 or later:</span></span>

<span data-ttu-id="47b83-137">**nuget.org 库**
![nuget.org 库](media/nuget-gallery-reserved-prefix.png)</span><span class="sxs-lookup"><span data-stu-id="47b83-137">**nuget.org Gallery**
![nuget.org Gallery](media/nuget-gallery-reserved-prefix.png)</span></span>

<span data-ttu-id="47b83-138">**Visual Studio**
![Visual Studio](media/visual-studio-reserved-prefix.png)</span><span class="sxs-lookup"><span data-stu-id="47b83-138">**Visual Studio**
![Visual Studio](media/visual-studio-reserved-prefix.png)</span></span>

## <a name="id-prefix-reservation-application-process"></a><span data-ttu-id="47b83-139">ID 前缀保留应用程序进程</span><span class="sxs-lookup"><span data-stu-id="47b83-139">ID prefix reservation application process</span></span>

1. <span data-ttu-id="47b83-140">查看验收[前缀 ID 保留条件](#id-prefix-reservation-criteria)。</span><span class="sxs-lookup"><span data-stu-id="47b83-140">Review the acceptance [criteria for prefix ID reservation](#id-prefix-reservation-criteria).</span></span>

1. <span data-ttu-id="47b83-141">确定你想要保留，除了任何命名的空间[高级前缀保留方案](#advanced-prefix-reservation-scenarios)可能需要。</span><span class="sxs-lookup"><span data-stu-id="47b83-141">Determine the namespaces you want to reserve, in addition to any [advanced prefix reservation scenarios](#advanced-prefix-reservation-scenarios) you may require.</span></span>

1. <span data-ttu-id="47b83-142">发送到邮件[ account@nuget.org ](mailto:account@nuget.org)与所有者显示名称上[nuget.org](https://www.nuget.org/)，以及任何您请求的保留前缀。</span><span class="sxs-lookup"><span data-stu-id="47b83-142">Send a mail to [account@nuget.org](mailto:account@nuget.org) with the owner display name on [nuget.org](https://www.nuget.org/), as well as any reserved prefixes you are requesting.</span></span> <span data-ttu-id="47b83-143">如果你的多个所有者分配前缀子集，请确保涉及所有所有者显示名称和前缀子集。</span><span class="sxs-lookup"><span data-stu-id="47b83-143">If you are delegating prefix subsets to multiple owners, make sure you mention all owner display names and prefix subsets.</span></span>

<span data-ttu-id="47b83-144">提交应用程序后，会接受或拒绝 （与导致拒绝的条件） 的通知您。</span><span class="sxs-lookup"><span data-stu-id="47b83-144">After the application is submitted, you are notified of acceptance or rejection (with the criteria that caused rejection).</span></span> <span data-ttu-id="47b83-145">我们可能需要询问其他标识的一些问题，以确认所有者身份。</span><span class="sxs-lookup"><span data-stu-id="47b83-145">We may need to ask additional identifying questions to confirm owner identity.</span></span>

### <a name="id-prefix-reservation-criteria"></a><span data-ttu-id="47b83-146">ID 前缀保留条件</span><span class="sxs-lookup"><span data-stu-id="47b83-146">ID prefix reservation criteria</span></span>

<span data-ttu-id="47b83-147">查看有关 ID 前缀保留任何应用程序时[nuget.org](https://www.nuget.org/)团队将评估针对对应用程序下面条件。</span><span class="sxs-lookup"><span data-stu-id="47b83-147">When reviewing any application for ID prefix reservation, the [nuget.org](https://www.nuget.org/) team will evaluate the application against the below criteria.</span></span> <span data-ttu-id="47b83-148">并非所有条件都需要满足的前缀以保留，但如果不满足 （的给定说明） 的条件的大量证据，应用程序可能会被拒绝：</span><span class="sxs-lookup"><span data-stu-id="47b83-148">Not all criteria needs to be met for a prefix to be reserved, but the application may be denied if there is not substantial evidence of the criteria being met (with an explanation given):</span></span>

1. <span data-ttu-id="47b83-149">没有包 ID 前缀正确并清楚地标识包所有者？</span><span class="sxs-lookup"><span data-stu-id="47b83-149">Does the package ID prefix properly and clearly identify the package owner?</span></span>

1. <span data-ttu-id="47b83-150">按下的包 ID 前缀所有者大量的已提交的包？</span><span class="sxs-lookup"><span data-stu-id="47b83-150">Are a significant number of the packages that have already been submitted by the owner under the package ID prefix?</span></span>

1. <span data-ttu-id="47b83-151">是很常见应不属于任何单个所有者或组织的包 ID 前缀？</span><span class="sxs-lookup"><span data-stu-id="47b83-151">Is the package ID prefix something common that should not belong to any individual owner or organization?</span></span>

1. <span data-ttu-id="47b83-152">将*不*保留的包 ID 前缀导致多义性和社区的困惑？</span><span class="sxs-lookup"><span data-stu-id="47b83-152">Would *not* reserving the package ID prefix cause ambiguity and confusion for the community?</span></span>

1. <span data-ttu-id="47b83-153">是匹配的包 ID 前缀清晰且一致 （尤其是程序包作者） 的包的标识属性？</span><span class="sxs-lookup"><span data-stu-id="47b83-153">Are the identifying properties of the packages that match the package ID prefix clear and consistent (especially the package author)?</span></span>

## <a name="third-party-feed-provider-scenarios"></a><span data-ttu-id="47b83-154">第三方源提供程序方案</span><span class="sxs-lookup"><span data-stu-id="47b83-154">Third party feed provider scenarios</span></span>

<span data-ttu-id="47b83-155">如果第三方源提供程序有兴趣实现其自己的服务提供前缀保留项，你可以执行以便 NuGet V3 中的搜索服务通过修改源提供程序。</span><span class="sxs-lookup"><span data-stu-id="47b83-155">If a third party feed provider is interested in implementing their own service to provide prefix reservations, you can do so by modifying the search service in the NuGet V3 feed providers.</span></span> <span data-ttu-id="47b83-156">源的搜索服务中添加是添加*验证*属性，并提供 V3 源下面的示例。</span><span class="sxs-lookup"><span data-stu-id="47b83-156">The addition in the feed search service is to add the *verified* property, with examples for the V3 feeds below.</span></span> <span data-ttu-id="47b83-157">NuGet 客户端将不支持在 V2 中源添加的属性。</span><span class="sxs-lookup"><span data-stu-id="47b83-157">The NuGet client will not support the added property in the V2 feed.</span></span>

<span data-ttu-id="47b83-158">有关详细信息，请参阅[有关 API 的搜索服务的文档](../api/search-query-service-resource.md)。</span><span class="sxs-lookup"><span data-stu-id="47b83-158">For more information, see the [documentation about the API's search service](../api/search-query-service-resource.md).</span></span>
