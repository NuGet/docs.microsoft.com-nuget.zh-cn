---
title: 使用 dotnet CLI 创建 NuGet 包
description: 设计和创建 NuGet 包流程的详细指南，包含文件和版本控制等关键决策点。
author: karann-msft
ms.author: karann
ms.date: 02/20/2020
ms.topic: conceptual
ms.openlocfilehash: 712e4c7159aa9719052330d8e45f63e18e390325
ms.sourcegitcommit: c81561e93a7be467c1983d639158d4e3dc25b93a
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/02/2020
ms.locfileid: "78230566"
---
# <a name="create-a-nuget-package-using-the-dotnet-cli"></a><span data-ttu-id="1672c-103">使用 dotnet CLI 创建 NuGet 包</span><span class="sxs-lookup"><span data-stu-id="1672c-103">Create a NuGet package using the dotnet CLI</span></span>

<span data-ttu-id="1672c-104">无论包是什么用途或者它包含什么代码，均使用其中一个 CLI 工具（`nuget.exe` 或 `dotnet.exe`）将该功能打包进可以与任意数量的其他开发人员共享且可以由其使用的组件中。</span><span class="sxs-lookup"><span data-stu-id="1672c-104">No matter what your package does or what code it contains, you use one of the CLI tools, either `nuget.exe` or `dotnet.exe`, to package that functionality into a component that can be shared with and used by any number of other developers.</span></span> <span data-ttu-id="1672c-105">本文介绍如何使用 dotnet CLI 创建包。</span><span class="sxs-lookup"><span data-stu-id="1672c-105">This article describes how to create a package using the dotnet CLI.</span></span> <span data-ttu-id="1672c-106">若要安装 `dotnet` CLI，请参阅[安装 NuGet 客户端工具](../install-nuget-client-tools.md)。</span><span class="sxs-lookup"><span data-stu-id="1672c-106">To install the `dotnet` CLI, see [Install NuGet client tools](../install-nuget-client-tools.md).</span></span> <span data-ttu-id="1672c-107">从 Visual Studio 2017 开始，dotnet CLI 包含在 .NET Core 工作负载中。</span><span class="sxs-lookup"><span data-stu-id="1672c-107">Starting in Visual Studio 2017, the dotnet CLI is included with .NET Core workloads.</span></span>

<span data-ttu-id="1672c-108">对于使用 [SDK 样式格式](../resources/check-project-format.md)的 .NET Core 和 .NET Standard 项目，以及任何其他 SDK 样式项目，NuGet 直接使用项目文件中的信息创建包。</span><span class="sxs-lookup"><span data-stu-id="1672c-108">For .NET Core and .NET Standard projects that use the [SDK-style format](../resources/check-project-format.md), and any other SDK-style projects, NuGet uses information in the project file directly to create a package.</span></span> <span data-ttu-id="1672c-109">若要查看分步教程，请参阅[使用 dotnet CLI 创建 .NET Standard 包](../quickstart/create-and-publish-a-package-using-the-dotnet-cli.md)或[使用 Visual Studio 创建 .NET Standard 包](../quickstart/create-and-publish-a-package-using-visual-studio.md)。</span><span class="sxs-lookup"><span data-stu-id="1672c-109">For step-by-step tutorials, see [Create .NET Standard Packages with dotnet CLI](../quickstart/create-and-publish-a-package-using-the-dotnet-cli.md) or [Create .NET Standard Packages with Visual Studio](../quickstart/create-and-publish-a-package-using-visual-studio.md).</span></span>

<span data-ttu-id="1672c-110">`msbuild -t:pack` 在功能上等效于 `dotnet pack`。</span><span class="sxs-lookup"><span data-stu-id="1672c-110">`msbuild -t:pack` is functionality equivalent to `dotnet pack`.</span></span> <span data-ttu-id="1672c-111">若要使用 MSBuild 进行生成，请参阅 [使用 MSBuild 创建 NuGet 包](creating-a-package-msbuild.md)。</span><span class="sxs-lookup"><span data-stu-id="1672c-111">To build with MSBuild, see [Create a NuGet package using MSBuild](creating-a-package-msbuild.md).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="1672c-112">本主题适用于 [ SDK 样式](../resources/check-project-format.md)的项目，通常是 .NET Core 和 .NET Standard 项目。</span><span class="sxs-lookup"><span data-stu-id="1672c-112">This topic applies to [SDK-style](../resources/check-project-format.md) projects, typically .NET Core and .NET Standard projects.</span></span>

