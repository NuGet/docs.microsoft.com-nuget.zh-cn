---
title: NuGet PackageReference 格式（项目文件中的包引用）
description: 详细介绍项目文件中 NuGet 4.0+、VS2017 和 .NET Core 2.0 支持的 NuGet PackageReference
author: karann-msft
ms.author: karann
ms.date: 03/16/2018
ms.topic: conceptual
ms.openlocfilehash: 16a14a72f8bb2e5d5a56f6c3c277f0988869273d
ms.sourcegitcommit: b6810860b77b2d50aab031040b047c20a333aca3
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/28/2019
ms.locfileid: "67426699"
---
# <a name="package-references-packagereference-in-project-files"></a><span data-ttu-id="af3c2-103">项目文件中的包引用 (PackageReference)</span><span class="sxs-lookup"><span data-stu-id="af3c2-103">Package references (PackageReference) in project files</span></span>

<span data-ttu-id="af3c2-104">使用 `PackageReference` 节点的包引用可直接在项目文件中管理 NuGet 依赖项（无需单独的 `packages.config` 文件）。</span><span class="sxs-lookup"><span data-stu-id="af3c2-104">Package references, using the `PackageReference` node, manage NuGet dependencies directly within project files (as opposed to a separate `packages.config` file).</span></span> <span data-ttu-id="af3c2-105">使用所谓的 PackageReference 不会影响 NuGet 的其他方面；例如，仍按照[常规 NuGet 配置](configuring-nuget-behavior.md)中的说明应用 `NuGet.config` 文件（包括包源）中的设置。</span><span class="sxs-lookup"><span data-stu-id="af3c2-105">Using PackageReference, as it's called, doesn't affect other aspects of NuGet; for example, settings in `NuGet.config` files (including package sources) are still applied as explained in [Common NuGet configurations](configuring-nuget-behavior.md).</span></span>

<span data-ttu-id="af3c2-106">利用 PackageReference，还可以使用 MSBuild 条件按目标框架、配置、平台或其他分组选择包引用。</span><span class="sxs-lookup"><span data-stu-id="af3c2-106">With PackageReference, you can also use MSBuild conditions to choose package references per target framework, configuration, platform, or other groupings.</span></span> <span data-ttu-id="af3c2-107">它还允许对依赖项和内容流实行精细控制。</span><span class="sxs-lookup"><span data-stu-id="af3c2-107">It also allows for fine-grained control over dependencies and content flow.</span></span> <span data-ttu-id="af3c2-108">（有关更多详细信息，请参阅[NuGet 打包和还原为 MSBuild 目标](../reference/msbuild-targets.md)。）</span><span class="sxs-lookup"><span data-stu-id="af3c2-108">(See For more details [NuGet pack and restore as MSBuild targets](../reference/msbuild-targets.md).)</span></span>

## <a name="project-type-support"></a><span data-ttu-id="af3c2-109">项目类型支持</span><span class="sxs-lookup"><span data-stu-id="af3c2-109">Project type support</span></span>

<span data-ttu-id="af3c2-110">默认情况下，PackageReference 用于 .NET Core 项目、.NET Standard 项目，以及面向 Windows 10 Build 15063（创意者更新）及更高版本的 UWP 项目（C++ UWP 项目除外）。</span><span class="sxs-lookup"><span data-stu-id="af3c2-110">By default, PackageReference is used for .NET Core projects, .NET Standard projects, and UWP projects targeting Windows 10 Build 15063 (Creators Update) and later, with the exception of C++ UWP projects.</span></span> <span data-ttu-id="af3c2-111">.NET 框架项目支持 PackageReference，但当前默认为 `packages.config`。</span><span class="sxs-lookup"><span data-stu-id="af3c2-111">.NET Framework projects support PackageReference, but currently default to `packages.config`.</span></span> <span data-ttu-id="af3c2-112">若要使用 PackageReference，请将 `packages.config` 中的依赖项[迁移](../reference/migrate-packages-config-to-package-reference.md)到项目文件中，然后删除 packages.config。</span><span class="sxs-lookup"><span data-stu-id="af3c2-112">To use PackageReference, [migrate](../reference/migrate-packages-config-to-package-reference.md) the dependencies from `packages.config` into your project file, then remove packages.config.</span></span>

