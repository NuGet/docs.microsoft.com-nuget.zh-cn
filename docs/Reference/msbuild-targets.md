---
title: "作为 MSBuild 目标的 NuGet 包和还原 | Microsoft Docs"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 04/03/2017
ms.topic: article
ms.prod: nuget
ms.technology: 
description: "NuGet 包和还原可作为 MSBuild 目标直接用于 NuGet 4.0+。"
keywords: "NuGet 和 MSBuild, NuGet 包目标, NuGet 还原目标"
ms.reviewer:
- karann-msft
ms.openlocfilehash: 4d448af3d31e0907cba223c0ccec55604e94f055
ms.sourcegitcommit: 7969f6cd94eccfee5b62031bb404422139ccc383
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/20/2018
---
# <a name="nuget-pack-and-restore-as-msbuild-targets"></a><span data-ttu-id="cfa0e-104">作为 MSBuild 目标的 NuGet 包和还原</span><span class="sxs-lookup"><span data-stu-id="cfa0e-104">NuGet pack and restore as MSBuild targets</span></span>

<span data-ttu-id="cfa0e-105">NuGet 4.0+</span><span class="sxs-lookup"><span data-stu-id="cfa0e-105">*NuGet 4.0+*</span></span>

<span data-ttu-id="cfa0e-106">使用 PackageReference 格式，NuGet 4.0+ 可以将所有清单元数据直接存储在项目文件中，而不是使用单独的 `.nuspec` 文件。</span><span class="sxs-lookup"><span data-stu-id="cfa0e-106">With the PackageReference format, NuGet 4.0+ can store all manifest metadata directly within a project file rather than using a separate `.nuspec` file.</span></span>

<span data-ttu-id="cfa0e-107">如下所述，对于 MSBuild 15.1+，NuGet 还是具有 `pack` 目标和 `restore` 目标的一等 MSBuild 公民。</span><span class="sxs-lookup"><span data-stu-id="cfa0e-107">With MSBuild 15.1+, NuGet is also a first-class MSBuild citizen with the `pack` and `restore` targets as described below.</span></span> <span data-ttu-id="cfa0e-108">借助这些目标，你可以像使用任何其他 MSBuild 任务或目标一样使用 NuGet。</span><span class="sxs-lookup"><span data-stu-id="cfa0e-108">These targets allow you to work with NuGet as you would with any other MSBuild task or target.</span></span> <span data-ttu-id="cfa0e-109">（对于 Nuget 3.x 及更早版本，通过 NuGet CLI 使用 [pack](../tools/cli-ref-pack.md) 和 [restore](../tools/cli-ref-restore.md) 命令。）</span><span class="sxs-lookup"><span data-stu-id="cfa0e-109">(For NuGet 3.x and earlier, you use the [pack](../tools/cli-ref-pack.md) and [restore](../tools/cli-ref-restore.md) commands through the NuGet CLI instead.)</span></span>

## <a name="target-build-order"></a><span data-ttu-id="cfa0e-110">目标生成顺序</span><span class="sxs-lookup"><span data-stu-id="cfa0e-110">Target build order</span></span>

<span data-ttu-id="cfa0e-111">由于 `pack` 和 `restore` 为 MSBuild 目标，因此可以访问它们以增强工作流。</span><span class="sxs-lookup"><span data-stu-id="cfa0e-111">Because `pack` and `restore` are  MSBuild targets, you can access them to enhance your workflow.</span></span> <span data-ttu-id="cfa0e-112">例如，假设希望在打包后将包复制到网络共享。</span><span class="sxs-lookup"><span data-stu-id="cfa0e-112">For example, let’s say you want to copy your package to a network share after packing it.</span></span> <span data-ttu-id="cfa0e-113">此操作可通过向项目文件中添加以下内容来完成：</span><span class="sxs-lookup"><span data-stu-id="cfa0e-113">You can do that by adding the following in your project file:</span></span>

```xml
<Target Name="CopyPackage" AfterTargets="Pack">
    <Copy
        SourceFiles="$(OutputPath)..\$(PackageId).$(PackageVersion).nupkg"
        DestinationFolder="\\myshare\packageshare\"
        />
</Target>
```

<span data-ttu-id="cfa0e-114">同样，你可以编写 MSBuild 任务、编写自己的目标并使用 MSBuild 任务中的 NuGet 属性。</span><span class="sxs-lookup"><span data-stu-id="cfa0e-114">Similarly, you can write an MSBuild task, write your own target and consume NuGet properties in the MSBuild task.</span></span>

## <a name="pack-target"></a><span data-ttu-id="cfa0e-115">包目标</span><span class="sxs-lookup"><span data-stu-id="cfa0e-115">pack target</span></span>

<span data-ttu-id="cfa0e-116">如果使用包目标，即 `msbuild /t:pack`，MSBuild 会从项目文件中描述其输入。</span><span class="sxs-lookup"><span data-stu-id="cfa0e-116">When using the pack target, that is, `msbuild /t:pack`, MSBuild draws its inputs from the project file.</span></span> <span data-ttu-id="cfa0e-117">下表描述了可以添加到项目文件第一个 `<PropertyGroup>` 节点中的 MSBuild 属性。</span><span class="sxs-lookup"><span data-stu-id="cfa0e-117">The table below describes the MSBuild properties that can be added to a project file within the first `<PropertyGroup>` node.</span></span> <span data-ttu-id="cfa0e-118">在 Visual Studio 2017 及更高版本中，通过右键单击项目并选择上下文菜单上的“编辑 {project_name}”，即可轻松进行这些编辑。</span><span class="sxs-lookup"><span data-stu-id="cfa0e-118">You can make these edits easily in Visual Studio 2017 and later by right-clicking the project and selecting **Edit {project_name}** on the context menu.</span></span> <span data-ttu-id="cfa0e-119">为方便起见，表由 [`.nuspec` 文件](../reference/nuspec.md)中的等效属性组织。</span><span class="sxs-lookup"><span data-stu-id="cfa0e-119">For convenience the table is organized by the equivalent property in a [`.nuspec` file](../reference/nuspec.md).</span></span>

<span data-ttu-id="cfa0e-120">请注意，`.nuspec` 的 `Owners` 和 `Summary` 属性不受 MSBuild 支持。</span><span class="sxs-lookup"><span data-stu-id="cfa0e-120">Note that the `Owners` and `Summary` properties from `.nuspec` are not supported with MSBuild.</span></span>

