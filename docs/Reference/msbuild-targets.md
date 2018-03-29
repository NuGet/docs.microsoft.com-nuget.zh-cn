---
title: 作为 MSBuild 目标的 NuGet 包和还原 | Microsoft Docs
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 03/23/2018
ms.topic: article
ms.prod: nuget
ms.technology: ''
description: NuGet 包和还原可作为 MSBuild 目标直接用于 NuGet 4.0+。
keywords: NuGet 和 MSBuild, NuGet 包目标, NuGet 还原目标
ms.reviewer:
- karann-msft
- unniravindranathan
ms.workload:
- dotnet
- aspnet
ms.openlocfilehash: a9c2c2229d717dff8472dce0ba568e4a21900b19
ms.sourcegitcommit: beb229893559824e8abd6ab16707fd5fe1c6ac26
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/28/2018
---
# <a name="nuget-pack-and-restore-as-msbuild-targets"></a><span data-ttu-id="eff7d-104">作为 MSBuild 目标的 NuGet 包和还原</span><span class="sxs-lookup"><span data-stu-id="eff7d-104">NuGet pack and restore as MSBuild targets</span></span>

<span data-ttu-id="eff7d-105">NuGet 4.0+</span><span class="sxs-lookup"><span data-stu-id="eff7d-105">*NuGet 4.0+*</span></span>

<span data-ttu-id="eff7d-106">使用 PackageReference 格式，NuGet 4.0+ 可以将所有清单元数据直接存储在项目文件中，而不是使用单独的 `.nuspec` 文件。</span><span class="sxs-lookup"><span data-stu-id="eff7d-106">With the PackageReference format, NuGet 4.0+ can store all manifest metadata directly within a project file rather than using a separate `.nuspec` file.</span></span>

<span data-ttu-id="eff7d-107">如下所述，对于 MSBuild 15.1+，NuGet 还是具有 `pack` 目标和 `restore` 目标的一等 MSBuild 公民。</span><span class="sxs-lookup"><span data-stu-id="eff7d-107">With MSBuild 15.1+, NuGet is also a first-class MSBuild citizen with the `pack` and `restore` targets as described below.</span></span> <span data-ttu-id="eff7d-108">借助这些目标，你可以像使用任何其他 MSBuild 任务或目标一样使用 NuGet。</span><span class="sxs-lookup"><span data-stu-id="eff7d-108">These targets allow you to work with NuGet as you would with any other MSBuild task or target.</span></span> <span data-ttu-id="eff7d-109">（对于 Nuget 3.x 及更早版本，通过 NuGet CLI 使用 [pack](../tools/cli-ref-pack.md) 和 [restore](../tools/cli-ref-restore.md) 命令。）</span><span class="sxs-lookup"><span data-stu-id="eff7d-109">(For NuGet 3.x and earlier, you use the [pack](../tools/cli-ref-pack.md) and [restore](../tools/cli-ref-restore.md) commands through the NuGet CLI instead.)</span></span>

## <a name="target-build-order"></a><span data-ttu-id="eff7d-110">目标生成顺序</span><span class="sxs-lookup"><span data-stu-id="eff7d-110">Target build order</span></span>

<span data-ttu-id="eff7d-111">由于 `pack` 和 `restore` 为 MSBuild 目标，因此可以访问它们以增强工作流。</span><span class="sxs-lookup"><span data-stu-id="eff7d-111">Because `pack` and `restore` are  MSBuild targets, you can access them to enhance your workflow.</span></span> <span data-ttu-id="eff7d-112">例如，假设希望在打包后将包复制到网络共享。</span><span class="sxs-lookup"><span data-stu-id="eff7d-112">For example, let’s say you want to copy your package to a network share after packing it.</span></span> <span data-ttu-id="eff7d-113">此操作可通过向项目文件中添加以下内容来完成：</span><span class="sxs-lookup"><span data-stu-id="eff7d-113">You can do that by adding the following in your project file:</span></span>

```xml
<Target Name="CopyPackage" AfterTargets="Pack">
    <Copy
        SourceFiles="$(OutputPath)..\$(PackageId).$(PackageVersion).nupkg"
        DestinationFolder="\\myshare\packageshare\"
        />
</Target>
```

<span data-ttu-id="eff7d-114">同样，你可以编写 MSBuild 任务、编写自己的目标并使用 MSBuild 任务中的 NuGet 属性。</span><span class="sxs-lookup"><span data-stu-id="eff7d-114">Similarly, you can write an MSBuild task, write your own target and consume NuGet properties in the MSBuild task.</span></span>

## <a name="pack-target"></a><span data-ttu-id="eff7d-115">包目标</span><span class="sxs-lookup"><span data-stu-id="eff7d-115">pack target</span></span>

<span data-ttu-id="eff7d-116">对于标准.NET 项目使用 PackageReference 格式，并使用`msbuild /t:pack`绘制从项目文件以在创建 NuGet 包时使用的输入。</span><span class="sxs-lookup"><span data-stu-id="eff7d-116">For .NET Standard projects using the PackageReference format, using `msbuild /t:pack` draws inputs from the project file to use in creating a NuGet package.</span></span>

<span data-ttu-id="eff7d-117">下表描述了可以添加到项目文件第一个 `<PropertyGroup>` 节点中的 MSBuild 属性。</span><span class="sxs-lookup"><span data-stu-id="eff7d-117">The table below describes the MSBuild properties that can be added to a project file within the first `<PropertyGroup>` node.</span></span> <span data-ttu-id="eff7d-118">在 Visual Studio 2017 及更高版本中，通过右键单击项目并选择上下文菜单上的“编辑 {project_name}”，即可轻松进行这些编辑。</span><span class="sxs-lookup"><span data-stu-id="eff7d-118">You can make these edits easily in Visual Studio 2017 and later by right-clicking the project and selecting **Edit {project_name}** on the context menu.</span></span> <span data-ttu-id="eff7d-119">为方便起见，表由 [`.nuspec` 文件](../reference/nuspec.md)中的等效属性组织。</span><span class="sxs-lookup"><span data-stu-id="eff7d-119">For convenience the table is organized by the equivalent property in a [`.nuspec` file](../reference/nuspec.md).</span></span>

<span data-ttu-id="eff7d-120">请注意，`.nuspec` 的 `Owners` 和 `Summary` 属性不受 MSBuild 支持。</span><span class="sxs-lookup"><span data-stu-id="eff7d-120">Note that the `Owners` and `Summary` properties from `.nuspec` are not supported with MSBuild.</span></span>

