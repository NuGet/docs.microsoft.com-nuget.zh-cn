---
title: NuGet 2.1 发行说明
description: NuGet 2.1 的发行说明，包括已知问题、bug 修复、新增功能和 Dcr。
author: JonDouglas
ms.author: jodou
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: c44ad32c8c4018ccb517b41bffda674eef1f11f3
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/26/2021
ms.locfileid: "98777029"
---
# <a name="nuget-21-release-notes"></a><span data-ttu-id="b197a-103">NuGet 2.1 发行说明</span><span class="sxs-lookup"><span data-stu-id="b197a-103">NuGet 2.1 Release Notes</span></span>

<span data-ttu-id="b197a-104">[NuGet 2.0 发行说明](../release-notes/nuget-2.0.md)  | [NuGet 2.2 发行说明](../release-notes/nuget-2.2.md)</span><span class="sxs-lookup"><span data-stu-id="b197a-104">[NuGet 2.0 Release Notes](../release-notes/nuget-2.0.md) | [NuGet 2.2 Release Notes](../release-notes/nuget-2.2.md)</span></span>

<span data-ttu-id="b197a-105">NuGet 2.1 于2012年10月4日发布。</span><span class="sxs-lookup"><span data-stu-id="b197a-105">NuGet 2.1 was released on October 4, 2012.</span></span>

## <a name="hierarchical-nugetconfig"></a><span data-ttu-id="b197a-106">分层 Nuget.Config</span><span class="sxs-lookup"><span data-stu-id="b197a-106">Hierarchical Nuget.Config</span></span>

<span data-ttu-id="b197a-107">NuGet 2.1 通过以递归方式遍历用于查找文件的文件夹结构 `NuGet.Config` ，然后从所有找到的文件集生成配置，为你提供更大的灵活性。</span><span class="sxs-lookup"><span data-stu-id="b197a-107">NuGet 2.1 gives you greater flexibility in controlling NuGet settings by way of recursively walking up the folder structure looking for `NuGet.Config` files and then building the configuration from the set of all found files.</span></span>  <span data-ttu-id="b197a-108">作为示例，请考虑这样一种情况：团队具有内部包存储库，用于 CI 的其他内部依赖项的生成。</span><span class="sxs-lookup"><span data-stu-id="b197a-108">As an example, consider the scenario where a team has an internal package repository for CI builds of other internal dependencies.</span></span> <span data-ttu-id="b197a-109">单个项目的文件夹结构可能如下所示：</span><span class="sxs-lookup"><span data-stu-id="b197a-109">The folder structure for an individual project might look like the following:</span></span>

```
C:\
C:\myteam\
C:\myteam\solution1
C:\myteam\solution1\project1
```

<span data-ttu-id="b197a-110">此外，如果为解决方案启用了包还原，则还会存在以下文件夹：</span><span class="sxs-lookup"><span data-stu-id="b197a-110">Additionally, if package restore is enabled for the solution, the following folder will also exist:</span></span>

```
C:\myteam\solution1\.nuget
```

<span data-ttu-id="b197a-111">为了使团队的内部包存储库可用于团队处理的所有项目，而不是使其可用于计算机上的每个项目，我们可以创建一个新的 Nuget.Config 文件并将其放在 c:\myteam 文件夹中。</span><span class="sxs-lookup"><span data-stu-id="b197a-111">In order to have the team’s internal package repository available for all projects that the team works on, while not making it available for every project on the machine, we can create a new Nuget.Config file and place it in the c:\myteam folder.</span></span> <span data-ttu-id="b197a-112">无法为每个项目指定包文件夹。</span><span class="sxs-lookup"><span data-stu-id="b197a-112">There is no way to specificy a packages folder per project.</span></span>

```xml
<configuration>
    <packageSources>
    <add key="Official project team source" value="http://teamserver/api/v2/" />
    </packageSources>
    <disabledPackageSources />
    <activePackageSource>
    <add key="Official project team source" value="http://teamserver/api/v2/" />
    </activePackageSource>
</configuration>
```