| <span data-ttu-id="cfa0e-121">属性/NuSpec 值</span><span class="sxs-lookup"><span data-stu-id="cfa0e-121">Attribute/NuSpec Value</span></span> | <span data-ttu-id="cfa0e-122">MSBuild 属性</span><span class="sxs-lookup"><span data-stu-id="cfa0e-122">MSBuild Property</span></span> | <span data-ttu-id="cfa0e-123">默认</span><span class="sxs-lookup"><span data-stu-id="cfa0e-123">Default</span></span> | <span data-ttu-id="cfa0e-124">说明</span><span class="sxs-lookup"><span data-stu-id="cfa0e-124">Notes</span></span> |
|--------|--------|--------|--------|
| <span data-ttu-id="cfa0e-125">Id</span><span class="sxs-lookup"><span data-stu-id="cfa0e-125">Id</span></span> | <span data-ttu-id="cfa0e-126">PackageId</span><span class="sxs-lookup"><span data-stu-id="cfa0e-126">PackageId</span></span> | <span data-ttu-id="cfa0e-127">AssemblyName</span><span class="sxs-lookup"><span data-stu-id="cfa0e-127">AssemblyName</span></span> | <span data-ttu-id="cfa0e-128">MSBuild 的 $(AssemblyName)</span><span class="sxs-lookup"><span data-stu-id="cfa0e-128">$(AssemblyName) from MSBuild</span></span> |
| <span data-ttu-id="cfa0e-129">版本</span><span class="sxs-lookup"><span data-stu-id="cfa0e-129">Version</span></span> | <span data-ttu-id="cfa0e-130">PackageVersion</span><span class="sxs-lookup"><span data-stu-id="cfa0e-130">PackageVersion</span></span> | <span data-ttu-id="cfa0e-131">版本</span><span class="sxs-lookup"><span data-stu-id="cfa0e-131">Version</span></span> | <span data-ttu-id="cfa0e-132">这与 SemVer 兼容，例如，“1.0.0”、“1.0.0-beta”或“1.0.0-beta-00345”</span><span class="sxs-lookup"><span data-stu-id="cfa0e-132">This is semver compatible, for example “1.0.0”, “1.0.0-beta”, or “1.0.0-beta-00345”</span></span> |
| <span data-ttu-id="cfa0e-133">VersionPrefix</span><span class="sxs-lookup"><span data-stu-id="cfa0e-133">VersionPrefix</span></span> | <span data-ttu-id="cfa0e-134">PackageVersionPrefix</span><span class="sxs-lookup"><span data-stu-id="cfa0e-134">PackageVersionPrefix</span></span> | <span data-ttu-id="cfa0e-135">空</span><span class="sxs-lookup"><span data-stu-id="cfa0e-135">empty</span></span> | <span data-ttu-id="cfa0e-136">设置 PackageVersion 会覆盖 PackageVersionPrefix</span><span class="sxs-lookup"><span data-stu-id="cfa0e-136">Setting PackageVersion overwrites PackageVersionPrefix</span></span> |
| <span data-ttu-id="cfa0e-137">VersionSuffix</span><span class="sxs-lookup"><span data-stu-id="cfa0e-137">VersionSuffix</span></span> | <span data-ttu-id="cfa0e-138">PackageVersionSuffix</span><span class="sxs-lookup"><span data-stu-id="cfa0e-138">PackageVersionSuffix</span></span> | <span data-ttu-id="cfa0e-139">空</span><span class="sxs-lookup"><span data-stu-id="cfa0e-139">empty</span></span> | <span data-ttu-id="cfa0e-140">MSBuild 的 $(VersionSuffix)。</span><span class="sxs-lookup"><span data-stu-id="cfa0e-140">$(VersionSuffix) from MSBuild.</span></span> <span data-ttu-id="cfa0e-141">设置 PackageVersion 会覆盖 PackageVersionSuffix</span><span class="sxs-lookup"><span data-stu-id="cfa0e-141">Setting PackageVersion overwrites PackageVersionSuffix</span></span> |
| <span data-ttu-id="cfa0e-142">作者</span><span class="sxs-lookup"><span data-stu-id="cfa0e-142">Authors</span></span> | <span data-ttu-id="cfa0e-143">作者</span><span class="sxs-lookup"><span data-stu-id="cfa0e-143">Authors</span></span> | <span data-ttu-id="cfa0e-144">当前用户的用户名</span><span class="sxs-lookup"><span data-stu-id="cfa0e-144">Username of the current user</span></span> | |
| <span data-ttu-id="cfa0e-145">Owners</span><span class="sxs-lookup"><span data-stu-id="cfa0e-145">Owners</span></span> | <span data-ttu-id="cfa0e-146">不可用</span><span class="sxs-lookup"><span data-stu-id="cfa0e-146">N/A</span></span> | <span data-ttu-id="cfa0e-147">NuSpec 中不存在</span><span class="sxs-lookup"><span data-stu-id="cfa0e-147">Not present in NuSpec</span></span> | |
| <span data-ttu-id="cfa0e-148">标题</span><span class="sxs-lookup"><span data-stu-id="cfa0e-148">Title</span></span> | <span data-ttu-id="cfa0e-149">标题</span><span class="sxs-lookup"><span data-stu-id="cfa0e-149">Title</span></span> | <span data-ttu-id="cfa0e-150">PackageId</span><span class="sxs-lookup"><span data-stu-id="cfa0e-150">The PackageId</span></span>| |
| <span data-ttu-id="cfa0e-151">描述</span><span class="sxs-lookup"><span data-stu-id="cfa0e-151">Description</span></span> | <span data-ttu-id="cfa0e-152">描述</span><span class="sxs-lookup"><span data-stu-id="cfa0e-152">Description</span></span> | <span data-ttu-id="cfa0e-153">“包描述”</span><span class="sxs-lookup"><span data-stu-id="cfa0e-153">"Package Description"</span></span> | |
| <span data-ttu-id="cfa0e-154">Copyright</span><span class="sxs-lookup"><span data-stu-id="cfa0e-154">Copyright</span></span> | <span data-ttu-id="cfa0e-155">Copyright</span><span class="sxs-lookup"><span data-stu-id="cfa0e-155">Copyright</span></span> | <span data-ttu-id="cfa0e-156">空</span><span class="sxs-lookup"><span data-stu-id="cfa0e-156">empty</span></span> | |
| <span data-ttu-id="cfa0e-157">requireLicenseAcceptance</span><span class="sxs-lookup"><span data-stu-id="cfa0e-157">RequireLicenseAcceptance</span></span> | <span data-ttu-id="cfa0e-158">PackageRequireLicenseAcceptance</span><span class="sxs-lookup"><span data-stu-id="cfa0e-158">PackageRequireLicenseAcceptance</span></span> | <span data-ttu-id="cfa0e-159">False</span><span class="sxs-lookup"><span data-stu-id="cfa0e-159">false</span></span> | |
| <span data-ttu-id="cfa0e-160">LicenseUrl</span><span class="sxs-lookup"><span data-stu-id="cfa0e-160">LicenseUrl</span></span> | <span data-ttu-id="cfa0e-161">PackageLicenseUrl</span><span class="sxs-lookup"><span data-stu-id="cfa0e-161">PackageLicenseUrl</span></span> | <span data-ttu-id="cfa0e-162">空</span><span class="sxs-lookup"><span data-stu-id="cfa0e-162">empty</span></span> | |
| <span data-ttu-id="cfa0e-163">ProjectUrl</span><span class="sxs-lookup"><span data-stu-id="cfa0e-163">ProjectUrl</span></span> | <span data-ttu-id="cfa0e-164">PackageProjectUrl</span><span class="sxs-lookup"><span data-stu-id="cfa0e-164">PackageProjectUrl</span></span> | <span data-ttu-id="cfa0e-165">空</span><span class="sxs-lookup"><span data-stu-id="cfa0e-165">empty</span></span> | |
| <span data-ttu-id="cfa0e-166">IconUrl</span><span class="sxs-lookup"><span data-stu-id="cfa0e-166">IconUrl</span></span> | <span data-ttu-id="cfa0e-167">PackageIconUrl</span><span class="sxs-lookup"><span data-stu-id="cfa0e-167">PackageIconUrl</span></span> | <span data-ttu-id="cfa0e-168">空</span><span class="sxs-lookup"><span data-stu-id="cfa0e-168">empty</span></span> | |
| <span data-ttu-id="cfa0e-169">Tags</span><span class="sxs-lookup"><span data-stu-id="cfa0e-169">Tags</span></span> | <span data-ttu-id="cfa0e-170">PackageTags</span><span class="sxs-lookup"><span data-stu-id="cfa0e-170">PackageTags</span></span> | <span data-ttu-id="cfa0e-171">空</span><span class="sxs-lookup"><span data-stu-id="cfa0e-171">empty</span></span> | <span data-ttu-id="cfa0e-172">使用分号分隔标记。</span><span class="sxs-lookup"><span data-stu-id="cfa0e-172">Tags are semi-colon delimited.</span></span> |
| <span data-ttu-id="cfa0e-173">ReleaseNotes</span><span class="sxs-lookup"><span data-stu-id="cfa0e-173">ReleaseNotes</span></span> | <span data-ttu-id="cfa0e-174">PackageReleaseNotes</span><span class="sxs-lookup"><span data-stu-id="cfa0e-174">PackageReleaseNotes</span></span> | <span data-ttu-id="cfa0e-175">空</span><span class="sxs-lookup"><span data-stu-id="cfa0e-175">empty</span></span> | |
| <span data-ttu-id="cfa0e-176">存储库/Url</span><span class="sxs-lookup"><span data-stu-id="cfa0e-176">Repository/Url</span></span> | <span data-ttu-id="cfa0e-177">RepositoryUrl</span><span class="sxs-lookup"><span data-stu-id="cfa0e-177">RepositoryUrl</span></span> | <span data-ttu-id="cfa0e-178">空</span><span class="sxs-lookup"><span data-stu-id="cfa0e-178">empty</span></span> | <span data-ttu-id="cfa0e-179">用于克隆或检索源代码存储库 URL。</span><span class="sxs-lookup"><span data-stu-id="cfa0e-179">Repository URL used to clone or retrieve source code.</span></span> <span data-ttu-id="cfa0e-180">示例： *https://github.com/NuGet/NuGet.Client.git*</span><span class="sxs-lookup"><span data-stu-id="cfa0e-180">Example: *https://github.com/NuGet/NuGet.Client.git*</span></span> |
| <span data-ttu-id="cfa0e-181">存储库/类型</span><span class="sxs-lookup"><span data-stu-id="cfa0e-181">Repository/Type</span></span> | <span data-ttu-id="cfa0e-182">RepositoryType</span><span class="sxs-lookup"><span data-stu-id="cfa0e-182">RepositoryType</span></span> | <span data-ttu-id="cfa0e-183">空</span><span class="sxs-lookup"><span data-stu-id="cfa0e-183">empty</span></span> | <span data-ttu-id="cfa0e-184">存储库类型。</span><span class="sxs-lookup"><span data-stu-id="cfa0e-184">Repository type.</span></span> <span data-ttu-id="cfa0e-185">示例： *git*， *tfs*。</span><span class="sxs-lookup"><span data-stu-id="cfa0e-185">Examples: *git*, *tfs*.</span></span> |
| <span data-ttu-id="cfa0e-186">存储库/分支</span><span class="sxs-lookup"><span data-stu-id="cfa0e-186">Repository/Branch</span></span> | <span data-ttu-id="cfa0e-187">RepositoryBranch</span><span class="sxs-lookup"><span data-stu-id="cfa0e-187">RepositoryBranch</span></span> | <span data-ttu-id="cfa0e-188">空</span><span class="sxs-lookup"><span data-stu-id="cfa0e-188">empty</span></span> | <span data-ttu-id="cfa0e-189">可选存储库分支信息。</span><span class="sxs-lookup"><span data-stu-id="cfa0e-189">Optional repository branch information.</span></span> <span data-ttu-id="cfa0e-190">*RepositoryUrl*还必须指定要包含此属性。</span><span class="sxs-lookup"><span data-stu-id="cfa0e-190">*RepositoryUrl* must also be specified for this property to be included.</span></span> <span data-ttu-id="cfa0e-191">示例： *master* (NuGet 4.7.0+)</span><span class="sxs-lookup"><span data-stu-id="cfa0e-191">Example: *master* (NuGet 4.7.0+)</span></span> |
| <span data-ttu-id="cfa0e-192">存储库/提交</span><span class="sxs-lookup"><span data-stu-id="cfa0e-192">Repository/Commit</span></span> | <span data-ttu-id="cfa0e-193">RepositoryCommit</span><span class="sxs-lookup"><span data-stu-id="cfa0e-193">RepositoryCommit</span></span> | <span data-ttu-id="cfa0e-194">空</span><span class="sxs-lookup"><span data-stu-id="cfa0e-194">empty</span></span> | <span data-ttu-id="cfa0e-195">针对构建的可选的存储库提交或变更集以指示哪些源包。</span><span class="sxs-lookup"><span data-stu-id="cfa0e-195">Optional repository commit or changeset to indicate which source the package was built against.</span></span> <span data-ttu-id="cfa0e-196">*RepositoryUrl*还必须指定要包含此属性。</span><span class="sxs-lookup"><span data-stu-id="cfa0e-196">*RepositoryUrl* must also be specified for this property to be included.</span></span> <span data-ttu-id="cfa0e-197">示例： *0e4d1b598f350b3dc675018d539114d1328189ef* (NuGet 4.7.0+)</span><span class="sxs-lookup"><span data-stu-id="cfa0e-197">Example: *0e4d1b598f350b3dc675018d539114d1328189ef* (NuGet 4.7.0+)</span></span> |
| <span data-ttu-id="cfa0e-198">PackageType</span><span class="sxs-lookup"><span data-stu-id="cfa0e-198">PackageType</span></span> | `<PackageType>DotNetCliTool, 1.0.0.0;Dependency, 2.0.0.0</PackageType>` | | |
| <span data-ttu-id="cfa0e-199">摘要</span><span class="sxs-lookup"><span data-stu-id="cfa0e-199">Summary</span></span> | <span data-ttu-id="cfa0e-200">不支持</span><span class="sxs-lookup"><span data-stu-id="cfa0e-200">Not supported</span></span> | | |

