---
title: 查找和选择 NuGet 包
description: 概述如何查找和选择最适合项目的 NuGet 包，包括有关 NuGet 搜索语法的详细信息。
author: karann-msft
ms.author: karann
ms.date: 06/04/2018
ms.topic: conceptual
ms.openlocfilehash: 8cd7529c4a1ecf659abde03fb1632e26431aebf3
ms.sourcegitcommit: b6810860b77b2d50aab031040b047c20a333aca3
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/28/2019
ms.locfileid: "67426753"
---
# <a name="finding-and-evaluating-nuget-packages-for-your-project"></a><span data-ttu-id="60dbd-103">针对项目查找和评估 NuGet 包</span><span class="sxs-lookup"><span data-stu-id="60dbd-103">Finding and evaluating NuGet packages for your project</span></span>

<span data-ttu-id="60dbd-104">启动任何 .NET 项目或识别应用或服务的功能需求时，使用可满足该需求的现有 NuGet 包可以大大地省时省力。</span><span class="sxs-lookup"><span data-stu-id="60dbd-104">When starting any .NET project, or whenever you identify a functional need for your app or service, you can save yourself lots of time and trouble by using existing NuGet packages that fulfill that need.</span></span> <span data-ttu-id="60dbd-105">这些包可能来自 [nuget.org](http://www.nuget.org/packages/) 中的公共集合，也可能来自组织或其他第三方提供的私有源。</span><span class="sxs-lookup"><span data-stu-id="60dbd-105">These packages can come from the public collection on [nuget.org](http://www.nuget.org/packages/), or a private source that's provided by your organization or another third party.</span></span>

## <a name="finding-packages"></a><span data-ttu-id="60dbd-106">查找包</span><span class="sxs-lookup"><span data-stu-id="60dbd-106">Finding packages</span></span>

<span data-ttu-id="60dbd-107">访问 nuget.org 或打开 Visual Studio 中的程序包管理器 UI 时，其中会显示一个包列表，这些包按总下载次数排列。</span><span class="sxs-lookup"><span data-stu-id="60dbd-107">When you visit nuget.org or open the Package Manager UI in Visual Studio, you see a list of packages sorted by total downloads.</span></span> <span data-ttu-id="60dbd-108">你可以立即看出在数以百万的 .NET 项目中使用次数最多的包。</span><span class="sxs-lookup"><span data-stu-id="60dbd-108">This immediately shows you the most widely-used packages across the millions of .NET projects.</span></span> <span data-ttu-id="60dbd-109">很可能前几页列出的某些包就适用于你的项目。</span><span class="sxs-lookup"><span data-stu-id="60dbd-109">There's a good chance, then, that at least some of the packages listed on the first few pages will be useful in your projects.</span></span>

![显示最常用包的 nuget.org/packages 的默认视图](media/Finding-01-Popularity.png)

<span data-ttu-id="60dbd-111">请注意页面右上角的“包括预发行版”选项  。</span><span class="sxs-lookup"><span data-stu-id="60dbd-111">Notice the **Include prerelease** option on the upper right of the page.</span></span> <span data-ttu-id="60dbd-112">勾选此选项时，nuget.org 将显示所有版本的包，包括 beta 版本和其他早期版本。</span><span class="sxs-lookup"><span data-stu-id="60dbd-112">When selected, nuget.org shows all versions of packages including beta and other early releases.</span></span> <span data-ttu-id="60dbd-113">若要仅显示稳定版本，请清除此选项。</span><span class="sxs-lookup"><span data-stu-id="60dbd-113">To show only stable released, clear the option.</span></span>

<span data-ttu-id="60dbd-114">对于特定需求，按标记搜索（在 Visual Studio 包管理器或在 nuget.org 等门户中）是发现适用包的最常用方法。</span><span class="sxs-lookup"><span data-stu-id="60dbd-114">For specific needs, searching by tags (within the Visual Studio Package Manager or on a portal like nuget.org) is the most common means of discovering a suitable package.</span></span> <span data-ttu-id="60dbd-115">例如，搜索“json”将列出具有该关键字标记的所有 NuGet 包，这些包必然与 JSON 数据格式存在某种关系。</span><span class="sxs-lookup"><span data-stu-id="60dbd-115">For example, searching on "json" lists all NuGet packages that are tagged with that keyword and thus have some relationship to the JSON data format.</span></span>

![nuget.org 中“json”的搜索结果](media/Finding-02-SearchResults.png)

<span data-ttu-id="60dbd-117">还可以使用包 ID 进行搜索（如果知道）。</span><span class="sxs-lookup"><span data-stu-id="60dbd-117">You can also search using the package ID, if you know it.</span></span> <span data-ttu-id="60dbd-118">请参阅下面的[搜索语法](#search-syntax)。</span><span class="sxs-lookup"><span data-stu-id="60dbd-118">See [Search Syntax](#search-syntax) below.</span></span>

<span data-ttu-id="60dbd-119">在此情况下，搜索结果将仅按相关性进行排序，因此通常至少需要浏览前几页结果才能找到满足需求的包；也可以优化搜索词，使其更加具体。</span><span class="sxs-lookup"><span data-stu-id="60dbd-119">At this time, search results are sorted only by relevance, so you generally want to look through at least the first few pages of results for packages that suit your needs, or refine your search terms to be more specific.</span></span>

### <a name="does-the-package-support-my-projects-target-framework"></a><span data-ttu-id="60dbd-120">包是否支持项目的目标框架？</span><span class="sxs-lookup"><span data-stu-id="60dbd-120">Does the package support my project's target framework?</span></span>

<span data-ttu-id="60dbd-121">仅当包支持的框架中包含该项目的目标框架时，NuGet 才会在项目中安装包。</span><span class="sxs-lookup"><span data-stu-id="60dbd-121">NuGet installs a package into a project only if that package's supported frameworks include the project's target framework.</span></span> <span data-ttu-id="60dbd-122">如果包不兼容，NuGet 将发出错误。</span><span class="sxs-lookup"><span data-stu-id="60dbd-122">If the package is not compatible, NuGet issues an error.</span></span>

<span data-ttu-id="60dbd-123">某些包会直接在 nuget.org 库中列出其支持的框架，但由于这些不是必需数据，因此许多包不会包含此列表。</span><span class="sxs-lookup"><span data-stu-id="60dbd-123">Some packages list their supported frameworks directly in the nuget.org gallery, but because such data is not required, many packages do not include that list.</span></span> <span data-ttu-id="60dbd-124">目前不支持在 nuget.org 中搜索支持特定目标框架的包（此功能处于考虑阶段，请参阅 [NuGet 问题 2936](https://github.com/NuGet/NuGetGallery/issues/2936)）。</span><span class="sxs-lookup"><span data-stu-id="60dbd-124">At present there is no means to search nuget.org for packages that support a specific target framework (the feature is under consideration, see [NuGet Issue 2936](https://github.com/NuGet/NuGetGallery/issues/2936)).</span></span>

<span data-ttu-id="60dbd-125">幸运的是，你可以通过以下两种方法确定受支持的框架：</span><span class="sxs-lookup"><span data-stu-id="60dbd-125">Fortunately, you can determine supported frameworks through two other means:</span></span>

1. <span data-ttu-id="60dbd-126">尝试在 NuGet 包管理器控制台中使用 [`Install-Package`](../tools/ps-ref-install-package.md) 命令将包安装到项目中。</span><span class="sxs-lookup"><span data-stu-id="60dbd-126">Attempt to install a package into a project using the [`Install-Package`](../tools/ps-ref-install-package.md) command in the NuGet Package Manager Console.</span></span> <span data-ttu-id="60dbd-127">如果包不兼容，此命令将显示包支持的框架。</span><span class="sxs-lookup"><span data-stu-id="60dbd-127">If the package is incompatible, this command shows you the package's supported frameworks.</span></span>

1. <span data-ttu-id="60dbd-128">在 nuget.org 中包的页面上，使用“信息”下的“手动下载”链接来下载包   。</span><span class="sxs-lookup"><span data-stu-id="60dbd-128">Download the package from its page on nuget.org using the **Manual download** link under **Info**.</span></span> <span data-ttu-id="60dbd-129">将扩展名从 `.nupkg` 更改为 `.zip`，然后打开文件查看 `lib` 文件夹的内容。</span><span class="sxs-lookup"><span data-stu-id="60dbd-129">Change the extension from `.nupkg` to `.zip`, and open the file to examine the content of its `lib` folder.</span></span> <span data-ttu-id="60dbd-130">你会看到每个受支持框架的子文件夹，每个子文件夹都以目标框架名字对象 (TFM)（请参阅[目标框架](../reference/target-frameworks.md)）命名。</span><span class="sxs-lookup"><span data-stu-id="60dbd-130">There you see subfolders for each of the supported frameworks, where each subfolder is named with a target framework moniker (TFM; see [Target Frameworks](../reference/target-frameworks.md)).</span></span> <span data-ttu-id="60dbd-131">如果 `lib` 下没有任何子文件夹而只有一个 DLL，此时则必须通过尝试将包安装到项目中来查看其是否兼容。</span><span class="sxs-lookup"><span data-stu-id="60dbd-131">If you see no subfolders under `lib` and only a single DLL, then you must attempt to install the package in your project to discover its compatibility.</span></span>

## <a name="pre-release-packages"></a><span data-ttu-id="60dbd-132">预发行包</span><span class="sxs-lookup"><span data-stu-id="60dbd-132">Pre-release packages</span></span>

<span data-ttu-id="60dbd-133">许多包创建者会提供预览版和 beta 版，他们会继续提供改进并收集其最新版本的反馈。</span><span class="sxs-lookup"><span data-stu-id="60dbd-133">Many package authors make preview and beta releases available as they continue to make improvements and seek feedback on their latest revisions.</span></span>

<span data-ttu-id="60dbd-134">默认情况下，nuget.org 会在搜索结果中显示预发行包。</span><span class="sxs-lookup"><span data-stu-id="60dbd-134">By default, nuget.org shows pre-release packages in search results.</span></span> <span data-ttu-id="60dbd-135">若要仅搜索稳定版发布，请清除页面右上角的“包括预发行版”选项 </span><span class="sxs-lookup"><span data-stu-id="60dbd-135">To search only stable releases, clear the **Include prerelease** option on the upper right of the page</span></span>

![nuget.org 上的“包括预发行版”复选框](media/Finding-06-include-prerelease.png)

<span data-ttu-id="60dbd-137">在 Visual Studio 中使用 NuGet 和 dotnet CLI 工具时，NuGet 默认不包括预发行版本。</span><span class="sxs-lookup"><span data-stu-id="60dbd-137">In Visual Studio, and when using the NuGet and dotnet CLI tools, NuGet does not include pre-release versions by default.</span></span> <span data-ttu-id="60dbd-138">若要更改此行为，请执行以下操作：</span><span class="sxs-lookup"><span data-stu-id="60dbd-138">To change this behavior, do the following steps:</span></span>

- <span data-ttu-id="60dbd-139">**Visual Studio 中的包管理器 UI**：在“管理 NuGet 包”UI 中，勾选“包括预发行版”框   。</span><span class="sxs-lookup"><span data-stu-id="60dbd-139">**Package Manager UI in Visual Studio**: In the **Manage NuGet Packages** UI, set the **Include prerelease** box.</span></span> <span data-ttu-id="60dbd-140">勾选或清除此框将刷新包管理器 UI 和可安装的可用版本列表。</span><span class="sxs-lookup"><span data-stu-id="60dbd-140">Setting or clearing this box refreshes the Package Manager UI and the list of available versions you can install.</span></span>

    ![Visual Studio 中的“包括预发行版”复选框](media/Prerelease_02-CheckPrerelease.png)

- <span data-ttu-id="60dbd-142">**包管理器控制台**：将 `-IncludePrerelease` 开关与 `Find-Package`、`Get-Package`、`Install-Package``Sync-Package` 和 `Update-Package` 命令配合使用。</span><span class="sxs-lookup"><span data-stu-id="60dbd-142">**Package Manager Console**: Use the `-IncludePrerelease` switch with the `Find-Package`, `Get-Package`, `Install-Package`, `Sync-Package`, and `Update-Package` commands.</span></span> <span data-ttu-id="60dbd-143">请参阅 [PowerShell 参考](../tools/powershell-reference.md)。</span><span class="sxs-lookup"><span data-stu-id="60dbd-143">Refer to the [PowerShell Reference](../tools/powershell-reference.md).</span></span>

- <span data-ttu-id="60dbd-144">**nuget.exe CLI**：将 `-prerelease` 开关与 `install`、`update`、`delete` 和 `mirror` 命令配合使用。</span><span class="sxs-lookup"><span data-stu-id="60dbd-144">**nuget.exe CLI**: Use the `-prerelease` switch with the `install`, `update`, `delete`, and `mirror` commands.</span></span> <span data-ttu-id="60dbd-145">请参阅 [NuGet CLI 参考](../tools/nuget-exe-cli-reference.md)</span><span class="sxs-lookup"><span data-stu-id="60dbd-145">Refer to the [NuGet CLI reference](../tools/nuget-exe-cli-reference.md)</span></span>

- <span data-ttu-id="60dbd-146">**dotnet.exe CLI**：使用 `-v` 参数指定确切的预发行版本。</span><span class="sxs-lookup"><span data-stu-id="60dbd-146">**dotnet.exe CLI**: Specify the exact pre-release version using the `-v` argument.</span></span> <span data-ttu-id="60dbd-147">请参阅 [dotnet 添加包参考](/dotnet/core/tools/dotnet-add-package)。</span><span class="sxs-lookup"><span data-stu-id="60dbd-147">Refer to the [dotnet add package reference](/dotnet/core/tools/dotnet-add-package).</span></span>

<a name="native-cpp-packages"></a>

### <a name="native-c-packages"></a><span data-ttu-id="60dbd-148">本机 C++ 包</span><span class="sxs-lookup"><span data-stu-id="60dbd-148">Native C++ packages</span></span>

<span data-ttu-id="60dbd-149">NuGet 支持本机 C++ 包，这些包可在 Visual Studio 的 C++ 项目中使用。</span><span class="sxs-lookup"><span data-stu-id="60dbd-149">NuGet supports native C++ packages can that can be used in C++ projects in Visual Studio.</span></span> <span data-ttu-id="60dbd-150">这将启用项目的“管理 NuGet 包”上下文菜单命令、引入 `native` 目标框架，以及提供 MSBuild 集成  。</span><span class="sxs-lookup"><span data-stu-id="60dbd-150">This enables the **Manage NuGet Packages** context-menu command for projects, introduces a `native` target framework, and provides MSBuild integration.</span></span>

<span data-ttu-id="60dbd-151">若要在 [nuget.org](https://www.nuget.org/packages) 中查找本机包，请搜索 `tag:native`。</span><span class="sxs-lookup"><span data-stu-id="60dbd-151">To find native packages on [nuget.org](https://www.nuget.org/packages), search using `tag:native`.</span></span> <span data-ttu-id="60dbd-152">此类包通常提供 `.targets` 和 `.props` 文件，NuGet 可在将包添加到项目中时自动导入这些文件。</span><span class="sxs-lookup"><span data-stu-id="60dbd-152">Such packages typically provide `.targets` and `.props` files, which NuGet imports automatically when the package is added to a project.</span></span>

## <a name="evaluating-packages"></a><span data-ttu-id="60dbd-153">评估包</span><span class="sxs-lookup"><span data-stu-id="60dbd-153">Evaluating packages</span></span>

<span data-ttu-id="60dbd-154">评估包用途的最佳方法是下载它并在你的代码中试用（顺便说一下，将对 nuget.org 的所有包进行常规病毒扫描）。</span><span class="sxs-lookup"><span data-stu-id="60dbd-154">The best way to evaluate the usefulness of a package is to download it and try it out in your code (all packages on nuget.org are routinely scanned for viruses, by the way).</span></span> <span data-ttu-id="60dbd-155">每一个被广泛使用的包起初都仅被少数开发人员采用，你也可能成为早期采用者之一！</span><span class="sxs-lookup"><span data-stu-id="60dbd-155">After all, every highly popular package got started with only a few developers using it, and you might be one of the early adopters!</span></span>

<span data-ttu-id="60dbd-156">同时，使用 NuGet 包则意味着与此包建立依赖关系，因此使用者希望确保包具有耐用性和可靠性。</span><span class="sxs-lookup"><span data-stu-id="60dbd-156">At the same time, using a NuGet package means taking a dependency on it, so you want to make sure it's robust and reliable.</span></span> <span data-ttu-id="60dbd-157">安装和直接测试包非常耗时，所以还可以通过使用包清单页面中的信息深入了解包的质量：</span><span class="sxs-lookup"><span data-stu-id="60dbd-157">Because installing and directly testing a package is time-consuming, you can also learn a lot about a package's quality by using the information on a package's listing page:</span></span>

- <span data-ttu-id="60dbd-158">*下载统计信息*：在 nuget.org 中，包页面上的“统计信息”部分显示总下载次数、最新版本下载次数以及日平均下载次数  。</span><span class="sxs-lookup"><span data-stu-id="60dbd-158">*Downloads statistics*: on the package page on nuget.org, the **Statistics** section shows total downloads, downloads of the most recent version, and average downloads per day.</span></span> <span data-ttu-id="60dbd-159">数值较大则表示已有许多开发人员选择与此包建立依赖关系，这说明此包已获得认可。</span><span class="sxs-lookup"><span data-stu-id="60dbd-159">Larger numbers indicate that many other developers have taken a dependency on the package, which means that it has proven itself.</span></span>

    ![包清单页面上的下载统计数据](media/Finding-03-Downloads.png)

- <span data-ttu-id="60dbd-161">*版本历史记录*：在包页面上，可在“信息”下查找最新更新的日期和查看“版本历史记录”   。</span><span class="sxs-lookup"><span data-stu-id="60dbd-161">*Version history*: on the package page, look under **Info** for the date of the most recent update and examine the **Version History**.</span></span> <span data-ttu-id="60dbd-162">维护良好的包应具有最新更新和丰富的版本历史记录。</span><span class="sxs-lookup"><span data-stu-id="60dbd-162">A well-maintained package has recent updates and a rich version history.</span></span> <span data-ttu-id="60dbd-163">疏于维护的包则仅具有几次更新，并且通常已长时间未更新。</span><span class="sxs-lookup"><span data-stu-id="60dbd-163">Neglected packages have few updates and often haven't been updated in some time.</span></span>

    ![包清单页面上的版本历史记录](media/Finding-04-VersionHistory.png)

- <span data-ttu-id="60dbd-165">*最近安装*：在包页面上，选择“统计信息”下的“查看完整统计信息”   。完整统计信息页面按版本号显示过去六周的包安装次数。</span><span class="sxs-lookup"><span data-stu-id="60dbd-165">*Recent installs*: on the package page under **Statistics**, select **View full stats**. The full stats page shows the package installs over the last six weeks by version number.</span></span> <span data-ttu-id="60dbd-166">其他开发人员频繁使用的包通常比鲜有使用的包更值得信赖。</span><span class="sxs-lookup"><span data-stu-id="60dbd-166">A package that other developers are actively using is typically a better choice than one that's not.</span></span>

- <span data-ttu-id="60dbd-167">支持  ：在包页面上，选择“信息”  下的“项目网站”  （如果可用）可查看作者提供的支持选项。</span><span class="sxs-lookup"><span data-stu-id="60dbd-167">*Support*: on the package page under **Info**, select **Project Site** (if available) to see what support options the author provides.</span></span> <span data-ttu-id="60dbd-168">具有专门网站的项目通常具备更好的支持。</span><span class="sxs-lookup"><span data-stu-id="60dbd-168">A project with a dedicated site is generally better supported.</span></span>

- <span data-ttu-id="60dbd-169">*开发人员历史记录*：在包页面上，选择“所有者”下的某个所有者可查看其已发布的其他包  。</span><span class="sxs-lookup"><span data-stu-id="60dbd-169">*Developer history*: on the package page under **Owners**, select an owner to see what other packages they've published.</span></span> <span data-ttu-id="60dbd-170">具有多个包的所有者更有可能在未来继续对其工作成果提供支持。</span><span class="sxs-lookup"><span data-stu-id="60dbd-170">Those with multiple packages are more likely to continue supporting their work in the future.</span></span>

- <span data-ttu-id="60dbd-171">*开源贡献*：很多包都在开源存储库中进行维护，这使依赖于包的开发人员可直接提供 bug 修补程序和功能改进。</span><span class="sxs-lookup"><span data-stu-id="60dbd-171">*Open source contributions*: many packages are maintained in open-source repositories, making it possible for developers depending on them to directly contribute bug fixes and feature improvements.</span></span> <span data-ttu-id="60dbd-172">任何给定包的贡献历史记录也能反映出积极参与的开发人员的数量。</span><span class="sxs-lookup"><span data-stu-id="60dbd-172">The contribution history of any given package is also a good indicator of how many developers are actively involved.</span></span>

- <span data-ttu-id="60dbd-173">*联系所有者*：新晋开发人员同样可以制作出可供使用的优质包，为他们提供向 NuGet 生态系统引入新内容的机会是非常好的做法。</span><span class="sxs-lookup"><span data-stu-id="60dbd-173">*Interview the owners*: new developers can certainly be equally committed to producing great packages for you to use, and it's good to give them a chance to bring something new to the NuGet ecosystem.</span></span> <span data-ttu-id="60dbd-174">若有此想法，使用清单页面中“信息”下的“联系所有者”选项即可直接联系包开发人员   。</span><span class="sxs-lookup"><span data-stu-id="60dbd-174">With this in mind, reach out directly to the package developers through the **Contact Owners** option under **Info** on the listing page.</span></span> <span data-ttu-id="60dbd-175">他们很可能非常乐于与你合作来满足你的需求！</span><span class="sxs-lookup"><span data-stu-id="60dbd-175">Chances are, they'll be happy to work with you to serve your needs!</span></span>

- <span data-ttu-id="60dbd-176">保留包 ID 前缀：许多包所有者已应用并授予了[保留包 ID 前缀](../nuget-org/id-prefix-reservation.md)  。</span><span class="sxs-lookup"><span data-stu-id="60dbd-176">*Reserved Package ID Prefixes*: many package owners have applied for and have been granted a [reserved package ID prefix](../nuget-org/id-prefix-reservation.md).</span></span> <span data-ttu-id="60dbd-177">如果 [nuget.org](https://www.nuget.org/) 上或 Visual Studio 中的包 ID 旁有视觉对象复选标记，这意味着包所有者已满足我们的 ID 前缀预留[条件](../nuget-org/id-prefix-reservation.md#id-prefix-reservation-criteria)。</span><span class="sxs-lookup"><span data-stu-id="60dbd-177">When you see the visual checkmark next to a package ID on [nuget.org](https://www.nuget.org/), or in Visual Studio, that means that the package owner has met our [criteria](../nuget-org/id-prefix-reservation.md#id-prefix-reservation-criteria) for ID prefix reservation.</span></span> <span data-ttu-id="60dbd-178">这意味着包所有者清楚了解如何标识自己及其包。</span><span class="sxs-lookup"><span data-stu-id="60dbd-178">This means the package owner is being clear on identifying themselves and their package.</span></span>

> [!Note]
> <span data-ttu-id="60dbd-179">应时刻留意包的许可条款 - 在 nuget.org 中的包清单页面上选择“许可信息”即可查看  。如果包未指定许可条款，请直接通过包页面上的“联系所有者”链接与包所有者联系  。</span><span class="sxs-lookup"><span data-stu-id="60dbd-179">Always be mindful of a package's license terms, which you can see by selecting **License Info** on a package's listing page on nuget.org. If a package does not specify license terms, contact the package owner directly using the **Contact owners** link on the package page.</span></span> <span data-ttu-id="60dbd-180">Microsoft 不向用户授予任何第三方包提供程序的知识产权许可，同时不对第三方提供的信息承担任何责任。</span><span class="sxs-lookup"><span data-stu-id="60dbd-180">Microsoft does not license any intellectual property to you from third party package providers and is not responsible for information provided by third parties.</span></span>

## <a name="license-url-deprecation"></a><span data-ttu-id="60dbd-181">许可证 URL 弃用</span><span class="sxs-lookup"><span data-stu-id="60dbd-181">License URL deprecation</span></span>
<span data-ttu-id="60dbd-182">在我们从 [licenseUrl](../reference/nuspec.md#licenseurl) 切换到 [license](../reference/nuspec.md#license) 时，一些 NuGet 客户端和 NuGet 源可能在某些情况下尚无法提供授权信息。</span><span class="sxs-lookup"><span data-stu-id="60dbd-182">As we transition from [licenseUrl](../reference/nuspec.md#licenseurl) to [license](../reference/nuspec.md#license), some NuGet clients and NuGet feeds may not yet have the ability to surface licensing information in some cases.</span></span> <span data-ttu-id="60dbd-183">为了维护向后兼容性，许可证 URL 会指向介绍如何在此类情况下检索许可证信息的文档。</span><span class="sxs-lookup"><span data-stu-id="60dbd-183">To maintain backward compatibility, the license URL points to this document which talks about how to retrieve the license information in such cases.</span></span>

<span data-ttu-id="60dbd-184">如果通过单击包的许可证 URL 转到此页面，表示包中有许可证文件；并且</span><span class="sxs-lookup"><span data-stu-id="60dbd-184">If clicking on the license URL for a package brought you to this page, it implies the package contains a license file and</span></span>
* <span data-ttu-id="60dbd-185">你已连接到尚不知道如何向客户端解释和显示新许可证信息的源；或者 </span><span class="sxs-lookup"><span data-stu-id="60dbd-185">You are connected to a feed that does not yet know how to interpret and surface the new license information to the client **OR**</span></span>
* <span data-ttu-id="60dbd-186">要使用的客户端尚不知道如何解释和读取源可能提供的新许可证信息；或者 </span><span class="sxs-lookup"><span data-stu-id="60dbd-186">You are using a client that does not yet know how to interpret and read the new license information that is potentially provided by the feed **OR**</span></span>
* <span data-ttu-id="60dbd-187">这两者的组合</span><span class="sxs-lookup"><span data-stu-id="60dbd-187">A combination of both</span></span>

<span data-ttu-id="60dbd-188">下面介绍了如何读取包内的许可证文件信息：</span><span class="sxs-lookup"><span data-stu-id="60dbd-188">Here is how you could read the information contained in the license file inside the package:</span></span>
1. <span data-ttu-id="60dbd-189">下载 NuGet 包，并将它的内容解压缩到文件夹中。</span><span class="sxs-lookup"><span data-stu-id="60dbd-189">Download the NuGet package, and unzip its contents to a folder.</span></span>
1. <span data-ttu-id="60dbd-190">打开位于此文件夹的根目录中的 `.nuspec` 文件。</span><span class="sxs-lookup"><span data-stu-id="60dbd-190">Open the `.nuspec` file which would be at the root of that folder.</span></span>
1. <span data-ttu-id="60dbd-191">它应有 `<license type="file">license\license.txt</license>` 等标记。</span><span class="sxs-lookup"><span data-stu-id="60dbd-191">It should have a tag like `<license type="file">license\license.txt</license>`.</span></span> <span data-ttu-id="60dbd-192">这意味着，许可证文件的命名为 `license.txt`，且它位于 `license` 文件夹的根目录中。</span><span class="sxs-lookup"><span data-stu-id="60dbd-192">This implies the license file is named `license.txt` and it is inside a folder called `license` which would also be at the root of that folder.</span></span>
1. <span data-ttu-id="60dbd-193">转到 `license` 文件夹，并打开 `license.txt` 文件。</span><span class="sxs-lookup"><span data-stu-id="60dbd-193">Navigate to the `license` folder and open the `license.txt` file.</span></span>


## <a name="search-syntax"></a><span data-ttu-id="60dbd-194">搜索语法</span><span class="sxs-lookup"><span data-stu-id="60dbd-194">Search Syntax</span></span>

<span data-ttu-id="60dbd-195">NuGet 包搜索在 nuget.org 上、NuGet CLI 中和 Visual Studio 的 NuGet 包管理器扩展中具有相同的使用方法。</span><span class="sxs-lookup"><span data-stu-id="60dbd-195">NuGet package search works the same on nuget.org, from the NuGet CLI, and within the NuGet Package Manager extension in Visual Studio.</span></span> <span data-ttu-id="60dbd-196">通常可使用关键字和包说明进行搜索。</span><span class="sxs-lookup"><span data-stu-id="60dbd-196">In general, search is applied to keywords as well as package descriptions.</span></span>

- <span data-ttu-id="60dbd-197">**关键字**：搜索操作将查找包含任何给定关键字的相关包。</span><span class="sxs-lookup"><span data-stu-id="60dbd-197">**Keywords**: Search looks for relevant packages that contain any of the provided keywords.</span></span> <span data-ttu-id="60dbd-198">示例：`modern UI`。</span><span class="sxs-lookup"><span data-stu-id="60dbd-198">Example: `modern UI`.</span></span> <span data-ttu-id="60dbd-199">若要搜索包含所有给定关键字的包，请在搜索词之间使用“+”，例如 `modern+UI`。</span><span class="sxs-lookup"><span data-stu-id="60dbd-199">To search for packages that contain all of the provided keywords, use "+" between the terms, such as `modern+UI`.</span></span>
- <span data-ttu-id="60dbd-200">**短语**：在引号内输入搜索词可查找与其大小写完全匹配的匹配项。</span><span class="sxs-lookup"><span data-stu-id="60dbd-200">**Phrases**: Entering terms within quotation marks looks for exact case-insensitive matches to those terms.</span></span> <span data-ttu-id="60dbd-201">示例：`"modern UI" package`</span><span class="sxs-lookup"><span data-stu-id="60dbd-201">Example: `"modern UI" package`</span></span>
- <span data-ttu-id="60dbd-202">**筛选**：可以按照语法 `<property>:<term>` 使用搜索词来搜索特定属性，其中，`<property>`（区分大小写）可为 `id`、`packageid`、`version`、`title`、`tags`、`author`、`description`、`summary` 和 `owner`。</span><span class="sxs-lookup"><span data-stu-id="60dbd-202">**Filtering**: You can apply a search term to a specific property by using the syntax `<property>:<term>` where `<property>` (case-insensitive) can be `id`, `packageid`, `version`, `title`, `tags`, `author`, `description`, `summary`, and `owner`.</span></span> <span data-ttu-id="60dbd-203">可将搜索词添加在引号中（如需要），还可以同时搜索多个属性。</span><span class="sxs-lookup"><span data-stu-id="60dbd-203">Terms can be contained in quotes if needed, and you can search for multiple properties at the same time.</span></span> <span data-ttu-id="60dbd-204">此外，按 `id` 属性搜索得到的是子字符串匹配项，而按 `packageid` 搜索将得到确切匹配。</span><span class="sxs-lookup"><span data-stu-id="60dbd-204">Also, searches on the `id` property are substring matches, whereas `packageid` uses an exact match.</span></span> <span data-ttu-id="60dbd-205">示例：</span><span class="sxs-lookup"><span data-stu-id="60dbd-205">Examples:</span></span>

    ```
    id:NuGet.Core                # Match any part of the id property
    Id:"Nuget.Core"
    ID:jQuery
    title:jquery                 # Searches title as shown on the package listing
    PackageId:jquery             # Match the package id exactly
    id:jquery id:ui              # Search for multiple terms in the id
    id:jquery tags:validation    # Search multiple properties
    id:"jquery.ui"               # Phrase search
    invalid:jquery ui            # Unsupported properties are ignored, so this
                                 # is the same as searching on jquery ui
    ```
