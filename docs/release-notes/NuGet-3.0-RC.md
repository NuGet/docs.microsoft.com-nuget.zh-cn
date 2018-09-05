---
title: NuGet 3.0 RC 发行说明
description: 包括已知的问题、 bug 修复、 新增的功能和 Dcr NuGet 3.0 RC 的发行说明。
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 0575cb1598f259a1cf1597f67123b644d67c31b5
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/04/2018
ms.locfileid: "43551714"
---
# <a name="nuget-30-rc-release-notes"></a><span data-ttu-id="0d564-103">NuGet 3.0 RC 发行说明</span><span class="sxs-lookup"><span data-stu-id="0d564-103">NuGet 3.0 RC Release Notes</span></span>

<span data-ttu-id="0d564-104">[NuGet 3.0 测试版发行说明](../release-notes/nuget-3.0-beta.md) | [NuGet 3.0 RC2 发行说明](../release-notes/nuget-3.0-RC2.md)</span><span class="sxs-lookup"><span data-stu-id="0d564-104">[NuGet 3.0 Beta Release Notes](../release-notes/nuget-3.0-beta.md) | [NuGet 3.0 RC2 Release Notes](../release-notes/nuget-3.0-RC2.md)</span></span>

<span data-ttu-id="0d564-105">NuGet 3.0 RC 与 Visual Studio 2015 RC 版本发布于 2015 年 4 月 29 日。</span><span class="sxs-lookup"><span data-stu-id="0d564-105">NuGet 3.0 RC was released on April 29, 2015 with the Visual Studio 2015 RC release.</span></span> <span data-ttu-id="0d564-106">此版本包含重要的 bug 修复、 性能改进和更新以支持新框架的数量。</span><span class="sxs-lookup"><span data-stu-id="0d564-106">This release has a number of important bug fixes, performance improvements and updates to support the new frameworks.</span></span>  <span data-ttu-id="0d564-107">它是仅适用于 Visual Studio 2015。</span><span class="sxs-lookup"><span data-stu-id="0d564-107">It is only available for Visual Studio 2015.</span></span>

### <a name="continued-focus-on-performance"></a><span data-ttu-id="0d564-108">对性能方面的不懈关注</span><span class="sxs-lookup"><span data-stu-id="0d564-108">Continued Focus on Performance</span></span>

<span data-ttu-id="0d564-109">稳定性和 NuGet 查询的性能仍是我们的重心一个热门的话题。</span><span class="sxs-lookup"><span data-stu-id="0d564-109">Stability and performance of NuGet queries continue to be a hot topic that we are focusing on.</span></span>  <span data-ttu-id="0d564-110">此版本中，您将会看到非常快速的搜索操作中的 NuGet UI 和网站。</span><span class="sxs-lookup"><span data-stu-id="0d564-110">With this release, you should start to see very quick search operations in the NuGet UI and website.</span></span>  <span data-ttu-id="0d564-111">我们正在监视服务以及如何使用该服务，以便我们可以继续调整这些操作。</span><span class="sxs-lookup"><span data-stu-id="0d564-111">We're monitoring the service and how you use the service so that we can continue to tune these operations.</span></span>

## <a name="significant-issues-resolved"></a><span data-ttu-id="0d564-112">已解决的重要问题</span><span class="sxs-lookup"><span data-stu-id="0d564-112">Significant Issues Resolved</span></span>

<span data-ttu-id="0d564-113">为了达到稳定状态的 NuGet 客户端，作为此发布的一部分解决许多问题。</span><span class="sxs-lookup"><span data-stu-id="0d564-113">In order to stabilize the NuGet clients, we resolved many issues as part of this release.</span></span>  <span data-ttu-id="0d564-114">下面是只是简要的一些更重要的问题已解决的列表：</span><span class="sxs-lookup"><span data-stu-id="0d564-114">Here is just a brief list of some of the more important issues resolved:</span></span>

