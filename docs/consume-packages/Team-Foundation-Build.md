---
title: 使用 Team Foundation 生成还原 NuGet 包的演练
description: 演练如何使用 Team Foundation Build（TFS 和 Visual Studio Team Services）还原 NuGet 包。
author: karann-msft
ms.author: karann
ms.date: 01/09/2017
ms.topic: conceptual
ms.openlocfilehash: a86a58f8afb4b0f1affeddd47d6c5606fb465757
ms.sourcegitcommit: 2b50c450cca521681a384aa466ab666679a40213
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/07/2020
ms.locfileid: "73611005"
---
# <a name="setting-up-package-restore-with-team-foundation-build"></a><span data-ttu-id="1af12-103">使用 Team Foundation Build 设置包还原</span><span class="sxs-lookup"><span data-stu-id="1af12-103">Setting up package restore with Team Foundation Build</span></span>

<span data-ttu-id="1af12-104">本文提供详细的演练：演示如何将包作为 [Team Services 生成](/vsts/build-release/index) 的一部分还原包，以实现 Git 和 Team Services 版本控制。</span><span class="sxs-lookup"><span data-stu-id="1af12-104">This article provides a detailed walkthrough on how to restore packages as part of the [Team Services Build](/vsts/build-release/index) both, for both Git and Team Services Version Control.</span></span>

<span data-ttu-id="1af12-105">虽然此演练针对使用 Visual Studio Team Services 的方案，但这些概念也适用于其他版本控制和生成系统。</span><span class="sxs-lookup"><span data-stu-id="1af12-105">Although this walkthrough is specific for the scenario of using Visual Studio Team Services, the concepts also apply to other version control and build systems.</span></span>

<span data-ttu-id="1af12-106">适用于：</span><span class="sxs-lookup"><span data-stu-id="1af12-106">Applies To:</span></span>

- <span data-ttu-id="1af12-107">在 TFS 任意版本上运行的自定义 MSBuild 项目</span><span class="sxs-lookup"><span data-stu-id="1af12-107">Custom MSBuild projects running on any version of TFS</span></span>
- <span data-ttu-id="1af12-108">Team Foundation Server 2012 或更早版本</span><span class="sxs-lookup"><span data-stu-id="1af12-108">Team Foundation Server 2012 or earlier</span></span>
- <span data-ttu-id="1af12-109">迁移到 TFS 2013 或更高版本的自定义 Team Foundation Build 过程模板</span><span class="sxs-lookup"><span data-stu-id="1af12-109">Custom Team Foundation Build Process Templates migrated to TFS 2013 or later</span></span>
- <span data-ttu-id="1af12-110">删除了 Nuget 还原功能的生成过程模板</span><span class="sxs-lookup"><span data-stu-id="1af12-110">Build Process Templates With Nuget Restore functionality removed</span></span>

<span data-ttu-id="1af12-111">如果使用 Visual Studio Team Services 或 Team Foundation Server 2013 及其生成过程模板，则将在生成过程中进行自动包还原。</span><span class="sxs-lookup"><span data-stu-id="1af12-111">If you're using Visual Studio Team Services or Team Foundation Server 2013 with its build process templates, automatic package restore happens as part of the build process.</span></span>

## <a name="the-general-approach"></a><span data-ttu-id="1af12-112">常规方法</span><span class="sxs-lookup"><span data-stu-id="1af12-112">The general approach</span></span>

<span data-ttu-id="1af12-113">使用 NuGet 的优点是可以用它来避免将二进制文件签入到版本控制系统。</span><span class="sxs-lookup"><span data-stu-id="1af12-113">An advantage of using NuGet is that you can use it to avoid checking in binaries to your version control system.</span></span>

