---
title: 项目文件中 NuGet 包的多目标
description: 介绍从项目文件的一个 NuGet 包中以多个 .NET Framework 版本为目标的各种方法。
author: JonDouglas
ms.author: jodou
ms.date: 07/15/2019
ms.topic: conceptual
ms.openlocfilehash: a05d053340bb2fe795991dfa5a2b95d8625dfd44
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/26/2021
ms.locfileid: "98774376"
---
# <a name="support-multiple-net-framework-versions-in-your-project-file"></a><span data-ttu-id="c0e62-103">支持项目文件中的多个 .NET Framework 版本</span><span class="sxs-lookup"><span data-stu-id="c0e62-103">Support multiple .NET Framework versions in your project file</span></span>

<span data-ttu-id="c0e62-104">首次创建项目时，建议创建 .NET Standard 类库，因为它提供了与最广泛使用项目的兼容性。</span><span class="sxs-lookup"><span data-stu-id="c0e62-104">When you first create a project, we recommend you create a .NET Standard class library, as it provides compatibility with the widest range of consuming projects.</span></span> <span data-ttu-id="c0e62-105">使用 .NET Standard 可以默认向 .NET 库添加[跨平台支持](/dotnet/standard/library-guidance/cross-platform-targeting)。</span><span class="sxs-lookup"><span data-stu-id="c0e62-105">By using .NET Standard, you add [cross-platform support](/dotnet/standard/library-guidance/cross-platform-targeting) to a .NET library by default.</span></span> <span data-ttu-id="c0e62-106">但是，在某些情况下，可能还需要包含针对特定框架的代码。</span><span class="sxs-lookup"><span data-stu-id="c0e62-106">However, in some scenarios, you may also need to include code that targets a particular framework.</span></span> <span data-ttu-id="c0e62-107">本文介绍如何针对 [SDK 样式](../resources/check-project-format.md)的项目执行该操作。</span><span class="sxs-lookup"><span data-stu-id="c0e62-107">This article shows you how to do that for [SDK-style](../resources/check-project-format.md) projects.</span></span>

<span data-ttu-id="c0e62-108">对于 SDK 样式的项目，可以在项目文件中配置对多个目标框架 ([TFM](/dotnet/standard/frameworks)) 的支持，然后使用`dotnet pack` 或 `msbuild /t:pack` 创建包。</span><span class="sxs-lookup"><span data-stu-id="c0e62-108">For SDK-style projects, you can configure support for multiple targets frameworks ([TFM](/dotnet/standard/frameworks)) in your project file, then use `dotnet pack` or `msbuild /t:pack` to create the package.</span></span>