* <span data-ttu-id="0d564-115">ASP.NET 5 K framework 的重命名的一部分，已更新了框架名字对象来处理 dnx 和 dnxcore[链接](https://github.com/NuGet/Home/issues/215)</span><span class="sxs-lookup"><span data-stu-id="0d564-115">As part of the rename of the K framework for ASP.NET 5, framework monikers have been updated to handle dnx and dnxcore [link](https://github.com/NuGet/Home/issues/215)</span></span>
* <span data-ttu-id="0d564-116">从 Visual Studio UI 中的链接添加帮助文档[链接](https://github.com/NuGet/Home/issues/232)</span><span class="sxs-lookup"><span data-stu-id="0d564-116">Added help documentation from links in the Visual Studio UI [link](https://github.com/NuGet/Home/issues/232)</span></span>
* <span data-ttu-id="0d564-117">更好地处理中的复杂引用`.nuspec`使用以逗号分隔的框架引用[链接](https://github.com/NuGet/Home/issues/276)</span><span class="sxs-lookup"><span data-stu-id="0d564-117">Better handling of complex references in `.nuspec` with comma-delimited framework references [link](https://github.com/NuGet/Home/issues/276)</span></span>
* <span data-ttu-id="0d564-118">修复了对日语区域性的支持[链接](https://github.com/NuGet/Home/issues/253)</span><span class="sxs-lookup"><span data-stu-id="0d564-118">Fixed support for Japanese cultures [link](https://github.com/NuGet/Home/issues/253)</span></span>
* <span data-ttu-id="0d564-119">更新的客户端以允许 ASP.NET 5 项目使用新的 v3 终结点[链接](https://github.com/NuGet/Home/issues/219)</span><span class="sxs-lookup"><span data-stu-id="0d564-119">Updated client to allow ASP.NET 5 projects to use new v3 endpoints [link](https://github.com/NuGet/Home/issues/219)</span></span>
* <span data-ttu-id="0d564-120">更新为更好的句柄与源代码管理的包文件夹[链接](https://github.com/NuGet/Home/issues/56)</span><span class="sxs-lookup"><span data-stu-id="0d564-120">Updated to better handle packages folder with source control [link](https://github.com/NuGet/Home/issues/56)</span></span>
* <span data-ttu-id="0d564-121">修复了对附属包的支持[链接](https://github.com/NuGet/Home/issues/17)</span><span class="sxs-lookup"><span data-stu-id="0d564-121">Fixed support for satellite packages [link](https://github.com/NuGet/Home/issues/17)</span></span>
* <span data-ttu-id="0d564-122">更正了对特定于框架的内容文件的支持[链接](https://github.com/NuGet/Home/issues/18)</span><span class="sxs-lookup"><span data-stu-id="0d564-122">Corrected support for framework-specific content files [link](https://github.com/NuGet/Home/issues/18)</span></span>

## <a name="github-presence-overhaul"></a><span data-ttu-id="0d564-123">GitHub 存在革新</span><span class="sxs-lookup"><span data-stu-id="0d564-123">GitHub presence overhaul</span></span>

<span data-ttu-id="0d564-124">我们做出了一些更改到我们[源代码存储库在 GitHub 上的](http://github.com/nuget/home)。</span><span class="sxs-lookup"><span data-stu-id="0d564-124">We've made some changes to our [source code repositories on GitHub](http://github.com/nuget/home).</span></span>  <span data-ttu-id="0d564-125">如果使用 Visual Studio 的 NuGet 客户端、 Powershell 命令或命令行中有任何问题可执行文件可以记录这些问题和监视其进度上我们[主页 GitHub 存储库问题列表](http://github.com/nuget/home/issues)。</span><span class="sxs-lookup"><span data-stu-id="0d564-125">If you have any issues with the NuGet Visual Studio client, the Powershell commands, or the command-line executable you can log those issues and monitor their progress on our [GitHub Home repository issues list](http://github.com/nuget/home/issues).</span></span>  <span data-ttu-id="0d564-126">我们在跟踪中的库的问题我们[GitHub NuGetGallery 存储库](http://github.com/nuget/NuGetGallery/issues)。</span><span class="sxs-lookup"><span data-stu-id="0d564-126">We are tracking issues for the gallery in our [GitHub NuGetGallery repository](http://github.com/nuget/NuGetGallery/issues).</span></span>


## <a name="stay-tuned"></a><span data-ttu-id="0d564-127">请继续关注</span><span class="sxs-lookup"><span data-stu-id="0d564-127">Stay Tuned</span></span>

<span data-ttu-id="0d564-128">请密切关注[我们的博客](http://blog.nuget.org)详细进度和 NuGet 3.0 的公告 ！</span><span class="sxs-lookup"><span data-stu-id="0d564-128">Please keep an eye on [our blog](http://blog.nuget.org) for more progress and announcements for NuGet 3.0!</span></span>