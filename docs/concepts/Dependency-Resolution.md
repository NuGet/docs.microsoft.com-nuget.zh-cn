---
title: NuGet 包依赖项解析
description: 详细说明解析 NuGet 包的依赖项以及在 NuGet 2.x 和 NuGet 3.x+ 上安装依赖项的流程。
author: karann-msft
ms.author: karann
ms.date: 08/14/2017
ms.topic: conceptual
ms.openlocfilehash: 4b95251e4b055523a9533b4125589b2650be932d
ms.sourcegitcommit: ddb52131e84dd54db199ce8331f6da18aa3feea1
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/16/2020
ms.locfileid: "79428467"
---
# <a name="how-nuget-resolves-package-dependencies"></a><span data-ttu-id="942d0-103">NuGet 如何解析包依赖项</span><span class="sxs-lookup"><span data-stu-id="942d0-103">How NuGet resolves package dependencies</span></span>

<span data-ttu-id="942d0-104">每当安装或重新安装包（包括在[还原](../consume-packages/package-restore.md)过程中安装）时，NuGet 还会安装第一个包所依赖的任何其他包。</span><span class="sxs-lookup"><span data-stu-id="942d0-104">Any time a package is installed or reinstalled, which includes being installed as part of a [restore](../consume-packages/package-restore.md) process, NuGet also installs any additional packages on which that first package depends.</span></span>

<span data-ttu-id="942d0-105">这些直接依赖项可能本身也具有依赖项，并可能继续延伸到任意深度。</span><span class="sxs-lookup"><span data-stu-id="942d0-105">Those immediate dependencies might then also have dependencies on their own, which can continue to an arbitrary depth.</span></span> <span data-ttu-id="942d0-106">这便形成了所谓的“依赖项关系图”，用于说明各级包之间的关系  。</span><span class="sxs-lookup"><span data-stu-id="942d0-106">This produces what's called a *dependency graph* that describes the relationships between packages at all levels.</span></span>

<span data-ttu-id="942d0-107">当多个包具有相同的依赖项时，同一个包 ID 会在关系图中多次出现且可能具有不同的版本约束。</span><span class="sxs-lookup"><span data-stu-id="942d0-107">When multiple packages have the same dependency, then the same package ID can appear in the graph multiple times, potentially with different version constraints.</span></span> <span data-ttu-id="942d0-108">但是，一个项目中只能使用给定包的一个版本，因此 NuGet 必须选择要使用的版本。</span><span class="sxs-lookup"><span data-stu-id="942d0-108">However, only one version of a given package can be used in a project, so NuGet must choose which version is used.</span></span> <span data-ttu-id="942d0-109">确切流程取决于要使用的包管理格式。</span><span class="sxs-lookup"><span data-stu-id="942d0-109">The exact process depends on the package management format being used.</span></span>

## <a name="dependency-resolution-with-packagereference"></a><span data-ttu-id="942d0-110">利用 PackageReference 解析依赖项</span><span class="sxs-lookup"><span data-stu-id="942d0-110">Dependency resolution with PackageReference</span></span>

<span data-ttu-id="942d0-111">当将包安装到使用 PackageReference 格式的项目中时，NuGet 将添加对相应文件中的平面包关系图的引用并提前解决冲突。</span><span class="sxs-lookup"><span data-stu-id="942d0-111">When installing packages into projects using the PackageReference format, NuGet adds references to a flat package graph in the appropriate file and resolves conflicts ahead of time.</span></span> <span data-ttu-id="942d0-112">此过程称为“传递还原”  。</span><span class="sxs-lookup"><span data-stu-id="942d0-112">This process is referred to as *transitive restore*.</span></span> <span data-ttu-id="942d0-113">重新安装或还原包指的是下载关系图中列出的包的过程，此过程可加快生成的速度和提高其可预测性。</span><span class="sxs-lookup"><span data-stu-id="942d0-113">Reinstalling or restoring packages is then a process of downloading the packages listed in the graph, resulting in faster and more predictable builds.</span></span> <span data-ttu-id="942d0-114">还可以利用 2.8.\* 等可变版本，以避免为了能使用最新版本的包而修改项目。</span><span class="sxs-lookup"><span data-stu-id="942d0-114">You can also take advantage of floating versions, such as 2.8.\*,  to avoid modifying the project to use the latest version of a package.</span></span>

