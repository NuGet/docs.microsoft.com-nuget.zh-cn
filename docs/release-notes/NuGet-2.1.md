---
title: NuGet 2.1 发行说明
description: 包括已知的问题、 bug 修复、 新增的功能和 Dcr NuGet 2.1 发行说明。
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: fd6dadc7968991c77c1b06a6a261415355b2fd73
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/04/2018
ms.locfileid: "43548592"
---
# <a name="nuget-21-release-notes"></a><span data-ttu-id="53378-103">NuGet 2.1 发行说明</span><span class="sxs-lookup"><span data-stu-id="53378-103">NuGet 2.1 Release Notes</span></span>

<span data-ttu-id="53378-104">[NuGet 2.0 发行说明](../release-notes/nuget-2.0.md) | [NuGet 2.2 发行说明](../release-notes/nuget-2.2.md)</span><span class="sxs-lookup"><span data-stu-id="53378-104">[NuGet 2.0 Release Notes](../release-notes/nuget-2.0.md) | [NuGet 2.2 Release Notes](../release-notes/nuget-2.2.md)</span></span>

<span data-ttu-id="53378-105">NuGet 2.1 已于 2012 年 10 月 4 日发布。</span><span class="sxs-lookup"><span data-stu-id="53378-105">NuGet 2.1 was released on October 4, 2012.</span></span>

## <a name="hierarchical-nugetconfig"></a><span data-ttu-id="53378-106">分层 Nuget.Config</span><span class="sxs-lookup"><span data-stu-id="53378-106">Hierarchical Nuget.Config</span></span>

<span data-ttu-id="53378-107">NuGet 2.1 为您提供了更灵活地控制通过以递归方式查找的文件夹结构向上遍历的 NuGet 设置`NuGet.Config`文件，然后生成中找到的所有文件组的配置。</span><span class="sxs-lookup"><span data-stu-id="53378-107">NuGet 2.1 gives you greater flexibility in controlling NuGet settings by way of recursively walking up the folder structure looking for `NuGet.Config` files and then building the configuration from the set of all found files.</span></span>  <span data-ttu-id="53378-108">作为示例，请考虑其中一个团队具有的其他内部的依赖项的 CI 生成的内部包存储库的方案。</span><span class="sxs-lookup"><span data-stu-id="53378-108">As an example, consider the scenario where a team has an internal package repository for CI builds of other internal dependencies.</span></span> <span data-ttu-id="53378-109">单个项目的文件夹结构可能类似以下形式：</span><span class="sxs-lookup"><span data-stu-id="53378-109">The folder structure for an individual project might look like the following:</span></span>

    C:\
    C:\myteam\
    C:\myteam\solution1
    C:\myteam\solution1\project1

<span data-ttu-id="53378-110">此外，如果解决方案启用了包还原，也将存在以下文件夹：</span><span class="sxs-lookup"><span data-stu-id="53378-110">Additionally, if package restore is enabled for the solution, the following folder will also exist:</span></span>

    C:\myteam\solution1\.nuget

<span data-ttu-id="53378-111">为了使团队的内部包存储库可用的所有项目的团队处理，同时不使它可为每个项目的计算机上，我们可以创建一个新的 Nuget.Config 文件，并将其放在 c:\myteam 文件夹中。</span><span class="sxs-lookup"><span data-stu-id="53378-111">In order to have the team’s internal package repository available for all projects that the team works on, while not making it available for every project on the machine, we can create a new Nuget.Config file and place it in the c:\myteam folder.</span></span> <span data-ttu-id="53378-112">无法为指定每个项目的 packages 文件夹。</span><span class="sxs-lookup"><span data-stu-id="53378-112">There is no way to specificy a packages folder per project.</span></span>

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

<span data-ttu-id="53378-113">现在，我们可以看到源被添加，如下所示的 c:\myteam 下任何文件夹中运行 nuget.exe 源命令：</span><span class="sxs-lookup"><span data-stu-id="53378-113">We can now see that the source was added by running the ‘nuget.exe sources’ command from any folder beneath c:\myteam as shown below:</span></span>

![从父 nuget 配置包源](./media/releasenotes-21-cfg-hierarchy.png)

<span data-ttu-id="53378-115">`NuGet.Config` 按以下顺序搜索了文件：</span><span class="sxs-lookup"><span data-stu-id="53378-115">`NuGet.Config` files are searched for in the following order:</span></span>

