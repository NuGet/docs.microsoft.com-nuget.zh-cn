---
title: NuGet PackageReference 格式（项目文件中的包引用）
description: 详细介绍项目文件中 NuGet 4.0+、VS2017 和 .NET Core 2.0 支持的 NuGet PackageReference
author: kraigb
ms.author: kraigb
manager: douge
ms.date: 03/16/2018
ms.topic: conceptual
ms.openlocfilehash: 8f277a8af7f988d6fdcfa75c43a10b3792c2ae22
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/26/2018
---
# <a name="package-references-packagereference-in-project-files"></a><span data-ttu-id="001ab-103">项目文件中的包引用 (PackageReference)</span><span class="sxs-lookup"><span data-stu-id="001ab-103">Package references (PackageReference) in project files</span></span>

<span data-ttu-id="001ab-104">使用 `PackageReference` 节点的包引用可直接在项目文件中管理 NuGet 依赖项（无需单独的 `packages.config` 文件）。</span><span class="sxs-lookup"><span data-stu-id="001ab-104">Package references, using the `PackageReference` node, manage NuGet dependencies directly within project files (as opposed to a separate `packages.config` file).</span></span> <span data-ttu-id="001ab-105">使用所谓的 PackageReference 不会影响 NuGet 的其他方面；例如，仍按照[配置 NuGet 行为](configuring-nuget-behavior.md)中的说明应用 `NuGet.Config` 文件（包括包源）中的设置。</span><span class="sxs-lookup"><span data-stu-id="001ab-105">Using PackageReference, as it's called, doesn't affect other aspects of NuGet; for example, settings in `NuGet.Config` files (including package sources) are still applied as explained in [Configuring NuGet Behavior](configuring-nuget-behavior.md).</span></span>

<span data-ttu-id="001ab-106">利用 PackageReference，还可以使用 MSBuild 条件按目标框架、配置、平台或其他分组选择包引用。</span><span class="sxs-lookup"><span data-stu-id="001ab-106">With PackageReference, you can also use MSBuild conditions to choose package references per target framework, configuration, platform, or other groupings.</span></span> <span data-ttu-id="001ab-107">它还允许对依赖项和内容流实行精细控制。</span><span class="sxs-lookup"><span data-stu-id="001ab-107">It also allows for fine-grained control over dependencies and content flow.</span></span> <span data-ttu-id="001ab-108">（有关更多详细信息，请参阅[NuGet 打包和还原为 MSBuild 目标](../reference/msbuild-targets.md)。）</span><span class="sxs-lookup"><span data-stu-id="001ab-108">(See For more details [NuGet pack and restore as MSBuild targets](../reference/msbuild-targets.md).)</span></span>

<span data-ttu-id="001ab-109">默认情况下，PackageReference 用于 .NET Core 项目、.NET Standard 项目，以及面向 Windows 10 Build 15063（创意者更新）及更高版本的 UWP 项目（C++ UWP 项目除外）。</span><span class="sxs-lookup"><span data-stu-id="001ab-109">By default, PackageReference is used for .NET Core projects, .NET Standard projects, and UWP projects targeting Windows 10 Build 15063 (Creators Update) and later, with the exception of C++ UWP projects.</span></span> <span data-ttu-id="001ab-110">.NET 完整框架项目支持 PackageReference，但当前默认为 `packages.config`。</span><span class="sxs-lookup"><span data-stu-id="001ab-110">.NET full framework projects support PackageReference, but currently default to `packages.config`.</span></span> <span data-ttu-id="001ab-111">若要使用 PackageReference，请将 `packages.config` 中的依赖项迁移到项目文件中，然后删除 packages.config。</span><span class="sxs-lookup"><span data-stu-id="001ab-111">To use PackageReference, migrate the dependencies from `packages.config` into your project file, then remove packages.config.</span></span>

## <a name="adding-a-packagereference"></a><span data-ttu-id="001ab-112">添加 PackageReference</span><span class="sxs-lookup"><span data-stu-id="001ab-112">Adding a PackageReference</span></span>

<span data-ttu-id="001ab-113">在项目文件中使用以下语法添加依赖项：</span><span class="sxs-lookup"><span data-stu-id="001ab-113">Add a dependency in your project file using the following syntax:</span></span>

```xml
<ItemGroup>
    <!-- ... -->
    <PackageReference Include="Contoso.Utility.UsefulStuff" Version="3.6.0" />
    <!-- ... -->
</ItemGroup>
```