<span data-ttu-id="942d0-115">当 NuGet 还原进程在生成之前运行时，它将首先解析内存中的依赖项，然后将生成的关系图写入名为 `project.assets.json` 的文件。</span><span class="sxs-lookup"><span data-stu-id="942d0-115">When the NuGet restore process runs prior to a build, it resolves dependencies first in memory, then writes the resulting graph to a file called `project.assets.json`.</span></span> <span data-ttu-id="942d0-116">如果[启用了锁定文件功能](../consume-packages/package-references-in-project-files.md#locking-dependencies)，它还会将已解析的依赖项写入名为 `packages.lock.json` 的锁定文件。</span><span class="sxs-lookup"><span data-stu-id="942d0-116">It also writes the resolved dependencies to a lock file named `packages.lock.json`, if the [lock file functionality is enabled](../consume-packages/package-references-in-project-files.md#locking-dependencies).</span></span>
<span data-ttu-id="942d0-117">资产文件位于 `MSBuildProjectExtensionsPath`，它默认是项目的“obj”文件夹。</span><span class="sxs-lookup"><span data-stu-id="942d0-117">The assets file is located at `MSBuildProjectExtensionsPath`, which defaults to the project's 'obj' folder.</span></span> <span data-ttu-id="942d0-118">MSBuild 随后将读取此文件并将其转换成一组文件夹（可在其中找到潜在引用），然后将它们添加到内存中的项目树。</span><span class="sxs-lookup"><span data-stu-id="942d0-118">MSBuild then reads this file and translates it into a set of folders where potential references can be found, and then adds them to the project tree in memory.</span></span>

<span data-ttu-id="942d0-119">`project.assets.json` 文件是临时的，不应添加到源代码管理中。</span><span class="sxs-lookup"><span data-stu-id="942d0-119">The `project.assets.json` file is temporary and should not be added to source control.</span></span> <span data-ttu-id="942d0-120">默认情况下，此文件将在 `.gitignore` 和 `.tfignore` 中列出。</span><span class="sxs-lookup"><span data-stu-id="942d0-120">It's listed by default in both `.gitignore` and `.tfignore`.</span></span> <span data-ttu-id="942d0-121">请参阅[包与源代码管理](../consume-packages/packages-and-source-control.md)。</span><span class="sxs-lookup"><span data-stu-id="942d0-121">See [Packages and source control](../consume-packages/packages-and-source-control.md).</span></span>

### <a name="dependency-resolution-rules"></a><span data-ttu-id="942d0-122">依赖项解析规则</span><span class="sxs-lookup"><span data-stu-id="942d0-122">Dependency resolution rules</span></span>

<span data-ttu-id="942d0-123">传递还原应用 4 条主要规则来解析依赖项：最低适用版本、可变版本、选择最近项和等距依赖项。</span><span class="sxs-lookup"><span data-stu-id="942d0-123">Transitive restore applies four main rules to resolve dependencies: lowest applicable version, floating versions, nearest-wins, and cousin dependencies.</span></span>

<a name="lowest-applicable-version"></a>

#### <a name="lowest-applicable-version"></a><span data-ttu-id="942d0-124">最低适用版本</span><span class="sxs-lookup"><span data-stu-id="942d0-124">Lowest applicable version</span></span>

<span data-ttu-id="942d0-125">最低适用版本规则根据包依赖项的定义还原包的最低可能版本。</span><span class="sxs-lookup"><span data-stu-id="942d0-125">The lowest applicable version rule restores the lowest possible version of a package as defined by its dependencies.</span></span> <span data-ttu-id="942d0-126">此规则还适用于应用程序上或类库上未声明为[可变](#floating-versions)的依赖项。</span><span class="sxs-lookup"><span data-stu-id="942d0-126">It also applies to dependencies on the application or the class library unless declared as [floating](#floating-versions).</span></span>

<span data-ttu-id="942d0-127">例如在下图中，1.0 beta 版本低于 1.0，因此 NuGet 选择 1.0 版本：</span><span class="sxs-lookup"><span data-stu-id="942d0-127">In the following figure, for example, 1.0-beta is considered lower than 1.0 so NuGet chooses the 1.0 version:</span></span>

![选择最低适用版本](media/projectJson-dependency-1.png)

<span data-ttu-id="942d0-129">在下图中，版本约束为 >= 2.1，但源上未提供版本 2.1 ，因此 NuGet 选取能找到的下一个最低版本，在此示例中即为 2.2：</span><span class="sxs-lookup"><span data-stu-id="942d0-129">In the next figure, version 2.1 is not available on the feed but because the version constraint is >= 2.1 NuGet picks the next lowest version it can find, in this case 2.2:</span></span>

![选择源上提供的下一个最低版本](media/projectJson-dependency-2.png)

<span data-ttu-id="942d0-131">当源上未提供应用程序指定的确切版本号（如 1.2）时，NuGet 将在尝试安装或还原包时出错并导致失败：</span><span class="sxs-lookup"><span data-stu-id="942d0-131">When an application specifies an exact version number, such as 1.2, that is not available on the feed, NuGet fails with an error when attempting to install or restore the package:</span></span>

![NuGet 在未提供确切包版本时生成错误](media/projectJson-dependency-3.png)

<a name="floating-versions"></a>

#### <a name="floating-versions"></a><span data-ttu-id="942d0-133">可变版本</span><span class="sxs-lookup"><span data-stu-id="942d0-133">Floating versions</span></span>

<span data-ttu-id="942d0-134">可变依赖项版本由 \* 字符指定。</span><span class="sxs-lookup"><span data-stu-id="942d0-134">A floating dependency version is specified with the \* character.</span></span> <span data-ttu-id="942d0-135">例如 `6.0.*`。</span><span class="sxs-lookup"><span data-stu-id="942d0-135">For example, `6.0.*`.</span></span> <span data-ttu-id="942d0-136">此版本规格表示“使用最新的 6.0.x 版本”；`4.*` 则表示“使用最新的 4.x 版本”。</span><span class="sxs-lookup"><span data-stu-id="942d0-136">This version specification says "use the latest 6.0.x version"; `4.*` means "use the latest 4.x version."</span></span> <span data-ttu-id="942d0-137">使用可变版本可减少对项目文件的更改，同时确保始终使用最新版本的依赖项。</span><span class="sxs-lookup"><span data-stu-id="942d0-137">Using a floating version reduces changes to the project file, while keeping up to date with the latest version of a dependency.</span></span>

<span data-ttu-id="942d0-138">使用可变版本时，NuGet 将解析与版本模式匹配的最高包版本，例如，请求 `6.0.*` 将获得以 6.0 开头的最高包版本：</span><span class="sxs-lookup"><span data-stu-id="942d0-138">When using a floating version, NuGet resolves the highest version of a package that matches the version pattern, for example `6.0.*` gets the highest version of a package that starts with 6.0:</span></span>

![请求可变版本 6.0.\* 时，选取版本 6.0.1](media/projectJson-dependency-4.png)

> [!Note]
> <span data-ttu-id="942d0-140">有关可变版本和预发行版本的行为的信息，请参阅[包版本控制](package-versioning.md#version-ranges)。</span><span class="sxs-lookup"><span data-stu-id="942d0-140">For information on the behavior of floating versions and pre-release versions, see [Package versioning](package-versioning.md#version-ranges).</span></span>


<a name="nearest-wins"></a>

#### <a name="nearest-wins"></a><span data-ttu-id="942d0-141">选择最近项</span><span class="sxs-lookup"><span data-stu-id="942d0-141">Nearest wins</span></span>

<span data-ttu-id="942d0-142">当应用程序的包关系图包含相同包的不同版本时，NuGet 将选择关系图中最接近应用程序的包并忽略所有其他包。</span><span class="sxs-lookup"><span data-stu-id="942d0-142">When the package graph for an application contains different versions of the same package, NuGet chooses the package that's closest to the application in the graph and ignores all others.</span></span> <span data-ttu-id="942d0-143">通过此行为，应用程序能够替代依赖项关系图中的任何特定包版本。</span><span class="sxs-lookup"><span data-stu-id="942d0-143">This behavior allows an application to override any particular package version in the dependency graph.</span></span>

<span data-ttu-id="942d0-144">在下面的示例中，应用程序直接依赖于版本约束为 >=2.0 的包 B。</span><span class="sxs-lookup"><span data-stu-id="942d0-144">In the example below, the application depends directly on Package B with a version constraint of >=2.0.</span></span> <span data-ttu-id="942d0-145">应用程序还依赖于版本约束为 >=1.0 的包 A，此包依赖于包 B。</span><span class="sxs-lookup"><span data-stu-id="942d0-145">The application also depends on Package A which in turn also depends on Package B, but with a >=1.0 constraint.</span></span> <span data-ttu-id="942d0-146">在关系图中，由于包 B 2.0 上的依赖项更接近应用程序，因此将使用该版本：</span><span class="sxs-lookup"><span data-stu-id="942d0-146">Because the dependency on Package B 2.0 is nearer to the application in the graph, that version is used:</span></span>

![使用“选择最近项”规则的应用程序](media/projectJson-dependency-5.png)

>[!Warning]
> <span data-ttu-id="942d0-148">“选择最近项”规则可导致包版本降级，可能破坏关系图中的其他依赖项。</span><span class="sxs-lookup"><span data-stu-id="942d0-148">The Nearest Wins rule can result in a downgrade of the package version, thus potentially breaking other dependencies in the graph.</span></span> <span data-ttu-id="942d0-149">因此用户应用此规则时会收到警告提醒。</span><span class="sxs-lookup"><span data-stu-id="942d0-149">Hence this rule is applied with a warning to alert the user.</span></span>

<span data-ttu-id="942d0-150">此规则还可提高大型依赖项关系图（如具有 BCL 包的关系图）的效率，因为忽略某个给定依赖项后，NuGet 还将忽略关系图中该分支上的所有其余依赖项。</span><span class="sxs-lookup"><span data-stu-id="942d0-150">This rule also results in greater efficiency with a large dependency graph (such as those with the BCL packages) because once a given dependency is ignored, NuGet also ignores all remaining dependencies on that branch of the graph.</span></span> <span data-ttu-id="942d0-151">例如在下图中，由于使用了包 C 2.0，因此 NuGet 忽略了关系图中引用旧版包 C 的所有分支：</span><span class="sxs-lookup"><span data-stu-id="942d0-151">In the diagram below, for example, because Package C 2.0 is used, NuGet ignores any branches in the graph that refer to an older version of Package C:</span></span>

![当 NuGet 忽略关系图中的某个包时，它将忽略其所在的整个分支](media/projectJson-dependency-6.png)

<a name="cousin-dependencies"></a>

#### <a name="cousin-dependencies"></a><span data-ttu-id="942d0-153">等距依赖项</span><span class="sxs-lookup"><span data-stu-id="942d0-153">Cousin dependencies</span></span>

<span data-ttu-id="942d0-154">当关系图中引用的不同包版本与应用程序具有相同距离时，NuGet 将使用满足所有版本要求的最低版本（与[最低适用版本](#lowest-applicable-version)和[可变版本](#floating-versions)规则相似）。</span><span class="sxs-lookup"><span data-stu-id="942d0-154">When different package versions are referred to at the same distance in the graph from the application, NuGet uses the lowest version that satisfies all version requirements (as with the [lowest applicable version](#lowest-applicable-version) and [floating versions](#floating-versions) rules).</span></span> <span data-ttu-id="942d0-155">例如在下图中，2.0 版本的包 B 满足另一个 >=1.0 约束，因此使用此包：</span><span class="sxs-lookup"><span data-stu-id="942d0-155">In the image below, for example, version 2.0 of Package B satisfies the other >=1.0 constraint, and is thus used:</span></span>

![使用满足所有约束的较低版本解析等距依赖项](media/projectJson-dependency-7.png)

<span data-ttu-id="942d0-157">某些情况下无法满足所有版本要求。</span><span class="sxs-lookup"><span data-stu-id="942d0-157">In some cases, it's not possible to meet all version requirements.</span></span> <span data-ttu-id="942d0-158">如下所示，如果包 A 明确要求包 B 1.0，而包 C 要求包 B >=2.0，NuGet 则无法解析依赖项并显示错误。</span><span class="sxs-lookup"><span data-stu-id="942d0-158">As shown below, if Package A requires exactly Package B 1.0 and Package C requires Package B >=2.0, then NuGet cannot resolve the dependencies and gives an error.</span></span>

![确切版本要求导致无法解析依赖项](media/projectJson-dependency-8.png)

<span data-ttu-id="942d0-160">在此情况下，顶层使用者（应用程序或包）应在包 B 上添加其自己的直接依赖项，以便应用[选择最近项](#nearest-wins)规则。</span><span class="sxs-lookup"><span data-stu-id="942d0-160">In these situations, the top-level consumer (the application or package) should add its own direct dependency on Package B so that the [Nearest Wins](#nearest-wins) rule applies.</span></span>

## <a name="dependency-resolution-with-packagesconfig"></a><span data-ttu-id="942d0-161">利用 packages.config 解析依赖项</span><span class="sxs-lookup"><span data-stu-id="942d0-161">Dependency resolution with packages.config</span></span>

<span data-ttu-id="942d0-162">利用 `packages.config`，项目依赖项 将作为简单列表写入 `packages.config`。</span><span class="sxs-lookup"><span data-stu-id="942d0-162">With `packages.config`, a project's dependencies are written to `packages.config` as a flat list.</span></span> <span data-ttu-id="942d0-163">这些包的所有依赖项也将写入同一列表。</span><span class="sxs-lookup"><span data-stu-id="942d0-163">Any dependencies of those packages are also written in the same list.</span></span> <span data-ttu-id="942d0-164">安装包时，NuGet 可能还会修改 `.csproj` 文件、`app.config`、`web.config` 和其他单独文件。</span><span class="sxs-lookup"><span data-stu-id="942d0-164">When packages are installed, NuGet might also modify the `.csproj` file, `app.config`, `web.config`, and other individual files.</span></span>

<span data-ttu-id="942d0-165">利用 `packages.config`，NuGet 可尝试解决在安装每个单独包期间出现的依赖项冲突。</span><span class="sxs-lookup"><span data-stu-id="942d0-165">With `packages.config`, NuGet attempts to resolve dependency conflicts during the installation of each individual package.</span></span> <span data-ttu-id="942d0-166">也就是说，如果正在安装包 A 并且其依赖于包 B，同时包 B 已作为其他项的依赖项在 `packages.config` 中列出，则 NuGet 将比较所请求的包 B 版本，并尝试找到满足所有版本约束的版本。</span><span class="sxs-lookup"><span data-stu-id="942d0-166">That is, if Package A is being installed and depends on Package B, and Package B is already listed in `packages.config` as a dependency of something else, NuGet compares the versions of Package B being requested and attempts to find a version that satisfies all version constraints.</span></span> <span data-ttu-id="942d0-167">具体而言，NuGet 将选择可满足依赖项的较低 major.minor 版本  。</span><span class="sxs-lookup"><span data-stu-id="942d0-167">Specifically, NuGet selects the lower *major.minor* version that satisfies dependencies.</span></span>

<span data-ttu-id="942d0-168">默认情况下，NuGet 2.8 会查找最低的修补程序版本（请参阅 [NuGet 2.8 发行说明](../release-notes/nuget-2.8.md#patch-resolution-for-dependencies)）。</span><span class="sxs-lookup"><span data-stu-id="942d0-168">By default, NuGet 2.8 looks for the lowest patch version (see [NuGet 2.8 release notes](../release-notes/nuget-2.8.md#patch-resolution-for-dependencies)).</span></span> <span data-ttu-id="942d0-169">可以通过 `Nuget.Config` 中的 `DependencyVersion` 属性和命令行上的 `-DependencyVersion` 开关控制此设置。</span><span class="sxs-lookup"><span data-stu-id="942d0-169">You can control this setting through the `DependencyVersion` attribute in `Nuget.Config` and the `-DependencyVersion` switch on the command line.</span></span>  

<span data-ttu-id="942d0-170">用于解析依赖项的 `packages.config` 进程会随着依赖项关系图的规模增大而愈加复杂。</span><span class="sxs-lookup"><span data-stu-id="942d0-170">The `packages.config` process for resolving dependencies gets complicated for larger dependency graphs.</span></span> <span data-ttu-id="942d0-171">每次安装新包都需要遍历整个关系图，并且可能引发版本冲突。</span><span class="sxs-lookup"><span data-stu-id="942d0-171">Each new package installation requires a traversal of the whole graph and raises the chance for version conflicts.</span></span> <span data-ttu-id="942d0-172">发生冲突时，安装将停止，此时项目处于不确定状态，很可能导致项目文件本身发生更改。</span><span class="sxs-lookup"><span data-stu-id="942d0-172">When a conflict occurs, installation is stopped, leaving the project in an indeterminate state, especially with potential modifications to the project file itself.</span></span> <span data-ttu-id="942d0-173">使用其他包管理格式时则不会出现此问题。</span><span class="sxs-lookup"><span data-stu-id="942d0-173">This is not an issue when using other package management formats.</span></span>

## <a name="managing-dependency-assets"></a><span data-ttu-id="942d0-174">管理依赖项资产</span><span class="sxs-lookup"><span data-stu-id="942d0-174">Managing dependency assets</span></span>

<span data-ttu-id="942d0-175">使用 PackageReference 格式时，可以控制依赖项中的哪些资产可流入顶层项目。</span><span class="sxs-lookup"><span data-stu-id="942d0-175">When using the PackageReference format, you can control which assets from dependencies flow into the top-level project.</span></span> <span data-ttu-id="942d0-176">有关详细信息，请参阅 [PackageReference](../consume-packages/package-references-in-project-files.md#controlling-dependency-assets)。</span><span class="sxs-lookup"><span data-stu-id="942d0-176">For details, see [PackageReference](../consume-packages/package-references-in-project-files.md#controlling-dependency-assets).</span></span>

<span data-ttu-id="942d0-177">当顶层项目本身是一个包时，还需要使用其依赖项在 `.nuspec` 文件中列出的 `include` 和 `exclude` 属性来控制此流。</span><span class="sxs-lookup"><span data-stu-id="942d0-177">When the top-level project is itself a package, you also have control over this flow by using the `include` and `exclude` attributes with dependencies listed in the `.nuspec` file.</span></span> <span data-ttu-id="942d0-178">请参阅 [.nuspec 引用 - 依赖项](../reference/nuspec.md#dependencies)。</span><span class="sxs-lookup"><span data-stu-id="942d0-178">See [.nuspec Reference - Dependencies](../reference/nuspec.md#dependencies).</span></span>

## <a name="excluding-references"></a><span data-ttu-id="942d0-179">排除引用</span><span class="sxs-lookup"><span data-stu-id="942d0-179">Excluding references</span></span>

<span data-ttu-id="942d0-180">对于有些方案，同一项目中可能多次引用具有相同名称的程序集，并因此生成设计时和生成时错误。</span><span class="sxs-lookup"><span data-stu-id="942d0-180">There are scenarios in which assemblies with the same name might be referenced more than once in a project, producing design-time and build-time errors.</span></span> <span data-ttu-id="942d0-181">例如，某个项目既包含自定义版本的 `C.dll`，又引用同样包含 `C.dll` 的包 C。</span><span class="sxs-lookup"><span data-stu-id="942d0-181">Consider a project that contains a custom version of `C.dll`, and references Package C that also contains `C.dll`.</span></span> <span data-ttu-id="942d0-182">同时，该项目还依赖于同样依赖于包 C 和 `C.dll` 的包 B。</span><span class="sxs-lookup"><span data-stu-id="942d0-182">At the same time, the project also depends on Package B which also depends on Package C and `C.dll`.</span></span> <span data-ttu-id="942d0-183">在此情况下，NuGet 无法确定要使用哪一个 `C.dll`，但你也不能直接删除包 C 上的项目依赖项，因为包 B 也依赖于此依赖项。</span><span class="sxs-lookup"><span data-stu-id="942d0-183">As a result, NuGet can't determine which `C.dll` to use, but you can't just remove the project's dependency on Package C because Package B also depends on it.</span></span>

<span data-ttu-id="942d0-184">要解决此问题，必须直接引用所需的 `C.dll`（或使用其他引用正确对象的包），然后在包 C 上添加不包括其所有资产的依赖项。</span><span class="sxs-lookup"><span data-stu-id="942d0-184">To resolve this, you must directly reference the `C.dll` you want (or use another package that references the right one), and then add a dependency on Package C that excludes all its assets.</span></span> <span data-ttu-id="942d0-185">此方法如下所示，具体取决于当前使用的包管理格式：</span><span class="sxs-lookup"><span data-stu-id="942d0-185">This is done as follows depending on the package management format in use:</span></span>

- <span data-ttu-id="942d0-186">[PackageReference](../consume-packages/package-references-in-project-files.md)：在依赖项中添加 `ExcludeAssets="All"`：</span><span class="sxs-lookup"><span data-stu-id="942d0-186">[PackageReference](../consume-packages/package-references-in-project-files.md): add `ExcludeAssets="All"` in the dependency:</span></span>

    ```xml
    <PackageReference Include="PackageC" Version="1.0.0" ExcludeAssets="All" />
    ```

- <span data-ttu-id="942d0-187">`packages.config`：从 `.csproj` 文件中删除对 PackageC 的引用，以便它仅引用所需版本的 `C.dll`。</span><span class="sxs-lookup"><span data-stu-id="942d0-187">`packages.config`: remove the reference to PackageC from the `.csproj` file so that it references only the version of `C.dll` that you want.</span></span>
    
## <a name="dependency-updates-during-package-install"></a><span data-ttu-id="942d0-188">在安装包期间更新依赖项</span><span class="sxs-lookup"><span data-stu-id="942d0-188">Dependency updates during package install</span></span> 

<span data-ttu-id="942d0-189">如果依赖项版本已满足，则在其他程序包安装期间不会更新依赖项。</span><span class="sxs-lookup"><span data-stu-id="942d0-189">If a dependency version is already satisfied, the dependency isn't updated during other package installations.</span></span> <span data-ttu-id="942d0-190">例如，假设包 A 依赖于包 B 并且指定版本号 1.0。</span><span class="sxs-lookup"><span data-stu-id="942d0-190">For example, consider package A that depends on package B and specifies 1.0 for the version number.</span></span> <span data-ttu-id="942d0-191">源存储库包含程序包 B 的版本 1.0、1.1 和 1.2。如果将 A 安装在已包含 B 版本 1.0 的项目中，则 B 1.0 将保持使用状态，因为它满足版本限制。</span><span class="sxs-lookup"><span data-stu-id="942d0-191">The source repository contains versions 1.0, 1.1, and 1.2 of package B. If A is installed in a project that already contains B version 1.0, then B 1.0 remains in use because it satisfies the version constraint.</span></span> <span data-ttu-id="942d0-192">但是，如果包 A 请求 1.1 或更高版本的 B，则会安装 B 1.2。</span><span class="sxs-lookup"><span data-stu-id="942d0-192">However, if package A had requests version 1.1 or higher of B, then B 1.2 would be installed.</span></span> 

## <a name="resolving-incompatible-package-errors"></a><span data-ttu-id="942d0-193">解决包不兼容错误</span><span class="sxs-lookup"><span data-stu-id="942d0-193">Resolving incompatible package errors</span></span>

<span data-ttu-id="942d0-194">在包还原操作期间，可能会看到错误“一个或多个包不兼容...”或包与项目的目标框架“不兼容”。</span><span class="sxs-lookup"><span data-stu-id="942d0-194">During a package restore operation, you may see the error "One or more packages are not compatible..." or that a package "is not compatible" with the project's target framework.</span></span>

<span data-ttu-id="942d0-195">如果项目中引用的一个或多个包未指示其支持包的目标框架，则会出现此错误；即，包的 `lib` 文件夹中不包含与此项目兼容的目标框架的适用 DLL。</span><span class="sxs-lookup"><span data-stu-id="942d0-195">This error occurs when one or more of the packages referenced in your project do not indicate that they support the project's target framework; that is, the package does not contain a suitable DLL in its `lib` folder for a target framework that is compatible with the project.</span></span> <span data-ttu-id="942d0-196">（请参阅[目标框架](../reference/target-frameworks.md)获取列表。）</span><span class="sxs-lookup"><span data-stu-id="942d0-196">(See [Target frameworks](../reference/target-frameworks.md) for a list.)</span></span> 

<span data-ttu-id="942d0-197">例如，如果项目面向 `netstandard1.6`，并且你尝试安装仅在 `lib\net20` 和 `\lib\net45` 文件夹中包含 DLL 的包，则将看到类似如下针对包或其依赖项的消息：</span><span class="sxs-lookup"><span data-stu-id="942d0-197">For example, if a project targets `netstandard1.6` and you attempt to install a package that contains DLLs in only the `lib\net20` and `\lib\net45` folders, then you see messages like the following for the package and possibly its dependents:</span></span>

```output
Restoring packages for myproject.csproj...
Package ContosoUtilities 2.1.2.3 is not compatible with netstandard1.6 (.NETStandard,Version=v1.6). Package ContosoUtilities 2.1.2.3 supports:
  - net20 (.NETFramework,Version=v2.0)
  - net45 (.NETFramework,Version=v4.5)
Package ContosoCore 0.86.0 is not compatible with netstandard1.6 (.NETStandard,Version=v1.6). Package ContosoCore 0.86.0 supports:
  - 11 (11,Version=v0.0)
  - net20 (.NETFramework,Version=v2.0)
  - sl3 (Silverlight,Version=v3.0)
  - sl4 (Silverlight,Version=v4.0)
One or more packages are incompatible with .NETStandard,Version=v1.6.
Package restore failed. Rolling back package changes for 'MyProject'.
```

<span data-ttu-id="942d0-198">要解决不兼容问题，请执行下列操作之一：</span><span class="sxs-lookup"><span data-stu-id="942d0-198">To resolve incompatibilities, do one of the following:</span></span>

- <span data-ttu-id="942d0-199">将项目重定向到要使用的包所支持的框架。</span><span class="sxs-lookup"><span data-stu-id="942d0-199">Retarget your project to a framework that is supported by the packages you want to use.</span></span>
- <span data-ttu-id="942d0-200">联系包创建者并与其协作添加对所选框架的支持。</span><span class="sxs-lookup"><span data-stu-id="942d0-200">Contact the author of the packages and work with them to add support for your chosen framework.</span></span> <span data-ttu-id="942d0-201">[nuget.org](https://www.nuget.org/) 中每个列出包的页面均针对此目的提供了“联系所有者”链接  。</span><span class="sxs-lookup"><span data-stu-id="942d0-201">Each package listing page on [nuget.org](https://www.nuget.org/) has a **Contact Owners** link for this purpose.</span></span>
