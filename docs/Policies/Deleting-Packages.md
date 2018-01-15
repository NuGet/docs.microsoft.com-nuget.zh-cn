---
title: "删除 nuget.org 的 NuGet 包 | Microsoft Docs"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 1/9/2017
ms.topic: article
ms.prod: nuget
ms.technology: 
ms.assetid: a348ca2e-0a5d-40ad-ba33-9bb37e1d980b
description: "用于取消列出 nuget.org 的包的策略；除非包违反其他策略，否则不支持永久删除。"
keywords: "NuGet 包删除, NuGet 包取消列出, 禁止使用包"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 9e388171f83fae7deb4f20033184dfa91bfab3da
ms.sourcegitcommit: a40c1c1cc05a46410f317a72f695ad1d80f39fa2
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/05/2018
---
# <a name="deleting-packages"></a><span data-ttu-id="49c6d-104">删除包</span><span class="sxs-lookup"><span data-stu-id="49c6d-104">Deleting packages</span></span>

<span data-ttu-id="49c6d-105">nuget.org 不支持永久删除包。</span><span class="sxs-lookup"><span data-stu-id="49c6d-105">nuget.org does not support permanent deletion of packages.</span></span> <span data-ttu-id="49c6d-106">此操作会破坏依赖该包可用性的每个项目，尤其是涉及包还原的生成工作流。</span><span class="sxs-lookup"><span data-stu-id="49c6d-106">Doing so would break every project depending on the availability of the package, especially with build workflows that involve package restore.</span></span>

<span data-ttu-id="49c6d-107">nuget.org 支持取消列出包，此操作可在网站上的包管理页中执行。</span><span class="sxs-lookup"><span data-stu-id="49c6d-107">nuget.org does supports *unlisting* a package, which can be done in the package management page on the web site.</span></span> <span data-ttu-id="49c6d-108">取消列出的包不会显示在 nuget.org、Visual Studio UI 或搜索结果中。</span><span class="sxs-lookup"><span data-stu-id="49c6d-108">Unlisted packages don't appear on nuget.org or in the Visual Studio UI, and do not appear in search results.</span></span> <span data-ttu-id="49c6d-109">但是，仍可使用支持包还原的确切版本号下载和安装取消列出的包。</span><span class="sxs-lookup"><span data-stu-id="49c6d-109">Unlisted packages, however, can still be downloaded and installed by using an exact version number, which supports package restore.</span></span> <span data-ttu-id="49c6d-110">此外，仍可能在以下特定方案中发现取消列出的包：</span><span class="sxs-lookup"><span data-stu-id="49c6d-110">In addition, unlisted packages may still be discovered in the following specific scenarios:</span></span>

- <span data-ttu-id="49c6d-111">如果与版本或依赖项约束匹配的最新可用包是取消列出的包，使用浮动版本（如 `1.0.0-*`）进行包还原。</span><span class="sxs-lookup"><span data-stu-id="49c6d-111">Package restore using floating versions (for example, `1.0.0-*`), if the latest available package matching the version or dependency constraints is an unlisted package.</span></span>
- <span data-ttu-id="49c6d-112">通过目录复制包（因为该目录也包含取消列出的包）。</span><span class="sxs-lookup"><span data-stu-id="49c6d-112">Replication of packages through the catalog (as the catalog also contains unlisted packages).</span></span>

## <a name="exceptions"></a><span data-ttu-id="49c6d-113">异常</span><span class="sxs-lookup"><span data-stu-id="49c6d-113">Exceptions</span></span>

<span data-ttu-id="49c6d-114">在侵犯版权和可能包含有害内容等例外情况下，NuGet 团队可以手动删除包。</span><span class="sxs-lookup"><span data-stu-id="49c6d-114">In exceptional situations such as copyright infringement and potentially harmful content, packages can be deleted manually by the NuGet team.</span></span> <span data-ttu-id="49c6d-115">通过 [NuGet 库](http://www.nuget.org)提交支持请求以启动该进程。</span><span class="sxs-lookup"><span data-stu-id="49c6d-115">Submit a support request through [NuGet Gallery](http://www.nuget.org) to start the process.</span></span>

## <a name="prohibited-use"></a><span data-ttu-id="49c6d-116">禁止使用</span><span class="sxs-lookup"><span data-stu-id="49c6d-116">Prohibited use</span></span>

<span data-ttu-id="49c6d-117">公共 NuGet 库中不允许存在满足以下任一条件的包，且将在不经过讨论的情况下立即删除这些包。</span><span class="sxs-lookup"><span data-stu-id="49c6d-117">Packages that meet any of the following criteria are not allowed on the public NuGet gallery and will be immediately removed without discussion.</span></span> <span data-ttu-id="49c6d-118">但是，包的所有者会获得删除包的通知。</span><span class="sxs-lookup"><span data-stu-id="49c6d-118">Package owners will, however, be notified of the removal.</span></span>

- <span data-ttu-id="49c6d-119">包含恶意软件、广告程序或任何类型的间谍软件。</span><span class="sxs-lookup"><span data-stu-id="49c6d-119">Contains malware, adware, or any kind of spyware.</span></span>
- <span data-ttu-id="49c6d-120">企图危害开发人员的工作站或组织。</span><span class="sxs-lookup"><span data-stu-id="49c6d-120">Are designed to harm a developer's workstation or their organization.</span></span>
- <span data-ttu-id="49c6d-121">侵犯版权或违反许可证。</span><span class="sxs-lookup"><span data-stu-id="49c6d-121">Infringes copyrights or violates licenses.</span></span>
- <span data-ttu-id="49c6d-122">包含非法内容。</span><span class="sxs-lookup"><span data-stu-id="49c6d-122">Contains illegal content.</span></span>
- <span data-ttu-id="49c6d-123">用于制止包标识符，包括包含零工作效率内容的包。</span><span class="sxs-lookup"><span data-stu-id="49c6d-123">Are being used to squat on package identifiers, including packages that have zero productive content.</span></span> <span data-ttu-id="49c6d-124">包必须包含代码，或所有者必须将标识符让与实际具有要运送的产品的某个人员。</span><span class="sxs-lookup"><span data-stu-id="49c6d-124">Packages must contain code or the owners must concede the identifier to someone who actually has a product to ship.</span></span>
- <span data-ttu-id="49c6d-125">尝试让库执行设计明确意图以外的操作。</span><span class="sxs-lookup"><span data-stu-id="49c6d-125">Attempt to make the gallery do something that it's not explicitly designed to do.</span></span>

<span data-ttu-id="49c6d-126">如果发现违反以上任一项的包，请单击包详细信息页上的“报告滥用行为”链接并提交报告。</span><span class="sxs-lookup"><span data-stu-id="49c6d-126">If you find a package that is in violation of any of these items, click the **Report Abuse** link on the package details page and submit a report.</span></span>

<span data-ttu-id="49c6d-127">请注意，NuGet 团队和 .NET Foundation 保留随时更改这些条件的权利。</span><span class="sxs-lookup"><span data-stu-id="49c6d-127">Note that the NuGet team and the .NET Foundation reserves the right to change these criteria at any time.</span></span>
