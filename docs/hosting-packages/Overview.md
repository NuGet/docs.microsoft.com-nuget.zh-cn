---
title: 承载自己的 NuGet 源概述
description: 概述了本地或远程承载自己的 NuGet 包源或库的打开。
author: kraigb
ms.author: kraigb
manager: douge
ms.date: 08/25/2017
ms.topic: conceptual
ms.reviewer: anangaur
ms.openlocfilehash: 27f799ef69736c6cf718324e903049871430536f
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/26/2018
---
# <a name="hosting-your-own-nuget-feeds"></a><span data-ttu-id="e9854-103">承载自己的 NuGet 源</span><span class="sxs-lookup"><span data-stu-id="e9854-103">Hosting your own NuGet feeds</span></span>

<span data-ttu-id="e9854-104">可能希望将包仅发布到有限受众（例如，组织或工作组），而不是将其公开发布。</span><span class="sxs-lookup"><span data-stu-id="e9854-104">Instead of making packages publicly available, you might want to release packages to only a limited audience, such as your organization or workgroup.</span></span> <span data-ttu-id="e9854-105">此外，一些公司可能希望限制其开发人员可以使用的第三方库，使他们从有限包源（而不是 nuget.org）中提取内容。</span><span class="sxs-lookup"><span data-stu-id="e9854-105">In addition, some companies may want to restrict which third-party libraries their developers may use, and thus direct those developers to draw from a limited package source rather than nuget.org.</span></span>

<span data-ttu-id="e9854-106">对于所有此类目的，NuGet 支持通过以下方式设置专用包源：</span><span class="sxs-lookup"><span data-stu-id="e9854-106">For all such purposes, NuGet supports setting up private package sources in the following ways:</span></span>