| <span data-ttu-id="eff7d-121">属性/NuSpec 值</span><span class="sxs-lookup"><span data-stu-id="eff7d-121">Attribute/NuSpec Value</span></span> | <span data-ttu-id="eff7d-122">MSBuild 属性</span><span class="sxs-lookup"><span data-stu-id="eff7d-122">MSBuild Property</span></span> | <span data-ttu-id="eff7d-123">默认</span><span class="sxs-lookup"><span data-stu-id="eff7d-123">Default</span></span> | <span data-ttu-id="eff7d-124">说明</span><span class="sxs-lookup"><span data-stu-id="eff7d-124">Notes</span></span> |
|--------|--------|--------|--------|
| <span data-ttu-id="eff7d-125">Id</span><span class="sxs-lookup"><span data-stu-id="eff7d-125">Id</span></span> | <span data-ttu-id="eff7d-126">PackageId</span><span class="sxs-lookup"><span data-stu-id="eff7d-126">PackageId</span></span> | <span data-ttu-id="eff7d-127">AssemblyName</span><span class="sxs-lookup"><span data-stu-id="eff7d-127">AssemblyName</span></span> | <span data-ttu-id="eff7d-128">MSBuild 的 $(AssemblyName)</span><span class="sxs-lookup"><span data-stu-id="eff7d-128">$(AssemblyName) from MSBuild</span></span> |
| <span data-ttu-id="eff7d-129">版本</span><span class="sxs-lookup"><span data-stu-id="eff7d-129">Version</span></span> | <span data-ttu-id="eff7d-130">PackageVersion</span><span class="sxs-lookup"><span data-stu-id="eff7d-130">PackageVersion</span></span> | <span data-ttu-id="eff7d-131">版本</span><span class="sxs-lookup"><span data-stu-id="eff7d-131">Version</span></span> | <span data-ttu-id="eff7d-132">这与 SemVer 兼容，例如，“1.0.0”、“1.0.0-beta”或“1.0.0-beta-00345”</span><span class="sxs-lookup"><span data-stu-id="eff7d-132">This is semver compatible, for example “1.0.0”, “1.0.0-beta”, or “1.0.0-beta-00345”</span></span> |
| <span data-ttu-id="eff7d-133">VersionPrefix</span><span class="sxs-lookup"><span data-stu-id="eff7d-133">VersionPrefix</span></span> | <span data-ttu-id="eff7d-134">PackageVersionPrefix</span><span class="sxs-lookup"><span data-stu-id="eff7d-134">PackageVersionPrefix</span></span> | <span data-ttu-id="eff7d-135">空</span><span class="sxs-lookup"><span data-stu-id="eff7d-135">empty</span></span> | <span data-ttu-id="eff7d-136">设置 PackageVersion 会覆盖 PackageVersionPrefix</span><span class="sxs-lookup"><span data-stu-id="eff7d-136">Setting PackageVersion overwrites PackageVersionPrefix</span></span> |
| <span data-ttu-id="eff7d-137">VersionSuffix</span><span class="sxs-lookup"><span data-stu-id="eff7d-137">VersionSuffix</span></span> | <span data-ttu-id="eff7d-138">PackageVersionSuffix</span><span class="sxs-lookup"><span data-stu-id="eff7d-138">PackageVersionSuffix</span></span> | <span data-ttu-id="eff7d-139">空</span><span class="sxs-lookup"><span data-stu-id="eff7d-139">empty</span></span> | <span data-ttu-id="eff7d-140">MSBuild 的 $(VersionSuffix)。</span><span class="sxs-lookup"><span data-stu-id="eff7d-140">$(VersionSuffix) from MSBuild.</span></span> <span data-ttu-id="eff7d-141">设置 PackageVersion 会覆盖 PackageVersionSuffix</span><span class="sxs-lookup"><span data-stu-id="eff7d-141">Setting PackageVersion overwrites PackageVersionSuffix</span></span> |
| <span data-ttu-id="eff7d-142">作者</span><span class="sxs-lookup"><span data-stu-id="eff7d-142">Authors</span></span> | <span data-ttu-id="eff7d-143">作者</span><span class="sxs-lookup"><span data-stu-id="eff7d-143">Authors</span></span> | <span data-ttu-id="eff7d-144">当前用户的用户名</span><span class="sxs-lookup"><span data-stu-id="eff7d-144">Username of the current user</span></span> | |
| <span data-ttu-id="eff7d-145">Owners</span><span class="sxs-lookup"><span data-stu-id="eff7d-145">Owners</span></span> | <span data-ttu-id="eff7d-146">不可用</span><span class="sxs-lookup"><span data-stu-id="eff7d-146">N/A</span></span> | <span data-ttu-id="eff7d-147">NuSpec 中不存在</span><span class="sxs-lookup"><span data-stu-id="eff7d-147">Not present in NuSpec</span></span> | |
| <span data-ttu-id="eff7d-148">标题</span><span class="sxs-lookup"><span data-stu-id="eff7d-148">Title</span></span> | <span data-ttu-id="eff7d-149">标题</span><span class="sxs-lookup"><span data-stu-id="eff7d-149">Title</span></span> | <span data-ttu-id="eff7d-150">PackageId</span><span class="sxs-lookup"><span data-stu-id="eff7d-150">The PackageId</span></span>| |
| <span data-ttu-id="eff7d-151">描述</span><span class="sxs-lookup"><span data-stu-id="eff7d-151">Description</span></span> | <span data-ttu-id="eff7d-152">PackageDescription</span><span class="sxs-lookup"><span data-stu-id="eff7d-152">PackageDescription</span></span> | <span data-ttu-id="eff7d-153">“包描述”</span><span class="sxs-lookup"><span data-stu-id="eff7d-153">"Package Description"</span></span> | |
| <span data-ttu-id="eff7d-154">Copyright</span><span class="sxs-lookup"><span data-stu-id="eff7d-154">Copyright</span></span> | <span data-ttu-id="eff7d-155">Copyright</span><span class="sxs-lookup"><span data-stu-id="eff7d-155">Copyright</span></span> | <span data-ttu-id="eff7d-156">空</span><span class="sxs-lookup"><span data-stu-id="eff7d-156">empty</span></span> | |
| <span data-ttu-id="eff7d-157">requireLicenseAcceptance</span><span class="sxs-lookup"><span data-stu-id="eff7d-157">RequireLicenseAcceptance</span></span> | <span data-ttu-id="eff7d-158">PackageRequireLicenseAcceptance</span><span class="sxs-lookup"><span data-stu-id="eff7d-158">PackageRequireLicenseAcceptance</span></span> | <span data-ttu-id="eff7d-159">False</span><span class="sxs-lookup"><span data-stu-id="eff7d-159">false</span></span> | |
| <span data-ttu-id="eff7d-160">LicenseUrl</span><span class="sxs-lookup"><span data-stu-id="eff7d-160">LicenseUrl</span></span> | <span data-ttu-id="eff7d-161">PackageLicenseUrl</span><span class="sxs-lookup"><span data-stu-id="eff7d-161">PackageLicenseUrl</span></span> | <span data-ttu-id="eff7d-162">空</span><span class="sxs-lookup"><span data-stu-id="eff7d-162">empty</span></span> | |
| <span data-ttu-id="eff7d-163">ProjectUrl</span><span class="sxs-lookup"><span data-stu-id="eff7d-163">ProjectUrl</span></span> | <span data-ttu-id="eff7d-164">PackageProjectUrl</span><span class="sxs-lookup"><span data-stu-id="eff7d-164">PackageProjectUrl</span></span> | <span data-ttu-id="eff7d-165">空</span><span class="sxs-lookup"><span data-stu-id="eff7d-165">empty</span></span> | |
| <span data-ttu-id="eff7d-166">IconUrl</span><span class="sxs-lookup"><span data-stu-id="eff7d-166">IconUrl</span></span> | <span data-ttu-id="eff7d-167">PackageIconUrl</span><span class="sxs-lookup"><span data-stu-id="eff7d-167">PackageIconUrl</span></span> | <span data-ttu-id="eff7d-168">空</span><span class="sxs-lookup"><span data-stu-id="eff7d-168">empty</span></span> | |
| <span data-ttu-id="eff7d-169">Tags</span><span class="sxs-lookup"><span data-stu-id="eff7d-169">Tags</span></span> | <span data-ttu-id="eff7d-170">PackageTags</span><span class="sxs-lookup"><span data-stu-id="eff7d-170">PackageTags</span></span> | <span data-ttu-id="eff7d-171">空</span><span class="sxs-lookup"><span data-stu-id="eff7d-171">empty</span></span> | <span data-ttu-id="eff7d-172">使用分号分隔标记。</span><span class="sxs-lookup"><span data-stu-id="eff7d-172">Tags are semi-colon delimited.</span></span> |
| <span data-ttu-id="eff7d-173">ReleaseNotes</span><span class="sxs-lookup"><span data-stu-id="eff7d-173">ReleaseNotes</span></span> | <span data-ttu-id="eff7d-174">PackageReleaseNotes</span><span class="sxs-lookup"><span data-stu-id="eff7d-174">PackageReleaseNotes</span></span> | <span data-ttu-id="eff7d-175">空</span><span class="sxs-lookup"><span data-stu-id="eff7d-175">empty</span></span> | |
| <span data-ttu-id="eff7d-176">存储库/Url</span><span class="sxs-lookup"><span data-stu-id="eff7d-176">Repository/Url</span></span> | <span data-ttu-id="eff7d-177">RepositoryUrl</span><span class="sxs-lookup"><span data-stu-id="eff7d-177">RepositoryUrl</span></span> | <span data-ttu-id="eff7d-178">空</span><span class="sxs-lookup"><span data-stu-id="eff7d-178">empty</span></span> | <span data-ttu-id="eff7d-179">用于克隆或检索源代码存储库 URL。</span><span class="sxs-lookup"><span data-stu-id="eff7d-179">Repository URL used to clone or retrieve source code.</span></span> <span data-ttu-id="eff7d-180">示例： *https://github.com/NuGet/NuGet.Client.git*</span><span class="sxs-lookup"><span data-stu-id="eff7d-180">Example: *https://github.com/NuGet/NuGet.Client.git*</span></span> |
| <span data-ttu-id="eff7d-181">存储库/类型</span><span class="sxs-lookup"><span data-stu-id="eff7d-181">Repository/Type</span></span> | <span data-ttu-id="eff7d-182">RepositoryType</span><span class="sxs-lookup"><span data-stu-id="eff7d-182">RepositoryType</span></span> | <span data-ttu-id="eff7d-183">空</span><span class="sxs-lookup"><span data-stu-id="eff7d-183">empty</span></span> | <span data-ttu-id="eff7d-184">存储库类型。</span><span class="sxs-lookup"><span data-stu-id="eff7d-184">Repository type.</span></span> <span data-ttu-id="eff7d-185">示例： *git*， *tfs*。</span><span class="sxs-lookup"><span data-stu-id="eff7d-185">Examples: *git*, *tfs*.</span></span> |
| <span data-ttu-id="eff7d-186">存储库/分支</span><span class="sxs-lookup"><span data-stu-id="eff7d-186">Repository/Branch</span></span> | <span data-ttu-id="eff7d-187">RepositoryBranch</span><span class="sxs-lookup"><span data-stu-id="eff7d-187">RepositoryBranch</span></span> | <span data-ttu-id="eff7d-188">空</span><span class="sxs-lookup"><span data-stu-id="eff7d-188">empty</span></span> | <span data-ttu-id="eff7d-189">可选存储库分支信息。</span><span class="sxs-lookup"><span data-stu-id="eff7d-189">Optional repository branch information.</span></span> <span data-ttu-id="eff7d-190">*RepositoryUrl*还必须指定要包含此属性。</span><span class="sxs-lookup"><span data-stu-id="eff7d-190">*RepositoryUrl* must also be specified for this property to be included.</span></span> <span data-ttu-id="eff7d-191">示例： *master* (NuGet 4.7.0+)</span><span class="sxs-lookup"><span data-stu-id="eff7d-191">Example: *master* (NuGet 4.7.0+)</span></span> |
| <span data-ttu-id="eff7d-192">存储库/提交</span><span class="sxs-lookup"><span data-stu-id="eff7d-192">Repository/Commit</span></span> | <span data-ttu-id="eff7d-193">RepositoryCommit</span><span class="sxs-lookup"><span data-stu-id="eff7d-193">RepositoryCommit</span></span> | <span data-ttu-id="eff7d-194">空</span><span class="sxs-lookup"><span data-stu-id="eff7d-194">empty</span></span> | <span data-ttu-id="eff7d-195">针对构建的可选的存储库提交或变更集以指示哪些源包。</span><span class="sxs-lookup"><span data-stu-id="eff7d-195">Optional repository commit or changeset to indicate which source the package was built against.</span></span> <span data-ttu-id="eff7d-196">*RepositoryUrl*还必须指定要包含此属性。</span><span class="sxs-lookup"><span data-stu-id="eff7d-196">*RepositoryUrl* must also be specified for this property to be included.</span></span> <span data-ttu-id="eff7d-197">示例： *0e4d1b598f350b3dc675018d539114d1328189ef* (NuGet 4.7.0+)</span><span class="sxs-lookup"><span data-stu-id="eff7d-197">Example: *0e4d1b598f350b3dc675018d539114d1328189ef* (NuGet 4.7.0+)</span></span> |
| <span data-ttu-id="eff7d-198">PackageType</span><span class="sxs-lookup"><span data-stu-id="eff7d-198">PackageType</span></span> | `<PackageType>DotNetCliTool, 1.0.0.0;Dependency, 2.0.0.0</PackageType>` | | |
| <span data-ttu-id="eff7d-199">总结</span><span class="sxs-lookup"><span data-stu-id="eff7d-199">Summary</span></span> | <span data-ttu-id="eff7d-200">不支持</span><span class="sxs-lookup"><span data-stu-id="eff7d-200">Not supported</span></span> | | |

