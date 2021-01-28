---
title: 使用 MSBuild 创建 NuGet 包
description: 设计和创建 NuGet 包流程的详细指南，包含文件和版本控制等关键决策点。
author: JonDouglas
ms.author: jodou
ms.date: 02/20/2020
ms.topic: conceptual
ms.openlocfilehash: 48741668af932a532240f2796a9bf5d490ee8e35
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/26/2021
ms.locfileid: "98774441"
---
# <a name="create-a-nuget-package-using-msbuild"></a><span data-ttu-id="0a183-103">使用 MSBuild 创建 NuGet 包</span><span class="sxs-lookup"><span data-stu-id="0a183-103">Create a NuGet package using MSBuild</span></span>

<span data-ttu-id="0a183-104">从代码中创建 NuGet 包时，会将该功能打包到一个组件中，该组件可以与任意数量的其他开发人员共享和使用。</span><span class="sxs-lookup"><span data-stu-id="0a183-104">When you create a NuGet package from your code, you package that functionality into a component that can be shared with and used by any number of other developers.</span></span> <span data-ttu-id="0a183-105">本文介绍如何使用 MSBuild 创建包。</span><span class="sxs-lookup"><span data-stu-id="0a183-105">This article describes how to create a package using MSBuild.</span></span> <span data-ttu-id="0a183-106">MSBuild 预安装了包含 NuGet 的所有 Visual Studio 工作负荷。</span><span class="sxs-lookup"><span data-stu-id="0a183-106">MSBuild comes preinstalled with every Visual Studio workload that contains NuGet.</span></span> <span data-ttu-id="0a183-107">此外，还可以通过 dotnet CLI 借助 [dotnet msbuild](/dotnet/core/tools/dotnet-msbuild) 来使用 MSBuild。</span><span class="sxs-lookup"><span data-stu-id="0a183-107">Additionally you can also use MSBuild through the dotnet CLI with [dotnet msbuild](/dotnet/core/tools/dotnet-msbuild).</span></span>

<span data-ttu-id="0a183-108">对于使用 [SDK 样式格式](../resources/check-project-format.md)的 .NET Core 和 .NET Standard 项目，以及任何其他 SDK 样式项目，NuGet 直接使用项目文件中的信息创建包。</span><span class="sxs-lookup"><span data-stu-id="0a183-108">For .NET Core and .NET Standard projects that use the [SDK-style format](../resources/check-project-format.md), and any other SDK-style projects, NuGet uses information in the project file directly to create a package.</span></span>  <span data-ttu-id="0a183-109">对于使用 `<PackageReference>` 的非 SDK 样式的项目，NuGet 还使用项目文件来创建包。</span><span class="sxs-lookup"><span data-stu-id="0a183-109">For a non-SDK-style project that uses `<PackageReference>`, NuGet also uses the project file to create a package.</span></span>

<span data-ttu-id="0a183-110">默认情况下，SDK 样式的项目具有可用的包功能。</span><span class="sxs-lookup"><span data-stu-id="0a183-110">SDK-style projects have the pack functionality available by default.</span></span> <span data-ttu-id="0a183-111">对于非 SDK 样式的 PackageReference 项目，需要将 NuGet.Build.Tasks.Pack 包添加到项目依赖项中。</span><span class="sxs-lookup"><span data-stu-id="0a183-111">For non SDK-style PackageReference projects, you need to add the NuGet.Build.Tasks.Pack package to the project dependencies.</span></span> <span data-ttu-id="0a183-112">有关 MSBuild 包目标的详细信息，请参阅[作为 MSBuild 目标的 NuGet 包和还原](../reference/msbuild-targets.md)。</span><span class="sxs-lookup"><span data-stu-id="0a183-112">For detailed information about MSBuild pack targets, see [NuGet pack and restore as MSBuild targets](../reference/msbuild-targets.md).</span></span>

<span data-ttu-id="0a183-113">用于创建包的命令 `msbuild -t:pack`，其功能相当于 `dotnet pack`。</span><span class="sxs-lookup"><span data-stu-id="0a183-113">The command that creates a package, `msbuild -t:pack`, is functionality equivalent to `dotnet pack`.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="0a183-114">本主题适用于 [SDK 样式](../resources/check-project-format.md)的项目（通常是 .NET Core 和 .NET Standard 项目）以及使用 PackageReference 的非 SDK 样式的项目。</span><span class="sxs-lookup"><span data-stu-id="0a183-114">This topic applies to [SDK-style](../resources/check-project-format.md) projects, typically .NET Core and .NET Standard projects, and to non-SDK-style projects that use PackageReference.</span></span>

