---
title: "作为 MSBuild 目标的 NuGet 包和还原 | Microsoft Docs"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 4/3/2017
ms.topic: article
ms.prod: nuget
ms.technology: 
ms.assetid: 86f7e724-2509-4d7d-aa8d-4a3fb913ded6
description: "NuGet 包和还原可作为 MSBuild 目标直接用于 NuGet 4.0+。"
keywords: "NuGet 和 MSBuild, NuGet 包目标, NuGet 还原目标"
ms.reviewer: karann-msft
ms.openlocfilehash: def01380e5bc3bf878e72dd437f52cd033641ca5
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/14/2017
---
# <a name="nuget-pack-and-restore-as-msbuild-targets"></a><span data-ttu-id="09969-104">作为 MSBuild 目标的 NuGet 包和还原</span><span class="sxs-lookup"><span data-stu-id="09969-104">NuGet pack and restore as MSBuild targets</span></span>

<span data-ttu-id="09969-105">NuGet 4.0+</span><span class="sxs-lookup"><span data-stu-id="09969-105">*NuGet 4.0+*</span></span>

<span data-ttu-id="09969-106">NuGet 4.0 + 可直接用于 `.csproj` 文件中的信息，无需单独的 `.nuspec` 或 `project.json` 文件。</span><span class="sxs-lookup"><span data-stu-id="09969-106">NuGet 4.0+ can work directly with the information in a `.csproj` file without requiring a separate `.nuspec` or `project.json` file.</span></span> <span data-ttu-id="09969-107">以前存储在这些配置文件中的所有元数据可改为直接存储在 `.csproj` 文件中，如下所述。</span><span class="sxs-lookup"><span data-stu-id="09969-107">All the metadata that was previously stored in those configuration files can be instead stored in the `.csproj` file directly, as described here.</span></span>

<span data-ttu-id="09969-108">如下所述，对于 MSBuild 15.1+，NuGet 还是具有 `pack` 目标和 `restore` 目标的一等 MSBuild 公民。</span><span class="sxs-lookup"><span data-stu-id="09969-108">With MSBuild 15.1+, NuGet is also a first-class MSBuild citizen with the `pack` and `restore` targets as described below.</span></span> <span data-ttu-id="09969-109">借助这些目标，你可以像使用任何其他 MSBuild 任务或目标一样使用 NuGet。</span><span class="sxs-lookup"><span data-stu-id="09969-109">These targets allow you to work with NuGet as you would with any other MSBuild task or target.</span></span> <span data-ttu-id="09969-110">（对于 Nuget 3.x 及更早版本，通过 NuGet CLI 使用 [pack](../tools/cli-ref-pack.md) 和 [restore](../tools/cli-ref-restore.md) 命令。）</span><span class="sxs-lookup"><span data-stu-id="09969-110">(For NuGet 3.x and earlier, you use the [pack](../tools/cli-ref-pack.md) and [restore](../tools/cli-ref-restore.md) commands through the NuGet CLI instead.)</span></span>

<span data-ttu-id="09969-111">在本主题中：</span><span class="sxs-lookup"><span data-stu-id="09969-111">In this topic:</span></span>