1. `.nuget\Nuget.Config`
2. <span data-ttu-id="53378-116">递归遍历到根项目文件夹中</span><span class="sxs-lookup"><span data-stu-id="53378-116">Recursive walk from project folder to root</span></span>
3. <span data-ttu-id="53378-117">全局`Nuget.Config`(`%appdata%\NuGet\Nuget.Config`)</span><span class="sxs-lookup"><span data-stu-id="53378-117">Global `Nuget.Config` (`%appdata%\NuGet\Nuget.Config`)</span></span>

<span data-ttu-id="53378-118">配置是不是应用于*反转顺序*，也就是说，取决于上述顺序，全局 Nuget.Config 将是首先应用后, 跟已发现的 Nuget.Config 文件从根项目文件夹，然后是通过`.nuget\Nuget.Config`。</span><span class="sxs-lookup"><span data-stu-id="53378-118">The configurations are than applied in the *reverse order*, meaning that based on the above ordering, the global Nuget.Config would be applied first, followed by the discovered Nuget.Config files from root to project folder, followed by `.nuget\Nuget.Config`.</span></span>  <span data-ttu-id="53378-119">这一点特别重要，如果您使用的`<clear/>`要从配置中删除一组项的元素。</span><span class="sxs-lookup"><span data-stu-id="53378-119">This is particularly important if you’re using the `<clear/>` element to remove a set of items from config.</span></span>

## <a name="specify-packages-folder-location"></a><span data-ttu-id="53378-120">指定包文件夹位置</span><span class="sxs-lookup"><span data-stu-id="53378-120">Specify ‘packages’ Folder Location</span></span>

<span data-ttu-id="53378-121">在过去，NuGet 具有托管解决方案的根文件夹下找到已知的包文件夹中的解决方案包。</span><span class="sxs-lookup"><span data-stu-id="53378-121">In the past, NuGet has managed a solution’s packages from a known ‘packages’ folder found beneath the solution root folder.</span></span>  <span data-ttu-id="53378-122">对于具有许多不同的解决方案的已安装的 NuGet 包的开发团队，这可能导致在文件系统上的多个不同位置中安装在同一包中。</span><span class="sxs-lookup"><span data-stu-id="53378-122">For development teams that have many different solutions which have NuGet packages installed, this can result in the same package being installed in many different places on the file system.</span></span>

<span data-ttu-id="53378-123">NuGet 2.1 提供了更精细地控制通过包文件夹的位置`repositoryPath`中的元素`NuGet.Config`文件。</span><span class="sxs-lookup"><span data-stu-id="53378-123">NuGet 2.1 provides more granular control over the location of the packages folder via the `repositoryPath` element in the `NuGet.Config` file.</span></span>  <span data-ttu-id="53378-124">生成的 Nuget.Config 的层次结构支持以上一个示例，假设我们想要拥有 C:\myteam\ 共享相同的包文件夹下的所有项目。</span><span class="sxs-lookup"><span data-stu-id="53378-124">Building on the previous example of hierarchical Nuget.Config support, assume that we wish to have all projects under C:\myteam\ share the same packages folder.</span></span>  <span data-ttu-id="53378-125">若要完成此操作，只需添加到以下一项`c:\myteam\Nuget.Config`。</span><span class="sxs-lookup"><span data-stu-id="53378-125">To accomplish this, simply add the following entry to `c:\myteam\Nuget.Config`.</span></span>

```xml
<configuration>
    <config>
    <add key="repositoryPath" value="C:\myteam\teampackages" />
    </config>
    ...
</configuration>
```

<span data-ttu-id="53378-126">在此示例中，共享`Nuget.Config`文件指定用于创建下方 C:\myteam，而不考虑深度的每个项目的共享的包文件夹。</span><span class="sxs-lookup"><span data-stu-id="53378-126">In this example, the shared `Nuget.Config` file specifies a shared packages folder for every project that is created beneath C:\myteam, regardless of depth.</span></span> <span data-ttu-id="53378-127">请注意，是否解决方案根目录下有一个现有的包文件夹，您需要 NuGet 会将包放置在新位置之前将其删除。</span><span class="sxs-lookup"><span data-stu-id="53378-127">Note that if you have an existing packages folder underneath your solution root, you need to delete it before NuGet will place packages in the new location.</span></span>