- <span data-ttu-id="e9854-107">本地源：包只需放置在合适的网络文件共享中，理想情况下使用 `nuget init` 和 `nuget add` 创建分层文件夹结构 (NuGet 3.3+)。</span><span class="sxs-lookup"><span data-stu-id="e9854-107">Local feed: Packages are simply placed on a suitable network file share, ideally using `nuget init` and `nuget add` to create a hierarchical folder structure (NuGet 3.3+).</span></span> <span data-ttu-id="e9854-108">有关详细信息，请参阅[本地源](../hosting-packages/local-feeds.md)。</span><span class="sxs-lookup"><span data-stu-id="e9854-108">For details, see [Local Feeds](../hosting-packages/local-feeds.md).</span></span>
- <span data-ttu-id="e9854-109">NuGet.Server：通过本地 HTTP 服务器提供包。</span><span class="sxs-lookup"><span data-stu-id="e9854-109">NuGet.Server: Packages are made available through a local HTTP server.</span></span> <span data-ttu-id="e9854-110">有关详细信息，请参阅 [NuGet.Server](../hosting-packages/nuget-server.md)。</span><span class="sxs-lookup"><span data-stu-id="e9854-110">For details, see [NuGet.Server](../hosting-packages/nuget-server.md).</span></span>
- <span data-ttu-id="e9854-111">NuGet 库：在使用 [NuGet 库项目](https://github.com/NuGet/NuGetGallery#build-and-run-the-gallery-in-arbitrary-number-easy-steps) (github.com) 的 Internet 服务器上承载包。</span><span class="sxs-lookup"><span data-stu-id="e9854-111">NuGet Gallery: Packages are hosted on an Internet server using the [NuGet Gallery Project](https://github.com/NuGet/NuGetGallery#build-and-run-the-gallery-in-arbitrary-number-easy-steps) (github.com).</span></span> <span data-ttu-id="e9854-112">NuGet 库提供用户管理和功能，如丰富的 Web UI，它允许从浏览器中搜索和浏览包，这与 nuget.org 相似。</span><span class="sxs-lookup"><span data-stu-id="e9854-112">NuGet Gallery provides user management and features such as an extensive web UI that allows searching and exploring packages from within the browser, similar to nuget.org.</span></span>

<span data-ttu-id="e9854-113">还有其他几个 NuGet 承载产品也支持远程专用源，其中包括：</span><span class="sxs-lookup"><span data-stu-id="e9854-113">There are also several other NuGet hosting products that support remote private feeds, including the following:</span></span>

- <span data-ttu-id="e9854-114">[Visual Studio Team Services 包管理](https://www.visualstudio.com/docs/package/nuget/publish)，Team Foundation Server 2017 及更高版本上也提供此产品。</span><span class="sxs-lookup"><span data-stu-id="e9854-114">[Visual Studio Team Services Package Management](https://www.visualstudio.com/docs/package/nuget/publish), which is also available on Team Foundation Server 2017 and later.</span></span>
- [<span data-ttu-id="e9854-115">MyGet</span><span class="sxs-lookup"><span data-stu-id="e9854-115">MyGet</span></span>](http://myget.org)
- <span data-ttu-id="e9854-116">Inedo 的 [ProGet](http://inedo.com/proget)</span><span class="sxs-lookup"><span data-stu-id="e9854-116">[ProGet](http://inedo.com/proget) from Inedo</span></span>
- <span data-ttu-id="e9854-117">[NuGet 服务器](http://nugetserver.net/)，Inedo 的社区项目</span><span class="sxs-lookup"><span data-stu-id="e9854-117">[NuGet Server](http://nugetserver.net/), a community project from Inedo</span></span>
- <span data-ttu-id="e9854-118">[NuGet 服务器（开放源代码）](http://nuget-server.net)，与 Inedo 的 NuGet 服务器相似的开放源代码实现</span><span class="sxs-lookup"><span data-stu-id="e9854-118">[NuGet Server (Open Source)](http://nuget-server.net), an open-source implementation similar to Inedo's NuGet Server</span></span>
- <span data-ttu-id="e9854-119">JFrog 的 [Artifactory](https://www.jfrog.com/artifactory/)。</span><span class="sxs-lookup"><span data-stu-id="e9854-119">[Artifactory](https://www.jfrog.com/artifactory/) from JFrog.</span></span>
- <span data-ttu-id="e9854-120">Sonatype 的 [Nexus](http://www.sonatype.org/nexus/)。</span><span class="sxs-lookup"><span data-stu-id="e9854-120">[Nexus](http://www.sonatype.org/nexus/) from Sonatype.</span></span>
- <span data-ttu-id="e9854-121">JetBrains 的 [TeamCity](https://www.jetbrains.com/teamcity/)。</span><span class="sxs-lookup"><span data-stu-id="e9854-121">[TeamCity](https://www.jetbrains.com/teamcity/) from JetBrains.</span></span>

<span data-ttu-id="e9854-122">无论包是什么样的承载方式，均可将其添加到 `NuGet.Config` 中的可用源列表以便访问。</span><span class="sxs-lookup"><span data-stu-id="e9854-122">Regardless of how packages are hosted, you access them by adding them to the list of available sources in `NuGet.Config`.</span></span> <span data-ttu-id="e9854-123">此操作可在 Visual Studio 中执行（如[包源](../tools/package-manager-ui.md#package-sources)中所述），或使用 [`nuget sources`](../tools/cli-ref-sources.md) 从命令行执行操作。</span><span class="sxs-lookup"><span data-stu-id="e9854-123">This can be done in Visual Studio as described in [Package Sources](../tools/package-manager-ui.md#package-sources), or from the command line using [`nuget sources`](../tools/cli-ref-sources.md).</span></span> <span data-ttu-id="e9854-124">源的路径可以是本地文件夹路径名、网络名称或 URL。</span><span class="sxs-lookup"><span data-stu-id="e9854-124">The path to a source can be a local folder pathname, a network name, or a URL.</span></span>
