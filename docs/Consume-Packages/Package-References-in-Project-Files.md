---
title: "Visual Studio 项目文件中的 NuGet PackageReference | Microsoft Docs"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 7/17/2017
ms.topic: article
ms.prod: nuget
ms.technology: 
ms.assetid: 5a554e9d-1266-48c2-92e8-6dd00b1d6810
description: "详细介绍项目文件中 NuGet 4.0+ 和 VS2017 支持的 NuGet PackageReference"
keywords: "NuGet 包依赖项, 包引用, 项目文件, PackageReference, packages.config, project.json, VS2017, Visual Studio 2017, NuGet 4"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: c8fc9e558557af444d9a35ace36d043a5f6382a7
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/14/2017
---
# <a name="package-references-packagereference-in-project-files"></a><span data-ttu-id="13cda-104">项目文件中的包引用 (PackageReference)</span><span class="sxs-lookup"><span data-stu-id="13cda-104">Package references (PackageReference) in project files</span></span>

<span data-ttu-id="13cda-105">使用 `PackageReference` 节点的包引用允许直接在项目文件中管理 NuGet 依赖项，无需单独的 `packages.config` 或 `project.json` 文件。</span><span class="sxs-lookup"><span data-stu-id="13cda-105">Package references, using the `PackageReference` node, allow you to manage NuGet dependencies directly within project files, rather than needing a separate `packages.config` or `project.json` file.</span></span> <span data-ttu-id="13cda-106">此方法不会影响 NuGet 的其他方面，例如，仍按照[配置 NuGet 行为](Configuring-NuGet-Behavior.md)中的说明应用 `NuGet.Config` 文件（包括包源）中的设置。</span><span class="sxs-lookup"><span data-stu-id="13cda-106">This method doesn't affect other aspects of NuGet; for example, settings in `NuGet.Config` files (including package sources) are still applied as explained in [Configuring NuGet Behavior](Configuring-NuGet-Behavior.md).</span></span>

> [!Important]
> <span data-ttu-id="13cda-107">目前，仅在 Visual Studio 2017 中支持将包引用用于 .NET Core 项目、.NET Standard 项目以及面向 Windows 10 Build 15063（创建者更新）的 UWP 项目。</span><span class="sxs-lookup"><span data-stu-id="13cda-107">At present, package references are supported in Visual Studio 2017 only, for .NET Core projects, .NET Standard projects, and UWP projects targeting Windows 10 Build 15063 (Creators Update).</span></span>

<span data-ttu-id="13cda-108">`PackageReference` 方法允许使用 MSBuild 条件按目标框架、配置、平台或其他分组选择包引用。</span><span class="sxs-lookup"><span data-stu-id="13cda-108">The `PackageReference` approach allows you to use MSBuild conditions to choose package references per target framework, configuration, platform, or other groupings.</span></span> <span data-ttu-id="13cda-109">它还允许对依赖项和内容流实行精细控制。</span><span class="sxs-lookup"><span data-stu-id="13cda-109">It also allows for fine-grained control over dependencies and content flow.</span></span> <span data-ttu-id="13cda-110">在行为和[依赖项解析](Dependency-Resolution.md)方面，它与使用 `project.json` 相同。</span><span class="sxs-lookup"><span data-stu-id="13cda-110">In terms of behavior and [dependency resolution](Dependency-Resolution.md), it is the same as using `project.json`.</span></span>

<span data-ttu-id="13cda-111">有关 MSBuild 与项目文件中的包引用集成的更多详细信息，请参阅 [NuGet 打包和还原为 MSBuild 目标](../schema/msbuild-targets.md)。</span><span class="sxs-lookup"><span data-stu-id="13cda-111">For more details on the integration of MSBuild with package references in project files, see [NuGet pack and restore as MSBuild targets](../schema/msbuild-targets.md).</span></span>

## <a name="adding-a-packagereference"></a><span data-ttu-id="13cda-112">添加 PackageReference</span><span class="sxs-lookup"><span data-stu-id="13cda-112">Adding a PackageReference</span></span>

<span data-ttu-id="13cda-113">在项目文件中使用以下语法添加依赖项：</span><span class="sxs-lookup"><span data-stu-id="13cda-113">Add a dependency in your project file using the following syntax:</span></span>

```xml
<ItemGroup>
    <!-- ... -->
    <PackageReference Include="Contoso.Utility.UsefulStuff" Version="3.6.0" />    
    <!-- ... -->
</ItemGroup>
```