<span data-ttu-id="b197a-113">现在，我们可以通过在 c:\myteam 下的任何文件夹中运行 "nuget.exe 源" 命令来添加源，如下所示：</span><span class="sxs-lookup"><span data-stu-id="b197a-113">We can now see that the source was added by running the ‘nuget.exe sources’ command from any folder beneath c:\myteam as shown below:</span></span>

![从父 nuget 配置包源](./media/releasenotes-21-cfg-hierarchy.png)

<span data-ttu-id="b197a-115">`NuGet.Config` 将按以下顺序搜索文件：</span><span class="sxs-lookup"><span data-stu-id="b197a-115">`NuGet.Config` files are searched for in the following order:</span></span>

1. `.nuget\Nuget.Config`
2. <span data-ttu-id="b197a-116">从项目文件夹到根的递归遍历</span><span class="sxs-lookup"><span data-stu-id="b197a-116">Recursive walk from project folder to root</span></span>
3. <span data-ttu-id="b197a-117">全局 `Nuget.Config` (`%appdata%\NuGet\Nuget.Config`) </span><span class="sxs-lookup"><span data-stu-id="b197a-117">Global `Nuget.Config` (`%appdata%\NuGet\Nuget.Config`)</span></span>

<span data-ttu-id="b197a-118">配置不是按 *顺序* 应用的，这意味着，根据上述排序，全局 Nuget.Config 首先应用，然后是从根到项目文件夹中发现的 Nuget.Config 文件，后跟 `.nuget\Nuget.Config` 。</span><span class="sxs-lookup"><span data-stu-id="b197a-118">The configurations are than applied in the *reverse order*, meaning that based on the above ordering, the global Nuget.Config would be applied first, followed by the discovered Nuget.Config files from root to project folder, followed by `.nuget\Nuget.Config`.</span></span>  <span data-ttu-id="b197a-119">如果你正在使用 `<clear/>` 元素从配置中删除一组项，则这一点特别重要。</span><span class="sxs-lookup"><span data-stu-id="b197a-119">This is particularly important if you’re using the `<clear/>` element to remove a set of items from config.</span></span>

## <a name="specify-packages-folder-location"></a><span data-ttu-id="b197a-120">指定 "包" 文件夹位置</span><span class="sxs-lookup"><span data-stu-id="b197a-120">Specify ‘packages’ Folder Location</span></span>

<span data-ttu-id="b197a-121">在过去，NuGet 从解决方案根文件夹下的已知 "包" 文件夹中管理了解决方案的包。</span><span class="sxs-lookup"><span data-stu-id="b197a-121">In the past, NuGet has managed a solution’s packages from a known ‘packages’ folder found beneath the solution root folder.</span></span>  <span data-ttu-id="b197a-122">对于具有多个安装了 NuGet 包的不同解决方案的开发团队，这可能会导致在文件系统上的多个不同位置安装相同的包。</span><span class="sxs-lookup"><span data-stu-id="b197a-122">For development teams that have many different solutions which have NuGet packages installed, this can result in the same package being installed in many different places on the file system.</span></span>

<span data-ttu-id="b197a-123">NuGet 2.1 通过文件中的元素，更精细地控制包文件夹的位置 `repositoryPath` `NuGet.Config` 。</span><span class="sxs-lookup"><span data-stu-id="b197a-123">NuGet 2.1 provides more granular control over the location of the packages folder via the `repositoryPath` element in the `NuGet.Config` file.</span></span>  <span data-ttu-id="b197a-124">根据上一个分层 Nuget.Config 支持示例，假设我们想让 C:\myteam\ 下的所有项目共享相同的包文件夹。</span><span class="sxs-lookup"><span data-stu-id="b197a-124">Building on the previous example of hierarchical Nuget.Config support, assume that we wish to have all projects under C:\myteam\ share the same packages folder.</span></span>  <span data-ttu-id="b197a-125">若要实现此目的，只需将以下项添加到 `c:\myteam\Nuget.Config` 。</span><span class="sxs-lookup"><span data-stu-id="b197a-125">To accomplish this, simply add the following entry to `c:\myteam\Nuget.Config`.</span></span>

