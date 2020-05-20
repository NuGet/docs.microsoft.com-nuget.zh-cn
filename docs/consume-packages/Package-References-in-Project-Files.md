---
title: NuGet PackageReference 格式（项目文件中的包引用）
description: 详细介绍项目文件中 NuGet 4.0+、VS2017 和 .NET Core 2.0 支持的 NuGet PackageReference
author: karann-msft
ms.author: karann
ms.date: 03/16/2018
ms.topic: conceptual
ms.openlocfilehash: a5833df60c5f7905359f421141347b1237f45d86
ms.sourcegitcommit: 2b50c450cca521681a384aa466ab666679a40213
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/07/2020
ms.locfileid: "79428503"
---
# <a name="package-references-packagereference-in-project-files"></a><span data-ttu-id="20044-103">项目文件中的包引用 (PackageReference)</span><span class="sxs-lookup"><span data-stu-id="20044-103">Package references (PackageReference) in project files</span></span>

<span data-ttu-id="20044-104">使用 `PackageReference` 节点的包引用可直接在项目文件中管理 NuGet 依赖项（无需单独的 `packages.config` 文件）。</span><span class="sxs-lookup"><span data-stu-id="20044-104">Package references, using the `PackageReference` node, manage NuGet dependencies directly within project files (as opposed to a separate `packages.config` file).</span></span> <span data-ttu-id="20044-105">使用所谓的 PackageReference 不会影响 NuGet 的其他方面；例如，仍按照[常规 NuGet 配置](configuring-nuget-behavior.md)中的说明应用 `NuGet.config` 文件（包括包源）中的设置。</span><span class="sxs-lookup"><span data-stu-id="20044-105">Using PackageReference, as it's called, doesn't affect other aspects of NuGet; for example, settings in `NuGet.config` files (including package sources) are still applied as explained in [Common NuGet configurations](configuring-nuget-behavior.md).</span></span>

<span data-ttu-id="20044-106">借助 PackageReference，还可使用 MSBuild 条件按目标框架或其他分组选择包引用。</span><span class="sxs-lookup"><span data-stu-id="20044-106">With PackageReference, you can also use MSBuild conditions to choose package references per target framework, or other groupings.</span></span> <span data-ttu-id="20044-107">它还允许对依赖项和内容流实行精细控制。</span><span class="sxs-lookup"><span data-stu-id="20044-107">It also allows for fine-grained control over dependencies and content flow.</span></span> <span data-ttu-id="20044-108">（有关更多详细信息，请参阅[NuGet 打包和还原为 MSBuild 目标](../reference/msbuild-targets.md)。）</span><span class="sxs-lookup"><span data-stu-id="20044-108">(See For more details [NuGet pack and restore as MSBuild targets](../reference/msbuild-targets.md).)</span></span>

## <a name="project-type-support"></a><span data-ttu-id="20044-109">项目类型支持</span><span class="sxs-lookup"><span data-stu-id="20044-109">Project type support</span></span>

<span data-ttu-id="20044-110">默认情况下，PackageReference 用于 .NET Core 项目、.NET Standard 项目，以及面向 Windows 10 Build 15063（创意者更新）及更高版本的 UWP 项目（C++ UWP 项目除外）。</span><span class="sxs-lookup"><span data-stu-id="20044-110">By default, PackageReference is used for .NET Core projects, .NET Standard projects, and UWP projects targeting Windows 10 Build 15063 (Creators Update) and later, with the exception of C++ UWP projects.</span></span> <span data-ttu-id="20044-111">.NET 框架项目支持 PackageReference，但当前默认为 `packages.config`。</span><span class="sxs-lookup"><span data-stu-id="20044-111">.NET Framework projects support PackageReference, but currently default to `packages.config`.</span></span> <span data-ttu-id="20044-112">若要使用 PackageReference，请将 `packages.config` 中的依赖项[迁移](../consume-packages/migrate-packages-config-to-package-reference.md)到项目文件中，然后删除 packages.config。</span><span class="sxs-lookup"><span data-stu-id="20044-112">To use PackageReference, [migrate](../consume-packages/migrate-packages-config-to-package-reference.md) the dependencies from `packages.config` into your project file, then remove packages.config.</span></span>

