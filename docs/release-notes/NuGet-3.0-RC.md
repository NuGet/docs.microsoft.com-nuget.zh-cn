---
title: NuGet 3.0 RC 发行说明
description: NuGet 3.0 RC 的发行说明，包括已知问题、bug 修复、新增功能和 Dcr。
author: JonDouglas
ms.author: jodou
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 19bc51a278425295811db253ca3f4ba4366ccf49
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/26/2021
ms.locfileid: "98776578"
---
# <a name="nuget-30-rc-release-notes"></a><span data-ttu-id="b81db-103">NuGet 3.0 RC 发行说明</span><span class="sxs-lookup"><span data-stu-id="b81db-103">NuGet 3.0 RC Release Notes</span></span>

<span data-ttu-id="b81db-104">[NuGet 3.0 Beta 发行说明](../release-notes/nuget-3.0-beta.md)  | [NuGet 3.0 RC2 发行说明](../release-notes/nuget-3.0-RC2.md)</span><span class="sxs-lookup"><span data-stu-id="b81db-104">[NuGet 3.0 Beta Release Notes](../release-notes/nuget-3.0-beta.md) | [NuGet 3.0 RC2 Release Notes](../release-notes/nuget-3.0-RC2.md)</span></span>

<span data-ttu-id="b81db-105">NuGet 3.0 RC 于年4月 29 2015 日发布了 Visual Studio 2015 RC 版本。</span><span class="sxs-lookup"><span data-stu-id="b81db-105">NuGet 3.0 RC was released on April 29, 2015 with the Visual Studio 2015 RC release.</span></span> <span data-ttu-id="b81db-106">此版本包含许多重要的 bug 修复、性能改进和更新以支持新框架。</span><span class="sxs-lookup"><span data-stu-id="b81db-106">This release has a number of important bug fixes, performance improvements and updates to support the new frameworks.</span></span>  <span data-ttu-id="b81db-107">它仅适用于 Visual Studio 2015。</span><span class="sxs-lookup"><span data-stu-id="b81db-107">It is only available for Visual Studio 2015.</span></span>

### <a name="continued-focus-on-performance"></a><span data-ttu-id="b81db-108">继续关注性能</span><span class="sxs-lookup"><span data-stu-id="b81db-108">Continued Focus on Performance</span></span>

<span data-ttu-id="b81db-109">NuGet 查询的稳定性和性能仍是我们关注的热点话题。</span><span class="sxs-lookup"><span data-stu-id="b81db-109">Stability and performance of NuGet queries continue to be a hot topic that we are focusing on.</span></span>  <span data-ttu-id="b81db-110">在此版本中，你应开始在 NuGet UI 和网站中查看非常快速的搜索操作。</span><span class="sxs-lookup"><span data-stu-id="b81db-110">With this release, you should start to see very quick search operations in the NuGet UI and website.</span></span>  <span data-ttu-id="b81db-111">我们将监视服务以及使用服务的方式，以便我们可以继续调整这些操作。</span><span class="sxs-lookup"><span data-stu-id="b81db-111">We're monitoring the service and how you use the service so that we can continue to tune these operations.</span></span>

## <a name="significant-issues-resolved"></a><span data-ttu-id="b81db-112">已解决的重要问题</span><span class="sxs-lookup"><span data-stu-id="b81db-112">Significant Issues Resolved</span></span>

<span data-ttu-id="b81db-113">为了使 NuGet 客户端稳定，我们在此版本中解决了许多问题。</span><span class="sxs-lookup"><span data-stu-id="b81db-113">In order to stabilize the NuGet clients, we resolved many issues as part of this release.</span></span>  <span data-ttu-id="b81db-114">下面只是一些更重要的问题已解决的简短列表：</span><span class="sxs-lookup"><span data-stu-id="b81db-114">Here is just a brief list of some of the more important issues resolved:</span></span>