<span data-ttu-id="1af12-114">如果使用[分布式版本控制](https://en.wikipedia.org/wiki/Distributed_revision_control)系统（例如 git），这会变得特别有趣，因为开发人员需要先克隆整个存储库（包括完整历史记录），才能在本地开始工作。</span><span class="sxs-lookup"><span data-stu-id="1af12-114">This is especially interesting if you are using a [distributed version control](https://en.wikipedia.org/wiki/Distributed_revision_control) system like git because developers need to clone the entire repository, including the full history, before they can start working locally.</span></span> <span data-ttu-id="1af12-115">签入二进制文件可能导致明显的存储库膨胀，因为二进制文件的存储通常不需要增量压缩。</span><span class="sxs-lookup"><span data-stu-id="1af12-115">Checking in binaries can cause significant repository bloat as binary files are typically stored without delta compression.</span></span>

<span data-ttu-id="1af12-116">NuGet 支持在生成过程中[还原包](../consume-packages/package-restore.md)，这种状态已经持续了一段较长的时间。</span><span class="sxs-lookup"><span data-stu-id="1af12-116">NuGet has supported [restoring packages](../consume-packages/package-restore.md) as part of the build for a long time now.</span></span> <span data-ttu-id="1af12-117">以前的实现对于想要扩展生成过程的包而言存在难分先后的问题，因为 NuGet 在生成项目的同时还原包。</span><span class="sxs-lookup"><span data-stu-id="1af12-117">The previous implementation had a chicken-and-egg problem for packages that want to extend the build process because NuGet restored packages while building the project.</span></span> <span data-ttu-id="1af12-118">但是，MSBuild 不允许在生成期间扩展生成；有人可能会说这是 MSBuild 的问题，但我认为这是一个固有问题。</span><span class="sxs-lookup"><span data-stu-id="1af12-118">However, MSBuild doesn't allow extending the build during the build; one could argue that this an issue in MSBuild but I would argue that this is an inherent problem.</span></span> <span data-ttu-id="1af12-119">根据需要扩展的特性，在还原包时才注册可能已经太迟。</span><span class="sxs-lookup"><span data-stu-id="1af12-119">Depending on which aspect you need to extend it might be too late to register by the time your package is restored.</span></span>

<span data-ttu-id="1af12-120">解决此问题的方法是确保在生成过程中的第一步还原包：</span><span class="sxs-lookup"><span data-stu-id="1af12-120">The cure to this problem is making sure that packages are restored as the first step in the build process:</span></span>

```cli
nuget restore path\to\solution.sln
```

<span data-ttu-id="1af12-121">当你的生成过程在生成代码前还原包时，不再需要签入 `.targets` 文件</span><span class="sxs-lookup"><span data-stu-id="1af12-121">When your build process restores packages before building the code, you don't need to check-in `.targets` files</span></span>

> [!Note]
> <span data-ttu-id="1af12-122">包必须创作为允许在 Visual Studio 中加载。</span><span class="sxs-lookup"><span data-stu-id="1af12-122">Packages must be authored to allow loading in Visual Studio.</span></span> <span data-ttu-id="1af12-123">否则，可能还是需要签入 `.targets` 文件，以便其他开发人员直接打开解决方案，而无需先还原包。</span><span class="sxs-lookup"><span data-stu-id="1af12-123">Otherwise, you may still want to check in `.targets` files so that other developers can simply open the solution without having to restore packages first.</span></span>

<span data-ttu-id="1af12-124">以下演示项目演示如何在不需要签入 `packages` 文件夹和 `.targets` 文件的情况下设置生成。</span><span class="sxs-lookup"><span data-stu-id="1af12-124">The following demo project shows how to set up the build in such a way that the `packages` folders and `.targets` files don't need to be checked-in.</span></span> <span data-ttu-id="1af12-125">它还演示如何在 Team Foundation Service 上为此示例项目设置自动化生成。</span><span class="sxs-lookup"><span data-stu-id="1af12-125">It also shows how to set up an automated build on the Team Foundation Service for this sample project.</span></span>

## <a name="repository-structure"></a><span data-ttu-id="1af12-126">存储库结构</span><span class="sxs-lookup"><span data-stu-id="1af12-126">Repository structure</span></span>

<span data-ttu-id="1af12-127">演示项目是一个使用命令行参数来查询必应的简单命令行工具。</span><span class="sxs-lookup"><span data-stu-id="1af12-127">Our demo project is a simple command line tool that uses the command line argument to query Bing.</span></span> <span data-ttu-id="1af12-128">它面向 .NET Framework 4 并使用多种 [BCL 包](https://www.nuget.org/profiles/dotnetframework/)（[Microsoft.Net.Http](https://www.nuget.org/packages/Microsoft.Net.Http)、[Microsoft.Bcl](https://www.nuget.org/packages/Microsoft.Bcl)、[Microsoft.Bcl.Async](https://www.nuget.org/packages/Microsoft.Bcl.Async) 和 [Microsoft.Bcl.Build](https://www.nuget.org/packages/Microsoft.Bcl.Build)）。</span><span class="sxs-lookup"><span data-stu-id="1af12-128">It targets the .NET Framework 4 and uses many of the [BCL packages](https://www.nuget.org/profiles/dotnetframework/) ([Microsoft.Net.Http](https://www.nuget.org/packages/Microsoft.Net.Http), [Microsoft.Bcl](https://www.nuget.org/packages/Microsoft.Bcl), [Microsoft.Bcl.Async](https://www.nuget.org/packages/Microsoft.Bcl.Async), and [Microsoft.Bcl.Build](https://www.nuget.org/packages/Microsoft.Bcl.Build)).</span></span>

<span data-ttu-id="1af12-129">存储库结构如下所示：</span><span class="sxs-lookup"><span data-stu-id="1af12-129">The structure of the repository looks as follows:</span></span>

    <Project>
        │   .gitignore
        │   .tfignore
        │   build.proj
        │
        ├───src
        │   │   BingSearcher.sln
        │   │
        │   └───BingSearcher
        │       │   App.config
        │       │   BingSearcher.csproj
        │       │   packages.config
        │       │   Program.cs
        │       │
        │       └───Properties
        │               AssemblyInfo.cs
        │
        └───tools
            └───NuGet
                    nuget.exe

<span data-ttu-id="1af12-130">可以看见我们既未签入 `packages` 文件夹，也未签入任何 `.targets` 文件。</span><span class="sxs-lookup"><span data-stu-id="1af12-130">You can see that we haven't checked-in the `packages` folder nor any `.targets` files.</span></span>

<span data-ttu-id="1af12-131">但我们签入了 `nuget.exe`，因为生成过程中需要它。</span><span class="sxs-lookup"><span data-stu-id="1af12-131">We have, however, checked-in the `nuget.exe` as it's needed during the build.</span></span> <span data-ttu-id="1af12-132">我们遵循广泛使用的约定，在共享的 `tools` 文件夹中签入它。</span><span class="sxs-lookup"><span data-stu-id="1af12-132">Following widely used conventions we've checked it in under a shared `tools` folder.</span></span>

<span data-ttu-id="1af12-133">源代码位于 `src` 文件夹下。</span><span class="sxs-lookup"><span data-stu-id="1af12-133">The source code is under the `src` folder.</span></span> <span data-ttu-id="1af12-134">虽然我们的演示仅使用单个解决方案，但是不难想象此文件夹包含不止一个解决方案。</span><span class="sxs-lookup"><span data-stu-id="1af12-134">Although our demo only uses a single solution, you can easily imagine that this folder contains more than one solution.</span></span>

### <a name="ignore-files"></a><span data-ttu-id="1af12-135">忽略文件</span><span class="sxs-lookup"><span data-stu-id="1af12-135">Ignore files</span></span>

> [!Note]
> <span data-ttu-id="1af12-136">[NuGet 客户端当前存在一个已知 bug](https://nuget.codeplex.com/workitem/4072)，它导致客户端依然将 `packages` 文件夹添加到版本控制。</span><span class="sxs-lookup"><span data-stu-id="1af12-136">There is currently a [known bug in the NuGet client](https://nuget.codeplex.com/workitem/4072) that causes the client to still add the `packages` folder to version control.</span></span> <span data-ttu-id="1af12-137">一种解决方法是禁用源代码管理集成。</span><span class="sxs-lookup"><span data-stu-id="1af12-137">A workaround is to disable the source control integration.</span></span> <span data-ttu-id="1af12-138">为了做到这一点，与解决方案并行的 `.nuget` 文件夹中需要一个 `Nuget.Config ` 文件。</span><span class="sxs-lookup"><span data-stu-id="1af12-138">In order to do that, you need a `Nuget.Config ` file in the  `.nuget` folder that is parallel to your solution.</span></span> <span data-ttu-id="1af12-139">如果此文件夹尚不存在，请先创建一个。</span><span class="sxs-lookup"><span data-stu-id="1af12-139">If this folder doesn't exist yet, you need to create it.</span></span> <span data-ttu-id="1af12-140">在 [`Nuget.Config`](../consume-packages/configuring-nuget-behavior.md) 中，添加以下内容：</span><span class="sxs-lookup"><span data-stu-id="1af12-140">In [`Nuget.Config`](../consume-packages/configuring-nuget-behavior.md), add the following content:</span></span>

```xml
<configuration>
    <solution>
        <add key="disableSourceControlIntegration" value="true" />
    </solution>
</configuration>
```

<span data-ttu-id="1af12-141">为了与不希望签入**包**文件夹的版本控制进行通信，我们还为 git (`.gitignore`) 和 TF 版本控制 (`.tfignore`) 添加了忽略文件。</span><span class="sxs-lookup"><span data-stu-id="1af12-141">To communicate to version control that we don’t intent to check-in the **packages** folders, we've also added ignore files for both git (`.gitignore`) as well as TF version control (`.tfignore`).</span></span> <span data-ttu-id="1af12-142">这些文件描述不希望签入的文件模式。</span><span class="sxs-lookup"><span data-stu-id="1af12-142">These files describe patterns of files you don't want to check-in.</span></span>

<span data-ttu-id="1af12-143">`.gitignore` 文件如下所示：</span><span class="sxs-lookup"><span data-stu-id="1af12-143">The `.gitignore` file looks as follows:</span></span>

    syntax: glob
    *.user
    *.suo
    bin
    obj
    packages
    *.nupkg
    project.lock.json
    project.assets.json

<span data-ttu-id="1af12-144">`.gitignore` 文件[非常强大](https://www.kernel.org/pub/software/scm/git/docs/gitignore.html)。</span><span class="sxs-lookup"><span data-stu-id="1af12-144">The `.gitignore` file is [quite powerful](https://www.kernel.org/pub/software/scm/git/docs/gitignore.html).</span></span> <span data-ttu-id="1af12-145">例如，如果需要通常情况下不签入 `packages` 文件夹的内容，但需要遵循之前有关签入 `.targets` 文件的指南，则可以替换为以下规则：</span><span class="sxs-lookup"><span data-stu-id="1af12-145">For example, if you want to generally not check-in the contents of the `packages` folder but want to go with previous guidance of checking in the `.targets` files you could have the following rule instead:</span></span>

    packages
    !packages/**/*.targets

<span data-ttu-id="1af12-146">这将排除所有 `packages` 文件夹，但会重新包含所有包含的 `.targets` 文件。</span><span class="sxs-lookup"><span data-stu-id="1af12-146">This will exclude all `packages` folders but will re-include all contained `.targets` files.</span></span> <span data-ttu-id="1af12-147">顺便说一下，可以[在此](https://github.com/github/gitignore/blob/master/VisualStudio.gitignore)找到专门针对 Visual Studio 开发人员需求定制的 `.gitignore` 文件模板。</span><span class="sxs-lookup"><span data-stu-id="1af12-147">By the way, you can find a template for `.gitignore` files that is specifically tailored for the needs of Visual Studio developers [here](https://github.com/github/gitignore/blob/master/VisualStudio.gitignore).</span></span>

<span data-ttu-id="1af12-148">TF 版本控制通过 [.tfignore](/vsts/tfvc/add-files-server#customize-which-files-are-ignored-by-version-control) 文件支持相似的机制。</span><span class="sxs-lookup"><span data-stu-id="1af12-148">TF version control supports a very similar mechanism via the [.tfignore](/vsts/tfvc/add-files-server#customize-which-files-are-ignored-by-version-control) file.</span></span> <span data-ttu-id="1af12-149">语法几乎是相同的：</span><span class="sxs-lookup"><span data-stu-id="1af12-149">The syntax is virtually the same:</span></span>

    *.user
    *.suo
    bin
    obj
    packages
    *.nupkg
    project.lock.json
    project.assets.json

## <a name="buildproj"></a><span data-ttu-id="1af12-150">build.proj</span><span class="sxs-lookup"><span data-stu-id="1af12-150">build.proj</span></span>

<span data-ttu-id="1af12-151">为进行演示，我们将生成过程控制到相当简单。</span><span class="sxs-lookup"><span data-stu-id="1af12-151">For our demo, we keep the build process fairly simple.</span></span> <span data-ttu-id="1af12-152">我们将创建一个 MSBuild 项目来生成所有包，同时确保在生成解决方案之前还原包。</span><span class="sxs-lookup"><span data-stu-id="1af12-152">We'll create an MSBuild project that builds all solutions while making sure that packages are restored before building the solutions.</span></span>

<span data-ttu-id="1af12-153">此项目将有三个常规目标（`Clean`、`Build` 和 `Rebuild`），以及一个新目标 `RestorePackages`。</span><span class="sxs-lookup"><span data-stu-id="1af12-153">This project will have the three conventional targets `Clean`, `Build` and `Rebuild` as well as a new target `RestorePackages`.</span></span>

- <span data-ttu-id="1af12-154">`Build` 和 `Rebuild` 目标均依赖于 `RestorePackages`。</span><span class="sxs-lookup"><span data-stu-id="1af12-154">The `Build` and `Rebuild` targets both depend on `RestorePackages`.</span></span> <span data-ttu-id="1af12-155">这将确保你可以运行 `Build` 和 `Rebuild`，并依赖于要还原的包。</span><span class="sxs-lookup"><span data-stu-id="1af12-155">This makes sure that you can both run `Build` and `Rebuild` and rely on packages being restored.</span></span>
- <span data-ttu-id="1af12-156">`Clean`、`Build` 和 `Rebuild` 调用所有解决方案文件上的相应 MSBuild 目标。</span><span class="sxs-lookup"><span data-stu-id="1af12-156">`Clean`, `Build` and `Rebuild` invoke the corresponding MSBuild target on all solution files.</span></span>
- <span data-ttu-id="1af12-157">`RestorePackages` 目标调用每个解决方案文件的 `nuget.exe`。</span><span class="sxs-lookup"><span data-stu-id="1af12-157">The `RestorePackages` target invokes `nuget.exe` for each solution file.</span></span> <span data-ttu-id="1af12-158">这通过使用 [MSBuild 批处理功能](/visualstudio/msbuild/msbuild-batching)完成。</span><span class="sxs-lookup"><span data-stu-id="1af12-158">This is accomplished by using [MSBuild's batching functionality](/visualstudio/msbuild/msbuild-batching).</span></span>

<span data-ttu-id="1af12-159">结果如下所示：</span><span class="sxs-lookup"><span data-stu-id="1af12-159">The result looks as follows:</span></span>

```xml
<?xml version="1.0" encoding="utf-8"?>
<Project ToolsVersion="4.0"
            DefaultTargets="Build"
            xmlns="http://schemas.microsoft.com/developer/msbuild/2003">

    <PropertyGroup>
    <OutDir Condition=" '$(OutDir)'=='' ">$(MSBuildThisFileDirectory)bin\</OutDir>
    <Configuration Condition=" '$(Configuration)'=='' ">Release</Configuration>
    <SourceHome Condition=" '$(SourceHome)'=='' ">$(MSBuildThisFileDirectory)src\</SourceHome>
    <ToolsHome Condition=" '$(ToolsHome)'=='' ">$(MSBuildThisFileDirectory)tools\</ToolsHome>
    </PropertyGroup>

    <ItemGroup>
    <Solution Include="$(SourceHome)*.sln">
        <AdditionalProperties>OutDir=$(OutDir);Configuration=$(Configuration)</AdditionalProperties>
    </Solution>
    </ItemGroup>

    <Target Name="RestorePackages">
    <Exec Command="&quot;$(ToolsHome)NuGet\nuget.exe&quot; restore &quot;%(Solution.Identity)&quot;" />
    </Target>

    <Target Name="Clean">
    <MSBuild Targets="Clean"
                Projects="@(Solution)" />
    </Target>

    <Target Name="Build" DependsOnTargets="RestorePackages">
    <MSBuild Targets="Build"
                Projects="@(Solution)" />
    </Target>

    <Target Name="Rebuild" DependsOnTargets="RestorePackages">
    <MSBuild Targets="Rebuild"
                Projects="@(Solution)" />
    </Target>
</Project>
```

## <a name="configuring-team-build"></a><span data-ttu-id="1af12-160">配置 Team Build</span><span class="sxs-lookup"><span data-stu-id="1af12-160">Configuring Team Build</span></span>

<span data-ttu-id="1af12-161">Team Build 提供不同的过程模板。</span><span class="sxs-lookup"><span data-stu-id="1af12-161">Team Build offers various process templates.</span></span> <span data-ttu-id="1af12-162">我们使用 Team Foundation Service 进行本演示。</span><span class="sxs-lookup"><span data-stu-id="1af12-162">For this demonstration, we're using the Team Foundation Service.</span></span> <span data-ttu-id="1af12-163">但 TFS 的本地安装将非常相似。</span><span class="sxs-lookup"><span data-stu-id="1af12-163">On-premises installations of TFS will be very similar though.</span></span>

<span data-ttu-id="1af12-164">Git 和 TF 版本控制有不同的 Team Build 模板，因此以下步骤将随着使用的版本控制系统变化。</span><span class="sxs-lookup"><span data-stu-id="1af12-164">Git and TF Version Control have different Team Build templates, so the following steps will vary depending on which version control system you are using.</span></span> <span data-ttu-id="1af12-165">在这两种情况下，只需选择 build.proj 作为需要生成的项目。</span><span class="sxs-lookup"><span data-stu-id="1af12-165">In both cases, all you need is selecting the build.proj as the project you want to build.</span></span>

<span data-ttu-id="1af12-166">我们先来看看适用于 git 的过程模板。</span><span class="sxs-lookup"><span data-stu-id="1af12-166">First, let's look at the process template for git.</span></span> <span data-ttu-id="1af12-167">在基于 git 的模板中，通过 `Solution to build` 属性选择生成：</span><span class="sxs-lookup"><span data-stu-id="1af12-167">In the git based template the build is selected via the property `Solution to build`:</span></span>

![适用于 git 的生成过程](media/PackageRestoreTeamBuildGit.png)

<span data-ttu-id="1af12-169">请注意，此属性是在存储库中的一个位置。</span><span class="sxs-lookup"><span data-stu-id="1af12-169">Please note that this property is a location in your repository.</span></span> <span data-ttu-id="1af12-170">由于 `build.proj` 位于根目录中，因此只需使用 `build.proj`。</span><span class="sxs-lookup"><span data-stu-id="1af12-170">Since our `build.proj` is in the root, we simply used `build.proj`.</span></span> <span data-ttu-id="1af12-171">如果将生成文件放在名为 `tools` 的文件夹下，该值将为 `tools\build.proj`。</span><span class="sxs-lookup"><span data-stu-id="1af12-171">If you place the build file under a folder called `tools`, the value would be `tools\build.proj`.</span></span>

<span data-ttu-id="1af12-172">在 TF 版本控制模板中，通过 `Projects` 属性选择项目：</span><span class="sxs-lookup"><span data-stu-id="1af12-172">In the TF version control template the project is selected via the property `Projects`:</span></span>

![适用于 TFVC 的生成过程](media/PackageRestoreTeamBuildTFVC.png)

<span data-ttu-id="1af12-174">与基于 git 的模板不同，TF 版本控制支持选取器（右侧带三个点的按钮）。</span><span class="sxs-lookup"><span data-stu-id="1af12-174">In contrast to the git based template the TF version control supports pickers (the button on the right hand side with the three dots).</span></span> <span data-ttu-id="1af12-175">因此，我们建议使用它们来选择项目，以避免任何键入错误。</span><span class="sxs-lookup"><span data-stu-id="1af12-175">So in order to avoid any typing errors we suggest you use them to select the project.</span></span>
