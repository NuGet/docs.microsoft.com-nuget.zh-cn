---
title: ID 前缀保留引用
description: 包 ID 前缀保留功能说明和作者指南。
author: diverdan92
ms.author: diverdan92
ms.date: 10/09/2017
ms.topic: reference
ms.reviewer: ananguar
ms.openlocfilehash: e8b902c89427333afb7a27ee9de0eeb99a92f391
ms.sourcegitcommit: 571644118e3c5a2fd818891d305b4b8de8ef21de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/02/2019
ms.locfileid: "57225870"
---
# <a name="package-id-prefix-reservation"></a><span data-ttu-id="4277b-103">包 ID 前缀保留</span><span class="sxs-lookup"><span data-stu-id="4277b-103">Package ID prefix reservation</span></span>

<span data-ttu-id="4277b-104">包所有者可保留，并通过保留 ID 前缀来保护其标识。</span><span class="sxs-lookup"><span data-stu-id="4277b-104">Package owners can reserve and protect their identity by reserving ID prefixes.</span></span> <span data-ttu-id="4277b-105">包使用者都是提供的其他信息时使用包，它们使用的包不是欺骗其标识的属性中。</span><span class="sxs-lookup"><span data-stu-id="4277b-105">Package consumers are provided with additional information when consuming packages that the package they are consuming are not deceptive in their identifying properties.</span></span> 