- [<span data-ttu-id="09969-112">目标生成顺序</span><span class="sxs-lookup"><span data-stu-id="09969-112">Target build order</span></span>](#target-build-order)
- [<span data-ttu-id="09969-113">包目标</span><span class="sxs-lookup"><span data-stu-id="09969-113">pack target</span></span>](#pack-target)
- [<span data-ttu-id="09969-114">包方案</span><span class="sxs-lookup"><span data-stu-id="09969-114">pack scenarios</span></span>](#pack-scenarios)
- [<span data-ttu-id="09969-115">还原目标</span><span class="sxs-lookup"><span data-stu-id="09969-115">restore target</span></span>](#restore-target)
- [<span data-ttu-id="09969-116">PackageTargetFallback</span><span class="sxs-lookup"><span data-stu-id="09969-116">PackageTargetFallback</span></span>](#packagetargetfallback)

## <a name="target-build-order"></a><span data-ttu-id="09969-117">目标生成顺序</span><span class="sxs-lookup"><span data-stu-id="09969-117">Target build order</span></span>

<span data-ttu-id="09969-118">由于 `pack` 和 `restore` 为 MSBuild 目标，因此可以访问它们以增强工作流。</span><span class="sxs-lookup"><span data-stu-id="09969-118">Because `pack` and `restore` are  MSBuild targets, you can access them to enhance your workflow.</span></span> <span data-ttu-id="09969-119">例如，假设希望在打包后将包复制到网络共享。</span><span class="sxs-lookup"><span data-stu-id="09969-119">For example, let’s say you want to copy your package to a network share after packing it.</span></span> <span data-ttu-id="09969-120">此操作可通过向项目文件中添加以下内容来完成：</span><span class="sxs-lookup"><span data-stu-id="09969-120">You can do that by adding the following in your project file:</span></span>

```xml
<Target Name="CopyPackage" AfterTargets="Pack">
    <Copy
        SourceFiles="$(OutputPath)..\$(PackageId).$(PackageVersion).nupkg"
        DestinationFolder="\\myshare\packageshare\"
        />
</Target>
```

<span data-ttu-id="09969-121">同样，你可以编写 MSBuild 任务、编写自己的目标并使用 MSBuild 任务中的 NuGet 属性。</span><span class="sxs-lookup"><span data-stu-id="09969-121">Similarly, you can write an MSBuild task, write your own target and consume NuGet properties in the MSBuild task.</span></span>

## <a name="pack-target"></a><span data-ttu-id="09969-122">包目标</span><span class="sxs-lookup"><span data-stu-id="09969-122">pack target</span></span>

<span data-ttu-id="09969-123">如果使用包目标，即 `msbuild /t:pack`，MSBuild 会从 `.csproj` 文件（而不是 `project.json` 或 `.nuspec` 文件）描述其输入。</span><span class="sxs-lookup"><span data-stu-id="09969-123">When using the pack target, that is, `msbuild /t:pack`, MSBuild draws its inputs from the `.csproj` file rather than `project.json` or `.nuspec` files.</span></span> <span data-ttu-id="09969-124">下表描述了可以添加到 `.csproj` 文件第一个 `<PropertyGroup>` 节点中的 MSBuild 属性。</span><span class="sxs-lookup"><span data-stu-id="09969-124">The table below describes the MSBuild properties that can be added to a `.csproj` file within the first `<PropertyGroup>` node.</span></span> <span data-ttu-id="09969-125">在 Visual Studio 2017 及更高版本中，通过右键单击项目并选择上下文菜单上的“编辑 {project_name}”，即可轻松进行这些编辑。</span><span class="sxs-lookup"><span data-stu-id="09969-125">You can make these edits easily in Visual Studio 2017 and later by right-clicking the project and selecting **Edit {project_name}** on the context menu.</span></span> <span data-ttu-id="09969-126">为方便起见，表由 [`.nuspec` 文件](../schema/nuspec.md)中的等效属性组织。</span><span class="sxs-lookup"><span data-stu-id="09969-126">For convenience the table is organized by the equivalent property in a [`.nuspec` file](../schema/nuspec.md).</span></span>

<span data-ttu-id="09969-127">请注意，`.nuspec` 的 `Owners` 和 `Summary` 属性不受 MSBuild 支持。</span><span class="sxs-lookup"><span data-stu-id="09969-127">Note that the `Owners` and `Summary` properties from `.nuspec` are not supported with MSBuild.</span></span>


| <span data-ttu-id="09969-128">属性/NuSpec 值</span><span class="sxs-lookup"><span data-stu-id="09969-128">Attribute/NuSpec Value</span></span> | <span data-ttu-id="09969-129">MSBuild 属性</span><span class="sxs-lookup"><span data-stu-id="09969-129">MSBuild Property</span></span> | <span data-ttu-id="09969-130">默认</span><span class="sxs-lookup"><span data-stu-id="09969-130">Default</span></span> | <span data-ttu-id="09969-131">说明</span><span class="sxs-lookup"><span data-stu-id="09969-131">Notes</span></span> |
|--------|--------|--------|--------|
| <span data-ttu-id="09969-132">Id</span><span class="sxs-lookup"><span data-stu-id="09969-132">Id</span></span> | <span data-ttu-id="09969-133">PackageId</span><span class="sxs-lookup"><span data-stu-id="09969-133">PackageId</span></span> | <span data-ttu-id="09969-134">AssemblyName</span><span class="sxs-lookup"><span data-stu-id="09969-134">AssemblyName</span></span> | <span data-ttu-id="09969-135">MSBuild 的 $(AssemblyName)</span><span class="sxs-lookup"><span data-stu-id="09969-135">$(AssemblyName) from MSBuild</span></span> |
| <span data-ttu-id="09969-136">版本</span><span class="sxs-lookup"><span data-stu-id="09969-136">Version</span></span> | <span data-ttu-id="09969-137">PackageVersion</span><span class="sxs-lookup"><span data-stu-id="09969-137">PackageVersion</span></span> | <span data-ttu-id="09969-138">版本</span><span class="sxs-lookup"><span data-stu-id="09969-138">Version</span></span> | <span data-ttu-id="09969-139">这与 SemVer 兼容，例如，“1.0.0”、“1.0.0-beta”或“1.0.0-beta-00345”</span><span class="sxs-lookup"><span data-stu-id="09969-139">This is semver compatible, for example “1.0.0”, “1.0.0-beta”, or “1.0.0-beta-00345”</span></span> |
| <span data-ttu-id="09969-140">VersionPrefix</span><span class="sxs-lookup"><span data-stu-id="09969-140">VersionPrefix</span></span> | <span data-ttu-id="09969-141">PackageVersionPrefix</span><span class="sxs-lookup"><span data-stu-id="09969-141">PackageVersionPrefix</span></span> | <span data-ttu-id="09969-142">空</span><span class="sxs-lookup"><span data-stu-id="09969-142">empty</span></span> | <span data-ttu-id="09969-143">设置 PackageVersion 将覆盖 PackageVersionPrefix</span><span class="sxs-lookup"><span data-stu-id="09969-143">Setting PackageVersion will overwrite PackageVersionPrefix</span></span> |
| <span data-ttu-id="09969-144">VersionSuffix</span><span class="sxs-lookup"><span data-stu-id="09969-144">VersionSuffix</span></span> | <span data-ttu-id="09969-145">PackageVersionSuffix</span><span class="sxs-lookup"><span data-stu-id="09969-145">PackageVersionSuffix</span></span> | <span data-ttu-id="09969-146">空</span><span class="sxs-lookup"><span data-stu-id="09969-146">empty</span></span> | <span data-ttu-id="09969-147">MSBuild 的 $(VersionSuffix)。</span><span class="sxs-lookup"><span data-stu-id="09969-147">$(VersionSuffix) from MSBuild.</span></span> <span data-ttu-id="09969-148">设置 PackageVersion 将覆盖 PackageVersionSuffix</span><span class="sxs-lookup"><span data-stu-id="09969-148">Setting PackageVersion will overwrite PackageVersionSuffix</span></span> | 
| <span data-ttu-id="09969-149">作者</span><span class="sxs-lookup"><span data-stu-id="09969-149">Authors</span></span> | <span data-ttu-id="09969-150">作者</span><span class="sxs-lookup"><span data-stu-id="09969-150">Authors</span></span> | <span data-ttu-id="09969-151">当前用户的用户名</span><span class="sxs-lookup"><span data-stu-id="09969-151">Username of the current user</span></span> | |
| <span data-ttu-id="09969-152">Owners</span><span class="sxs-lookup"><span data-stu-id="09969-152">Owners</span></span> | <span data-ttu-id="09969-153">不可用</span><span class="sxs-lookup"><span data-stu-id="09969-153">N/A</span></span> | <span data-ttu-id="09969-154">NuSpec 中不存在</span><span class="sxs-lookup"><span data-stu-id="09969-154">Not present in NuSpec</span></span> | |
| <span data-ttu-id="09969-155">标题</span><span class="sxs-lookup"><span data-stu-id="09969-155">Title</span></span> | <span data-ttu-id="09969-156">标题</span><span class="sxs-lookup"><span data-stu-id="09969-156">Title</span></span> | <span data-ttu-id="09969-157">PackageId</span><span class="sxs-lookup"><span data-stu-id="09969-157">The PackageId</span></span>| |
| <span data-ttu-id="09969-158">描述</span><span class="sxs-lookup"><span data-stu-id="09969-158">Description</span></span> | <span data-ttu-id="09969-159">描述</span><span class="sxs-lookup"><span data-stu-id="09969-159">Description</span></span> | <span data-ttu-id="09969-160">“包描述”</span><span class="sxs-lookup"><span data-stu-id="09969-160">"Package Description"</span></span> | |
| <span data-ttu-id="09969-161">Copyright</span><span class="sxs-lookup"><span data-stu-id="09969-161">Copyright</span></span> | <span data-ttu-id="09969-162">Copyright</span><span class="sxs-lookup"><span data-stu-id="09969-162">Copyright</span></span> | <span data-ttu-id="09969-163">空</span><span class="sxs-lookup"><span data-stu-id="09969-163">empty</span></span> | |
| <span data-ttu-id="09969-164">requireLicenseAcceptance</span><span class="sxs-lookup"><span data-stu-id="09969-164">RequireLicenseAcceptance</span></span> | <span data-ttu-id="09969-165">PackageRequireLicenseAcceptance</span><span class="sxs-lookup"><span data-stu-id="09969-165">PackageRequireLicenseAcceptance</span></span> | <span data-ttu-id="09969-166">false</span><span class="sxs-lookup"><span data-stu-id="09969-166">false</span></span> | |
| <span data-ttu-id="09969-167">LicenseUrl</span><span class="sxs-lookup"><span data-stu-id="09969-167">LicenseUrl</span></span> | <span data-ttu-id="09969-168">PackageLicenseUrl</span><span class="sxs-lookup"><span data-stu-id="09969-168">PackageLicenseUrl</span></span> | <span data-ttu-id="09969-169">空</span><span class="sxs-lookup"><span data-stu-id="09969-169">empty</span></span> | |
| <span data-ttu-id="09969-170">ProjectUrl</span><span class="sxs-lookup"><span data-stu-id="09969-170">ProjectUrl</span></span> | <span data-ttu-id="09969-171">PackageProjectUrl</span><span class="sxs-lookup"><span data-stu-id="09969-171">PackageProjectUrl</span></span> | <span data-ttu-id="09969-172">空</span><span class="sxs-lookup"><span data-stu-id="09969-172">empty</span></span> | |
| <span data-ttu-id="09969-173">IconUrl</span><span class="sxs-lookup"><span data-stu-id="09969-173">IconUrl</span></span> | <span data-ttu-id="09969-174">PackageIconUrl</span><span class="sxs-lookup"><span data-stu-id="09969-174">PackageIconUrl</span></span> | <span data-ttu-id="09969-175">空</span><span class="sxs-lookup"><span data-stu-id="09969-175">empty</span></span> | |
| <span data-ttu-id="09969-176">Tags</span><span class="sxs-lookup"><span data-stu-id="09969-176">Tags</span></span> | <span data-ttu-id="09969-177">PackageTags</span><span class="sxs-lookup"><span data-stu-id="09969-177">PackageTags</span></span> | <span data-ttu-id="09969-178">空</span><span class="sxs-lookup"><span data-stu-id="09969-178">empty</span></span> | <span data-ttu-id="09969-179">使用分号分隔标记。</span><span class="sxs-lookup"><span data-stu-id="09969-179">Tags are semi-colon delimited.</span></span> |
| <span data-ttu-id="09969-180">ReleaseNotes</span><span class="sxs-lookup"><span data-stu-id="09969-180">ReleaseNotes</span></span> | <span data-ttu-id="09969-181">PackageReleaseNotes</span><span class="sxs-lookup"><span data-stu-id="09969-181">PackageReleaseNotes</span></span> | <span data-ttu-id="09969-182">空</span><span class="sxs-lookup"><span data-stu-id="09969-182">empty</span></span> | |
| <span data-ttu-id="09969-183">RepositoryUrl</span><span class="sxs-lookup"><span data-stu-id="09969-183">RepositoryUrl</span></span> | <span data-ttu-id="09969-184">RepositoryUrl</span><span class="sxs-lookup"><span data-stu-id="09969-184">RepositoryUrl</span></span> | <span data-ttu-id="09969-185">空</span><span class="sxs-lookup"><span data-stu-id="09969-185">empty</span></span> | |
| <span data-ttu-id="09969-186">RepositoryType</span><span class="sxs-lookup"><span data-stu-id="09969-186">RepositoryType</span></span> | <span data-ttu-id="09969-187">RepositoryType</span><span class="sxs-lookup"><span data-stu-id="09969-187">RepositoryType</span></span> | <span data-ttu-id="09969-188">空</span><span class="sxs-lookup"><span data-stu-id="09969-188">empty</span></span> | |
| <span data-ttu-id="09969-189">PackageType</span><span class="sxs-lookup"><span data-stu-id="09969-189">PackageType</span></span> | `<PackageType>DotNetCliTool, 1.0.0.0;Dependency, 2.0.0.0</PackageType>` | | |
| <span data-ttu-id="09969-190">摘要</span><span class="sxs-lookup"><span data-stu-id="09969-190">Summary</span></span> | <span data-ttu-id="09969-191">不支持</span><span class="sxs-lookup"><span data-stu-id="09969-191">Not supported</span></span> | | |


### <a name="pack-target-inputs"></a><span data-ttu-id="09969-192">包目标输入</span><span class="sxs-lookup"><span data-stu-id="09969-192">pack target inputs</span></span>

- <span data-ttu-id="09969-193">IsPackable</span><span class="sxs-lookup"><span data-stu-id="09969-193">IsPackable</span></span>
- <span data-ttu-id="09969-194">PackageVersion</span><span class="sxs-lookup"><span data-stu-id="09969-194">PackageVersion</span></span>
- <span data-ttu-id="09969-195">PackageId</span><span class="sxs-lookup"><span data-stu-id="09969-195">PackageId</span></span>
- <span data-ttu-id="09969-196">作者</span><span class="sxs-lookup"><span data-stu-id="09969-196">Authors</span></span>
- <span data-ttu-id="09969-197">描述</span><span class="sxs-lookup"><span data-stu-id="09969-197">Description</span></span>
- <span data-ttu-id="09969-198">Copyright</span><span class="sxs-lookup"><span data-stu-id="09969-198">Copyright</span></span>
- <span data-ttu-id="09969-199">PackageRequireLicenseAcceptance</span><span class="sxs-lookup"><span data-stu-id="09969-199">PackageRequireLicenseAcceptance</span></span>
- <span data-ttu-id="09969-200">DevelopmentDependency</span><span class="sxs-lookup"><span data-stu-id="09969-200">DevelopmentDependency</span></span>
- <span data-ttu-id="09969-201">PackageLicenseUrl</span><span class="sxs-lookup"><span data-stu-id="09969-201">PackageLicenseUrl</span></span>
- <span data-ttu-id="09969-202">PackageProjectUrl</span><span class="sxs-lookup"><span data-stu-id="09969-202">PackageProjectUrl</span></span>
- <span data-ttu-id="09969-203">PackageIconUrl</span><span class="sxs-lookup"><span data-stu-id="09969-203">PackageIconUrl</span></span>
- <span data-ttu-id="09969-204">PackageReleaseNotes</span><span class="sxs-lookup"><span data-stu-id="09969-204">PackageReleaseNotes</span></span>
- <span data-ttu-id="09969-205">PackageTags</span><span class="sxs-lookup"><span data-stu-id="09969-205">PackageTags</span></span>
- <span data-ttu-id="09969-206">PackageOutputPath</span><span class="sxs-lookup"><span data-stu-id="09969-206">PackageOutputPath</span></span>
- <span data-ttu-id="09969-207">IncludeSymbols</span><span class="sxs-lookup"><span data-stu-id="09969-207">IncludeSymbols</span></span>
- <span data-ttu-id="09969-208">IncludeSource</span><span class="sxs-lookup"><span data-stu-id="09969-208">IncludeSource</span></span>
- <span data-ttu-id="09969-209">PackageTypes</span><span class="sxs-lookup"><span data-stu-id="09969-209">PackageTypes</span></span>
- <span data-ttu-id="09969-210">IsTool</span><span class="sxs-lookup"><span data-stu-id="09969-210">IsTool</span></span>
- <span data-ttu-id="09969-211">RepositoryUrl</span><span class="sxs-lookup"><span data-stu-id="09969-211">RepositoryUrl</span></span>
- <span data-ttu-id="09969-212">RepositoryType</span><span class="sxs-lookup"><span data-stu-id="09969-212">RepositoryType</span></span>
- <span data-ttu-id="09969-213">NoPackageAnalysis</span><span class="sxs-lookup"><span data-stu-id="09969-213">NoPackageAnalysis</span></span>
- <span data-ttu-id="09969-214">MinClientVersion</span><span class="sxs-lookup"><span data-stu-id="09969-214">MinClientVersion</span></span>
- <span data-ttu-id="09969-215">IncludeBuildOutput</span><span class="sxs-lookup"><span data-stu-id="09969-215">IncludeBuildOutput</span></span>
- <span data-ttu-id="09969-216">IncludeContentInPack</span><span class="sxs-lookup"><span data-stu-id="09969-216">IncludeContentInPack</span></span>
- <span data-ttu-id="09969-217">BuildOutputTargetFolder</span><span class="sxs-lookup"><span data-stu-id="09969-217">BuildOutputTargetFolder</span></span>
- <span data-ttu-id="09969-218">ContentTargetFolders</span><span class="sxs-lookup"><span data-stu-id="09969-218">ContentTargetFolders</span></span>
- <span data-ttu-id="09969-219">NuspecFile</span><span class="sxs-lookup"><span data-stu-id="09969-219">NuspecFile</span></span>
- <span data-ttu-id="09969-220">NuspecBasePath</span><span class="sxs-lookup"><span data-stu-id="09969-220">NuspecBasePath</span></span>
- <span data-ttu-id="09969-221">NuspecProperties</span><span class="sxs-lookup"><span data-stu-id="09969-221">NuspecProperties</span></span>

## <a name="pack-scenarios"></a><span data-ttu-id="09969-222">包方案</span><span class="sxs-lookup"><span data-stu-id="09969-222">pack scenarios</span></span>

### <a name="packageiconurl"></a><span data-ttu-id="09969-223">PackageIconUrl</span><span class="sxs-lookup"><span data-stu-id="09969-223">PackageIconUrl</span></span>

<span data-ttu-id="09969-224">作为 [NuGet 问题 2582](https://github.com/NuGet/Home/issues/2582) 更改的一部分，`PackageIconUrl` 最终将更改为 `PackageIconUri` 并且可成为包括在生成包根目录下的图标文件的相对路径。</span><span class="sxs-lookup"><span data-stu-id="09969-224">As part of the change for [NuGet Issue 2582](https://github.com/NuGet/Home/issues/2582), `PackageIconUrl` will eventually be changed to `PackageIconUri` and can be relative path to a icon file which will included at the root of the resulting package.</span></span>

### <a name="output-assemblies"></a><span data-ttu-id="09969-225">输出程序集</span><span class="sxs-lookup"><span data-stu-id="09969-225">Output assemblies</span></span>

<span data-ttu-id="09969-226">`nuget pack` 会复制扩展名为 `.exe`、`.dll`、`.xml`、`.winmd`、`.json` 和 `.pri` 的输出文件。</span><span class="sxs-lookup"><span data-stu-id="09969-226">`nuget pack` copies output files with extensions `.exe`, `.dll`, `.xml`, `.winmd`, `.json`, and `.pri`.</span></span> <span data-ttu-id="09969-227">复制的输出文件取决于 MSBuild 从 `BuiltOutputProjectGroup` 目标提供的内容。</span><span class="sxs-lookup"><span data-stu-id="09969-227">The output files that are copied depend on what MSBuild provides from the `BuiltOutputProjectGroup` target.</span></span>

<span data-ttu-id="09969-228">在项目文件或命令行中，有两种 MSBuild 属性可用于控制输出程序集的位置：</span><span class="sxs-lookup"><span data-stu-id="09969-228">There are two MSBuild  properties that you can use in your project file or command line to control where output assemblies go:</span></span>

- <span data-ttu-id="09969-229">`IncludeBuildOutput`：确定包中是否应包括生成输出程序集的布尔值。</span><span class="sxs-lookup"><span data-stu-id="09969-229">`IncludeBuildOutput`: A boolean that determines whether the build output assemblies should be included in the package.</span></span>
- <span data-ttu-id="09969-230">`BuildOutputTargetFolder`：指定应放置输出程序集的文件夹。</span><span class="sxs-lookup"><span data-stu-id="09969-230">`BuildOutputTargetFolder`: Specifies the folder in which the output assemblies should be placed.</span></span> <span data-ttu-id="09969-231">输出程序集（和其他输出文件）会复制到各自的框架文件夹中。</span><span class="sxs-lookup"><span data-stu-id="09969-231">The output assemblies (and other output files) are copied into their respective framework folders.</span></span>

### <a name="package-references"></a><span data-ttu-id="09969-232">包引用</span><span class="sxs-lookup"><span data-stu-id="09969-232">Package references</span></span>

<span data-ttu-id="09969-233">请参阅[项目文件中的包引用](../consume-packages/package-references-in-project-files.md)</span><span class="sxs-lookup"><span data-stu-id="09969-233">See [Package References in Project Files](../consume-packages/package-references-in-project-files.md).</span></span>

### <a name="project-to-project-references"></a><span data-ttu-id="09969-234">项目到项目的引用</span><span class="sxs-lookup"><span data-stu-id="09969-234">Project to project references</span></span>

<span data-ttu-id="09969-235">默认情况下，项目到项目的引用被视为 nuget 包引用，例如：</span><span class="sxs-lookup"><span data-stu-id="09969-235">Project to project references are considered by default as nuget package references, for example:</span></span>

```xml
<ProjectReference Include="..\UwpLibrary2\UwpLibrary2.csproj"/>
```

<span data-ttu-id="09969-236">也可将以下元数据添加到项目引用：</span><span class="sxs-lookup"><span data-stu-id="09969-236">You can also add the following metadata to your project reference:</span></span>

```xml
<IncludeAssets>
<ExcludeAssets>
<PrivateAssets>
```

### <a name="including-content-in-a-package"></a><span data-ttu-id="09969-237">在包中添加内容</span><span class="sxs-lookup"><span data-stu-id="09969-237">Including content in a package</span></span>

<span data-ttu-id="09969-238">若要添加内容，请将额外的元数据添加到现有的 `<Content>` 项。</span><span class="sxs-lookup"><span data-stu-id="09969-238">To include content, add extra metadata to the existing `<Content>` item.</span></span> <span data-ttu-id="09969-239">默认情况下，类型“Content”的所有内容都包括在包中，除非使用以下条目替代：</span><span class="sxs-lookup"><span data-stu-id="09969-239">By default everything of type "Content" gets included in the package unless you override with entries like the following:</span></span>

 ```xml
    <Content Include="..\win7-x64\libuv.txt">
        <Pack>false</Pack>
    </Content>
 ```

<span data-ttu-id="09969-240">默认情况下，所有内容都添加到包中 `content` 和 `contentFiles\any\<target_framework>` 文件夹根目录，并保留相对文件夹结构，除非指定包路径：</span><span class="sxs-lookup"><span data-stu-id="09969-240">By default, everything gets added to the root of the `content` and `contentFiles\any\<target_framework>` folder within a package and preserves the relative folder structure, unless you specify a package path:</span></span>

```xml
<Content Include="..\win7-x64\libuv.txt">        
    <Pack>true</Pack>
    <PackagePath>content\myfiles\</PackagePath>
</Content>
```

<span data-ttu-id="09969-241">如果仅希望将所有内容都复制到特定根文件夹（而不是 `content` 和 `contentFiles`），可使用 MSBuild 属性 `ContentTargetFolders`，其默认值为“content;contentFiles”，但可以设置为任何其他文件夹名称。</span><span class="sxs-lookup"><span data-stu-id="09969-241">If you want to copy all your content to only a specific root folder(s) (instead of `content` and `contentFiles` both), you can use the MSBuild property `ContentTargetFolders`, which defaults to "content;contentFiles" but can be set to any other folder names.</span></span> <span data-ttu-id="09969-242">请注意，基于 `buildAction`，仅在 `ContentTargetFolders` 中指定“contentFiles”会将文件置于 `contentFiles\any\<target_framework>` 或 `contentFiles\<language>\<target_framework>` 下。</span><span class="sxs-lookup"><span data-stu-id="09969-242">Note that just specifying "contentFiles" in `ContentTargetFolders` puts files under `contentFiles\any\<target_framework>` or `contentFiles\<language>\<target_framework>` based on `buildAction`.</span></span>

<span data-ttu-id="09969-243">`PackagePath` 可以是一组以分号分隔的目标路径。</span><span class="sxs-lookup"><span data-stu-id="09969-243">`PackagePath` can be a semicolon-delimited set of target paths.</span></span> <span data-ttu-id="09969-244">指定空的包路径会将文件添加到包的根目录。</span><span class="sxs-lookup"><span data-stu-id="09969-244">Specifying an empty package path would add the file to the root of the package.</span></span> <span data-ttu-id="09969-245">例如，以下操作会将 `libuv.txt` 添加到 `content\myfiles`、`content\samples` 和包的根目录：</span><span class="sxs-lookup"><span data-stu-id="09969-245">For example, the following adds `libuv.txt` to `content\myfiles`, `content\samples`, and the package root:</span></span>

```xml
<Content Include="..\win7-x64\libuv.txt">
    <Pack>true</Pack>
    <PackagePath>content\myfiles;content\sample;;</PackagePath>
</Content>
```

<span data-ttu-id="09969-246">另外还有 MSBuild 属性 `$(IncludeContentInPack)`，默认值为 `true`。</span><span class="sxs-lookup"><span data-stu-id="09969-246">There is also an MSBuild property `$(IncludeContentInPack)`, which defaults to `true`.</span></span> <span data-ttu-id="09969-247">如果在任何项目中将此值设置为 `false`，则该项目的内容不会包括在 nuget 包中。</span><span class="sxs-lookup"><span data-stu-id="09969-247">If this is set to `false` on any project, then the content from that project are not included in the nuget package.</span></span>

<span data-ttu-id="09969-248">其他可在任何上述项上设置的特定于包的元数据包括 ```<PackageCopyToOutput>``` 和 ```<PackageFlatten>```，后者在输出 nuspec 中的 ```contentFiles``` 条目上设置 ```CopyToOutput``` 和 ```Flatten``` 值。</span><span class="sxs-lookup"><span data-stu-id="09969-248">Other pack specific metadata that you can set on any of the above items includes ```<PackageCopyToOutput>``` and ```<PackageFlatten>``` which sets ```CopyToOutput``` and ```Flatten``` values on the ```contentFiles``` entry in the output nuspec.</span></span>


> [!Note]
> <span data-ttu-id="09969-249">除了“Content”项，`<Pack>` 和 `<PackagePath>` 元数据还可以在具有 Compile、EmbeddedResource、ApplicationDefinition、Page、Resource、SplashScreen、DesignData、DesignDataWithDesignTimeCreatableTypes、CodeAnalysisDictionary、AndroidAsset、AndroidResource、BundleResource 或 None 生成操作的文件上进行设置。</span><span class="sxs-lookup"><span data-stu-id="09969-249">Apart from Content items, the `<Pack>` and `<PackagePath>` metadata can also be set on files with a build action of Compile, EmbeddedResource, ApplicationDefinition, Page, Resource, SplashScreen, DesignData, DesignDataWithDesignTimeCreatableTypes, CodeAnalysisDictionary, AndroidAsset, AndroidResource, BundleResource or None.</span></span>
>
> <span data-ttu-id="09969-250">使用通配模式时，对于将包的文件名追加到包路径，包路径必须以文件夹分隔符结尾，否则包路径将被视为包括文件名的完整路径。</span><span class="sxs-lookup"><span data-stu-id="09969-250">For pack to append the filename to your package path when using globbing patterns, your package path must end with the folder separator character, otherwise the package path is treated as the full path including the file name.</span></span>

### <a name="includesymbols"></a><span data-ttu-id="09969-251">IncludeSymbols</span><span class="sxs-lookup"><span data-stu-id="09969-251">IncludeSymbols</span></span>

<span data-ttu-id="09969-252">使用 `MSBuild /t:pack /p:IncludeSymbols=true` 时，相应的 `.pdb` 文件将随其他输出文件（`.dll`、`.exe`、`.winmd`、`.xml`、`.json`、`.pri`）一起复制。</span><span class="sxs-lookup"><span data-stu-id="09969-252">When using `MSBuild /t:pack /p:IncludeSymbols=true`, the corresponding `.pdb` files are copied along with other output files (`.dll`, `.exe`, `.winmd`, `.xml`, `.json`, `.pri`).</span></span> <span data-ttu-id="09969-253">请注意，设置 `IncludeSymbols=true` 会创建常规包和符号包。</span><span class="sxs-lookup"><span data-stu-id="09969-253">Note that setting `IncludeSymbols=true` creates a regular package *and* a symbols package.</span></span>

### <a name="includesource"></a><span data-ttu-id="09969-254">IncludeSource</span><span class="sxs-lookup"><span data-stu-id="09969-254">IncludeSource</span></span>

<span data-ttu-id="09969-255">这与 `IncludeSymbols` 相同，但它还会连同 `.pdb` 文件复制源文件。</span><span class="sxs-lookup"><span data-stu-id="09969-255">This is the same as `IncludeSymbols`, except that it copies source files along with `.pdb` files as well.</span></span> <span data-ttu-id="09969-256">类型为 `Compile` 的所有文件都会复制到 `src\<ProjectName>\`，并保留生成包中的相对路径文件夹结构。</span><span class="sxs-lookup"><span data-stu-id="09969-256">All files of type `Compile` are copied over to `src\<ProjectName>\` preserving the relative path folder structure in the resulting package.</span></span> <span data-ttu-id="09969-257">对于将 `TreatAsPackageReference` 设置为 `false` 的任何 `ProjectReference` 的源文件也是如此。</span><span class="sxs-lookup"><span data-stu-id="09969-257">The same also happens for source files of any `ProjectReference` which has `TreatAsPackageReference` set to `false`.</span></span>

<span data-ttu-id="09969-258">如果类型为 Compile 的文件位于项目文件夹外，则仅将其添加到了 `src\<ProjectName>\`。</span><span class="sxs-lookup"><span data-stu-id="09969-258">If a file of type Compile, is outside the project folder, then it is just added to `src\<ProjectName>\`.</span></span>

### <a name="istool"></a><span data-ttu-id="09969-259">IsTool</span><span class="sxs-lookup"><span data-stu-id="09969-259">IsTool</span></span>

<span data-ttu-id="09969-260">使用 `MSBuild /t:pack /p:IsTool=true` 时，所有输出文件（如[输出程序集](#output-assemblies)方案中所指定）都被复制到 `tools` 文件夹，而不是 `lib` 文件夹。</span><span class="sxs-lookup"><span data-stu-id="09969-260">When using `MSBuild /t:pack /p:IsTool=true`, all output files, as specified in the [Output Assemblies](#output-assemblies) scenario, are copied to the `tools` folder instead of the `lib` folder.</span></span> <span data-ttu-id="09969-261">请注意，这不同于 `DotNetCliTool`，后者通过在 `.csproj` 文件中设置 `PackageType` 进行指定。</span><span class="sxs-lookup"><span data-stu-id="09969-261">Note that this is different from a `DotNetCliTool` which is specified by setting the `PackageType` in `.csproj` file.</span></span>

### <a name="packing-using-a-nuspec"></a><span data-ttu-id="09969-262">使用 .nuspec 打包</span><span class="sxs-lookup"><span data-stu-id="09969-262">Packing using a .nuspec</span></span>

<span data-ttu-id="09969-263">可以使用 `.nuspec` 文件打包项目，前提是拥有可导入 `NuGet.Build.Tasks.Pack.targets` 的项目文件，以便可执行包任务。</span><span class="sxs-lookup"><span data-stu-id="09969-263">You can use a `.nuspec` file to pack your project provided that you have a project file to import `NuGet.Build.Tasks.Pack.targets` so that the pack task can be executed.</span></span> <span data-ttu-id="09969-264">以下三个 MSBuild 属性与使用 `.nuspec` 的打包相关：</span><span class="sxs-lookup"><span data-stu-id="09969-264">The following three MSBuild properties are relevant to packing using a `.nuspec`:</span></span>

1. <span data-ttu-id="09969-265">`NuspecFile`：用于打包的 `.nuspec` 文件的相对或绝对路径。</span><span class="sxs-lookup"><span data-stu-id="09969-265">`NuspecFile`: relative or absolute path to the `.nuspec` file being used for packing.</span></span>
1. <span data-ttu-id="09969-266">`NuspecProperties`：键=值对的分号分隔列表。</span><span class="sxs-lookup"><span data-stu-id="09969-266">`NuspecProperties`: a semicolon-separated list of key=value pairs.</span></span> <span data-ttu-id="09969-267">由于 MSBuild 命令行分析工作的方式，必须指定多个属性，如下所示：`/p:NuspecProperties=\"key1=value1;key2=value2\"`。</span><span class="sxs-lookup"><span data-stu-id="09969-267">Due to the way MSBuild command-line parsing works, multiple properties must be specified as follows: `/p:NuspecProperties=\"key1=value1;key2=value2\"`.</span></span>  
1. <span data-ttu-id="09969-268">`NuspecBasePath`：`.nuspec` 文件的基路径。</span><span class="sxs-lookup"><span data-stu-id="09969-268">`NuspecBasePath`: Base path for the `.nuspec` file.</span></span>

<span data-ttu-id="09969-269">如果使用 `dotnet.exe` 打包项目，请使用类似于下面的命令：</span><span class="sxs-lookup"><span data-stu-id="09969-269">If using `dotnet.exe` to pack your project, use a command like the following:</span></span>

```
dotnet pack <path to .csproj file> /p:NuspecFile=<path to nuspec file> /p:NuspecProperties=<> /p:NuspecBasePath=<Base path> 
```

<span data-ttu-id="09969-270">如果使用 MSBuild 打包项目，请使用类似于下面的命令：</span><span class="sxs-lookup"><span data-stu-id="09969-270">If using MSBuild to pack your project, use a command like the following:</span></span>

```
msbuild /t:pack <path to .csproj file> /p:NuspecFile=<path to nuspec file> /p:NuspecProperties=<> /p:NuspecBasePath=<Base path> 
```

## <a name="restore-target"></a><span data-ttu-id="09969-271">还原目标</span><span class="sxs-lookup"><span data-stu-id="09969-271">restore target</span></span>

<span data-ttu-id="09969-272">`MSBuild /t:restore`（`nuget restore` 和 `dotnet restore` 与 .NET Core 项目一起使用）会还原项目文件中引用的包，如下所示：</span><span class="sxs-lookup"><span data-stu-id="09969-272">`MSBuild /t:restore` (which `nuget restore` and `dotnet restore` use with .NET Core projects), restores packages referenced in the project file as follows:</span></span>

1. <span data-ttu-id="09969-273">读取所有项目到项目的引用</span><span class="sxs-lookup"><span data-stu-id="09969-273">Read all project to project references</span></span>
1. <span data-ttu-id="09969-274">读取项目属性以查找中间文件夹和目标框架</span><span class="sxs-lookup"><span data-stu-id="09969-274">Read the project properties to find the intermediate folder and target frameworks</span></span>
1. <span data-ttu-id="09969-275">将 msbuild 数据传递到 NuGet.Build.Tasks.dll</span><span class="sxs-lookup"><span data-stu-id="09969-275">Pass msbuild data to NuGet.Build.Tasks.dll</span></span>
1. <span data-ttu-id="09969-276">运行还原</span><span class="sxs-lookup"><span data-stu-id="09969-276">Run restore</span></span>
1. <span data-ttu-id="09969-277">下载包</span><span class="sxs-lookup"><span data-stu-id="09969-277">Download packages</span></span>
1. <span data-ttu-id="09969-278">编写资产文件、目标和属性</span><span class="sxs-lookup"><span data-stu-id="09969-278">Write assets file, targets, and props</span></span>


### <a name="restore-properties"></a><span data-ttu-id="09969-279">还原属性</span><span class="sxs-lookup"><span data-stu-id="09969-279">Restore properties</span></span>

<span data-ttu-id="09969-280">其他的还原设置可能来自项目文件中的 MSBuild 属性。</span><span class="sxs-lookup"><span data-stu-id="09969-280">Additional restore settings may come from MSBuild properties in the project file.</span></span> <span data-ttu-id="09969-281">还可以从命令行使用 `/p:` 开关设置值（请参阅以下示例）。</span><span class="sxs-lookup"><span data-stu-id="09969-281">Values can also be set from the command line using the `/p:` switch (see Examples below).</span></span>

| <span data-ttu-id="09969-282">属性</span><span class="sxs-lookup"><span data-stu-id="09969-282">Property</span></span> | <span data-ttu-id="09969-283">描述</span><span class="sxs-lookup"><span data-stu-id="09969-283">Description</span></span> |
|--------|--------|
| <span data-ttu-id="09969-284">RestoreSources</span><span class="sxs-lookup"><span data-stu-id="09969-284">RestoreSources</span></span> | <span data-ttu-id="09969-285">以分号分隔的包源列表。</span><span class="sxs-lookup"><span data-stu-id="09969-285">Semicolon-delimited list of package sources.</span></span> |
| <span data-ttu-id="09969-286">RestorePackagesPath</span><span class="sxs-lookup"><span data-stu-id="09969-286">RestorePackagesPath</span></span> | <span data-ttu-id="09969-287">用户包文件夹路径。</span><span class="sxs-lookup"><span data-stu-id="09969-287">User packages folder path.</span></span> |
| <span data-ttu-id="09969-288">RestoreDisableParallel</span><span class="sxs-lookup"><span data-stu-id="09969-288">RestoreDisableParallel</span></span> | <span data-ttu-id="09969-289">将下载限制为一次一个。</span><span class="sxs-lookup"><span data-stu-id="09969-289">Limit downloads to one at a time.</span></span> |
| <span data-ttu-id="09969-290">RestoreConfigFile</span><span class="sxs-lookup"><span data-stu-id="09969-290">RestoreConfigFile</span></span> | <span data-ttu-id="09969-291">要应用的 `Nuget.Config` 文件的路径。</span><span class="sxs-lookup"><span data-stu-id="09969-291">Path to a `Nuget.Config` file to apply.</span></span> |
| <span data-ttu-id="09969-292">RestoreNoCache</span><span class="sxs-lookup"><span data-stu-id="09969-292">RestoreNoCache</span></span> | <span data-ttu-id="09969-293">如果为“true”，则避免使用 web 缓存。</span><span class="sxs-lookup"><span data-stu-id="09969-293">If true, avoids using the web cache.</span></span> |
| <span data-ttu-id="09969-294">RestoreIgnoreFailedSources</span><span class="sxs-lookup"><span data-stu-id="09969-294">RestoreIgnoreFailedSources</span></span> | <span data-ttu-id="09969-295">如果为“true”，则忽略失败或丢失的包源。</span><span class="sxs-lookup"><span data-stu-id="09969-295">If true, ignores failing or missing package sources.</span></span> |
| <span data-ttu-id="09969-296">RestoreTaskAssemblyFile</span><span class="sxs-lookup"><span data-stu-id="09969-296">RestoreTaskAssemblyFile</span></span> | <span data-ttu-id="09969-297">`NuGet.Build.Tasks.dll` 的路径。</span><span class="sxs-lookup"><span data-stu-id="09969-297">Path to `NuGet.Build.Tasks.dll`.</span></span> |
| <span data-ttu-id="09969-298">RestoreGraphProjectInput</span><span class="sxs-lookup"><span data-stu-id="09969-298">RestoreGraphProjectInput</span></span> | <span data-ttu-id="09969-299">要还原的以分号分隔的项目列表，其中应包含绝对路径。</span><span class="sxs-lookup"><span data-stu-id="09969-299">Semicolon-delimited list of projects to restore, which should contain absolute paths.</span></span> |
| <span data-ttu-id="09969-300">RestoreOutputPath</span><span class="sxs-lookup"><span data-stu-id="09969-300">RestoreOutputPath</span></span> | <span data-ttu-id="09969-301">输出文件夹，默认为 `obj` 文件夹。</span><span class="sxs-lookup"><span data-stu-id="09969-301">Output folder, defaulting to the `obj` folder.</span></span> |

<span data-ttu-id="09969-302">**示例**</span><span class="sxs-lookup"><span data-stu-id="09969-302">**Examples**</span></span>

<span data-ttu-id="09969-303">命令行：</span><span class="sxs-lookup"><span data-stu-id="09969-303">Command line:</span></span>

```
msbuild /t:restore /p:RestoreConfigFile=<path>
```

<span data-ttu-id="09969-304">项目文件：</span><span class="sxs-lookup"><span data-stu-id="09969-304">Project file:</span></span>

```xml
<PropertyGroup>
    <RestoreIgnoreFailedSource>true</RestoreIgnoreFailedSource>
<PropertyGroup>
```

### <a name="restore-outputs"></a><span data-ttu-id="09969-305">还原输出</span><span class="sxs-lookup"><span data-stu-id="09969-305">Restore outputs</span></span>

<span data-ttu-id="09969-306">还原会在生成 `obj` 文件夹中创建以下文件：</span><span class="sxs-lookup"><span data-stu-id="09969-306">Restore creates the following files in the build `obj` folder:</span></span>

| <span data-ttu-id="09969-307">文件</span><span class="sxs-lookup"><span data-stu-id="09969-307">File</span></span> | <span data-ttu-id="09969-308">描述</span><span class="sxs-lookup"><span data-stu-id="09969-308">Description</span></span> |
|--------|--------|
| `project.assets.json` | <span data-ttu-id="09969-309">以前为 `project.lock.json`</span><span class="sxs-lookup"><span data-stu-id="09969-309">Previously `project.lock.json`</span></span> |
| `{projectName}.projectFileExtension.nuget.g.props` | <span data-ttu-id="09969-310">包中包含的对 MSBuild 属性的引用</span><span class="sxs-lookup"><span data-stu-id="09969-310">References to MSBuild props contained in packages</span></span> |
| `{projectName}.projectFileExtension.nuget.g.targets` | <span data-ttu-id="09969-311">包中包含的对 MSBuild 目标的引用</span><span class="sxs-lookup"><span data-stu-id="09969-311">References to MSBuild targets contained in packages</span></span> |


### <a name="packagetargetfallback"></a><span data-ttu-id="09969-312">PackageTargetFallback</span><span class="sxs-lookup"><span data-stu-id="09969-312">PackageTargetFallback</span></span> 

<span data-ttu-id="09969-313">`PackageTargetFallback` 元素可用于指定要在还原包时使用的一组兼容目标（等效于 [`project.json` 中的 `imports`](../schema/project-json.md#imports)）。</span><span class="sxs-lookup"><span data-stu-id="09969-313">The `PackageTargetFallback` element allows you to specify a set of compatible targets to be used when restoring packages (the equivalent of [`imports` in `project.json`](../schema/project-json.md#imports)).</span></span> <span data-ttu-id="09969-314">旨在允许使用 dotnet [TxM](../schema/target-frameworks.md) 的包与未声明 dotnet TxM 的兼容包结合使用。</span><span class="sxs-lookup"><span data-stu-id="09969-314">It's designed to allow packages that use a dotnet [TxM](../schema/target-frameworks.md) to work with compatible packages that don't declare a dotnet TxM.</span></span> <span data-ttu-id="09969-315">也就是说，如果项目使用 dotnet TxM，那么所依赖的所有包也必须有 dotnet TxM，除非将 `<PackageTargetFallback>` 添加到项目中，以允许非 dotnet 平台与 dotnet 兼容。</span><span class="sxs-lookup"><span data-stu-id="09969-315">That is, if your project uses the dotnet TxM, then all the packages it depends on must also have a dotnet TxM, unless you add the `<PackageTargetFallback>` to your project in order to allow non-dotnet platforms to be compatible with dotnet.</span></span> 

<span data-ttu-id="09969-316">例如，如果项目使用的是 `netstandard1.6` TxM，且从属包仅包含 `lib/net45/a.dll` 和 `lib/portable-net45+win81/a.dll`，则项目将无法生成。</span><span class="sxs-lookup"><span data-stu-id="09969-316">For example, if the project is using the `netstandard1.6` TxM, and a dependent package contains only `lib/net45/a.dll` and `lib/portable-net45+win81/a.dll`, then the project will fail to build.</span></span> <span data-ttu-id="09969-317">如果需要的是后一种 DLL，则可以按照如下所示添加 `PackageTargetFallback`，声明 `portable-net45+win81` DLL 是兼容的：</span><span class="sxs-lookup"><span data-stu-id="09969-317">If what you want to bring in is the latter DLL, then you can add a `PackageTargetFallback` as follows to say that the `portable-net45+win81` DLL is compatible:</span></span>

```xml
<PackageTargetFallback Condition="'$(TargetFramework)'=='netstandard1.6'">
    portable-net45+win81
</PackageTargetFallback>
```

<span data-ttu-id="09969-318">若要声明项目中所有目标的回退，请停止 `Condition` 属性。</span><span class="sxs-lookup"><span data-stu-id="09969-318">To declare a fallback for all targets in your project, leave off the `Condition` attribute.</span></span> <span data-ttu-id="09969-319">还可以通过包括 `$(PackageTargetFallback)` 扩展任何现有 `PackageTargetFallback`，如下所示：</span><span class="sxs-lookup"><span data-stu-id="09969-319">You can also extend any existing `PackageTargetFallback` by including `$(PackageTargetFallback)` as shown here:</span></span>

```xml
<PackageTargetFallback>
    $(PackageTargetFallback);portable-net45+win81
</PackageTargetFallback >
```


### <a name="replacing-one-library-from-a-restore-graph"></a><span data-ttu-id="09969-320">从还原图中替换一个库</span><span class="sxs-lookup"><span data-stu-id="09969-320">Replacing one library from a restore graph</span></span>

<span data-ttu-id="09969-321">如果还原引入了错误的程序集，可以排除包默认选项，并将其替换为自己的选项。</span><span class="sxs-lookup"><span data-stu-id="09969-321">If a restore is bringing the wrong assembly, it is possible to exclude that packages default choice, and replace it with your own choice.</span></span> <span data-ttu-id="09969-322">首先使用顶级 `PackageReference`，排除所有资产：</span><span class="sxs-lookup"><span data-stu-id="09969-322">First with a top level `PackageReference`, exclude all assets:</span></span>

```xml
<PackageReference Include="Newtonsoft.Json" Version="9.0.1">
    <ExcludeAssets>All</ExcludeAssets>
</PackageReference>
```

<span data-ttu-id="09969-323">接下来，将自己的引用添加到适当的 DLL 本地副本：</span><span class="sxs-lookup"><span data-stu-id="09969-323">Next, add your own reference to the appropriate local copy of the DLL:</span></span>

```xml
<Reference Include="Newtonsoft.Json.dll" />
```
