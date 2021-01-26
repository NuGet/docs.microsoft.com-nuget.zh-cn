---
title: NuGet 1.3 发行说明
description: NuGet 1.3 的发行说明，包括已知问题、bug 修复、新增功能和 Dcr。
author: JonDouglas
ms.author: jodou
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 54eda149352810eacc1d6340ad16cec1b03194e3
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/26/2021
ms.locfileid: "98777115"
---
# <a name="nuget-13-release-notes"></a><span data-ttu-id="d0530-103">NuGet 1.3 发行说明</span><span class="sxs-lookup"><span data-stu-id="d0530-103">NuGet 1.3 Release Notes</span></span>

<span data-ttu-id="d0530-104">[NuGet 1.2 发行说明](../release-notes/nuget-1.2.md)  | [NuGet 1.4 发行说明](../release-notes/nuget-1.4.md)</span><span class="sxs-lookup"><span data-stu-id="d0530-104">[NuGet 1.2 Release Notes](../release-notes/nuget-1.2.md) | [NuGet 1.4 Release Notes](../release-notes/nuget-1.4.md)</span></span>

<span data-ttu-id="d0530-105">NuGet 1.3 于2011年4月25日发布。</span><span class="sxs-lookup"><span data-stu-id="d0530-105">NuGet 1.3 was released on April 25, 2011.</span></span>

## <a name="new-features"></a><span data-ttu-id="d0530-106">新功能</span><span class="sxs-lookup"><span data-stu-id="d0530-106">New Features</span></span>

### <a name="streamlined-package-creation-with-symbol-server-integration"></a><span data-ttu-id="d0530-107">通过符号服务器集成简化包创建</span><span class="sxs-lookup"><span data-stu-id="d0530-107">Streamlined Package Creation with symbol server integration</span></span>

