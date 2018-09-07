---
title: NuGet 生态系统概述
description: NuGet 生态系统中的完整资源，包括 NuGet 源、非 Microsoft NuGet 项目、实用程序和培训材料。
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: conceptual
ms.openlocfilehash: 31243076f36f6ff274c4377c1773ea59dda8c834
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/04/2018
ms.locfileid: "43548139"
---
# <a name="an-overview-of-the-nuget-ecosystem"></a><span data-ttu-id="fdbab-103">NuGet 生态系统概述</span><span class="sxs-lookup"><span data-stu-id="fdbab-103">An overview of the NuGet ecosystem</span></span>

<span data-ttu-id="fdbab-104">自 2010 年推出以来，NuGet 提供了良好的机遇来改善和自动化开发过程的不同方面。</span><span class="sxs-lookup"><span data-stu-id="fdbab-104">Since it's introduction in 2010, NuGet has presented a great opportunity to improve and automate different aspects of the development processes.</span></span>

<span data-ttu-id="fdbab-105">由于 NuGet 是根据限制性弱的 [Apache v2 许可证](http://choosealicense.com/licenses/apache/)许可的开放源代码，因此其他项目可以利用 NuGet，公司也可在其产品中生成对 NuGet 的支持。</span><span class="sxs-lookup"><span data-stu-id="fdbab-105">Because NuGet is open source under a permissive [Apache v2 license](http://choosealicense.com/licenses/apache/), other projects can leverage NuGet and companies can build support for it in their products.</span></span> <span data-ttu-id="fdbab-106">无论是对于开源项目还是企业应用程序开发，NuGet 和以 NuGet 为基础生成的其他应用程序提供了广泛的工具生态系统，以便改善软件开发过程。</span><span class="sxs-lookup"><span data-stu-id="fdbab-106">Whether for open-source projects or enterprise application development, NuGet and other applications built on and around NuGet provide a broad ecosystem of tools for improving your software development process.</span></span>

<span data-ttu-id="fdbab-107">由于开发人员的贡献，所有这些项目都能够进行创新。</span><span class="sxs-lookup"><span data-stu-id="fdbab-107">All of these projects are able to innovate because of developer contributions.</span></span> <span data-ttu-id="fdbab-108">正如参与到 NuGet 本身中去，也通过报告缺陷和新功能创意、提供反馈、编写文档以及参与代码，尽力对这些项目做出贡献。</span><span class="sxs-lookup"><span data-stu-id="fdbab-108">Just as you contribute to NuGet itself, also make contribution to these projects by reporting defects and new feature ideas, providing feedback, writing documentation, and contributing code where possible.</span></span>

## <a name="net-foundation-projects"></a><span data-ttu-id="fdbab-109">.NET Foundation 项目</span><span class="sxs-lookup"><span data-stu-id="fdbab-109">.NET Foundation projects</span></span>

<span data-ttu-id="fdbab-110">NuGet 为 Microsoft 开发平台提供了免费的开放源代码程序包管理系统。</span><span class="sxs-lookup"><span data-stu-id="fdbab-110">NuGet provides a free, open source package management system for the Microsoft development platform.</span></span> <span data-ttu-id="fdbab-111">它包含一些客户端工具以及一组服务，这些工具和服务构成了[正式 NuGet 库](http://www.nuget.org)。</span><span class="sxs-lookup"><span data-stu-id="fdbab-111">It consists of a few client tools as well as the set of services that comprise the [official NuGet Gallery](http://www.nuget.org).</span></span> <span data-ttu-id="fdbab-112">一经组合，便形成受 [.NET Foundation](http://www.dotnetfoundation.org/) 控制的 NuGet 项目。</span><span class="sxs-lookup"><span data-stu-id="fdbab-112">Combined, these form the NuGet project which is governed by the [.NET Foundation](http://www.dotnetfoundation.org/).</span></span>

<span data-ttu-id="fdbab-113">NuGet 组织包含 GitHub 上的各种存储库。</span><span class="sxs-lookup"><span data-stu-id="fdbab-113">The NuGet Organization contains various repositories on GitHub.</span></span> <span data-ttu-id="fdbab-114">[https://github.com/Nuget/Home](https://github.com/Nuget/Home) 概述了所有存储库以及可在何处找到各种 NuGet 组件。</span><span class="sxs-lookup"><span data-stu-id="fdbab-114">[https://github.com/Nuget/Home](https://github.com/Nuget/Home) gives an overview of all the repositories and where to find the various NuGet components.</span></span>

## <a name="microsoft-projects"></a><span data-ttu-id="fdbab-115">Microsoft 项目</span><span class="sxs-lookup"><span data-stu-id="fdbab-115">Microsoft projects</span></span>

<span data-ttu-id="fdbab-116">Microsoft 对 NuGet 的开发做出了巨大的贡献。</span><span class="sxs-lookup"><span data-stu-id="fdbab-116">Microsoft has contributed extensively to the development of NuGet.</span></span> <span data-ttu-id="fdbab-117">Microsoft 员工做出的所有贡献也均为开放源代码，并将捐赠（包括版权）给 .NET Foundation。</span><span class="sxs-lookup"><span data-stu-id="fdbab-117">All contributions made by Microsoft employees are also open source and are donated (including copyrights) to the .NET Foundation.</span></span>

## <a name="non-microsoft-projects"></a><span data-ttu-id="fdbab-118">非 Microsoft 项目</span><span class="sxs-lookup"><span data-stu-id="fdbab-118">Non-Microsoft projects</span></span>

<span data-ttu-id="fdbab-119">许多其他个人和公司也为 NuGet 生态系统做出了重要贡献。</span><span class="sxs-lookup"><span data-stu-id="fdbab-119">Many other individuals and companies have made significant contributions to the NuGet ecosystem.</span></span> <span data-ttu-id="fdbab-120">此处所列每个项目的许可证可能与核心 NuGet 组件的不同，因此请在使用前确认许可条款是否可接受：</span><span class="sxs-lookup"><span data-stu-id="fdbab-120">Each project listed here may have a different license than the core NuGet components, so confirm that the license terms are acceptable prior to use:</span></span>

- [<span data-ttu-id="fdbab-121">AppVeyor CI</span><span class="sxs-lookup"><span data-stu-id="fdbab-121">AppVeyor CI</span></span>](https://www.appveyor.com/)
- [<span data-ttu-id="fdbab-122">Artifactory</span><span class="sxs-lookup"><span data-stu-id="fdbab-122">Artifactory</span></span>](https://www.jfrog.com/artifactory/)
- [<span data-ttu-id="fdbab-123">BoxStarter</span><span class="sxs-lookup"><span data-stu-id="fdbab-123">BoxStarter</span></span>](http://boxstarter.org/)
- [<span data-ttu-id="fdbab-124">Chocolatey</span><span class="sxs-lookup"><span data-stu-id="fdbab-124">Chocolatey</span></span>](https://chocolatey.org/)
- [<span data-ttu-id="fdbab-125">CoApp</span><span class="sxs-lookup"><span data-stu-id="fdbab-125">CoApp</span></span>](http://coapp.org/)
- [<span data-ttu-id="fdbab-126">JetBrains ReSharper</span><span class="sxs-lookup"><span data-stu-id="fdbab-126">JetBrains ReSharper</span></span>](https://resharper-plugins.jetbrains.com/)
- [<span data-ttu-id="fdbab-127">JetBrains TeamCity</span><span class="sxs-lookup"><span data-stu-id="fdbab-127">JetBrains TeamCity</span></span>](https://www.jetbrains.com/teamcity/)
- [<span data-ttu-id="fdbab-128">Klondike</span><span class="sxs-lookup"><span data-stu-id="fdbab-128">Klondike</span></span>](https://github.com/themotleyfool/Klondike)
- [<span data-ttu-id="fdbab-129">MinimalNugetServer</span><span class="sxs-lookup"><span data-stu-id="fdbab-129">MinimalNugetServer</span></span>](https://github.com/TanukiSharp/MinimalNugetServer)
- [<span data-ttu-id="fdbab-130">MyGet（或 NuGet 即服务）</span><span class="sxs-lookup"><span data-stu-id="fdbab-130">MyGet (or NuGet-as-a-service)</span></span>](http://www.myget.org/)
- [<span data-ttu-id="fdbab-131">NuGet 包资源管理器</span><span class="sxs-lookup"><span data-stu-id="fdbab-131">NuGet Package Explorer</span></span>](https://github.com/NuGetPackageExplorer/NuGetPackageExplorer)
- [<span data-ttu-id="fdbab-132">NuGet 服务器</span><span class="sxs-lookup"><span data-stu-id="fdbab-132">NuGet Server</span></span>](http://nugetserver.net/)
- [<span data-ttu-id="fdbab-133">OctopusDeploy</span><span class="sxs-lookup"><span data-stu-id="fdbab-133">OctopusDeploy</span></span>](https://octopus.com/)
- [<span data-ttu-id="fdbab-134">Paket</span><span class="sxs-lookup"><span data-stu-id="fdbab-134">Paket</span></span>](https://fsprojects.github.io/Paket/)
- [<span data-ttu-id="fdbab-135">ProGet (Inedo)</span><span class="sxs-lookup"><span data-stu-id="fdbab-135">ProGet (Inedo)</span></span>](http://inedo.com/proget)
- [<span data-ttu-id="fdbab-136">scriptcs</span><span class="sxs-lookup"><span data-stu-id="fdbab-136">scriptcs</span></span>](http://scriptcs.net/)
- [<span data-ttu-id="fdbab-137">SharpDevelop</span><span class="sxs-lookup"><span data-stu-id="fdbab-137">SharpDevelop</span></span>](http://community.sharpdevelop.net/blogs/mattward/archive/2011/01/23/NuGetSupportInSharpDevelop.aspx)
- [<span data-ttu-id="fdbab-138">Sonatype Nexus</span><span class="sxs-lookup"><span data-stu-id="fdbab-138">Sonatype Nexus</span></span>](http://www.sonatype.com/nexus-repository-sonatype)
- [<span data-ttu-id="fdbab-139">SymbolSource</span><span class="sxs-lookup"><span data-stu-id="fdbab-139">SymbolSource</span></span>](http://www.symbolsource.org/Public)
- [<span data-ttu-id="fdbab-140">Xamarin 和 MonoDevelop</span><span class="sxs-lookup"><span data-stu-id="fdbab-140">Xamarin and MonoDevelop</span></span>](https://github.com/mrward/monodevelop-nuget-addin)

## <a name="other-nuget-based-utilities"></a><span data-ttu-id="fdbab-141">其他基于 NuGet 的实用程序</span><span class="sxs-lookup"><span data-stu-id="fdbab-141">Other NuGet-based utilities</span></span>

<span data-ttu-id="fdbab-142">以下是在 NuGet 基础上生成的工具和实用程序：</span><span class="sxs-lookup"><span data-stu-id="fdbab-142">These are tools and utilities built on NuGet:</span></span>

- <span data-ttu-id="fdbab-143">[Glimpse 扩展](http://getglimpse.com/Packages)（插件均为包）</span><span class="sxs-lookup"><span data-stu-id="fdbab-143">[Glimpse Extensions](http://getglimpse.com/Packages) (plug-ins are packages)</span></span>
- [<span data-ttu-id="fdbab-144">NuGetMustHaves.com</span><span class="sxs-lookup"><span data-stu-id="fdbab-144">NuGetMustHaves.com</span></span>](http://nugetmusthaves.com/)
- <span data-ttu-id="fdbab-145">[Orchard](http://www.orchardproject.net/)（CMS 模块从 Orchard 库中托管的 v1 NuGet 源提取）</span><span class="sxs-lookup"><span data-stu-id="fdbab-145">[Orchard](http://www.orchardproject.net/) (CMS modules are fetched from a v1 NuGet feed hosted in the Orchard Gallery)</span></span>
- [<span data-ttu-id="fdbab-146">NuGet 服务器的 Java 实现</span><span class="sxs-lookup"><span data-stu-id="fdbab-146">Java implementation of NuGet Server</span></span>](http://jonnyzzz.com/blog/2012/03/07/nuget-server-in-pure-java/)
- <span data-ttu-id="fdbab-147">[NuGetLatest](https://twitter.com/NuGetLatest)（发表新包发布推文的 Twitter 自动程序）</span><span class="sxs-lookup"><span data-stu-id="fdbab-147">[NuGetLatest](https://twitter.com/NuGetLatest) (Twitter bot tweeting new package publications)</span></span>
- <span data-ttu-id="fdbab-148">[DefinitelyTyped](http://definitelytyped.org/)（[发布到 NuGet](http://www.nuget.org/packages?q=DefinitelyTyped) 的[自动化](https://github.com/DefinitelyTyped/NugetAutomation/) TypeScript 类型定义）</span><span class="sxs-lookup"><span data-stu-id="fdbab-148">[DefinitelyTyped](http://definitelytyped.org/) ([Automatic](https://github.com/DefinitelyTyped/NugetAutomation/) TypeScript Type [Definitions published to NuGet](http://www.nuget.org/packages?q=DefinitelyTyped))</span></span>

## <a name="training-materials-and-references"></a><span data-ttu-id="fdbab-149">培训材料和参考资料</span><span class="sxs-lookup"><span data-stu-id="fdbab-149">Training materials and references</span></span>

<span data-ttu-id="fdbab-150">使用新工具或技术通常伴有学习曲线。</span><span class="sxs-lookup"><span data-stu-id="fdbab-150">Using a new tool or technology usually comes with a learning curve.</span></span> <span data-ttu-id="fdbab-151">幸运的是，NuGet 完全没有陡峭的学习曲线！</span><span class="sxs-lookup"><span data-stu-id="fdbab-151">Luckily for you, NuGet has no steep learning curve it all!</span></span> <span data-ttu-id="fdbab-152">事实上，任何人都可以快速[入门包的使用](../quickstart/use-a-package.md)。</span><span class="sxs-lookup"><span data-stu-id="fdbab-152">In fact, anyone can [get started consuming packages](../quickstart/use-a-package.md) quickly.</span></span>

<span data-ttu-id="fdbab-153">即便如此，创作包（尤其是好的包）以及在自动生成和部署过程中利用 NuGet，需要在以下资源上花费更多时间：</span><span class="sxs-lookup"><span data-stu-id="fdbab-153">That said, authoring packages–and especially good packages–along with  embracing NuGet in automated build and deployment processes, requires spending a little more time with the following resources:</span></span>

- [<span data-ttu-id="fdbab-154">NuGet 博客</span><span class="sxs-lookup"><span data-stu-id="fdbab-154">NuGet Blog</span></span>](http://blog.nuget.org/)
- [<span data-ttu-id="fdbab-155">Twitter 上的 NuGet 团队，@nuget</span><span class="sxs-lookup"><span data-stu-id="fdbab-155">NuGet team on Twitter, @nuget</span></span>](http://twitter.com/nuget)
- <span data-ttu-id="fdbab-156">书籍：</span><span class="sxs-lookup"><span data-stu-id="fdbab-156">Books:</span></span>
  - [<span data-ttu-id="fdbab-157">Apress Pro NuGet</span><span class="sxs-lookup"><span data-stu-id="fdbab-157">Apress Pro NuGet</span></span>](http://bit.ly/ProNuGet)
  - [<span data-ttu-id="fdbab-158">NuGet 2 基础知识</span><span class="sxs-lookup"><span data-stu-id="fdbab-158">NuGet 2 Essentials</span></span>](http://www.amazon.com/NuGet-2-Essentials-Damir-Arh-ebook/dp/B00GTQD5M4)

## <a name="documentation-for-individual-packages"></a><span data-ttu-id="fdbab-159">单个包的文档</span><span class="sxs-lookup"><span data-stu-id="fdbab-159">Documentation for individual packages</span></span>

<span data-ttu-id="fdbab-160">[NuDoq](http://nudoq.org) 提供了适用于 NuGet 包的直接访问、更新和文档。</span><span class="sxs-lookup"><span data-stu-id="fdbab-160">[NuDoq](http://nudoq.org) provides straightforward access and updates and documentation for NuGet packages.</span></span>

<span data-ttu-id="fdbab-161">NuDoq 定期轮询 nuget.org 库服务器以获取最新的包更新，解压缩并处理库文档文件，以及相应地对站点进行更新。</span><span class="sxs-lookup"><span data-stu-id="fdbab-161">NuDoq regularly polls the nuget.org gallery server for the latest package updates, unpacks and processes the library documentation files, and updates the site accordingly.</span></span>

## <a name="adding-your-project"></a><span data-ttu-id="fdbab-162">添加项目</span><span class="sxs-lookup"><span data-stu-id="fdbab-162">Adding your project</span></span>

<span data-ttu-id="fdbab-163">如果有 NuGet 生态系统项目，且是对本页有价值的补充，请向本页提交带编辑的拉取请求。</span><span class="sxs-lookup"><span data-stu-id="fdbab-163">If you have a NuGet ecosystem project that would be a valuable addition to this page, please  submit a pull request with an edit to this page.</span></span>