<span data-ttu-id="af3c2-113">面向完整 .NET Framework 的 ASP.NET 应用仅包括对 PackageReference 的[有限支持](https://github.com/NuGet/Home/issues/5877)。</span><span class="sxs-lookup"><span data-stu-id="af3c2-113">ASP.NET apps targeting the full .NET Framework include only [limited support](https://github.com/NuGet/Home/issues/5877) for PackageReference.</span></span> <span data-ttu-id="af3c2-114">不支持 C++ 和 JavaScript 项目类型。</span><span class="sxs-lookup"><span data-stu-id="af3c2-114">C++ and JavaScript project types are unsupported.</span></span>

## <a name="adding-a-packagereference"></a><span data-ttu-id="af3c2-115">添加 PackageReference</span><span class="sxs-lookup"><span data-stu-id="af3c2-115">Adding a PackageReference</span></span>

<span data-ttu-id="af3c2-116">在项目文件中使用以下语法添加依赖项：</span><span class="sxs-lookup"><span data-stu-id="af3c2-116">Add a dependency in your project file using the following syntax:</span></span>

```xml
<ItemGroup>
    <!-- ... -->
    <PackageReference Include="Contoso.Utility.UsefulStuff" Version="3.6.0" />
    <!-- ... -->
</ItemGroup>
```

## <a name="controlling-dependency-version"></a><span data-ttu-id="af3c2-117">控制依赖项版本</span><span class="sxs-lookup"><span data-stu-id="af3c2-117">Controlling dependency version</span></span>

<span data-ttu-id="af3c2-118">用于指定包版本的约定与使用 `packages.config` 时的约定相同：</span><span class="sxs-lookup"><span data-stu-id="af3c2-118">The convention for specifying the version of a package is the same as when using `packages.config`:</span></span>

```xml
<ItemGroup>
    <!-- ... -->
    <PackageReference Include="Contoso.Utility.UsefulStuff" Version="3.6.0" />
    <!-- ... -->
</ItemGroup>
```

<span data-ttu-id="af3c2-119">在上述示例中，3.6.0 指 >=3.6.0 的任何版本（首选项为最低版本），详见[包版本控制](../reference/package-versioning.md#version-ranges-and-wildcards)。</span><span class="sxs-lookup"><span data-stu-id="af3c2-119">In the example above, 3.6.0 means any version that is >=3.6.0 with preference for the lowest version, as described on [Package versioning](../reference/package-versioning.md#version-ranges-and-wildcards).</span></span>

## <a name="using-packagereference-for-a-project-with-no-packagereferences"></a><span data-ttu-id="af3c2-120">对没有 PackageReferences 的项目使用 PackageReference</span><span class="sxs-lookup"><span data-stu-id="af3c2-120">Using PackageReference for a project with no PackageReferences</span></span>
<span data-ttu-id="af3c2-121">高级：如果没有在项目中安装包（项目文件中没有 PackageReference，也没有 packages.config 文件），但要将项目还原为 PackageReference 样式，可以在项目文件中将项目属性 RestoreProjectStyle 设置为 PackageReference。</span><span class="sxs-lookup"><span data-stu-id="af3c2-121">Advanced: If you have no packages installed in a project (no PackageReferences in project file and no packages.config file), but want the project to be restored as PackageReference style, you can set a Project property RestoreProjectStyle to PackageReference in your project file.</span></span>
```xml
<PropertyGroup>
    <!--- ... -->
    <RestoreProjectStyle>PackageReference</RestoreProjectStyle>
    <!--- ... -->
</PropertyGroup>    
```
<span data-ttu-id="af3c2-122">如果引用 PackageReference 样式的项目（现有 csproj 或 SDK 样式的项目），这可能很有用。</span><span class="sxs-lookup"><span data-stu-id="af3c2-122">This may be useful, if you reference projects which are PackageReference styled (existing csproj or SDK-style projects).</span></span> <span data-ttu-id="af3c2-123">这可让其他项目以“可传递”的方式引用这些项目引用的包。</span><span class="sxs-lookup"><span data-stu-id="af3c2-123">This will enable packages that those projects refer to, to be "transitively" referenced by your project.</span></span>

## <a name="floating-versions"></a><span data-ttu-id="af3c2-124">可变版本</span><span class="sxs-lookup"><span data-stu-id="af3c2-124">Floating Versions</span></span>

<span data-ttu-id="af3c2-125">`PackageReference` 支持[可变版本](../consume-packages/dependency-resolution.md#floating-versions)：</span><span class="sxs-lookup"><span data-stu-id="af3c2-125">[Floating versions](../consume-packages/dependency-resolution.md#floating-versions) are supported with `PackageReference`:</span></span>

```xml
<ItemGroup>
    <!-- ... -->
    <PackageReference Include="Contoso.Utility.UsefulStuff" Version="3.6.*" />
    <PackageReference Include="Contoso.Utility.UsefulStuff" Version="3.6.0-beta*" />
    <!-- ... -->
</ItemGroup>
```

## <a name="controlling-dependency-assets"></a><span data-ttu-id="af3c2-126">控制依赖项资产</span><span class="sxs-lookup"><span data-stu-id="af3c2-126">Controlling dependency assets</span></span>

<span data-ttu-id="af3c2-127">你可能只是将依赖项用作开发工具，而不希望将它向会使用包的项目公开。</span><span class="sxs-lookup"><span data-stu-id="af3c2-127">You might be using a dependency purely as a development harness and might not want to expose that to projects that will consume your package.</span></span> <span data-ttu-id="af3c2-128">在此情况下，可使用 `PrivateAssets` 元数据控制此行为。</span><span class="sxs-lookup"><span data-stu-id="af3c2-128">In this scenario, you can use the `PrivateAssets` metadata to control this behavior.</span></span>

```xml
<ItemGroup>
    <!-- ... -->

    <PackageReference Include="Contoso.Utility.UsefulStuff" Version="3.6.0">
        <PrivateAssets>all</PrivateAssets>
    </PackageReference>

    <!-- ... -->
</ItemGroup>
```

<span data-ttu-id="af3c2-129">以下元数据标记控制依赖项资产：</span><span class="sxs-lookup"><span data-stu-id="af3c2-129">The following metadata tags control dependency assets:</span></span>

| <span data-ttu-id="af3c2-130">标记</span><span class="sxs-lookup"><span data-stu-id="af3c2-130">Tag</span></span> | <span data-ttu-id="af3c2-131">说明</span><span class="sxs-lookup"><span data-stu-id="af3c2-131">Description</span></span> | <span data-ttu-id="af3c2-132">默认值</span><span class="sxs-lookup"><span data-stu-id="af3c2-132">Default Value</span></span> |
| --- | --- | --- |
| <span data-ttu-id="af3c2-133">IncludeAssets</span><span class="sxs-lookup"><span data-stu-id="af3c2-133">IncludeAssets</span></span> | <span data-ttu-id="af3c2-134">将使用这些资产</span><span class="sxs-lookup"><span data-stu-id="af3c2-134">These assets will be consumed</span></span> | <span data-ttu-id="af3c2-135">全部</span><span class="sxs-lookup"><span data-stu-id="af3c2-135">all</span></span> |
| <span data-ttu-id="af3c2-136">ExcludeAssets</span><span class="sxs-lookup"><span data-stu-id="af3c2-136">ExcludeAssets</span></span> | <span data-ttu-id="af3c2-137">不会使用这些资产</span><span class="sxs-lookup"><span data-stu-id="af3c2-137">These assets will not be consumed</span></span> | <span data-ttu-id="af3c2-138">无</span><span class="sxs-lookup"><span data-stu-id="af3c2-138">none</span></span> |
| <span data-ttu-id="af3c2-139">PrivateAssets</span><span class="sxs-lookup"><span data-stu-id="af3c2-139">PrivateAssets</span></span> | <span data-ttu-id="af3c2-140">将使用这些资产，但它们不会流入上级项目</span><span class="sxs-lookup"><span data-stu-id="af3c2-140">These assets will be consumed but won't flow to the parent project</span></span> | <span data-ttu-id="af3c2-141">contentfiles;analyzers;build</span><span class="sxs-lookup"><span data-stu-id="af3c2-141">contentfiles;analyzers;build</span></span> |

<span data-ttu-id="af3c2-142">以下是这些标记的允许值，其中用分号分隔多个值（但 `all` 和 `none` 必须单独显示）：</span><span class="sxs-lookup"><span data-stu-id="af3c2-142">Allowable values for these tags are as follows, with multiple values separated by a semicolon except with `all` and `none` which must appear by themselves:</span></span>

| <span data-ttu-id="af3c2-143">值</span><span class="sxs-lookup"><span data-stu-id="af3c2-143">Value</span></span> | <span data-ttu-id="af3c2-144">说明</span><span class="sxs-lookup"><span data-stu-id="af3c2-144">Description</span></span> |
| --- | ---
| <span data-ttu-id="af3c2-145">编译</span><span class="sxs-lookup"><span data-stu-id="af3c2-145">compile</span></span> | <span data-ttu-id="af3c2-146">`lib` 文件夹的内容，控制项目能否对文件夹中的程序集进行编译</span><span class="sxs-lookup"><span data-stu-id="af3c2-146">Contents of the `lib` folder and controls whether your project can compile against the assemblies within the folder</span></span> |
| <span data-ttu-id="af3c2-147">Runtime — 运行时</span><span class="sxs-lookup"><span data-stu-id="af3c2-147">runtime</span></span> | <span data-ttu-id="af3c2-148">`lib` 和 `runtimes` 文件夹的内容，控制是否会复制这些程序集，以生成输出目录</span><span class="sxs-lookup"><span data-stu-id="af3c2-148">Contents of the `lib` and `runtimes` folder and controls whether these assemblies will be copied out to the build output directory</span></span> |
| <span data-ttu-id="af3c2-149">contentFiles</span><span class="sxs-lookup"><span data-stu-id="af3c2-149">contentFiles</span></span> | <span data-ttu-id="af3c2-150">`contentfiles` 文件夹中的内容</span><span class="sxs-lookup"><span data-stu-id="af3c2-150">Contents of the `contentfiles` folder</span></span> |
| <span data-ttu-id="af3c2-151">生成</span><span class="sxs-lookup"><span data-stu-id="af3c2-151">build</span></span> | <span data-ttu-id="af3c2-152">`build` 文件夹中的属性和目标</span><span class="sxs-lookup"><span data-stu-id="af3c2-152">Props and targets in the `build` folder</span></span> |
| <span data-ttu-id="af3c2-153">analyzers</span><span class="sxs-lookup"><span data-stu-id="af3c2-153">analyzers</span></span> | <span data-ttu-id="af3c2-154">.NET 分析器</span><span class="sxs-lookup"><span data-stu-id="af3c2-154">.NET analyzers</span></span> |
| <span data-ttu-id="af3c2-155">本机</span><span class="sxs-lookup"><span data-stu-id="af3c2-155">native</span></span> | <span data-ttu-id="af3c2-156">`native` 文件夹中的内容</span><span class="sxs-lookup"><span data-stu-id="af3c2-156">Contents of the `native` folder</span></span> |
| <span data-ttu-id="af3c2-157">无</span><span class="sxs-lookup"><span data-stu-id="af3c2-157">none</span></span> | <span data-ttu-id="af3c2-158">不使用以上任何内容。</span><span class="sxs-lookup"><span data-stu-id="af3c2-158">None of the above are used.</span></span> |
| <span data-ttu-id="af3c2-159">全部</span><span class="sxs-lookup"><span data-stu-id="af3c2-159">all</span></span> | <span data-ttu-id="af3c2-160">以上都是（除 `none` 之外）</span><span class="sxs-lookup"><span data-stu-id="af3c2-160">All of the above (except `none`)</span></span> |

<span data-ttu-id="af3c2-161">在以下示例中，项目将使用除包中的内容文件之外的所有项，并且除内容文件和分析器之外的所有项均会流入上级项目。</span><span class="sxs-lookup"><span data-stu-id="af3c2-161">In the following example, everything except the content files from the package would be consumed by the project and everything except content files and analyzers would flow to the parent project.</span></span>

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

<span data-ttu-id="af3c2-162">请注意，因为 `PrivateAssets` 未包括 `build`，所以目标和属性将流入上级项目  。</span><span class="sxs-lookup"><span data-stu-id="af3c2-162">Note that because `build` is not included with `PrivateAssets`, targets and props *will* flow to the parent project.</span></span> <span data-ttu-id="af3c2-163">例如，假设在生成名为 AppLogger 的 NuGet 包的项目中使用上述引用。</span><span class="sxs-lookup"><span data-stu-id="af3c2-163">Consider, for example, that the reference above is used in a project that builds a NuGet package called AppLogger.</span></span> <span data-ttu-id="af3c2-164">AppLogger 可以使用 `Contoso.Utility.UsefulStuff` 中的目标和属性，使用 AppLogger 的项目也可以。</span><span class="sxs-lookup"><span data-stu-id="af3c2-164">AppLogger can consume the targets and props from `Contoso.Utility.UsefulStuff`, as can projects that consume AppLogger.</span></span>

## <a name="adding-a-packagereference-condition"></a><span data-ttu-id="af3c2-165">添加 PackageReference 条件</span><span class="sxs-lookup"><span data-stu-id="af3c2-165">Adding a PackageReference condition</span></span>

<span data-ttu-id="af3c2-166">可使用条件控制是否包括包，在哪种条件可使用任何 MSBuild 变量或者目标或属性文件中定义的变量。</span><span class="sxs-lookup"><span data-stu-id="af3c2-166">You can use a condition to control whether a package is included, where conditions can use any MSBuild variable or a variable defined in the targets or props file.</span></span> <span data-ttu-id="af3c2-167">但目前仅支持 `TargetFramework` 变量。</span><span class="sxs-lookup"><span data-stu-id="af3c2-167">However, at presently, only the `TargetFramework` variable is supported.</span></span>

<span data-ttu-id="af3c2-168">例如，假设目标为 `netstandard1.4` 和 `net452`，但具有的依赖项仅适用于 `net452`。</span><span class="sxs-lookup"><span data-stu-id="af3c2-168">For example, say you're targeting `netstandard1.4` as well as `net452` but have a dependency that is applicable only for `net452`.</span></span> <span data-ttu-id="af3c2-169">在此情况下，你不希望使用包的 `netstandard1.4` 项目添加该不必要的依赖项。</span><span class="sxs-lookup"><span data-stu-id="af3c2-169">In this case you don't want a `netstandard1.4` project that's consuming your package to add that unnecessary dependency.</span></span> <span data-ttu-id="af3c2-170">要防止此情况，请在 `PackageReference` 上指定条件，如下所示：</span><span class="sxs-lookup"><span data-stu-id="af3c2-170">To prevent this, you specify a condition on the `PackageReference` as follows:</span></span>

```xml
<ItemGroup>
    <!-- ... -->
    <PackageReference Include="Newtonsoft.Json" Version="9.0.1" Condition="'$(TargetFramework)' == 'net452'" />
    <!-- ... -->
</ItemGroup>
```

<span data-ttu-id="af3c2-171">使用此项目生成的包会显示，仅对于 `net452` 目标，Newtonsoft.json 包含为依赖项：</span><span class="sxs-lookup"><span data-stu-id="af3c2-171">A package built using this project will show that Newtonsoft.Json is included as a dependency only for a `net452` target:</span></span>

![对 VS2017 的 PackageReference 应用条件的结果](media/PackageReference-Condition.png)

<span data-ttu-id="af3c2-173">还可以在 `ItemGroup` 级别应用条件，并将其应用到所有子级 `PackageReference` 元素：</span><span class="sxs-lookup"><span data-stu-id="af3c2-173">Conditions can also be applied at the `ItemGroup` level and will apply to all children `PackageReference` elements:</span></span>

```xml
<ItemGroup Condition = "'$(TargetFramework)' == 'net452'">
    <!-- ... -->
    <PackageReference Include="Newtonsoft.Json" Version="9.0.1" />
    <PackageReference Include="Contoso.Utility.UsefulStuff" Version="3.6.0" />
    <!-- ... -->
</ItemGroup>
```

## <a name="locking-dependencies"></a><span data-ttu-id="af3c2-174">锁定依赖项</span><span class="sxs-lookup"><span data-stu-id="af3c2-174">Locking dependencies</span></span>
<span data-ttu-id="af3c2-175">NuGet 4.9  或更高版本以及 Visual Studio 2017 15.9  或更高版本随附此功能。 </span><span class="sxs-lookup"><span data-stu-id="af3c2-175">*This feature is available with NuGet **4.9** or above and with Visual Studio 2017 **15.9** or above.*</span></span>

<span data-ttu-id="af3c2-176">对 NuGet 还原的输入是项目文件中的一组包引用（顶级或直接依赖项），而输出则是所有包依赖项的完整闭包，其中包括可传递依赖项。</span><span class="sxs-lookup"><span data-stu-id="af3c2-176">Input to NuGet restore is a set of Package References from the project file (top-level or direct dependencies) and the output is a full closure of all the package dependencies including transitive dependencies.</span></span> <span data-ttu-id="af3c2-177">如果输入 PackageReference 列表尚未更改，则 NuGet 尝试始终生成相同的完整闭包。</span><span class="sxs-lookup"><span data-stu-id="af3c2-177">NuGet tries to always produce the same full closure of package dependencies if the input PackageReference list has not changed.</span></span> <span data-ttu-id="af3c2-178">但是，在某些情况下，它无法执行此操作。</span><span class="sxs-lookup"><span data-stu-id="af3c2-178">However, there are some scenarios where it is unable to do so.</span></span> <span data-ttu-id="af3c2-179">例如:</span><span class="sxs-lookup"><span data-stu-id="af3c2-179">For example:</span></span>

* <span data-ttu-id="af3c2-180">在使用 `<PackageReference Include="My.Sample.Lib" Version="4.*"/>` 等浮动版本时。</span><span class="sxs-lookup"><span data-stu-id="af3c2-180">When you use floating versions like `<PackageReference Include="My.Sample.Lib" Version="4.*"/>`.</span></span> <span data-ttu-id="af3c2-181">尽管在此处这样做的目的是浮动到每个包还原的最新版本，但是在某些情况下，用户需要在一个显式动作后，将图形锁定到某个最新版本并浮动到更高版本（如果有可用的更高版本）。</span><span class="sxs-lookup"><span data-stu-id="af3c2-181">While the intention here is to float to the latest version on every restore of packages, there are scenarios where users require the graph to be locked to a certain latest version and float to a later version, if available, upon an explicit gesture.</span></span>
* <span data-ttu-id="af3c2-182">匹配 PackageReference 版本要求的较新版本已发布。</span><span class="sxs-lookup"><span data-stu-id="af3c2-182">A newer version of the package matching PackageReference version requirements is published.</span></span> <span data-ttu-id="af3c2-183">例如，</span><span class="sxs-lookup"><span data-stu-id="af3c2-183">E.g.</span></span> 

  * <span data-ttu-id="af3c2-184">第 1 天：如果指定了 `<PackageReference Include="My.Sample.Lib" Version="4.0.0"/>`，但在 NuGet 存储库上可用的版本为 4.1.0、4.2.0 和 4.3.0。</span><span class="sxs-lookup"><span data-stu-id="af3c2-184">Day 1: if you specified `<PackageReference Include="My.Sample.Lib" Version="4.0.0"/>` but the versions available on the NuGet repositories were 4.1.0, 4.2.0 and 4.3.0.</span></span> <span data-ttu-id="af3c2-185">在这种情况下，NuGet 将解析为 4.1.0（最接近的最低版本）</span><span class="sxs-lookup"><span data-stu-id="af3c2-185">In this case, NuGet would have resolved to  4.1.0 (nearest minimum version)</span></span>

  * <span data-ttu-id="af3c2-186">第 2 天：版本 4.0.0 发布。</span><span class="sxs-lookup"><span data-stu-id="af3c2-186">Day 2: Version 4.0.0 gets published.</span></span> <span data-ttu-id="af3c2-187">NuGet 现在将查找完全匹配并开始解析到 4.0.0</span><span class="sxs-lookup"><span data-stu-id="af3c2-187">NuGet will now find the exact match and start resolving to 4.0.0</span></span>

* <span data-ttu-id="af3c2-188">给定包版本将从存储库中删除。</span><span class="sxs-lookup"><span data-stu-id="af3c2-188">A given package version is removed from the repository.</span></span> <span data-ttu-id="af3c2-189">尽管 nuget.org 不允许包删除，但并非所有包存储库都具有此约束。</span><span class="sxs-lookup"><span data-stu-id="af3c2-189">Though nuget.org does not allow package deletions, not all package repositories have this constraints.</span></span> <span data-ttu-id="af3c2-190">这导致 NuGet 在无法解析到已删除的版本时查找最佳匹配项。</span><span class="sxs-lookup"><span data-stu-id="af3c2-190">This results in NuGet finding the best match when it cannot resolve to the deleted version.</span></span>

### <a name="enabling-lock-file"></a><span data-ttu-id="af3c2-191">启用锁定文件</span><span class="sxs-lookup"><span data-stu-id="af3c2-191">Enabling lock file</span></span>
<span data-ttu-id="af3c2-192">为了保留包依赖项的完整闭包，可以选择锁定文件功能，方法是通过设置项目的 MSBuild 属性 `RestorePackagesWithLockFile`：</span><span class="sxs-lookup"><span data-stu-id="af3c2-192">In order to persist the full closure of package dependencies you can opt-in to the lock file feature by setting the MSBuild property `RestorePackagesWithLockFile` for your project:</span></span>

```xml
<PropertyGroup>
    <!--- ... -->
    <RestorePackagesWithLockFile>true</RestorePackagesWithLockFile>
    <!--- ... -->
</PropertyGroup>    
```

<span data-ttu-id="af3c2-193">如果设置此属性，NuGet 还原将生成一个锁定文件 - 项目根目录中列出所有包依赖项的 `packages.lock.json` 文件。</span><span class="sxs-lookup"><span data-stu-id="af3c2-193">If this property is set, NuGet restore will generate a lock file - `packages.lock.json` file at the project root directory that lists all the package dependencies.</span></span> 

> [!Note]
> <span data-ttu-id="af3c2-194">一旦项目在其根目录中具有 `packages.lock.json` 文件，则即使在未设置属性 `RestorePackagesWithLockFile` 时，锁定文件仍将始终与还原配合使用。</span><span class="sxs-lookup"><span data-stu-id="af3c2-194">Once a project has `packages.lock.json` file in its root directory, the lock file is always used with restore even if the property `RestorePackagesWithLockFile` is not set.</span></span> <span data-ttu-id="af3c2-195">因此，选择加入此功能的另一个方法是在项目的根目录中创建一个虚拟空白 `packages.lock.json` 文件。</span><span class="sxs-lookup"><span data-stu-id="af3c2-195">So another way to opt-in to this feature is to create a dummy blank `packages.lock.json` file in the project's root directory.</span></span>

### <a name="restore-behavior-with-lock-file"></a><span data-ttu-id="af3c2-196">锁定文件的 `restore` 行为</span><span class="sxs-lookup"><span data-stu-id="af3c2-196">`restore` behavior with lock file</span></span>
<span data-ttu-id="af3c2-197">如果项目存在锁定文件，则 NuGet 使用此锁定文件来运行 `restore`。</span><span class="sxs-lookup"><span data-stu-id="af3c2-197">If a lock file is present for project, NuGet uses this lock file to run `restore`.</span></span> <span data-ttu-id="af3c2-198">NuGet 将执行一次快速检查，以确定在包依赖项中是否存在项目文件（或相关项目的文件）中所提及的任何更改，如果没有任何更改，则它将仅还原锁定文件中提及的包。</span><span class="sxs-lookup"><span data-stu-id="af3c2-198">NuGet does a quick check to see if there were any changes in the package dependencies as mentioned in the project file (or dependent projects' files) and if there were no changes it just restores the packages mentioned in the lock file.</span></span> <span data-ttu-id="af3c2-199">不会对包依赖项进行重新评估。</span><span class="sxs-lookup"><span data-stu-id="af3c2-199">There is no re-evaluation of package dependencies.</span></span>

<span data-ttu-id="af3c2-200">如果 NuGet 检测到在定义的依赖项中存在一个或多个项目文件中提及的更改，它会重新评估包关系图，并将锁定文件更新为反映项目的新闭包。</span><span class="sxs-lookup"><span data-stu-id="af3c2-200">If NuGet detects a change in the defined dependencies as mentioned in the project file(s), it re-evaluates the package graph and updates the lock file to reflect the new package closure for the project.</span></span>

<span data-ttu-id="af3c2-201">对于 CI/CD 和其他方案（不想匆忙更改包依赖项），为此可以将 `lockedmode` 设置为 `true`：</span><span class="sxs-lookup"><span data-stu-id="af3c2-201">For CI/CD and other scenarios, where you would not want to change the package dependencies on the fly, you can do so by setting the `lockedmode` to `true`:</span></span>

<span data-ttu-id="af3c2-202">对于 dotnet.exe，请运行：</span><span class="sxs-lookup"><span data-stu-id="af3c2-202">For dotnet.exe, run:</span></span>
```
> dotnet.exe restore --locked-mode
```

<span data-ttu-id="af3c2-203">对于 msbuild.exe，请运行：</span><span class="sxs-lookup"><span data-stu-id="af3c2-203">For msbuild.exe, run:</span></span>
```
> msbuild.exe -t:restore -p:RestoreLockedMode=true
```

<span data-ttu-id="af3c2-204">此外，还可以在项目文件中设置此条件 MSBuild 属性：</span><span class="sxs-lookup"><span data-stu-id="af3c2-204">You may also set this conditional MSBuild property in your project file:</span></span>
```xml
<PropertyGroup>
    <!--- ... -->
    <RestoreLockedMode>true</RestoreLockedMode>
    <!--- ... -->
</PropertyGroup> 
```

<span data-ttu-id="af3c2-205">如果锁定模式为 `true`，则还原将还原锁定文件中列出的完全匹配的包，或者，如果在锁定文件创建后为项目更新了定义的包依赖项，则还原将失败。</span><span class="sxs-lookup"><span data-stu-id="af3c2-205">If locked mode is `true`, restore will either restore the exact packages as listed in the lock file or fail if you updated the defined package dependencies for the project after lock file was created.</span></span>

### <a name="make-lock-file-part-of-your-source-repository"></a><span data-ttu-id="af3c2-206">使锁定文件作为源存储库的一部分</span><span class="sxs-lookup"><span data-stu-id="af3c2-206">Make lock file part of your source repository</span></span>
<span data-ttu-id="af3c2-207">若要生成应用程序，且可执行文件和相关项目位于依赖关系链的开头，请将锁定文件签入源代码存储库，以便 NuGet 能够在还原期间使用它。</span><span class="sxs-lookup"><span data-stu-id="af3c2-207">If you are building an application, an executable and the project in question is at the start of the dependency chain then do check in the lock file to the source code repository so that NuGet can make use of it during restore.</span></span>

<span data-ttu-id="af3c2-208">但是，如果你的项目是不交付的库项目或其他项目依赖的常用代码项目，则不应  将锁定文件作为源代码的一部分签入。</span><span class="sxs-lookup"><span data-stu-id="af3c2-208">However, if your project is a library project that you do not ship or a common code project on which other projects depend upon, you **should not** check in the lock file as part of your source code.</span></span> <span data-ttu-id="af3c2-209">保留锁定文件没有任何坏处，但在依赖于此常用代码项目的项目还原/生成期间，锁定文件中列出的常用代码项目的锁定的包依赖项可能无法使用。</span><span class="sxs-lookup"><span data-stu-id="af3c2-209">There is no harm in keeping the lock file but the locked package dependencies for the common code project may not be used, as listed in the lock file, during the restore/build of a project that depends on this common-code project.</span></span>

<span data-ttu-id="af3c2-210">例如，</span><span class="sxs-lookup"><span data-stu-id="af3c2-210">Eg.</span></span>
```
ProjectA
  |------> PackageX 2.0.0
  |------> ProjectB
             |------>PackageX 1.0.0
```
<span data-ttu-id="af3c2-211">如果 `ProjectA` 在 `PackageX` 版本 `2.0.0` 上具有依赖项并引用依赖于 `PackageX` 版本 `1.0.0` 的 `ProjectB`，则 `ProjectB` 的锁定文件将列出 `PackageX` 版本 `1.0.0` 的依赖项。</span><span class="sxs-lookup"><span data-stu-id="af3c2-211">If `ProjectA` has a dependency on a `PackageX` version `2.0.0` and also references `ProjectB` that depends on `PackageX` version `1.0.0`, then the lock file for `ProjectB` will list a dependency on `PackageX` version `1.0.0`.</span></span> <span data-ttu-id="af3c2-212">但是，当生成 `ProjectA` 时，其锁定文件将包含 `ProjectB` 锁定文件中列出的 `PackageX` 版本 `2.0.0`  （而不是 `1.0.0`  ）上的依赖项。</span><span class="sxs-lookup"><span data-stu-id="af3c2-212">However, when `ProjectA` is built, its lock file will contain a dependency on `PackageX` version **`2.0.0`** and **not** `1.0.0` as listed in the lock file for `ProjectB`.</span></span> <span data-ttu-id="af3c2-213">因此，常用代码项目的锁定文件对依赖于它的项目进行解析的包几乎没有控制。</span><span class="sxs-lookup"><span data-stu-id="af3c2-213">Thus, the lock file of a common code project has little say over the packages resolved for projects that depend on it.</span></span>

### <a name="lock-file-extensibility"></a><span data-ttu-id="af3c2-214">锁定文件可扩展性</span><span class="sxs-lookup"><span data-stu-id="af3c2-214">Lock file extensibility</span></span>
<span data-ttu-id="af3c2-215">可以使用以下所述的锁定文件控制各种还原行为：</span><span class="sxs-lookup"><span data-stu-id="af3c2-215">You can control various behaviors of restore with lock file as described below:</span></span>

| <span data-ttu-id="af3c2-216">选项</span><span class="sxs-lookup"><span data-stu-id="af3c2-216">Option</span></span> | <span data-ttu-id="af3c2-217">MSBuild 等效选项</span><span class="sxs-lookup"><span data-stu-id="af3c2-217">MSBuild equivalent option</span></span> | 
|:---  |:--- |
| `--use-lock-file` | <span data-ttu-id="af3c2-218">为项目启动锁定文件的使用。</span><span class="sxs-lookup"><span data-stu-id="af3c2-218">Bootstraps use of lock file for a project.</span></span> <span data-ttu-id="af3c2-219">或者，可以在项目文件中设置 `RestorePackagesWithLockFile` 属性</span><span class="sxs-lookup"><span data-stu-id="af3c2-219">You can alternatively set `RestorePackagesWithLockFile` property in the project file</span></span> | 
| `--locked-mode` | <span data-ttu-id="af3c2-220">为还原启用锁定模式。</span><span class="sxs-lookup"><span data-stu-id="af3c2-220">Enables locked mode for restore.</span></span> <span data-ttu-id="af3c2-221">这对于要获取可重复生成的 CI/CD 方案非常有用。</span><span class="sxs-lookup"><span data-stu-id="af3c2-221">This is useful in CI/CD scenarios where you would like to get the repeatable builds.</span></span> <span data-ttu-id="af3c2-222">通过将 `RestoreLockedMode` MSBuild 属性设置为 `true` 也可以实现此目的</span><span class="sxs-lookup"><span data-stu-id="af3c2-222">This can be also by setting the `RestoreLockedMode` MSBuild property to `true`</span></span> |  
| `--force-evaluate` | <span data-ttu-id="af3c2-223">对于在项目中定义了浮动版本的包，此选项也非常有用。</span><span class="sxs-lookup"><span data-stu-id="af3c2-223">This option is useful with packages with floating version defined in the project.</span></span> <span data-ttu-id="af3c2-224">默认情况下，NuGet 还原不会在每次还原时自动更新包版本，除非使用 `--force-evaluate` 选项运行还原。</span><span class="sxs-lookup"><span data-stu-id="af3c2-224">By default, NuGet restore will not update the package version automatically upon each restore unless you run restore with `--force-evaluate` option.</span></span> |
| `--lock-file-path` | <span data-ttu-id="af3c2-225">为项目定义自定义锁定文件位置。</span><span class="sxs-lookup"><span data-stu-id="af3c2-225">Defines a custom lock file location for a project.</span></span> <span data-ttu-id="af3c2-226">这也可以通过设置 MSBuild 属性 `NuGetLockFilePath` 来实现。</span><span class="sxs-lookup"><span data-stu-id="af3c2-226">This can be also achieved by setting the MSBuild property `NuGetLockFilePath`.</span></span> <span data-ttu-id="af3c2-227">默认情况下，NuGet 支持根目录中的 `packages.lock.json`。</span><span class="sxs-lookup"><span data-stu-id="af3c2-227">By default, NuGet supports `packages.lock.json` at the root directory.</span></span> <span data-ttu-id="af3c2-228">如果在同一目录中具有多个项目，则 NuGet 支持特定于项目的锁定文件 `packages.<project_name>.lock.json`</span><span class="sxs-lookup"><span data-stu-id="af3c2-228">If you have multiple projects in the same directory, NuGet supports project specific lock file `packages.<project_name>.lock.json`</span></span> |
