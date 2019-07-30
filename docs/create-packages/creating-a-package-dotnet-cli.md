---
title: 使用 dotnet CLI 创建 NuGet 包
description: 设计和创建 NuGet 包流程的详细指南，包含文件和版本控制等关键决策点。
author: karann-msft
ms.author: karann
ms.date: 07/09/2019
ms.topic: conceptual
ms.openlocfilehash: da5dbc8b1659cef66e8439b9a3c3bb2c9205cbe6
ms.sourcegitcommit: f291ff91561a6b58c2aec41c624d798e00ce41fa
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/24/2019
ms.locfileid: "68462458"
---
# <a name="create-a-nuget-package-using-the-dotnet-cli"></a><span data-ttu-id="7ae2e-103">使用 dotnet CLI 创建 NuGet 包</span><span class="sxs-lookup"><span data-stu-id="7ae2e-103">Create a NuGet package using the dotnet CLI</span></span>

<span data-ttu-id="7ae2e-104">无论包是什么用途或者它包含什么代码，均使用其中一个 CLI 工具（`nuget.exe` 或 `dotnet.exe`）将该功能打包进可以与任意数量的其他开发人员共享且可以由其使用的组件中。</span><span class="sxs-lookup"><span data-stu-id="7ae2e-104">No matter what your package does or what code it contains, you use one of the CLI tools, either `nuget.exe` or `dotnet.exe`, to package that functionality into a component that can be shared with and used by any number of other developers.</span></span> <span data-ttu-id="7ae2e-105">本文介绍如何使用 dotnet CLI 创建包。</span><span class="sxs-lookup"><span data-stu-id="7ae2e-105">This article describes how to create a package using the dotnet CLI.</span></span> <span data-ttu-id="7ae2e-106">若要安装 `dotnet` CLI，请参阅[安装 NuGet 客户端工具](../install-nuget-client-tools.md)。</span><span class="sxs-lookup"><span data-stu-id="7ae2e-106">To install the `dotnet` CLI, see [Install NuGet client tools](../install-nuget-client-tools.md).</span></span> <span data-ttu-id="7ae2e-107">从 Visual Studio 2017 开始，dotnet CLI 包含在 .NET Core 工作负载中。</span><span class="sxs-lookup"><span data-stu-id="7ae2e-107">Starting in Visual Studio 2017, the dotnet CLI is included with .NET Core workloads.</span></span>

<span data-ttu-id="7ae2e-108">对于使用 [SDK 样式格式](../resources/check-project-format.md)的 .NET Core 和 .NET Standard 项目，以及任何其他 SDK 样式项目，NuGet 直接使用项目文件中的信息创建包。</span><span class="sxs-lookup"><span data-stu-id="7ae2e-108">For .NET Core and .NET Standard projects that use the [SDK-style format](../resources/check-project-format.md), and any other SDK-style projects, NuGet uses information in the project file directly to create a package.</span></span> <span data-ttu-id="7ae2e-109">若要查看分步教程，请参阅[使用 dotnet CLI 创建 .NET Standard 包](../quickstart/create-and-publish-a-package-using-the-dotnet-cli.md)和[使用 Visual Studio 创建 .NET Standard 包](../quickstart/create-and-publish-a-package-using-visual-studio.md)。</span><span class="sxs-lookup"><span data-stu-id="7ae2e-109">For step-by-step tutorials, see [Create .NET Standard Packages with dotnet CLI](../quickstart/create-and-publish-a-package-using-the-dotnet-cli.md), [Create .NET Standard Packages with Visual Studio](../quickstart/create-and-publish-a-package-using-visual-studio.md).</span></span>