### <a name="pack-target-inputs"></a><span data-ttu-id="eff7d-201">包目标输入</span><span class="sxs-lookup"><span data-stu-id="eff7d-201">pack target inputs</span></span>

- <span data-ttu-id="eff7d-202">IsPackable</span><span class="sxs-lookup"><span data-stu-id="eff7d-202">IsPackable</span></span>
- <span data-ttu-id="eff7d-203">PackageVersion</span><span class="sxs-lookup"><span data-stu-id="eff7d-203">PackageVersion</span></span>
- <span data-ttu-id="eff7d-204">PackageId</span><span class="sxs-lookup"><span data-stu-id="eff7d-204">PackageId</span></span>
- <span data-ttu-id="eff7d-205">作者</span><span class="sxs-lookup"><span data-stu-id="eff7d-205">Authors</span></span>
- <span data-ttu-id="eff7d-206">描述</span><span class="sxs-lookup"><span data-stu-id="eff7d-206">Description</span></span>
- <span data-ttu-id="eff7d-207">Copyright</span><span class="sxs-lookup"><span data-stu-id="eff7d-207">Copyright</span></span>
- <span data-ttu-id="eff7d-208">PackageRequireLicenseAcceptance</span><span class="sxs-lookup"><span data-stu-id="eff7d-208">PackageRequireLicenseAcceptance</span></span>
- <span data-ttu-id="eff7d-209">DevelopmentDependency</span><span class="sxs-lookup"><span data-stu-id="eff7d-209">DevelopmentDependency</span></span>
- <span data-ttu-id="eff7d-210">PackageLicenseUrl</span><span class="sxs-lookup"><span data-stu-id="eff7d-210">PackageLicenseUrl</span></span>
- <span data-ttu-id="eff7d-211">PackageProjectUrl</span><span class="sxs-lookup"><span data-stu-id="eff7d-211">PackageProjectUrl</span></span>
- <span data-ttu-id="eff7d-212">PackageIconUrl</span><span class="sxs-lookup"><span data-stu-id="eff7d-212">PackageIconUrl</span></span>
- <span data-ttu-id="eff7d-213">PackageReleaseNotes</span><span class="sxs-lookup"><span data-stu-id="eff7d-213">PackageReleaseNotes</span></span>
- <span data-ttu-id="eff7d-214">PackageTags</span><span class="sxs-lookup"><span data-stu-id="eff7d-214">PackageTags</span></span>
- <span data-ttu-id="eff7d-215">PackageOutputPath</span><span class="sxs-lookup"><span data-stu-id="eff7d-215">PackageOutputPath</span></span>
- <span data-ttu-id="eff7d-216">IncludeSymbols</span><span class="sxs-lookup"><span data-stu-id="eff7d-216">IncludeSymbols</span></span>
- <span data-ttu-id="eff7d-217">IncludeSource</span><span class="sxs-lookup"><span data-stu-id="eff7d-217">IncludeSource</span></span>
- <span data-ttu-id="eff7d-218">PackageTypes</span><span class="sxs-lookup"><span data-stu-id="eff7d-218">PackageTypes</span></span>
- <span data-ttu-id="eff7d-219">IsTool</span><span class="sxs-lookup"><span data-stu-id="eff7d-219">IsTool</span></span>
- <span data-ttu-id="eff7d-220">RepositoryUrl</span><span class="sxs-lookup"><span data-stu-id="eff7d-220">RepositoryUrl</span></span>
- <span data-ttu-id="eff7d-221">RepositoryType</span><span class="sxs-lookup"><span data-stu-id="eff7d-221">RepositoryType</span></span>
- <span data-ttu-id="eff7d-222">RepositoryBranch</span><span class="sxs-lookup"><span data-stu-id="eff7d-222">RepositoryBranch</span></span>
- <span data-ttu-id="eff7d-223">RepositoryCommit</span><span class="sxs-lookup"><span data-stu-id="eff7d-223">RepositoryCommit</span></span>
- <span data-ttu-id="eff7d-224">NoPackageAnalysis</span><span class="sxs-lookup"><span data-stu-id="eff7d-224">NoPackageAnalysis</span></span>
- <span data-ttu-id="eff7d-225">MinClientVersion</span><span class="sxs-lookup"><span data-stu-id="eff7d-225">MinClientVersion</span></span>
- <span data-ttu-id="eff7d-226">IncludeBuildOutput</span><span class="sxs-lookup"><span data-stu-id="eff7d-226">IncludeBuildOutput</span></span>
- <span data-ttu-id="eff7d-227">IncludeContentInPack</span><span class="sxs-lookup"><span data-stu-id="eff7d-227">IncludeContentInPack</span></span>
- <span data-ttu-id="eff7d-228">BuildOutputTargetFolder</span><span class="sxs-lookup"><span data-stu-id="eff7d-228">BuildOutputTargetFolder</span></span>
- <span data-ttu-id="eff7d-229">ContentTargetFolders</span><span class="sxs-lookup"><span data-stu-id="eff7d-229">ContentTargetFolders</span></span>
- <span data-ttu-id="eff7d-230">NuspecFile</span><span class="sxs-lookup"><span data-stu-id="eff7d-230">NuspecFile</span></span>
- <span data-ttu-id="eff7d-231">NuspecBasePath</span><span class="sxs-lookup"><span data-stu-id="eff7d-231">NuspecBasePath</span></span>
- <span data-ttu-id="eff7d-232">NuspecProperties</span><span class="sxs-lookup"><span data-stu-id="eff7d-232">NuspecProperties</span></span>