* <span data-ttu-id="b81db-115">在重命名 ASP.NET 5 的 K framework 的过程中，框架名字对象已更新为处理 dnx 和 dnxcore [链接](https://github.com/NuGet/Home/issues/215)</span><span class="sxs-lookup"><span data-stu-id="b81db-115">As part of the rename of the K framework for ASP.NET 5, framework monikers have been updated to handle dnx and dnxcore [link](https://github.com/NuGet/Home/issues/215)</span></span>
* <span data-ttu-id="b81db-116">通过 Visual Studio UI[链接](https://github.com/NuGet/Home/issues/232)中的链接添加了帮助文档</span><span class="sxs-lookup"><span data-stu-id="b81db-116">Added help documentation from links in the Visual Studio UI [link](https://github.com/NuGet/Home/issues/232)</span></span>
* <span data-ttu-id="b81db-117">`.nuspec`用逗号分隔的框架引用[链接](https://github.com/NuGet/Home/issues/276)更好地处理中的复杂引用</span><span class="sxs-lookup"><span data-stu-id="b81db-117">Better handling of complex references in `.nuspec` with comma-delimited framework references [link](https://github.com/NuGet/Home/issues/276)</span></span>
* <span data-ttu-id="b81db-118">固定支持日语区域性 [链接](https://github.com/NuGet/Home/issues/253)</span><span class="sxs-lookup"><span data-stu-id="b81db-118">Fixed support for Japanese cultures [link](https://github.com/NuGet/Home/issues/253)</span></span>
* <span data-ttu-id="b81db-119">更新了客户端以允许 ASP.NET 5 项目使用新的 v3 终结点 [链接](https://github.com/NuGet/Home/issues/219)</span><span class="sxs-lookup"><span data-stu-id="b81db-119">Updated client to allow ASP.NET 5 projects to use new v3 endpoints [link](https://github.com/NuGet/Home/issues/219)</span></span>
* <span data-ttu-id="b81db-120">更新了以更好地处理包含源代码管理[链接](https://github.com/NuGet/Home/issues/56)的包文件夹</span><span class="sxs-lookup"><span data-stu-id="b81db-120">Updated to better handle packages folder with source control [link](https://github.com/NuGet/Home/issues/56)</span></span>
* <span data-ttu-id="b81db-121">修复了对附属包的支持 [链接](https://github.com/NuGet/Home/issues/17)</span><span class="sxs-lookup"><span data-stu-id="b81db-121">Fixed support for satellite packages [link](https://github.com/NuGet/Home/issues/17)</span></span>
* <span data-ttu-id="b81db-122">更正了对框架特定内容文件[链接](https://github.com/NuGet/Home/issues/18)的支持</span><span class="sxs-lookup"><span data-stu-id="b81db-122">Corrected support for framework-specific content files [link](https://github.com/NuGet/Home/issues/18)</span></span>

## <a name="github-presence-overhaul"></a><span data-ttu-id="b81db-123">GitHub 状态检修</span><span class="sxs-lookup"><span data-stu-id="b81db-123">GitHub presence overhaul</span></span>

<span data-ttu-id="b81db-124">我们已对 [GitHub 上的源代码存储库](http://github.com/nuget/home)进行了一些更改。</span><span class="sxs-lookup"><span data-stu-id="b81db-124">We've made some changes to our [source code repositories on GitHub](http://github.com/nuget/home).</span></span>  <span data-ttu-id="b81db-125">如果你在 NuGet Visual Studio 客户端、Powershell 命令或命令行可执行文件中有任何问题，可以记录这些问题，并在 [GitHub Home 存储库问题列表](http://github.com/nuget/home/issues)中监视其进度。</span><span class="sxs-lookup"><span data-stu-id="b81db-125">If you have any issues with the NuGet Visual Studio client, the Powershell commands, or the command-line executable you can log those issues and monitor their progress on our [GitHub Home repository issues list](http://github.com/nuget/home/issues).</span></span>  <span data-ttu-id="b81db-126">我们正在跟踪 [GitHub NuGetGallery 存储库](http://github.com/nuget/NuGetGallery/issues)中的库问题。</span><span class="sxs-lookup"><span data-stu-id="b81db-126">We are tracking issues for the gallery in our [GitHub NuGetGallery repository](http://github.com/nuget/NuGetGallery/issues).</span></span>


## <a name="stay-tuned"></a><span data-ttu-id="b81db-127">保持关注</span><span class="sxs-lookup"><span data-stu-id="b81db-127">Stay Tuned</span></span>

<span data-ttu-id="b81db-128">有关 NuGet 3.0 的更多进度和公告，请关注 [我们的博客](http://blog.nuget.org) ！</span><span class="sxs-lookup"><span data-stu-id="b81db-128">Please keep an eye on [our blog](http://blog.nuget.org) for more progress and announcements for NuGet 3.0!</span></span>