## <a name="controlling-dependency-version"></a><span data-ttu-id="001ab-114">控制依赖项版本</span><span class="sxs-lookup"><span data-stu-id="001ab-114">Controlling dependency version</span></span>

<span data-ttu-id="001ab-115">用于指定包版本的约定与使用 `packages.config` 时的约定相同：</span><span class="sxs-lookup"><span data-stu-id="001ab-115">The convention for specifying the version of a package is the same as when using `packages.config`:</span></span>

```xml
<ItemGroup>
    <!-- ... -->
    <PackageReference Include="Contoso.Utility.UsefulStuff" Version="3.6.0" />
    <!-- ... -->
</ItemGroup>
```

<span data-ttu-id="001ab-116">在上述示例中，3.6.0 指 >=3.6.0 的任何版本（首选项为最低版本），详见[包版本控制](../reference/package-versioning.md#version-ranges-and-wildcards)。</span><span class="sxs-lookup"><span data-stu-id="001ab-116">In the example above, 3.6.0 means any version that is >=3.6.0 with preference for the lowest version, as described on [Package versioning](../reference/package-versioning.md#version-ranges-and-wildcards).</span></span>

## <a name="floating-versions"></a><span data-ttu-id="001ab-117">可变版本</span><span class="sxs-lookup"><span data-stu-id="001ab-117">Floating Versions</span></span>

<span data-ttu-id="001ab-118">`PackageReference` 支持[可变版本](../consume-packages/dependency-resolution.md#floating-versions)：</span><span class="sxs-lookup"><span data-stu-id="001ab-118">[Floating versions](../consume-packages/dependency-resolution.md#floating-versions) are supported with `PackageReference`:</span></span>

```xml
<ItemGroup>
    <!-- ... -->
    <PackageReference Include="Contoso.Utility.UsefulStuff" Version="3.6.*" />
    <PackageReference Include="Contoso.Utility.UsefulStuff" Version="3.6.0-beta*" />
    <!-- ... -->
</ItemGroup>
```

## <a name="controlling-dependency-assets"></a><span data-ttu-id="001ab-119">控制依赖项资产</span><span class="sxs-lookup"><span data-stu-id="001ab-119">Controlling dependency assets</span></span>

<span data-ttu-id="001ab-120">你可能只是将依赖项用作开发工具，而不希望将它向会使用包的项目公开。</span><span class="sxs-lookup"><span data-stu-id="001ab-120">You might be using a dependency purely as a development harness and might not want to expose that to projects that will consume your package.</span></span> <span data-ttu-id="001ab-121">在此情况下，可使用 `PrivateAssets` 元数据控制此行为。</span><span class="sxs-lookup"><span data-stu-id="001ab-121">In this scenario, you can use the `PrivateAssets` metadata to control this behavior.</span></span>

```xml
<ItemGroup>
    <!-- ... -->

    <PackageReference Include="Contoso.Utility.UsefulStuff" Version="3.6.0">
        <PrivateAssets>all</PrivateAssets>
    </PackageReference>

    <!-- ... -->
</ItemGroup>
```

<span data-ttu-id="001ab-122">以下元数据标记控制依赖项资产：</span><span class="sxs-lookup"><span data-stu-id="001ab-122">The following metadata tags control dependency assets:</span></span>

| <span data-ttu-id="001ab-123">标记</span><span class="sxs-lookup"><span data-stu-id="001ab-123">Tag</span></span> | <span data-ttu-id="001ab-124">描述</span><span class="sxs-lookup"><span data-stu-id="001ab-124">Description</span></span> | <span data-ttu-id="001ab-125">默认值</span><span class="sxs-lookup"><span data-stu-id="001ab-125">Default Value</span></span> |
| --- | --- | --- |
| <span data-ttu-id="001ab-126">IncludeAssets</span><span class="sxs-lookup"><span data-stu-id="001ab-126">IncludeAssets</span></span> | <span data-ttu-id="001ab-127">将使用这些资产</span><span class="sxs-lookup"><span data-stu-id="001ab-127">These assets will be consumed</span></span> | <span data-ttu-id="001ab-128">全部</span><span class="sxs-lookup"><span data-stu-id="001ab-128">all</span></span> |
| <span data-ttu-id="001ab-129">ExcludeAssets</span><span class="sxs-lookup"><span data-stu-id="001ab-129">ExcludeAssets</span></span> | <span data-ttu-id="001ab-130">不会使用这些资产</span><span class="sxs-lookup"><span data-stu-id="001ab-130">These assets will not be consumed</span></span> | <span data-ttu-id="001ab-131">无</span><span class="sxs-lookup"><span data-stu-id="001ab-131">none</span></span> |
| <span data-ttu-id="001ab-132">PrivateAssets</span><span class="sxs-lookup"><span data-stu-id="001ab-132">PrivateAssets</span></span> | <span data-ttu-id="001ab-133">将使用这些资产，但它们不会流入上级项目</span><span class="sxs-lookup"><span data-stu-id="001ab-133">These assets will be consumed but won't flow to the parent project</span></span> | <span data-ttu-id="001ab-134">contentfiles;analyzers;build</span><span class="sxs-lookup"><span data-stu-id="001ab-134">contentfiles;analyzers;build</span></span> |

<span data-ttu-id="001ab-135">以下是这些标记的允许值，其中用分号分隔多个值（但 `all` 和 `none` 必须单独显示）：</span><span class="sxs-lookup"><span data-stu-id="001ab-135">Allowable values for these tags are as follows, with multiple values separated by a semicolon except with `all` and `none` which must appear by themselves:</span></span>

| <span data-ttu-id="001ab-136">“值”</span><span class="sxs-lookup"><span data-stu-id="001ab-136">Value</span></span> | <span data-ttu-id="001ab-137">描述</span><span class="sxs-lookup"><span data-stu-id="001ab-137">Description</span></span> |
| --- | ---
| <span data-ttu-id="001ab-138">编译</span><span class="sxs-lookup"><span data-stu-id="001ab-138">compile</span></span> | <span data-ttu-id="001ab-139">`lib` 文件夹的内容，控制项目能否对文件夹中的程序集进行编译</span><span class="sxs-lookup"><span data-stu-id="001ab-139">Contents of the `lib` folder and controls whether your project can compile against the assemblies within the folder</span></span> |
| <span data-ttu-id="001ab-140">Runtime — 运行时</span><span class="sxs-lookup"><span data-stu-id="001ab-140">runtime</span></span> | <span data-ttu-id="001ab-141">`lib` 和 `runtimes` 文件夹的内容，控制是否会复制这些程序集，以生成输出目录</span><span class="sxs-lookup"><span data-stu-id="001ab-141">Contents of the `lib` and `runtimes` folder and controls whether these assemblies will be copied out to the build output directory</span></span> |
| <span data-ttu-id="001ab-142">contentFiles</span><span class="sxs-lookup"><span data-stu-id="001ab-142">contentFiles</span></span> | <span data-ttu-id="001ab-143">`contentfiles` 文件夹中的内容</span><span class="sxs-lookup"><span data-stu-id="001ab-143">Contents of the `contentfiles` folder</span></span> |
| <span data-ttu-id="001ab-144">生成</span><span class="sxs-lookup"><span data-stu-id="001ab-144">build</span></span> | <span data-ttu-id="001ab-145">`build` 文件夹中的属性和目标</span><span class="sxs-lookup"><span data-stu-id="001ab-145">Props and targets in the `build` folder</span></span> |
| <span data-ttu-id="001ab-146">analyzers</span><span class="sxs-lookup"><span data-stu-id="001ab-146">analyzers</span></span> | <span data-ttu-id="001ab-147">.NET 分析器</span><span class="sxs-lookup"><span data-stu-id="001ab-147">.NET analyzers</span></span> |
| <span data-ttu-id="001ab-148">本机</span><span class="sxs-lookup"><span data-stu-id="001ab-148">native</span></span> | <span data-ttu-id="001ab-149">`native` 文件夹中的内容</span><span class="sxs-lookup"><span data-stu-id="001ab-149">Contents of the `native` folder</span></span> |
| <span data-ttu-id="001ab-150">无</span><span class="sxs-lookup"><span data-stu-id="001ab-150">none</span></span> | <span data-ttu-id="001ab-151">不使用以上任何内容。</span><span class="sxs-lookup"><span data-stu-id="001ab-151">None of the above are used.</span></span> |
| <span data-ttu-id="001ab-152">全部</span><span class="sxs-lookup"><span data-stu-id="001ab-152">all</span></span> | <span data-ttu-id="001ab-153">以上都是（除 `none` 之外）</span><span class="sxs-lookup"><span data-stu-id="001ab-153">All of the above (except `none`)</span></span> |

<span data-ttu-id="001ab-154">在以下示例中，项目将使用除包中的内容文件之外的所有项，并且除内容文件和分析器之外的所有项均会流入上级项目。</span><span class="sxs-lookup"><span data-stu-id="001ab-154">In the following example, everything except the content files from the package would be consumed by the project and everything except content files and analyzers would flow to the parent project.</span></span>

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

<span data-ttu-id="001ab-155">请注意，因为 `PrivateAssets` 未包括 `build`，所以目标和属性将流入上级项目。</span><span class="sxs-lookup"><span data-stu-id="001ab-155">Note that because `build` is not included with `PrivateAssets`, targets and props *will* flow to the parent project.</span></span> <span data-ttu-id="001ab-156">例如，假设在生成名为 AppLogger 的 NuGet 包的项目中使用上述引用。</span><span class="sxs-lookup"><span data-stu-id="001ab-156">Consider, for example, that the reference above is used in a project that builds a NuGet package called AppLogger.</span></span> <span data-ttu-id="001ab-157">AppLogger 可以使用 `Contoso.Utility.UsefulStuff` 中的目标和属性，使用 AppLogger 的项目也可以。</span><span class="sxs-lookup"><span data-stu-id="001ab-157">AppLogger can consume the targets and props from `Contoso.Utility.UsefulStuff`, as can projects that consume AppLogger.</span></span>

## <a name="adding-a-packagereference-condition"></a><span data-ttu-id="001ab-158">添加 PackageReference 条件</span><span class="sxs-lookup"><span data-stu-id="001ab-158">Adding a PackageReference condition</span></span>

<span data-ttu-id="001ab-159">可使用条件控制是否包括包，在哪种条件可使用任何 MSBuild 变量或者目标或属性文件中定义的变量。</span><span class="sxs-lookup"><span data-stu-id="001ab-159">You can use a condition to control whether a package is included, where conditions can use any MSBuild variable or a variable defined in the targets or props file.</span></span> <span data-ttu-id="001ab-160">但目前仅支持 `TargetFramework` 变量。</span><span class="sxs-lookup"><span data-stu-id="001ab-160">However, at presently, only the `TargetFramework` variable is supported.</span></span>

<span data-ttu-id="001ab-161">例如，假设目标为 `netstandard1.4` 和 `net452`，但具有的依赖项仅适用于 `net452`。</span><span class="sxs-lookup"><span data-stu-id="001ab-161">For example, say you're targeting `netstandard1.4` as well as `net452` but have a dependency that is applicable only for `net452`.</span></span> <span data-ttu-id="001ab-162">在此情况下，你不希望使用包的 `netstandard1.4` 项目添加该不必要的依赖项。</span><span class="sxs-lookup"><span data-stu-id="001ab-162">In this case you don't want a `netstandard1.4` project that's consuming your package to add that unnecessary dependency.</span></span> <span data-ttu-id="001ab-163">要防止此情况，请在 `PackageReference` 上指定条件，如下所示：</span><span class="sxs-lookup"><span data-stu-id="001ab-163">To prevent this, you specify a condition on the `PackageReference` as follows:</span></span>

```xml
<ItemGroup>
    <!-- ... -->
    <PackageReference Include="Newtonsoft.json" Version="9.0.1" Condition="'$(TargetFramework)' == 'net452'" />
    <!-- ... -->
</ItemGroup>
```

<span data-ttu-id="001ab-164">使用此项目生成的包会显示仅针对 `net452` 目标包括 Newtonsoft.json 作为依赖项：</span><span class="sxs-lookup"><span data-stu-id="001ab-164">A package built using this project will show that Newtonsoft.json is included as a dependency only for a `net452` target:</span></span>

![对 VS2017 的 PackageReference 应用条件的结果](media/PackageReference-Condition.png)

<span data-ttu-id="001ab-166">还可以在 `ItemGroup` 级别应用条件，并将其应用到所有子级 `PackageReference` 元素：</span><span class="sxs-lookup"><span data-stu-id="001ab-166">Conditions can also be applied at the `ItemGroup` level and will apply to all children `PackageReference` elements:</span></span>

```xml
<ItemGroup Condition = "'$(TargetFramework)' == 'net452'">
    <!-- ... -->
    <PackageReference Include="Newtonsoft.json" Version="9.0.1" />
    <PackageReference Include="Contoso.Utility.UsefulStuff" Version="3.6.0" />
    <!-- ... -->
</ItemGroup>
```