## <a name="pack-scenarios"></a><span data-ttu-id="eff7d-233">包方案</span><span class="sxs-lookup"><span data-stu-id="eff7d-233">pack scenarios</span></span>

### <a name="packageiconurl"></a><span data-ttu-id="eff7d-234">PackageIconUrl</span><span class="sxs-lookup"><span data-stu-id="eff7d-234">PackageIconUrl</span></span>

<span data-ttu-id="eff7d-235">更改的一部分[NuGet 问题 352](https://github.com/NuGet/Home/issues/352)，`PackageIconUrl`最终将更改为`PackageIconUri`和可以是到图标文件，它将包括在得到的包的根目录的相对路径。</span><span class="sxs-lookup"><span data-stu-id="eff7d-235">As part of the change for [NuGet Issue 352](https://github.com/NuGet/Home/issues/352), `PackageIconUrl` will eventually be changed to `PackageIconUri` and can be relative path to a icon file which will included at the root of the resulting package.</span></span>

### <a name="output-assemblies"></a><span data-ttu-id="eff7d-236">输出程序集</span><span class="sxs-lookup"><span data-stu-id="eff7d-236">Output assemblies</span></span>

<span data-ttu-id="eff7d-237">`nuget pack` 会复制扩展名为 `.exe`、`.dll`、`.xml`、`.winmd`、`.json` 和 `.pri` 的输出文件。</span><span class="sxs-lookup"><span data-stu-id="eff7d-237">`nuget pack` copies output files with extensions `.exe`, `.dll`, `.xml`, `.winmd`, `.json`, and `.pri`.</span></span> <span data-ttu-id="eff7d-238">复制的输出文件取决于 MSBuild 从 `BuiltOutputProjectGroup` 目标提供的内容。</span><span class="sxs-lookup"><span data-stu-id="eff7d-238">The output files that are copied depend on what MSBuild provides from the `BuiltOutputProjectGroup` target.</span></span>

<span data-ttu-id="eff7d-239">在项目文件或命令行中，有两种 MSBuild 属性可用于控制输出程序集的位置：</span><span class="sxs-lookup"><span data-stu-id="eff7d-239">There are two MSBuild  properties that you can use in your project file or command line to control where output assemblies go:</span></span>

- <span data-ttu-id="eff7d-240">`IncludeBuildOutput`：确定包中是否应包括生成输出程序集的布尔值。</span><span class="sxs-lookup"><span data-stu-id="eff7d-240">`IncludeBuildOutput`: A boolean that determines whether the build output assemblies should be included in the package.</span></span>
- <span data-ttu-id="eff7d-241">`BuildOutputTargetFolder`：指定应放置输出程序集的文件夹。</span><span class="sxs-lookup"><span data-stu-id="eff7d-241">`BuildOutputTargetFolder`: Specifies the folder in which the output assemblies should be placed.</span></span> <span data-ttu-id="eff7d-242">输出程序集（和其他输出文件）会复制到各自的框架文件夹中。</span><span class="sxs-lookup"><span data-stu-id="eff7d-242">The output assemblies (and other output files) are copied into their respective framework folders.</span></span>

### <a name="package-references"></a><span data-ttu-id="eff7d-243">包引用</span><span class="sxs-lookup"><span data-stu-id="eff7d-243">Package references</span></span>

<span data-ttu-id="eff7d-244">请参阅[项目文件中的包引用](../consume-packages/package-references-in-project-files.md)</span><span class="sxs-lookup"><span data-stu-id="eff7d-244">See [Package References in Project Files](../consume-packages/package-references-in-project-files.md).</span></span>

### <a name="project-to-project-references"></a><span data-ttu-id="eff7d-245">项目到项目的引用</span><span class="sxs-lookup"><span data-stu-id="eff7d-245">Project to project references</span></span>

<span data-ttu-id="eff7d-246">默认情况下，项目到项目的引用被视为 nuget 包引用，例如：</span><span class="sxs-lookup"><span data-stu-id="eff7d-246">Project to project references are considered by default as nuget package references, for example:</span></span>

```xml
<ProjectReference Include="..\UwpLibrary2\UwpLibrary2.csproj"/>
```

<span data-ttu-id="eff7d-247">也可将以下元数据添加到项目引用：</span><span class="sxs-lookup"><span data-stu-id="eff7d-247">You can also add the following metadata to your project reference:</span></span>

```xml
<IncludeAssets>
<ExcludeAssets>
<PrivateAssets>
```

### <a name="including-content-in-a-package"></a><span data-ttu-id="eff7d-248">在包中添加内容</span><span class="sxs-lookup"><span data-stu-id="eff7d-248">Including content in a package</span></span>

<span data-ttu-id="eff7d-249">若要添加内容，请将额外的元数据添加到现有的 `<Content>` 项。</span><span class="sxs-lookup"><span data-stu-id="eff7d-249">To include content, add extra metadata to the existing `<Content>` item.</span></span> <span data-ttu-id="eff7d-250">默认情况下，类型“Content”的所有内容都包括在包中，除非使用以下条目替代：</span><span class="sxs-lookup"><span data-stu-id="eff7d-250">By default everything of type "Content" gets included in the package unless you override with entries like the following:</span></span>

 ```xml
    <Content Include="..\win7-x64\libuv.txt">
        <Pack>false</Pack>
    </Content>
 ```

<span data-ttu-id="eff7d-251">默认情况下，所有内容都添加到包中 `content` 和 `contentFiles\any\<target_framework>` 文件夹根目录，并保留相对文件夹结构，除非指定包路径：</span><span class="sxs-lookup"><span data-stu-id="eff7d-251">By default, everything gets added to the root of the `content` and `contentFiles\any\<target_framework>` folder within a package and preserves the relative folder structure, unless you specify a package path:</span></span>

```xml
<Content Include="..\win7-x64\libuv.txt">
    <Pack>true</Pack>
    <PackagePath>content\myfiles\</PackagePath>
</Content>
```

<span data-ttu-id="eff7d-252">如果仅希望将所有内容都复制到特定根文件夹（而不是 `content` 和 `contentFiles`），可使用 MSBuild 属性 `ContentTargetFolders`，其默认值为“content;contentFiles”，但可以设置为任何其他文件夹名称。</span><span class="sxs-lookup"><span data-stu-id="eff7d-252">If you want to copy all your content to only a specific root folder(s) (instead of `content` and `contentFiles` both), you can use the MSBuild property `ContentTargetFolders`, which defaults to "content;contentFiles" but can be set to any other folder names.</span></span> <span data-ttu-id="eff7d-253">请注意，基于 `buildAction`，仅在 `ContentTargetFolders` 中指定“contentFiles”会将文件置于 `contentFiles\any\<target_framework>` 或 `contentFiles\<language>\<target_framework>` 下。</span><span class="sxs-lookup"><span data-stu-id="eff7d-253">Note that just specifying "contentFiles" in `ContentTargetFolders` puts files under `contentFiles\any\<target_framework>` or `contentFiles\<language>\<target_framework>` based on `buildAction`.</span></span>

<span data-ttu-id="eff7d-254">`PackagePath` 可以是一组以分号分隔的目标路径。</span><span class="sxs-lookup"><span data-stu-id="eff7d-254">`PackagePath` can be a semicolon-delimited set of target paths.</span></span> <span data-ttu-id="eff7d-255">指定空的包路径会将文件添加到包的根目录。</span><span class="sxs-lookup"><span data-stu-id="eff7d-255">Specifying an empty package path would add the file to the root of the package.</span></span> <span data-ttu-id="eff7d-256">例如，以下操作会将 `libuv.txt` 添加到 `content\myfiles`、`content\samples` 和包的根目录：</span><span class="sxs-lookup"><span data-stu-id="eff7d-256">For example, the following adds `libuv.txt` to `content\myfiles`, `content\samples`, and the package root:</span></span>

```xml
<Content Include="..\win7-x64\libuv.txt">
    <Pack>true</Pack>
    <PackagePath>content\myfiles;content\sample;;</PackagePath>
</Content>
```

<span data-ttu-id="eff7d-257">另外还有 MSBuild 属性 `$(IncludeContentInPack)`，默认值为 `true`。</span><span class="sxs-lookup"><span data-stu-id="eff7d-257">There is also an MSBuild property `$(IncludeContentInPack)`, which defaults to `true`.</span></span> <span data-ttu-id="eff7d-258">如果在任何项目中将此值设置为 `false`，则该项目的内容不会包括在 nuget 包中。</span><span class="sxs-lookup"><span data-stu-id="eff7d-258">If this is set to `false` on any project, then the content from that project are not included in the nuget package.</span></span>

<span data-ttu-id="eff7d-259">其他可在任何上述项上设置的特定于包的元数据包括 ```<PackageCopyToOutput>``` 和 ```<PackageFlatten>```，后者在输出 nuspec 中的 ```contentFiles``` 条目上设置 ```CopyToOutput``` 和 ```Flatten``` 值。</span><span class="sxs-lookup"><span data-stu-id="eff7d-259">Other pack specific metadata that you can set on any of the above items includes ```<PackageCopyToOutput>``` and ```<PackageFlatten>``` which sets ```CopyToOutput``` and ```Flatten``` values on the ```contentFiles``` entry in the output nuspec.</span></span>

> [!Note]
> <span data-ttu-id="eff7d-260">除了“Content”项，`<Pack>` 和 `<PackagePath>` 元数据还可以在具有 Compile、EmbeddedResource、ApplicationDefinition、Page、Resource、SplashScreen、DesignData、DesignDataWithDesignTimeCreateableTypes、CodeAnalysisDictionary、AndroidAsset、AndroidResource、BundleResource 或 None 生成操作的文件上进行设置。</span><span class="sxs-lookup"><span data-stu-id="eff7d-260">Apart from Content items, the `<Pack>` and `<PackagePath>` metadata can also be set on files with a build action of Compile, EmbeddedResource, ApplicationDefinition, Page, Resource, SplashScreen, DesignData, DesignDataWithDesignTimeCreateableTypes, CodeAnalysisDictionary, AndroidAsset, AndroidResource, BundleResource or None.</span></span>
>
> <span data-ttu-id="eff7d-261">使用通配模式时，对于将包的文件名追加到包路径，包路径必须以文件夹分隔符结尾，否则包路径将被视为包括文件名的完整路径。</span><span class="sxs-lookup"><span data-stu-id="eff7d-261">For pack to append the filename to your package path when using globbing patterns, your package path must end with the folder separator character, otherwise the package path is treated as the full path including the file name.</span></span>

### <a name="includesymbols"></a><span data-ttu-id="eff7d-262">IncludeSymbols</span><span class="sxs-lookup"><span data-stu-id="eff7d-262">IncludeSymbols</span></span>

<span data-ttu-id="eff7d-263">使用 `MSBuild /t:pack /p:IncludeSymbols=true` 时，相应的 `.pdb` 文件将随其他输出文件（`.dll`、`.exe`、`.winmd`、`.xml`、`.json`、`.pri`）一起复制。</span><span class="sxs-lookup"><span data-stu-id="eff7d-263">When using `MSBuild /t:pack /p:IncludeSymbols=true`, the corresponding `.pdb` files are copied along with other output files (`.dll`, `.exe`, `.winmd`, `.xml`, `.json`, `.pri`).</span></span> <span data-ttu-id="eff7d-264">请注意，设置 `IncludeSymbols=true` 会创建常规包和符号包。</span><span class="sxs-lookup"><span data-stu-id="eff7d-264">Note that setting `IncludeSymbols=true` creates a regular package *and* a symbols package.</span></span>

### <a name="includesource"></a><span data-ttu-id="eff7d-265">IncludeSource</span><span class="sxs-lookup"><span data-stu-id="eff7d-265">IncludeSource</span></span>

<span data-ttu-id="eff7d-266">这与 `IncludeSymbols` 相同，但它还会连同 `.pdb` 文件复制源文件。</span><span class="sxs-lookup"><span data-stu-id="eff7d-266">This is the same as `IncludeSymbols`, except that it copies source files along with `.pdb` files as well.</span></span> <span data-ttu-id="eff7d-267">类型为 `Compile` 的所有文件都会复制到 `src\<ProjectName>\`，并保留生成包中的相对路径文件夹结构。</span><span class="sxs-lookup"><span data-stu-id="eff7d-267">All files of type `Compile` are copied over to `src\<ProjectName>\` preserving the relative path folder structure in the resulting package.</span></span> <span data-ttu-id="eff7d-268">对于将 `TreatAsPackageReference` 设置为 `false` 的任何 `ProjectReference` 的源文件也是如此。</span><span class="sxs-lookup"><span data-stu-id="eff7d-268">The same also happens for source files of any `ProjectReference` which has `TreatAsPackageReference` set to `false`.</span></span>

<span data-ttu-id="eff7d-269">如果类型为 Compile 的文件位于项目文件夹外，则它只添加到了 `src\<ProjectName>\`。</span><span class="sxs-lookup"><span data-stu-id="eff7d-269">If a file of type Compile, is outside the project folder, then it's just added to `src\<ProjectName>\`.</span></span>

### <a name="istool"></a><span data-ttu-id="eff7d-270">IsTool</span><span class="sxs-lookup"><span data-stu-id="eff7d-270">IsTool</span></span>

<span data-ttu-id="eff7d-271">使用 `MSBuild /t:pack /p:IsTool=true` 时，所有输出文件（如[输出程序集](#output-assemblies)方案中所指定）都被复制到 `tools` 文件夹，而不是 `lib` 文件夹。</span><span class="sxs-lookup"><span data-stu-id="eff7d-271">When using `MSBuild /t:pack /p:IsTool=true`, all output files, as specified in the [Output Assemblies](#output-assemblies) scenario, are copied to the `tools` folder instead of the `lib` folder.</span></span> <span data-ttu-id="eff7d-272">请注意，这不同于 `DotNetCliTool`，后者通过在 `.csproj` 文件中设置 `PackageType` 进行指定。</span><span class="sxs-lookup"><span data-stu-id="eff7d-272">Note that this is different from a `DotNetCliTool` which is specified by setting the `PackageType` in `.csproj` file.</span></span>

### <a name="packing-using-a-nuspec"></a><span data-ttu-id="eff7d-273">使用 .nuspec 打包</span><span class="sxs-lookup"><span data-stu-id="eff7d-273">Packing using a .nuspec</span></span>

<span data-ttu-id="eff7d-274">你可以使用`.nuspec`文件打包你的项目，前提是具有一个 SDK 项目文件导入`NuGet.Build.Tasks.Pack.targets`，以便可以执行包任务。</span><span class="sxs-lookup"><span data-stu-id="eff7d-274">You can use a `.nuspec` file to pack your project provided that you have a SDK project file to import `NuGet.Build.Tasks.Pack.targets` so that the pack task can be executed.</span></span> <span data-ttu-id="eff7d-275">你仍需要将项目还原之前可以包 nuspec 文件。</span><span class="sxs-lookup"><span data-stu-id="eff7d-275">You still need to restore the project before you can pack a nuspec file.</span></span> <span data-ttu-id="eff7d-276">项目文件的目标框架是不相关和封装 nuspec 时不使用。</span><span class="sxs-lookup"><span data-stu-id="eff7d-276">The target framework of the project file is irrelevant and not used when packing a nuspec.</span></span> <span data-ttu-id="eff7d-277">以下三个 MSBuild 属性与使用 `.nuspec` 的打包相关：</span><span class="sxs-lookup"><span data-stu-id="eff7d-277">The following three MSBuild properties are relevant to packing using a `.nuspec`:</span></span>

1. <span data-ttu-id="eff7d-278">`NuspecFile`：用于打包的 `.nuspec` 文件的相对或绝对路径。</span><span class="sxs-lookup"><span data-stu-id="eff7d-278">`NuspecFile`: relative or absolute path to the `.nuspec` file being used for packing.</span></span>
1. <span data-ttu-id="eff7d-279">`NuspecProperties`：键=值对的分号分隔列表。</span><span class="sxs-lookup"><span data-stu-id="eff7d-279">`NuspecProperties`: a semicolon-separated list of key=value pairs.</span></span> <span data-ttu-id="eff7d-280">由于 MSBuild 命令行分析工作的方式，必须指定多个属性，如下所示：`/p:NuspecProperties=\"key1=value1;key2=value2\"`。</span><span class="sxs-lookup"><span data-stu-id="eff7d-280">Due to the way MSBuild command-line parsing works, multiple properties must be specified as follows: `/p:NuspecProperties=\"key1=value1;key2=value2\"`.</span></span>  
1. <span data-ttu-id="eff7d-281">`NuspecBasePath`：`.nuspec` 文件的基路径。</span><span class="sxs-lookup"><span data-stu-id="eff7d-281">`NuspecBasePath`: Base path for the `.nuspec` file.</span></span>

<span data-ttu-id="eff7d-282">如果使用 `dotnet.exe` 打包项目，请使用类似于下面的命令：</span><span class="sxs-lookup"><span data-stu-id="eff7d-282">If using `dotnet.exe` to pack your project, use a command like the following:</span></span>

```cli
dotnet pack <path to .csproj file> /p:NuspecFile=<path to nuspec file> /p:NuspecProperties=<> /p:NuspecBasePath=<Base path> 
```

<span data-ttu-id="eff7d-283">如果使用 MSBuild 打包项目，请使用类似于下面的命令：</span><span class="sxs-lookup"><span data-stu-id="eff7d-283">If using MSBuild to pack your project, use a command like the following:</span></span>

```cli
msbuild /t:pack <path to .csproj file> /p:NuspecFile=<path to nuspec file> /p:NuspecProperties=<> /p:NuspecBasePath=<Base path> 
```

<span data-ttu-id="eff7d-284">请注意，封装 nuspec 使用 dotnet.exe 或 msbuild 也会导致到默认情况下生成项目。</span><span class="sxs-lookup"><span data-stu-id="eff7d-284">Please note that packing a nuspec using dotnet.exe or msbuild also leads to building the project by default.</span></span> <span data-ttu-id="eff7d-285">这可以避免通过传递```--no-build```dotnet.exe，等同于设置属性```<NoBuild>true</NoBuild> ```在项目文件中，以及设置```<IncludeBuildOutput>false</IncludeBuildOutput> ```项目文件中</span><span class="sxs-lookup"><span data-stu-id="eff7d-285">This can be avoided by passing ```--no-build``` property to dotnet.exe, which is the equivalent of setting ```<NoBuild>true</NoBuild> ``` in your project file, along with setting ```<IncludeBuildOutput>false</IncludeBuildOutput> ``` in the project file</span></span>

<span data-ttu-id="eff7d-286">是要包 nuspec 文件的 csproj 文件的示例：</span><span class="sxs-lookup"><span data-stu-id="eff7d-286">An example of a csproj file to pack a nuspec file is:</span></span>

```
<Project Sdk="Microsoft.NET.Sdk">
  <PropertyGroup>
    <TargetFramework>netstandard2.0</TargetFramework>
    <NoBuild>true</NoBuild>
    <IncludeBuildOutput>false</IncludeBuildOutput>
    <NuspecFile>PATH_TO_NUSPEC_FILE</NuspecFile>
    <NuspecProperties>add nuspec properties here</NuspecProperties>
    <NuspecBasePath>optional to provide</NuspecBasePath>
  </PropertyGroup>
</Project>
```

### <a name="advanced-extension-points-to-create-customized-package"></a><span data-ttu-id="eff7d-287">高级扩展点，以创建自定义的程序包</span><span class="sxs-lookup"><span data-stu-id="eff7d-287">Advanced extension points to create customized package</span></span>

<span data-ttu-id="eff7d-288">`pack`目标提供了两个扩展点，在内部，目标 framework 特定生成中运行。</span><span class="sxs-lookup"><span data-stu-id="eff7d-288">The `pack` target provides two extension points that run in the inner, target framework specific build.</span></span> <span data-ttu-id="eff7d-289">包括目标框架特定内容和程序集放在一个程序包支持的扩展点：</span><span class="sxs-lookup"><span data-stu-id="eff7d-289">The extension points support including target framework specific content and assemblies into a package:</span></span>

- <span data-ttu-id="eff7d-290">`TargetsForTfmSpecificBuildOutput` 目标： 用于中的文件`lib`文件夹或使用指定的文件夹`BuildOutputTargetFolder`。</span><span class="sxs-lookup"><span data-stu-id="eff7d-290">`TargetsForTfmSpecificBuildOutput` target: Use for files inside the `lib` folder or a folder specified using `BuildOutputTargetFolder`.</span></span>
- <span data-ttu-id="eff7d-291">`TargetsForTfmSpecificContentInPackage` 目标： 用于外部文件`BuildOutputTargetFolder`。</span><span class="sxs-lookup"><span data-stu-id="eff7d-291">`TargetsForTfmSpecificContentInPackage` target: Use for files outside the `BuildOutputTargetFolder`.</span></span>

#### <a name="targetsfortfmspecificbuildoutput"></a><span data-ttu-id="eff7d-292">TargetsForTfmSpecificBuildOutput</span><span class="sxs-lookup"><span data-stu-id="eff7d-292">TargetsForTfmSpecificBuildOutput</span></span>

<span data-ttu-id="eff7d-293">编写自定义的目标和指定的值为`$(TargetsForTfmSpecificBuildOutput)`属性。</span><span class="sxs-lookup"><span data-stu-id="eff7d-293">Write a custom target and specify it as the value of the `$(TargetsForTfmSpecificBuildOutput)` property.</span></span> <span data-ttu-id="eff7d-294">需要转到任何文件`BuildOutputTargetFolder`(默认情况下的为 lib)，目标应将这些文件写入到 ItemGroup`BuildOutputInPackage`并设置以下两个元数据值：</span><span class="sxs-lookup"><span data-stu-id="eff7d-294">For any files that need to go into the `BuildOutputTargetFolder` (lib by default), the target should write those files into the ItemGroup `BuildOutputInPackage` and set the following two metadata values:</span></span>

- <span data-ttu-id="eff7d-295">`FinalOutputPath`: 该文件; 绝对路径如果未提供，标识用于评估源路径。</span><span class="sxs-lookup"><span data-stu-id="eff7d-295">`FinalOutputPath`: The absolute path of the file; if not provided, the Identity is used to evaluate source path.</span></span>
- <span data-ttu-id="eff7d-296">`TargetPath`: （可选) 时该文件必须转到子文件夹内设置`lib\<TargetFramework>`，像在其各自的区域性文件夹下，该转到附属程序集一样。</span><span class="sxs-lookup"><span data-stu-id="eff7d-296">`TargetPath`:  (Optional) Set when the file needs to go into a subfolder within `lib\<TargetFramework>` , like satellite assemblies that go under their respective culture folders.</span></span> <span data-ttu-id="eff7d-297">默认值为文件的名称。</span><span class="sxs-lookup"><span data-stu-id="eff7d-297">Defaults to the name of the file.</span></span>