## <a name="set-properties"></a><span data-ttu-id="1672c-113">设置属性</span><span class="sxs-lookup"><span data-stu-id="1672c-113">Set properties</span></span>

<span data-ttu-id="1672c-114">创建包需要以下属性。</span><span class="sxs-lookup"><span data-stu-id="1672c-114">The following properties are required to create a package.</span></span>

- <span data-ttu-id="1672c-115">`PackageId`，包标识符，在托管包的库中必须是唯一的。</span><span class="sxs-lookup"><span data-stu-id="1672c-115">`PackageId`, the package identifier, which must be unique across the gallery that hosts the package.</span></span> <span data-ttu-id="1672c-116">如果未指定，默认值为 `AssemblyName`。</span><span class="sxs-lookup"><span data-stu-id="1672c-116">If not specified, the default value is `AssemblyName`.</span></span>
- <span data-ttu-id="1672c-117">`Version`，窗体 Major.Minor.Patch[-Suffix] 中特定的版本号，其中 -Suffix 标识[预发布版本](prerelease-packages.md)   。</span><span class="sxs-lookup"><span data-stu-id="1672c-117">`Version`, a specific version number in the form *Major.Minor.Patch[-Suffix]* where *-Suffix* identifies [pre-release versions](prerelease-packages.md).</span></span> <span data-ttu-id="1672c-118">如果未指定，默认值为 1.0.0。</span><span class="sxs-lookup"><span data-stu-id="1672c-118">If not specified, the default value is 1.0.0.</span></span>
- <span data-ttu-id="1672c-119">包标题应出现在主机上（例如 nuget.org）</span><span class="sxs-lookup"><span data-stu-id="1672c-119">The package title as it should appear on the host (like nuget.org)</span></span>
- <span data-ttu-id="1672c-120">`Authors`，作者和所有者信息。</span><span class="sxs-lookup"><span data-stu-id="1672c-120">`Authors`, author and owner information.</span></span> <span data-ttu-id="1672c-121">如果未指定，默认值为 `AssemblyName`。</span><span class="sxs-lookup"><span data-stu-id="1672c-121">If not specified, the default value is `AssemblyName`.</span></span>
- <span data-ttu-id="1672c-122">`Company`，公司名称。</span><span class="sxs-lookup"><span data-stu-id="1672c-122">`Company`, your company name.</span></span> <span data-ttu-id="1672c-123">如果未指定，默认值为 `AssemblyName`。</span><span class="sxs-lookup"><span data-stu-id="1672c-123">If not specified, the default value is `AssemblyName`.</span></span>

<span data-ttu-id="1672c-124">在 Visual Studio 中，可以在项目属性中设置这些值（在解决方案资源管理器中右键单击项目，选择“属性”  ，然后选择“包”  选项卡）。</span><span class="sxs-lookup"><span data-stu-id="1672c-124">In Visual Studio, you can set these values in the project properties (right-click the project in Solution Explorer, choose **Properties**, and select the **Package** tab).</span></span> <span data-ttu-id="1672c-125">也可以直接在项目文件 (`.csproj`) 中设置这些属性。</span><span class="sxs-lookup"><span data-stu-id="1672c-125">You can also set these properties directly in the project files (`.csproj`).</span></span>

```xml
<PropertyGroup>
  <PackageId>AppLogger</PackageId>
  <Version>1.0.0</Version>
  <Authors>your_name</Authors>
  <Company>your_company</Company>
</PropertyGroup>
```

> [!Important]
> <span data-ttu-id="1672c-126">为包提供一个在 nuget.org 中唯一或你使用的任何包资源的标识符。</span><span class="sxs-lookup"><span data-stu-id="1672c-126">Give the package an identifier that's unique across nuget.org or whatever package source you're using.</span></span>