<span data-ttu-id="d0530-108">NuGet 团队与 [SymbolSource.org](http://www.symbolsource.org/) 的用户进行了合作，提供了一种非常简单的方式来将源和 PDB 与包一起发布。</span><span class="sxs-lookup"><span data-stu-id="d0530-108">The NuGet team partnered with the folks at [SymbolSource.org](http://www.symbolsource.org/) to offer a really simple way of publishing your sources and PDB’s along with your package.</span></span> <span data-ttu-id="d0530-109">这允许你的包的使用者在调试器中单步执行包的源。</span><span class="sxs-lookup"><span data-stu-id="d0530-109">This allows consumers of your package to step into the source for your package in the debugger.</span></span> <span data-ttu-id="d0530-110">有关更多详细信息，请参阅 [创建和发布符号包](../create-packages/symbol-packages.md) 使用源发布 NuGet 包的简单方法。</span><span class="sxs-lookup"><span data-stu-id="d0530-110">For more details, read [Creating and Publishing a Symbol Package](../create-packages/symbol-packages.md) The easy way to publish NuGet packages with sources.</span></span> <span data-ttu-id="d0530-111">你还可以观看此功能的实时演示，作为 NuGet 深入了解 Mix11。</span><span class="sxs-lookup"><span data-stu-id="d0530-111">You can also watch a live demonstration of this feature as part of the NuGet in Depth talk at Mix11.</span></span> <span data-ttu-id="d0530-112">此功能在视频的20分钟标记处开始完全演示。</span><span class="sxs-lookup"><span data-stu-id="d0530-112">This feature is fully demonstrated starting at the 20 minute mark of the video.</span></span>

### <a name="open-packagepage-command"></a><span data-ttu-id="d0530-113">`Open-PackagePage` 命令</span><span class="sxs-lookup"><span data-stu-id="d0530-113">`Open-PackagePage` Command</span></span>

<span data-ttu-id="d0530-114">使用此命令可以轻松地从包管理器控制台中访问包的项目页。</span><span class="sxs-lookup"><span data-stu-id="d0530-114">This command makes it easy to get to the project page for a package from within the Package Manager Console.</span></span> <span data-ttu-id="d0530-115">它还提供了用于打开包的 "许可证 URL" 和 "报表滥用" 页的选项。</span><span class="sxs-lookup"><span data-stu-id="d0530-115">It also provides options to open the license URL and the report abuse page for the package.</span></span>
<span data-ttu-id="d0530-116">命令的语法为：</span><span class="sxs-lookup"><span data-stu-id="d0530-116">The syntax for the command is:</span></span>

```
Open-PackagePage -Id <string> [-Version] [-Source] [-License] [-ReportAbuse] [-PassThru]
```

<span data-ttu-id="d0530-117">`-PassThru`选项用于返回指定 URL 的值。</span><span class="sxs-lookup"><span data-stu-id="d0530-117">The `-PassThru` option is used to return the value of the specified URL.</span></span>

<span data-ttu-id="d0530-118">示例:</span><span class="sxs-lookup"><span data-stu-id="d0530-118">Examples:</span></span>

```
PM> Open-PackagePage Ninject
```

<span data-ttu-id="d0530-119">打开浏览器，指向在 Ninject 包中指定的项目 URL。</span><span class="sxs-lookup"><span data-stu-id="d0530-119">Opens a browser to the project URL specified in the Ninject package.</span></span>

```
PM> Open-PackagePage Ninject -License
```

<span data-ttu-id="d0530-120">打开浏览器，指向在 Ninject 包中指定的许可证 URL。</span><span class="sxs-lookup"><span data-stu-id="d0530-120">Opens a browser to the license URL specified in the Ninject package.</span></span>

```
PM> Open-PackagePage Ninject -ReportAbuse
```

<span data-ttu-id="d0530-121">打开浏览器，指向当前包源中用于报告指定包的滥用的 URL。</span><span class="sxs-lookup"><span data-stu-id="d0530-121">Opens a browser to the URL at the current package source used to report abuse for the specified package.</span></span>

```
PM> $url = Open-PackagePage Ninject -License -WhatIf -PassThru
```

<span data-ttu-id="d0530-122">将许可证 URL 分配给变量 $url，而无需在浏览器中打开该 URL。</span><span class="sxs-lookup"><span data-stu-id="d0530-122">Assigns the license URL to the variable, $url, without opening the URL in a browser.</span></span>

### <a name="performance-improvements"></a><span data-ttu-id="d0530-123">性能改进</span><span class="sxs-lookup"><span data-stu-id="d0530-123">Performance Improvements</span></span>

<span data-ttu-id="d0530-124">NuGet 1.3 引入了大量性能改进。</span><span class="sxs-lookup"><span data-stu-id="d0530-124">NuGet 1.3 introduces a lot of performance improvements.</span></span> <span data-ttu-id="d0530-125">NuGet 1.3 通过包含本地的每用户缓存避免多次下载包的同一版本。</span><span class="sxs-lookup"><span data-stu-id="d0530-125">NuGet 1.3 avoids downloading the same version of a package multiple times by including a local per-user cache.</span></span> <span data-ttu-id="d0530-126">可以通过 "包管理器设置" 对话框访问和清除缓存：</span><span class="sxs-lookup"><span data-stu-id="d0530-126">The cache can be accessed and cleared via the Package Manager Settings dialog:</span></span>

![包含包缓存设置的 NuGet 选项对话框](./media/nuget-options.png)

<span data-ttu-id="d0530-128">其他性能改进包括添加对 HTTP 压缩的支持和在 Visual Studio 中提高包的安装速度。</span><span class="sxs-lookup"><span data-stu-id="d0530-128">Other performance improvements include adding support for HTTP compression and improving the package installation speed within Visual Studio.</span></span>

### <a name="visual-studio-and-nugetexe-uses-the-same-list-of-package-sources"></a><span data-ttu-id="d0530-129">Visual Studio 和 nuget.exe 使用相同的包源列表</span><span class="sxs-lookup"><span data-stu-id="d0530-129">Visual Studio and nuget.exe uses the same list of package sources</span></span>

<span data-ttu-id="d0530-130">在 NuGet 1.3 之前，nuget.exe 和 NuGet Visual Studio Add-In 使用的包源列表未存储在同一位置。</span><span class="sxs-lookup"><span data-stu-id="d0530-130">Prior to NuGet 1.3, the list of package sources used by nuget.exe and the NuGet Visual Studio Add-In were not stored in the same place.</span></span> <span data-ttu-id="d0530-131">NuGet 1.3 现在同时在这两个位置使用同一列表。</span><span class="sxs-lookup"><span data-stu-id="d0530-131">NuGet 1.3 now uses the same list in both places.</span></span> <span data-ttu-id="d0530-132">该列表存储在中 `NuGet.Config` 并存储在 AppData 文件夹中。</span><span class="sxs-lookup"><span data-stu-id="d0530-132">The list is stored in `NuGet.Config` and stored in the AppData folder.</span></span>

### <a name="nugetexe-ignores-files-and-folders-that-start-with--by-default"></a><span data-ttu-id="d0530-133">默认情况下，nuget.exe 忽略以 "." 开头的文件和文件夹</span><span class="sxs-lookup"><span data-stu-id="d0530-133">nuget.exe Ignores Files and Folders that start with '.' by default</span></span>

<span data-ttu-id="d0530-134">为了使 NuGet 更好地用于源控制系统（如 Subversion 和 Mercurial），nuget.exe 在创建包时忽略以 "." 字符开头的文件夹和文件。</span><span class="sxs-lookup"><span data-stu-id="d0530-134">In order to make NuGet work well with source control systems such Subversion and Mercurial, nuget.exe ignores folders and files that start with the '.' character when creating packages.</span></span> <span data-ttu-id="d0530-135">这可以使用两个新标志进行重写：</span><span class="sxs-lookup"><span data-stu-id="d0530-135">This can be overridden using two new flags:</span></span>

* <span data-ttu-id="d0530-136">__-NoDefaultExcludes__ 用于覆盖此设置并包括所有文件。</span><span class="sxs-lookup"><span data-stu-id="d0530-136">__-NoDefaultExcludes__ is used to override this setting and include all files.</span></span>
* <span data-ttu-id="d0530-137">__-Exclude__ 用于使用模式添加要排除的其他文件/文件夹。</span><span class="sxs-lookup"><span data-stu-id="d0530-137">__-Exclude__ is used to add other files/folders to exclude using a pattern.</span></span> <span data-ttu-id="d0530-138">例如，若要排除文件扩展名为 ".bak" 的所有文件</span><span class="sxs-lookup"><span data-stu-id="d0530-138">For example, to exclude all files with the '.bak' file extension</span></span>

```cli
nuget Pack MyPackage.nuspec -Exclude **\*.bak
```  

<span data-ttu-id="d0530-139">_注意：默认情况下，该模式不是递归的。_</span><span class="sxs-lookup"><span data-stu-id="d0530-139">_Note: the pattern is not recursive by default._</span></span>

### <a name="support-for-wix-projects-and-the-net-micro-framework"></a><span data-ttu-id="d0530-140">对 WiX 项目和 .NET 微框架的支持</span><span class="sxs-lookup"><span data-stu-id="d0530-140">Support for WiX Projects and the .NET Micro Framework</span></span>

<span data-ttu-id="d0530-141">由于社区贡献，NuGet 包含对 WiX 项目类型和 .NET 微框架的支持。</span><span class="sxs-lookup"><span data-stu-id="d0530-141">Thanks to community contributions, NuGet includes support for WiX project types as well as the .NET Micro Framework.</span></span>

## <a name="bug-fixes"></a><span data-ttu-id="d0530-142">Bug 修复</span><span class="sxs-lookup"><span data-stu-id="d0530-142">Bug Fixes</span></span>

<span data-ttu-id="d0530-143">有关 bug 修复的完整列表，请查看 [此版本的 NuGet 问题跟踪](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=All&type=All&priority=All&release=NuGet%201.3&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0)程序。</span><span class="sxs-lookup"><span data-stu-id="d0530-143">For a full list of bug fixes, please view the [NuGet Issue Tracker for this release](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=All&type=All&priority=All&release=NuGet%201.3&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0).</span></span>

## <a name="bug-fixes-worth-noting"></a><span data-ttu-id="d0530-144">Bug 修复值得注意</span><span class="sxs-lookup"><span data-stu-id="d0530-144">Bug fixes worth noting</span></span>

* <span data-ttu-id="d0530-145">包含源文件的包可在网站和 Web 应用程序项目中使用。</span><span class="sxs-lookup"><span data-stu-id="d0530-145">Packages with source files work in both Websites and in Web Application Projects.</span></span>
<span data-ttu-id="d0530-146">对于网站，源文件将复制到文件夹中 `App_Code`</span><span class="sxs-lookup"><span data-stu-id="d0530-146">For Websites, source files are copied into the `App_Code` folder</span></span>
