---
title: "NuGet 2.1 发行说明 |Microsoft 文档"
author: karann-msft
ms.author: karann-msft
manager: ghogen
ms.date: 11/11/2016
ms.topic: article
ms.prod: nuget
ms.technology: 
ms.assetid: 6f972803-9e17-43f5-b77b-973c3accf695
description: "包括已知的问题、 bug 修复、 增加的功能，以及 DCRs NuGet 2.1 的发行说明。"
keywords: "NuGet 2.1 发行说明，bug 修复的已知问题，添加了一些功能，DCRs"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: c45cfb9f6a46a1efd9fe4531602191973da66290
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/14/2017
---
# <a name="nuget-21-release-notes"></a><span data-ttu-id="fb9eb-104">NuGet 2.1 发行说明</span><span class="sxs-lookup"><span data-stu-id="fb9eb-104">NuGet 2.1 Release Notes</span></span>

<span data-ttu-id="fb9eb-105">[NuGet 2.0 发行说明](../release-notes/nuget-2.0.md) | [NuGet 2.2 发行说明](../release-notes/nuget-2.2.md)</span><span class="sxs-lookup"><span data-stu-id="fb9eb-105">[NuGet 2.0 Release Notes](../release-notes/nuget-2.0.md) | [NuGet 2.2 Release Notes](../release-notes/nuget-2.2.md)</span></span>

<span data-ttu-id="fb9eb-106">NuGet 2.1 已于 2012 年 10 月 4 日发布。</span><span class="sxs-lookup"><span data-stu-id="fb9eb-106">NuGet 2.1 was released on October 4, 2012.</span></span>

## <a name="hierarchical-nugetconfig"></a><span data-ttu-id="fb9eb-107">分层 Nuget.Config</span><span class="sxs-lookup"><span data-stu-id="fb9eb-107">Hierarchical Nuget.Config</span></span>
<span data-ttu-id="fb9eb-108">NuGet 2.1 提供更灵活地控制通过以递归方式查找的文件夹结构向上遍历 NuGet 设置`NuGet.Config`文件，然后构建中找到的所有文件组的配置。</span><span class="sxs-lookup"><span data-stu-id="fb9eb-108">NuGet 2.1 gives you greater flexibility in controlling NuGet settings by way of recursively walking up the folder structure looking for `NuGet.Config` files and then building the configuration from the set of all found files.</span></span>  <span data-ttu-id="fb9eb-109">作为示例，请考虑其中团队具有的其他内部的依赖关系的 CI 生成的内部包存储库的方案。</span><span class="sxs-lookup"><span data-stu-id="fb9eb-109">As an example, consider the scenario where a team has an internal package repository for CI builds of other internal dependencies.</span></span> <span data-ttu-id="fb9eb-110">为单个项目的文件夹结构可能如下所示：</span><span class="sxs-lookup"><span data-stu-id="fb9eb-110">The folder structure for an individual project might look like the following:</span></span>

    C:\
    C:\myteam\
    C:\myteam\solution1
    C:\myteam\solution1\project1

<span data-ttu-id="fb9eb-111">此外，如果启用程序包还原了解决方案，还会存在以下文件夹：</span><span class="sxs-lookup"><span data-stu-id="fb9eb-111">Additionally, if package restore is enabled for the solution, the following folder will also exist:</span></span>

    C:\myteam\solution1\.nuget

<span data-ttu-id="fb9eb-112">为了具有可用的所有项目的团队处理，同时不使它可用于每个项目的计算机上的团队的内部的程序包存储库中，我们可以创建新的 Nuget.Config 文件，并将它置于 c:\myteam 文件夹。</span><span class="sxs-lookup"><span data-stu-id="fb9eb-112">In order to have the team’s internal package repository available for all projects that the team works on, while not making it available for every project on the machine, we can create a new Nuget.Config file and place it in the c:\myteam folder.</span></span> <span data-ttu-id="fb9eb-113">无法为指定每个项目的 packages 文件夹。</span><span class="sxs-lookup"><span data-stu-id="fb9eb-113">There is no way to specificy a packages folder per project.</span></span>

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