<span data-ttu-id="7ae2e-110">`msbuild -t:pack` 在功能上等效于 `dotnet pack`。</span><span class="sxs-lookup"><span data-stu-id="7ae2e-110">`msbuild -t:pack` is functionality equivalent to `dotnet pack`.</span></span> <span data-ttu-id="7ae2e-111">若要用 MSBuild 进行生成，概念与本文中所述的概念相同，但命令行命令略有不同。</span><span class="sxs-lookup"><span data-stu-id="7ae2e-111">To build with MSBuild, the concepts are the same as described in this article, but the command line commands are slightly different.</span></span> <span data-ttu-id="7ae2e-112">同样，对于非 SDK 样式的项目和 `<PackageReference>`，可以使用 `msbuild /t:pack`。</span><span class="sxs-lookup"><span data-stu-id="7ae2e-112">Similarly, with a non-SDK-style project and `<PackageReference>`, you can use `msbuild /t:pack`.</span></span> <span data-ttu-id="7ae2e-113">在这些情况下，需要将 NuGet.Build.Tasks.Pack 包添加到其依赖项。</span><span class="sxs-lookup"><span data-stu-id="7ae2e-113">In these scenarios, you need to add the NuGet.Build.Tasks.Pack package to their dependencies.</span></span> <span data-ttu-id="7ae2e-114">请参阅[作为 MSBuild 目标的 NuGet 包和还原](../reference/msbuild-targets.md)。</span><span class="sxs-lookup"><span data-stu-id="7ae2e-114">See [NuGet pack and restore as MSBuild targets](../reference/msbuild-targets.md).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="7ae2e-115">本主题适用于 [ SDK 样式](../resources/check-project-format.md)的项目，通常是 .NET Core 和 .NET Standard 项目。</span><span class="sxs-lookup"><span data-stu-id="7ae2e-115">This topic applies to [SDK-style](../resources/check-project-format.md) projects, typically .NET Core and .NET Standard projects.</span></span>

## <a name="set-properties"></a><span data-ttu-id="7ae2e-116">设置属性</span><span class="sxs-lookup"><span data-stu-id="7ae2e-116">Set properties</span></span>

<span data-ttu-id="7ae2e-117">创建包需要以下属性。</span><span class="sxs-lookup"><span data-stu-id="7ae2e-117">The following properties are required to create a package.</span></span>

- <span data-ttu-id="7ae2e-118">`PackageId`，包标识符，在托管包的库中必须是唯一的。</span><span class="sxs-lookup"><span data-stu-id="7ae2e-118">`PackageId`, the package identifier, which must be unique across the gallery that hosts the package.</span></span> <span data-ttu-id="7ae2e-119">如果未指定，默认值为 `AssemblyName`。</span><span class="sxs-lookup"><span data-stu-id="7ae2e-119">If not specified, the default value is `AssemblyName`.</span></span>
- <span data-ttu-id="7ae2e-120">`Version`，窗体 Major.Minor.Patch[-Suffix] 中特定的版本号，其中 -Suffix 标识[预发布版本](prerelease-packages.md)   。</span><span class="sxs-lookup"><span data-stu-id="7ae2e-120">`Version`, a specific version number in the form *Major.Minor.Patch[-Suffix]* where *-Suffix* identifies [pre-release versions](prerelease-packages.md).</span></span> <span data-ttu-id="7ae2e-121">如果未指定，默认值为 1.0.0。</span><span class="sxs-lookup"><span data-stu-id="7ae2e-121">If not specified, the default value is 1.0.0.</span></span>
- <span data-ttu-id="7ae2e-122">包标题应出现在主机上（例如 nuget.org）</span><span class="sxs-lookup"><span data-stu-id="7ae2e-122">The package title as it should appear on the host (like nuget.org)</span></span>
- <span data-ttu-id="7ae2e-123">`Authors`，作者和所有者信息。</span><span class="sxs-lookup"><span data-stu-id="7ae2e-123">`Authors`, author and owner information.</span></span> <span data-ttu-id="7ae2e-124">如果未指定，默认值为 `AssemblyName`。</span><span class="sxs-lookup"><span data-stu-id="7ae2e-124">If not specified, the default value is `AssemblyName`.</span></span>
- <span data-ttu-id="7ae2e-125">`Company`，公司名称。</span><span class="sxs-lookup"><span data-stu-id="7ae2e-125">`Company`, your company name.</span></span> <span data-ttu-id="7ae2e-126">如果未指定，默认值为 `AssemblyName`。</span><span class="sxs-lookup"><span data-stu-id="7ae2e-126">If not specified, the default value is `AssemblyName`.</span></span>