## <a name="controlling-dependency-version"></a><span data-ttu-id="13cda-114">控制依赖项版本</span><span class="sxs-lookup"><span data-stu-id="13cda-114">Controlling dependency version</span></span>

<span data-ttu-id="13cda-115">用于指定包版本的约定与使用 `packages.config` 或 `project.json` 时的约定相同：</span><span class="sxs-lookup"><span data-stu-id="13cda-115">The convention for specifying the version of a package is the same as when using `packages.config` or `project.json`:</span></span>

```xml
<ItemGroup>
    <!-- ... -->
    <PackageReference Include="Contoso.Utility.UsefulStuff" Version="3.6.0" />
    <!-- ... -->
</ItemGroup>
```

<span data-ttu-id="13cda-116">在上述示例中，3.6.0 指 >=3.6.0 的任何版本（首选项为最低版本），详见[包版本控制](../reference/package-versioning.md#version-ranges-and-wildcards)。</span><span class="sxs-lookup"><span data-stu-id="13cda-116">In the example above, 3.6.0 means any version that is >=3.6.0 with preference for the lowest version, as described on [Package versioning](../reference/package-versioning.md#version-ranges-and-wildcards).</span></span>

## <a name="floating-versions"></a><span data-ttu-id="13cda-117">可变版本</span><span class="sxs-lookup"><span data-stu-id="13cda-117">Floating Versions</span></span>

<span data-ttu-id="13cda-118">`PackageReference` 支持[可变版本](../consume-packages/dependency-resolution.md#floating-versions)：</span><span class="sxs-lookup"><span data-stu-id="13cda-118">[Floating versions](../consume-packages/dependency-resolution.md#floating-versions) are supported with `PackageReference`:</span></span>

```xml
<ItemGroup>
    <!-- ... -->
    <PackageReference Include="Contoso.Utility.UsefulStuff" Version="3.6.*" />
    <PackageReference Include="Contoso.Utility.UsefulStuff" Version="3.6.0-beta*" />
    <!-- ... -->
</ItemGroup>
```

## <a name="controlling-dependency-assets"></a><span data-ttu-id="13cda-119">控制依赖项资产</span><span class="sxs-lookup"><span data-stu-id="13cda-119">Controlling dependency assets</span></span>

<span data-ttu-id="13cda-120">你可能只是将依赖项用作开发工具，而不希望将它向会使用包的项目公开。</span><span class="sxs-lookup"><span data-stu-id="13cda-120">You might be using a dependency purely as a development harness and might not want to expose that to projects that will consume your package.</span></span> <span data-ttu-id="13cda-121">在此情况下，可使用 `PrivateAssets` 元数据控制此行为。</span><span class="sxs-lookup"><span data-stu-id="13cda-121">In this scenario, you can use the `PrivateAssets` metadata to control this behavior.</span></span>

```xml
<ItemGroup>
    <!-- ... -->

    <PackageReference Include="Contoso.Utility.UsefulStuff" Version="3.6.0">
        <PrivateAssets>all</PrivateAssets>
    </PackageReference>

    <!-- ... -->
</ItemGroup>
```

<span data-ttu-id="13cda-122">以下元数据标记控制依赖项资产：</span><span class="sxs-lookup"><span data-stu-id="13cda-122">The following metadata tags control dependency assets:</span></span>

| <span data-ttu-id="13cda-123">标记</span><span class="sxs-lookup"><span data-stu-id="13cda-123">Tag</span></span> | <span data-ttu-id="13cda-124">描述</span><span class="sxs-lookup"><span data-stu-id="13cda-124">Description</span></span> | <span data-ttu-id="13cda-125">默认值</span><span class="sxs-lookup"><span data-stu-id="13cda-125">Default Value</span></span> |
| --- | --- | --- |
| <span data-ttu-id="13cda-126">IncludeAssets</span><span class="sxs-lookup"><span data-stu-id="13cda-126">IncludeAssets</span></span> | <span data-ttu-id="13cda-127">将使用这些资产</span><span class="sxs-lookup"><span data-stu-id="13cda-127">These assets will be consumed</span></span> | <span data-ttu-id="13cda-128">全部</span><span class="sxs-lookup"><span data-stu-id="13cda-128">all</span></span> |
| <span data-ttu-id="13cda-129">ExcludeAssets</span><span class="sxs-lookup"><span data-stu-id="13cda-129">ExcludeAssets</span></span> | <span data-ttu-id="13cda-130">不会使用这些资产</span><span class="sxs-lookup"><span data-stu-id="13cda-130">These assets will not be consumed</span></span> | <span data-ttu-id="13cda-131">无</span><span class="sxs-lookup"><span data-stu-id="13cda-131">none</span></span> | 
| <span data-ttu-id="13cda-132">PrivateAssets</span><span class="sxs-lookup"><span data-stu-id="13cda-132">PrivateAssets</span></span> | <span data-ttu-id="13cda-133">将使用这些资产，但它们不会流入上级项目</span><span class="sxs-lookup"><span data-stu-id="13cda-133">These assets will be consumed but won't flow to the parent project</span></span> | <span data-ttu-id="13cda-134">contentfiles;analyzers;build</span><span class="sxs-lookup"><span data-stu-id="13cda-134">contentfiles;analyzers;build</span></span> |


<span data-ttu-id="13cda-135">以下是这些标记的允许值，其中用分号分隔多个值（但 `all` 和 `none` 必须单独显示）：</span><span class="sxs-lookup"><span data-stu-id="13cda-135">Allowable values for these tags are as follows, with multiple values separated by a semicolon except with `all` and `none` which must appear by themselves:</span></span>

| <span data-ttu-id="13cda-136">值</span><span class="sxs-lookup"><span data-stu-id="13cda-136">Value</span></span> | <span data-ttu-id="13cda-137">描述</span><span class="sxs-lookup"><span data-stu-id="13cda-137">Description</span></span> |
| --- | ---
| <span data-ttu-id="13cda-138">compile</span><span class="sxs-lookup"><span data-stu-id="13cda-138">compile</span></span> | <span data-ttu-id="13cda-139">`lib` 文件夹中的内容</span><span class="sxs-lookup"><span data-stu-id="13cda-139">Contents of the `lib` folder</span></span> |
| <span data-ttu-id="13cda-140">runtime</span><span class="sxs-lookup"><span data-stu-id="13cda-140">runtime</span></span> | <span data-ttu-id="13cda-141">`runtime` 文件夹中的内容</span><span class="sxs-lookup"><span data-stu-id="13cda-141">Contents of the `runtime` folder</span></span> |
| <span data-ttu-id="13cda-142">contentFiles</span><span class="sxs-lookup"><span data-stu-id="13cda-142">contentFiles</span></span> | <span data-ttu-id="13cda-143">`contentfiles` 文件夹中的内容</span><span class="sxs-lookup"><span data-stu-id="13cda-143">Contents of the `contentfiles` folder</span></span> |
| <span data-ttu-id="13cda-144">build</span><span class="sxs-lookup"><span data-stu-id="13cda-144">build</span></span> | <span data-ttu-id="13cda-145">`build` 文件夹中的属性和目标</span><span class="sxs-lookup"><span data-stu-id="13cda-145">Props and targets in the `build` folder</span></span> |
| <span data-ttu-id="13cda-146">analyzers</span><span class="sxs-lookup"><span data-stu-id="13cda-146">analyzers</span></span> | <span data-ttu-id="13cda-147">.NET 分析器</span><span class="sxs-lookup"><span data-stu-id="13cda-147">.NET analyzers</span></span> |
| <span data-ttu-id="13cda-148">native</span><span class="sxs-lookup"><span data-stu-id="13cda-148">native</span></span> | <span data-ttu-id="13cda-149">`native` 文件夹中的内容</span><span class="sxs-lookup"><span data-stu-id="13cda-149">Contents of the `native` folder</span></span> |
| <span data-ttu-id="13cda-150">none</span><span class="sxs-lookup"><span data-stu-id="13cda-150">none</span></span> | <span data-ttu-id="13cda-151">不使用以上任何内容。</span><span class="sxs-lookup"><span data-stu-id="13cda-151">None of the above are used.</span></span> |
| <span data-ttu-id="13cda-152">all</span><span class="sxs-lookup"><span data-stu-id="13cda-152">all</span></span> | <span data-ttu-id="13cda-153">以上都是（除 `none` 之外）</span><span class="sxs-lookup"><span data-stu-id="13cda-153">All of the above (except `none`)</span></span> |

<span data-ttu-id="13cda-154">在以下示例中，项目将使用除包中的内容文件之外的所有项，并且除内容文件和分析器之外的所有项均会流入上级项目。</span><span class="sxs-lookup"><span data-stu-id="13cda-154">In the following example, everything except the content files from the package would be consumed by the project and everything except content files and analyzers would flow to the parent project.</span></span>

```xml
<ItemGroup>
    <!-- ... -->

    <PackageReference Include="Contoso.Utility.UsefulStuff" Version="3.6.0">
        <IncludeAssets>all</IncludeAssets>
        <ExcludeAssets>contentFiles</ExcludeAssets>
        <PrivateAssets>contentFiles;analyzers</PrivateAssets>
    </PackageReference>

    <!-- ... -->
</ItemGroup>
```

<span data-ttu-id="13cda-155">请注意，因为 `PrivateAssets` 未包括 `build`，所以目标和属性将流入上级项目。</span><span class="sxs-lookup"><span data-stu-id="13cda-155">Note that because `build` is not included with `PrivateAssets`, targets and props *will* flow to the parent project.</span></span> <span data-ttu-id="13cda-156">例如，假设在生成名为 AppLogger 的 NuGet 包的项目中使用上述引用。</span><span class="sxs-lookup"><span data-stu-id="13cda-156">Consider, for example, that the reference above is used in a project that builds a NuGet package called AppLogger.</span></span> <span data-ttu-id="13cda-157">AppLogger 可以使用 `Contoso.Utility.UsefulStuff` 中的目标和属性，使用 AppLogger 的项目也可以。</span><span class="sxs-lookup"><span data-stu-id="13cda-157">AppLogger can consume the targets and props from `Contoso.Utility.UsefulStuff`, as can projects that consume AppLogger.</span></span>

## <a name="adding-a-packagereference-condition"></a><span data-ttu-id="13cda-158">添加 PackageReference 条件</span><span class="sxs-lookup"><span data-stu-id="13cda-158">Adding a PackageReference condition</span></span>

<span data-ttu-id="13cda-159">可使用条件控制是否包括包，在哪种条件可使用任何 MSBuild 变量或者目标或属性文件中定义的变量。</span><span class="sxs-lookup"><span data-stu-id="13cda-159">You can use a condition to control whether a package is included, where conditions can use any MSBuild variable or a variable defined in the targets or props file.</span></span> <span data-ttu-id="13cda-160">但目前仅支持 `TargetFramework` 变量。</span><span class="sxs-lookup"><span data-stu-id="13cda-160">However, at presently, only the `TargetFramework` variable is supported.</span></span>

<span data-ttu-id="13cda-161">例如，假设目标为 `netstandard1.4` 和 `net452`，但具有的依赖项仅适用于 `net452`。</span><span class="sxs-lookup"><span data-stu-id="13cda-161">For example, say you're targeting `netstandard1.4` as well as `net452` but have a dependency that is applicable only for `net452`.</span></span> <span data-ttu-id="13cda-162">在此情况下，你不希望使用包的 `netstandard1.4` 项目添加该不必要的依赖项。</span><span class="sxs-lookup"><span data-stu-id="13cda-162">In this case you don't want a `netstandard1.4` project that's consuming your package to add that unnecessary dependency.</span></span> <span data-ttu-id="13cda-163">要防止此情况，请在 `PackageReference` 上指定条件，如下所示：</span><span class="sxs-lookup"><span data-stu-id="13cda-163">To prevent this, you specify a condition on the `PackageReference` as follows:</span></span>

```xml
<ItemGroup>
    <!-- ... -->
    <PackageReference Include="Newtonsoft.json" Version="9.0.1" Condition="'$(TargetFramework)' == 'net452'" />    
    <!-- ... -->
</ItemGroup>
```

<span data-ttu-id="13cda-164">使用此项目生成的包会显示仅针对 `net452` 目标包括 Newtonsoft.json 作为依赖项：</span><span class="sxs-lookup"><span data-stu-id="13cda-164">A package built using this project will show that Newtonsoft.json is included as a dependency only for a `net452` target:</span></span>

![对 VS2017 的 PackageReference 应用条件的结果](media/PackageReference-Condition.png)

<span data-ttu-id="13cda-166">还可以在 `ItemGroup` 级别应用条件，并将其应用到所有子级 `PackageReference` 元素：</span><span class="sxs-lookup"><span data-stu-id="13cda-166">Conditions can also be applied at the `ItemGroup` level and will apply to all children `PackageReference` elements:</span></span>

```xml
<ItemGroup Condition = "'$(TargetFramework)' == 'net452'">
    <!-- ... -->
    <PackageReference Include="Newtonsoft.json" Version="9.0.1" />
    <PackageReference Include="Contoso.Utility.UsefulStuff" Version="3.6.0" />
    <!-- ... -->
</ItemGroup>
```