<span data-ttu-id="fb9eb-114">现在，我们可以看到的源通过从下 c:\myteam 如下所示的所有文件夹运行 'nuget.exe 资源' 命令添加：</span><span class="sxs-lookup"><span data-stu-id="fb9eb-114">We can now see that the source was added by running the ‘nuget.exe sources’ command from any folder beneath c:\myteam as shown below:</span></span>

![从父 nuget 配置的包源](./media/releasenotes-21-cfg-hierarchy.png)

<span data-ttu-id="fb9eb-116">`NuGet.Config`按以下顺序搜索了文件：</span><span class="sxs-lookup"><span data-stu-id="fb9eb-116">`NuGet.Config` files are searched for in the following order:</span></span>

1. `.nuget\Nuget.Config`
2. <span data-ttu-id="fb9eb-117">递归从项目文件夹审核到根</span><span class="sxs-lookup"><span data-stu-id="fb9eb-117">Recursive walk from project folder to root</span></span>
3. <span data-ttu-id="fb9eb-118">全局`Nuget.Config`(`%appdata%\NuGet\Nuget.Config`)</span><span class="sxs-lookup"><span data-stu-id="fb9eb-118">Global `Nuget.Config` (`%appdata%\NuGet\Nuget.Config`)</span></span>

<span data-ttu-id="fb9eb-119">配置是不是在应用*逆序*，这意味着，取决于上述排序，全局 Nuget.Config 将是首先应用、 发现 Nuget.Config 文件从根到项目文件夹依次跟通过`.nuget\Nuget.Config`。</span><span class="sxs-lookup"><span data-stu-id="fb9eb-119">The configurations are than applied in the *reverse order*, meaning that based on the above ordering, the global Nuget.Config would be applied first, followed by the discovered Nuget.Config files from root to project folder, followed by `.nuget\Nuget.Config`.</span></span>  <span data-ttu-id="fb9eb-120">这一点特别重要，如果你使用`<clear/>`要从配置中删除一组项的元素。</span><span class="sxs-lookup"><span data-stu-id="fb9eb-120">This is particularly important if you’re using the `<clear/>` element to remove a set of items from config.</span></span>

## <a name="specify-packages-folder-location"></a><span data-ttu-id="fb9eb-121">指定 packages 文件夹位置</span><span class="sxs-lookup"><span data-stu-id="fb9eb-121">Specify ‘packages’ Folder Location</span></span>
<span data-ttu-id="fb9eb-122">在过去，NuGet 具有托管的解决方案的根文件夹下找到的已知 packages 文件夹从解决方案的包。</span><span class="sxs-lookup"><span data-stu-id="fb9eb-122">In the past, NuGet has managed a solution’s packages from a known ‘packages’ folder found beneath the solution root folder.</span></span>  <span data-ttu-id="fb9eb-123">对于具有很多不同的解决方案的 NuGet 包安装的开发团队而言，这可能导致同一个包安装在文件系统上的许多不同的位置。</span><span class="sxs-lookup"><span data-stu-id="fb9eb-123">For development teams that have many different solutions which have NuGet packages installed, this can result in the same package being installed in many different places on the file system.</span></span>

<span data-ttu-id="fb9eb-124">NuGet 2.1 提供更精细地控制通过包文件夹的位置`repositoryPath`中的元素`NuGet.Config`文件。</span><span class="sxs-lookup"><span data-stu-id="fb9eb-124">NuGet 2.1 provides more granular control over the location of the packages folder via the `repositoryPath` element in the `NuGet.Config` file.</span></span>  <span data-ttu-id="fb9eb-125">生成的分层 Nuget.Config 支持前面的示例，假设我们想要有 C:\myteam\ 共享相同的包文件夹下的所有项目。</span><span class="sxs-lookup"><span data-stu-id="fb9eb-125">Building on the previous example of hierarchical Nuget.Config support, assume that we wish to have all projects under C:\myteam\ share the same packages folder.</span></span>  <span data-ttu-id="fb9eb-126">若要完成此操作，只需将添加以下条目到`c:\myteam\Nuget.Config`。</span><span class="sxs-lookup"><span data-stu-id="fb9eb-126">To accomplish this, simply add the following entry to `c:\myteam\Nuget.Config`.</span></span>