### <a name="pack-target-inputs"></a><span data-ttu-id="cfa0e-201">包目标输入</span><span class="sxs-lookup"><span data-stu-id="cfa0e-201">pack target inputs</span></span>

- <span data-ttu-id="cfa0e-202">IsPackable</span><span class="sxs-lookup"><span data-stu-id="cfa0e-202">IsPackable</span></span>
- <span data-ttu-id="cfa0e-203">PackageVersion</span><span class="sxs-lookup"><span data-stu-id="cfa0e-203">PackageVersion</span></span>
- <span data-ttu-id="cfa0e-204">PackageId</span><span class="sxs-lookup"><span data-stu-id="cfa0e-204">PackageId</span></span>
- <span data-ttu-id="cfa0e-205">作者</span><span class="sxs-lookup"><span data-stu-id="cfa0e-205">Authors</span></span>
- <span data-ttu-id="cfa0e-206">描述</span><span class="sxs-lookup"><span data-stu-id="cfa0e-206">Description</span></span>
- <span data-ttu-id="cfa0e-207">Copyright</span><span class="sxs-lookup"><span data-stu-id="cfa0e-207">Copyright</span></span>
- <span data-ttu-id="cfa0e-208">PackageRequireLicenseAcceptance</span><span class="sxs-lookup"><span data-stu-id="cfa0e-208">PackageRequireLicenseAcceptance</span></span>
- <span data-ttu-id="cfa0e-209">DevelopmentDependency</span><span class="sxs-lookup"><span data-stu-id="cfa0e-209">DevelopmentDependency</span></span>
- <span data-ttu-id="cfa0e-210">PackageLicenseUrl</span><span class="sxs-lookup"><span data-stu-id="cfa0e-210">PackageLicenseUrl</span></span>
- <span data-ttu-id="cfa0e-211">PackageProjectUrl</span><span class="sxs-lookup"><span data-stu-id="cfa0e-211">PackageProjectUrl</span></span>
- <span data-ttu-id="cfa0e-212">PackageIconUrl</span><span class="sxs-lookup"><span data-stu-id="cfa0e-212">PackageIconUrl</span></span>
- <span data-ttu-id="cfa0e-213">PackageReleaseNotes</span><span class="sxs-lookup"><span data-stu-id="cfa0e-213">PackageReleaseNotes</span></span>
- <span data-ttu-id="cfa0e-214">PackageTags</span><span class="sxs-lookup"><span data-stu-id="cfa0e-214">PackageTags</span></span>
- <span data-ttu-id="cfa0e-215">PackageOutputPath</span><span class="sxs-lookup"><span data-stu-id="cfa0e-215">PackageOutputPath</span></span>
- <span data-ttu-id="cfa0e-216">IncludeSymbols</span><span class="sxs-lookup"><span data-stu-id="cfa0e-216">IncludeSymbols</span></span>
- <span data-ttu-id="cfa0e-217">IncludeSource</span><span class="sxs-lookup"><span data-stu-id="cfa0e-217">IncludeSource</span></span>
- <span data-ttu-id="cfa0e-218">PackageTypes</span><span class="sxs-lookup"><span data-stu-id="cfa0e-218">PackageTypes</span></span>
- <span data-ttu-id="cfa0e-219">IsTool</span><span class="sxs-lookup"><span data-stu-id="cfa0e-219">IsTool</span></span>
- <span data-ttu-id="cfa0e-220">RepositoryUrl</span><span class="sxs-lookup"><span data-stu-id="cfa0e-220">RepositoryUrl</span></span>
- <span data-ttu-id="cfa0e-221">RepositoryType</span><span class="sxs-lookup"><span data-stu-id="cfa0e-221">RepositoryType</span></span>
- <span data-ttu-id="cfa0e-222">RepositoryBranch</span><span class="sxs-lookup"><span data-stu-id="cfa0e-222">RepositoryBranch</span></span>
- <span data-ttu-id="cfa0e-223">RepositoryCommit</span><span class="sxs-lookup"><span data-stu-id="cfa0e-223">RepositoryCommit</span></span>
- <span data-ttu-id="cfa0e-224">NoPackageAnalysis</span><span class="sxs-lookup"><span data-stu-id="cfa0e-224">NoPackageAnalysis</span></span>
- <span data-ttu-id="cfa0e-225">MinClientVersion</span><span class="sxs-lookup"><span data-stu-id="cfa0e-225">MinClientVersion</span></span>
- <span data-ttu-id="cfa0e-226">IncludeBuildOutput</span><span class="sxs-lookup"><span data-stu-id="cfa0e-226">IncludeBuildOutput</span></span>
- <span data-ttu-id="cfa0e-227">IncludeContentInPack</span><span class="sxs-lookup"><span data-stu-id="cfa0e-227">IncludeContentInPack</span></span>
- <span data-ttu-id="cfa0e-228">BuildOutputTargetFolder</span><span class="sxs-lookup"><span data-stu-id="cfa0e-228">BuildOutputTargetFolder</span></span>
- <span data-ttu-id="cfa0e-229">ContentTargetFolders</span><span class="sxs-lookup"><span data-stu-id="cfa0e-229">ContentTargetFolders</span></span>
- <span data-ttu-id="cfa0e-230">NuspecFile</span><span class="sxs-lookup"><span data-stu-id="cfa0e-230">NuspecFile</span></span>
- <span data-ttu-id="cfa0e-231">NuspecBasePath</span><span class="sxs-lookup"><span data-stu-id="cfa0e-231">NuspecBasePath</span></span>
- <span data-ttu-id="cfa0e-232">NuspecProperties</span><span class="sxs-lookup"><span data-stu-id="cfa0e-232">NuspecProperties</span></span>

