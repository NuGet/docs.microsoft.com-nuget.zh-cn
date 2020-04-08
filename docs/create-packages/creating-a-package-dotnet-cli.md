---
title: 使用 dotnet CLI 创建 NuGet 包
description: 设计和创建 NuGet 包流程的详细指南，包含文件和版本控制等关键决策点。
author: karann-msft
ms.author: karann
ms.date: 02/20/2020
ms.topic: conceptual
ms.openlocfilehash: 712e4c7159aa9719052330d8e45f63e18e390325
ms.sourcegitcommit: 2b50c450cca521681a384aa466ab666679a40213
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/07/2020
ms.locfileid: "78230566"
---
# <a name="create-a-nuget-package-using-the-dotnet-cli"></a>使用 dotnet CLI 创建 NuGet 包

无论包是什么用途或者它包含什么代码，均使用其中一个 CLI 工具（`nuget.exe` 或 `dotnet.exe`）将该功能打包进可以与任意数量的其他开发人员共享且可以由其使用的组件中。 本文介绍如何使用 dotnet CLI 创建包。 若要安装 `dotnet` CLI，请参阅[安装 NuGet 客户端工具](../install-nuget-client-tools.md)。 从 Visual Studio 2017 开始，dotnet CLI 包含在 .NET Core 工作负载中。

对于使用 [SDK 样式格式](../resources/check-project-format.md)的 .NET Core 和 .NET Standard 项目，以及任何其他 SDK 样式项目，NuGet 直接使用项目文件中的信息创建包。 若要查看分步教程，请参阅[使用 dotnet CLI 创建 .NET Standard 包](../quickstart/create-and-publish-a-package-using-the-dotnet-cli.md)或[使用 Visual Studio 创建 .NET Standard 包](../quickstart/create-and-publish-a-package-using-visual-studio.md)。

`msbuild -t:pack` 在功能上等效于 `dotnet pack`。 若要使用 MSBuild 进行生成，请参阅 [使用 MSBuild 创建 NuGet 包](creating-a-package-msbuild.md)。

> [!IMPORTANT]
> 本主题适用于 [ SDK 样式](../resources/check-project-format.md)的项目，通常是 .NET Core 和 .NET Standard 项目。

## <a name="set-properties"></a>设置属性

创建包需要以下属性。

- `PackageId`，包标识符，在托管包的库中必须是唯一的。 如果未指定，默认值为 `AssemblyName`。
- `Version`，窗体 Major.Minor.Patch[-Suffix] 中特定的版本号，其中 -Suffix 标识[预发布版本](prerelease-packages.md)   。 如果未指定，默认值为 1.0.0。
- 包标题应出现在主机上（例如 nuget.org）
- `Authors`，作者和所有者信息。 如果未指定，默认值为 `AssemblyName`。
- `Company`，公司名称。 如果未指定，默认值为 `AssemblyName`。

在 Visual Studio 中，可以在项目属性中设置这些值（在解决方案资源管理器中右键单击项目，选择“属性”  ，然后选择“包”  选项卡）。 也可以直接在项目文件 (`.csproj`) 中设置这些属性。

```xml
<PropertyGroup>
  <PackageId>AppLogger</PackageId>
  <Version>1.0.0</Version>
  <Authors>your_name</Authors>
  <Company>your_company</Company>
</PropertyGroup>
```

> [!Important]
> 为包提供一个在 nuget.org 中唯一或你使用的任何包资源的标识符。

以下示例显示了包含这些属性的简单、完整的项目文件。 （可以使用 `dotnet new classlib` 命令创建新的默认项目。）

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

另外，还可以设置可选属性，例如 `Title`、`PackageDescription` 和 `PackageTags`，如 [MSBuild 包目标](../reference/msbuild-targets.md#pack-target)、[控制依赖项资产](../consume-packages/package-references-in-project-files.md#controlling-dependency-assets)和 [NuGet 元数据属性](/dotnet/core/tools/csproj#nuget-metadata-properties)中所述。

> [!NOTE]
> 对于面向公共使用而生成的包，请特别注意 **PackageTags** 属性，因为这些标记可帮助其他人查找包并了解其用途。

有关声明依赖项并指定版本号的详细信息，请参阅[项目文件中的包引用](../consume-packages/package-references-in-project-files.md)和[包版本控制](../concepts/package-versioning.md)。 还可以使用 `<IncludeAssets>` 和 `<ExcludeAssets>` 特性直接在包中呈现依赖项的资产。 有关详细信息，请参阅[控制依赖项资产](../consume-packages/package-references-in-project-files.md#controlling-dependency-assets)。

## <a name="add-an-optional-description-field"></a>添加可选说明字段

[!INCLUDE [add description to package](includes/add-description.md)]

## <a name="choose-a-unique-package-identifier-and-set-the-version-number"></a>选择唯一的包标识符并设置版本号

[!INCLUDE [choose-package-id](includes/choose-package-id.md)]

## <a name="run-the-pack-command"></a>运行 pack 命令

若要从项目中生成 NuGet 包（`.nupkg` 文件），运行 `dotnet pack` 命令，它也会自动生成项目：

```dotnetcli
# Uses the project file in the current folder by default
dotnet pack
```

输出将显示 `.nupkg` 文件的路径。

```output
Microsoft (R) Build Engine version 15.5.180.51428 for .NET Core
Copyright (C) Microsoft Corporation. All rights reserved.

  Restore completed in 29.91 ms for D:\proj\AppLoggerNet\AppLogger\AppLogger.csproj.
  AppLogger -> D:\proj\AppLoggerNet\AppLogger\bin\Debug\netstandard2.0\AppLogger.dll
  Successfully created package 'D:\proj\AppLoggerNet\AppLogger\bin\Debug\AppLogger.1.0.0.nupkg'.
```

### <a name="automatically-generate-package-on-build"></a>在生成期间自动生成包

若要在运行 `dotnet build` 时自动运行 `dotnet pack`，请将以下行添加到 `<PropertyGroup>` 中的项目文件内：

```xml
<GeneratePackageOnBuild>true</GeneratePackageOnBuild>
```

在解决方案上运行 `dotnet pack` 时，会打包解决方案中可打包的所有项目（[<IsPackable>](/dotnet/core/tools/csproj#nuget-metadata-properties) 属性设置为 `true`）。

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

- [包版本控制](../concepts/package-versioning.md)
- [支持多个目标框架](../create-packages/multiple-target-frameworks-project-file.md)
- [添加包图标](../reference/nuspec.md#icon)
- [源和配置文件的转换](../create-packages/source-and-config-file-transformations.md)
- [本地化](../create-packages/creating-localized-packages.md)
- [预发布版本](../create-packages/prerelease-packages.md)
- [设置包类型](../create-packages/set-package-type.md)
- [使用 COM 互操作程序集创建包](../create-packages/author-packages-with-COM-interop-assemblies.md)

最后，有需要注意的其他包类型：

- [本机包](../guides/native-packages.md)
- [符号包](../create-packages/symbol-packages-snupkg.md)