> [!NOTE]
> <span data-ttu-id="c0e62-109">nuget.exe CLI 不支持打包 SDK 样式的项目，因此应只使用 `dotnet pack` 或 `msbuild /t:pack`。</span><span class="sxs-lookup"><span data-stu-id="c0e62-109">nuget.exe CLI does not support packing SDK-style projects, so you should only use `dotnet pack` or `msbuild /t:pack`.</span></span> <span data-ttu-id="c0e62-110">我们建议改为[包含所有属性](../reference/msbuild-targets.md#pack-target)（项目文件的 `.nuspec` 文件中通常包含的所有属性）。</span><span class="sxs-lookup"><span data-stu-id="c0e62-110">We recommend that you [include all the properties](../reference/msbuild-targets.md#pack-target) that are usually in the `.nuspec` file in the project file instead.</span></span> <span data-ttu-id="c0e62-111">要在非 SDK 样式的项目中以多个 .NET Framework 版本为目标，请参阅[支持多个 .NET Framework 版本](supporting-multiple-target-frameworks.md)。</span><span class="sxs-lookup"><span data-stu-id="c0e62-111">To target multiple .NET Framework versions in a non-SDK-style project, see [Supporting multiple .NET Framework versions](supporting-multiple-target-frameworks.md).</span></span>

## <a name="create-a-project-that-supports-multiple-net-framework-versions"></a><span data-ttu-id="c0e62-112">创建一个支持多个 .NET Framework 版本的项目</span><span class="sxs-lookup"><span data-stu-id="c0e62-112">Create a project that supports multiple .NET Framework versions</span></span>

1. <span data-ttu-id="c0e62-113">在 Visual Studio 中或使用 `dotnet new classlib` 创建新的 .NET Standard 类库。</span><span class="sxs-lookup"><span data-stu-id="c0e62-113">Create a new .NET Standard class library either in Visual Studio or use `dotnet new classlib`.</span></span>

   <span data-ttu-id="c0e62-114">建议创建 .NET Standard 类库以获得最佳兼容性。</span><span class="sxs-lookup"><span data-stu-id="c0e62-114">We recommend that you create a .NET Standard class library for best compatibility.</span></span>

2. <span data-ttu-id="c0e62-115">编辑 .csproj  文件以支持目标框架。</span><span class="sxs-lookup"><span data-stu-id="c0e62-115">Edit the *.csproj* file to support the target frameworks.</span></span> <span data-ttu-id="c0e62-116">例如，更改</span><span class="sxs-lookup"><span data-stu-id="c0e62-116">For example, change</span></span>
   
   `<TargetFramework>netstandard2.0</TargetFramework>`
   
   <span data-ttu-id="c0e62-117">更改为：</span><span class="sxs-lookup"><span data-stu-id="c0e62-117">to:</span></span>
   
   `<TargetFrameworks>netstandard2.0;net45</TargetFrameworks>`

   <span data-ttu-id="c0e62-118">确保将 XML 元素从单数更改为复数（将“s”添加到开始和结束标记）。</span><span class="sxs-lookup"><span data-stu-id="c0e62-118">Make sure that you change the XML element changed from singular to plural (add the "s" to both the open and close tags).</span></span>

3. <span data-ttu-id="c0e62-119">如果你有任何仅在一个 TFM 中工作的代码，则可以使用 `#if NET45` 或 `#if NETSTANDARD2_0` 分隔与 TFM 相关的代码。</span><span class="sxs-lookup"><span data-stu-id="c0e62-119">If you have any code that only works in one TFM, you can use `#if NET45` or `#if NETSTANDARD2_0` to separate TFM-dependent code.</span></span> <span data-ttu-id="c0e62-120">（有关详细信息，请参阅[如何实现多目标](/dotnet/core/tutorials/libraries#how-to-multitarget)。）例如，可以使用以下代码：</span><span class="sxs-lookup"><span data-stu-id="c0e62-120">(For more information, see [How to multitarget](/dotnet/core/tutorials/libraries#how-to-multitarget).) For example, you can use the following code:</span></span>

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

4. <span data-ttu-id="c0e62-121">将你需要的任何 NuGet 元数据添加到 .csproj  作为 MSBuild 属性。</span><span class="sxs-lookup"><span data-stu-id="c0e62-121">Add any NuGet metadata you want to the *.csproj* as MSBuild properties.</span></span>

   <span data-ttu-id="c0e62-122">有关可用包元数据和 MSBuild 属性名称的列表，请参阅 [pack 目标](../reference/msbuild-targets.md#pack-target)。</span><span class="sxs-lookup"><span data-stu-id="c0e62-122">For the list of available package metadata and the MSBuild property names, see [pack target](../reference/msbuild-targets.md#pack-target).</span></span> <span data-ttu-id="c0e62-123">另请参阅[控制依赖项资产](../consume-packages/package-references-in-project-files.md#controlling-dependency-assets)。</span><span class="sxs-lookup"><span data-stu-id="c0e62-123">Also see [Controlling dependency assets](../consume-packages/package-references-in-project-files.md#controlling-dependency-assets).</span></span>

   <span data-ttu-id="c0e62-124">如果要将与生成相关的属性与 NuGet 元数据分开，可以使用不同的 `PropertyGroup`，或将 NuGet 属性放在另一个文件中，并使用 MSBuild 的 `Import` 指令将其包含在内。</span><span class="sxs-lookup"><span data-stu-id="c0e62-124">If you want to separate build-related properties from NuGet metadata, you can use a different `PropertyGroup`, or put the NuGet properties in another file and use MSBuild's `Import` directive to include it.</span></span> <span data-ttu-id="c0e62-125">从 MSBuild 15.0. 开始，还支持 `Directory.Build.Props` 和 `Directory.Build.Targets`。</span><span class="sxs-lookup"><span data-stu-id="c0e62-125">`Directory.Build.Props` and `Directory.Build.Targets` are also supported starting with MSBuild 15.0.</span></span>

5. <span data-ttu-id="c0e62-126">现在，使用 `dotnet pack` 和生成的 .nupkg  以 .NET Standard 2.0 和 .NET Framework 4.5 为目标。</span><span class="sxs-lookup"><span data-stu-id="c0e62-126">Now, use `dotnet pack` and the resulting *.nupkg* targets both .NET Standard 2.0 and .NET Framework 4.5.</span></span>

<span data-ttu-id="c0e62-127">以下是使用上述步骤和 .NET Core SDK 2.2 生成的 .csproj  文件。</span><span class="sxs-lookup"><span data-stu-id="c0e62-127">Here is the *.csproj* file that is generated using the preceding steps and .NET Core SDK 2.2.</span></span>

```xml
<Project Sdk="Microsoft.NET.Sdk">

  <PropertyGroup>
    <TargetFrameworks>netstandard2.0;net45</TargetFrameworks>
    <Description>Sample project that targets multiple TFMs</Description>
  </PropertyGroup>

</Project>
```

## <a name="see-also"></a><span data-ttu-id="c0e62-128">请参阅</span><span class="sxs-lookup"><span data-stu-id="c0e62-128">See also</span></span>

* [<span data-ttu-id="c0e62-129">如何指定目标框架</span><span class="sxs-lookup"><span data-stu-id="c0e62-129">How to specify target frameworks</span></span>](/dotnet/standard/frameworks#how-to-specify-target-frameworks)
* [<span data-ttu-id="c0e62-130">跨平台定位</span><span class="sxs-lookup"><span data-stu-id="c0e62-130">Cross-platform targeting</span></span>](/dotnet/standard/library-guidance/cross-platform-targeting)
