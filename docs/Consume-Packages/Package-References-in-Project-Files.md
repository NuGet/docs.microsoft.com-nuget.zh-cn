---
title: NuGet PackageReference 格式（项目文件中的包引用）| Microsoft 文档
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 03/16/2018
ms.topic: article
ms.prod: nuget
ms.technology: ''
description: 详细介绍项目文件中 NuGet 4.0+、VS2017 和 .NET Core 2.0 支持的 NuGet PackageReference
keywords: NuGet 包依赖项, 包引用, 项目文件, PackageReference, packages.config, VS2017, Visual Studio 2017, NuGet 4, .NET Core 2.0
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: e1880c9b294e19ef1b71c7b17b02df8ff1cf1b73
ms.sourcegitcommit: 718e6cb88e45fa07c85d653f216bf92eaaf81625
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/20/2018
---
# <a name="package-references-packagereference-in-project-files"></a><span data-ttu-id="12001-104">项目文件中的包引用 (PackageReference)</span><span class="sxs-lookup"><span data-stu-id="12001-104">Package references (PackageReference) in project files</span></span>

<span data-ttu-id="12001-105">使用 `PackageReference` 节点的包引用可直接在项目文件中管理 NuGet 依赖项（无需单独的 `packages.config` 文件）。</span><span class="sxs-lookup"><span data-stu-id="12001-105">Package references, using the `PackageReference` node, manage NuGet dependencies directly within project files (as opposed to a separate `packages.config` file).</span></span> <span data-ttu-id="12001-106">使用所谓的 PackageReference 不会影响 NuGet 的其他方面；例如，仍按照[配置 NuGet 行为](configuring-nuget-behavior.md)中的说明应用 `NuGet.Config` 文件（包括包源）中的设置。</span><span class="sxs-lookup"><span data-stu-id="12001-106">Using PackageReference, as it's called, doesn't affect other aspects of NuGet; for example, settings in `NuGet.Config` files (including package sources) are still applied as explained in [Configuring NuGet Behavior](configuring-nuget-behavior.md).</span></span>

<span data-ttu-id="12001-107">利用 PackageReference，还可以使用 MSBuild 条件按目标框架、配置、平台或其他分组选择包引用。</span><span class="sxs-lookup"><span data-stu-id="12001-107">With PackageReference, you can also use MSBuild conditions to choose package references per target framework, configuration, platform, or other groupings.</span></span> <span data-ttu-id="12001-108">它还允许对依赖项和内容流实行精细控制。</span><span class="sxs-lookup"><span data-stu-id="12001-108">It also allows for fine-grained control over dependencies and content flow.</span></span> <span data-ttu-id="12001-109">（有关更多详细信息，请参阅[NuGet 打包和还原为 MSBuild 目标](../reference/msbuild-targets.md)。）</span><span class="sxs-lookup"><span data-stu-id="12001-109">(See For more details [NuGet pack and restore as MSBuild targets](../reference/msbuild-targets.md).)</span></span>

<span data-ttu-id="12001-110">默认情况下，PackageReference 用于 .NET Core 项目、.NET Standard 项目，以及面向 Windows 10 Build 15063（创意者更新）及更高版本的 UWP 项目（C++ UWP 项目除外）。</span><span class="sxs-lookup"><span data-stu-id="12001-110">By default, PackageReference is used for .NET Core projects, .NET Standard projects, and UWP projects targeting Windows 10 Build 15063 (Creators Update) and later, with the exception of C++ UWP projects.</span></span> <span data-ttu-id="12001-111">.NET 完整框架项目支持 PackageReference，但当前默认为 `packages.config`。</span><span class="sxs-lookup"><span data-stu-id="12001-111">.NET full framework projects support PackageReference, but currently default to `packages.config`.</span></span> <span data-ttu-id="12001-112">若要使用 PackageReference，请将 `packages.config` 中的依赖项迁移到项目文件中，然后删除 packages.config。</span><span class="sxs-lookup"><span data-stu-id="12001-112">To use PackageReference, migrate the dependencies from `packages.config` into your project file, then remove packages.config.</span></span>

## <a name="adding-a-packagereference"></a><span data-ttu-id="12001-113">添加 PackageReference</span><span class="sxs-lookup"><span data-stu-id="12001-113">Adding a PackageReference</span></span>