<span data-ttu-id="7ae2e-127">在 Visual Studio 中，可以在项目属性中设置这些值（在解决方案资源管理器中右键单击项目，选择“属性”  ，然后选择“包”  选项卡）。</span><span class="sxs-lookup"><span data-stu-id="7ae2e-127">In Visual Studio, you can set these values in the project properties (right-click the project in Solution Explorer, choose **Properties**, and select the **Package** tab).</span></span> <span data-ttu-id="7ae2e-128">也可以直接在项目文件 (`.csproj`) 中设置这些属性。</span><span class="sxs-lookup"><span data-stu-id="7ae2e-128">You can also set these properties directly in the project files (`.csproj`).</span></span>

    ```xml
    <PropertyGroup>
      ...
      <PackageId>AppLogger</PackageId>
      <Version>1.0.0</Version>
      <Authors>your_name</Authors>
      <Company>your_company</Company>
    </PropertyGroup>
    ```

> [!Important]
> <span data-ttu-id="7ae2e-129">为包提供一个在 nuget.org 中唯一或你使用的任何包资源的标识符。</span><span class="sxs-lookup"><span data-stu-id="7ae2e-129">Give the package an identifier that's unique across nuget.org or whatever package source you're using.</span></span>

<span data-ttu-id="7ae2e-130">另外，还可以设置可选属性，例如 `Title`、`PackageDescription` 和 `PackageTags`，如 [MSBuild 包目标](../reference/msbuild-targets.md#pack-target)、[控制依赖项资产](../consume-packages/package-references-in-project-files.md#controlling-dependency-assets)和 [NuGet 元数据属性](/dotnet/core/tools/csproj#nuget-metadata-properties)中所述。</span><span class="sxs-lookup"><span data-stu-id="7ae2e-130">You can also set the optional properties, such as `Title`, `PackageDescription`, and `PackageTags`, as described in [MSBuild pack targets](../reference/msbuild-targets.md#pack-target), [Controlling dependency assets](../consume-packages/package-references-in-project-files.md#controlling-dependency-assets), and [NuGet metadata properties](/dotnet/core/tools/csproj#nuget-metadata-properties).</span></span>

> [!NOTE]
> <span data-ttu-id="7ae2e-131">对于面向公共使用而生成的包，请特别注意 **PackageTags** 属性，因为这些标记可帮助其他人查找包并了解其用途。</span><span class="sxs-lookup"><span data-stu-id="7ae2e-131">For packages built for public consumption, pay special attention to the **PackageTags** property, as tags help others find your package and understand what it does.</span></span>

<span data-ttu-id="7ae2e-132">有关声明依赖项并指定版本号的详细信息，请参阅[包版本控制](../reference/package-versioning.md)。</span><span class="sxs-lookup"><span data-stu-id="7ae2e-132">For details on declaring dependencies and specifying version numbers, see [Package versioning](../reference/package-versioning.md).</span></span> <span data-ttu-id="7ae2e-133">还可以使用 `<IncludeAssets>` 和 `<ExcludeAssets>` 特性直接在包中呈现依赖项的资产。</span><span class="sxs-lookup"><span data-stu-id="7ae2e-133">It is also possible to surface assets from dependencies directly in the package by using the `<IncludeAssets>` and `<ExcludeAssets>` attributes.</span></span> <span data-ttu-id="7ae2e-134">有关详细信息，请参阅[控制依赖项资产](../consume-packages/package-references-in-project-files.md#controlling-dependency-assets)。</span><span class="sxs-lookup"><span data-stu-id="7ae2e-134">For more information, seee [Controlling dependency assets](../consume-packages/package-references-in-project-files.md#controlling-dependency-assets).</span></span>

## <a name="choose-a-unique-package-identifier-and-set-the-version-number"></a><span data-ttu-id="7ae2e-135">选择唯一的包标识符并设置版本号</span><span class="sxs-lookup"><span data-stu-id="7ae2e-135">Choose a unique package identifier and set the version number</span></span>

<span data-ttu-id="7ae2e-136">包标识符和版本号是项目中最重要的两个值，因为它们唯一标识包中包含的确切代码。</span><span class="sxs-lookup"><span data-stu-id="7ae2e-136">The package identifier and the version number are the two most important values in the project because they uniquely identify the exact code that's contained in the package.</span></span>

<span data-ttu-id="7ae2e-137">**针对包标识符的最佳做法：**</span><span class="sxs-lookup"><span data-stu-id="7ae2e-137">**Best practices for the package identifier:**</span></span>

- <span data-ttu-id="7ae2e-138">**唯一性**：标识符必须在 nuget.org 或托管包的任意库中是唯一的。</span><span class="sxs-lookup"><span data-stu-id="7ae2e-138">**Uniqueness**: The identifier must be unique across nuget.org or whatever gallery hosts the package.</span></span> <span data-ttu-id="7ae2e-139">确定标识符之前，请搜索适用库以检查该名称是否已使用。</span><span class="sxs-lookup"><span data-stu-id="7ae2e-139">Before deciding on an identifier, search the applicable gallery to check if the name is already in use.</span></span> <span data-ttu-id="7ae2e-140">为了避免冲突，最好使用公司名作为标识符的第一部分（例如 `Contoso.`）。</span><span class="sxs-lookup"><span data-stu-id="7ae2e-140">To avoid conflicts, a good pattern is to use your company name as the first part of the identifier, such as `Contoso.`.</span></span>
- <span data-ttu-id="7ae2e-141">**类似于命名空间的名称**：遵循类似于 .NET 中命名空间的模式，使用点表示法（而不是连字符）。</span><span class="sxs-lookup"><span data-stu-id="7ae2e-141">**Namespace-like names**: Follow a pattern similar to namespaces in .NET, using dot notation instead of hyphens.</span></span> <span data-ttu-id="7ae2e-142">例如，使用 `Contoso.Utility.UsefulStuff` 而不是 `Contoso-Utility-UsefulStuff` 或 `Contoso_Utility_UsefulStuff`。</span><span class="sxs-lookup"><span data-stu-id="7ae2e-142">For example, use `Contoso.Utility.UsefulStuff` rather than `Contoso-Utility-UsefulStuff` or `Contoso_Utility_UsefulStuff`.</span></span> <span data-ttu-id="7ae2e-143">当包标识符与代码中使用的命名空间相匹配时，这个方法也很有用。</span><span class="sxs-lookup"><span data-stu-id="7ae2e-143">Consumers also find it helpful when the package identifier matches the namespaces used in the code.</span></span>
- <span data-ttu-id="7ae2e-144">**示例包**：如果生成展示如何使用另一个包的示例代码包，请附加 `.Sample` 作为标识符的后缀，就像 `Contoso.Utility.UsefulStuff.Sample` 中一样。</span><span class="sxs-lookup"><span data-stu-id="7ae2e-144">**Sample Packages**: If you produce a package of sample code that demonstrates how to use another package, attach `.Sample` as a suffix to the identifier, as in `Contoso.Utility.UsefulStuff.Sample`.</span></span> <span data-ttu-id="7ae2e-145">（当然，示例包会在其他包上有依赖项。）创建示例包时，请在 `<IncludeAssets>` 中使用 `contentFiles` 值。</span><span class="sxs-lookup"><span data-stu-id="7ae2e-145">(The sample package would of course have a dependency on the other package.) When creating a sample package, use the `contentFiles` value in `<IncludeAssets>`.</span></span> <span data-ttu-id="7ae2e-146">在 `content` 文件夹中，在名为 `\Samples\<identifier>` 的文件夹中排列示例代码，与 `\Samples\Contoso.Utility.UsefulStuff.Sample` 中相似。</span><span class="sxs-lookup"><span data-stu-id="7ae2e-146">In the `content` folder, arrange the sample code in a folder called `\Samples\<identifier>` as in `\Samples\Contoso.Utility.UsefulStuff.Sample`.</span></span>

<span data-ttu-id="7ae2e-147">**针对包版本的最佳做法：**</span><span class="sxs-lookup"><span data-stu-id="7ae2e-147">**Best practices for the package version:**</span></span>

- <span data-ttu-id="7ae2e-148">一般情况下，将包的版本设置为与项目（或程序集）相匹配，但这不是必须的。</span><span class="sxs-lookup"><span data-stu-id="7ae2e-148">In general, set the version of the package to match the project (or assembly), though this is not strictly required.</span></span> <span data-ttu-id="7ae2e-149">如果将包限制为单个程序集，那么这是一个简单的问题。</span><span class="sxs-lookup"><span data-stu-id="7ae2e-149">This is a simple matter when you limit a package to a single assembly.</span></span> <span data-ttu-id="7ae2e-150">总的来说，请记住解析依赖项时，NuGet 自己处理包版本而不是程序集版本。</span><span class="sxs-lookup"><span data-stu-id="7ae2e-150">Overall, remember that NuGet itself deals with package versions when resolving dependencies, not assembly versions.</span></span>
- <span data-ttu-id="7ae2e-151">使用非标准版本方案时，请确保考虑使用 NuGet 版本控制规则，如[包版本控制](../reference/package-versioning.md)中所述。</span><span class="sxs-lookup"><span data-stu-id="7ae2e-151">When using a non-standard version scheme, be sure to consider the NuGet versioning rules as explained in [Package versioning](../reference/package-versioning.md).</span></span> <span data-ttu-id="7ae2e-152">NuGet 主要与 [semver 2 兼容](../reference/package-versioning.md#semantic-versioning-200)。</span><span class="sxs-lookup"><span data-stu-id="7ae2e-152">NuGet is mostly [semver 2 compliant](../reference/package-versioning.md#semantic-versioning-200).</span></span>

> <span data-ttu-id="7ae2e-153">有关依赖项解析的信息，请参阅[使用 PackageReference 的依赖项解析](../consume-packages/dependency-resolution.md#dependency-resolution-with-packagereference)。</span><span class="sxs-lookup"><span data-stu-id="7ae2e-153">For information on dependency resolution, see [Dependency resolution with PackageReference](../consume-packages/dependency-resolution.md#dependency-resolution-with-packagereference).</span></span> <span data-ttu-id="7ae2e-154">对于可能有助于更好地理解版本控制的较旧信息，请参阅此系列博客文章。</span><span class="sxs-lookup"><span data-stu-id="7ae2e-154">For older information that may also be helpful to better understand versioning, see this series of blog posts.</span></span>
>
> - [<span data-ttu-id="7ae2e-155">第 1 部分：解决 DLL 地狱</span><span class="sxs-lookup"><span data-stu-id="7ae2e-155">Part 1: Taking on DLL Hell</span></span>](http://blog.davidebbo.com/2011/01/nuget-versioning-part-1-taking-on-dll.html)
> - [<span data-ttu-id="7ae2e-156">第 2 部分：核心算法</span><span class="sxs-lookup"><span data-stu-id="7ae2e-156">Part 2: The core algorithm</span></span>](http://blog.davidebbo.com/2011/01/nuget-versioning-part-2-core-algorithm.html)
> - [<span data-ttu-id="7ae2e-157">第 3 部分：通过绑定重定向实现统一</span><span class="sxs-lookup"><span data-stu-id="7ae2e-157">Part 3: Unification via Binding Redirects</span></span>](http://blog.davidebbo.com/2011/01/nuget-versioning-part-3-unification-via.html)

## <a name="run-the-pack-command"></a><span data-ttu-id="7ae2e-158">运行 pack 命令</span><span class="sxs-lookup"><span data-stu-id="7ae2e-158">Run the pack command</span></span>

<span data-ttu-id="7ae2e-159">若要从项目中生成 NuGet 包（`.nupkg` 文件），运行 `dotnet pack` 命令，它也会自动生成项目：</span><span class="sxs-lookup"><span data-stu-id="7ae2e-159">To build a NuGet package (a `.nupkg` file) from the project, run the `dotnet pack` command, which also builds the project automatically:</span></span>

```cli
# Uses the project file in the current folder by default
dotnet pack
```

<span data-ttu-id="7ae2e-160">输出显示 `.nupkg` 文件的路径：</span><span class="sxs-lookup"><span data-stu-id="7ae2e-160">The output shows the path to the `.nupkg` file:</span></span>

```output
Microsoft (R) Build Engine version 15.5.180.51428 for .NET Core
Copyright (C) Microsoft Corporation. All rights reserved.

  Restore completed in 29.91 ms for D:\proj\AppLoggerNet\AppLogger\AppLogger.csproj.
  AppLogger -> D:\proj\AppLoggerNet\AppLogger\bin\Debug\netstandard2.0\AppLogger.dll
  Successfully created package 'D:\proj\AppLoggerNet\AppLogger\bin\Debug\AppLogger.1.0.0.nupkg'.
```

### <a name="automatically-generate-package-on-build"></a><span data-ttu-id="7ae2e-161">在生成期间自动生成包</span><span class="sxs-lookup"><span data-stu-id="7ae2e-161">Automatically generate package on build</span></span>

<span data-ttu-id="7ae2e-162">若要在运行 `dotnet build` 时自动运行 `dotnet pack`，请将以下行添加到 `<PropertyGroup>` 中的项目文件内：</span><span class="sxs-lookup"><span data-stu-id="7ae2e-162">To automatically run `dotnet pack` when you run `dotnet build`, add the following line to your project file within `<PropertyGroup>`:</span></span>

```xml
<GeneratePackageOnBuild>true</GeneratePackageOnBuild>
```

<span data-ttu-id="7ae2e-163">在解决方案上运行 `dotnet pack` 时，会打包解决方案中可打包的所有项目（[<IsPackable>](/dotnet/core/tools/csproj#nuget-metadata-properties) 属性设置为 `true`。</span><span class="sxs-lookup"><span data-stu-id="7ae2e-163">When you run `dotnet pack` on a solution, this packs all the projects in the solution that are packable ([<IsPackable>](/dotnet/core/tools/csproj#nuget-metadata-properties) property is set to `true`.</span></span>

> [!NOTE]
> <span data-ttu-id="7ae2e-164">自动生成包时，打包时间会增加项目的生成时间。</span><span class="sxs-lookup"><span data-stu-id="7ae2e-164">When you automatically generate the package, the time to pack increases the build time for your project.</span></span>

### <a name="test-package-installation"></a><span data-ttu-id="7ae2e-165">测试包安装</span><span class="sxs-lookup"><span data-stu-id="7ae2e-165">Test package installation</span></span>

<span data-ttu-id="7ae2e-166">发布包前，通常需要测试将包安装到项目的过程。</span><span class="sxs-lookup"><span data-stu-id="7ae2e-166">Before publishing a package, you typically want to test the process of installing a package into a project.</span></span> <span data-ttu-id="7ae2e-167">测试确保所有文件一定在项目中正确的位置结束。</span><span class="sxs-lookup"><span data-stu-id="7ae2e-167">The tests make sure that the necessarily files all end up in their correct places in the project.</span></span>

<span data-ttu-id="7ae2e-168">可以在 Visual Studio 中手动测试安装，或是使用常规[包安装步骤](../consume-packages/overview-and-workflow.md#ways-to-install-a-nuget-package)在命令行上测试。</span><span class="sxs-lookup"><span data-stu-id="7ae2e-168">You can test installations manually in Visual Studio or on the command line using the normal [package installation steps](../consume-packages/overview-and-workflow.md#ways-to-install-a-nuget-package).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="7ae2e-169">包是不可变的。</span><span class="sxs-lookup"><span data-stu-id="7ae2e-169">Packages are immutable.</span></span> <span data-ttu-id="7ae2e-170">如果更正了问题，请更改包的内容并再次打包，重新测试时，仍将使用旧版本的包，直到[清除全局包](../consume-packages/managing-the-global-packages-and-cache-folders.md#clearing-local-folders)文件夹。</span><span class="sxs-lookup"><span data-stu-id="7ae2e-170">If you correct a problem, change the contents of the package and pack again, when you retest you will still be using the old version of the package until you [clear your global packages](../consume-packages/managing-the-global-packages-and-cache-folders.md#clearing-local-folders) folder.</span></span> <span data-ttu-id="7ae2e-171">在测试每次生成时不使用唯一预发布标签的包时，这尤为重要。</span><span class="sxs-lookup"><span data-stu-id="7ae2e-171">This is especially relevant when testing packages that don't use a unique prerelease label on every build.</span></span>

## <a name="next-steps"></a><span data-ttu-id="7ae2e-172">后续步骤</span><span class="sxs-lookup"><span data-stu-id="7ae2e-172">Next Steps</span></span>

<span data-ttu-id="7ae2e-173">创建包（`.nupkg` 文件）后，可以将其发布到选择的库，如[发布包](../nuget-org/publish-a-package.md)中所述。</span><span class="sxs-lookup"><span data-stu-id="7ae2e-173">Once you've created a package, which is a `.nupkg` file, you can publish it to the gallery of your choice as described on [Publishing a Package](../nuget-org/publish-a-package.md).</span></span>

<span data-ttu-id="7ae2e-174">你可能还希望扩展包的功能，或者支持其他方案，如以下主题所述：</span><span class="sxs-lookup"><span data-stu-id="7ae2e-174">You might also want to extend the capabilities of your package or otherwise support other scenarios as described in the following topics:</span></span>

- [<span data-ttu-id="7ae2e-175">包版本控制</span><span class="sxs-lookup"><span data-stu-id="7ae2e-175">Package versioning</span></span>](../reference/package-versioning.md)
- [<span data-ttu-id="7ae2e-176">支持多个目标框架</span><span class="sxs-lookup"><span data-stu-id="7ae2e-176">Support multiple target frameworks</span></span>](../create-packages/multiple-target-frameworks-project-file.md)
- [<span data-ttu-id="7ae2e-177">源和配置文件的转换</span><span class="sxs-lookup"><span data-stu-id="7ae2e-177">Transformations of source and configuration files</span></span>](../create-packages/source-and-config-file-transformations.md)
- [<span data-ttu-id="7ae2e-178">本地化</span><span class="sxs-lookup"><span data-stu-id="7ae2e-178">Localization</span></span>](../create-packages/creating-localized-packages.md)
- [<span data-ttu-id="7ae2e-179">预发布版本</span><span class="sxs-lookup"><span data-stu-id="7ae2e-179">Pre-release versions</span></span>](../create-packages/prerelease-packages.md)
- [<span data-ttu-id="7ae2e-180">设置包类型</span><span class="sxs-lookup"><span data-stu-id="7ae2e-180">Set package type</span></span>](../create-packages/set-package-type.md)
- [<span data-ttu-id="7ae2e-181">使用 COM 互操作程序集创建包</span><span class="sxs-lookup"><span data-stu-id="7ae2e-181">Create packages with COM interop assemblies</span></span>](../create-packages/author-packages-with-COM-interop-assemblies.md)

<span data-ttu-id="7ae2e-182">最后，有需要注意的其他包类型：</span><span class="sxs-lookup"><span data-stu-id="7ae2e-182">Finally, there are additional package types to be aware of:</span></span>

- [<span data-ttu-id="7ae2e-183">本机包</span><span class="sxs-lookup"><span data-stu-id="7ae2e-183">Native Packages</span></span>](../create-packages/native-packages.md)
- [<span data-ttu-id="7ae2e-184">符号包</span><span class="sxs-lookup"><span data-stu-id="7ae2e-184">Symbol Packages</span></span>](../create-packages/symbol-packages.md)