<span data-ttu-id="eff7d-298">示例:</span><span class="sxs-lookup"><span data-stu-id="eff7d-298">Example:</span></span>

```
<PropertyGroup>
  <TargetsForTfmSpecificBuildOutput>$(TargetsForTfmSpecificBuildOutput);GetMyPackageFiles</TargetsForTfmSpecificBuildOutput>
</PropertyGroup>

<Target Name="GetMyPackageFiles">
  <ItemGroup>
    <BuildOutputInPackage Include="$(OutputPath)cs\$(AssemblyName).resources.dll">
        <TargetPath>cs</TargetPath>
    </BuildOutputInPackage>
  </ItemGroup>
</Target>
```

#### <a name="targetsfortfmspecificcontentinpackage"></a><span data-ttu-id="eff7d-299">TargetsForTfmSpecificContentInPackage</span><span class="sxs-lookup"><span data-stu-id="eff7d-299">TargetsForTfmSpecificContentInPackage</span></span>

<span data-ttu-id="eff7d-300">编写自定义的目标和指定的值为`$(TargetsForTfmSpecificContentInPackage)`属性。</span><span class="sxs-lookup"><span data-stu-id="eff7d-300">Write a custom target and specify it as the value of the `$(TargetsForTfmSpecificContentInPackage)` property.</span></span> <span data-ttu-id="eff7d-301">对于要在包中包含任何文件，目标应写入这些文件 ItemGroup`TfmSpecificPackageFile`并设置以下可选元数据：</span><span class="sxs-lookup"><span data-stu-id="eff7d-301">For any files to include in the package, the target should write those files into the ItemGroup `TfmSpecificPackageFile` and set the following optional metadata:</span></span>

