---
title: 使用 MSBuild 创建 NuGet 包
description: 设计和创建 NuGet 包流程的详细指南，包含文件和版本控制等关键决策点。
author: karann-msft
ms.author: karann
ms.date: 08/05/2019
ms.topic: conceptual
ms.openlocfilehash: b45c25a92c0134228fb507ab321cb00ce156527f
ms.sourcegitcommit: 39f2ae79fbbc308e06acf67ee8e24cfcdb2c831b
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/05/2019
ms.locfileid: "73610559"
---
# <a name="create-a-nuget-package-using-msbuild"></a>使用 MSBuild 创建 NuGet 包

从代码中创建 NuGet 包时，会将该功能打包到一个组件中，该组件可以与任意数量的其他开发人员共享和使用。 本文介绍如何使用 MSBuild 创建包。 MSBuild 预安装了包含 NuGet 的所有 Visual Studio 工作负荷。 此外，还可以通过 dotnet CLI 借助 [dotnet msbuild](https://docs.microsoft.com/dotnet/core/tools/dotnet-msbuild) 来使用 MSBuild。

对于使用 [SDK 样式格式](../resources/check-project-format.md)的 .NET Core 和 .NET Standard 项目，以及任何其他 SDK 样式项目，NuGet 直接使用项目文件中的信息创建包。  对于使用 `<PackageReference>` 的非 SDK 样式的项目，NuGet 还使用项目文件来创建包。

默认情况下，SDK 样式的项目具有可用的包功能。 对于非 SDK 样式的 PackageReference 项目，需要将 NuGet.Build.Tasks.Pack 包添加到项目依赖项中。 有关 MSBuild 包目标的详细信息，请参阅[作为 MSBuild 目标的 NuGet 包和还原](../reference/msbuild-targets.md)。

用于创建包的命令 `msbuild -t:pack`，其功能相当于 `dotnet pack`。

> [!IMPORTANT]
> 本主题适用于 [SDK 样式](../resources/check-project-format.md)的项目（通常是 .NET Core 和 .NET Standard 项目）以及使用 PackageReference 的非 SDK 样式的项目。

## <a name="set-properties"></a>设置属性

创建包需要以下属性。

- `PackageId`，包标识符，在托管包的库中必须是唯一的。 如果未指定，默认值为 `AssemblyName`。
- `Version`，窗体 Major.Minor.Patch[-Suffix] 中特定的版本号，其中 -Suffix 标识[预发布版本](prerelease-packages.md)   。 如果未指定，默认值为 1.0.0。
- 包标题应出现在主机上（例如 nuget.org）
- `Authors`，作者和所有者信息。 如果未指定，默认值为 `AssemblyName`。
- `Company`，公司名称。 如果未指定，默认值为 `AssemblyName`。

在 Visual Studio 中，可以在项目属性中设置这些值（在解决方案资源管理器中右键单击项目，选择“属性”  ，然后选择“包”  选项卡）。 也可以直接在项目文件 (.csproj) 中设置这些属性  。

```xml
<PropertyGroup>
  <PackageId>ClassLibDotNetStandard</PackageId>
  <Version>1.0.0</Version>
  <Authors>your_name</Authors>
  <Company>your_company</Company>
</PropertyGroup>
```

> [!Important]
> 为包提供一个在 nuget.org 中唯一或你使用的任何包资源的标识符。

以下示例显示了包含这些属性的简单、完整的项目文件。

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

另外，还可以设置可选属性，例如 `Title`、`PackageDescription` 和 `PackageTags`，如 [MSBuild 包目标](../reference/msbuild-targets.md#pack-target)、[控制依赖项资产](../consume-packages/package-references-in-project-files.md#controlling-dependency-assets)和 [NuGet 元数据属性](/dotnet/core/tools/csproj#nuget-metadata-properties)中所述。

> [!NOTE]
> 对于面向公共使用而生成的包，请特别注意 **PackageTags** 属性，因为这些标记可帮助其他人查找包并了解其用途。

有关声明依赖项并指定版本号的详细信息，请参阅[项目文件中的包引用](../consume-packages/package-references-in-project-files.md)和[包版本控制](../concepts/package-versioning.md)。 还可以使用 `<IncludeAssets>` 和 `<ExcludeAssets>` 特性直接在包中呈现依赖项的资产。 有关详细信息，请参阅[控制依赖项资产](../consume-packages/package-references-in-project-files.md#controlling-dependency-assets)。

## <a name="choose-a-unique-package-identifier-and-set-the-version-number"></a>选择唯一的包标识符并设置版本号

[!INCLUDE [choose-package-id](includes/choose-package-id.md)]

## <a name="add-the-nugetbuildtaskspack-package"></a>添加 NuGet.Build.Tasks.Pack 包

如果将 MSBuild 与非 SDK 样式项目和 PackageReference 一起使用，请将 NuGet.Build.Tasks.Pack 包添加到项目中。

1. 打开项目文件并在 `<PropertyGroup>` 元素后面添加以下内容：

   ```xml
   <ItemGroup>
     <!-- ... -->
     <PackageReference Include="NuGet.Build.Tasks.Pack" Version="5.2.0"/>
     <!-- ... -->
   </ItemGroup>
   ```

2. 打开开发人员命令提示符（在“搜索”框中，键入“开发人员命令提示符”）   。

   用户通常习惯从“开始”菜单中启动“适用于 Visual Studio 的开发人员命令提示符”，因为它将使用 MSBuild 的所有必需路径进行配置  。

3. 切换到包含项目文件的文件夹，然后键入以下命令以安装 NuGet.Build.Tasks.Pack 包。

   ```cmd
   # Uses the project file in the current folder by default
   msbuild -t:restore
   ```

   确保 MSBuild 输出指示生成已成功完成。

## <a name="run-the-msbuild--tpack-command"></a>运行 msbuild -t:pack 命令

若要从项目中生成 NuGet 包（`.nupkg` 文件），运行 `msbuild -t:pack` 命令，它也会自动生成项目：

在 Visual Studio 开发人员命令提示处，键入以下命令：

```cmd
# Uses the project file in the current folder by default
msbuild -t:pack
```

输出将显示 `.nupkg` 文件的路径。

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

### <a name="automatically-generate-package-on-build"></a>在生成期间自动生成包

若要在生成和还原项目时自动运行 `msbuild -t:pack`，请将以下行添加到 `<PropertyGroup>` 中的项目文件内：

```xml
<GeneratePackageOnBuild>true</GeneratePackageOnBuild>
```

在解决方案上运行 `msbuild -t:pack` 时，会打包解决方案中可打包的所有项目（[<IsPackable>](/dotnet/core/tools/csproj#nuget-metadata-properties) 属性设置为 `true`）。

> [!NOTE]
> 自动生成包时，打包时间会增加项目的生成时间。

### <a name="test-package-installation"></a>测试包安装

发布包前，通常需要测试将包安装到项目的过程。 测试确保所有文件一定在项目中正确的位置结束。

可以在 Visual Studio 中手动测试安装，或是使用常规[包安装步骤](../consume-packages/overview-and-workflow.md#ways-to-install-a-nuget-package)在命令行上测试。

> [!IMPORTANT]
> 包是不可变的。 如果更正了问题，请更改包的内容并再次打包，重新测试时，仍将使用旧版本的包，直到[清除全局包](../consume-packages/managing-the-global-packages-and-cache-folders.md#clearing-local-folders)文件夹。 在测试每次生成时不使用唯一预发布标签的包时，这尤为重要。

## <a name="next-steps"></a>后续步骤

创建包（`.nupkg` 文件）后，可以将其发布到选择的库，如[发布包](../nuget-org/publish-a-package.md)中所述。

你可能还希望扩展包的功能，或者支持其他方案，如以下主题所述：

- [作为 MSBuild 目标的 NuGet 包和还原](../reference/msbuild-targets.md)
- [包版本控制](../concepts/package-versioning.md)
- [支持多个目标框架](../create-packages/multiple-target-frameworks-project-file.md)
- [源和配置文件的转换](../create-packages/source-and-config-file-transformations.md)
- [本地化](../create-packages/creating-localized-packages.md)
- [预发布版本](../create-packages/prerelease-packages.md)
- [设置包类型](../create-packages/set-package-type.md)
- [使用 COM 互操作程序集创建包](../create-packages/author-packages-with-COM-interop-assemblies.md)

最后，有需要注意的其他包类型：

- [本机包](../guides/native-packages.md)
- [符号包](../create-packages/symbol-packages-snupkg.md)
