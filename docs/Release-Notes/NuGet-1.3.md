---
title: "NuGet 1.3 发行说明 |Microsoft 文档"
author: karann-msft
ms.author: karann-msft
manager: ghogen
ms.date: 11/11/2016
ms.topic: article
ms.prod: nuget
ms.technology: 
description: "包括已知的问题、 bug 修复、 增加的功能，以及 DCRs NuGet 1.3 的发行说明。"
keywords: "NuGet 1.3 发行说明，bug 修复的已知问题，添加了一些功能，DCRs"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 59169be5b39ba4436e13e0935a0ad6efa724e08e
ms.sourcegitcommit: 262d026beeffd4f3b6fc47d780a2f701451663a8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/25/2018
---
# <a name="nuget-13-release-notes"></a><span data-ttu-id="df7fe-104">NuGet 1.3 的发行说明</span><span class="sxs-lookup"><span data-stu-id="df7fe-104">NuGet 1.3 Release Notes</span></span>

<span data-ttu-id="df7fe-105">[NuGet 1.2 发行说明](../release-notes/nuget-1.2.md) | [NuGet 1.4 的发行说明](../release-notes/nuget-1.4.md)</span><span class="sxs-lookup"><span data-stu-id="df7fe-105">[NuGet 1.2 Release Notes](../release-notes/nuget-1.2.md) | [NuGet 1.4 Release Notes](../release-notes/nuget-1.4.md)</span></span>

<span data-ttu-id="df7fe-106">NuGet 1.3 已于 2011 年 4 月 25 日发布。</span><span class="sxs-lookup"><span data-stu-id="df7fe-106">NuGet 1.3 was released on April 25, 2011.</span></span>

## <a name="new-features"></a><span data-ttu-id="df7fe-107">新增功能</span><span class="sxs-lookup"><span data-stu-id="df7fe-107">New Features</span></span>

### <a name="streamlined-package-creation-with-symbol-server-integration"></a><span data-ttu-id="df7fe-108">简化的创建符号服务器集成包</span><span class="sxs-lookup"><span data-stu-id="df7fe-108">Streamlined Package Creation with symbol server integration</span></span>