## <a name="support-for-portable-libraries"></a><span data-ttu-id="53378-128">对可移植库的支持</span><span class="sxs-lookup"><span data-stu-id="53378-128">Support for Portable Libraries</span></span>

<span data-ttu-id="53378-129">[可移植库](/dotnet/standard/cross-platform/cross-platform-development-with-the-portable-class-library)是首次随.NET 4 中，可用于生成可以无需修改即可在不同的 Microsoft 平台，从.net Framework 对 Windows Phone 和甚至 Xbox silverlight 版本上的程序集的功能360 （尽管在此期间，NuGet 不支持 Xbox 可移植库目标）。</span><span class="sxs-lookup"><span data-stu-id="53378-129">[Portable libraries](/dotnet/standard/cross-platform/cross-platform-development-with-the-portable-class-library) is a feature first introduced with .NET 4 that enables you to build assemblies that can work without modification on different Microsoft platforms, from versions of the.NET Framework to Silverlight to Windows Phone and even Xbox 360 (though at this time, NuGet does not support the Xbox portable library target).</span></span>  <span data-ttu-id="53378-130">通过扩展[打包约定](../create-packages/supporting-multiple-target-frameworks.md)framework 版本和配置文件，NuGet 2.1 现在支持可移植库，使您创建具有复合框架和配置文件目标的包`lib`文件夹。</span><span class="sxs-lookup"><span data-stu-id="53378-130">By extending the [package conventions](../create-packages/supporting-multiple-target-frameworks.md) for framework versions and profiles, NuGet 2.1 now supports portable libraries by enabling you to create packages that have compound framework and profile target `lib` folders.</span></span>

<span data-ttu-id="53378-131">作为示例，请考虑以下可移植库的可用目标平台。</span><span class="sxs-lookup"><span data-stu-id="53378-131">As an example, consider the following portable class library’s available target platforms.</span></span>

![可移植库创建对话框](./media/releasenotes-21-plib.png)

<span data-ttu-id="53378-133">构建库后，该命令`nuget.exe pack MyPortableProject.csproj`运行时，新的可移植库包文件夹结构可以通过检查生成的 NuGet 包的内容发现。</span><span class="sxs-lookup"><span data-stu-id="53378-133">After the library is built and the command `nuget.exe pack MyPortableProject.csproj` is run, the new portable library package folder structure can be seen by examining the contents of the generated NuGet package.</span></span>

![可移植库包布局](./media/releasenotes-21-plib-layout.png)

<span data-ttu-id="53378-135">正如您所看到的可移植库文件夹名称约定遵循的模式可移植的 {framework 1} + {framework n} 的框架标识符遵循现有[framework 名称和版本约定](../reference/target-frameworks.md)。</span><span class="sxs-lookup"><span data-stu-id="53378-135">As you can see, the portable library folder name convention follows the pattern ‘portable-{framework 1}+{framework n}’ where the framework identifiers follow the existing [framework name and version conventions](../reference/target-frameworks.md).</span></span> <span data-ttu-id="53378-136">用于 Windows Phone 的框架标识符中找到了一个异常的名称和版本的约定。</span><span class="sxs-lookup"><span data-stu-id="53378-136">One exception to the name and version conventions is found in the framework identifier used for Windows Phone.</span></span>  <span data-ttu-id="53378-137">此名字对象应使用的框架名称 wp （wp7、 wp71 或 wp8）。</span><span class="sxs-lookup"><span data-stu-id="53378-137">This moniker should use the framework name ‘wp’ (wp7, wp71 or wp8).</span></span> <span data-ttu-id="53378-138">使用 silverlight-wp7，例如，将导致错误。</span><span class="sxs-lookup"><span data-stu-id="53378-138">Using ‘silverlight-wp7’, for example, will result in an error.</span></span>

<span data-ttu-id="53378-139">在安装时创建此文件夹结构中的包，NuGet 现在可以将其框架和配置文件规则应用于多个目标，文件夹名称中指定。</span><span class="sxs-lookup"><span data-stu-id="53378-139">When installing the package that is created from this folder structure, NuGet can now apply its framework and profile rules to multiple targets, as specified in the folder name.</span></span>  <span data-ttu-id="53378-140">NuGet 的匹配规则是，"更多特定"目标将优先于"不太特定"的原则。</span><span class="sxs-lookup"><span data-stu-id="53378-140">Behind NuGet’s matching rules is the principle that “more specific” targets will take precedence over “less specific” ones.</span></span>  <span data-ttu-id="53378-141">这意味着，面向特定平台的名字对象将始终是首选通过可移植的如果它们都与一个项目兼容。</span><span class="sxs-lookup"><span data-stu-id="53378-141">This means that monikers targeting a specific platform will always be preferred over portable ones if they are both compatible with a project.</span></span>  <span data-ttu-id="53378-142">此外，如果多个可移植目标兼容使用项目，NuGet 将首选支持的平台设置为"最靠近"项目引用包。</span><span class="sxs-lookup"><span data-stu-id="53378-142">Additionally, if multiple portable targets are compatible with a project, NuGet will prefer the one where the set of platforms supported is “closest” to the project referencing the package.</span></span>