<span data-ttu-id="4277b-106">[nuget.org](https://www.nuget.org/)和 Visual Studio 2017 版本 15.4 或更高版本的包所有者具有保留的包 ID 前缀，前提是保留的 ID 相匹配的包提交前缀的命名模式显示可视的指示器。</span><span class="sxs-lookup"><span data-stu-id="4277b-106">[nuget.org](https://www.nuget.org/) and Visual Studio 2017 version 15.4 or later show a visual indicator for packages that are submitted by owners with a reserved package ID prefix, as long as the package matches the reserved ID prefix naming pattern.</span></span> <span data-ttu-id="4277b-107">参考以下说明 ID 前缀保留的需要，以及如何将所有者可以应用 ID 前缀。</span><span class="sxs-lookup"><span data-stu-id="4277b-107">The below reference explains what the ID prefix reservation entails, and how an owner can apply for an ID prefix.</span></span>

## <a name="id-prefix-reservation-details"></a><span data-ttu-id="4277b-108">ID 前缀保留详细信息</span><span class="sxs-lookup"><span data-stu-id="4277b-108">ID prefix reservation details</span></span>

<span data-ttu-id="4277b-109">保留包 ID 前缀后上, 会发生以下情况[nuget.org](https://www.nuget.org/)库，如 Visual Studio 中所示。</span><span class="sxs-lookup"><span data-stu-id="4277b-109">When a package ID prefix is reserved, several things happen on the [nuget.org](https://www.nuget.org/) gallery, as well as in Visual Studio.</span></span> <span data-ttu-id="4277b-110">此外，一些高级的方案支持的 ID 前缀保留项，例如，设置为 public，将前缀子集委派给多个所有者的前缀。</span><span class="sxs-lookup"><span data-stu-id="4277b-110">In addition, there are advanced scenarios that are supported by ID prefix reservations, such as setting a prefix as 'public', delegating prefix subsets to multiple owners.</span></span>

### <a name="id-prefix-reservation-on-nugetorg"></a><span data-ttu-id="4277b-111">在 nuget.org 上的 ID 前缀保留</span><span class="sxs-lookup"><span data-stu-id="4277b-111">ID prefix reservation on nuget.org</span></span>

<span data-ttu-id="4277b-112">当上保留前缀[nuget.org](https://www.nuget.org/)，将发生以下情况：</span><span class="sxs-lookup"><span data-stu-id="4277b-112">When a prefix is reserved on [nuget.org](https://www.nuget.org/), the following will happen:</span></span>

1. <span data-ttu-id="4277b-113">前缀保留相关联的所有者或组的所有者与上[nuget.org](https://www.nuget.org/)。</span><span class="sxs-lookup"><span data-stu-id="4277b-113">A prefix reservation is associated with an owner or set of owners on [nuget.org](https://www.nuget.org/).</span></span>

1. <span data-ttu-id="4277b-114">每当包提交给[nuget.org](https://www.nuget.org/) id 相匹配的保留的 ID 前缀，包被拒绝，除非它来自保留 ID 前缀的所有者。</span><span class="sxs-lookup"><span data-stu-id="4277b-114">Whenever a package is submitted to [nuget.org](https://www.nuget.org/) with an ID that matches the reserved ID prefix, the package is rejected unless it originates from the owner(s) that reserved the ID prefix.</span></span>

1. <span data-ttu-id="4277b-115">匹配保留的 ID 前缀和源自所有者的 ID 前缀保留的任何包将在 Visual Studio 2017 版本 15.4 或更高版本，以及具有可视的指示器[nuget.org](https://www.nuget.org/) ，该值指示包正在保留的 ID 前缀。</span><span class="sxs-lookup"><span data-stu-id="4277b-115">Any package that matches the reserved ID prefix and originates from the owner(s) that reserved the ID prefix will have a visual indicator in Visual Studio 2017 version 15.4 or later, and on [nuget.org](https://www.nuget.org/) indicating that the package is under a reserved ID prefix.</span></span> <span data-ttu-id="4277b-116">这适用于新的包提交以及在所有者下的现有包。</span><span class="sxs-lookup"><span data-stu-id="4277b-116">This is true for both new package submissions as well as existing packages under the owner(s).</span></span> <span data-ttu-id="4277b-117">**注意：** 仅当单个源选择作为数据包来源，将显示 Visual Studio 中的指示符。</span><span class="sxs-lookup"><span data-stu-id="4277b-117">**Note:** The indicator in Visual Studio appears only if a single feed is selected as the package source.</span></span>

1. <span data-ttu-id="4277b-118">所有先前存在的包相匹配的保留的 ID 前缀，但都*不*的保留所有者所拥有的前缀将保持不变 （它们将不会取消列出，但它们还将不具有可视的指示器）。</span><span class="sxs-lookup"><span data-stu-id="4277b-118">All previously existing packages that match the reserved ID prefix, but are *not* owned by the owner of the reserved prefix will remain unchanged (they will not be unlisted, but they will also not have the visual indicator).</span></span> <span data-ttu-id="4277b-119">此外，这些包的所有者将仍能够提交到包的新版本。</span><span class="sxs-lookup"><span data-stu-id="4277b-119">In addition, owners of these packages will still be able to submit new versions to the package.</span></span>

<span data-ttu-id="4277b-120">这些更改基于以下条件，并且有多个附加限制：</span><span class="sxs-lookup"><span data-stu-id="4277b-120">These changes are based on the following conditions and impose several additional restrictions:</span></span>

- <span data-ttu-id="4277b-121">只有一个所有者的包需要具有可视的指示器显示 （适用于具有多个所有者的包） 的保留的前缀。</span><span class="sxs-lookup"><span data-stu-id="4277b-121">Only one owner of a package needs to have the reserved prefix for the visual indicator to appear (for packages with multiple-owners).</span></span>

- <span data-ttu-id="4277b-122">如果有多个包，一个或多个所有者具有保留的前缀，而一个或多个所有者不具有保留的前缀的所有者，仅保留的前缀与所有者可以删除其他所有者使用保留的前缀。</span><span class="sxs-lookup"><span data-stu-id="4277b-122">If there is more than one owner of a package where one or more owners has the reserved prefix and one or more owners does not have the reserved prefix, then only the owner(s) with the reserved prefix can remove other owner(s) with a reserved prefix.</span></span> <span data-ttu-id="4277b-123">所有者不具有保留的前缀不能删除以保留前缀的所有者。</span><span class="sxs-lookup"><span data-stu-id="4277b-123">The owners who do not have the prefix reserved cannot remove owners with the prefix reserved.</span></span> <span data-ttu-id="4277b-124">他们仍可以删除其他所有者也不具有保留的前缀。</span><span class="sxs-lookup"><span data-stu-id="4277b-124">They can still remove other owners that also do not have the prefix reserved.</span></span>

- <span data-ttu-id="4277b-125">后一个包具有可视的指示器，它应*始终*具有可视的指示器 （保证与保留的前缀，至少一个所有者始终将保持所有者）</span><span class="sxs-lookup"><span data-stu-id="4277b-125">Once a package has the visual indicator, it should *always* have the visual indicator (guaranteeing that at least one owner with the reserved prefix will always remain an owner)</span></span>

### <a name="advanced-prefix-reservation-scenarios"></a><span data-ttu-id="4277b-126">高级的前缀保留方案</span><span class="sxs-lookup"><span data-stu-id="4277b-126">Advanced prefix reservation scenarios</span></span>

<span data-ttu-id="4277b-127">有更高级的多个前缀保留方案如下所述包括 subprefix 委派和为公共的标记前缀。</span><span class="sxs-lookup"><span data-stu-id="4277b-127">There are several more advanced prefix reservation scenarios described below, including subprefix delegation, and marking prefixes as public.</span></span> <span data-ttu-id="4277b-128">以下是可以进行更高级的前缀保留项。</span><span class="sxs-lookup"><span data-stu-id="4277b-128">Below are the more advanced prefix reservations that can be made.</span></span> 

- <span data-ttu-id="4277b-129">在前缀保留命令可以委派前缀子集 （或前缀） 到其他所有者请求所有者。</span><span class="sxs-lookup"><span data-stu-id="4277b-129">During prefix reservation, the owner can request delegation of prefix subsets (or the prefix) to other owners.</span></span> <span data-ttu-id="4277b-130">例如，如果 '[Microsoft](https://www.nuget.org/profiles/microsoft)拥有 Microsoft。\*，但[aspnet](https://www.nuget.org/profiles/aspnet)想要保留 Microsoft.AspNet。\*'，'[Microsoft](https://www.nuget.org/profiles/microsoft)可以选择委派 Microsoft.AspNet。\*到[aspnet](https://www.nuget.org/profiles/aspnet)帐户。</span><span class="sxs-lookup"><span data-stu-id="4277b-130">For example, if '[Microsoft](https://www.nuget.org/profiles/microsoft)' owns 'Microsoft.\*', but '[aspnet](https://www.nuget.org/profiles/aspnet)' wants to reserve 'Microsoft.AspNet.\*', '[Microsoft](https://www.nuget.org/profiles/microsoft)' can choose to delegate 'Microsoft.AspNet.\*' to the [aspnet](https://www.nuget.org/profiles/aspnet) account.</span></span>

- <span data-ttu-id="4277b-131">在前缀保留所有者可以选择公开一个前缀。</span><span class="sxs-lookup"><span data-stu-id="4277b-131">During prefix reservation, the owner can choose to make a prefix public.</span></span> <span data-ttu-id="4277b-132">这将仍为其提供包源自保留的前缀，但它将显示可视的指示器**不**阻止未来的程序包提交前缀上的任何所有者。</span><span class="sxs-lookup"><span data-stu-id="4277b-132">This will still give them the visual indicator showing that the package originates from a reserved prefix, but it will **not** block future package submissions on the prefix for any owner.</span></span> <span data-ttu-id="4277b-133">这是可用于对开放源代码项目具有很多参与者-顶部或核心参与者可以具有前缀保留，但它仍可能会受到所有 contributors （参与者）。</span><span class="sxs-lookup"><span data-stu-id="4277b-133">This is useful for open source projects with many contributors - the top or core contributors can have the prefix reserved, but it can still be open to all contributors.</span></span> 

### <a name="prefix-reservation-visual-indicator"></a><span data-ttu-id="4277b-134">前缀保留可视的指示器</span><span class="sxs-lookup"><span data-stu-id="4277b-134">Prefix reservation visual indicator</span></span>

<span data-ttu-id="4277b-135">当包从保留的前缀，您可以看到如下上的可视指示符[nuget.org](https://www.nuget.org/)库和 Visual Studio 2017 版本 15.4 或更高版本中：</span><span class="sxs-lookup"><span data-stu-id="4277b-135">When a package comes from a reserved prefix, you see the below visual indicators on the [nuget.org](https://www.nuget.org/) gallery and in Visual Studio 2017 version 15.4 or later:</span></span>

<span data-ttu-id="4277b-136">**nuget.org 库**
![nuget.org 库](media/nuget-gallery-reserved-prefix.png)</span><span class="sxs-lookup"><span data-stu-id="4277b-136">**nuget.org Gallery**
![nuget.org Gallery](media/nuget-gallery-reserved-prefix.png)</span></span>

<span data-ttu-id="4277b-137">**Visual Studio**
![Visual Studio](media/visual-studio-reserved-prefix.png)</span><span class="sxs-lookup"><span data-stu-id="4277b-137">**Visual Studio**
![Visual Studio](media/visual-studio-reserved-prefix.png)</span></span>

## <a name="id-prefix-reservation-application-process"></a><span data-ttu-id="4277b-138">ID 前缀保留应用程序进程</span><span class="sxs-lookup"><span data-stu-id="4277b-138">ID prefix reservation application process</span></span>

1. <span data-ttu-id="4277b-139">查看验收[为前缀 ID 预订条件](#id-prefix-reservation-criteria)。</span><span class="sxs-lookup"><span data-stu-id="4277b-139">Review the acceptance [criteria for prefix ID reservation](#id-prefix-reservation-criteria).</span></span>

2. <span data-ttu-id="4277b-140">确定你想要保留，以及任何的前缀[高级前缀保留方案](#advanced-prefix-reservation-scenarios)，你可能需要。</span><span class="sxs-lookup"><span data-stu-id="4277b-140">Determine the prefixes you want to reserve, in addition to any [advanced prefix reservation scenarios](#advanced-prefix-reservation-scenarios) you may require.</span></span>

3. <span data-ttu-id="4277b-141">发送到邮件[ account@nuget.org ](mailto:account@nuget.org)与所有者上显示名称[nuget.org](https://www.nuget.org/)，以及正在请求任何保留前缀。</span><span class="sxs-lookup"><span data-stu-id="4277b-141">Send a mail to [account@nuget.org](mailto:account@nuget.org) with the owner display name on [nuget.org](https://www.nuget.org/), as well as any reserved prefixes you are requesting.</span></span> <span data-ttu-id="4277b-142">如果您前缀子集委派到多个所有者，请确保提及所有所有者显示名称和前缀子集。</span><span class="sxs-lookup"><span data-stu-id="4277b-142">If you are delegating prefix subsets to multiple owners, make sure you mention all owner display names and prefix subsets.</span></span>

<span data-ttu-id="4277b-143">提交应用程序后，会接受或拒绝 （具有导致拒绝的条件） 的通知你。</span><span class="sxs-lookup"><span data-stu-id="4277b-143">After the application is submitted, you are notified of acceptance or rejection (with the criteria that caused rejection).</span></span> <span data-ttu-id="4277b-144">我们可能需要询问其他标识问题，以确认所有者身份。</span><span class="sxs-lookup"><span data-stu-id="4277b-144">We may need to ask additional identifying questions to confirm owner identity.</span></span>

### <a name="id-prefix-reservation-criteria"></a><span data-ttu-id="4277b-145">ID 前缀保留标准</span><span class="sxs-lookup"><span data-stu-id="4277b-145">ID prefix reservation criteria</span></span>

<span data-ttu-id="4277b-146">评审 ID 前缀保留任何应用程序时[nuget.org](https://www.nuget.org/)团队会评估将应用程序与以下条件。</span><span class="sxs-lookup"><span data-stu-id="4277b-146">When reviewing any application for ID prefix reservation, the [nuget.org](https://www.nuget.org/) team will evaluate the application against the below criteria.</span></span> <span data-ttu-id="4277b-147">不是所有条件都需要满足的前缀保留，但如果不存在大量证据的条件得到满足 （以及给定的说明），可能会拒绝应用程序：</span><span class="sxs-lookup"><span data-stu-id="4277b-147">Not all criteria needs to be met for a prefix to be reserved, but the application may be denied if there is not substantial evidence of the criteria being met (with an explanation given):</span></span>

1. <span data-ttu-id="4277b-148">没有包 ID 前缀正确并清楚地标识包所有者？</span><span class="sxs-lookup"><span data-stu-id="4277b-148">Does the package ID prefix properly and clearly identify the package owner?</span></span>

1. <span data-ttu-id="4277b-149">大量的已提交的包的包 ID 前缀下的所有者？</span><span class="sxs-lookup"><span data-stu-id="4277b-149">Are a significant number of the packages that have already been submitted by the owner under the package ID prefix?</span></span>

1. <span data-ttu-id="4277b-150">包 ID 前缀是很常见，不应属于的任何单个所有者或组织？</span><span class="sxs-lookup"><span data-stu-id="4277b-150">Is the package ID prefix something common that should not belong to any individual owner or organization?</span></span>

1. <span data-ttu-id="4277b-151">将*不*保留包 ID 前缀导致二义性和社区的困惑吗？</span><span class="sxs-lookup"><span data-stu-id="4277b-151">Would *not* reserving the package ID prefix cause ambiguity and confusion for the community?</span></span>

1. <span data-ttu-id="4277b-152">是与匹配的包 ID 前缀清晰、 一致 （尤其是包的作者） 的程序包的标识属性？</span><span class="sxs-lookup"><span data-stu-id="4277b-152">Are the identifying properties of the packages that match the package ID prefix clear and consistent (especially the package author)?</span></span>

1. <span data-ttu-id="4277b-153">执行包具有的许可证 (使用[许可证](https://docs.microsoft.com/en-us/nuget/reference/nuspec#license)元数据元素，并不将被弃用的 licenseUrl)？</span><span class="sxs-lookup"><span data-stu-id="4277b-153">Do the packages have a license (using the [license](https://docs.microsoft.com/en-us/nuget/reference/nuspec#license) metadata element and NOT licenseUrl which is being deprecated)?</span></span>

## <a name="third-party-feed-provider-scenarios"></a><span data-ttu-id="4277b-154">第三方源提供程序方案</span><span class="sxs-lookup"><span data-stu-id="4277b-154">Third party feed provider scenarios</span></span>

<span data-ttu-id="4277b-155">如果第三方源提供程序是有意实施其自己的服务来提供前缀保留项，可以执行以便 NuGet V3 中的搜索服务通过修改源提供程序。</span><span class="sxs-lookup"><span data-stu-id="4277b-155">If a third party feed provider is interested in implementing their own service to provide prefix reservations, you can do so by modifying the search service in the NuGet V3 feed providers.</span></span> <span data-ttu-id="4277b-156">源的搜索服务中的功能是将添加*验证*属性，并提供 V3 源下面的示例。</span><span class="sxs-lookup"><span data-stu-id="4277b-156">The addition in the feed search service is to add the *verified* property, with examples for the V3 feeds below.</span></span> <span data-ttu-id="4277b-157">NuGet 客户端将不支持在源 V2 中添加的属性。</span><span class="sxs-lookup"><span data-stu-id="4277b-157">The NuGet client will not support the added property in the V2 feed.</span></span>

<span data-ttu-id="4277b-158">有关详细信息，请参阅[有关 API 的搜索服务的文档](../api/search-query-service-resource.md)。</span><span class="sxs-lookup"><span data-stu-id="4277b-158">For more information, see the [documentation about the API's search service](../api/search-query-service-resource.md).</span></span>

## <a name="package-id-prefix-reservation-dispute-policy"></a><span data-ttu-id="4277b-159">包 ID 前缀保留争议策略</span><span class="sxs-lookup"><span data-stu-id="4277b-159">Package ID Prefix Reservation Dispute Policy</span></span>
<span data-ttu-id="4277b-160">如果你在认为所有者[NuGet.org](https://www.nuget.org)分配就不符合上述列出的条件，或侵犯任何商标或版权请电子邮件的包 ID 前缀保留[ support@nuget.org ](mailto:support@nuget.org)与有问题的 ID 前缀，所有者 ID 前缀，以及已分配的前缀保留争议的原因。</span><span class="sxs-lookup"><span data-stu-id="4277b-160">If you believe an owner on [NuGet.org](https://www.nuget.org) was assigned a package ID prefix reservation that goes against the above listed criteria, or infringes on any trademarks or copyrights, please email [support@nuget.org](mailto:support@nuget.org) with the ID prefix in question, the owner of the ID prefix, and the reason for disputing the assigned prefix reservation.</span></span>