<span data-ttu-id="df7fe-109">NuGet 团队的整个过程的人员合作[SymbolSource.org](http://www.symbolsource.org/)以提供了非常简单的方法，以及你的包中发布你的源和 PDB。</span><span class="sxs-lookup"><span data-stu-id="df7fe-109">The NuGet team partnered with the folks at [SymbolSource.org](http://www.symbolsource.org/) to offer a really simple way of publishing your sources and PDB’s along with your package.</span></span> <span data-ttu-id="df7fe-110">这允许你的包的使用者单步执行你在调试器中的包的源。</span><span class="sxs-lookup"><span data-stu-id="df7fe-110">This allows consumers of your package to step into the source for your package in the debugger.</span></span> <span data-ttu-id="df7fe-111">有关详细信息，请阅读[创建和发布符号包](../create-packages/symbol-packages.md)发布 NuGet 包与源的简单方法。</span><span class="sxs-lookup"><span data-stu-id="df7fe-111">For more details, read [Creating and Publishing a Symbol Package](../create-packages/symbol-packages.md) The easy way to publish NuGet packages with sources.</span></span> <span data-ttu-id="df7fe-112">你也可以观看实时演示此功能的深度 NuGet 的一部分在 Mix11 对话。</span><span class="sxs-lookup"><span data-stu-id="df7fe-112">You can also watch a live demonstration of this feature as part of the NuGet in Depth talk at Mix11.</span></span> <span data-ttu-id="df7fe-113">此功能完全进行了演示视频的 20 分钟标记处开始。</span><span class="sxs-lookup"><span data-stu-id="df7fe-113">This feature is fully demonstrated starting at the 20 minute mark of the video.</span></span>

### <a name="open-packagepage-command"></a><span data-ttu-id="df7fe-114">`Open-PackagePage`命令</span><span class="sxs-lookup"><span data-stu-id="df7fe-114">`Open-PackagePage` Command</span></span>

<span data-ttu-id="df7fe-115">此命令可以轻松获取到从程序包管理器控制台中的包的项目页。</span><span class="sxs-lookup"><span data-stu-id="df7fe-115">This command makes it easy to get to the project page for a package from within the Package Manager Console.</span></span> <span data-ttu-id="df7fe-116">它还提供了选项，若要打开的许可证 URL 和包的报告滥用行为页。</span><span class="sxs-lookup"><span data-stu-id="df7fe-116">It also provides options to open the license URL and the report abuse page for the package.</span></span>
<span data-ttu-id="df7fe-117">该命令的语法是：</span><span class="sxs-lookup"><span data-stu-id="df7fe-117">The syntax for the command is:</span></span>

    Open-PackagePage -Id <string> [-Version] [-Source] [-License] [-ReportAbuse] [-PassThru]

<span data-ttu-id="df7fe-118">`-PassThru`选项用于返回指定的 URL 的值。</span><span class="sxs-lookup"><span data-stu-id="df7fe-118">The `-PassThru` option is used to return the value of the specified URL.</span></span>

<span data-ttu-id="df7fe-119">示例：</span><span class="sxs-lookup"><span data-stu-id="df7fe-119">Examples:</span></span>

    PM> Open-PackagePage Ninject

<span data-ttu-id="df7fe-120">将打开 Ninject 程序包中指定的项目 URL 在浏览器。</span><span class="sxs-lookup"><span data-stu-id="df7fe-120">Opens a browser to the project URL specified in the Ninject package.</span></span>

    PM> Open-PackagePage Ninject -License

<span data-ttu-id="df7fe-121">将打开 Ninject 程序包中指定的许可证 URL 在浏览器。</span><span class="sxs-lookup"><span data-stu-id="df7fe-121">Opens a browser to the license URL specified in the Ninject package.</span></span>

    PM> Open-PackagePage Ninject -ReportAbuse

<span data-ttu-id="df7fe-122">打开浏览器中用于指定包的报告滥用行为的当前程序包源的 URL。</span><span class="sxs-lookup"><span data-stu-id="df7fe-122">Opens a browser to the URL at the current package source used to report abuse for the specified package.</span></span>

    PM> $url = Open-PackagePage Ninject -License -WhatIf -PassThru

<span data-ttu-id="df7fe-123">将许可证 URL 分配给变量，$url，，而无需在浏览器打开 URL。</span><span class="sxs-lookup"><span data-stu-id="df7fe-123">Assigns the license URL to the variable, $url, without opening the URL in a browser.</span></span>

### <a name="performance-improvements"></a><span data-ttu-id="df7fe-124">性能改进</span><span class="sxs-lookup"><span data-stu-id="df7fe-124">Performance Improvements</span></span>

<span data-ttu-id="df7fe-125">NuGet 1.3 引入了大量的性能改进。</span><span class="sxs-lookup"><span data-stu-id="df7fe-125">NuGet 1.3 introduces a lot of performance improvements.</span></span> <span data-ttu-id="df7fe-126">NuGet 1.3 可避免通过包括每用户本地缓存多次下载相同版本的包。</span><span class="sxs-lookup"><span data-stu-id="df7fe-126">NuGet 1.3 avoids downloading the same version of a package multiple times by including a local per-user cache.</span></span> <span data-ttu-id="df7fe-127">可以访问缓存，并将其清除通过程序包管理器设置对话框：</span><span class="sxs-lookup"><span data-stu-id="df7fe-127">The cache can be accessed and cleared via the Package Manager Settings dialog:</span></span>

![使用包缓存设置的 NuGet 选项对话框](./media/nuget-options.png)

<span data-ttu-id="df7fe-129">其他性能改进包括添加对 HTTP 压缩的支持和改进 Visual Studio 中的包安装速度。</span><span class="sxs-lookup"><span data-stu-id="df7fe-129">Other performance improvements include adding support for HTTP compression and improving the package installation speed within Visual Studio.</span></span>

### <a name="visual-studio-and-nugetexe-uses-the-same-list-of-package-sources"></a><span data-ttu-id="df7fe-130">Visual Studio 和 nuget.exe 使用相同的包源列表</span><span class="sxs-lookup"><span data-stu-id="df7fe-130">Visual Studio and nuget.exe uses the same list of package sources</span></span>

<span data-ttu-id="df7fe-131">在 NuGet 1.3 之前 nuget.exe 和 NuGet Visual Studio 外接程序使用的包源的列表未存储在同一位置。</span><span class="sxs-lookup"><span data-stu-id="df7fe-131">Prior to NuGet 1.3, the list of package sources used by nuget.exe and the NuGet Visual Studio Add-In were not stored in the same place.</span></span> <span data-ttu-id="df7fe-132">NuGet 1.3 现在使用这两个位置中的相同列表。</span><span class="sxs-lookup"><span data-stu-id="df7fe-132">NuGet 1.3 now uses the same list in both places.</span></span> <span data-ttu-id="df7fe-133">列表存储在`NuGet.Config`并且存储在应用程序数据文件夹。</span><span class="sxs-lookup"><span data-stu-id="df7fe-133">The list is stored in `NuGet.Config` and stored in the AppData folder.</span></span>

### <a name="nugetexe-ignores-files-and-folders-that-start-with--by-default"></a><span data-ttu-id="df7fe-134">nuget.exe 忽略文件和文件夹以开头的。 默认情况下</span><span class="sxs-lookup"><span data-stu-id="df7fe-134">nuget.exe Ignores Files and Folders that start with '.' by default</span></span>

<span data-ttu-id="df7fe-135">为了进行很好地配合源代码管理系统，此类子版本号和 Mercurial 的 NuGet，nuget.exe 忽略文件夹和开头的文件。 ' 字符创建包时。</span><span class="sxs-lookup"><span data-stu-id="df7fe-135">In order to make NuGet work well with source control systems such Subversion and Mercurial, nuget.exe ignores folders and files that start with the '.' character when creating packages.</span></span> <span data-ttu-id="df7fe-136">这可以重写使用两个新的标志：</span><span class="sxs-lookup"><span data-stu-id="df7fe-136">This can be overridden using two new flags:</span></span>

* <span data-ttu-id="df7fe-137">__-NoDefaultExcludes__用于重写此设置，并包括所有文件。</span><span class="sxs-lookup"><span data-stu-id="df7fe-137">__-NoDefaultExcludes__ is used to override this setting and include all files.</span></span>
* <span data-ttu-id="df7fe-138">__-排除__用于添加要使用的模式中排除其他文件/文件夹。</span><span class="sxs-lookup"><span data-stu-id="df7fe-138">__-Exclude__ is used to add other files/folders to exclude using a pattern.</span></span> <span data-ttu-id="df7fe-139">例如，若要排除具有 '.bak' 文件扩展名的所有文件</span><span class="sxs-lookup"><span data-stu-id="df7fe-139">For example, to exclude all files with the '.bak' file extension</span></span>

```
nuget Pack MyPackage.nuspec -Exclude **\*.bak
```  

<span data-ttu-id="df7fe-140">_注意： 的模式不是默认情况下的递归。_</span><span class="sxs-lookup"><span data-stu-id="df7fe-140">_Note: the pattern is not recursive by default._</span></span>

### <a name="support-for-wix-projects-and-the-net-micro-framework"></a><span data-ttu-id="df7fe-141">WiX 项目和.NET Micro Framework 的支持</span><span class="sxs-lookup"><span data-stu-id="df7fe-141">Support for WiX Projects and the .NET Micro Framework</span></span>

<span data-ttu-id="df7fe-142">感谢社区贡献 NuGet 包括对 WiX 项目类型，以及.NET Micro Framework 支持。</span><span class="sxs-lookup"><span data-stu-id="df7fe-142">Thanks to community contributions, NuGet includes support for WiX project types as well as the .NET Micro Framework.</span></span>

## <a name="bug-fixes"></a><span data-ttu-id="df7fe-143">Bug 修复</span><span class="sxs-lookup"><span data-stu-id="df7fe-143">Bug Fixes</span></span>

<span data-ttu-id="df7fe-144">Bug 修复的完整列表，请查看[对于此版本的 NuGet 问题跟踪程序](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=All&type=All&priority=All&release=NuGet%201.3&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0)。</span><span class="sxs-lookup"><span data-stu-id="df7fe-144">For a full list of bug fixes, please view the [NuGet Issue Tracker for this release](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=All&type=All&priority=All&release=NuGet%201.3&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0).</span></span>

## <a name="bug-fixes-worth-noting"></a><span data-ttu-id="df7fe-145">值得注意的 bug 修复</span><span class="sxs-lookup"><span data-stu-id="df7fe-145">Bug fixes worth noting</span></span>

* <span data-ttu-id="df7fe-146">源文件的包可以使用这两个网站和 Web 应用程序项目中。</span><span class="sxs-lookup"><span data-stu-id="df7fe-146">Packages with source files work in both Websites and in Web Application Projects.</span></span>
<span data-ttu-id="df7fe-147">对于网站，将源文件复制到`App_Code`文件夹</span><span class="sxs-lookup"><span data-stu-id="df7fe-147">For Websites, source files are copied into the `App_Code` folder</span></span>