## <a name="set-properties"></a><span data-ttu-id="0a183-115">设置属性</span><span class="sxs-lookup"><span data-stu-id="0a183-115">Set properties</span></span>

<span data-ttu-id="0a183-116">创建包需要以下属性。</span><span class="sxs-lookup"><span data-stu-id="0a183-116">The following properties are required to create a package.</span></span>

- <span data-ttu-id="0a183-117">`PackageId`，包标识符，在托管包的库中必须是唯一的。</span><span class="sxs-lookup"><span data-stu-id="0a183-117">`PackageId`, the package identifier, which must be unique across the gallery that hosts the package.</span></span> <span data-ttu-id="0a183-118">如果未指定，默认值为 `AssemblyName`。</span><span class="sxs-lookup"><span data-stu-id="0a183-118">If not specified, the default value is `AssemblyName`.</span></span>
- <span data-ttu-id="0a183-119">`Version`，窗体 Major.Minor.Patch[-Suffix] 中特定的版本号，其中 -Suffix 标识[预发布版本](prerelease-packages.md)。</span><span class="sxs-lookup"><span data-stu-id="0a183-119">`Version`, a specific version number in the form *Major.Minor.Patch[-Suffix]* where *-Suffix* identifies [pre-release versions](prerelease-packages.md).</span></span> <span data-ttu-id="0a183-120">如果未指定，默认值为 1.0.0。</span><span class="sxs-lookup"><span data-stu-id="0a183-120">If not specified, the default value is 1.0.0.</span></span>
- <span data-ttu-id="0a183-121">包标题应出现在主机上（例如 nuget.org）</span><span class="sxs-lookup"><span data-stu-id="0a183-121">The package title as it should appear on the host (like nuget.org)</span></span>
- <span data-ttu-id="0a183-122">`Authors`，作者和所有者信息。</span><span class="sxs-lookup"><span data-stu-id="0a183-122">`Authors`, author and owner information.</span></span> <span data-ttu-id="0a183-123">如果未指定，默认值为 `AssemblyName`。</span><span class="sxs-lookup"><span data-stu-id="0a183-123">If not specified, the default value is `AssemblyName`.</span></span>
- <span data-ttu-id="0a183-124">`Company`，公司名称。</span><span class="sxs-lookup"><span data-stu-id="0a183-124">`Company`, your company name.</span></span> <span data-ttu-id="0a183-125">如果未指定，默认值为 `AssemblyName`。</span><span class="sxs-lookup"><span data-stu-id="0a183-125">If not specified, the default value is `AssemblyName`.</span></span>

<span data-ttu-id="0a183-126">此外，如要打包使用 PackageReference 的非 SDK 类项目，则需要满足以下要求：</span><span class="sxs-lookup"><span data-stu-id="0a183-126">Additionally if you are packing non-SDK-style projects that use PackageReference, the following is required:</span></span>

- <span data-ttu-id="0a183-127">`PackageOutputPath`（调用 pack 时生成的包的输出文件夹）。</span><span class="sxs-lookup"><span data-stu-id="0a183-127">`PackageOutputPath`, the output folder for the package generated when calling pack.</span></span>

<span data-ttu-id="0a183-128">在 Visual Studio 中，可以在项目属性中设置这些值（在解决方案资源管理器中右键单击项目，选择“属性”  ，然后选择“包”  选项卡）。</span><span class="sxs-lookup"><span data-stu-id="0a183-128">In Visual Studio, you can set these values in the project properties (right-click the project in Solution Explorer, choose **Properties**, and select the **Package** tab).</span></span> <span data-ttu-id="0a183-129">也可以直接在项目文件 (.csproj) 中设置这些属性  。</span><span class="sxs-lookup"><span data-stu-id="0a183-129">You can also set these properties directly in the project files (*.csproj*).</span></span>

