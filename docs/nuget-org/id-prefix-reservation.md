---
title: ID 前缀预留
description: 包 ID 前缀预留功能说明和作者指南。
author: karann-msft
ms.author: karann
ms.date: 09/07/2019
ms.topic: reference
ms.reviewer: karann
ms.openlocfilehash: da464cc44d8c874e13c0cdfab871f31e643b577f
ms.sourcegitcommit: 2b50c450cca521681a384aa466ab666679a40213
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/07/2020
ms.locfileid: "73610494"
---
# <a name="package-id-prefix-reservation"></a><span data-ttu-id="c894c-103">包 ID 前缀预留</span><span class="sxs-lookup"><span data-stu-id="c894c-103">Package ID prefix reservation</span></span>

<span data-ttu-id="c894c-104">包所有者可以通过保留 ID 前缀来保留和保护其标识。</span><span class="sxs-lookup"><span data-stu-id="c894c-104">Package owners can reserve and protect their identity by reserving ID prefixes.</span></span> <span data-ttu-id="c894c-105">当使用者使用的包在其标识属性中不具有欺骗性时，他们将收到附加信息。</span><span class="sxs-lookup"><span data-stu-id="c894c-105">Package consumers are provided with additional information when the packages that they are consuming are not deceptive in their identifying properties.</span></span> 