<span data-ttu-id="20044-113">面向完整 .NET Framework 的 ASP.NET 应用仅包括对 PackageReference 的[有限支持](https://github.com/NuGet/Home/issues/5877)。</span><span class="sxs-lookup"><span data-stu-id="20044-113">ASP.NET apps targeting the full .NET Framework include only [limited support](https://github.com/NuGet/Home/issues/5877) for PackageReference.</span></span> <span data-ttu-id="20044-114">不支持 C++ 和 JavaScript 项目类型。</span><span class="sxs-lookup"><span data-stu-id="20044-114">C++ and JavaScript project types are unsupported.</span></span>

## <a name="adding-a-packagereference"></a><span data-ttu-id="20044-115">添加 PackageReference</span><span class="sxs-lookup"><span data-stu-id="20044-115">Adding a PackageReference</span></span>

<span data-ttu-id="20044-116">在项目文件中使用以下语法添加依赖项：</span><span class="sxs-lookup"><span data-stu-id="20044-116">Add a dependency in your project file using the following syntax:</span></span>

```xml
<ItemGroup>
    <!-- ... -->
    <PackageReference Include="Contoso.Utility.UsefulStuff" Version="3.6.0" />
    <!-- ... -->
</ItemGroup>
```

## <a name="controlling-dependency-version"></a><span data-ttu-id="20044-117">控制依赖项版本</span><span class="sxs-lookup"><span data-stu-id="20044-117">Controlling dependency version</span></span>

<span data-ttu-id="20044-118">用于指定包版本的约定与使用 `packages.config` 时的约定相同：</span><span class="sxs-lookup"><span data-stu-id="20044-118">The convention for specifying the version of a package is the same as when using `packages.config`:</span></span>

```xml
<ItemGroup>
    <!-- ... -->
    <PackageReference Include="Contoso.Utility.UsefulStuff" Version="3.6.0" />
    <!-- ... -->
</ItemGroup>
```

<span data-ttu-id="20044-119">在上述示例中，3.6.0 指 >=3.6.0 的任何版本（首选项为最低版本），详见[包版本控制](../concepts/package-versioning.md#version-ranges)。</span><span class="sxs-lookup"><span data-stu-id="20044-119">In the example above, 3.6.0 means any version that is >=3.6.0 with preference for the lowest version, as described on [Package versioning](../concepts/package-versioning.md#version-ranges).</span></span>

## <a name="using-packagereference-for-a-project-with-no-packagereferences"></a><span data-ttu-id="20044-120">对没有 PackageReferences 的项目使用 PackageReference</span><span class="sxs-lookup"><span data-stu-id="20044-120">Using PackageReference for a project with no PackageReferences</span></span>

<span data-ttu-id="20044-121">高级：如果项目中没有安装包（项目文件中没有 PackageReference，也没有 packages.config 文件），但想要项目还原为 PackageReference 样式，则可以在项目文件中将项目属性 RestoreProjectStyle 设置为 PackageReference。</span><span class="sxs-lookup"><span data-stu-id="20044-121">Advanced: If you have no packages installed in a project (no PackageReferences in project file and no packages.config file), but want the project to be restored as PackageReference style, you can set a Project property RestoreProjectStyle to PackageReference in your project file.</span></span>

```xml
<PropertyGroup>
    <!--- ... -->
    <RestoreProjectStyle>PackageReference</RestoreProjectStyle>
    <!--- ... -->
</PropertyGroup>    
```

<span data-ttu-id="20044-122">如果引用 PackageReference 样式的项目（现有 csproj 或 SDK 样式的项目），这可能很有用。</span><span class="sxs-lookup"><span data-stu-id="20044-122">This may be useful, if you reference projects which are PackageReference styled (existing csproj or SDK-style projects).</span></span> <span data-ttu-id="20044-123">这可让其他项目以“可传递”的方式引用这些项目引用的包。</span><span class="sxs-lookup"><span data-stu-id="20044-123">This will enable packages that those projects refer to, to be "transitively" referenced by your project.</span></span>

## <a name="packagereference-and-sources"></a><span data-ttu-id="20044-124">PackageReference 和源</span><span class="sxs-lookup"><span data-stu-id="20044-124">PackageReference and sources</span></span>

<span data-ttu-id="20044-125">在 PackageReference 项目中，在还原时解析可传递依赖项版本。</span><span class="sxs-lookup"><span data-stu-id="20044-125">In PackageReference projects, the transitive dependency versions are resolved at restore time.</span></span> <span data-ttu-id="20044-126">因此，在 PackageReference 项目中，所有源必须可用于所有还原。</span><span class="sxs-lookup"><span data-stu-id="20044-126">As such, in PackageReference projects all sources need to be available for all restores.</span></span> 

## <a name="floating-versions"></a><span data-ttu-id="20044-127">可变版本</span><span class="sxs-lookup"><span data-stu-id="20044-127">Floating Versions</span></span>

<span data-ttu-id="20044-128">`PackageReference` 支持[可变版本](../concepts/dependency-resolution.md#floating-versions)：</span><span class="sxs-lookup"><span data-stu-id="20044-128">[Floating versions](../concepts/dependency-resolution.md#floating-versions) are supported with `PackageReference`:</span></span>

```xml
<ItemGroup>
    <!-- ... -->
    <PackageReference Include="Contoso.Utility.UsefulStuff" Version="3.6.*" />
    <PackageReference Include="Contoso.Utility.UsefulStuff" Version="3.6.0-beta*" />
    <!-- ... -->
</ItemGroup>
```

## <a name="controlling-dependency-assets"></a><span data-ttu-id="20044-129">控制依赖项资产</span><span class="sxs-lookup"><span data-stu-id="20044-129">Controlling dependency assets</span></span>

<span data-ttu-id="20044-130">你可能只是将依赖项用作开发工具，而不希望将它向会使用包的项目公开。</span><span class="sxs-lookup"><span data-stu-id="20044-130">You might be using a dependency purely as a development harness and might not want to expose that to projects that will consume your package.</span></span> <span data-ttu-id="20044-131">在此情况下，可使用 `PrivateAssets` 元数据控制此行为。</span><span class="sxs-lookup"><span data-stu-id="20044-131">In this scenario, you can use the `PrivateAssets` metadata to control this behavior.</span></span>

```xml
<ItemGroup>
    <!-- ... -->

    <PackageReference Include="Contoso.Utility.UsefulStuff" Version="3.6.0">
        <PrivateAssets>all</PrivateAssets>
    </PackageReference>

    <!-- ... -->
</ItemGroup>
```

<span data-ttu-id="20044-132">以下元数据标记控制依赖项资产：</span><span class="sxs-lookup"><span data-stu-id="20044-132">The following metadata tags control dependency assets:</span></span>

| <span data-ttu-id="20044-133">标记</span><span class="sxs-lookup"><span data-stu-id="20044-133">Tag</span></span> | <span data-ttu-id="20044-134">说明</span><span class="sxs-lookup"><span data-stu-id="20044-134">Description</span></span> | <span data-ttu-id="20044-135">默认值</span><span class="sxs-lookup"><span data-stu-id="20044-135">Default Value</span></span> |
| --- | --- | --- |
| <span data-ttu-id="20044-136">IncludeAssets</span><span class="sxs-lookup"><span data-stu-id="20044-136">IncludeAssets</span></span> | <span data-ttu-id="20044-137">将使用这些资产</span><span class="sxs-lookup"><span data-stu-id="20044-137">These assets will be consumed</span></span> | <span data-ttu-id="20044-138">all</span><span class="sxs-lookup"><span data-stu-id="20044-138">all</span></span> |
| <span data-ttu-id="20044-139">ExcludeAssets</span><span class="sxs-lookup"><span data-stu-id="20044-139">ExcludeAssets</span></span> | <span data-ttu-id="20044-140">不会使用这些资产</span><span class="sxs-lookup"><span data-stu-id="20044-140">These assets will not be consumed</span></span> | <span data-ttu-id="20044-141">none</span><span class="sxs-lookup"><span data-stu-id="20044-141">none</span></span> |
| <span data-ttu-id="20044-142">PrivateAssets</span><span class="sxs-lookup"><span data-stu-id="20044-142">PrivateAssets</span></span> | <span data-ttu-id="20044-143">将使用这些资产，但它们不会流入上级项目</span><span class="sxs-lookup"><span data-stu-id="20044-143">These assets will be consumed but won't flow to the parent project</span></span> | <span data-ttu-id="20044-144">contentfiles;analyzers;build</span><span class="sxs-lookup"><span data-stu-id="20044-144">contentfiles;analyzers;build</span></span> |

<span data-ttu-id="20044-145">以下是这些标记的允许值，其中用分号分隔多个值（但 `all` 和 `none` 必须单独显示）：</span><span class="sxs-lookup"><span data-stu-id="20044-145">Allowable values for these tags are as follows, with multiple values separated by a semicolon except with `all` and `none` which must appear by themselves:</span></span>

| <span data-ttu-id="20044-146">值</span><span class="sxs-lookup"><span data-stu-id="20044-146">Value</span></span> | <span data-ttu-id="20044-147">说明</span><span class="sxs-lookup"><span data-stu-id="20044-147">Description</span></span> |
| --- | ---
| <span data-ttu-id="20044-148">编译</span><span class="sxs-lookup"><span data-stu-id="20044-148">compile</span></span> | <span data-ttu-id="20044-149">`lib` 文件夹的内容，控制项目能否对文件夹中的程序集进行编译</span><span class="sxs-lookup"><span data-stu-id="20044-149">Contents of the `lib` folder and controls whether your project can compile against the assemblies within the folder</span></span> |
| <span data-ttu-id="20044-150">运行库</span><span class="sxs-lookup"><span data-stu-id="20044-150">runtime</span></span> | <span data-ttu-id="20044-151">`lib` 和 `runtimes` 文件夹的内容，控制是否会复制这些程序集，以生成输出目录</span><span class="sxs-lookup"><span data-stu-id="20044-151">Contents of the `lib` and `runtimes` folder and controls whether these assemblies will be copied out to the build output directory</span></span> |
| <span data-ttu-id="20044-152">contentFiles</span><span class="sxs-lookup"><span data-stu-id="20044-152">contentFiles</span></span> | <span data-ttu-id="20044-153">`contentfiles` 文件夹中的内容</span><span class="sxs-lookup"><span data-stu-id="20044-153">Contents of the `contentfiles` folder</span></span> |
| <span data-ttu-id="20044-154">build</span><span class="sxs-lookup"><span data-stu-id="20044-154">build</span></span> | <span data-ttu-id="20044-155">`build` 文件夹中的 `.props` 和 `.targets`</span><span class="sxs-lookup"><span data-stu-id="20044-155">`.props` and `.targets` in the `build` folder</span></span> |
| <span data-ttu-id="20044-156">buildMultitargeting</span><span class="sxs-lookup"><span data-stu-id="20044-156">buildMultitargeting</span></span> | <span data-ttu-id="20044-157">(4.0) *文件夹中跨框架目标的* 和 `.props``.targets``buildMultitargeting`</span><span class="sxs-lookup"><span data-stu-id="20044-157">*(4.0)* `.props` and `.targets` in the `buildMultitargeting` folder, for cross-framework targeting</span></span> |
| <span data-ttu-id="20044-158">buildTransitive</span><span class="sxs-lookup"><span data-stu-id="20044-158">buildTransitive</span></span> | <span data-ttu-id="20044-159">(5.0+) 以可传递的方式流入任意使用项目的资产的 *文件夹中的* 和 `.props``.targets``buildTransitive`。</span><span class="sxs-lookup"><span data-stu-id="20044-159">*(5.0+)* `.props` and `.targets` in the `buildTransitive` folder, for assets that flow transitively to any consuming project.</span></span> <span data-ttu-id="20044-160">请参阅[功能](https://github.com/NuGet/Home/wiki/Allow-package--authors-to-define-build-assets-transitive-behavior)页。</span><span class="sxs-lookup"><span data-stu-id="20044-160">See the [feature](https://github.com/NuGet/Home/wiki/Allow-package--authors-to-define-build-assets-transitive-behavior) page.</span></span> |
| <span data-ttu-id="20044-161">analyzers</span><span class="sxs-lookup"><span data-stu-id="20044-161">analyzers</span></span> | <span data-ttu-id="20044-162">.NET 分析器</span><span class="sxs-lookup"><span data-stu-id="20044-162">.NET analyzers</span></span> |
| <span data-ttu-id="20044-163">本机</span><span class="sxs-lookup"><span data-stu-id="20044-163">native</span></span> | <span data-ttu-id="20044-164">`native` 文件夹中的内容</span><span class="sxs-lookup"><span data-stu-id="20044-164">Contents of the `native` folder</span></span> |
| <span data-ttu-id="20044-165">none</span><span class="sxs-lookup"><span data-stu-id="20044-165">none</span></span> | <span data-ttu-id="20044-166">不使用以上任何内容。</span><span class="sxs-lookup"><span data-stu-id="20044-166">None of the above are used.</span></span> |
| <span data-ttu-id="20044-167">all</span><span class="sxs-lookup"><span data-stu-id="20044-167">all</span></span> | <span data-ttu-id="20044-168">以上都是（除 `none` 之外）</span><span class="sxs-lookup"><span data-stu-id="20044-168">All of the above (except `none`)</span></span> |

<span data-ttu-id="20044-169">在以下示例中，项目将使用除包中的内容文件之外的所有项，并且除内容文件和分析器之外的所有项均会流入上级项目。</span><span class="sxs-lookup"><span data-stu-id="20044-169">In the following example, everything except the content files from the package would be consumed by the project and everything except content files and analyzers would flow to the parent project.</span></span>

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

<span data-ttu-id="20044-170">请注意，因为 `PrivateAssets` 未包括 `build`，所以目标和属性将流入上级项目。</span><span class="sxs-lookup"><span data-stu-id="20044-170">Note that because `build` is not included with `PrivateAssets`, targets and props *will* flow to the parent project.</span></span> <span data-ttu-id="20044-171">例如，假设在生成名为 AppLogger 的 NuGet 包的项目中使用上述引用。</span><span class="sxs-lookup"><span data-stu-id="20044-171">Consider, for example, that the reference above is used in a project that builds a NuGet package called AppLogger.</span></span> <span data-ttu-id="20044-172">AppLogger 可以使用 `Contoso.Utility.UsefulStuff` 中的目标和属性，使用 AppLogger 的项目也可以。</span><span class="sxs-lookup"><span data-stu-id="20044-172">AppLogger can consume the targets and props from `Contoso.Utility.UsefulStuff`, as can projects that consume AppLogger.</span></span>

> [!NOTE]
> <span data-ttu-id="20044-173">在 `.nuspec` 文件中将 `developmentDependency` 设置为 `true` 时，会将包标记为仅开发依赖项，从而防止包作为依赖项包含到其他包中。</span><span class="sxs-lookup"><span data-stu-id="20044-173">When `developmentDependency` is set to `true` in a `.nuspec` file, this marks a package as a development-only dependency, which prevents the package from being included as a dependency in other packages.</span></span> <span data-ttu-id="20044-174">利用 PackageReference (NuGet 4.8+)  ，此标志还意味着将从编译中排除编译时资产。</span><span class="sxs-lookup"><span data-stu-id="20044-174">With PackageReference *(NuGet 4.8+)*, this flag also means that it will exclude compile-time assets from compilation.</span></span> <span data-ttu-id="20044-175">有关详细信息，请参阅 [PackageReference 的 DevelopmentDependency 支持](https://github.com/NuGet/Home/wiki/DevelopmentDependency-support-for-PackageReference)。</span><span class="sxs-lookup"><span data-stu-id="20044-175">For more information, see [DevelopmentDependency support for PackageReference](https://github.com/NuGet/Home/wiki/DevelopmentDependency-support-for-PackageReference).</span></span>

## <a name="adding-a-packagereference-condition"></a><span data-ttu-id="20044-176">添加 PackageReference 条件</span><span class="sxs-lookup"><span data-stu-id="20044-176">Adding a PackageReference condition</span></span>

<span data-ttu-id="20044-177">可使用条件控制是否包括包，在哪种条件可使用任何 MSBuild 变量或者目标或属性文件中定义的变量。</span><span class="sxs-lookup"><span data-stu-id="20044-177">You can use a condition to control whether a package is included, where conditions can use any MSBuild variable or a variable defined in the targets or props file.</span></span> <span data-ttu-id="20044-178">但目前仅支持 `TargetFramework` 变量。</span><span class="sxs-lookup"><span data-stu-id="20044-178">However, at presently, only the `TargetFramework` variable is supported.</span></span>

<span data-ttu-id="20044-179">例如，假设目标为 `netstandard1.4` 和 `net452`，但具有的依赖项仅适用于 `net452`。</span><span class="sxs-lookup"><span data-stu-id="20044-179">For example, say you're targeting `netstandard1.4` as well as `net452` but have a dependency that is applicable only for `net452`.</span></span> <span data-ttu-id="20044-180">在此情况下，你不希望使用包的 `netstandard1.4` 项目添加该不必要的依赖项。</span><span class="sxs-lookup"><span data-stu-id="20044-180">In this case you don't want a `netstandard1.4` project that's consuming your package to add that unnecessary dependency.</span></span> <span data-ttu-id="20044-181">要防止此情况，请在 `PackageReference` 上指定条件，如下所示：</span><span class="sxs-lookup"><span data-stu-id="20044-181">To prevent this, you specify a condition on the `PackageReference` as follows:</span></span>

```xml
<ItemGroup>
    <!-- ... -->
    <PackageReference Include="Newtonsoft.Json" Version="9.0.1" Condition="'$(TargetFramework)' == 'net452'" />
    <!-- ... -->
</ItemGroup>
```

<span data-ttu-id="20044-182">使用此项目生成的包会显示，仅对于 `net452` 目标，Newtonsoft.json 包含为依赖项：</span><span class="sxs-lookup"><span data-stu-id="20044-182">A package built using this project will show that Newtonsoft.Json is included as a dependency only for a `net452` target:</span></span>

![对 VS2017 的 PackageReference 应用条件的结果](media/PackageReference-Condition.png)

<span data-ttu-id="20044-184">还可以在 `ItemGroup` 级别应用条件，并将其应用到所有子级 `PackageReference` 元素：</span><span class="sxs-lookup"><span data-stu-id="20044-184">Conditions can also be applied at the `ItemGroup` level and will apply to all children `PackageReference` elements:</span></span>

```xml
<ItemGroup Condition = "'$(TargetFramework)' == 'net452'">
    <!-- ... -->
    <PackageReference Include="Newtonsoft.Json" Version="9.0.1" />
    <PackageReference Include="Contoso.Utility.UsefulStuff" Version="3.6.0" />
    <!-- ... -->
</ItemGroup>
```

## <a name="generatepathproperty"></a><span data-ttu-id="20044-185">GeneratePathProperty</span><span class="sxs-lookup"><span data-stu-id="20044-185">GeneratePathProperty</span></span>

<span data-ttu-id="20044-186">NuGet 5.0 或更高版本以及 Visual Studio 2019 16.0 或更高版本随附此功能   。</span><span class="sxs-lookup"><span data-stu-id="20044-186">This feature is available with NuGet **5.0** or above and with Visual Studio 2019 **16.0** or above.</span></span>

<span data-ttu-id="20044-187">有时需要从 MSBuild 目标引用包中的文件。</span><span class="sxs-lookup"><span data-stu-id="20044-187">Sometimes it is desirable to reference files in a package from an MSBuild target.</span></span>
<span data-ttu-id="20044-188">在基于 `packages.config` 的项目中，包安装在项目文件所在的文件夹中。</span><span class="sxs-lookup"><span data-stu-id="20044-188">In `packages.config` based projects, the packages are installed in a folder relative to the project file.</span></span> <span data-ttu-id="20044-189">但是，在 PackageReference 中，包是在 global-packages 文件夹中[使用](../concepts/package-installation-process.md)的，此文件可能会因计算机而异  。</span><span class="sxs-lookup"><span data-stu-id="20044-189">However in PackageReference, the packages are [consumed](../concepts/package-installation-process.md) from the *global-packages* folder, which can vary from machine to machine.</span></span>

<span data-ttu-id="20044-190">为了消除这种差异，NuGet 引入了一个指向包使用位置的属性。</span><span class="sxs-lookup"><span data-stu-id="20044-190">To bridge that gap, NuGet introduced a property that points to the location from which the package will be consumed.</span></span>

<span data-ttu-id="20044-191">示例：</span><span class="sxs-lookup"><span data-stu-id="20044-191">Example:</span></span>

```xml
  <ItemGroup>
      <PackageReference Include="Some.Package" Version="1.0.0" GeneratePathProperty="true" />
  </ItemGroup>

  <Target Name="TakeAction" AfterTargets="Build">
    <Exec Command="$(PkgSome_Package)\something.exe" />
  </Target>
````

<span data-ttu-id="20044-192">此外，NuGet 会对包含 tools 文件夹的包自动生成属性。</span><span class="sxs-lookup"><span data-stu-id="20044-192">Additionally NuGet will automatically generate properties for packages containing a tools folder.</span></span>

```xml
  <ItemGroup>
      <PackageReference Include="Package.With.Tools" Version="1.0.0" />
  </ItemGroup>

  <Target Name="TakeAction" AfterTargets="Build">
    <Exec Command="$(PkgPackage_With_Tools)\tools\tool.exe" />
  </Target>
````

<span data-ttu-id="20044-193">MSBuild 属性和包标识不具有相同的限制，因此包标识需要改为一个 MSBuild 易记名称（以 `Pkg` 为前缀）。</span><span class="sxs-lookup"><span data-stu-id="20044-193">MSBuild properties and package identities do not have the same restrictions so the package identity needs to be changed to an MSBuild friendly name, prefixed by the word `Pkg`.</span></span>
<span data-ttu-id="20044-194">若要验证生成的属性的确切名称，请查看生成的 [nuget.g.props](../reference/msbuild-targets.md#restore-outputs) 文件。</span><span class="sxs-lookup"><span data-stu-id="20044-194">To verify the exact name of the property generated, look at the generated [nuget.g.props](../reference/msbuild-targets.md#restore-outputs) file.</span></span>

## <a name="nuget-warnings-and-errors"></a><span data-ttu-id="20044-195">NuGet 警告和错误</span><span class="sxs-lookup"><span data-stu-id="20044-195">NuGet warnings and errors</span></span>

<span data-ttu-id="20044-196">NuGet 4.3 或更高版本以及 Visual Studio 2017 15.3 或更高版本随附此功能。</span><span class="sxs-lookup"><span data-stu-id="20044-196">*This feature is available with NuGet **4.3** or above and with Visual Studio 2017 **15.3** or above.*</span></span>

<span data-ttu-id="20044-197">对于许多打包和还原方案，所有 NuGet 警告和错误都经过编码，且以 `NU****` 开头。</span><span class="sxs-lookup"><span data-stu-id="20044-197">For many pack and restore scenarios, all NuGet warnings and errors are coded, and start with `NU****`.</span></span> <span data-ttu-id="20044-198">所有 NuGet 警告和错误都列在[参考](../reference/errors-and-warnings.md)文档中。</span><span class="sxs-lookup"><span data-stu-id="20044-198">All NuGet warnings and errors are listed in the [reference](../reference/errors-and-warnings.md) documentation.</span></span>

<span data-ttu-id="20044-199">NuGet 遵循以下警告属性：</span><span class="sxs-lookup"><span data-stu-id="20044-199">NuGet observes the following warning properties:</span></span>

- <span data-ttu-id="20044-200">`TreatWarningsAsErrors` 将所有警告视为错误</span><span class="sxs-lookup"><span data-stu-id="20044-200">`TreatWarningsAsErrors`, treat all warnings as errors</span></span>
- <span data-ttu-id="20044-201">`WarningsAsErrors` 将特定警告报告为错误</span><span class="sxs-lookup"><span data-stu-id="20044-201">`WarningsAsErrors`, treat specific warnings as errors</span></span>
- <span data-ttu-id="20044-202">`NoWarn` 隐藏项目范围或包范围内的特定警告。</span><span class="sxs-lookup"><span data-stu-id="20044-202">`NoWarn`, hide specific warnings, either project-wide or package-wide.</span></span>

<span data-ttu-id="20044-203">示例：</span><span class="sxs-lookup"><span data-stu-id="20044-203">Examples:</span></span>

```xml
<PropertyGroup>
    <TreatWarningsAsErrors>true</TreatWarningsAsErrors>
</PropertyGroup>
...
<PropertyGroup>
    <WarningsAsErrors>$(WarningsAsErrors);NU1603;NU1605</WarningsAsErrors>
</PropertyGroup>
...
<PropertyGroup>
    <NoWarn>$(NoWarn);NU5124</NoWarn>
</PropertyGroup>
...
<ItemGroup>
    <PackageReference Include="Contoso.Package" Version="1.0.0" NoWarn="NU1605" />
</ItemGroup>
```

### <a name="suppressing-nuget-warnings"></a><span data-ttu-id="20044-204">阻止 NuGet 警告</span><span class="sxs-lookup"><span data-stu-id="20044-204">Suppressing NuGet warnings</span></span>

<span data-ttu-id="20044-205">虽然推荐在打包和还原操作期间解决所有 NuGet 警告，在某些情况下可以禁止显示警告。</span><span class="sxs-lookup"><span data-stu-id="20044-205">While it is recommended that you resolve all NuGet warnings during your pack and restore operations, in certain situations suppressing them is warranted.</span></span>
<span data-ttu-id="20044-206">若要禁止显示项目范围内的警告，请考虑执行以下操作：</span><span class="sxs-lookup"><span data-stu-id="20044-206">To suppress a warning project wide, consider doing:</span></span>

```xml
<PropertyGroup>
    <PackageVersion>5.0.0</PackageVersion>
    <NoWarn>$(NoWarn);NU5104</NoWarn>
</PropertyGroup>
<ItemGroup>
    <PackageReference Include="Contoso.Package" Version="1.0.0-beta.1"/>
</ItemGroup>
```

<span data-ttu-id="20044-207">有时，警告仅适用于图中的特定包。</span><span class="sxs-lookup"><span data-stu-id="20044-207">Sometimes warnings apply only to a certain package in the graph.</span></span> <span data-ttu-id="20044-208">通过对 PackageReference 项目添加 `NoWarn`，我们可以有更多地选择来禁止显示该警告。</span><span class="sxs-lookup"><span data-stu-id="20044-208">We can choose to suppress that warning more selectively by adding a `NoWarn` on the PackageReference item.</span></span> 

```xml
<PropertyGroup>
    <PackageVersion>5.0.0</PackageVersion>
</PropertyGroup>
<ItemGroup>
    <PackageReference Include="Contoso.Package" Version="1.0.0-beta.1" NoWarn="NU1603" />
</ItemGroup>
```

#### <a name="suppressing-nuget-package-warnings-in-visual-studio"></a><span data-ttu-id="20044-209">在 Visual Studio 中禁止显示 NuGet 包警告</span><span class="sxs-lookup"><span data-stu-id="20044-209">Suppressing NuGet package warnings in Visual Studio</span></span>

<span data-ttu-id="20044-210">在 Visual Studio 中，还可以通过 IDE [禁止显示警告](/visualstudio/ide/how-to-suppress-compiler-warnings#suppress-warnings-for-nuget-packages
)。</span><span class="sxs-lookup"><span data-stu-id="20044-210">When in Visual Studio, you can also [suppress warnings](/visualstudio/ide/how-to-suppress-compiler-warnings#suppress-warnings-for-nuget-packages
) through the IDE.</span></span>

## <a name="locking-dependencies"></a><span data-ttu-id="20044-211">锁定依赖项</span><span class="sxs-lookup"><span data-stu-id="20044-211">Locking dependencies</span></span>

<span data-ttu-id="20044-212">NuGet 4.9 或更高版本以及 Visual Studio 2017 15.9 或更高版本随附此功能。</span><span class="sxs-lookup"><span data-stu-id="20044-212">*This feature is available with NuGet **4.9** or above and with Visual Studio 2017 **15.9** or above.*</span></span>

<span data-ttu-id="20044-213">对 NuGet 还原的输入是项目文件中的一组包引用（顶级或直接依赖项），而输出则是所有包依赖项的完整闭包，其中包括可传递依赖项。</span><span class="sxs-lookup"><span data-stu-id="20044-213">Input to NuGet restore is a set of Package References from the project file (top-level or direct dependencies) and the output is a full closure of all the package dependencies including transitive dependencies.</span></span> <span data-ttu-id="20044-214">如果输入 PackageReference 列表尚未更改，则 NuGet 尝试始终生成相同的完整闭包。</span><span class="sxs-lookup"><span data-stu-id="20044-214">NuGet tries to always produce the same full closure of package dependencies if the input PackageReference list has not changed.</span></span> <span data-ttu-id="20044-215">但是，在某些情况下，它无法执行此操作。</span><span class="sxs-lookup"><span data-stu-id="20044-215">However, there are some scenarios where it is unable to do so.</span></span> <span data-ttu-id="20044-216">例如：</span><span class="sxs-lookup"><span data-stu-id="20044-216">For example:</span></span>

* <span data-ttu-id="20044-217">在使用 `<PackageReference Include="My.Sample.Lib" Version="4.*"/>` 等浮动版本时。</span><span class="sxs-lookup"><span data-stu-id="20044-217">When you use floating versions like `<PackageReference Include="My.Sample.Lib" Version="4.*"/>`.</span></span> <span data-ttu-id="20044-218">尽管在此处这样做的目的是浮动到每个包还原的最新版本，但是在某些情况下，用户需要在一个显式动作后，将图形锁定到某个最新版本并浮动到更高版本（如果有可用的更高版本）。</span><span class="sxs-lookup"><span data-stu-id="20044-218">While the intention here is to float to the latest version on every restore of packages, there are scenarios where users require the graph to be locked to a certain latest version and float to a later version, if available, upon an explicit gesture.</span></span>
* <span data-ttu-id="20044-219">匹配 PackageReference 版本要求的较新版本已发布。</span><span class="sxs-lookup"><span data-stu-id="20044-219">A newer version of the package matching PackageReference version requirements is published.</span></span> <span data-ttu-id="20044-220">例如</span><span class="sxs-lookup"><span data-stu-id="20044-220">E.g.</span></span> 

  * <span data-ttu-id="20044-221">第 1 天：如果指定了 `<PackageReference Include="My.Sample.Lib" Version="4.0.0"/>`，但在 NuGet 存储库上可用的版本为 4.1.0、4.2.0 和 4.3.0。</span><span class="sxs-lookup"><span data-stu-id="20044-221">Day 1: if you specified `<PackageReference Include="My.Sample.Lib" Version="4.0.0"/>` but the versions available on the NuGet repositories were 4.1.0, 4.2.0 and 4.3.0.</span></span> <span data-ttu-id="20044-222">在这种情况下，NuGet 将解析为 4.1.0（最接近的最低版本）</span><span class="sxs-lookup"><span data-stu-id="20044-222">In this case, NuGet would have resolved to  4.1.0 (nearest minimum version)</span></span>

  * <span data-ttu-id="20044-223">第 2 天：版本 4.0.0 发布。</span><span class="sxs-lookup"><span data-stu-id="20044-223">Day 2: Version 4.0.0 gets published.</span></span> <span data-ttu-id="20044-224">NuGet 现在将查找完全匹配并开始解析到 4.0.0</span><span class="sxs-lookup"><span data-stu-id="20044-224">NuGet will now find the exact match and start resolving to 4.0.0</span></span>

* <span data-ttu-id="20044-225">给定包版本将从存储库中删除。</span><span class="sxs-lookup"><span data-stu-id="20044-225">A given package version is removed from the repository.</span></span> <span data-ttu-id="20044-226">尽管 nuget.org 不允许包删除，但并非所有包存储库都具有此约束。</span><span class="sxs-lookup"><span data-stu-id="20044-226">Though nuget.org does not allow package deletions, not all package repositories have this constraints.</span></span> <span data-ttu-id="20044-227">这导致 NuGet 在无法解析到已删除的版本时查找最佳匹配项。</span><span class="sxs-lookup"><span data-stu-id="20044-227">This results in NuGet finding the best match when it cannot resolve to the deleted version.</span></span>

### <a name="enabling-lock-file"></a><span data-ttu-id="20044-228">启用锁定文件</span><span class="sxs-lookup"><span data-stu-id="20044-228">Enabling lock file</span></span>

<span data-ttu-id="20044-229">为了保留包依赖项的完整闭包，可以选择锁定文件功能，方法是通过设置项目的 MSBuild 属性 `RestorePackagesWithLockFile`：</span><span class="sxs-lookup"><span data-stu-id="20044-229">In order to persist the full closure of package dependencies you can opt-in to the lock file feature by setting the MSBuild property `RestorePackagesWithLockFile` for your project:</span></span>

```xml
<PropertyGroup>
    <!--- ... -->
    <RestorePackagesWithLockFile>true</RestorePackagesWithLockFile>
    <!--- ... -->
</PropertyGroup>    
```

<span data-ttu-id="20044-230">如果设置此属性，NuGet 还原将生成一个锁定文件 - 项目根目录中列出所有包依赖项的 `packages.lock.json` 文件。</span><span class="sxs-lookup"><span data-stu-id="20044-230">If this property is set, NuGet restore will generate a lock file - `packages.lock.json` file at the project root directory that lists all the package dependencies.</span></span> 

> [!Note]
> <span data-ttu-id="20044-231">一旦项目在其根目录中具有 `packages.lock.json` 文件，则即使在未设置属性 `RestorePackagesWithLockFile` 时，锁定文件仍将始终与还原配合使用。</span><span class="sxs-lookup"><span data-stu-id="20044-231">Once a project has `packages.lock.json` file in its root directory, the lock file is always used with restore even if the property `RestorePackagesWithLockFile` is not set.</span></span> <span data-ttu-id="20044-232">因此，选择加入此功能的另一个方法是在项目的根目录中创建一个虚拟空白 `packages.lock.json` 文件。</span><span class="sxs-lookup"><span data-stu-id="20044-232">So another way to opt-in to this feature is to create a dummy blank `packages.lock.json` file in the project's root directory.</span></span>

### <a name="restore-behavior-with-lock-file"></a><span data-ttu-id="20044-233">锁定文件的 `restore` 行为</span><span class="sxs-lookup"><span data-stu-id="20044-233">`restore` behavior with lock file</span></span>
<span data-ttu-id="20044-234">如果项目存在锁定文件，则 NuGet 使用此锁定文件来运行 `restore`。</span><span class="sxs-lookup"><span data-stu-id="20044-234">If a lock file is present for project, NuGet uses this lock file to run `restore`.</span></span> <span data-ttu-id="20044-235">NuGet 将执行一次快速检查，以确定在包依赖项中是否存在项目文件（或相关项目的文件）中所提及的任何更改，如果没有任何更改，则它将仅还原锁定文件中提及的包。</span><span class="sxs-lookup"><span data-stu-id="20044-235">NuGet does a quick check to see if there were any changes in the package dependencies as mentioned in the project file (or dependent projects' files) and if there were no changes it just restores the packages mentioned in the lock file.</span></span> <span data-ttu-id="20044-236">不会对包依赖项进行重新评估。</span><span class="sxs-lookup"><span data-stu-id="20044-236">There is no re-evaluation of package dependencies.</span></span>

<span data-ttu-id="20044-237">如果 NuGet 检测到在定义的依赖项中存在一个或多个项目文件中提及的更改，它会重新评估包关系图，并将锁定文件更新为反映项目的新闭包。</span><span class="sxs-lookup"><span data-stu-id="20044-237">If NuGet detects a change in the defined dependencies as mentioned in the project file(s), it re-evaluates the package graph and updates the lock file to reflect the new package closure for the project.</span></span>

<span data-ttu-id="20044-238">对于 CI/CD 和其他方案（不想匆忙更改包依赖项），为此可以将 `lockedmode` 设置为 `true`：</span><span class="sxs-lookup"><span data-stu-id="20044-238">For CI/CD and other scenarios, where you would not want to change the package dependencies on the fly, you can do so by setting the `lockedmode` to `true`:</span></span>

<span data-ttu-id="20044-239">对于 dotnet.exe，请运行：</span><span class="sxs-lookup"><span data-stu-id="20044-239">For dotnet.exe, run:</span></span>

```
> dotnet.exe restore --locked-mode
```

<span data-ttu-id="20044-240">对于 msbuild.exe，请运行：</span><span class="sxs-lookup"><span data-stu-id="20044-240">For msbuild.exe, run:</span></span>

```
> msbuild.exe -t:restore -p:RestoreLockedMode=true
```

<span data-ttu-id="20044-241">此外，还可以在项目文件中设置此条件 MSBuild 属性：</span><span class="sxs-lookup"><span data-stu-id="20044-241">You may also set this conditional MSBuild property in your project file:</span></span>

```xml
<PropertyGroup>
    <!--- ... -->
    <RestoreLockedMode>true</RestoreLockedMode>
    <!--- ... -->
</PropertyGroup> 
```

<span data-ttu-id="20044-242">如果锁定模式为 `true`，则还原将还原锁定文件中列出的完全匹配的包，或者，如果在锁定文件创建后为项目更新了定义的包依赖项，则还原将失败。</span><span class="sxs-lookup"><span data-stu-id="20044-242">If locked mode is `true`, restore will either restore the exact packages as listed in the lock file or fail if you updated the defined package dependencies for the project after lock file was created.</span></span>

### <a name="make-lock-file-part-of-your-source-repository"></a><span data-ttu-id="20044-243">使锁定文件作为源存储库的一部分</span><span class="sxs-lookup"><span data-stu-id="20044-243">Make lock file part of your source repository</span></span>
<span data-ttu-id="20044-244">若要生成应用程序，且可执行文件和相关项目位于依赖关系链的开头，请将锁定文件签入源代码存储库，以便 NuGet 能够在还原期间使用它。</span><span class="sxs-lookup"><span data-stu-id="20044-244">If you are building an application, an executable and the project in question is at the start of the dependency chain then do check in the lock file to the source code repository so that NuGet can make use of it during restore.</span></span>

<span data-ttu-id="20044-245">但是，如果你的项目是不交付的库项目或其他项目依赖的常用代码项目，则不应  将锁定文件作为源代码的一部分签入。</span><span class="sxs-lookup"><span data-stu-id="20044-245">However, if your project is a library project that you do not ship or a common code project on which other projects depend upon, you **should not** check in the lock file as part of your source code.</span></span> <span data-ttu-id="20044-246">保留锁定文件没有任何坏处，但在依赖于此常用代码项目的项目还原/生成期间，锁定文件中列出的常用代码项目的锁定的包依赖项可能无法使用。</span><span class="sxs-lookup"><span data-stu-id="20044-246">There is no harm in keeping the lock file but the locked package dependencies for the common code project may not be used, as listed in the lock file, during the restore/build of a project that depends on this common-code project.</span></span>

<span data-ttu-id="20044-247">例如</span><span class="sxs-lookup"><span data-stu-id="20044-247">Eg.</span></span>

```
ProjectA
  |------> PackageX 2.0.0
  |------> ProjectB
             |------>PackageX 1.0.0
```

<span data-ttu-id="20044-248">如果 `ProjectA` 在 `PackageX` 版本 `2.0.0` 上具有依赖项并引用依赖于 `PackageX` 版本 `1.0.0` 的 `ProjectB`，则 `ProjectB` 的锁定文件将列出 `PackageX` 版本 `1.0.0` 的依赖项。</span><span class="sxs-lookup"><span data-stu-id="20044-248">If `ProjectA` has a dependency on a `PackageX` version `2.0.0` and also references `ProjectB` that depends on `PackageX` version `1.0.0`, then the lock file for `ProjectB` will list a dependency on `PackageX` version `1.0.0`.</span></span> <span data-ttu-id="20044-249">但是，当生成 `ProjectA` 时，其锁定文件将包含 `PackageX` 锁定文件中列出的 **版本 `2.0.0`（而不是**）上的依赖项  `1.0.0``ProjectB`。</span><span class="sxs-lookup"><span data-stu-id="20044-249">However, when `ProjectA` is built, its lock file will contain a dependency on `PackageX` version **`2.0.0`** and **not** `1.0.0` as listed in the lock file for `ProjectB`.</span></span> <span data-ttu-id="20044-250">因此，常用代码项目的锁定文件对依赖于它的项目进行解析的包几乎没有控制。</span><span class="sxs-lookup"><span data-stu-id="20044-250">Thus, the lock file of a common code project has little say over the packages resolved for projects that depend on it.</span></span>

### <a name="lock-file-extensibility"></a><span data-ttu-id="20044-251">锁定文件可扩展性</span><span class="sxs-lookup"><span data-stu-id="20044-251">Lock file extensibility</span></span>

<span data-ttu-id="20044-252">可以使用以下所述的锁定文件控制各种还原行为：</span><span class="sxs-lookup"><span data-stu-id="20044-252">You can control various behaviors of restore with lock file as described below:</span></span>

| <span data-ttu-id="20044-253">NuGet.exe 选项</span><span class="sxs-lookup"><span data-stu-id="20044-253">NuGet.exe option</span></span> | <span data-ttu-id="20044-254">dotnet 选项</span><span class="sxs-lookup"><span data-stu-id="20044-254">dotnet option</span></span> | <span data-ttu-id="20044-255">MSBuild 等效选项</span><span class="sxs-lookup"><span data-stu-id="20044-255">MSBuild equivalent option</span></span> | <span data-ttu-id="20044-256">说明</span><span class="sxs-lookup"><span data-stu-id="20044-256">Description</span></span> |
|:--- |:--- |:--- |:--- |
| `-UseLockFile` |`--use-lock-file` | <span data-ttu-id="20044-257">RestorePackagesWithLockFile</span><span class="sxs-lookup"><span data-stu-id="20044-257">RestorePackagesWithLockFile</span></span> | <span data-ttu-id="20044-258">选择使用锁定文件。</span><span class="sxs-lookup"><span data-stu-id="20044-258">Opts into the usage of a lock file.</span></span> |
| `-LockedMode` | `--locked-mode` | <span data-ttu-id="20044-259">RestoreLockedMode</span><span class="sxs-lookup"><span data-stu-id="20044-259">RestoreLockedMode</span></span> | <span data-ttu-id="20044-260">为还原启用锁定模式。</span><span class="sxs-lookup"><span data-stu-id="20044-260">Enables locked mode for restore.</span></span> <span data-ttu-id="20044-261">这对于要获取可重复生成的 CI/CD 方案非常有用。</span><span class="sxs-lookup"><span data-stu-id="20044-261">This is useful in CI/CD scenarios where you want repeatable builds.</span></span>|   
| `-ForceEvaluate` | `--force-evaluate` | <span data-ttu-id="20044-262">RestoreForceEvaluate</span><span class="sxs-lookup"><span data-stu-id="20044-262">RestoreForceEvaluate</span></span> | <span data-ttu-id="20044-263">对于在项目中定义了浮动版本的包，此选项也非常有用。</span><span class="sxs-lookup"><span data-stu-id="20044-263">This option is useful with packages with floating version defined in the project.</span></span> <span data-ttu-id="20044-264">默认情况下，NuGet 还原不会在每次还原时自动更新包版本，除非使用此选项运行还原。</span><span class="sxs-lookup"><span data-stu-id="20044-264">By default, NuGet restore will not update the package version automatically upon each restore unless you run restore with this option.</span></span> |
| `-LockFilePath` | `--lock-file-path` | <span data-ttu-id="20044-265">NuGetLockFilePath</span><span class="sxs-lookup"><span data-stu-id="20044-265">NuGetLockFilePath</span></span> | <span data-ttu-id="20044-266">为项目定义自定义锁定文件位置。</span><span class="sxs-lookup"><span data-stu-id="20044-266">Defines a custom lock file location for a project.</span></span> <span data-ttu-id="20044-267">默认情况下，NuGet 支持根目录中的 `packages.lock.json`。</span><span class="sxs-lookup"><span data-stu-id="20044-267">By default, NuGet supports `packages.lock.json` at the root directory.</span></span> <span data-ttu-id="20044-268">如果在同一目录中具有多个项目，则 NuGet 支持特定于项目的锁定文件 `packages.<project_name>.lock.json`</span><span class="sxs-lookup"><span data-stu-id="20044-268">If you have multiple projects in the same directory, NuGet supports project specific lock file `packages.<project_name>.lock.json`</span></span> |