<span data-ttu-id="1672c-127">以下示例显示了包含这些属性的简单、完整的项目文件。</span><span class="sxs-lookup"><span data-stu-id="1672c-127">The following example shows a simple, complete project file with these properties included.</span></span> <span data-ttu-id="1672c-128">（可以使用 `dotnet new classlib` 命令创建新的默认项目。）</span><span class="sxs-lookup"><span data-stu-id="1672c-128">(You can create a new default project using the `dotnet new classlib` command.)</span></span>

```xml
<Project Sdk="Microsoft.NET.Sdk">
  <PropertyGroup>
    <TargetFramework>netstandard2.0</TargetFramework>
    <PackageId>AppLogger</PackageId>
    <Version>1.0.0</Version>
    <Authors>your_name</Authors>
    <Company>your_company</Company>
  </PropertyGroup>
</Project>
```

<span data-ttu-id="1672c-129">另外，还可以设置可选属性，例如 `Title`、`PackageDescription` 和 `PackageTags`，如 [MSBuild 包目标](../reference/msbuild-targets.md#pack-target)、[控制依赖项资产](../consume-packages/package-references-in-project-files.md#controlling-dependency-assets)和 [NuGet 元数据属性](/dotnet/core/tools/csproj#nuget-metadata-properties)中所述。</span><span class="sxs-lookup"><span data-stu-id="1672c-129">You can also set the optional properties, such as `Title`, `PackageDescription`, and `PackageTags`, as described in [MSBuild pack targets](../reference/msbuild-targets.md#pack-target), [Controlling dependency assets](../consume-packages/package-references-in-project-files.md#controlling-dependency-assets), and [NuGet metadata properties](/dotnet/core/tools/csproj#nuget-metadata-properties).</span></span>

> [!NOTE]
> <span data-ttu-id="1672c-130">对于面向公共使用而生成的包，请特别注意 **PackageTags** 属性，因为这些标记可帮助其他人查找包并了解其用途。</span><span class="sxs-lookup"><span data-stu-id="1672c-130">For packages built for public consumption, pay special attention to the **PackageTags** property, as tags help others find your package and understand what it does.</span></span>

<span data-ttu-id="1672c-131">有关声明依赖项并指定版本号的详细信息，请参阅[项目文件中的包引用](../consume-packages/package-references-in-project-files.md)和[包版本控制](../concepts/package-versioning.md)。</span><span class="sxs-lookup"><span data-stu-id="1672c-131">For details on declaring dependencies and specifying version numbers, see [Package references in project files](../consume-packages/package-references-in-project-files.md) and [Package versioning](../concepts/package-versioning.md).</span></span> <span data-ttu-id="1672c-132">还可以使用 `<IncludeAssets>` 和 `<ExcludeAssets>` 特性直接在包中呈现依赖项的资产。</span><span class="sxs-lookup"><span data-stu-id="1672c-132">It is also possible to surface assets from dependencies directly in the package by using the `<IncludeAssets>` and `<ExcludeAssets>` attributes.</span></span> <span data-ttu-id="1672c-133">有关详细信息，请参阅[控制依赖项资产](../consume-packages/package-references-in-project-files.md#controlling-dependency-assets)。</span><span class="sxs-lookup"><span data-stu-id="1672c-133">For more information, seee [Controlling dependency assets](../consume-packages/package-references-in-project-files.md#controlling-dependency-assets).</span></span>

## <a name="add-an-optional-description-field"></a><span data-ttu-id="1672c-134">添加可选说明字段</span><span class="sxs-lookup"><span data-stu-id="1672c-134">Add an optional description field</span></span>

[!INCLUDE [add description to package](includes/add-description.md)]

## <a name="choose-a-unique-package-identifier-and-set-the-version-number"></a><span data-ttu-id="1672c-135">选择唯一的包标识符并设置版本号</span><span class="sxs-lookup"><span data-stu-id="1672c-135">Choose a unique package identifier and set the version number</span></span>

[!INCLUDE [choose-package-id](includes/choose-package-id.md)]

## <a name="run-the-pack-command"></a><span data-ttu-id="1672c-136">运行 pack 命令</span><span class="sxs-lookup"><span data-stu-id="1672c-136">Run the pack command</span></span>

<span data-ttu-id="1672c-137">若要从项目中生成 NuGet 包（`.nupkg` 文件），运行 `dotnet pack` 命令，它也会自动生成项目：</span><span class="sxs-lookup"><span data-stu-id="1672c-137">To build a NuGet package (a `.nupkg` file) from the project, run the `dotnet pack` command, which also builds the project automatically:</span></span>

```dotnetcli
# Uses the project file in the current folder by default
dotnet pack
```

<span data-ttu-id="1672c-138">输出将显示 `.nupkg` 文件的路径。</span><span class="sxs-lookup"><span data-stu-id="1672c-138">The output shows the path to the `.nupkg` file.</span></span>

```output
Microsoft (R) Build Engine version 15.5.180.51428 for .NET Core
Copyright (C) Microsoft Corporation. All rights reserved.

  Restore completed in 29.91 ms for D:\proj\AppLoggerNet\AppLogger\AppLogger.csproj.
  AppLogger -> D:\proj\AppLoggerNet\AppLogger\bin\Debug\netstandard2.0\AppLogger.dll
  Successfully created package 'D:\proj\AppLoggerNet\AppLogger\bin\Debug\AppLogger.1.0.0.nupkg'.
```

### <a name="automatically-generate-package-on-build"></a><span data-ttu-id="1672c-139">在生成期间自动生成包</span><span class="sxs-lookup"><span data-stu-id="1672c-139">Automatically generate package on build</span></span>

<span data-ttu-id="1672c-140">若要在运行 `dotnet build` 时自动运行 `dotnet pack`，请将以下行添加到 `<PropertyGroup>` 中的项目文件内：</span><span class="sxs-lookup"><span data-stu-id="1672c-140">To automatically run `dotnet pack` when you run `dotnet build`, add the following line to your project file within `<PropertyGroup>`:</span></span>

```xml
<GeneratePackageOnBuild>true</GeneratePackageOnBuild>
```

<span data-ttu-id="1672c-141">在解决方案上运行 `dotnet pack` 时，会打包解决方案中可打包的所有项目（[<IsPackable>](/dotnet/core/tools/csproj#nuget-metadata-properties) 属性设置为 `true`）。</span><span class="sxs-lookup"><span data-stu-id="1672c-141">When you run `dotnet pack` on a solution, this packs all the projects in the solution that are packable ([<IsPackable>](/dotnet/core/tools/csproj#nuget-metadata-properties) property is set to `true`).</span></span>

> [!NOTE]
> <span data-ttu-id="1672c-142">自动生成包时，打包时间会增加项目的生成时间。</span><span class="sxs-lookup"><span data-stu-id="1672c-142">When you automatically generate the package, the time to pack increases the build time for your project.</span></span>

### <a name="test-package-installation"></a><span data-ttu-id="1672c-143">测试包安装</span><span class="sxs-lookup"><span data-stu-id="1672c-143">Test package installation</span></span>

<span data-ttu-id="1672c-144">发布包前，通常需要测试将包安装到项目的过程。</span><span class="sxs-lookup"><span data-stu-id="1672c-144">Before publishing a package, you typically want to test the process of installing a package into a project.</span></span> <span data-ttu-id="1672c-145">测试确保所有文件一定在项目中正确的位置结束。</span><span class="sxs-lookup"><span data-stu-id="1672c-145">The tests make sure that the necessarily files all end up in their correct places in the project.</span></span>

<span data-ttu-id="1672c-146">可以在 Visual Studio 中手动测试安装，或是使用常规[包安装步骤](../consume-packages/overview-and-workflow.md#ways-to-install-a-nuget-package)在命令行上测试。</span><span class="sxs-lookup"><span data-stu-id="1672c-146">You can test installations manually in Visual Studio or on the command line using the normal [package installation steps](../consume-packages/overview-and-workflow.md#ways-to-install-a-nuget-package).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="1672c-147">包是不可变的。</span><span class="sxs-lookup"><span data-stu-id="1672c-147">Packages are immutable.</span></span> <span data-ttu-id="1672c-148">如果更正了问题，请更改包的内容并再次打包，重新测试时，仍将使用旧版本的包，直到[清除全局包](../consume-packages/managing-the-global-packages-and-cache-folders.md#clearing-local-folders)文件夹。</span><span class="sxs-lookup"><span data-stu-id="1672c-148">If you correct a problem, change the contents of the package and pack again, when you retest you will still be using the old version of the package until you [clear your global packages](../consume-packages/managing-the-global-packages-and-cache-folders.md#clearing-local-folders) folder.</span></span> <span data-ttu-id="1672c-149">在测试每次生成时不使用唯一预发布标签的包时，这尤为重要。</span><span class="sxs-lookup"><span data-stu-id="1672c-149">This is especially relevant when testing packages that don't use a unique prerelease label on every build.</span></span>

## <a name="next-steps"></a><span data-ttu-id="1672c-150">后续步骤</span><span class="sxs-lookup"><span data-stu-id="1672c-150">Next Steps</span></span>

<span data-ttu-id="1672c-151">创建包（`.nupkg` 文件）后，可以将其发布到选择的库，如[发布包](../nuget-org/publish-a-package.md)中所述。</span><span class="sxs-lookup"><span data-stu-id="1672c-151">Once you've created a package, which is a `.nupkg` file, you can publish it to the gallery of your choice as described on [Publishing a Package](../nuget-org/publish-a-package.md).</span></span>

<span data-ttu-id="1672c-152">你可能还希望扩展包的功能，或者支持其他方案，如以下主题所述：</span><span class="sxs-lookup"><span data-stu-id="1672c-152">You might also want to extend the capabilities of your package or otherwise support other scenarios as described in the following topics:</span></span>

- [<span data-ttu-id="1672c-153">包版本控制</span><span class="sxs-lookup"><span data-stu-id="1672c-153">Package versioning</span></span>](../concepts/package-versioning.md)
- [<span data-ttu-id="1672c-154">支持多个目标框架</span><span class="sxs-lookup"><span data-stu-id="1672c-154">Support multiple target frameworks</span></span>](../create-packages/multiple-target-frameworks-project-file.md)
- [<span data-ttu-id="1672c-155">添加包图标</span><span class="sxs-lookup"><span data-stu-id="1672c-155">Add a package icon</span></span>](../reference/nuspec.md#icon)
- [<span data-ttu-id="1672c-156">源和配置文件的转换</span><span class="sxs-lookup"><span data-stu-id="1672c-156">Transformations of source and configuration files</span></span>](../create-packages/source-and-config-file-transformations.md)
- [<span data-ttu-id="1672c-157">本地化</span><span class="sxs-lookup"><span data-stu-id="1672c-157">Localization</span></span>](../create-packages/creating-localized-packages.md)
- [<span data-ttu-id="1672c-158">预发布版本</span><span class="sxs-lookup"><span data-stu-id="1672c-158">Pre-release versions</span></span>](../create-packages/prerelease-packages.md)
- [<span data-ttu-id="1672c-159">设置包类型</span><span class="sxs-lookup"><span data-stu-id="1672c-159">Set package type</span></span>](../create-packages/set-package-type.md)
- [<span data-ttu-id="1672c-160">使用 COM 互操作程序集创建包</span><span class="sxs-lookup"><span data-stu-id="1672c-160">Create packages with COM interop assemblies</span></span>](../create-packages/author-packages-with-COM-interop-assemblies.md)

<span data-ttu-id="1672c-161">最后，有需要注意的其他包类型：</span><span class="sxs-lookup"><span data-stu-id="1672c-161">Finally, there are additional package types to be aware of:</span></span>

- [<span data-ttu-id="1672c-162">本机包</span><span class="sxs-lookup"><span data-stu-id="1672c-162">Native Packages</span></span>](../guides/native-packages.md)
- [<span data-ttu-id="1672c-163">符号包</span><span class="sxs-lookup"><span data-stu-id="1672c-163">Symbol Packages</span></span>](../create-packages/symbol-packages-snupkg.md)