## <a name="targeting-windows-8-and-windows-phone-8-projects"></a><span data-ttu-id="53378-143">面向 Windows 8 和 Windows Phone 8 项目</span><span class="sxs-lookup"><span data-stu-id="53378-143">Targeting Windows 8 and Windows Phone 8 Projects</span></span>

<span data-ttu-id="53378-144">除了添加支持面向可移植库项目，NuGet 2.1 所提供的 Windows 8 应用商店和 Windows Phone 8 项目，以及为 Windows 应用商店和 Windows Phone 项目将一些新常规名字对象的新框架名字对象更轻松地跨各自的平台的未来版本管理。</span><span class="sxs-lookup"><span data-stu-id="53378-144">In addition to adding support for targeting portable library projects, NuGet 2.1 provides new framework monikers for both Windows 8 Store and Windows Phone 8 projects, as well as some new general monikers for Windows Store and Windows Phone projects that will be easier to manage across future versions of the respective platforms.</span></span>

<span data-ttu-id="53378-145">对于 Windows 8 应用商店应用程序中，标识符如下所示：</span><span class="sxs-lookup"><span data-stu-id="53378-145">For Windows 8 Store applications, the identifiers look as follows:</span></span>

| <span data-ttu-id="53378-146">NuGet 2.0 及更早版本</span><span class="sxs-lookup"><span data-stu-id="53378-146">NuGet 2.0 and earlier</span></span> | <span data-ttu-id="53378-147">NuGet 2.1</span><span class="sxs-lookup"><span data-stu-id="53378-147">NuGet 2.1</span></span> |
| ---------------- | ----------- |
| <span data-ttu-id="53378-148">winRT45, .NETCore45</span><span class="sxs-lookup"><span data-stu-id="53378-148">winRT45, .NETCore45</span></span> | <span data-ttu-id="53378-149">Windows，Windows8，win win8</span><span class="sxs-lookup"><span data-stu-id="53378-149">Windows, Windows8, win, win8</span></span> |

<br/>
<span data-ttu-id="53378-150">对于 Windows Phone 项目，标识符如下所示：</span><span class="sxs-lookup"><span data-stu-id="53378-150">For Windows Phone projects, the identifiers look as follows:</span></span>

| <span data-ttu-id="53378-151">Phone 操作系统</span><span class="sxs-lookup"><span data-stu-id="53378-151">Phone OS</span></span> | <span data-ttu-id="53378-152">NuGet 2.0 及更早版本</span><span class="sxs-lookup"><span data-stu-id="53378-152">NuGet 2.0 and earlier</span></span> | <span data-ttu-id="53378-153">NuGet 2.1</span><span class="sxs-lookup"><span data-stu-id="53378-153">NuGet 2.1</span></span> |
| --- | --- | --- |
| <span data-ttu-id="53378-154">Windows Phone 7</span><span class="sxs-lookup"><span data-stu-id="53378-154">Windows Phone 7</span></span> | <span data-ttu-id="53378-155">silverlight3 wp</span><span class="sxs-lookup"><span data-stu-id="53378-155">silverlight3-wp</span></span> | <span data-ttu-id="53378-156">wp wp7，WindowsPhone WindowsPhone7</span><span class="sxs-lookup"><span data-stu-id="53378-156">wp, wp7, WindowsPhone, WindowsPhone7</span></span> |
| <span data-ttu-id="53378-157">Windows Phone 7.5 (Mango)</span><span class="sxs-lookup"><span data-stu-id="53378-157">Windows Phone 7.5 (Mango)</span></span> | <span data-ttu-id="53378-158">silverlight4 wp71</span><span class="sxs-lookup"><span data-stu-id="53378-158">silverlight4-wp71</span></span> | <span data-ttu-id="53378-159">wp71 WindowsPhone71</span><span class="sxs-lookup"><span data-stu-id="53378-159">wp71, WindowsPhone71</span></span> |
| <span data-ttu-id="53378-160">Windows Phone 8</span><span class="sxs-lookup"><span data-stu-id="53378-160">Windows Phone 8</span></span> | <span data-ttu-id="53378-161">（不支持）</span><span class="sxs-lookup"><span data-stu-id="53378-161">(not supported)</span></span> | <span data-ttu-id="53378-162">wp8 WindowsPhone8</span><span class="sxs-lookup"><span data-stu-id="53378-162">wp8, WindowsPhone8</span></span> |