- <span data-ttu-id="eff7d-302">`PackagePath`： 该文件应在包中的输出路径。</span><span class="sxs-lookup"><span data-stu-id="eff7d-302">`PackagePath`: Path where the file should be output in the package.</span></span> <span data-ttu-id="eff7d-303">如果多个文件添加到相同的包路径，NuGet 将发出警告。</span><span class="sxs-lookup"><span data-stu-id="eff7d-303">NuGet issues a warning if more than one file is added to the same package path.</span></span>
- <span data-ttu-id="eff7d-304">`BuildAction`: 生成操作以分配给文件，仅当时才需要的包路径中`contentFiles`文件夹。</span><span class="sxs-lookup"><span data-stu-id="eff7d-304">`BuildAction`: The build action to assign to the file, required only if the package path is in the `contentFiles` folder.</span></span> <span data-ttu-id="eff7d-305">默认值为"None"。</span><span class="sxs-lookup"><span data-stu-id="eff7d-305">Defaults to "None".</span></span>

<span data-ttu-id="eff7d-306">示例：</span><span class="sxs-lookup"><span data-stu-id="eff7d-306">An example:</span></span>
```
<PropertyGroup>
    <TargetsForTfmSpecificContentInPackage>$(TargetsForTfmSpecificContentInPackage);CustomContentTarget</TargetsForTfmSpecificContentInPackage>
</PropertyGroup>

<Target Name=""CustomContentTarget"">
    <ItemGroup>
      <TfmSpecificPackageFile Include=""abc.txt"">
        <PackagePath>mycontent/$(TargetFramework)</PackagePath>
      </TfmSpecificPackageFile>
      <TfmSpecificPackageFile Include=""Extensions/ext.txt"" Condition=""'$(TargetFramework)' == 'net46'"">
        <PackagePath>net46content</PackagePath>
      </TfmSpecificPackageFile>  
    </ItemGroup>
  </Target>  
```