## <a name="pack-scenarios"></a><span data-ttu-id="cfa0e-233">包方案</span><span class="sxs-lookup"><span data-stu-id="cfa0e-233">pack scenarios</span></span>

### <a name="packageiconurl"></a><span data-ttu-id="cfa0e-234">PackageIconUrl</span><span class="sxs-lookup"><span data-stu-id="cfa0e-234">PackageIconUrl</span></span>

<span data-ttu-id="cfa0e-235">作为 [NuGet 问题 2582](https://github.com/NuGet/Home/issues/2582) 更改的一部分，`PackageIconUrl` 最终将更改为 `PackageIconUri` 并且可成为包括在生成包根目录下的图标文件的相对路径。</span><span class="sxs-lookup"><span data-stu-id="cfa0e-235">As part of the change for [NuGet Issue 2582](https://github.com/NuGet/Home/issues/2582), `PackageIconUrl` will eventually be changed to `PackageIconUri` and can be relative path to a icon file which will included at the root of the resulting package.</span></span>

### <a name="output-assemblies"></a><span data-ttu-id="cfa0e-236">输出程序集</span><span class="sxs-lookup"><span data-stu-id="cfa0e-236">Output assemblies</span></span>

<span data-ttu-id="cfa0e-237">`nuget pack` 会复制扩展名为 `.exe`、`.dll`、`.xml`、`.winmd`、`.json` 和 `.pri` 的输出文件。</span><span class="sxs-lookup"><span data-stu-id="cfa0e-237">`nuget pack` copies output files with extensions `.exe`, `.dll`, `.xml`, `.winmd`, `.json`, and `.pri`.</span></span> <span data-ttu-id="cfa0e-238">复制的输出文件取决于 MSBuild 从 `BuiltOutputProjectGroup` 目标提供的内容。</span><span class="sxs-lookup"><span data-stu-id="cfa0e-238">The output files that are copied depend on what MSBuild provides from the `BuiltOutputProjectGroup` target.</span></span>

<span data-ttu-id="cfa0e-239">在项目文件或命令行中，有两种 MSBuild 属性可用于控制输出程序集的位置：</span><span class="sxs-lookup"><span data-stu-id="cfa0e-239">There are two MSBuild  properties that you can use in your project file or command line to control where output assemblies go:</span></span>

- <span data-ttu-id="cfa0e-240">`IncludeBuildOutput`：确定包中是否应包括生成输出程序集的布尔值。</span><span class="sxs-lookup"><span data-stu-id="cfa0e-240">`IncludeBuildOutput`: A boolean that determines whether the build output assemblies should be included in the package.</span></span>
- <span data-ttu-id="cfa0e-241">`BuildOutputTargetFolder`：指定应放置输出程序集的文件夹。</span><span class="sxs-lookup"><span data-stu-id="cfa0e-241">`BuildOutputTargetFolder`: Specifies the folder in which the output assemblies should be placed.</span></span> <span data-ttu-id="cfa0e-242">输出程序集（和其他输出文件）会复制到各自的框架文件夹中。</span><span class="sxs-lookup"><span data-stu-id="cfa0e-242">The output assemblies (and other output files) are copied into their respective framework folders.</span></span>

### <a name="package-references"></a><span data-ttu-id="cfa0e-243">包引用</span><span class="sxs-lookup"><span data-stu-id="cfa0e-243">Package references</span></span>

<span data-ttu-id="cfa0e-244">请参阅[项目文件中的包引用](../consume-packages/package-references-in-project-files.md)</span><span class="sxs-lookup"><span data-stu-id="cfa0e-244">See [Package References in Project Files](../consume-packages/package-references-in-project-files.md).</span></span>

### <a name="project-to-project-references"></a><span data-ttu-id="cfa0e-245">项目到项目的引用</span><span class="sxs-lookup"><span data-stu-id="cfa0e-245">Project to project references</span></span>

<span data-ttu-id="cfa0e-246">默认情况下，项目到项目的引用被视为 nuget 包引用，例如：</span><span class="sxs-lookup"><span data-stu-id="cfa0e-246">Project to project references are considered by default as nuget package references, for example:</span></span>

```xml
<ProjectReference Include="..\UwpLibrary2\UwpLibrary2.csproj"/>
```

<span data-ttu-id="cfa0e-247">也可将以下元数据添加到项目引用：</span><span class="sxs-lookup"><span data-stu-id="cfa0e-247">You can also add the following metadata to your project reference:</span></span>

```xml
<IncludeAssets>
<ExcludeAssets>
<PrivateAssets>
```

### <a name="including-content-in-a-package"></a><span data-ttu-id="cfa0e-248">在包中添加内容</span><span class="sxs-lookup"><span data-stu-id="cfa0e-248">Including content in a package</span></span>

<span data-ttu-id="cfa0e-249">若要添加内容，请将额外的元数据添加到现有的 `<Content>` 项。</span><span class="sxs-lookup"><span data-stu-id="cfa0e-249">To include content, add extra metadata to the existing `<Content>` item.</span></span> <span data-ttu-id="cfa0e-250">默认情况下，类型“Content”的所有内容都包括在包中，除非使用以下条目替代：</span><span class="sxs-lookup"><span data-stu-id="cfa0e-250">By default everything of type "Content" gets included in the package unless you override with entries like the following:</span></span>

 ```xml
    <Content Include="..\win7-x64\libuv.txt">
        <Pack>false</Pack>
    </Content>
 ```

<span data-ttu-id="cfa0e-251">默认情况下，所有内容都添加到包中 `content` 和 `contentFiles\any\<target_framework>` 文件夹根目录，并保留相对文件夹结构，除非指定包路径：</span><span class="sxs-lookup"><span data-stu-id="cfa0e-251">By default, everything gets added to the root of the `content` and `contentFiles\any\<target_framework>` folder within a package and preserves the relative folder structure, unless you specify a package path:</span></span>

```xml
<Content Include="..\win7-x64\libuv.txt">
    <Pack>true</Pack>
    <PackagePath>content\myfiles\</PackagePath>
</Content>
```

<span data-ttu-id="cfa0e-252">如果仅希望将所有内容都复制到特定根文件夹（而不是 `content` 和 `contentFiles`），可使用 MSBuild 属性 `ContentTargetFolders`，其默认值为“content;contentFiles”，但可以设置为任何其他文件夹名称。</span><span class="sxs-lookup"><span data-stu-id="cfa0e-252">If you want to copy all your content to only a specific root folder(s) (instead of `content` and `contentFiles` both), you can use the MSBuild property `ContentTargetFolders`, which defaults to "content;contentFiles" but can be set to any other folder names.</span></span> <span data-ttu-id="cfa0e-253">请注意，基于 `buildAction`，仅在 `ContentTargetFolders` 中指定“contentFiles”会将文件置于 `contentFiles\any\<target_framework>` 或 `contentFiles\<language>\<target_framework>` 下。</span><span class="sxs-lookup"><span data-stu-id="cfa0e-253">Note that just specifying "contentFiles" in `ContentTargetFolders` puts files under `contentFiles\any\<target_framework>` or `contentFiles\<language>\<target_framework>` based on `buildAction`.</span></span>

<span data-ttu-id="cfa0e-254">`PackagePath` 可以是一组以分号分隔的目标路径。</span><span class="sxs-lookup"><span data-stu-id="cfa0e-254">`PackagePath` can be a semicolon-delimited set of target paths.</span></span> <span data-ttu-id="cfa0e-255">指定空的包路径会将文件添加到包的根目录。</span><span class="sxs-lookup"><span data-stu-id="cfa0e-255">Specifying an empty package path would add the file to the root of the package.</span></span> <span data-ttu-id="cfa0e-256">例如，以下操作会将 `libuv.txt` 添加到 `content\myfiles`、`content\samples` 和包的根目录：</span><span class="sxs-lookup"><span data-stu-id="cfa0e-256">For example, the following adds `libuv.txt` to `content\myfiles`, `content\samples`, and the package root:</span></span>

```xml
<Content Include="..\win7-x64\libuv.txt">
    <Pack>true</Pack>
    <PackagePath>content\myfiles;content\sample;;</PackagePath>
</Content>
```

<span data-ttu-id="cfa0e-257">另外还有 MSBuild 属性 `$(IncludeContentInPack)`，默认值为 `true`。</span><span class="sxs-lookup"><span data-stu-id="cfa0e-257">There is also an MSBuild property `$(IncludeContentInPack)`, which defaults to `true`.</span></span> <span data-ttu-id="cfa0e-258">如果在任何项目中将此值设置为 `false`，则该项目的内容不会包括在 nuget 包中。</span><span class="sxs-lookup"><span data-stu-id="cfa0e-258">If this is set to `false` on any project, then the content from that project are not included in the nuget package.</span></span>

<span data-ttu-id="cfa0e-259">其他可在任何上述项上设置的特定于包的元数据包括 ```<PackageCopyToOutput>``` 和 ```<PackageFlatten>```，后者在输出 nuspec 中的 ```contentFiles``` 条目上设置 ```CopyToOutput``` 和 ```Flatten``` 值。</span><span class="sxs-lookup"><span data-stu-id="cfa0e-259">Other pack specific metadata that you can set on any of the above items includes ```<PackageCopyToOutput>``` and ```<PackageFlatten>``` which sets ```CopyToOutput``` and ```Flatten``` values on the ```contentFiles``` entry in the output nuspec.</span></span>

> [!Note]
> <span data-ttu-id="cfa0e-260">除了“Content”项，`<Pack>` 和 `<PackagePath>` 元数据还可以在具有 Compile、EmbeddedResource、ApplicationDefinition、Page、Resource、SplashScreen、DesignData、DesignDataWithDesignTimeCreateableTypes、CodeAnalysisDictionary、AndroidAsset、AndroidResource、BundleResource 或 None 生成操作的文件上进行设置。</span><span class="sxs-lookup"><span data-stu-id="cfa0e-260">Apart from Content items, the `<Pack>` and `<PackagePath>` metadata can also be set on files with a build action of Compile, EmbeddedResource, ApplicationDefinition, Page, Resource, SplashScreen, DesignData, DesignDataWithDesignTimeCreateableTypes, CodeAnalysisDictionary, AndroidAsset, AndroidResource, BundleResource or None.</span></span>
>
> <span data-ttu-id="cfa0e-261">使用通配模式时，对于将包的文件名追加到包路径，包路径必须以文件夹分隔符结尾，否则包路径将被视为包括文件名的完整路径。</span><span class="sxs-lookup"><span data-stu-id="cfa0e-261">For pack to append the filename to your package path when using globbing patterns, your package path must end with the folder separator character, otherwise the package path is treated as the full path including the file name.</span></span>

### <a name="includesymbols"></a><span data-ttu-id="cfa0e-262">IncludeSymbols</span><span class="sxs-lookup"><span data-stu-id="cfa0e-262">IncludeSymbols</span></span>

<span data-ttu-id="cfa0e-263">使用 `MSBuild /t:pack /p:IncludeSymbols=true` 时，相应的 `.pdb` 文件将随其他输出文件（`.dll`、`.exe`、`.winmd`、`.xml`、`.json`、`.pri`）一起复制。</span><span class="sxs-lookup"><span data-stu-id="cfa0e-263">When using `MSBuild /t:pack /p:IncludeSymbols=true`, the corresponding `.pdb` files are copied along with other output files (`.dll`, `.exe`, `.winmd`, `.xml`, `.json`, `.pri`).</span></span> <span data-ttu-id="cfa0e-264">请注意，设置 `IncludeSymbols=true` 会创建常规包和符号包。</span><span class="sxs-lookup"><span data-stu-id="cfa0e-264">Note that setting `IncludeSymbols=true` creates a regular package *and* a symbols package.</span></span>

### <a name="includesource"></a><span data-ttu-id="cfa0e-265">IncludeSource</span><span class="sxs-lookup"><span data-stu-id="cfa0e-265">IncludeSource</span></span>

<span data-ttu-id="cfa0e-266">这与 `IncludeSymbols` 相同，但它还会连同 `.pdb` 文件复制源文件。</span><span class="sxs-lookup"><span data-stu-id="cfa0e-266">This is the same as `IncludeSymbols`, except that it copies source files along with `.pdb` files as well.</span></span> <span data-ttu-id="cfa0e-267">类型为 `Compile` 的所有文件都会复制到 `src\<ProjectName>\`，并保留生成包中的相对路径文件夹结构。</span><span class="sxs-lookup"><span data-stu-id="cfa0e-267">All files of type `Compile` are copied over to `src\<ProjectName>\` preserving the relative path folder structure in the resulting package.</span></span> <span data-ttu-id="cfa0e-268">对于将 `TreatAsPackageReference` 设置为 `false` 的任何 `ProjectReference` 的源文件也是如此。</span><span class="sxs-lookup"><span data-stu-id="cfa0e-268">The same also happens for source files of any `ProjectReference` which has `TreatAsPackageReference` set to `false`.</span></span>

<span data-ttu-id="cfa0e-269">如果类型为 Compile 的文件位于项目文件夹外，则它只添加到了 `src\<ProjectName>\`。</span><span class="sxs-lookup"><span data-stu-id="cfa0e-269">If a file of type Compile, is outside the project folder, then it's just added to `src\<ProjectName>\`.</span></span>

### <a name="istool"></a><span data-ttu-id="cfa0e-270">IsTool</span><span class="sxs-lookup"><span data-stu-id="cfa0e-270">IsTool</span></span>

<span data-ttu-id="cfa0e-271">使用 `MSBuild /t:pack /p:IsTool=true` 时，所有输出文件（如[输出程序集](#output-assemblies)方案中所指定）都被复制到 `tools` 文件夹，而不是 `lib` 文件夹。</span><span class="sxs-lookup"><span data-stu-id="cfa0e-271">When using `MSBuild /t:pack /p:IsTool=true`, all output files, as specified in the [Output Assemblies](#output-assemblies) scenario, are copied to the `tools` folder instead of the `lib` folder.</span></span> <span data-ttu-id="cfa0e-272">请注意，这不同于 `DotNetCliTool`，后者通过在 `.csproj` 文件中设置 `PackageType` 进行指定。</span><span class="sxs-lookup"><span data-stu-id="cfa0e-272">Note that this is different from a `DotNetCliTool` which is specified by setting the `PackageType` in `.csproj` file.</span></span>

### <a name="packing-using-a-nuspec"></a><span data-ttu-id="cfa0e-273">使用 .nuspec 打包</span><span class="sxs-lookup"><span data-stu-id="cfa0e-273">Packing using a .nuspec</span></span>

<span data-ttu-id="cfa0e-274">可以使用 `.nuspec` 文件打包项目，前提是拥有可导入 `NuGet.Build.Tasks.Pack.targets` 的项目文件，以便可执行包任务。</span><span class="sxs-lookup"><span data-stu-id="cfa0e-274">You can use a `.nuspec` file to pack your project provided that you have a project file to import `NuGet.Build.Tasks.Pack.targets` so that the pack task can be executed.</span></span> <span data-ttu-id="cfa0e-275">以下三个 MSBuild 属性与使用 `.nuspec` 的打包相关：</span><span class="sxs-lookup"><span data-stu-id="cfa0e-275">The following three MSBuild properties are relevant to packing using a `.nuspec`:</span></span>

1. <span data-ttu-id="cfa0e-276">`NuspecFile`：用于打包的 `.nuspec` 文件的相对或绝对路径。</span><span class="sxs-lookup"><span data-stu-id="cfa0e-276">`NuspecFile`: relative or absolute path to the `.nuspec` file being used for packing.</span></span>
1. <span data-ttu-id="cfa0e-277">`NuspecProperties`：键=值对的分号分隔列表。</span><span class="sxs-lookup"><span data-stu-id="cfa0e-277">`NuspecProperties`: a semicolon-separated list of key=value pairs.</span></span> <span data-ttu-id="cfa0e-278">由于 MSBuild 命令行分析工作的方式，必须指定多个属性，如下所示：`/p:NuspecProperties=\"key1=value1;key2=value2\"`。</span><span class="sxs-lookup"><span data-stu-id="cfa0e-278">Due to the way MSBuild command-line parsing works, multiple properties must be specified as follows: `/p:NuspecProperties=\"key1=value1;key2=value2\"`.</span></span>  
1. <span data-ttu-id="cfa0e-279">`NuspecBasePath`：`.nuspec` 文件的基路径。</span><span class="sxs-lookup"><span data-stu-id="cfa0e-279">`NuspecBasePath`: Base path for the `.nuspec` file.</span></span>

<span data-ttu-id="cfa0e-280">如果使用 `dotnet.exe` 打包项目，请使用类似于下面的命令：</span><span class="sxs-lookup"><span data-stu-id="cfa0e-280">If using `dotnet.exe` to pack your project, use a command like the following:</span></span>

```cli
dotnet pack <path to .csproj file> /p:NuspecFile=<path to nuspec file> /p:NuspecProperties=<> /p:NuspecBasePath=<Base path> 
```

<span data-ttu-id="cfa0e-281">如果使用 MSBuild 打包项目，请使用类似于下面的命令：</span><span class="sxs-lookup"><span data-stu-id="cfa0e-281">If using MSBuild to pack your project, use a command like the following:</span></span>

```cli
msbuild /t:pack <path to .csproj file> /p:NuspecFile=<path to nuspec file> /p:NuspecProperties=<> /p:NuspecBasePath=<Base path> 
```

## <a name="restore-target"></a><span data-ttu-id="cfa0e-282">还原目标</span><span class="sxs-lookup"><span data-stu-id="cfa0e-282">restore target</span></span>

<span data-ttu-id="cfa0e-283">`MSBuild /t:restore`（`nuget restore` 和 `dotnet restore` 与 .NET Core 项目一起使用）会还原项目文件中引用的包，如下所示：</span><span class="sxs-lookup"><span data-stu-id="cfa0e-283">`MSBuild /t:restore` (which `nuget restore` and `dotnet restore` use with .NET Core projects), restores packages referenced in the project file as follows:</span></span>

1. <span data-ttu-id="cfa0e-284">读取所有项目到项目的引用</span><span class="sxs-lookup"><span data-stu-id="cfa0e-284">Read all project to project references</span></span>
1. <span data-ttu-id="cfa0e-285">读取项目属性以查找中间文件夹和目标框架</span><span class="sxs-lookup"><span data-stu-id="cfa0e-285">Read the project properties to find the intermediate folder and target frameworks</span></span>
1. <span data-ttu-id="cfa0e-286">将 msbuild 数据传递到 NuGet.Build.Tasks.dll</span><span class="sxs-lookup"><span data-stu-id="cfa0e-286">Pass msbuild data to NuGet.Build.Tasks.dll</span></span>
1. <span data-ttu-id="cfa0e-287">运行还原</span><span class="sxs-lookup"><span data-stu-id="cfa0e-287">Run restore</span></span>
1. <span data-ttu-id="cfa0e-288">下载包</span><span class="sxs-lookup"><span data-stu-id="cfa0e-288">Download packages</span></span>
1. <span data-ttu-id="cfa0e-289">编写资产文件、目标和属性</span><span class="sxs-lookup"><span data-stu-id="cfa0e-289">Write assets file, targets, and props</span></span>

### <a name="restore-properties"></a><span data-ttu-id="cfa0e-290">还原属性</span><span class="sxs-lookup"><span data-stu-id="cfa0e-290">Restore properties</span></span>

<span data-ttu-id="cfa0e-291">其他的还原设置可能来自项目文件中的 MSBuild 属性。</span><span class="sxs-lookup"><span data-stu-id="cfa0e-291">Additional restore settings may come from MSBuild properties in the project file.</span></span> <span data-ttu-id="cfa0e-292">还可以从命令行使用 `/p:` 开关设置值（请参阅以下示例）。</span><span class="sxs-lookup"><span data-stu-id="cfa0e-292">Values can also be set from the command line using the `/p:` switch (see Examples below).</span></span>

| <span data-ttu-id="cfa0e-293">属性</span><span class="sxs-lookup"><span data-stu-id="cfa0e-293">Property</span></span> | <span data-ttu-id="cfa0e-294">描述</span><span class="sxs-lookup"><span data-stu-id="cfa0e-294">Description</span></span> |
|--------|--------|
| <span data-ttu-id="cfa0e-295">RestoreSources</span><span class="sxs-lookup"><span data-stu-id="cfa0e-295">RestoreSources</span></span> | <span data-ttu-id="cfa0e-296">以分号分隔的包源列表。</span><span class="sxs-lookup"><span data-stu-id="cfa0e-296">Semicolon-delimited list of package sources.</span></span> |
| <span data-ttu-id="cfa0e-297">RestorePackagesPath</span><span class="sxs-lookup"><span data-stu-id="cfa0e-297">RestorePackagesPath</span></span> | <span data-ttu-id="cfa0e-298">用户包文件夹路径。</span><span class="sxs-lookup"><span data-stu-id="cfa0e-298">User packages folder path.</span></span> |
| <span data-ttu-id="cfa0e-299">RestoreDisableParallel</span><span class="sxs-lookup"><span data-stu-id="cfa0e-299">RestoreDisableParallel</span></span> | <span data-ttu-id="cfa0e-300">将下载限制为一次一个。</span><span class="sxs-lookup"><span data-stu-id="cfa0e-300">Limit downloads to one at a time.</span></span> |
| <span data-ttu-id="cfa0e-301">RestoreConfigFile</span><span class="sxs-lookup"><span data-stu-id="cfa0e-301">RestoreConfigFile</span></span> | <span data-ttu-id="cfa0e-302">要应用的 `Nuget.Config` 文件的路径。</span><span class="sxs-lookup"><span data-stu-id="cfa0e-302">Path to a `Nuget.Config` file to apply.</span></span> |
| <span data-ttu-id="cfa0e-303">RestoreNoCache</span><span class="sxs-lookup"><span data-stu-id="cfa0e-303">RestoreNoCache</span></span> | <span data-ttu-id="cfa0e-304">如果为“true”，则避免使用 web 缓存。</span><span class="sxs-lookup"><span data-stu-id="cfa0e-304">If true, avoids using the web cache.</span></span> |
| <span data-ttu-id="cfa0e-305">RestoreIgnoreFailedSources</span><span class="sxs-lookup"><span data-stu-id="cfa0e-305">RestoreIgnoreFailedSources</span></span> | <span data-ttu-id="cfa0e-306">如果为“true”，则忽略失败或丢失的包源。</span><span class="sxs-lookup"><span data-stu-id="cfa0e-306">If true, ignores failing or missing package sources.</span></span> |
| <span data-ttu-id="cfa0e-307">RestoreTaskAssemblyFile</span><span class="sxs-lookup"><span data-stu-id="cfa0e-307">RestoreTaskAssemblyFile</span></span> | <span data-ttu-id="cfa0e-308">`NuGet.Build.Tasks.dll` 的路径。</span><span class="sxs-lookup"><span data-stu-id="cfa0e-308">Path to `NuGet.Build.Tasks.dll`.</span></span> |
| <span data-ttu-id="cfa0e-309">RestoreGraphProjectInput</span><span class="sxs-lookup"><span data-stu-id="cfa0e-309">RestoreGraphProjectInput</span></span> | <span data-ttu-id="cfa0e-310">要还原的以分号分隔的项目列表，其中应包含绝对路径。</span><span class="sxs-lookup"><span data-stu-id="cfa0e-310">Semicolon-delimited list of projects to restore, which should contain absolute paths.</span></span> |
| <span data-ttu-id="cfa0e-311">RestoreOutputPath</span><span class="sxs-lookup"><span data-stu-id="cfa0e-311">RestoreOutputPath</span></span> | <span data-ttu-id="cfa0e-312">输出文件夹，默认为 `obj` 文件夹。</span><span class="sxs-lookup"><span data-stu-id="cfa0e-312">Output folder, defaulting to the `obj` folder.</span></span> |

#### <a name="examples"></a><span data-ttu-id="cfa0e-313">示例</span><span class="sxs-lookup"><span data-stu-id="cfa0e-313">Examples</span></span>

<span data-ttu-id="cfa0e-314">命令行：</span><span class="sxs-lookup"><span data-stu-id="cfa0e-314">Command line:</span></span>

```cli
msbuild /t:restore /p:RestoreConfigFile=<path>
```

<span data-ttu-id="cfa0e-315">项目文件：</span><span class="sxs-lookup"><span data-stu-id="cfa0e-315">Project file:</span></span>

```xml
<PropertyGroup>
    <RestoreIgnoreFailedSource>true</RestoreIgnoreFailedSource>
<PropertyGroup>
```

### <a name="restore-outputs"></a><span data-ttu-id="cfa0e-316">还原输出</span><span class="sxs-lookup"><span data-stu-id="cfa0e-316">Restore outputs</span></span>

<span data-ttu-id="cfa0e-317">还原会在生成 `obj` 文件夹中创建以下文件：</span><span class="sxs-lookup"><span data-stu-id="cfa0e-317">Restore creates the following files in the build `obj` folder:</span></span>

| <span data-ttu-id="cfa0e-318">文件</span><span class="sxs-lookup"><span data-stu-id="cfa0e-318">File</span></span> | <span data-ttu-id="cfa0e-319">描述</span><span class="sxs-lookup"><span data-stu-id="cfa0e-319">Description</span></span> |
|--------|--------|
| `project.assets.json` | <span data-ttu-id="cfa0e-320">以前为 `project.lock.json`</span><span class="sxs-lookup"><span data-stu-id="cfa0e-320">Previously `project.lock.json`</span></span> |
| `{projectName}.projectFileExtension.nuget.g.props` | <span data-ttu-id="cfa0e-321">包中包含的对 MSBuild 属性的引用</span><span class="sxs-lookup"><span data-stu-id="cfa0e-321">References to MSBuild props contained in packages</span></span> |
| `{projectName}.projectFileExtension.nuget.g.targets` | <span data-ttu-id="cfa0e-322">包中包含的对 MSBuild 目标的引用</span><span class="sxs-lookup"><span data-stu-id="cfa0e-322">References to MSBuild targets contained in packages</span></span> |

### <a name="packagetargetfallback"></a><span data-ttu-id="cfa0e-323">PackageTargetFallback</span><span class="sxs-lookup"><span data-stu-id="cfa0e-323">PackageTargetFallback</span></span>

<span data-ttu-id="cfa0e-324">`PackageTargetFallback` 元素可用于指定要在还原包时使用的一组兼容目标。</span><span class="sxs-lookup"><span data-stu-id="cfa0e-324">The `PackageTargetFallback` element allows you to specify a set of compatible targets to be used when restoring packages.</span></span> <span data-ttu-id="cfa0e-325">旨在允许使用 dotnet [TxM](../reference/target-frameworks.md) 的包与未声明 dotnet TxM 的兼容包结合使用。</span><span class="sxs-lookup"><span data-stu-id="cfa0e-325">It's designed to allow packages that use a dotnet [TxM](../reference/target-frameworks.md) to work with compatible packages that don't declare a dotnet TxM.</span></span> <span data-ttu-id="cfa0e-326">也就是说，如果项目使用 dotnet TxM，那么所依赖的所有包也必须有 dotnet TxM，除非将 `<PackageTargetFallback>` 添加到项目中，以允许非 dotnet 平台与 dotnet 兼容。</span><span class="sxs-lookup"><span data-stu-id="cfa0e-326">That is, if your project uses the dotnet TxM, then all the packages it depends on must also have a dotnet TxM, unless you add the `<PackageTargetFallback>` to your project in order to allow non-dotnet platforms to be compatible with dotnet.</span></span>

<span data-ttu-id="cfa0e-327">例如，如果项目使用的是 `netstandard1.6` TxM，且从属包仅包含 `lib/net45/a.dll` 和 `lib/portable-net45+win81/a.dll`，则项目将无法生成。</span><span class="sxs-lookup"><span data-stu-id="cfa0e-327">For example, if the project is using the `netstandard1.6` TxM, and a dependent package contains only `lib/net45/a.dll` and `lib/portable-net45+win81/a.dll`, then the project will fail to build.</span></span> <span data-ttu-id="cfa0e-328">如果需要的是后一种 DLL，则可以按照如下所示添加 `PackageTargetFallback`，声明 `portable-net45+win81` DLL 是兼容的：</span><span class="sxs-lookup"><span data-stu-id="cfa0e-328">If what you want to bring in is the latter DLL, then you can add a `PackageTargetFallback` as follows to say that the `portable-net45+win81` DLL is compatible:</span></span>

```xml
<PackageTargetFallback Condition="'$(TargetFramework)'=='netstandard1.6'">
    portable-net45+win81
</PackageTargetFallback>
```

<span data-ttu-id="cfa0e-329">若要声明项目中所有目标的回退，请停止 `Condition` 属性。</span><span class="sxs-lookup"><span data-stu-id="cfa0e-329">To declare a fallback for all targets in your project, leave off the `Condition` attribute.</span></span> <span data-ttu-id="cfa0e-330">还可以通过包括 `$(PackageTargetFallback)` 扩展任何现有 `PackageTargetFallback`，如下所示：</span><span class="sxs-lookup"><span data-stu-id="cfa0e-330">You can also extend any existing `PackageTargetFallback` by including `$(PackageTargetFallback)` as shown here:</span></span>

```xml
<PackageTargetFallback>
    $(PackageTargetFallback);portable-net45+win81
</PackageTargetFallback >
```

### <a name="replacing-one-library-from-a-restore-graph"></a><span data-ttu-id="cfa0e-331">从还原图中替换一个库</span><span class="sxs-lookup"><span data-stu-id="cfa0e-331">Replacing one library from a restore graph</span></span>

<span data-ttu-id="cfa0e-332">如果还原引入了错误的程序集，可以排除包默认选项，并将其替换为自己的选项。</span><span class="sxs-lookup"><span data-stu-id="cfa0e-332">If a restore is bringing the wrong assembly, it's possible to exclude that packages default choice, and replace it with your own choice.</span></span> <span data-ttu-id="cfa0e-333">首先使用顶级 `PackageReference`，排除所有资产：</span><span class="sxs-lookup"><span data-stu-id="cfa0e-333">First with a top level `PackageReference`, exclude all assets:</span></span>

```xml
<PackageReference Include="Newtonsoft.Json" Version="9.0.1">
    <ExcludeAssets>All</ExcludeAssets>
</PackageReference>
```

<span data-ttu-id="cfa0e-334">接下来，将自己的引用添加到适当的 DLL 本地副本：</span><span class="sxs-lookup"><span data-stu-id="cfa0e-334">Next, add your own reference to the appropriate local copy of the DLL:</span></span>

```xml
<Reference Include="Newtonsoft.Json.dll" />
```