```xml
<configuration>
    <config>
    <add key="repositoryPath" value="C:\myteam\teampackages" />
    </config>
    ...
</configuration>
```

<span data-ttu-id="fb9eb-127">在此示例中，共享`Nuget.Config`文件指定无论深度创建下方 C:\myteam，每个项目的共享的包文件夹。</span><span class="sxs-lookup"><span data-stu-id="fb9eb-127">In this example, the shared `Nuget.Config` file specifies a shared packages folder for every project that is created beneath C:\myteam, regardless of depth.</span></span> <span data-ttu-id="fb9eb-128">请注意，是否你的解决方案根目录下有现有的包文件夹，你将需要将其删除之前 NuGet 会将包放置在新位置。</span><span class="sxs-lookup"><span data-stu-id="fb9eb-128">Note that if you have an existing packages folder underneath your solution root, you will need to delete it before NuGet will place packages in the new location.</span></span>

## <a name="support-for-portable-libraries"></a><span data-ttu-id="fb9eb-129">对可移植库的支持</span><span class="sxs-lookup"><span data-stu-id="fb9eb-129">Support for Portable Libraries</span></span>
<span data-ttu-id="fb9eb-130">[可移植库](http://msdn.microsoft.com/library/gg597391.aspx)是一项功能首次引入，可生成程序集的可在不修改不同 Microsoft 在平台上，从版本的.net Framework 对 Windows Phone 和 Xbox 甚至 Silverlight 的.NET 4360 （但在此期间，NuGet 不支持 Xbox 可移植运行库目标）。</span><span class="sxs-lookup"><span data-stu-id="fb9eb-130">[Portable libraries](http://msdn.microsoft.com/library/gg597391.aspx) is a feature first introduced with .NET 4 that enables you to build assemblies that can work without modification on different Microsoft platforms, from versions of the.NET Framework to Silverlight to Windows Phone and even Xbox 360 (though at this time, NuGet does not support the Xbox portable library target).</span></span>  <span data-ttu-id="fb9eb-131">通过扩展[打包约定](../create-packages/supporting-multiple-target-frameworks.md)framework 版本和配置文件，NuGet 2.1 现在支持可移植库，使您用于创建包来让复合 framework 和配置文件目标`lib`文件夹。</span><span class="sxs-lookup"><span data-stu-id="fb9eb-131">By extending the [package conventions](../create-packages/supporting-multiple-target-frameworks.md) for framework versions and profiles, NuGet 2.1 now supports portable libraries by enabling you to create packages that have compound framework and profile target `lib` folders.</span></span>

<span data-ttu-id="fb9eb-132">作为示例，请考虑以下可移植类库的可用目标平台。</span><span class="sxs-lookup"><span data-stu-id="fb9eb-132">As an example, consider the following portable class library’s available target platforms.</span></span>

![可移植运行库创建对话框](./media/releasenotes-21-plib.png)

<span data-ttu-id="fb9eb-134">构建库之后和命令`nuget.exe pack MyPortableProject.csproj`运行时，新的可移植库包文件夹结构可以看到，检查生成的 NuGet 包的内容。</span><span class="sxs-lookup"><span data-stu-id="fb9eb-134">After the library is built and the command `nuget.exe pack MyPortableProject.csproj` is run, the new portable library package folder structure can be seen by examining the contents of the generated NuGet package.</span></span>

![可移植运行库包布局](./media/releasenotes-21-plib-layout.png)

<span data-ttu-id="fb9eb-136">如你所见，可移植运行库文件夹命名约定遵循模式 '可移植 {框架 1} + {framework n}' framework 标识符遵循现有[framework 名称和版本约定](../schema/target-frameworks.md)。</span><span class="sxs-lookup"><span data-stu-id="fb9eb-136">As you can see, the portable library folder name convention follows the pattern ‘portable-{framework 1}+{framework n}’ where the framework identifiers follow the existing [framework name and version conventions](../schema/target-frameworks.md).</span></span> <span data-ttu-id="fb9eb-137">名称和版本约定的一个例外是用于 Windows Phone framework 标识符中找到。</span><span class="sxs-lookup"><span data-stu-id="fb9eb-137">One exception to the name and version conventions is found in the framework identifier used for Windows Phone.</span></span>  <span data-ttu-id="fb9eb-138">此名字对象应使用的框架名称 wp （wp7、 wp71 或 wp8）。</span><span class="sxs-lookup"><span data-stu-id="fb9eb-138">This moniker should use the framework name ‘wp’ (wp7, wp71 or wp8).</span></span> <span data-ttu-id="fb9eb-139">使用 silverlight-wp7，例如，将导致错误。</span><span class="sxs-lookup"><span data-stu-id="fb9eb-139">Using ‘silverlight-wp7’, for example, will result in an error.</span></span>

<span data-ttu-id="fb9eb-140">在安装时创建此文件夹结构中的包，NuGet 现在可以将其框架和配置文件规则应用到多个目标，作为文件夹名称中指定。</span><span class="sxs-lookup"><span data-stu-id="fb9eb-140">When installing the package that is created from this folder structure, NuGet can now apply its framework and profile rules to multiple targets, as specified in the folder name.</span></span>  <span data-ttu-id="fb9eb-141">在 NuGet 的匹配规则后面是，"详细"目标将优先于"不太具体"的原则。</span><span class="sxs-lookup"><span data-stu-id="fb9eb-141">Behind NuGet’s matching rules is the principle that “more specific” targets will take precedence over “less specific” ones.</span></span>  <span data-ttu-id="fb9eb-142">这意味着，面向特定平台的名字对象将始终为首选通过可移植的两个类型都与一个项目兼容。</span><span class="sxs-lookup"><span data-stu-id="fb9eb-142">This means that monikers targeting a specific platform will always be preferred over portable ones if they are both compatible with a project.</span></span>  <span data-ttu-id="fb9eb-143">此外，如果多个可移植目标符合项目，NuGet 将首选的一套支持的平台是"最靠近的"到项目引用包的一个。</span><span class="sxs-lookup"><span data-stu-id="fb9eb-143">Additionally, if multiple portable targets are compatible with a project, NuGet will prefer the one where the set of platforms supported is “closest” to the project referencing the package.</span></span>

## <a name="targeting-windows-8-and-windows-phone-8-projects"></a><span data-ttu-id="fb9eb-144">面向 Windows 8 和 Windows Phone 8 项目</span><span class="sxs-lookup"><span data-stu-id="fb9eb-144">Targeting Windows 8 and Windows Phone 8 Projects</span></span>
<span data-ttu-id="fb9eb-145">除了添加针对可移植类库项目的支持，NuGet 2.1 所提供的 Windows 8 应用商店和 Windows Phone 8 项目中，以及为 Windows 应用商店和 Windows Phone 项目将某些新常规名字对象的新框架名字对象易于管理各个将来版本的相应的平台。</span><span class="sxs-lookup"><span data-stu-id="fb9eb-145">In addition to adding support for targeting portable library projects, NuGet 2.1 provides new framework monikers for both Windows 8 Store and Windows Phone 8 projects, as well as some new general monikers for Windows Store and Windows Phone projects that will be easier to manage across future versions of the respective platforms.</span></span>

<span data-ttu-id="fb9eb-146">对于 Windows 8 应用商店应用程序中，标识符如下所示：</span><span class="sxs-lookup"><span data-stu-id="fb9eb-146">For Windows 8 Store applications, the identifiers look as follows:</span></span>

|<span data-ttu-id="fb9eb-147">NuGet 2.0 及更早版本</span><span class="sxs-lookup"><span data-stu-id="fb9eb-147">NuGet 2.0 and earlier</span></span>|<span data-ttu-id="fb9eb-148">NuGet 2.1</span><span class="sxs-lookup"><span data-stu-id="fb9eb-148">NuGet 2.1</span></span>|
|----------------|-----------|
|<span data-ttu-id="fb9eb-149">winRT45。NETCore45</span><span class="sxs-lookup"><span data-stu-id="fb9eb-149">winRT45, .NETCore45</span></span>|<span data-ttu-id="fb9eb-150">Windows、 windows 8，win win8</span><span class="sxs-lookup"><span data-stu-id="fb9eb-150">Windows, Windows8, win, win8</span></span>|

<br/>
<span data-ttu-id="fb9eb-151">对于 Windows Phone 项目，标识符如下所示：</span><span class="sxs-lookup"><span data-stu-id="fb9eb-151">For Windows Phone projects, the identifiers look as follows:</span></span>

|<span data-ttu-id="fb9eb-152">Phone OS</span><span class="sxs-lookup"><span data-stu-id="fb9eb-152">Phone OS</span></span>|<span data-ttu-id="fb9eb-153">NuGet 2.0 及更早版本</span><span class="sxs-lookup"><span data-stu-id="fb9eb-153">NuGet 2.0 and earlier</span></span>|<span data-ttu-id="fb9eb-154">NuGet 2.1</span><span class="sxs-lookup"><span data-stu-id="fb9eb-154">NuGet 2.1</span></span>
|----------------|-----------|-----------|
|<span data-ttu-id="fb9eb-155">Windows Phone 7</span><span class="sxs-lookup"><span data-stu-id="fb9eb-155">Windows Phone 7</span></span>|<span data-ttu-id="fb9eb-156">silverlight3 wp</span><span class="sxs-lookup"><span data-stu-id="fb9eb-156">silverlight3-wp</span></span>|<span data-ttu-id="fb9eb-157">wp，wp7，WindowsPhone WindowsPhone7</span><span class="sxs-lookup"><span data-stu-id="fb9eb-157">wp, wp7, WindowsPhone, WindowsPhone7</span></span>|
|<span data-ttu-id="fb9eb-158">Windows Phone 7.5 (Mango)</span><span class="sxs-lookup"><span data-stu-id="fb9eb-158">Windows Phone 7.5 (Mango)</span></span>|<span data-ttu-id="fb9eb-159">silverilght4 wp71</span><span class="sxs-lookup"><span data-stu-id="fb9eb-159">silverilght4-wp71</span></span>|<span data-ttu-id="fb9eb-160">wp71 WindowsPhone71</span><span class="sxs-lookup"><span data-stu-id="fb9eb-160">wp71, WindowsPhone71</span></span>|
|<span data-ttu-id="fb9eb-161">Windows Phone 8</span><span class="sxs-lookup"><span data-stu-id="fb9eb-161">Windows Phone 8</span></span>|<span data-ttu-id="fb9eb-162">（不支持）</span><span class="sxs-lookup"><span data-stu-id="fb9eb-162">(not supported)</span></span>|<span data-ttu-id="fb9eb-163">wp8 WindowsPhone8</span><span class="sxs-lookup"><span data-stu-id="fb9eb-163">wp8, WindowsPhone8</span></span>|
<br/>
<span data-ttu-id="fb9eb-164">在所有上述更改，旧的框架名称将继续由 NuGet 2.1 完全支持。</span><span class="sxs-lookup"><span data-stu-id="fb9eb-164">In all of the above changes, the old framework names will continue to be fully supported by NuGet 2.1.</span></span>  <span data-ttu-id="fb9eb-165">接着，新名称应使用因为将更稳定，各个将来版本的相应的平台。</span><span class="sxs-lookup"><span data-stu-id="fb9eb-165">Moving forward, the new names should be used as they will be more stable across future versions of the respective platforms.</span></span> <span data-ttu-id="fb9eb-166">新名称将*不*是 2.1 之前的 NuGet 版本中受支持，但是，因此制定相应的计划来确定何时进行切换。</span><span class="sxs-lookup"><span data-stu-id="fb9eb-166">The new names will *not* be supported in versions of NuGet prior to 2.1, however, so plan accordingly for when to make the switch.</span></span>

## <a name="improved-search-in-package-manager-dialog"></a><span data-ttu-id="fb9eb-167">改进的搜索，在程序包管理器对话框</span><span class="sxs-lookup"><span data-stu-id="fb9eb-167">Improved Search in Package Manager Dialog</span></span>
<span data-ttu-id="fb9eb-168">通过过去的若干次迭代，更改已引入到极大地改进的速度和相关性的包搜索 NuGet 库。</span><span class="sxs-lookup"><span data-stu-id="fb9eb-168">Over the past several iterations, changes have been introduced to the NuGet gallery that greatly improved the speed and relevance of package searches.</span></span>  <span data-ttu-id="fb9eb-169">但是，这些改进会受限于 nuget.org Web 站点。</span><span class="sxs-lookup"><span data-stu-id="fb9eb-169">However, these improvements were limited to the nuget.org Web site.</span></span>  <span data-ttu-id="fb9eb-170">NuGet 2.1 使改进的搜索体验可通过 NuGet 包管理器对话框。</span><span class="sxs-lookup"><span data-stu-id="fb9eb-170">NuGet 2.1 makes the improved search experience available through the NuGet package manager dialog.</span></span>  <span data-ttu-id="fb9eb-171">例如，假设你想要查找 Windows Azure Caching 预览包。</span><span class="sxs-lookup"><span data-stu-id="fb9eb-171">As an example, imagine that you wanted to find the Windows Azure Caching Preview package.</span></span>  <span data-ttu-id="fb9eb-172">此包的合理的搜索查询可能是"Azure 缓存"。</span><span class="sxs-lookup"><span data-stu-id="fb9eb-172">A reasonable search query for this package may be “Azure Cache”.</span></span>  <span data-ttu-id="fb9eb-173">在以前版本的包管理器对话框中，所需的包将不甚至上列出的结果的第一页。</span><span class="sxs-lookup"><span data-stu-id="fb9eb-173">In previous versions of the package manager dialog, the desired package would not even be listed on the first page of results.</span></span>  <span data-ttu-id="fb9eb-174">但是，在 NuGet 2.1 中，所需的包现在显示在搜索结果顶部。</span><span class="sxs-lookup"><span data-stu-id="fb9eb-174">However, in NuGet 2.1, the desired package now shows up at the top of the search results.</span></span>

![包管理器对话框搜索](./media/releasenotes-21-vsdlg-search.png)

## <a name="force-package-update"></a><span data-ttu-id="fb9eb-176">强制包更新</span><span class="sxs-lookup"><span data-stu-id="fb9eb-176">Force Package Update</span></span>
<span data-ttu-id="fb9eb-177">在 NuGet 2.1 之前 NuGet 将跳过更新包时不高的版本号。</span><span class="sxs-lookup"><span data-stu-id="fb9eb-177">Prior to NuGet 2.1, NuGet would skip updating a package when there was a not a high version number.</span></span>  <span data-ttu-id="fb9eb-178">这就产生了某些方案-尤其是对于其中团队又不想针对每个生成的数字将包版本递增的生成或 CI 方案的问题。</span><span class="sxs-lookup"><span data-stu-id="fb9eb-178">This introduced friction for certain scenarios – particularly in the case of build or CI scenarios where the team did not want to increment the package version number with each build.</span></span>  <span data-ttu-id="fb9eb-179">所需的行为是强制执行更新而不考虑。</span><span class="sxs-lookup"><span data-stu-id="fb9eb-179">The desired behavior was to force an update regardless.</span></span>  <span data-ttu-id="fb9eb-180">NuGet 2.1 可解决这的重新安装标志。</span><span class="sxs-lookup"><span data-stu-id="fb9eb-180">NuGet 2.1 addresses this with the ‘reinstall’ flag.</span></span>  <span data-ttu-id="fb9eb-181">例如，当尝试更新包中没有的较新的包版本以前版本的 NuGet 将导致以下：</span><span class="sxs-lookup"><span data-stu-id="fb9eb-181">For example, previous versions of NuGet would result in the following when attempting to update a package that did not have a more recent package version:</span></span>

    PM> Update-Package Moq
    No updates available for 'Moq' in project 'MySolution.MyConsole'.

<span data-ttu-id="fb9eb-182">进行重新安装标志，包将会更新而不管是否没有较新版本。</span><span class="sxs-lookup"><span data-stu-id="fb9eb-182">With the reinstall flag, the package will be updated regardless of whether there is a newer version.</span></span>

    PM> Update-Package Moq -Reinstall
    Successfully removed 'Moq 4.0.10827' from MySolution.MyConsole.
    Successfully uninstalled 'Moq 4.0.10827'.
    Successfully installed 'Moq 4.0.10827'.
    Successfully added 'Moq 4.0.10827' to MySolution.MyConsole.

<span data-ttu-id="fb9eb-183">重新安装标志证明有益的另一种情况是 framework 重定目标。</span><span class="sxs-lookup"><span data-stu-id="fb9eb-183">Another scenario where the reinstall flag proves beneficial is that of framework re-targeting.</span></span> <span data-ttu-id="fb9eb-184">更改一个项目 （例如，为.NET 4.5 的.NET 4) 的目标框架时更新包的重新安装可更新对项目中安装的所有 NuGet 包的正确程序集的引用。</span><span class="sxs-lookup"><span data-stu-id="fb9eb-184">When changing the target framework of a project (for example, from .NET 4 to .NET 4.5), Update-Package -Reinstall can update references to the correct assemblies for all NuGet packages installed in the project.</span></span>

