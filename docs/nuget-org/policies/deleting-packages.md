---
title: 删除 nuget.org 的 NuGet 包
description: 用于取消列出 nuget.org 的包的策略；除非包违反其他策略，否则不支持永久删除。
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: conceptual
ms.openlocfilehash: 833f4a67bc75c5d650e85180b52ecd8f69218f15
ms.sourcegitcommit: b6810860b77b2d50aab031040b047c20a333aca3
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/28/2019
ms.locfileid: "67426972"
---
# <a name="deleting-packages"></a><span data-ttu-id="54e64-103">删除包</span><span class="sxs-lookup"><span data-stu-id="54e64-103">Deleting packages</span></span>

<span data-ttu-id="54e64-104">nuget.org 不支持永久删除包。</span><span class="sxs-lookup"><span data-stu-id="54e64-104">nuget.org does not support permanent deletion of packages.</span></span> <span data-ttu-id="54e64-105">此操作会破坏依赖该包可用性的每个项目，尤其是涉及包还原的生成工作流。</span><span class="sxs-lookup"><span data-stu-id="54e64-105">Doing so would break every project depending on the availability of the package, especially with build workflows that involve package restore.</span></span>

<span data-ttu-id="54e64-106">nuget.org 支持取消列出包，此操作可在网站上的包管理页中执行  。</span><span class="sxs-lookup"><span data-stu-id="54e64-106">nuget.org does supports *unlisting* a package, which can be done in the package management page on the web site.</span></span> <span data-ttu-id="54e64-107">取消列出的包不会显示在 nuget.org、Visual Studio UI 或搜索结果中。</span><span class="sxs-lookup"><span data-stu-id="54e64-107">Unlisted packages don't appear on nuget.org or in the Visual Studio UI, and do not appear in search results.</span></span> <span data-ttu-id="54e64-108">但是，仍可使用支持包还原的确切版本号下载和安装取消列出的包。</span><span class="sxs-lookup"><span data-stu-id="54e64-108">Unlisted packages, however, can still be downloaded and installed by using an exact version number, which supports package restore.</span></span> <span data-ttu-id="54e64-109">此外，仍可能在以下特定方案中发现取消列出的包：</span><span class="sxs-lookup"><span data-stu-id="54e64-109">In addition, unlisted packages may still be discovered in the following specific scenarios:</span></span>

- <span data-ttu-id="54e64-110">如果与版本或依赖项约束匹配的最新可用包是取消列出的包，使用浮动版本（如 `1.0.0-*`）进行包还原。</span><span class="sxs-lookup"><span data-stu-id="54e64-110">Package restore using floating versions (for example, `1.0.0-*`), if the latest available package matching the version or dependency constraints is an unlisted package.</span></span>
- <span data-ttu-id="54e64-111">通过目录复制包（因为该目录也包含取消列出的包）。</span><span class="sxs-lookup"><span data-stu-id="54e64-111">Replication of packages through the catalog (as the catalog also contains unlisted packages).</span></span>

## <a name="exceptions"></a><span data-ttu-id="54e64-112">异常</span><span class="sxs-lookup"><span data-stu-id="54e64-112">Exceptions</span></span>

<span data-ttu-id="54e64-113">在侵犯版权和可能包含有害内容等例外情况下，NuGet 团队可以手动删除包。</span><span class="sxs-lookup"><span data-stu-id="54e64-113">In exceptional situations such as copyright infringement and potentially harmful content, packages can be deleted manually by the NuGet team.</span></span> <span data-ttu-id="54e64-114">可使用 NuGet.org 包详细信息页上的“报告滥用情况”按钮报告相关包。</span><span class="sxs-lookup"><span data-stu-id="54e64-114">You can report a package using the "Report abuse" button on the NuGet.org package details page.</span></span> <span data-ttu-id="54e64-115">如果你是包所有者，请登录 NuGet.org 帐户，使用 NuGet.org 包详细信息页上的“联系支持人员”按钮联系 NuGet 支持人员。</span><span class="sxs-lookup"><span data-stu-id="54e64-115">If you are the package owner, login to your NuGet.org account to reach NuGet support using the "Contact support" button on the NuGet.org package details page.</span></span>

## <a name="prohibited-use"></a><span data-ttu-id="54e64-116">禁止使用</span><span class="sxs-lookup"><span data-stu-id="54e64-116">Prohibited use</span></span>

<span data-ttu-id="54e64-117">公共 NuGet 库中不允许存在满足以下任一条件的包，且将在不经过讨论的情况下立即删除这些包。</span><span class="sxs-lookup"><span data-stu-id="54e64-117">Packages that meet any of the following criteria are not allowed on the public NuGet gallery and will be immediately removed without discussion.</span></span> <span data-ttu-id="54e64-118">但是，包的所有者会获得删除包的通知。</span><span class="sxs-lookup"><span data-stu-id="54e64-118">Package owners will, however, be notified of the removal.</span></span>

- <span data-ttu-id="54e64-119">包含恶意软件、广告程序或任何类型的间谍软件。</span><span class="sxs-lookup"><span data-stu-id="54e64-119">Contains malware, adware, or any kind of spyware.</span></span>
- <span data-ttu-id="54e64-120">企图危害开发人员的工作站或组织。</span><span class="sxs-lookup"><span data-stu-id="54e64-120">Are designed to harm a developer's workstation or their organization.</span></span>
- <span data-ttu-id="54e64-121">侵犯版权或违反许可证。</span><span class="sxs-lookup"><span data-stu-id="54e64-121">Infringes copyrights or violates licenses.</span></span>
- <span data-ttu-id="54e64-122">包含非法内容。</span><span class="sxs-lookup"><span data-stu-id="54e64-122">Contains illegal content.</span></span>
- <span data-ttu-id="54e64-123">用于制止包标识符，包括包含零工作效率内容的包。</span><span class="sxs-lookup"><span data-stu-id="54e64-123">Are being used to squat on package identifiers, including packages that have zero productive content.</span></span> <span data-ttu-id="54e64-124">包必须包含代码，或所有者必须将标识符让与实际具有要运送的产品的某个人员。</span><span class="sxs-lookup"><span data-stu-id="54e64-124">Packages must contain code or the owners must concede the identifier to someone who actually has a product to ship.</span></span>
- <span data-ttu-id="54e64-125">尝试让库执行设计明确意图以外的操作。</span><span class="sxs-lookup"><span data-stu-id="54e64-125">Attempt to make the gallery do something that it's not explicitly designed to do.</span></span>

<span data-ttu-id="54e64-126">如果发现违反以上任一项的包，请单击包详细信息页上的“报告滥用行为”链接并提交报告  。</span><span class="sxs-lookup"><span data-stu-id="54e64-126">If you find a package that is in violation of any of these items, click the **Report Abuse** link on the package details page and submit a report.</span></span>

<span data-ttu-id="54e64-127">请注意，NuGet 团队和 .NET Foundation 保留随时更改这些条件的权利。</span><span class="sxs-lookup"><span data-stu-id="54e64-127">Note that the NuGet team and the .NET Foundation reserves the right to change these criteria at any time.</span></span>