```xml
<configuration>
    <config>
    <add key="repositoryPath" value="C:\myteam\teampackages" />
    </config>
    ...
</configuration>
```

<span data-ttu-id="b197a-126">在此示例中，共享 `Nuget.Config` 文件为在 C:\myteam 下创建的每个项目指定共享包文件夹，而不考虑深度。</span><span class="sxs-lookup"><span data-stu-id="b197a-126">In this example, the shared `Nuget.Config` file specifies a shared packages folder for every project that is created beneath C:\myteam, regardless of depth.</span></span> <span data-ttu-id="b197a-127">请注意，如果你在解决方案根目录下有 "现有包" 文件夹，则需要将其删除，NuGet 才能将包置于新位置。</span><span class="sxs-lookup"><span data-stu-id="b197a-127">Note that if you have an existing packages folder underneath your solution root, you need to delete it before NuGet will place packages in the new location.</span></span>

## <a name="support-for-portable-libraries"></a><span data-ttu-id="b197a-128">支持可移植库</span><span class="sxs-lookup"><span data-stu-id="b197a-128">Support for Portable Libraries</span></span>

<span data-ttu-id="b197a-129">[可移植库](/dotnet/standard/cross-platform/cross-platform-development-with-the-portable-class-library) 是 .net 4 中首次引入的一项功能，使你能够构建可在不同 Microsoft 平台上无需修改的程序集（从 the.NET Framework 版本到 Silverlight 再到 Windows Phone 甚至 Xbox 360)  (）</span><span class="sxs-lookup"><span data-stu-id="b197a-129">[Portable libraries](/dotnet/standard/cross-platform/cross-platform-development-with-the-portable-class-library) is a feature first introduced with .NET 4 that enables you to build assemblies that can work without modification on different Microsoft platforms, from versions of the.NET Framework to Silverlight to Windows Phone and even Xbox 360 (though at this time, NuGet does not support the Xbox portable library target).</span></span>  <span data-ttu-id="b197a-130">通过扩展框架版本和配置文件的 [包约定](../create-packages/supporting-multiple-target-frameworks.md) ，NuGet 2.1 现在支持可移植库，使你能够创建具有复合框架和配置文件目标 `lib` 文件夹的包。</span><span class="sxs-lookup"><span data-stu-id="b197a-130">By extending the [package conventions](../create-packages/supporting-multiple-target-frameworks.md) for framework versions and profiles, NuGet 2.1 now supports portable libraries by enabling you to create packages that have compound framework and profile target `lib` folders.</span></span>

<span data-ttu-id="b197a-131">例如，请考虑以下可移植类库的可用目标平台。</span><span class="sxs-lookup"><span data-stu-id="b197a-131">As an example, consider the following portable class library’s available target platforms.</span></span>

![可移植库创建对话框](./media/releasenotes-21-plib.png)

<span data-ttu-id="b197a-133">生成库并运行该命令后 `nuget.exe pack MyPortableProject.csproj` ，可以通过检查生成的 NuGet 包的内容来查看新的可移植库包文件夹结构。</span><span class="sxs-lookup"><span data-stu-id="b197a-133">After the library is built and the command `nuget.exe pack MyPortableProject.csproj` is run, the new portable library package folder structure can be seen by examining the contents of the generated NuGet package.</span></span>

![可移植库包布局](./media/releasenotes-21-plib-layout.png)

<span data-ttu-id="b197a-135">如您所见，可移植库文件夹名称约定遵循模式 "可移植-{framework 1} + {framework n}"，其中框架标识符遵循现有的 [框架名称和版本约定](../reference/target-frameworks.md)。</span><span class="sxs-lookup"><span data-stu-id="b197a-135">As you can see, the portable library folder name convention follows the pattern ‘portable-{framework 1}+{framework n}’ where the framework identifiers follow the existing [framework name and version conventions](../reference/target-frameworks.md).</span></span> <span data-ttu-id="b197a-136">用于 Windows Phone 的框架标识符中提供了名称和版本约定的一个例外。</span><span class="sxs-lookup"><span data-stu-id="b197a-136">One exception to the name and version conventions is found in the framework identifier used for Windows Phone.</span></span>  <span data-ttu-id="b197a-137">此名字对象应使用框架名称 "wp" (wp7、wp71 或 wp8) 。</span><span class="sxs-lookup"><span data-stu-id="b197a-137">This moniker should use the framework name ‘wp’ (wp7, wp71 or wp8).</span></span> <span data-ttu-id="b197a-138">例如，使用 "wp7" 将导致错误。</span><span class="sxs-lookup"><span data-stu-id="b197a-138">Using ‘silverlight-wp7’, for example, will result in an error.</span></span>

<span data-ttu-id="b197a-139">安装从此文件夹结构创建的包时，NuGet 现在可以将其框架和配置文件规则应用到多个目标，如文件夹名称中所指定。</span><span class="sxs-lookup"><span data-stu-id="b197a-139">When installing the package that is created from this folder structure, NuGet can now apply its framework and profile rules to multiple targets, as specified in the folder name.</span></span>  <span data-ttu-id="b197a-140">NuGet 的匹配规则的后面是 "更具体的" 目标优先于 "不太具体" 的原则。</span><span class="sxs-lookup"><span data-stu-id="b197a-140">Behind NuGet’s matching rules is the principle that “more specific” targets will take precedence over “less specific” ones.</span></span>  <span data-ttu-id="b197a-141">这意味着，如果某个特定平台的名字对象均与项目兼容，则该名字对象将始终优先于可移植的名字对象。</span><span class="sxs-lookup"><span data-stu-id="b197a-141">This means that monikers targeting a specific platform will always be preferred over portable ones if they are both compatible with a project.</span></span>  <span data-ttu-id="b197a-142">此外，如果多个可移植目标与项目兼容，NuGet 将更喜欢其中一组受支持的平台 "最接近于引用包的项目"。</span><span class="sxs-lookup"><span data-stu-id="b197a-142">Additionally, if multiple portable targets are compatible with a project, NuGet will prefer the one where the set of platforms supported is “closest” to the project referencing the package.</span></span>

## <a name="targeting-windows-8-and-windows-phone-8-projects"></a><span data-ttu-id="b197a-143">面向 Windows 8 和 Windows Phone 8 项目</span><span class="sxs-lookup"><span data-stu-id="b197a-143">Targeting Windows 8 and Windows Phone 8 Projects</span></span>

<span data-ttu-id="b197a-144">除了添加对面向可移植库项目的支持外，NuGet 2.1 还为 Windows 8 应用商店和 Windows Phone 8 项目提供了新的框架名字对象，还为 Windows 应用商店和 Windows Phone 项目提供了一些新的常规名字对象。</span><span class="sxs-lookup"><span data-stu-id="b197a-144">In addition to adding support for targeting portable library projects, NuGet 2.1 provides new framework monikers for both Windows 8 Store and Windows Phone 8 projects, as well as some new general monikers for Windows Store and Windows Phone projects that will be easier to manage across future versions of the respective platforms.</span></span>

<span data-ttu-id="b197a-145">对于 Windows 8 应用商店应用程序，标识符如下所示：</span><span class="sxs-lookup"><span data-stu-id="b197a-145">For Windows 8 Store applications, the identifiers look as follows:</span></span>

| <span data-ttu-id="b197a-146">NuGet 2.0 及更早版本</span><span class="sxs-lookup"><span data-stu-id="b197a-146">NuGet 2.0 and earlier</span></span> | <span data-ttu-id="b197a-147">NuGet 2.1</span><span class="sxs-lookup"><span data-stu-id="b197a-147">NuGet 2.1</span></span> |
| ---------------- | ----------- |
| <span data-ttu-id="b197a-148">winRT45、。NETCore45</span><span class="sxs-lookup"><span data-stu-id="b197a-148">winRT45, .NETCore45</span></span> | <span data-ttu-id="b197a-149">Windows、Windows8、win、win8</span><span class="sxs-lookup"><span data-stu-id="b197a-149">Windows, Windows8, win, win8</span></span> |

<br/>
<span data-ttu-id="b197a-150">对于 Windows Phone 项目，标识符如下所示：</span><span class="sxs-lookup"><span data-stu-id="b197a-150">For Windows Phone projects, the identifiers look as follows:</span></span>

| <span data-ttu-id="b197a-151">电话 OS</span><span class="sxs-lookup"><span data-stu-id="b197a-151">Phone OS</span></span> | <span data-ttu-id="b197a-152">NuGet 2.0 及更早版本</span><span class="sxs-lookup"><span data-stu-id="b197a-152">NuGet 2.0 and earlier</span></span> | <span data-ttu-id="b197a-153">NuGet 2.1</span><span class="sxs-lookup"><span data-stu-id="b197a-153">NuGet 2.1</span></span> |
| --- | --- | --- |
| <span data-ttu-id="b197a-154">Windows 7 Phone</span><span class="sxs-lookup"><span data-stu-id="b197a-154">Windows Phone 7</span></span> | <span data-ttu-id="b197a-155">silverlight3-wp</span><span class="sxs-lookup"><span data-stu-id="b197a-155">silverlight3-wp</span></span> | <span data-ttu-id="b197a-156">wp、wp7、WindowsPhone、WindowsPhone7</span><span class="sxs-lookup"><span data-stu-id="b197a-156">wp, wp7, WindowsPhone, WindowsPhone7</span></span> |
| <span data-ttu-id="b197a-157">Windows Phone 7.5 (Mango) </span><span class="sxs-lookup"><span data-stu-id="b197a-157">Windows Phone 7.5 (Mango)</span></span> | <span data-ttu-id="b197a-158">silverlight4-wp71</span><span class="sxs-lookup"><span data-stu-id="b197a-158">silverlight4-wp71</span></span> | <span data-ttu-id="b197a-159">wp71, WindowsPhone71</span><span class="sxs-lookup"><span data-stu-id="b197a-159">wp71, WindowsPhone71</span></span> |
| <span data-ttu-id="b197a-160">Windows Phone 8</span><span class="sxs-lookup"><span data-stu-id="b197a-160">Windows Phone 8</span></span> | <span data-ttu-id="b197a-161">（不支持）</span><span class="sxs-lookup"><span data-stu-id="b197a-161">(not supported)</span></span> | <span data-ttu-id="b197a-162">wp8、WindowsPhone8</span><span class="sxs-lookup"><span data-stu-id="b197a-162">wp8, WindowsPhone8</span></span> |

<br/>
<span data-ttu-id="b197a-163">在上述所有更改中，NuGet 2.1 将继续完全支持旧框架名称。</span><span class="sxs-lookup"><span data-stu-id="b197a-163">In all of the above changes, the old framework names will continue to be fully supported by NuGet 2.1.</span></span>  <span data-ttu-id="b197a-164">前进时，应使用新的名称，因为这些名称在各个平台的未来版本中将更为稳定。</span><span class="sxs-lookup"><span data-stu-id="b197a-164">Moving forward, the new names should be used as they will be more stable across future versions of the respective platforms.</span></span> <span data-ttu-id="b197a-165">但是，在2.1 之前的版本中将 *不* 支持新的名称，因此请相应地计划何时进行切换。</span><span class="sxs-lookup"><span data-stu-id="b197a-165">The new names will *not* be supported in versions of NuGet prior to 2.1, however, so plan accordingly for when to make the switch.</span></span>

## <a name="improved-search-in-package-manager-dialog"></a><span data-ttu-id="b197a-166">改进了包管理器对话框中的搜索</span><span class="sxs-lookup"><span data-stu-id="b197a-166">Improved Search in Package Manager Dialog</span></span>

<span data-ttu-id="b197a-167">在过去几个迭代中，已将更改引入到 NuGet 库，大大提高了包搜索速度和相关性。</span><span class="sxs-lookup"><span data-stu-id="b197a-167">Over the past several iterations, changes have been introduced to the NuGet gallery that greatly improved the speed and relevance of package searches.</span></span>  <span data-ttu-id="b197a-168">不过，这些改进仅限于 nuget.org 网站。</span><span class="sxs-lookup"><span data-stu-id="b197a-168">However, these improvements were limited to the nuget.org Web site.</span></span>  <span data-ttu-id="b197a-169">NuGet 2.1 通过 "NuGet 包管理器" 对话框提供改进的搜索体验。</span><span class="sxs-lookup"><span data-stu-id="b197a-169">NuGet 2.1 makes the improved search experience available through the NuGet package manager dialog.</span></span>  <span data-ttu-id="b197a-170">例如，假设你想要查找 Microsoft Azure 缓存预览版包。</span><span class="sxs-lookup"><span data-stu-id="b197a-170">As an example, imagine that you wanted to find the Windows Azure Caching Preview package.</span></span>  <span data-ttu-id="b197a-171">此包的合理搜索查询可以是 "Azure Cache"。</span><span class="sxs-lookup"><span data-stu-id="b197a-171">A reasonable search query for this package may be “Azure Cache”.</span></span>  <span data-ttu-id="b197a-172">在以前版本的 "包管理器" 对话框中，所需的包甚至不会在结果的第一页上列出。</span><span class="sxs-lookup"><span data-stu-id="b197a-172">In previous versions of the package manager dialog, the desired package would not even be listed on the first page of results.</span></span>  <span data-ttu-id="b197a-173">但在 NuGet 2.1 中，所需的包现在会显示在搜索结果的顶部。</span><span class="sxs-lookup"><span data-stu-id="b197a-173">However, in NuGet 2.1, the desired package now shows up at the top of the search results.</span></span>

![程序包管理器对话框搜索](./media/releasenotes-21-vsdlg-search.png)

## <a name="force-package-update"></a><span data-ttu-id="b197a-175">强制包更新</span><span class="sxs-lookup"><span data-stu-id="b197a-175">Force Package Update</span></span>

<span data-ttu-id="b197a-176">在 NuGet 2.1 之前，NuGet 将跳过更新包（如果版本编号不高）。</span><span class="sxs-lookup"><span data-stu-id="b197a-176">Prior to NuGet 2.1, NuGet would skip updating a package when there was a not a high version number.</span></span>  <span data-ttu-id="b197a-177">这在某些情况下引入了摩擦，特别是对于生成或 CI 方案，团队不希望在每次生成时递增包版本号。</span><span class="sxs-lookup"><span data-stu-id="b197a-177">This introduced friction for certain scenarios – particularly in the case of build or CI scenarios where the team did not want to increment the package version number with each build.</span></span>  <span data-ttu-id="b197a-178">所需行为是强制更新，而不考虑。</span><span class="sxs-lookup"><span data-stu-id="b197a-178">The desired behavior was to force an update regardless.</span></span>  <span data-ttu-id="b197a-179">NuGet 2.1 通过 "重新安装" 标志来解决此情况。</span><span class="sxs-lookup"><span data-stu-id="b197a-179">NuGet 2.1 addresses this with the ‘reinstall’ flag.</span></span>  <span data-ttu-id="b197a-180">例如，在尝试更新不具有更新包版本的包时，早期版本的 NuGet 会导致以下情况：</span><span class="sxs-lookup"><span data-stu-id="b197a-180">For example, previous versions of NuGet would result in the following when attempting to update a package that did not have a more recent package version:</span></span>

```
PM> Update-Package Moq
No updates available for 'Moq' in project 'MySolution.MyConsole'.
```

<span data-ttu-id="b197a-181">使用 "重新安装" 标志，无论是否有较新的版本，都将更新程序包。</span><span class="sxs-lookup"><span data-stu-id="b197a-181">With the reinstall flag, the package will be updated regardless of whether there is a newer version.</span></span>

```
PM> Update-Package Moq -Reinstall
Successfully removed 'Moq 4.0.10827' from MySolution.MyConsole.
Successfully uninstalled 'Moq 4.0.10827'.
Successfully installed 'Moq 4.0.10827'.
Successfully added 'Moq 4.0.10827' to MySolution.MyConsole.
```

<span data-ttu-id="b197a-182">重新安装标志证明好处的另一种情况是框架重新设定目标。</span><span class="sxs-lookup"><span data-stu-id="b197a-182">Another scenario where the reinstall flag proves beneficial is that of framework re-targeting.</span></span> <span data-ttu-id="b197a-183">在更改项目的目标框架时 (例如，从 .NET 4 到 .NET 4.5) ，Update-Package 重新安装可以将对项目中安装的所有 NuGet 包的引用更新为正确的程序集。</span><span class="sxs-lookup"><span data-stu-id="b197a-183">When changing the target framework of a project (for example, from .NET 4 to .NET 4.5), Update-Package -Reinstall can update references to the correct assemblies for all NuGet packages installed in the project.</span></span>

## <a name="edit-package-sources-within-visual-studio"></a><span data-ttu-id="b197a-184">在 Visual Studio 中编辑包源</span><span class="sxs-lookup"><span data-stu-id="b197a-184">Edit Package Sources Within Visual Studio</span></span>

<span data-ttu-id="b197a-185">在以前版本的 NuGet 中，从 Visual Studio 的 "选项" 对话框中更新包源需要删除并重新添加包源。</span><span class="sxs-lookup"><span data-stu-id="b197a-185">In previous versions of NuGet, updating a package source from within the Visual Studio options dialog required deleting and re-adding the package source.</span></span>  <span data-ttu-id="b197a-186">NuGet 2.1 通过支持更新作为配置用户界面的第一类函数来改进此工作流。</span><span class="sxs-lookup"><span data-stu-id="b197a-186">NuGet 2.1 improves this workflow by supporting update as a first class function of the configuration user interface.</span></span>

![程序包管理器配置对话框](./media/releasenotes-21-edit-pkg-source.png)

## <a name="bug-fixes"></a><span data-ttu-id="b197a-188">Bug 修复</span><span class="sxs-lookup"><span data-stu-id="b197a-188">Bug Fixes</span></span>

<span data-ttu-id="b197a-189">NuGet 2.1 包含多个 bug 修复。</span><span class="sxs-lookup"><span data-stu-id="b197a-189">NuGet 2.1 includes many bug fixes.</span></span> <span data-ttu-id="b197a-190">有关 NuGet 2.0 中已修复的工作项的完整列表，请查看 [此版本的 NuGet 问题跟踪程序](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Fixed&type=All&priority=All&release=NuGet%202.1&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0)。</span><span class="sxs-lookup"><span data-stu-id="b197a-190">For a full list of work items fixed in NuGet 2.0, please view the [NuGet Issue Tracker for this release](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Fixed&type=All&priority=All&release=NuGet%202.1&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0).</span></span>