## <a name="edit-package-sources-within-visual-studio"></a><span data-ttu-id="fb9eb-185">编辑 Visual Studio 中的包源</span><span class="sxs-lookup"><span data-stu-id="fb9eb-185">Edit Package Sources Within Visual Studio</span></span>
<span data-ttu-id="fb9eb-186">在以前版本的 NuGet 中，更新在 Visual Studio 选项对话框中所需删除然后重新添加包源从包源。</span><span class="sxs-lookup"><span data-stu-id="fb9eb-186">In previous versions of NuGet, updating a package source from within the Visual Studio options dialog required deleting and re-adding the package source.</span></span>  <span data-ttu-id="fb9eb-187">NuGet 2.1 通过支持为配置用户界面的第一类函数的更新，提高了此工作流。</span><span class="sxs-lookup"><span data-stu-id="fb9eb-187">NuGet 2.1 improves this workflow by supporting update as a first class function of the configuration user interface.</span></span>

![包管理器配置对话框](./media/releasenotes-21-edit-pkg-source.png)

## <a name="bug-fixes"></a><span data-ttu-id="fb9eb-189">Bug 修复</span><span class="sxs-lookup"><span data-stu-id="fb9eb-189">Bug Fixes</span></span>
<span data-ttu-id="fb9eb-190">NuGet 2.1 包括许多的 bug 修补程序。</span><span class="sxs-lookup"><span data-stu-id="fb9eb-190">NuGet 2.1 includes many bug fixes.</span></span> <span data-ttu-id="fb9eb-191">有关工作的完整列表项固定在 NuGet 2.0 中，请查看[对于此版本的 NuGet 问题跟踪程序](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Fixed&type=All&priority=All&release=NuGet%202.1&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0)。</span><span class="sxs-lookup"><span data-stu-id="fb9eb-191">For a full list of work items fixed in NuGet 2.0, please view the [NuGet Issue Tracker for this release](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Fixed&type=All&priority=All&release=NuGet%202.1&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0).</span></span>