## <a name="restore-target"></a><span data-ttu-id="eff7d-307">还原目标</span><span class="sxs-lookup"><span data-stu-id="eff7d-307">restore target</span></span>

<span data-ttu-id="eff7d-308">`MSBuild /t:restore`（`nuget restore` 和 `dotnet restore` 与 .NET Core 项目一起使用）会还原项目文件中引用的包，如下所示：</span><span class="sxs-lookup"><span data-stu-id="eff7d-308">`MSBuild /t:restore` (which `nuget restore` and `dotnet restore` use with .NET Core projects), restores packages referenced in the project file as follows:</span></span>

1. <span data-ttu-id="eff7d-309">读取所有项目到项目的引用</span><span class="sxs-lookup"><span data-stu-id="eff7d-309">Read all project to project references</span></span>
1. <span data-ttu-id="eff7d-310">读取项目属性以查找中间文件夹和目标框架</span><span class="sxs-lookup"><span data-stu-id="eff7d-310">Read the project properties to find the intermediate folder and target frameworks</span></span>
1. <span data-ttu-id="eff7d-311">将 msbuild 数据传递到 NuGet.Build.Tasks.dll</span><span class="sxs-lookup"><span data-stu-id="eff7d-311">Pass msbuild data to NuGet.Build.Tasks.dll</span></span>
1. <span data-ttu-id="eff7d-312">运行还原</span><span class="sxs-lookup"><span data-stu-id="eff7d-312">Run restore</span></span>
1. <span data-ttu-id="eff7d-313">下载包</span><span class="sxs-lookup"><span data-stu-id="eff7d-313">Download packages</span></span>
1. <span data-ttu-id="eff7d-314">编写资产文件、目标和属性</span><span class="sxs-lookup"><span data-stu-id="eff7d-314">Write assets file, targets, and props</span></span>

<span data-ttu-id="eff7d-315">`restore`目标工作原理**仅**对于使用 PackageReference 格式的项目。</span><span class="sxs-lookup"><span data-stu-id="eff7d-315">The `restore` target works **only** for projects using the PackageReference format.</span></span> <span data-ttu-id="eff7d-316">与其**不**工作的项目使用`packages.config`进行格式设置; 使用[nuget 还原](../tools/cli-ref-restore.md)相反。</span><span class="sxs-lookup"><span data-stu-id="eff7d-316">It does **not** work for projects using the `packages.config` format; use [nuget restore](../tools/cli-ref-restore.md) instead.</span></span>

### <a name="restore-properties"></a><span data-ttu-id="eff7d-317">还原属性</span><span class="sxs-lookup"><span data-stu-id="eff7d-317">Restore properties</span></span>

<span data-ttu-id="eff7d-318">其他的还原设置可能来自项目文件中的 MSBuild 属性。</span><span class="sxs-lookup"><span data-stu-id="eff7d-318">Additional restore settings may come from MSBuild properties in the project file.</span></span> <span data-ttu-id="eff7d-319">还可以从命令行使用 `/p:` 开关设置值（请参阅以下示例）。</span><span class="sxs-lookup"><span data-stu-id="eff7d-319">Values can also be set from the command line using the `/p:` switch (see Examples below).</span></span>

| <span data-ttu-id="eff7d-320">属性</span><span class="sxs-lookup"><span data-stu-id="eff7d-320">Property</span></span> | <span data-ttu-id="eff7d-321">描述</span><span class="sxs-lookup"><span data-stu-id="eff7d-321">Description</span></span> |
|--------|--------|
| <span data-ttu-id="eff7d-322">RestoreSources</span><span class="sxs-lookup"><span data-stu-id="eff7d-322">RestoreSources</span></span> | <span data-ttu-id="eff7d-323">以分号分隔的包源列表。</span><span class="sxs-lookup"><span data-stu-id="eff7d-323">Semicolon-delimited list of package sources.</span></span> |
| <span data-ttu-id="eff7d-324">RestorePackagesPath</span><span class="sxs-lookup"><span data-stu-id="eff7d-324">RestorePackagesPath</span></span> | <span data-ttu-id="eff7d-325">用户包文件夹路径。</span><span class="sxs-lookup"><span data-stu-id="eff7d-325">User packages folder path.</span></span> |
| <span data-ttu-id="eff7d-326">RestoreDisableParallel</span><span class="sxs-lookup"><span data-stu-id="eff7d-326">RestoreDisableParallel</span></span> | <span data-ttu-id="eff7d-327">将下载限制为一次一个。</span><span class="sxs-lookup"><span data-stu-id="eff7d-327">Limit downloads to one at a time.</span></span> |
| <span data-ttu-id="eff7d-328">RestoreConfigFile</span><span class="sxs-lookup"><span data-stu-id="eff7d-328">RestoreConfigFile</span></span> | <span data-ttu-id="eff7d-329">要应用的 `Nuget.Config` 文件的路径。</span><span class="sxs-lookup"><span data-stu-id="eff7d-329">Path to a `Nuget.Config` file to apply.</span></span> |
| <span data-ttu-id="eff7d-330">RestoreNoCache</span><span class="sxs-lookup"><span data-stu-id="eff7d-330">RestoreNoCache</span></span> | <span data-ttu-id="eff7d-331">如果为 true，则避免使用缓存的包。</span><span class="sxs-lookup"><span data-stu-id="eff7d-331">If true, avoids using cached packages.</span></span> <span data-ttu-id="eff7d-332">请参阅[管理全局包和缓存文件夹](../consume-packages/managing-the-global-packages-and-cache-folders.md)。</span><span class="sxs-lookup"><span data-stu-id="eff7d-332">See [Managing the global packages and cache folders](../consume-packages/managing-the-global-packages-and-cache-folders.md).</span></span> |
| <span data-ttu-id="eff7d-333">RestoreIgnoreFailedSources</span><span class="sxs-lookup"><span data-stu-id="eff7d-333">RestoreIgnoreFailedSources</span></span> | <span data-ttu-id="eff7d-334">如果为“true”，则忽略失败或丢失的包源。</span><span class="sxs-lookup"><span data-stu-id="eff7d-334">If true, ignores failing or missing package sources.</span></span> |
| <span data-ttu-id="eff7d-335">RestoreTaskAssemblyFile</span><span class="sxs-lookup"><span data-stu-id="eff7d-335">RestoreTaskAssemblyFile</span></span> | <span data-ttu-id="eff7d-336">`NuGet.Build.Tasks.dll` 的路径。</span><span class="sxs-lookup"><span data-stu-id="eff7d-336">Path to `NuGet.Build.Tasks.dll`.</span></span> |
| <span data-ttu-id="eff7d-337">RestoreGraphProjectInput</span><span class="sxs-lookup"><span data-stu-id="eff7d-337">RestoreGraphProjectInput</span></span> | <span data-ttu-id="eff7d-338">要还原的以分号分隔的项目列表，其中应包含绝对路径。</span><span class="sxs-lookup"><span data-stu-id="eff7d-338">Semicolon-delimited list of projects to restore, which should contain absolute paths.</span></span> |
| <span data-ttu-id="eff7d-339">RestoreOutputPath</span><span class="sxs-lookup"><span data-stu-id="eff7d-339">RestoreOutputPath</span></span> | <span data-ttu-id="eff7d-340">输出文件夹，默认为 `obj` 文件夹。</span><span class="sxs-lookup"><span data-stu-id="eff7d-340">Output folder, defaulting to the `obj` folder.</span></span> |