<br/>
<span data-ttu-id="53378-163">在所有上述更改，将继续得到的 NuGet 2.1 完全支持旧的框架名称。</span><span class="sxs-lookup"><span data-stu-id="53378-163">In all of the above changes, the old framework names will continue to be fully supported by NuGet 2.1.</span></span>  <span data-ttu-id="53378-164">展望未来，新的名称应将更稳定，将来版本的各自的平台。</span><span class="sxs-lookup"><span data-stu-id="53378-164">Moving forward, the new names should be used as they will be more stable across future versions of the respective platforms.</span></span> <span data-ttu-id="53378-165">新名称将*不*是支持在 2.1 之前的 NuGet 版本，但是，因此相应地规划时切换。</span><span class="sxs-lookup"><span data-stu-id="53378-165">The new names will *not* be supported in versions of NuGet prior to 2.1, however, so plan accordingly for when to make the switch.</span></span>

## <a name="improved-search-in-package-manager-dialog"></a><span data-ttu-id="53378-166">在包管理器对话框改进的搜索</span><span class="sxs-lookup"><span data-stu-id="53378-166">Improved Search in Package Manager Dialog</span></span>

<span data-ttu-id="53378-167">在过去的几个迭代，引入了更改到 NuGet 库，大大提高速度和包搜索相关性。</span><span class="sxs-lookup"><span data-stu-id="53378-167">Over the past several iterations, changes have been introduced to the NuGet gallery that greatly improved the speed and relevance of package searches.</span></span>  <span data-ttu-id="53378-168">但是，这些改进的限制为 nuget.org Web 站点。</span><span class="sxs-lookup"><span data-stu-id="53378-168">However, these improvements were limited to the nuget.org Web site.</span></span>  <span data-ttu-id="53378-169">NuGet 2.1 可通过 NuGet 包管理器对话框提供改进的搜索体验。</span><span class="sxs-lookup"><span data-stu-id="53378-169">NuGet 2.1 makes the improved search experience available through the NuGet package manager dialog.</span></span>  <span data-ttu-id="53378-170">例如，假设您想要找到 Windows Azure Caching 预览包。</span><span class="sxs-lookup"><span data-stu-id="53378-170">As an example, imagine that you wanted to find the Windows Azure Caching Preview package.</span></span>  <span data-ttu-id="53378-171">此包的合理的搜索查询可能是"Azure 缓存"。</span><span class="sxs-lookup"><span data-stu-id="53378-171">A reasonable search query for this package may be “Azure Cache”.</span></span>  <span data-ttu-id="53378-172">在以前版本的包管理器对话框中，所需的包将不甚至会列出结果的第一页。</span><span class="sxs-lookup"><span data-stu-id="53378-172">In previous versions of the package manager dialog, the desired package would not even be listed on the first page of results.</span></span>  <span data-ttu-id="53378-173">但是，在 NuGet 2.1 所需的包现在显示在搜索结果顶部。</span><span class="sxs-lookup"><span data-stu-id="53378-173">However, in NuGet 2.1, the desired package now shows up at the top of the search results.</span></span>

![包管理器对话框中搜索](./media/releasenotes-21-vsdlg-search.png)

## <a name="force-package-update"></a><span data-ttu-id="53378-175">强制执行包更新</span><span class="sxs-lookup"><span data-stu-id="53378-175">Force Package Update</span></span>

