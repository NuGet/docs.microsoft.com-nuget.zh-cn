---
title: 项目文件中 NuGet 包的多目标
description: 介绍从一个 NuGet 包中以多个 .NET Framework 版本为目标的各种方法。
author: karann-msft
ms.author: karann
ms.date: 07/15/2019
ms.topic: conceptual
ms.openlocfilehash: 1d23759433efb405fa5f0035049befced2c43d6b
ms.sourcegitcommit: 363ec6843409b4714c91b75b105619a3a3184b43
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/16/2019
ms.locfileid: "72380679"
---
# <a name="support-multiple-net-framework-versions-in-your-project-file"></a>支持项目文件中的多个 .NET Framework 版本

首次创建项目时，建议创建 .NET Standard 类库，因为它提供了与最广泛使用项目的兼容性。 使用 .NET Standard 可以默认向 .NET 库添加[跨平台支持](/dotnet/standard/library-guidance/cross-platform-targeting)。 但是，在某些情况下，可能还需要包含针对特定框架的代码。 本文介绍如何针对 [SDK 样式](../resources/check-project-format.md)的项目执行该操作。

对于 SDK 样式的项目，可以在项目文件中配置对多个目标框架 ([TFM](/dotnet/standard/frameworks)) 的支持，然后使用`dotnet pack` 或 `msbuild /t:pack` 创建包。

> [!NOTE]
> nuget.exe CLI 不支持打包 SDK 样式的项目，因此应只使用 `dotnet pack` 或 `msbuild /t:pack`。 我们建议改为[包含所有属性](../reference/msbuild-targets.md#pack-target)（项目文件的 `.nuspec` 文件中通常包含的所有属性）。 要在非 SDK 样式的项目中以多个 .NET Framework 版本为目标，请参阅[支持多个 .NET Framework 版本](supporting-multiple-target-frameworks.md)。

## <a name="create-a-project-that-supports-multiple-net-framework-versions"></a>创建一个支持多个 .NET Framework 版本的项目

1. 在 Visual Studio 中或使用 `dotnet new classlib` 创建新的 .NET Standard 类库。

   建议创建 .NET Standard 类库以获得最佳兼容性。

2. 编辑 .csproj  文件以支持目标框架。 例如，更改
   
   `<TargetFramework>netstandard2.0</TargetFramework>`
   
   更改为：
   
   `<TargetFrameworks>netstandard2.0;net45</TargetFrameworks>`

   确保将 XML 元素从单数更改为复数（将“s”添加到开始和结束标记）。

3. 如果你有任何仅在一个 TFM 中工作的代码，则可以使用 `#if NET45` 或 `#if NETSTANDARD2_0` 分隔与 TFM 相关的代码。 （有关详细信息，请参阅[如何实现多目标](/dotnet/core/tutorials/libraries#how-to-multitarget)。）例如，可以使用以下代码：

   ```csharp
   public string Platform {
      get {
   #if NET45
         return ".NET Framework"
   #elif NETSTANDARD2_0
         return ".NET Standard"
   #else
   #error This code block does not match csproj TargetFrameworks list
   #endif
      }
   }
   ```

4. 将你需要的任何 NuGet 元数据添加到 .csproj  作为 MSBuild 属性。

   有关可用包元数据和 MSBuild 属性名称的列表，请参阅 [pack 目标](../reference/msbuild-targets.md#pack-target)。 另请参阅[控制依赖项资产](../consume-packages/package-references-in-project-files.md#controlling-dependency-assets)。

   如果要将与生成相关的属性与 NuGet 元数据分开，可以使用不同的 `PropertyGroup`，或将 NuGet 属性放在另一个文件中，并使用 MSBuild 的 `Import` 指令将其包含在内。 从 MSBuild 15.0. 开始，还支持 `Directory.Build.Props` 和 `Directory.Build.Targets`。

5. 现在，使用 `dotnet pack` 和生成的 .nupkg  以 .NET Standard 2.0 和 .NET Framework 4.5 为目标。

以下是使用上述步骤和 .NET Core SDK 2.2 生成的 .csproj  文件。

```xml
<Project Sdk="Microsoft.NET.Sdk">

  <PropertyGroup>
    <TargetFrameworks>netstandard2.0;net45</TargetFrameworks>
    <Description>Sample project that targets multiple TFMs</Description>
  </PropertyGroup>

</Project>
```

## <a name="see-also"></a>请参阅

* [如何指定目标框架](/dotnet/standard/frameworks#how-to-specify-target-frameworks)
* [跨平台定位](/dotnet/standard/library-guidance/cross-platform-targeting)