#### <a name="examples"></a><span data-ttu-id="eff7d-341">示例</span><span class="sxs-lookup"><span data-stu-id="eff7d-341">Examples</span></span>

<span data-ttu-id="eff7d-342">命令行：</span><span class="sxs-lookup"><span data-stu-id="eff7d-342">Command line:</span></span>

```cli
msbuild /t:restore /p:RestoreConfigFile=<path>
```

<span data-ttu-id="eff7d-343">项目文件：</span><span class="sxs-lookup"><span data-stu-id="eff7d-343">Project file:</span></span>

```xml
<PropertyGroup>
    <RestoreIgnoreFailedSource>true</RestoreIgnoreFailedSource>
<PropertyGroup>
```

### <a name="restore-outputs"></a><span data-ttu-id="eff7d-344">还原输出</span><span class="sxs-lookup"><span data-stu-id="eff7d-344">Restore outputs</span></span>

<span data-ttu-id="eff7d-345">还原会在生成 `obj` 文件夹中创建以下文件：</span><span class="sxs-lookup"><span data-stu-id="eff7d-345">Restore creates the following files in the build `obj` folder:</span></span>

| <span data-ttu-id="eff7d-346">文件</span><span class="sxs-lookup"><span data-stu-id="eff7d-346">File</span></span> | <span data-ttu-id="eff7d-347">描述</span><span class="sxs-lookup"><span data-stu-id="eff7d-347">Description</span></span> |
|--------|--------|
| `project.assets.json` | <span data-ttu-id="eff7d-348">包含的所有包引用的依赖项关系图。</span><span class="sxs-lookup"><span data-stu-id="eff7d-348">Contains the dependency graph of all package references.</span></span> |
| `{projectName}.projectFileExtension.nuget.g.props` | <span data-ttu-id="eff7d-349">包中包含的对 MSBuild 属性的引用</span><span class="sxs-lookup"><span data-stu-id="eff7d-349">References to MSBuild props contained in packages</span></span> |
| `{projectName}.projectFileExtension.nuget.g.targets` | <span data-ttu-id="eff7d-350">包中包含的对 MSBuild 目标的引用</span><span class="sxs-lookup"><span data-stu-id="eff7d-350">References to MSBuild targets contained in packages</span></span> |

### <a name="packagetargetfallback"></a><span data-ttu-id="eff7d-351">PackageTargetFallback</span><span class="sxs-lookup"><span data-stu-id="eff7d-351">PackageTargetFallback</span></span>

<span data-ttu-id="eff7d-352">`PackageTargetFallback` 元素可用于指定要在还原包时使用的一组兼容目标。</span><span class="sxs-lookup"><span data-stu-id="eff7d-352">The `PackageTargetFallback` element allows you to specify a set of compatible targets to be used when restoring packages.</span></span> <span data-ttu-id="eff7d-353">旨在允许使用 dotnet [TxM](../reference/target-frameworks.md) 的包与未声明 dotnet TxM 的兼容包结合使用。</span><span class="sxs-lookup"><span data-stu-id="eff7d-353">It's designed to allow packages that use a dotnet [TxM](../reference/target-frameworks.md) to work with compatible packages that don't declare a dotnet TxM.</span></span> <span data-ttu-id="eff7d-354">也就是说，如果项目使用 dotnet TxM，那么所依赖的所有包也必须有 dotnet TxM，除非将 `<PackageTargetFallback>` 添加到项目中，以允许非 dotnet 平台与 dotnet 兼容。</span><span class="sxs-lookup"><span data-stu-id="eff7d-354">That is, if your project uses the dotnet TxM, then all the packages it depends on must also have a dotnet TxM, unless you add the `<PackageTargetFallback>` to your project in order to allow non-dotnet platforms to be compatible with dotnet.</span></span>

<span data-ttu-id="eff7d-355">例如，如果项目使用的是 `netstandard1.6` TxM，且从属包仅包含 `lib/net45/a.dll` 和 `lib/portable-net45+win81/a.dll`，则项目将无法生成。</span><span class="sxs-lookup"><span data-stu-id="eff7d-355">For example, if the project is using the `netstandard1.6` TxM, and a dependent package contains only `lib/net45/a.dll` and `lib/portable-net45+win81/a.dll`, then the project will fail to build.</span></span> <span data-ttu-id="eff7d-356">如果需要的是后一种 DLL，则可以按照如下所示添加 `PackageTargetFallback`，声明 `portable-net45+win81` DLL 是兼容的：</span><span class="sxs-lookup"><span data-stu-id="eff7d-356">If what you want to bring in is the latter DLL, then you can add a `PackageTargetFallback` as follows to say that the `portable-net45+win81` DLL is compatible:</span></span>

```xml
<PackageTargetFallback Condition="'$(TargetFramework)'=='netstandard1.6'">
    portable-net45+win81
</PackageTargetFallback>
```

<span data-ttu-id="eff7d-357">若要声明项目中所有目标的回退，请停止 `Condition` 属性。</span><span class="sxs-lookup"><span data-stu-id="eff7d-357">To declare a fallback for all targets in your project, leave off the `Condition` attribute.</span></span> <span data-ttu-id="eff7d-358">还可以通过包括 `$(PackageTargetFallback)` 扩展任何现有 `PackageTargetFallback`，如下所示：</span><span class="sxs-lookup"><span data-stu-id="eff7d-358">You can also extend any existing `PackageTargetFallback` by including `$(PackageTargetFallback)` as shown here:</span></span>

```xml
<PackageTargetFallback>
    $(PackageTargetFallback);portable-net45+win81
</PackageTargetFallback >
```

### <a name="replacing-one-library-from-a-restore-graph"></a><span data-ttu-id="eff7d-359">从还原图中替换一个库</span><span class="sxs-lookup"><span data-stu-id="eff7d-359">Replacing one library from a restore graph</span></span>

<span data-ttu-id="eff7d-360">如果还原引入了错误的程序集，可以排除包默认选项，并将其替换为自己的选项。</span><span class="sxs-lookup"><span data-stu-id="eff7d-360">If a restore is bringing the wrong assembly, it's possible to exclude that packages default choice, and replace it with your own choice.</span></span> <span data-ttu-id="eff7d-361">首先使用顶级 `PackageReference`，排除所有资产：</span><span class="sxs-lookup"><span data-stu-id="eff7d-361">First with a top level `PackageReference`, exclude all assets:</span></span>

```xml
<PackageReference Include="Newtonsoft.Json" Version="9.0.1">
    <ExcludeAssets>All</ExcludeAssets>
</PackageReference>
```

<span data-ttu-id="eff7d-362">接下来，将自己的引用添加到适当的 DLL 本地副本：</span><span class="sxs-lookup"><span data-stu-id="eff7d-362">Next, add your own reference to the appropriate local copy of the DLL:</span></span>

```xml
<Reference Include="Newtonsoft.Json.dll" />
```