<span data-ttu-id="12001-114">在项目文件中使用以下语法添加依赖项：</span><span class="sxs-lookup"><span data-stu-id="12001-114">Add a dependency in your project file using the following syntax:</span></span>

```xml
<ItemGroup>
    <!-- ... -->
    <PackageReference Include="Contoso.Utility.UsefulStuff" Version="3.6.0" />
    <!-- ... -->
</ItemGroup>
```

## <a name="controlling-dependency-version"></a><span data-ttu-id="12001-115">控制依赖项版本</span><span class="sxs-lookup"><span data-stu-id="12001-115">Controlling dependency version</span></span>

<span data-ttu-id="12001-116">用于指定包版本的约定与使用 `packages.config` 时的约定相同：</span><span class="sxs-lookup"><span data-stu-id="12001-116">The convention for specifying the version of a package is the same as when using `packages.config`:</span></span>

```xml
<ItemGroup>
    <!-- ... -->
    <PackageReference Include="Contoso.Utility.UsefulStuff" Version="3.6.0" />
    <!-- ... -->
</ItemGroup>
```

<span data-ttu-id="12001-117">在上述示例中，3.6.0 指 >=3.6.0 的任何版本（首选项为最低版本），详见[包版本控制](../reference/package-versioning.md#version-ranges-and-wildcards)。</span><span class="sxs-lookup"><span data-stu-id="12001-117">In the example above, 3.6.0 means any version that is >=3.6.0 with preference for the lowest version, as described on [Package versioning](../reference/package-versioning.md#version-ranges-and-wildcards).</span></span>

## <a name="floating-versions"></a><span data-ttu-id="12001-118">可变版本</span><span class="sxs-lookup"><span data-stu-id="12001-118">Floating Versions</span></span>

<span data-ttu-id="12001-119">`PackageReference` 支持[可变版本](../consume-packages/dependency-resolution.md#floating-versions)：</span><span class="sxs-lookup"><span data-stu-id="12001-119">[Floating versions](../consume-packages/dependency-resolution.md#floating-versions) are supported with `PackageReference`:</span></span>

```xml
<ItemGroup>
    <!-- ... -->
    <PackageReference Include="Contoso.Utility.UsefulStuff" Version="3.6.*" />
    <PackageReference Include="Contoso.Utility.UsefulStuff" Version="3.6.0-beta*" />
    <!-- ... -->
</ItemGroup>
```

## <a name="controlling-dependency-assets"></a><span data-ttu-id="12001-120">控制依赖项资产</span><span class="sxs-lookup"><span data-stu-id="12001-120">Controlling dependency assets</span></span>

<span data-ttu-id="12001-121">你可能只是将依赖项用作开发工具，而不希望将它向会使用包的项目公开。</span><span class="sxs-lookup"><span data-stu-id="12001-121">You might be using a dependency purely as a development harness and might not want to expose that to projects that will consume your package.</span></span> <span data-ttu-id="12001-122">在此情况下，可使用 `PrivateAssets` 元数据控制此行为。</span><span class="sxs-lookup"><span data-stu-id="12001-122">In this scenario, you can use the `PrivateAssets` metadata to control this behavior.</span></span>

```xml
<ItemGroup>
    <!-- ... -->

    <PackageReference Include="Contoso.Utility.UsefulStuff" Version="3.6.0">
        <PrivateAssets>all</PrivateAssets>
    </PackageReference>

    <!-- ... -->
</ItemGroup>
```

<span data-ttu-id="12001-123">以下元数据标记控制依赖项资产：</span><span class="sxs-lookup"><span data-stu-id="12001-123">The following metadata tags control dependency assets:</span></span>

| <span data-ttu-id="12001-124">标记</span><span class="sxs-lookup"><span data-stu-id="12001-124">Tag</span></span> | <span data-ttu-id="12001-125">描述</span><span class="sxs-lookup"><span data-stu-id="12001-125">Description</span></span> | <span data-ttu-id="12001-126">默认值</span><span class="sxs-lookup"><span data-stu-id="12001-126">Default Value</span></span> |
| --- | --- | --- |
| <span data-ttu-id="12001-127">IncludeAssets</span><span class="sxs-lookup"><span data-stu-id="12001-127">IncludeAssets</span></span> | <span data-ttu-id="12001-128">将使用这些资产</span><span class="sxs-lookup"><span data-stu-id="12001-128">These assets will be consumed</span></span> | <span data-ttu-id="12001-129">全部</span><span class="sxs-lookup"><span data-stu-id="12001-129">all</span></span> |
| <span data-ttu-id="12001-130">ExcludeAssets</span><span class="sxs-lookup"><span data-stu-id="12001-130">ExcludeAssets</span></span> | <span data-ttu-id="12001-131">不会使用这些资产</span><span class="sxs-lookup"><span data-stu-id="12001-131">These assets will not be consumed</span></span> | <span data-ttu-id="12001-132">无</span><span class="sxs-lookup"><span data-stu-id="12001-132">none</span></span> |
| <span data-ttu-id="12001-133">PrivateAssets</span><span class="sxs-lookup"><span data-stu-id="12001-133">PrivateAssets</span></span> | <span data-ttu-id="12001-134">将使用这些资产，但它们不会流入上级项目</span><span class="sxs-lookup"><span data-stu-id="12001-134">These assets will be consumed but won't flow to the parent project</span></span> | <span data-ttu-id="12001-135">contentfiles;analyzers;build</span><span class="sxs-lookup"><span data-stu-id="12001-135">contentfiles;analyzers;build</span></span> |

<span data-ttu-id="12001-136">以下是这些标记的允许值，其中用分号分隔多个值（但 `all` 和 `none` 必须单独显示）：</span><span class="sxs-lookup"><span data-stu-id="12001-136">Allowable values for these tags are as follows, with multiple values separated by a semicolon except with `all` and `none` which must appear by themselves:</span></span>

| <span data-ttu-id="12001-137">“值”</span><span class="sxs-lookup"><span data-stu-id="12001-137">Value</span></span> | <span data-ttu-id="12001-138">描述</span><span class="sxs-lookup"><span data-stu-id="12001-138">Description</span></span> |
| --- | ---
| <span data-ttu-id="12001-139">编译</span><span class="sxs-lookup"><span data-stu-id="12001-139">compile</span></span> | <span data-ttu-id="12001-140">`lib` 文件夹中的内容</span><span class="sxs-lookup"><span data-stu-id="12001-140">Contents of the `lib` folder</span></span> |
| <span data-ttu-id="12001-141">Runtime — 运行时</span><span class="sxs-lookup"><span data-stu-id="12001-141">runtime</span></span> | <span data-ttu-id="12001-142">`runtimes` 文件夹中的内容</span><span class="sxs-lookup"><span data-stu-id="12001-142">Contents of the `runtimes` folder</span></span> |
| <span data-ttu-id="12001-143">contentFiles</span><span class="sxs-lookup"><span data-stu-id="12001-143">contentFiles</span></span> | <span data-ttu-id="12001-144">`contentfiles` 文件夹中的内容</span><span class="sxs-lookup"><span data-stu-id="12001-144">Contents of the `contentfiles` folder</span></span> |
| <span data-ttu-id="12001-145">生成</span><span class="sxs-lookup"><span data-stu-id="12001-145">build</span></span> | <span data-ttu-id="12001-146">`build` 文件夹中的属性和目标</span><span class="sxs-lookup"><span data-stu-id="12001-146">Props and targets in the `build` folder</span></span> |
| <span data-ttu-id="12001-147">analyzers</span><span class="sxs-lookup"><span data-stu-id="12001-147">analyzers</span></span> | <span data-ttu-id="12001-148">.NET 分析器</span><span class="sxs-lookup"><span data-stu-id="12001-148">.NET analyzers</span></span> |
| <span data-ttu-id="12001-149">本机</span><span class="sxs-lookup"><span data-stu-id="12001-149">native</span></span> | <span data-ttu-id="12001-150">`native` 文件夹中的内容</span><span class="sxs-lookup"><span data-stu-id="12001-150">Contents of the `native` folder</span></span> |
| <span data-ttu-id="12001-151">无</span><span class="sxs-lookup"><span data-stu-id="12001-151">none</span></span> | <span data-ttu-id="12001-152">不使用以上任何内容。</span><span class="sxs-lookup"><span data-stu-id="12001-152">None of the above are used.</span></span> |
| <span data-ttu-id="12001-153">全部</span><span class="sxs-lookup"><span data-stu-id="12001-153">all</span></span> | <span data-ttu-id="12001-154">以上都是（除 `none` 之外）</span><span class="sxs-lookup"><span data-stu-id="12001-154">All of the above (except `none`)</span></span> |

<span data-ttu-id="12001-155">在以下示例中，项目将使用除包中的内容文件之外的所有项，并且除内容文件和分析器之外的所有项均会流入上级项目。</span><span class="sxs-lookup"><span data-stu-id="12001-155">In the following example, everything except the content files from the package would be consumed by the project and everything except content files and analyzers would flow to the parent project.</span></span>

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

<span data-ttu-id="12001-156">请注意，因为 `PrivateAssets` 未包括 `build`，所以目标和属性将流入上级项目。</span><span class="sxs-lookup"><span data-stu-id="12001-156">Note that because `build` is not included with `PrivateAssets`, targets and props *will* flow to the parent project.</span></span> <span data-ttu-id="12001-157">例如，假设在生成名为 AppLogger 的 NuGet 包的项目中使用上述引用。</span><span class="sxs-lookup"><span data-stu-id="12001-157">Consider, for example, that the reference above is used in a project that builds a NuGet package called AppLogger.</span></span> <span data-ttu-id="12001-158">AppLogger 可以使用 `Contoso.Utility.UsefulStuff` 中的目标和属性，使用 AppLogger 的项目也可以。</span><span class="sxs-lookup"><span data-stu-id="12001-158">AppLogger can consume the targets and props from `Contoso.Utility.UsefulStuff`, as can projects that consume AppLogger.</span></span>

## <a name="adding-a-packagereference-condition"></a><span data-ttu-id="12001-159">添加 PackageReference 条件</span><span class="sxs-lookup"><span data-stu-id="12001-159">Adding a PackageReference condition</span></span>

<span data-ttu-id="12001-160">可使用条件控制是否包括包，在哪种条件可使用任何 MSBuild 变量或者目标或属性文件中定义的变量。</span><span class="sxs-lookup"><span data-stu-id="12001-160">You can use a condition to control whether a package is included, where conditions can use any MSBuild variable or a variable defined in the targets or props file.</span></span> <span data-ttu-id="12001-161">但目前仅支持 `TargetFramework` 变量。</span><span class="sxs-lookup"><span data-stu-id="12001-161">However, at presently, only the `TargetFramework` variable is supported.</span></span>

<span data-ttu-id="12001-162">例如，假设目标为 `netstandard1.4` 和 `net452`，但具有的依赖项仅适用于 `net452`。</span><span class="sxs-lookup"><span data-stu-id="12001-162">For example, say you're targeting `netstandard1.4` as well as `net452` but have a dependency that is applicable only for `net452`.</span></span> <span data-ttu-id="12001-163">在此情况下，你不希望使用包的 `netstandard1.4` 项目添加该不必要的依赖项。</span><span class="sxs-lookup"><span data-stu-id="12001-163">In this case you don't want a `netstandard1.4` project that's consuming your package to add that unnecessary dependency.</span></span> <span data-ttu-id="12001-164">要防止此情况，请在 `PackageReference` 上指定条件，如下所示：</span><span class="sxs-lookup"><span data-stu-id="12001-164">To prevent this, you specify a condition on the `PackageReference` as follows:</span></span>

```xml
<ItemGroup>
    <!-- ... -->
    <PackageReference Include="Newtonsoft.json" Version="9.0.1" Condition="'$(TargetFramework)' == 'net452'" />
    <!-- ... -->
</ItemGroup>
```

<span data-ttu-id="12001-165">使用此项目生成的包会显示仅针对 `net452` 目标包括 Newtonsoft.json 作为依赖项：</span><span class="sxs-lookup"><span data-stu-id="12001-165">A package built using this project will show that Newtonsoft.json is included as a dependency only for a `net452` target:</span></span>

![对 VS2017 的 PackageReference 应用条件的结果](media/PackageReference-Condition.png)

<span data-ttu-id="12001-167">还可以在 `ItemGroup` 级别应用条件，并将其应用到所有子级 `PackageReference` 元素：</span><span class="sxs-lookup"><span data-stu-id="12001-167">Conditions can also be applied at the `ItemGroup` level and will apply to all children `PackageReference` elements:</span></span>

```xml
<ItemGroup Condition = "'$(TargetFramework)' == 'net452'">
    <!-- ... -->
    <PackageReference Include="Newtonsoft.json" Version="9.0.1" />
    <PackageReference Include="Contoso.Utility.UsefulStuff" Version="3.6.0" />
    <!-- ... -->
</ItemGroup>
```