<span data-ttu-id="c894c-106">[nuget.org](https://www.nuget.org/) 和 Visual Studio 2017 15.4 或更高版本只要包与保留的 ID 前缀命名模式匹配，就会显示所有者提交的具有保留的包 ID 前缀的包的视觉提示。</span><span class="sxs-lookup"><span data-stu-id="c894c-106">[nuget.org](https://www.nuget.org/) and Visual Studio 2017 version 15.4 or later show a visual indicator for packages that are submitted by owners with a reserved package ID prefix, as long as the package matches the reserved ID prefix naming pattern.</span></span> <span data-ttu-id="c894c-107">以下参考资料说明了 ID 前缀预留需要的内容，以及所有者如何申请 ID 前缀。</span><span class="sxs-lookup"><span data-stu-id="c894c-107">The below reference explains what the ID prefix reservation entails, and how an owner can apply for an ID prefix.</span></span>

## <a name="id-prefix-reservation-details"></a><span data-ttu-id="c894c-108">ID 前缀预留详细信息</span><span class="sxs-lookup"><span data-stu-id="c894c-108">ID prefix reservation details</span></span>

<span data-ttu-id="c894c-109">保留包 ID 前缀时，在 [nuget.org](https://www.nuget.org/) 库和 Visual Studio 中会发生一些情况。</span><span class="sxs-lookup"><span data-stu-id="c894c-109">When a package ID prefix is reserved, several things happen on the [nuget.org](https://www.nuget.org/) gallery, as well as in Visual Studio.</span></span> <span data-ttu-id="c894c-110">此外，ID 前缀预留还支持一些高级方案，比如将前缀设置为“public”，将前缀子集委托给多个所有者。</span><span class="sxs-lookup"><span data-stu-id="c894c-110">In addition, there are advanced scenarios that are supported by ID prefix reservations, such as setting a prefix as 'public', delegating prefix subsets to multiple owners.</span></span>

### <a name="id-prefix-reservation-on-nugetorg"></a><span data-ttu-id="c894c-111">nuget.org 上的 ID 前缀预留</span><span class="sxs-lookup"><span data-stu-id="c894c-111">ID prefix reservation on nuget.org</span></span>

<span data-ttu-id="c894c-112">在 [nuget.org](https://www.nuget.org/) 上保留前缀时，将发生以下情况：</span><span class="sxs-lookup"><span data-stu-id="c894c-112">When a prefix is reserved on [nuget.org](https://www.nuget.org/), the following will happen:</span></span>

1. <span data-ttu-id="c894c-113">前缀预留与 [nuget.org](https://www.nuget.org/) 上的所有者或所有者组相关。</span><span class="sxs-lookup"><span data-stu-id="c894c-113">A prefix reservation is associated with an owner or set of owners on [nuget.org](https://www.nuget.org/).</span></span>

1. <span data-ttu-id="c894c-114">每当包提交到 ID 与保留的 ID 前缀匹配的 [nuget.org](https://www.nuget.org/) 时，都会拒绝该包，除非它来自已保留 ID 前缀的所有者。</span><span class="sxs-lookup"><span data-stu-id="c894c-114">Whenever a package is submitted to [nuget.org](https://www.nuget.org/) with an ID that matches the reserved ID prefix, the package is rejected unless it originates from the owner(s) that reserved the ID prefix.</span></span>

1. <span data-ttu-id="c894c-115">任何与保留 ID 前缀匹配并来自已保留 ID 前缀的所有者的包将在 Visual Studio 2017 15.4 或更高版本中和在 [nuget.org](https://www.nuget.org/) 上具有视觉提示，指示该包位于保留 ID 前缀下。</span><span class="sxs-lookup"><span data-stu-id="c894c-115">Any package that matches the reserved ID prefix and originates from the owner(s) that reserved the ID prefix will have a visual indicator in Visual Studio 2017 version 15.4 or later, and on [nuget.org](https://www.nuget.org/) indicating that the package is under a reserved ID prefix.</span></span> <span data-ttu-id="c894c-116">提交的新包和所有者名下的现有包都是如此。</span><span class="sxs-lookup"><span data-stu-id="c894c-116">This is true for both new package submissions as well as existing packages under the owner(s).</span></span> <span data-ttu-id="c894c-117">**注意：** 仅当选择单个订阅源作为包来源时，Visual Studio 中才会出现标志。</span><span class="sxs-lookup"><span data-stu-id="c894c-117">**Note:** The indicator in Visual Studio appears only if a single feed is selected as the package source.</span></span>

1. <span data-ttu-id="c894c-118">所有先前存在的包如果与保留 ID 前缀匹配，但不属于保留前缀所有者，则将保持不变（它们依然会被列出，但没有视觉提示）  。</span><span class="sxs-lookup"><span data-stu-id="c894c-118">All previously existing packages that match the reserved ID prefix, but are *not* owned by the owner of the reserved prefix will remain unchanged (they will not be unlisted, but they will also not have the visual indicator).</span></span> <span data-ttu-id="c894c-119">此外，这些包的所有者仍然可以向包提交新版本。</span><span class="sxs-lookup"><span data-stu-id="c894c-119">In addition, owners of these packages will still be able to submit new versions to the package.</span></span>

<span data-ttu-id="c894c-120">这些更改基于以下条件，并附加了一些限制：</span><span class="sxs-lookup"><span data-stu-id="c894c-120">These changes are based on the following conditions and impose several additional restrictions:</span></span>

- <span data-ttu-id="c894c-121">为了显示视觉提示，只有一个包所有者需要保留前缀（适用于具有多个所有者的包）。</span><span class="sxs-lookup"><span data-stu-id="c894c-121">Only one owner of a package needs to have the reserved prefix for the visual indicator to appear (for packages with multiple-owners).</span></span>

- <span data-ttu-id="c894c-122">如果一个包有多个所有者，其中一个或多个所有者具有保留前缀，而一个或多个所有者没有保留前缀，那么只有具有保留前缀的所有者才能移除具有保留前缀的其他所有者。</span><span class="sxs-lookup"><span data-stu-id="c894c-122">If there is more than one owner of a package where one or more owners has the reserved prefix and one or more owners does not have the reserved prefix, then only the owner(s) with the reserved prefix can remove other owner(s) with a reserved prefix.</span></span> <span data-ttu-id="c894c-123">没有保留前缀的所有者无法移除保留了前缀的所有者。</span><span class="sxs-lookup"><span data-stu-id="c894c-123">The owners who do not have the prefix reserved cannot remove owners with the prefix reserved.</span></span> <span data-ttu-id="c894c-124">他们仍然可以移除其他没有保留前缀的所有者。</span><span class="sxs-lookup"><span data-stu-id="c894c-124">They can still remove other owners that also do not have the prefix reserved.</span></span>

- <span data-ttu-id="c894c-125">一旦包具有视觉提示，它应该始终具有视觉提示（确保至少有一个具有保留前缀的所有者始终保持所有者身份） </span><span class="sxs-lookup"><span data-stu-id="c894c-125">Once a package has the visual indicator, it should *always* have the visual indicator (guaranteeing that at least one owner with the reserved prefix will always remain an owner)</span></span>

### <a name="advanced-prefix-reservation-scenarios"></a><span data-ttu-id="c894c-126">高级前缀预留方案</span><span class="sxs-lookup"><span data-stu-id="c894c-126">Advanced prefix reservation scenarios</span></span>

<span data-ttu-id="c894c-127">下面描述了几种更高级的前缀预留方案，包括子前缀委托和将前缀标记为公用。</span><span class="sxs-lookup"><span data-stu-id="c894c-127">There are several more advanced prefix reservation scenarios described below, including subprefix delegation, and marking prefixes as public.</span></span> <span data-ttu-id="c894c-128">以下是可以进行的更高级的前缀预留。</span><span class="sxs-lookup"><span data-stu-id="c894c-128">Below are the more advanced prefix reservations that can be made.</span></span> 

- <span data-ttu-id="c894c-129">在前缀预留期间，所有者可以请求将前缀子集（或前缀）委托给其他所有者。</span><span class="sxs-lookup"><span data-stu-id="c894c-129">During prefix reservation, the owner can request delegation of prefix subsets (or the prefix) to other owners.</span></span> <span data-ttu-id="c894c-130">例如，如果“[Microsoft](https://www.nuget.org/profiles/microsoft)”具有“Microsoft.\*”，但“[aspnet](https://www.nuget.org/profiles/aspnet)”希望保留“Microsoft.AspNet.\*”，则“[Microsoft](https://www.nuget.org/profiles/microsoft)”可以选择将“Microsoft.AspNet.\*”委托给 [aspnet](https://www.nuget.org/profiles/aspnet) 帐户。</span><span class="sxs-lookup"><span data-stu-id="c894c-130">For example, if '[Microsoft](https://www.nuget.org/profiles/microsoft)' owns 'Microsoft.\*', but '[aspnet](https://www.nuget.org/profiles/aspnet)' wants to reserve 'Microsoft.AspNet.\*', '[Microsoft](https://www.nuget.org/profiles/microsoft)' can choose to delegate 'Microsoft.AspNet.\*' to the [aspnet](https://www.nuget.org/profiles/aspnet) account.</span></span>

- <span data-ttu-id="c894c-131">在前缀预留期间，所有者可以选择设置公用前缀。</span><span class="sxs-lookup"><span data-stu-id="c894c-131">During prefix reservation, the owner can choose to make a prefix public.</span></span> <span data-ttu-id="c894c-132">这仍将为他们提供视觉提示，显示包源自保留的前缀，但它以后不会对任何所有者的前缀阻止提交包  。</span><span class="sxs-lookup"><span data-stu-id="c894c-132">This will still give them the visual indicator showing that the package originates from a reserved prefix, but it will **not** block future package submissions on the prefix for any owner.</span></span> <span data-ttu-id="c894c-133">这对于有许多贡献者的开源项目很有用，顶级或核心贡献者可以保留前缀，但它仍然可以向所有贡献者开放。</span><span class="sxs-lookup"><span data-stu-id="c894c-133">This is useful for open source projects with many contributors - the top or core contributors can have the prefix reserved, but it can still be open to all contributors.</span></span> 

### <a name="prefix-reservation-visual-indicator"></a><span data-ttu-id="c894c-134">前缀预留视觉提示</span><span class="sxs-lookup"><span data-stu-id="c894c-134">Prefix reservation visual indicator</span></span>

<span data-ttu-id="c894c-135">当包来自保留前缀时，在 [nuget.org](https://www.nuget.org/) 库和 Visual Studio 2017 15.4 或更高版本中将看到以下视觉提示：</span><span class="sxs-lookup"><span data-stu-id="c894c-135">When a package comes from a reserved prefix, you see the below visual indicators on the [nuget.org](https://www.nuget.org/) gallery and in Visual Studio 2017 version 15.4 or later:</span></span>

<span data-ttu-id="c894c-136">**nuget.org 库**
![nuget.org Gallery](media/nuget-gallery-reserved-prefix.png)</span><span class="sxs-lookup"><span data-stu-id="c894c-136">**nuget.org Gallery**
![nuget.org Gallery](media/nuget-gallery-reserved-prefix.png)</span></span>

<span data-ttu-id="c894c-137">**Visual Studio**
![Visual Studio](media/visual-studio-reserved-prefix.png)</span><span class="sxs-lookup"><span data-stu-id="c894c-137">**Visual Studio**
![Visual Studio](media/visual-studio-reserved-prefix.png)</span></span>

## <a name="id-prefix-reservation-application-process"></a><span data-ttu-id="c894c-138">ID 前缀预留申请过程</span><span class="sxs-lookup"><span data-stu-id="c894c-138">ID prefix reservation application process</span></span>

1. <span data-ttu-id="c894c-139">查看[前缀 ID 预留的验收条件](#id-prefix-reservation-criteria)。</span><span class="sxs-lookup"><span data-stu-id="c894c-139">Review the acceptance [criteria for prefix ID reservation](#id-prefix-reservation-criteria).</span></span>

2. <span data-ttu-id="c894c-140">确定你想预留的前缀，以及可能需要的任何[高级前缀预留方案](#advanced-prefix-reservation-scenarios)。</span><span class="sxs-lookup"><span data-stu-id="c894c-140">Determine the prefixes you want to reserve, in addition to any [advanced prefix reservation scenarios](#advanced-prefix-reservation-scenarios) you may require.</span></span>

3. <span data-ttu-id="c894c-141">使用 [nuget.org](https://www.nuget.org/) 上的所有者显示名称以及你请求的任何保留前缀向 [account@nuget.org](mailto:account@nuget.org) 发送邮件。</span><span class="sxs-lookup"><span data-stu-id="c894c-141">Send a mail to [account@nuget.org](mailto:account@nuget.org) with the owner display name on [nuget.org](https://www.nuget.org/), as well as any reserved prefixes you are requesting.</span></span> <span data-ttu-id="c894c-142">如果要将前缀子集委托给多个所有者，请确保提及所有的所有者显示名称和前缀子集。</span><span class="sxs-lookup"><span data-stu-id="c894c-142">If you are delegating prefix subsets to multiple owners, make sure you mention all owner display names and prefix subsets.</span></span>

<span data-ttu-id="c894c-143">提交申请后，你会收到接受或拒绝通知（以及拒绝标准）。</span><span class="sxs-lookup"><span data-stu-id="c894c-143">After the application is submitted, you are notified of acceptance or rejection (with the criteria that caused rejection).</span></span> <span data-ttu-id="c894c-144">我们可能需要提出其他标识问题以确认所有者身份。</span><span class="sxs-lookup"><span data-stu-id="c894c-144">We may need to ask additional identifying questions to confirm owner identity.</span></span>

### <a name="id-prefix-reservation-criteria"></a><span data-ttu-id="c894c-145">ID 前缀预留标准</span><span class="sxs-lookup"><span data-stu-id="c894c-145">ID prefix reservation criteria</span></span>

<span data-ttu-id="c894c-146">在审核任何 ID 前缀预留申请时，[nuget.org](https://www.nuget.org/) 团队将根据以下标准评估申请。</span><span class="sxs-lookup"><span data-stu-id="c894c-146">When reviewing any application for ID prefix reservation, the [nuget.org](https://www.nuget.org/) team will evaluate the application against the below criteria.</span></span> <span data-ttu-id="c894c-147">并非所有标准均需满足才可保留前缀，但如没有确实证据证明满足标准（并给出解释），申请可能会被拒绝：</span><span class="sxs-lookup"><span data-stu-id="c894c-147">Not all criteria needs to be met for a prefix to be reserved, but the application may be denied if there is not substantial evidence of the criteria being met (with an explanation given):</span></span>

1. <span data-ttu-id="c894c-148">包 ID 前缀是否会正确且清楚地标识包所有者？</span><span class="sxs-lookup"><span data-stu-id="c894c-148">Does the package ID prefix properly and clearly identify the package owner?</span></span>

1. <span data-ttu-id="c894c-149">是否让包所有者[启用了其 NuGet.org 帐户的 2FA](individual-accounts.md#enable-two-factor-authentication-2fa)？</span><span class="sxs-lookup"><span data-stu-id="c894c-149">Has the package owner [enabled 2FA for their NuGet.org account](individual-accounts.md#enable-two-factor-authentication-2fa)?</span></span>

1. <span data-ttu-id="c894c-150">所有者已提交的大量包是否已在包 ID 前缀下？</span><span class="sxs-lookup"><span data-stu-id="c894c-150">Are a significant number of the packages that have already been submitted by the owner under the package ID prefix?</span></span>

1. <span data-ttu-id="c894c-151">包 ID 前缀是否为不应属于任何个人所有者或组织的常见内容？</span><span class="sxs-lookup"><span data-stu-id="c894c-151">Is the package ID prefix something common that should not belong to any individual owner or organization?</span></span>

1. <span data-ttu-id="c894c-152">不保留包 ID 前缀是否会给社区带来歧义和混淆  ？</span><span class="sxs-lookup"><span data-stu-id="c894c-152">Would *not* reserving the package ID prefix cause ambiguity and confusion for the community?</span></span>

1. <span data-ttu-id="c894c-153">与包 ID 前缀匹配的包的标识属性是否清晰且一致（尤其是包作者）？</span><span class="sxs-lookup"><span data-stu-id="c894c-153">Are the identifying properties of the packages that match the package ID prefix clear and consistent (especially the package author)?</span></span>

1. <span data-ttu-id="c894c-154">包是否具有许可证（使用[许可证](../reference/nuspec.md#license)元数据元素而不是弃用的 licenseUrl？</span><span class="sxs-lookup"><span data-stu-id="c894c-154">Do the packages have a license (using the [license](../reference/nuspec.md#license) metadata element and NOT licenseUrl which is being deprecated)?</span></span>

1. <span data-ttu-id="c894c-155">如果包具有图标（使用 iconUrl 元数据元素），则这些包是否也使用该[图标](../reference/nuspec.md#icon) 元数据元素（不需要删除 iconUrl）？</span><span class="sxs-lookup"><span data-stu-id="c894c-155">If the packages have an icon (using the iconUrl metadata element), are they also using the [icon](../reference/nuspec.md#icon) metadata element (it is not a requirement to remove the iconUrl)?</span></span>

## <a name="third-party-feed-provider-scenarios"></a><span data-ttu-id="c894c-156">第三方源提供程序方案</span><span class="sxs-lookup"><span data-stu-id="c894c-156">Third party feed provider scenarios</span></span>

<span data-ttu-id="c894c-157">如果第三方源提供程序有兴趣实现自己的服务以提供前缀预留，则可以通过修改 NuGet V3 源提供程序中的搜索服务来实现。</span><span class="sxs-lookup"><span data-stu-id="c894c-157">If a third party feed provider is interested in implementing their own service to provide prefix reservations, they can do so by modifying the search service in the NuGet V3 feed providers.</span></span> <span data-ttu-id="c894c-158">源搜索服务中的更改是添加 `verified` 属性。</span><span class="sxs-lookup"><span data-stu-id="c894c-158">The change in the feed search service is to add the `verified` property.</span></span> <span data-ttu-id="c894c-159">NuGet 客户端不支持 V2 源中添加的属性。</span><span class="sxs-lookup"><span data-stu-id="c894c-159">The NuGet client will not support the added property in the V2 feed.</span></span>

<span data-ttu-id="c894c-160">有关详细信息，请参阅[有关 API 搜索服务的文档](../api/search-query-service-resource.md)。</span><span class="sxs-lookup"><span data-stu-id="c894c-160">For more information, see the [documentation about the API's search service](../api/search-query-service-resource.md).</span></span>

## <a name="package-id-prefix-reservation-dispute-policy"></a><span data-ttu-id="c894c-161">包 ID 前缀预留争议策略</span><span class="sxs-lookup"><span data-stu-id="c894c-161">Package ID Prefix Reservation Dispute Policy</span></span>
<span data-ttu-id="c894c-162">如果你认为 [NuGet.org](https://www.nuget.org) 上的所有者被分配了违反上述标准或侵犯任何商标或版权的包 ID 前缀预留，请通过电子邮件发送相关的 ID 前缀、ID 前缀的所有者以及质疑分配的前缀预留的原因至 [support@nuget.org](mailto:support@nuget.org)。</span><span class="sxs-lookup"><span data-stu-id="c894c-162">If you believe an owner on [NuGet.org](https://www.nuget.org) was assigned a package ID prefix reservation that goes against the above listed criteria, or infringes on any trademarks or copyrights, please email [support@nuget.org](mailto:support@nuget.org) with the ID prefix in question, the owner of the ID prefix, and the reason for disputing the assigned prefix reservation.</span></span>