<span data-ttu-id="53378-176">在 NuGet 2.1 之前 NuGet 将跳过更新包时出现不高的版本号。</span><span class="sxs-lookup"><span data-stu-id="53378-176">Prior to NuGet 2.1, NuGet would skip updating a package when there was a not a high version number.</span></span>  <span data-ttu-id="53378-177">这就产生了某些情况下-尤其是对于生成或 CI 方案，团队没有不需要每次生成数字将包版本递增的冲突。</span><span class="sxs-lookup"><span data-stu-id="53378-177">This introduced friction for certain scenarios – particularly in the case of build or CI scenarios where the team did not want to increment the package version number with each build.</span></span>  <span data-ttu-id="53378-178">所需的行为是强制进行更新，而不考虑。</span><span class="sxs-lookup"><span data-stu-id="53378-178">The desired behavior was to force an update regardless.</span></span>  <span data-ttu-id="53378-179">NuGet 2.1 可解决这的重新安装标志。</span><span class="sxs-lookup"><span data-stu-id="53378-179">NuGet 2.1 addresses this with the ‘reinstall’ flag.</span></span>  <span data-ttu-id="53378-180">例如，尝试更新不具有最新包版本的包时 NuGet 的早期版本将导致以下：</span><span class="sxs-lookup"><span data-stu-id="53378-180">For example, previous versions of NuGet would result in the following when attempting to update a package that did not have a more recent package version:</span></span>

    PM> Update-Package Moq
    No updates available for 'Moq' in project 'MySolution.MyConsole'.

<span data-ttu-id="53378-181">通过重新安装标志，包将更新无论是否还有一个较新版本。</span><span class="sxs-lookup"><span data-stu-id="53378-181">With the reinstall flag, the package will be updated regardless of whether there is a newer version.</span></span>

    PM> Update-Package Moq -Reinstall
    Successfully removed 'Moq 4.0.10827' from MySolution.MyConsole.
    Successfully uninstalled 'Moq 4.0.10827'.
    Successfully installed 'Moq 4.0.10827'.
    Successfully added 'Moq 4.0.10827' to MySolution.MyConsole.

<span data-ttu-id="53378-182">重新安装标志证明有益的另一种方案是 framework 重定目标。</span><span class="sxs-lookup"><span data-stu-id="53378-182">Another scenario where the reinstall flag proves beneficial is that of framework re-targeting.</span></span> <span data-ttu-id="53378-183">更改 （例如，从.NET 4 中为.NET 4.5)，一个项目的目标框架时更新包的重新安装可以更新到正确的程序集的所有项目中安装的 NuGet 包的引用。</span><span class="sxs-lookup"><span data-stu-id="53378-183">When changing the target framework of a project (for example, from .NET 4 to .NET 4.5), Update-Package -Reinstall can update references to the correct assemblies for all NuGet packages installed in the project.</span></span>

## <a name="edit-package-sources-within-visual-studio"></a><span data-ttu-id="53378-184">编辑 Visual Studio 中的包源</span><span class="sxs-lookup"><span data-stu-id="53378-184">Edit Package Sources Within Visual Studio</span></span>

<span data-ttu-id="53378-185">在以前版本的 NuGet，正在更新从 Visual Studio 选项对话框所需删除并重新添加包源中的包源。</span><span class="sxs-lookup"><span data-stu-id="53378-185">In previous versions of NuGet, updating a package source from within the Visual Studio options dialog required deleting and re-adding the package source.</span></span>  <span data-ttu-id="53378-186">NuGet 2.1 通过支持更新作为配置用户界面的第一类函数来改进此工作流。</span><span class="sxs-lookup"><span data-stu-id="53378-186">NuGet 2.1 improves this workflow by supporting update as a first class function of the configuration user interface.</span></span>

![包管理器配置对话框](./media/releasenotes-21-edit-pkg-source.png)

## <a name="bug-fixes"></a><span data-ttu-id="53378-188">Bug 修复</span><span class="sxs-lookup"><span data-stu-id="53378-188">Bug Fixes</span></span>

<span data-ttu-id="53378-189">NuGet 2.1 包括许多 bug 修复。</span><span class="sxs-lookup"><span data-stu-id="53378-189">NuGet 2.1 includes many bug fixes.</span></span> <span data-ttu-id="53378-190">有关工作的完整列表项中已修复 NuGet 2.0，请查看[对于此版本的 NuGet 问题跟踪程序](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Fixed&type=All&priority=All&release=NuGet%202.1&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0)。</span><span class="sxs-lookup"><span data-stu-id="53378-190">For a full list of work items fixed in NuGet 2.0, please view the [NuGet Issue Tracker for this release](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Fixed&type=All&priority=All&release=NuGet%202.1&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0).</span></span>