```xml
<PropertyGroup>
  <PackageId>ClassLibDotNetStandard</PackageId>
  <Version>1.0.0</Version>
  <Authors>your_name</Authors>
  <Company>your_company</Company>
</PropertyGroup>
```

> [!Important]
> <span data-ttu-id="0a183-130">为包提供一个在 nuget.org 中唯一或你使用的任何包资源的标识符。</span><span class="sxs-lookup"><span data-stu-id="0a183-130">Give the package an identifier that's unique across nuget.org or whatever package source you're using.</span></span>

<span data-ttu-id="0a183-131">以下示例显示了包含这些属性的简单、完整的项目文件。</span><span class="sxs-lookup"><span data-stu-id="0a183-131">The following example shows a simple, complete project file with these properties included.</span></span>

```xml
<Project Sdk="Microsoft.NET.Sdk">
  <PropertyGroup>
    <TargetFramework>netstandard2.0</TargetFramework>
    <PackageId>ClassLibDotNetStandard</PackageId>
    <Version>1.0.0</Version>
    <Authors>your_name</Authors>
    <Company>your_company</Company>
  </PropertyGroup>
</Project>
```

<span data-ttu-id="0a183-132">另外，还可以设置可选属性，例如 `Title`、`PackageDescription` 和 `PackageTags`，如 [MSBuild 包目标](../reference/msbuild-targets.md#pack-target)、[控制依赖项资产](../consume-packages/package-references-in-project-files.md#controlling-dependency-assets)和 [NuGet 元数据属性](/dotnet/core/tools/csproj#nuget-metadata-properties)中所述。</span><span class="sxs-lookup"><span data-stu-id="0a183-132">You can also set the optional properties, such as `Title`, `PackageDescription`, and `PackageTags`, as described in [MSBuild pack targets](../reference/msbuild-targets.md#pack-target), [Controlling dependency assets](../consume-packages/package-references-in-project-files.md#controlling-dependency-assets), and [NuGet metadata properties](/dotnet/core/tools/csproj#nuget-metadata-properties).</span></span>

> [!NOTE]
> <span data-ttu-id="0a183-133">对于面向公共使用而生成的包，请特别注意 **PackageTags** 属性，因为这些标记可帮助其他人查找包并了解其用途。</span><span class="sxs-lookup"><span data-stu-id="0a183-133">For packages built for public consumption, pay special attention to the **PackageTags** property, as tags help others find your package and understand what it does.</span></span>

<span data-ttu-id="0a183-134">有关声明依赖项并指定版本号的详细信息，请参阅[项目文件中的包引用](../consume-packages/package-references-in-project-files.md)和[包版本控制](../concepts/package-versioning.md)。</span><span class="sxs-lookup"><span data-stu-id="0a183-134">For details on declaring dependencies and specifying version numbers, see [Package references in project files](../consume-packages/package-references-in-project-files.md) and [Package versioning](../concepts/package-versioning.md).</span></span> <span data-ttu-id="0a183-135">还可以使用 `<IncludeAssets>` 和 `<ExcludeAssets>` 特性直接在包中呈现依赖项的资产。</span><span class="sxs-lookup"><span data-stu-id="0a183-135">It is also possible to surface assets from dependencies directly in the package by using the `<IncludeAssets>` and `<ExcludeAssets>` attributes.</span></span> <span data-ttu-id="0a183-136">有关详细信息，请参阅[控制依赖项资产](../consume-packages/package-references-in-project-files.md#controlling-dependency-assets)。</span><span class="sxs-lookup"><span data-stu-id="0a183-136">For more information, seee [Controlling dependency assets](../consume-packages/package-references-in-project-files.md#controlling-dependency-assets).</span></span>

## <a name="add-an-optional-description-field"></a><span data-ttu-id="0a183-137">添加可选说明字段</span><span class="sxs-lookup"><span data-stu-id="0a183-137">Add an optional description field</span></span>

[!INCLUDE [add description to package](includes/add-description.md)]

## <a name="choose-a-unique-package-identifier-and-set-the-version-number"></a><span data-ttu-id="0a183-138">选择唯一的包标识符并设置版本号</span><span class="sxs-lookup"><span data-stu-id="0a183-138">Choose a unique package identifier and set the version number</span></span>

[!INCLUDE [choose-package-id](includes/choose-package-id.md)]

## <a name="add-the-nugetbuildtaskspack-package"></a><span data-ttu-id="0a183-139">添加 NuGet.Build.Tasks.Pack 包</span><span class="sxs-lookup"><span data-stu-id="0a183-139">Add the NuGet.Build.Tasks.Pack package</span></span>

<span data-ttu-id="0a183-140">如果将 MSBuild 与非 SDK 样式项目和 PackageReference 一起使用，请将 NuGet.Build.Tasks.Pack 包添加到项目中。</span><span class="sxs-lookup"><span data-stu-id="0a183-140">If you are using MSBuild with a non-SDK-style project and PackageReference, add the NuGet.Build.Tasks.Pack package to your project.</span></span>

1. <span data-ttu-id="0a183-141">打开项目文件并在 `<PropertyGroup>` 元素后面添加以下内容：</span><span class="sxs-lookup"><span data-stu-id="0a183-141">Open the project file and add the following after the `<PropertyGroup>` element:</span></span>

   ```xml
   <ItemGroup>
     <!-- ... -->
     <PackageReference Include="NuGet.Build.Tasks.Pack" Version="5.2.0"/>
     <!-- ... -->
   </ItemGroup>
   ```

2. <span data-ttu-id="0a183-142">打开开发人员命令提示符（在“搜索”框中，键入“开发人员命令提示符”）   。</span><span class="sxs-lookup"><span data-stu-id="0a183-142">Open a Developer command prompt (In the **Search** box, type **Developer command prompt**).</span></span>

   <span data-ttu-id="0a183-143">用户通常习惯从“开始”菜单中启动“适用于 Visual Studio 的开发人员命令提示符”，因为它将使用 MSBuild 的所有必需路径进行配置  。</span><span class="sxs-lookup"><span data-stu-id="0a183-143">You typically want to start the Developer Command Prompt for Visual Studio from the **Start** menu, as it will be configured with all the necessary paths for MSBuild.</span></span>

3. <span data-ttu-id="0a183-144">切换到包含项目文件的文件夹，然后键入以下命令以安装 NuGet.Build.Tasks.Pack 包。</span><span class="sxs-lookup"><span data-stu-id="0a183-144">Switch to the folder containing the project file and type the following command to install the NuGet.Build.Tasks.Pack package.</span></span>

   ```cmd
   # Uses the project file in the current folder by default
   msbuild -t:restore
   ```

   <span data-ttu-id="0a183-145">确保 MSBuild 输出指示生成已成功完成。</span><span class="sxs-lookup"><span data-stu-id="0a183-145">Make sure that the MSBuild output indicates that the build completed successfully.</span></span>

## <a name="run-the-msbuild--tpack-command"></a><span data-ttu-id="0a183-146">运行 msbuild -t:pack 命令</span><span class="sxs-lookup"><span data-stu-id="0a183-146">Run the msbuild -t:pack command</span></span>

<span data-ttu-id="0a183-147">若要从项目中生成 NuGet 包（`.nupkg` 文件），运行 `msbuild -t:pack` 命令，它也会自动生成项目：</span><span class="sxs-lookup"><span data-stu-id="0a183-147">To build a NuGet package (a `.nupkg` file) from the project, run the `msbuild -t:pack` command, which also builds the project automatically:</span></span>

<span data-ttu-id="0a183-148">在 Visual Studio 开发人员命令提示处，键入以下命令：</span><span class="sxs-lookup"><span data-stu-id="0a183-148">In the Developer command prompt for Visual Studio, type the following command:</span></span>

```cmd
# Uses the project file in the current folder by default
msbuild -t:pack
```

<span data-ttu-id="0a183-149">输出将显示 `.nupkg` 文件的路径。</span><span class="sxs-lookup"><span data-stu-id="0a183-149">The output shows the path to the `.nupkg` file.</span></span>

```output
Microsoft (R) Build Engine version 16.1.76+g14b0a930a7 for .NET Framework
Copyright (C) Microsoft Corporation. All rights reserved.

Build started 8/5/2019 3:09:15 PM.
Project "C:\Users\username\source\repos\ClassLib_DotNetStandard\ClassLib_DotNetStandard.csproj" on node 1 (pack target(s)).
GenerateTargetFrameworkMonikerAttribute:
Skipping target "GenerateTargetFrameworkMonikerAttribute" because all output files are up-to-date with respect to the input files.
CoreCompile:
  ...
CopyFilesToOutputDirectory:
  Copying file from "C:\Users\username\source\repos\ClassLib_DotNetStandard\obj\Debug\netstandard2.0\ClassLib_DotNetStandard.dll" to "C:\Use
  rs\username\source\repos\ClassLib_DotNetStandard\bin\Debug\netstandard2.0\ClassLib_DotNetStandard.dll".
  ClassLib_DotNetStandard -> C:\Users\username\source\repos\ClassLib_DotNetStandard\bin\Debug\netstandard2.0\ClassLib_DotNetStandard.dll
  Copying file from "C:\Users\username\source\repos\ClassLib_DotNetStandard\obj\Debug\netstandard2.0\ClassLib_DotNetStandard.pdb" to "C:\Use
  rs\username\source\repos\ClassLib_DotNetStandard\bin\Debug\netstandard2.0\ClassLib_DotNetStandard.pdb".
GenerateNuspec:
  Successfully created package 'C:\Users\username\source\repos\ClassLib_DotNetStandard\bin\Debug\AppLogger.1.0.0.nupkg'.
Done Building Project "C:\Users\username\source\repos\ClassLib_DotNetStandard\ClassLib_DotNetStandard.csproj" (pack target(s)).

Build succeeded.
    0 Warning(s)
    0 Error(s)

Time Elapsed 00:00:01.21
```

### <a name="automatically-generate-package-on-build"></a><span data-ttu-id="0a183-150">在生成期间自动生成包</span><span class="sxs-lookup"><span data-stu-id="0a183-150">Automatically generate package on build</span></span>

<span data-ttu-id="0a183-151">若要在生成和还原项目时自动运行 `msbuild -t:pack`，请将以下行添加到 `<PropertyGroup>` 中的项目文件内：</span><span class="sxs-lookup"><span data-stu-id="0a183-151">To automatically run `msbuild -t:pack` when you build or restore the project, add the following line to your project file within `<PropertyGroup>`:</span></span>

```xml
<GeneratePackageOnBuild>true</GeneratePackageOnBuild>
```

<span data-ttu-id="0a183-152">在解决方案上运行 `msbuild -t:pack` 时，会打包解决方案中可打包的所有项目（[<IsPackable>](/dotnet/core/tools/csproj#nuget-metadata-properties) 属性设置为 `true`）。</span><span class="sxs-lookup"><span data-stu-id="0a183-152">When you run `msbuild -t:pack` on a solution, this packs all the projects in the solution that are packable ([<IsPackable>](/dotnet/core/tools/csproj#nuget-metadata-properties) property is set to `true`).</span></span>

> [!NOTE]
> <span data-ttu-id="0a183-153">自动生成包时，打包时间会增加项目的生成时间。</span><span class="sxs-lookup"><span data-stu-id="0a183-153">When you automatically generate the package, the time to pack increases the build time for your project.</span></span>

### <a name="test-package-installation"></a><span data-ttu-id="0a183-154">测试包安装</span><span class="sxs-lookup"><span data-stu-id="0a183-154">Test package installation</span></span>

<span data-ttu-id="0a183-155">发布包前，通常需要测试将包安装到项目的过程。</span><span class="sxs-lookup"><span data-stu-id="0a183-155">Before publishing a package, you typically want to test the process of installing a package into a project.</span></span> <span data-ttu-id="0a183-156">测试确保所有文件一定在项目中正确的位置结束。</span><span class="sxs-lookup"><span data-stu-id="0a183-156">The tests make sure that the necessarily files all end up in their correct places in the project.</span></span>

<span data-ttu-id="0a183-157">可以在 Visual Studio 中手动测试安装，或是使用常规[包安装步骤](../consume-packages/overview-and-workflow.md#ways-to-install-a-nuget-package)在命令行上测试。</span><span class="sxs-lookup"><span data-stu-id="0a183-157">You can test installations manually in Visual Studio or on the command line using the normal [package installation steps](../consume-packages/overview-and-workflow.md#ways-to-install-a-nuget-package).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="0a183-158">包是不可变的。</span><span class="sxs-lookup"><span data-stu-id="0a183-158">Packages are immutable.</span></span> <span data-ttu-id="0a183-159">如果更正了问题，请更改包的内容并再次打包，重新测试时，仍将使用旧版本的包，直到[清除全局包](../consume-packages/managing-the-global-packages-and-cache-folders.md#clearing-local-folders)文件夹。</span><span class="sxs-lookup"><span data-stu-id="0a183-159">If you correct a problem, change the contents of the package and pack again, when you retest you will still be using the old version of the package until you [clear your global packages](../consume-packages/managing-the-global-packages-and-cache-folders.md#clearing-local-folders) folder.</span></span> <span data-ttu-id="0a183-160">在测试每次生成时不使用唯一预发布标签的包时，这尤为重要。</span><span class="sxs-lookup"><span data-stu-id="0a183-160">This is especially relevant when testing packages that don't use a unique prerelease label on every build.</span></span>

## <a name="next-steps"></a><span data-ttu-id="0a183-161">后续步骤</span><span class="sxs-lookup"><span data-stu-id="0a183-161">Next Steps</span></span>

<span data-ttu-id="0a183-162">创建包（`.nupkg` 文件）后，可以将其发布到选择的库，如[发布包](../nuget-org/publish-a-package.md)中所述。</span><span class="sxs-lookup"><span data-stu-id="0a183-162">Once you've created a package, which is a `.nupkg` file, you can publish it to the gallery of your choice as described on [Publishing a Package](../nuget-org/publish-a-package.md).</span></span>

<span data-ttu-id="0a183-163">你可能还希望扩展包的功能，或者支持其他方案，如以下主题所述：</span><span class="sxs-lookup"><span data-stu-id="0a183-163">You might also want to extend the capabilities of your package or otherwise support other scenarios as described in the following topics:</span></span>

- [<span data-ttu-id="0a183-164">作为 MSBuild 目标的 NuGet 包和还原</span><span class="sxs-lookup"><span data-stu-id="0a183-164">NuGet pack and restore as MSBuild targets</span></span>](../reference/msbuild-targets.md)
- [<span data-ttu-id="0a183-165">包版本控制</span><span class="sxs-lookup"><span data-stu-id="0a183-165">Package versioning</span></span>](../concepts/package-versioning.md)
- [<span data-ttu-id="0a183-166">支持多个目标框架</span><span class="sxs-lookup"><span data-stu-id="0a183-166">Support multiple target frameworks</span></span>](../create-packages/multiple-target-frameworks-project-file.md)
- [<span data-ttu-id="0a183-167">源和配置文件的转换</span><span class="sxs-lookup"><span data-stu-id="0a183-167">Transformations of source and configuration files</span></span>](../create-packages/source-and-config-file-transformations.md)
- [<span data-ttu-id="0a183-168">本地化</span><span class="sxs-lookup"><span data-stu-id="0a183-168">Localization</span></span>](../create-packages/creating-localized-packages.md)
- [<span data-ttu-id="0a183-169">预发布版本</span><span class="sxs-lookup"><span data-stu-id="0a183-169">Pre-release versions</span></span>](../create-packages/prerelease-packages.md)
- [<span data-ttu-id="0a183-170">设置包类型</span><span class="sxs-lookup"><span data-stu-id="0a183-170">Set package type</span></span>](../create-packages/set-package-type.md)
- [<span data-ttu-id="0a183-171">使用 COM 互操作程序集创建包</span><span class="sxs-lookup"><span data-stu-id="0a183-171">Create packages with COM interop assemblies</span></span>](../create-packages/author-packages-with-COM-interop-assemblies.md)

<span data-ttu-id="0a183-172">最后，有需要注意的其他包类型：</span><span class="sxs-lookup"><span data-stu-id="0a183-172">Finally, there are additional package types to be aware of:</span></span>

- [<span data-ttu-id="0a183-173">本机包</span><span class="sxs-lookup"><span data-stu-id="0a183-173">Native Packages</span></span>](../guides/native-packages.md)
- [<span data-ttu-id="0a183-174">符号包</span><span class="sxs-lookup"><span data-stu-id="0a183-174">Symbol Packages</span></span>](../create-packages/symbol-packages-snupkg.md)