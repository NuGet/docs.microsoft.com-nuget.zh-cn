---
title: 作为 MSBuild 目标的 NuGet 包和还原
description: NuGet 包和还原可作为 MSBuild 目标直接用于 NuGet 4.0+。
author: karann-msft
ms.author: karann
ms.date: 03/23/2018
ms.topic: conceptual
ms.openlocfilehash: 7b3fc72ddd3ad6c9185c2bd0f2563df59e77f1c8
ms.sourcegitcommit: 0c5a49ec6e0254a4e7a9d8bca7daeefb853c433a
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/28/2018
ms.locfileid: "52453541"
---
# <a name="nuget-pack-and-restore-as-msbuild-targets"></a><span data-ttu-id="e672a-103">作为 MSBuild 目标的 NuGet 包和还原</span><span class="sxs-lookup"><span data-stu-id="e672a-103">NuGet pack and restore as MSBuild targets</span></span>

<span data-ttu-id="e672a-104">NuGet 4.0+</span><span class="sxs-lookup"><span data-stu-id="e672a-104">*NuGet 4.0+*</span></span>

<span data-ttu-id="e672a-105">使用 PackageReference 格式，NuGet 4.0+ 可以将所有清单元数据直接存储在项目文件中，而不是使用单独的 `.nuspec` 文件。</span><span class="sxs-lookup"><span data-stu-id="e672a-105">With the PackageReference format, NuGet 4.0+ can store all manifest metadata directly within a project file rather than using a separate `.nuspec` file.</span></span>

<span data-ttu-id="e672a-106">如下所述，对于 MSBuild 15.1+，NuGet 还是具有 `pack` 目标和 `restore` 目标的一等 MSBuild 公民。</span><span class="sxs-lookup"><span data-stu-id="e672a-106">With MSBuild 15.1+, NuGet is also a first-class MSBuild citizen with the `pack` and `restore` targets as described below.</span></span> <span data-ttu-id="e672a-107">借助这些目标，你可以像使用任何其他 MSBuild 任务或目标一样使用 NuGet。</span><span class="sxs-lookup"><span data-stu-id="e672a-107">These targets allow you to work with NuGet as you would with any other MSBuild task or target.</span></span> <span data-ttu-id="e672a-108">（对于 Nuget 3.x 及更早版本，通过 NuGet CLI 使用 [pack](../tools/cli-ref-pack.md) 和 [restore](../tools/cli-ref-restore.md) 命令。）</span><span class="sxs-lookup"><span data-stu-id="e672a-108">(For NuGet 3.x and earlier, you use the [pack](../tools/cli-ref-pack.md) and [restore](../tools/cli-ref-restore.md) commands through the NuGet CLI instead.)</span></span>

## <a name="target-build-order"></a><span data-ttu-id="e672a-109">目标生成顺序</span><span class="sxs-lookup"><span data-stu-id="e672a-109">Target build order</span></span>

<span data-ttu-id="e672a-110">由于 `pack` 和 `restore` 为 MSBuild 目标，因此可以访问它们以增强工作流。</span><span class="sxs-lookup"><span data-stu-id="e672a-110">Because `pack` and `restore` are  MSBuild targets, you can access them to enhance your workflow.</span></span> <span data-ttu-id="e672a-111">例如，假设希望在打包后将包复制到网络共享。</span><span class="sxs-lookup"><span data-stu-id="e672a-111">For example, let’s say you want to copy your package to a network share after packing it.</span></span> <span data-ttu-id="e672a-112">此操作可通过向项目文件中添加以下内容来完成：</span><span class="sxs-lookup"><span data-stu-id="e672a-112">You can do that by adding the following in your project file:</span></span>

```xml
<Target Name="CopyPackage" AfterTargets="Pack">
  <Copy
    SourceFiles="$(OutputPath)..\$(PackageId).$(PackageVersion).nupkg"
    DestinationFolder="\\myshare\packageshare\"
    />
</Target>
```

<span data-ttu-id="e672a-113">同样，你可以编写 MSBuild 任务、编写自己的目标并使用 MSBuild 任务中的 NuGet 属性。</span><span class="sxs-lookup"><span data-stu-id="e672a-113">Similarly, you can write an MSBuild task, write your own target and consume NuGet properties in the MSBuild task.</span></span>

## <a name="pack-target"></a><span data-ttu-id="e672a-114">包目标</span><span class="sxs-lookup"><span data-stu-id="e672a-114">pack target</span></span>

<span data-ttu-id="e672a-115">.NET Standard 项目使用 PackageReference 格式，并使用`msbuild -t:pack`绘制从项目文件可用于创建 NuGet 包的输入。</span><span class="sxs-lookup"><span data-stu-id="e672a-115">For .NET Standard projects using the PackageReference format, using `msbuild -t:pack` draws inputs from the project file to use in creating a NuGet package.</span></span>

<span data-ttu-id="e672a-116">下表描述了可以添加到项目文件第一个 `<PropertyGroup>` 节点中的 MSBuild 属性。</span><span class="sxs-lookup"><span data-stu-id="e672a-116">The table below describes the MSBuild properties that can be added to a project file within the first `<PropertyGroup>` node.</span></span> <span data-ttu-id="e672a-117">在 Visual Studio 2017 及更高版本中，通过右键单击项目并选择上下文菜单上的“编辑 {project_name}”，即可轻松进行这些编辑。</span><span class="sxs-lookup"><span data-stu-id="e672a-117">You can make these edits easily in Visual Studio 2017 and later by right-clicking the project and selecting **Edit {project_name}** on the context menu.</span></span> <span data-ttu-id="e672a-118">为方便起见，表由 [`.nuspec` 文件](../reference/nuspec.md)中的等效属性组织。</span><span class="sxs-lookup"><span data-stu-id="e672a-118">For convenience the table is organized by the equivalent property in a [`.nuspec` file](../reference/nuspec.md).</span></span>

<span data-ttu-id="e672a-119">请注意，`.nuspec` 的 `Owners` 和 `Summary` 属性不受 MSBuild 支持。</span><span class="sxs-lookup"><span data-stu-id="e672a-119">Note that the `Owners` and `Summary` properties from `.nuspec` are not supported with MSBuild.</span></span>

| <span data-ttu-id="e672a-120">属性/NuSpec 值</span><span class="sxs-lookup"><span data-stu-id="e672a-120">Attribute/NuSpec Value</span></span> | <span data-ttu-id="e672a-121">MSBuild 属性</span><span class="sxs-lookup"><span data-stu-id="e672a-121">MSBuild Property</span></span> | <span data-ttu-id="e672a-122">默认</span><span class="sxs-lookup"><span data-stu-id="e672a-122">Default</span></span> | <span data-ttu-id="e672a-123">说明</span><span class="sxs-lookup"><span data-stu-id="e672a-123">Notes</span></span> |
|--------|--------|--------|--------|
| <span data-ttu-id="e672a-124">Id</span><span class="sxs-lookup"><span data-stu-id="e672a-124">Id</span></span> | <span data-ttu-id="e672a-125">PackageId</span><span class="sxs-lookup"><span data-stu-id="e672a-125">PackageId</span></span> | <span data-ttu-id="e672a-126">AssemblyName</span><span class="sxs-lookup"><span data-stu-id="e672a-126">AssemblyName</span></span> | <span data-ttu-id="e672a-127">MSBuild 的 $(AssemblyName)</span><span class="sxs-lookup"><span data-stu-id="e672a-127">$(AssemblyName) from MSBuild</span></span> |
| <span data-ttu-id="e672a-128">版本</span><span class="sxs-lookup"><span data-stu-id="e672a-128">Version</span></span> | <span data-ttu-id="e672a-129">PackageVersion</span><span class="sxs-lookup"><span data-stu-id="e672a-129">PackageVersion</span></span> | <span data-ttu-id="e672a-130">版本</span><span class="sxs-lookup"><span data-stu-id="e672a-130">Version</span></span> | <span data-ttu-id="e672a-131">这与 SemVer 兼容，例如，“1.0.0”、“1.0.0-beta”或“1.0.0-beta-00345”</span><span class="sxs-lookup"><span data-stu-id="e672a-131">This is semver compatible, for example “1.0.0”, “1.0.0-beta”, or “1.0.0-beta-00345”</span></span> |
| <span data-ttu-id="e672a-132">VersionPrefix</span><span class="sxs-lookup"><span data-stu-id="e672a-132">VersionPrefix</span></span> | <span data-ttu-id="e672a-133">PackageVersionPrefix</span><span class="sxs-lookup"><span data-stu-id="e672a-133">PackageVersionPrefix</span></span> | <span data-ttu-id="e672a-134">空</span><span class="sxs-lookup"><span data-stu-id="e672a-134">empty</span></span> | <span data-ttu-id="e672a-135">设置 PackageVersion 会覆盖 PackageVersionPrefix</span><span class="sxs-lookup"><span data-stu-id="e672a-135">Setting PackageVersion overwrites PackageVersionPrefix</span></span> |
| <span data-ttu-id="e672a-136">VersionSuffix</span><span class="sxs-lookup"><span data-stu-id="e672a-136">VersionSuffix</span></span> | <span data-ttu-id="e672a-137">PackageVersionSuffix</span><span class="sxs-lookup"><span data-stu-id="e672a-137">PackageVersionSuffix</span></span> | <span data-ttu-id="e672a-138">空</span><span class="sxs-lookup"><span data-stu-id="e672a-138">empty</span></span> | <span data-ttu-id="e672a-139">MSBuild 的 $(VersionSuffix)。</span><span class="sxs-lookup"><span data-stu-id="e672a-139">$(VersionSuffix) from MSBuild.</span></span> <span data-ttu-id="e672a-140">设置 PackageVersion 会覆盖 PackageVersionSuffix</span><span class="sxs-lookup"><span data-stu-id="e672a-140">Setting PackageVersion overwrites PackageVersionSuffix</span></span> |
| <span data-ttu-id="e672a-141">作者</span><span class="sxs-lookup"><span data-stu-id="e672a-141">Authors</span></span> | <span data-ttu-id="e672a-142">作者</span><span class="sxs-lookup"><span data-stu-id="e672a-142">Authors</span></span> | <span data-ttu-id="e672a-143">当前用户的用户名</span><span class="sxs-lookup"><span data-stu-id="e672a-143">Username of the current user</span></span> | |
| <span data-ttu-id="e672a-144">Owners</span><span class="sxs-lookup"><span data-stu-id="e672a-144">Owners</span></span> | <span data-ttu-id="e672a-145">不可用</span><span class="sxs-lookup"><span data-stu-id="e672a-145">N/A</span></span> | <span data-ttu-id="e672a-146">NuSpec 中不存在</span><span class="sxs-lookup"><span data-stu-id="e672a-146">Not present in NuSpec</span></span> | |
| <span data-ttu-id="e672a-147">标题</span><span class="sxs-lookup"><span data-stu-id="e672a-147">Title</span></span> | <span data-ttu-id="e672a-148">标题</span><span class="sxs-lookup"><span data-stu-id="e672a-148">Title</span></span> | <span data-ttu-id="e672a-149">PackageId</span><span class="sxs-lookup"><span data-stu-id="e672a-149">The PackageId</span></span>| |
| <span data-ttu-id="e672a-150">描述</span><span class="sxs-lookup"><span data-stu-id="e672a-150">Description</span></span> | <span data-ttu-id="e672a-151">描述</span><span class="sxs-lookup"><span data-stu-id="e672a-151">Description</span></span> | <span data-ttu-id="e672a-152">“包描述”</span><span class="sxs-lookup"><span data-stu-id="e672a-152">"Package Description"</span></span> | |
| <span data-ttu-id="e672a-153">Copyright</span><span class="sxs-lookup"><span data-stu-id="e672a-153">Copyright</span></span> | <span data-ttu-id="e672a-154">Copyright</span><span class="sxs-lookup"><span data-stu-id="e672a-154">Copyright</span></span> | <span data-ttu-id="e672a-155">空</span><span class="sxs-lookup"><span data-stu-id="e672a-155">empty</span></span> | |
| <span data-ttu-id="e672a-156">requireLicenseAcceptance</span><span class="sxs-lookup"><span data-stu-id="e672a-156">RequireLicenseAcceptance</span></span> | <span data-ttu-id="e672a-157">PackageRequireLicenseAcceptance</span><span class="sxs-lookup"><span data-stu-id="e672a-157">PackageRequireLicenseAcceptance</span></span> | <span data-ttu-id="e672a-158">False</span><span class="sxs-lookup"><span data-stu-id="e672a-158">false</span></span> | |
| <span data-ttu-id="e672a-159">许可证</span><span class="sxs-lookup"><span data-stu-id="e672a-159">license</span></span> | <span data-ttu-id="e672a-160">PackageLicenseExpression</span><span class="sxs-lookup"><span data-stu-id="e672a-160">PackageLicenseExpression</span></span> | <span data-ttu-id="e672a-161">空</span><span class="sxs-lookup"><span data-stu-id="e672a-161">empty</span></span> | <span data-ttu-id="e672a-162">对应于 `<license type="expression">`</span><span class="sxs-lookup"><span data-stu-id="e672a-162">Corresponds to `<license type="expression">`</span></span> |
| <span data-ttu-id="e672a-163">许可证</span><span class="sxs-lookup"><span data-stu-id="e672a-163">license</span></span> | <span data-ttu-id="e672a-164">PackageLicenseFile</span><span class="sxs-lookup"><span data-stu-id="e672a-164">PackageLicenseFile</span></span> | <span data-ttu-id="e672a-165">空</span><span class="sxs-lookup"><span data-stu-id="e672a-165">empty</span></span> | <span data-ttu-id="e672a-166">对应到 `<license type="file">`。</span><span class="sxs-lookup"><span data-stu-id="e672a-166">Corresponds to `<license type="file">`.</span></span> <span data-ttu-id="e672a-167">您可能需要显式包引用的许可证文件。</span><span class="sxs-lookup"><span data-stu-id="e672a-167">You may need to explicitly pack the referenced license file.</span></span> |
| <span data-ttu-id="e672a-168">LicenseUrl</span><span class="sxs-lookup"><span data-stu-id="e672a-168">LicenseUrl</span></span> | <span data-ttu-id="e672a-169">PackageLicenseUrl</span><span class="sxs-lookup"><span data-stu-id="e672a-169">PackageLicenseUrl</span></span> | <span data-ttu-id="e672a-170">空</span><span class="sxs-lookup"><span data-stu-id="e672a-170">empty</span></span> | <span data-ttu-id="e672a-171">`licenseUrl` 已弃用，使用 PackageLicenseExpression 或 PackageLicenseFile 属性</span><span class="sxs-lookup"><span data-stu-id="e672a-171">`licenseUrl` is being deprecated, use the PackageLicenseExpression or PackageLicenseFile property</span></span> |
| <span data-ttu-id="e672a-172">ProjectUrl</span><span class="sxs-lookup"><span data-stu-id="e672a-172">ProjectUrl</span></span> | <span data-ttu-id="e672a-173">PackageProjectUrl</span><span class="sxs-lookup"><span data-stu-id="e672a-173">PackageProjectUrl</span></span> | <span data-ttu-id="e672a-174">空</span><span class="sxs-lookup"><span data-stu-id="e672a-174">empty</span></span> | |
| <span data-ttu-id="e672a-175">IconUrl</span><span class="sxs-lookup"><span data-stu-id="e672a-175">IconUrl</span></span> | <span data-ttu-id="e672a-176">PackageIconUrl</span><span class="sxs-lookup"><span data-stu-id="e672a-176">PackageIconUrl</span></span> | <span data-ttu-id="e672a-177">空</span><span class="sxs-lookup"><span data-stu-id="e672a-177">empty</span></span> | |
| <span data-ttu-id="e672a-178">Tags</span><span class="sxs-lookup"><span data-stu-id="e672a-178">Tags</span></span> | <span data-ttu-id="e672a-179">PackageTags</span><span class="sxs-lookup"><span data-stu-id="e672a-179">PackageTags</span></span> | <span data-ttu-id="e672a-180">空</span><span class="sxs-lookup"><span data-stu-id="e672a-180">empty</span></span> | <span data-ttu-id="e672a-181">使用分号分隔标记。</span><span class="sxs-lookup"><span data-stu-id="e672a-181">Tags are semi-colon delimited.</span></span> |
| <span data-ttu-id="e672a-182">ReleaseNotes</span><span class="sxs-lookup"><span data-stu-id="e672a-182">ReleaseNotes</span></span> | <span data-ttu-id="e672a-183">PackageReleaseNotes</span><span class="sxs-lookup"><span data-stu-id="e672a-183">PackageReleaseNotes</span></span> | <span data-ttu-id="e672a-184">空</span><span class="sxs-lookup"><span data-stu-id="e672a-184">empty</span></span> | |
| <span data-ttu-id="e672a-185">存储库/Url</span><span class="sxs-lookup"><span data-stu-id="e672a-185">Repository/Url</span></span> | <span data-ttu-id="e672a-186">RepositoryUrl</span><span class="sxs-lookup"><span data-stu-id="e672a-186">RepositoryUrl</span></span> | <span data-ttu-id="e672a-187">空</span><span class="sxs-lookup"><span data-stu-id="e672a-187">empty</span></span> | <span data-ttu-id="e672a-188">用来克隆或检索源代码存储库 URL。</span><span class="sxs-lookup"><span data-stu-id="e672a-188">Repository URL used to clone or retrieve source code.</span></span> <span data-ttu-id="e672a-189">示例： *https://github.com/NuGet/NuGet.Client.git*</span><span class="sxs-lookup"><span data-stu-id="e672a-189">Example: *https://github.com/NuGet/NuGet.Client.git*</span></span> |
| <span data-ttu-id="e672a-190">存储库/类型</span><span class="sxs-lookup"><span data-stu-id="e672a-190">Repository/Type</span></span> | <span data-ttu-id="e672a-191">RepositoryType</span><span class="sxs-lookup"><span data-stu-id="e672a-191">RepositoryType</span></span> | <span data-ttu-id="e672a-192">空</span><span class="sxs-lookup"><span data-stu-id="e672a-192">empty</span></span> | <span data-ttu-id="e672a-193">存储库类型。</span><span class="sxs-lookup"><span data-stu-id="e672a-193">Repository type.</span></span> <span data-ttu-id="e672a-194">示例： *git*， *tfs*。</span><span class="sxs-lookup"><span data-stu-id="e672a-194">Examples: *git*, *tfs*.</span></span> |
| <span data-ttu-id="e672a-195">存储库/分支</span><span class="sxs-lookup"><span data-stu-id="e672a-195">Repository/Branch</span></span> | <span data-ttu-id="e672a-196">RepositoryBranch</span><span class="sxs-lookup"><span data-stu-id="e672a-196">RepositoryBranch</span></span> | <span data-ttu-id="e672a-197">空</span><span class="sxs-lookup"><span data-stu-id="e672a-197">empty</span></span> | <span data-ttu-id="e672a-198">可选存储库分支的信息。</span><span class="sxs-lookup"><span data-stu-id="e672a-198">Optional repository branch information.</span></span> <span data-ttu-id="e672a-199">*RepositoryUrl*还必须指定要包含此属性。</span><span class="sxs-lookup"><span data-stu-id="e672a-199">*RepositoryUrl* must also be specified for this property to be included.</span></span> <span data-ttu-id="e672a-200">示例：*主*(NuGet 4.7.0+)</span><span class="sxs-lookup"><span data-stu-id="e672a-200">Example: *master* (NuGet 4.7.0+)</span></span> |
| <span data-ttu-id="e672a-201">存储库/提交</span><span class="sxs-lookup"><span data-stu-id="e672a-201">Repository/Commit</span></span> | <span data-ttu-id="e672a-202">RepositoryCommit</span><span class="sxs-lookup"><span data-stu-id="e672a-202">RepositoryCommit</span></span> | <span data-ttu-id="e672a-203">空</span><span class="sxs-lookup"><span data-stu-id="e672a-203">empty</span></span> | <span data-ttu-id="e672a-204">可选存储库提交或变更集以指示哪些源包已针对构建。</span><span class="sxs-lookup"><span data-stu-id="e672a-204">Optional repository commit or changeset to indicate which source the package was built against.</span></span> <span data-ttu-id="e672a-205">*RepositoryUrl*还必须指定要包含此属性。</span><span class="sxs-lookup"><span data-stu-id="e672a-205">*RepositoryUrl* must also be specified for this property to be included.</span></span> <span data-ttu-id="e672a-206">示例： *0e4d1b598f350b3dc675018d539114d1328189ef* (NuGet 4.7.0+)</span><span class="sxs-lookup"><span data-stu-id="e672a-206">Example: *0e4d1b598f350b3dc675018d539114d1328189ef* (NuGet 4.7.0+)</span></span> |
| <span data-ttu-id="e672a-207">PackageType</span><span class="sxs-lookup"><span data-stu-id="e672a-207">PackageType</span></span> | `<PackageType>DotNetCliTool, 1.0.0.0;Dependency, 2.0.0.0</PackageType>` | | |
| <span data-ttu-id="e672a-208">总结</span><span class="sxs-lookup"><span data-stu-id="e672a-208">Summary</span></span> | <span data-ttu-id="e672a-209">不支持</span><span class="sxs-lookup"><span data-stu-id="e672a-209">Not supported</span></span> | | |

### <a name="pack-target-inputs"></a><span data-ttu-id="e672a-210">包目标输入</span><span class="sxs-lookup"><span data-stu-id="e672a-210">pack target inputs</span></span>

- <span data-ttu-id="e672a-211">IsPackable</span><span class="sxs-lookup"><span data-stu-id="e672a-211">IsPackable</span></span>
- <span data-ttu-id="e672a-212">PackageVersion</span><span class="sxs-lookup"><span data-stu-id="e672a-212">PackageVersion</span></span>
- <span data-ttu-id="e672a-213">PackageId</span><span class="sxs-lookup"><span data-stu-id="e672a-213">PackageId</span></span>
- <span data-ttu-id="e672a-214">作者</span><span class="sxs-lookup"><span data-stu-id="e672a-214">Authors</span></span>
- <span data-ttu-id="e672a-215">描述</span><span class="sxs-lookup"><span data-stu-id="e672a-215">Description</span></span>
- <span data-ttu-id="e672a-216">Copyright</span><span class="sxs-lookup"><span data-stu-id="e672a-216">Copyright</span></span>
- <span data-ttu-id="e672a-217">PackageRequireLicenseAcceptance</span><span class="sxs-lookup"><span data-stu-id="e672a-217">PackageRequireLicenseAcceptance</span></span>
- <span data-ttu-id="e672a-218">DevelopmentDependency</span><span class="sxs-lookup"><span data-stu-id="e672a-218">DevelopmentDependency</span></span>
- <span data-ttu-id="e672a-219">PackageLicenseExpression</span><span class="sxs-lookup"><span data-stu-id="e672a-219">PackageLicenseExpression</span></span>
- <span data-ttu-id="e672a-220">PackageLicenseFile</span><span class="sxs-lookup"><span data-stu-id="e672a-220">PackageLicenseFile</span></span>
- <span data-ttu-id="e672a-221">PackageLicenseUrl</span><span class="sxs-lookup"><span data-stu-id="e672a-221">PackageLicenseUrl</span></span>
- <span data-ttu-id="e672a-222">PackageProjectUrl</span><span class="sxs-lookup"><span data-stu-id="e672a-222">PackageProjectUrl</span></span>
- <span data-ttu-id="e672a-223">PackageIconUrl</span><span class="sxs-lookup"><span data-stu-id="e672a-223">PackageIconUrl</span></span>
- <span data-ttu-id="e672a-224">PackageReleaseNotes</span><span class="sxs-lookup"><span data-stu-id="e672a-224">PackageReleaseNotes</span></span>
- <span data-ttu-id="e672a-225">PackageTags</span><span class="sxs-lookup"><span data-stu-id="e672a-225">PackageTags</span></span>
- <span data-ttu-id="e672a-226">PackageOutputPath</span><span class="sxs-lookup"><span data-stu-id="e672a-226">PackageOutputPath</span></span>
- <span data-ttu-id="e672a-227">IncludeSymbols</span><span class="sxs-lookup"><span data-stu-id="e672a-227">IncludeSymbols</span></span>
- <span data-ttu-id="e672a-228">IncludeSource</span><span class="sxs-lookup"><span data-stu-id="e672a-228">IncludeSource</span></span>
- <span data-ttu-id="e672a-229">PackageTypes</span><span class="sxs-lookup"><span data-stu-id="e672a-229">PackageTypes</span></span>
- <span data-ttu-id="e672a-230">IsTool</span><span class="sxs-lookup"><span data-stu-id="e672a-230">IsTool</span></span>
- <span data-ttu-id="e672a-231">RepositoryUrl</span><span class="sxs-lookup"><span data-stu-id="e672a-231">RepositoryUrl</span></span>
- <span data-ttu-id="e672a-232">RepositoryType</span><span class="sxs-lookup"><span data-stu-id="e672a-232">RepositoryType</span></span>
- <span data-ttu-id="e672a-233">RepositoryBranch</span><span class="sxs-lookup"><span data-stu-id="e672a-233">RepositoryBranch</span></span>
- <span data-ttu-id="e672a-234">RepositoryCommit</span><span class="sxs-lookup"><span data-stu-id="e672a-234">RepositoryCommit</span></span>
- <span data-ttu-id="e672a-235">NoPackageAnalysis</span><span class="sxs-lookup"><span data-stu-id="e672a-235">NoPackageAnalysis</span></span>
- <span data-ttu-id="e672a-236">MinClientVersion</span><span class="sxs-lookup"><span data-stu-id="e672a-236">MinClientVersion</span></span>
- <span data-ttu-id="e672a-237">IncludeBuildOutput</span><span class="sxs-lookup"><span data-stu-id="e672a-237">IncludeBuildOutput</span></span>
- <span data-ttu-id="e672a-238">IncludeContentInPack</span><span class="sxs-lookup"><span data-stu-id="e672a-238">IncludeContentInPack</span></span>
- <span data-ttu-id="e672a-239">BuildOutputTargetFolder</span><span class="sxs-lookup"><span data-stu-id="e672a-239">BuildOutputTargetFolder</span></span>
- <span data-ttu-id="e672a-240">ContentTargetFolders</span><span class="sxs-lookup"><span data-stu-id="e672a-240">ContentTargetFolders</span></span>
- <span data-ttu-id="e672a-241">NuspecFile</span><span class="sxs-lookup"><span data-stu-id="e672a-241">NuspecFile</span></span>
- <span data-ttu-id="e672a-242">NuspecBasePath</span><span class="sxs-lookup"><span data-stu-id="e672a-242">NuspecBasePath</span></span>
- <span data-ttu-id="e672a-243">NuspecProperties</span><span class="sxs-lookup"><span data-stu-id="e672a-243">NuspecProperties</span></span>

## <a name="pack-scenarios"></a><span data-ttu-id="e672a-244">包方案</span><span class="sxs-lookup"><span data-stu-id="e672a-244">pack scenarios</span></span>

### <a name="packageiconurl"></a><span data-ttu-id="e672a-245">PackageIconUrl</span><span class="sxs-lookup"><span data-stu-id="e672a-245">PackageIconUrl</span></span>

<span data-ttu-id="e672a-246">有关更改的一部分[NuGet 问题 352](https://github.com/NuGet/Home/issues/352)，`PackageIconUrl`最终将更改为`PackageIconUri`，可以是相对路径将包含生成的包的根目录下的图标文件。</span><span class="sxs-lookup"><span data-stu-id="e672a-246">As part of the change for [NuGet Issue 352](https://github.com/NuGet/Home/issues/352), `PackageIconUrl` will eventually be changed to `PackageIconUri` and can be relative path to a icon file which will included at the root of the resulting package.</span></span>

### <a name="output-assemblies"></a><span data-ttu-id="e672a-247">输出程序集</span><span class="sxs-lookup"><span data-stu-id="e672a-247">Output assemblies</span></span>

<span data-ttu-id="e672a-248">`nuget pack` 会复制扩展名为 `.exe`、`.dll`、`.xml`、`.winmd`、`.json` 和 `.pri` 的输出文件。</span><span class="sxs-lookup"><span data-stu-id="e672a-248">`nuget pack` copies output files with extensions `.exe`, `.dll`, `.xml`, `.winmd`, `.json`, and `.pri`.</span></span> <span data-ttu-id="e672a-249">复制的输出文件取决于 MSBuild 从 `BuiltOutputProjectGroup` 目标提供的内容。</span><span class="sxs-lookup"><span data-stu-id="e672a-249">The output files that are copied depend on what MSBuild provides from the `BuiltOutputProjectGroup` target.</span></span>

<span data-ttu-id="e672a-250">在项目文件或命令行中，有两种 MSBuild 属性可用于控制输出程序集的位置：</span><span class="sxs-lookup"><span data-stu-id="e672a-250">There are two MSBuild  properties that you can use in your project file or command line to control where output assemblies go:</span></span>

- <span data-ttu-id="e672a-251">`IncludeBuildOutput`：确定包中是否应包括生成输出程序集的布尔值。</span><span class="sxs-lookup"><span data-stu-id="e672a-251">`IncludeBuildOutput`: A boolean that determines whether the build output assemblies should be included in the package.</span></span>
- <span data-ttu-id="e672a-252">`BuildOutputTargetFolder`：指定应放置输出程序集的文件夹。</span><span class="sxs-lookup"><span data-stu-id="e672a-252">`BuildOutputTargetFolder`: Specifies the folder in which the output assemblies should be placed.</span></span> <span data-ttu-id="e672a-253">输出程序集（和其他输出文件）会复制到各自的框架文件夹中。</span><span class="sxs-lookup"><span data-stu-id="e672a-253">The output assemblies (and other output files) are copied into their respective framework folders.</span></span>

### <a name="package-references"></a><span data-ttu-id="e672a-254">包引用</span><span class="sxs-lookup"><span data-stu-id="e672a-254">Package references</span></span>

<span data-ttu-id="e672a-255">请参阅[项目文件中的包引用](../consume-packages/package-references-in-project-files.md)</span><span class="sxs-lookup"><span data-stu-id="e672a-255">See [Package References in Project Files](../consume-packages/package-references-in-project-files.md).</span></span>

### <a name="project-to-project-references"></a><span data-ttu-id="e672a-256">项目到项目的引用</span><span class="sxs-lookup"><span data-stu-id="e672a-256">Project to project references</span></span>

<span data-ttu-id="e672a-257">默认情况下，项目到项目的引用被视为 nuget 包引用，例如：</span><span class="sxs-lookup"><span data-stu-id="e672a-257">Project to project references are considered by default as nuget package references, for example:</span></span>

```xml
<ProjectReference Include="..\UwpLibrary2\UwpLibrary2.csproj"/>
```

<span data-ttu-id="e672a-258">也可将以下元数据添加到项目引用：</span><span class="sxs-lookup"><span data-stu-id="e672a-258">You can also add the following metadata to your project reference:</span></span>

```xml
<IncludeAssets>
<ExcludeAssets>
<PrivateAssets>
```

### <a name="including-content-in-a-package"></a><span data-ttu-id="e672a-259">在包中添加内容</span><span class="sxs-lookup"><span data-stu-id="e672a-259">Including content in a package</span></span>

<span data-ttu-id="e672a-260">若要添加内容，请将额外的元数据添加到现有的 `<Content>` 项。</span><span class="sxs-lookup"><span data-stu-id="e672a-260">To include content, add extra metadata to the existing `<Content>` item.</span></span> <span data-ttu-id="e672a-261">默认情况下，类型“Content”的所有内容都包括在包中，除非使用以下条目替代：</span><span class="sxs-lookup"><span data-stu-id="e672a-261">By default everything of type "Content" gets included in the package unless you override with entries like the following:</span></span>

 ```xml
<Content Include="..\win7-x64\libuv.txt">
  <Pack>false</Pack>
</Content>
 ```

<span data-ttu-id="e672a-262">默认情况下，所有内容都添加到包中 `content` 和 `contentFiles\any\<target_framework>` 文件夹根目录，并保留相对文件夹结构，除非指定包路径：</span><span class="sxs-lookup"><span data-stu-id="e672a-262">By default, everything gets added to the root of the `content` and `contentFiles\any\<target_framework>` folder within a package and preserves the relative folder structure, unless you specify a package path:</span></span>

```xml
<Content Include="..\win7-x64\libuv.txt">
  <Pack>true</Pack>
  <PackagePath>content\myfiles\</PackagePath>
</Content>
```

<span data-ttu-id="e672a-263">如果仅希望将所有内容都复制到特定根文件夹（而不是 `content` 和 `contentFiles`），可使用 MSBuild 属性 `ContentTargetFolders`，其默认值为“content;contentFiles”，但可以设置为任何其他文件夹名称。</span><span class="sxs-lookup"><span data-stu-id="e672a-263">If you want to copy all your content to only a specific root folder(s) (instead of `content` and `contentFiles` both), you can use the MSBuild property `ContentTargetFolders`, which defaults to "content;contentFiles" but can be set to any other folder names.</span></span> <span data-ttu-id="e672a-264">请注意，基于 `buildAction`，仅在 `ContentTargetFolders` 中指定“contentFiles”会将文件置于 `contentFiles\any\<target_framework>` 或 `contentFiles\<language>\<target_framework>` 下。</span><span class="sxs-lookup"><span data-stu-id="e672a-264">Note that just specifying "contentFiles" in `ContentTargetFolders` puts files under `contentFiles\any\<target_framework>` or `contentFiles\<language>\<target_framework>` based on `buildAction`.</span></span>

<span data-ttu-id="e672a-265">`PackagePath` 可以是一组以分号分隔的目标路径。</span><span class="sxs-lookup"><span data-stu-id="e672a-265">`PackagePath` can be a semicolon-delimited set of target paths.</span></span> <span data-ttu-id="e672a-266">指定空的包路径会将文件添加到包的根目录。</span><span class="sxs-lookup"><span data-stu-id="e672a-266">Specifying an empty package path would add the file to the root of the package.</span></span> <span data-ttu-id="e672a-267">例如，以下操作会将 `libuv.txt` 添加到 `content\myfiles`、`content\samples` 和包的根目录：</span><span class="sxs-lookup"><span data-stu-id="e672a-267">For example, the following adds `libuv.txt` to `content\myfiles`, `content\samples`, and the package root:</span></span>

```xml
<Content Include="..\win7-x64\libuv.txt">
  <Pack>true</Pack>
  <PackagePath>content\myfiles;content\sample;;</PackagePath>
</Content>
```

<span data-ttu-id="e672a-268">另外还有 MSBuild 属性 `$(IncludeContentInPack)`，默认值为 `true`。</span><span class="sxs-lookup"><span data-stu-id="e672a-268">There is also an MSBuild property `$(IncludeContentInPack)`, which defaults to `true`.</span></span> <span data-ttu-id="e672a-269">如果在任何项目中将此值设置为 `false`，则该项目的内容不会包括在 nuget 包中。</span><span class="sxs-lookup"><span data-stu-id="e672a-269">If this is set to `false` on any project, then the content from that project are not included in the nuget package.</span></span>

<span data-ttu-id="e672a-270">其他可在任何上述项上设置的特定于包的元数据包括 ```<PackageCopyToOutput>``` 和 ```<PackageFlatten>```，后者在输出 nuspec 中的 ```contentFiles``` 条目上设置 ```CopyToOutput``` 和 ```Flatten``` 值。</span><span class="sxs-lookup"><span data-stu-id="e672a-270">Other pack specific metadata that you can set on any of the above items includes ```<PackageCopyToOutput>``` and ```<PackageFlatten>``` which sets ```CopyToOutput``` and ```Flatten``` values on the ```contentFiles``` entry in the output nuspec.</span></span>

> [!Note]
> <span data-ttu-id="e672a-271">除了“Content”项，`<Pack>` 和 `<PackagePath>` 元数据还可以在具有 Compile、EmbeddedResource、ApplicationDefinition、Page、Resource、SplashScreen、DesignData、DesignDataWithDesignTimeCreateableTypes、CodeAnalysisDictionary、AndroidAsset、AndroidResource、BundleResource 或 None 生成操作的文件上进行设置。</span><span class="sxs-lookup"><span data-stu-id="e672a-271">Apart from Content items, the `<Pack>` and `<PackagePath>` metadata can also be set on files with a build action of Compile, EmbeddedResource, ApplicationDefinition, Page, Resource, SplashScreen, DesignData, DesignDataWithDesignTimeCreateableTypes, CodeAnalysisDictionary, AndroidAsset, AndroidResource, BundleResource or None.</span></span>
>
> <span data-ttu-id="e672a-272">使用通配模式时，对于将包的文件名追加到包路径，包路径必须以文件夹分隔符结尾，否则包路径将被视为包括文件名的完整路径。</span><span class="sxs-lookup"><span data-stu-id="e672a-272">For pack to append the filename to your package path when using globbing patterns, your package path must end with the folder separator character, otherwise the package path is treated as the full path including the file name.</span></span>

### <a name="includesymbols"></a><span data-ttu-id="e672a-273">IncludeSymbols</span><span class="sxs-lookup"><span data-stu-id="e672a-273">IncludeSymbols</span></span>

<span data-ttu-id="e672a-274">使用 `MSBuild -t:pack -p:IncludeSymbols=true` 时，相应的 `.pdb` 文件将随其他输出文件（`.dll`、`.exe`、`.winmd`、`.xml`、`.json`、`.pri`）一起复制。</span><span class="sxs-lookup"><span data-stu-id="e672a-274">When using `MSBuild -t:pack -p:IncludeSymbols=true`, the corresponding `.pdb` files are copied along with other output files (`.dll`, `.exe`, `.winmd`, `.xml`, `.json`, `.pri`).</span></span> <span data-ttu-id="e672a-275">请注意，设置 `IncludeSymbols=true` 会创建常规包和符号包。</span><span class="sxs-lookup"><span data-stu-id="e672a-275">Note that setting `IncludeSymbols=true` creates a regular package *and* a symbols package.</span></span>

### <a name="includesource"></a><span data-ttu-id="e672a-276">IncludeSource</span><span class="sxs-lookup"><span data-stu-id="e672a-276">IncludeSource</span></span>

<span data-ttu-id="e672a-277">这与 `IncludeSymbols` 相同，但它还会连同 `.pdb` 文件复制源文件。</span><span class="sxs-lookup"><span data-stu-id="e672a-277">This is the same as `IncludeSymbols`, except that it copies source files along with `.pdb` files as well.</span></span> <span data-ttu-id="e672a-278">类型为 `Compile` 的所有文件都会复制到 `src\<ProjectName>\`，并保留生成包中的相对路径文件夹结构。</span><span class="sxs-lookup"><span data-stu-id="e672a-278">All files of type `Compile` are copied over to `src\<ProjectName>\` preserving the relative path folder structure in the resulting package.</span></span> <span data-ttu-id="e672a-279">对于将 `TreatAsPackageReference` 设置为 `false` 的任何 `ProjectReference` 的源文件也是如此。</span><span class="sxs-lookup"><span data-stu-id="e672a-279">The same also happens for source files of any `ProjectReference` which has `TreatAsPackageReference` set to `false`.</span></span>

<span data-ttu-id="e672a-280">如果类型为 Compile 的文件位于项目文件夹外，则它只添加到了 `src\<ProjectName>\`。</span><span class="sxs-lookup"><span data-stu-id="e672a-280">If a file of type Compile, is outside the project folder, then it's just added to `src\<ProjectName>\`.</span></span>

### <a name="packing-a-license-expression-or-a-license-file"></a><span data-ttu-id="e672a-281">装箱许可证表达式或许可证文件</span><span class="sxs-lookup"><span data-stu-id="e672a-281">Packing a license expression or a license file</span></span>

<span data-ttu-id="e672a-282">在使用许可证表达式时，应使用 PackageLicenseExpression 属性。</span><span class="sxs-lookup"><span data-stu-id="e672a-282">When using a license expression, the PackageLicenseExpression property should be used.</span></span> 
<span data-ttu-id="e672a-283">[许可证表达式示例](#https://github.com/NuGet/Samples/tree/master/PackageLicenseExpressionExample)。</span><span class="sxs-lookup"><span data-stu-id="e672a-283">[License expression sample](#https://github.com/NuGet/Samples/tree/master/PackageLicenseExpressionExample).</span></span>

<span data-ttu-id="e672a-284">封装的许可证文件，需要使用 PackageLicenseFile 属性来指定包的路径，相对于包的根。</span><span class="sxs-lookup"><span data-stu-id="e672a-284">When packing a license file, you need to use PackageLicenseFile property to specify the package path, relative to the root of the package.</span></span> <span data-ttu-id="e672a-285">此外，您需要确保该文件包含在包中。</span><span class="sxs-lookup"><span data-stu-id="e672a-285">In addition, you need to make sure that the file is included in the package.</span></span> <span data-ttu-id="e672a-286">例如：</span><span class="sxs-lookup"><span data-stu-id="e672a-286">For example:</span></span>

```xml
<PropertyGroup>
    <PackageLicenseFile>LICENSE.txt</PackageLicenseFile>
</PropertyGroup>

<ItemGroup>
    <None Include="licenses\LICENSE.txt" Pack="true" PackagePath="$(PackageLicenseFile)"/>
</ItemGroup>
```
<span data-ttu-id="e672a-287">[许可证生命示例](#https://github.com/NuGet/Samples/tree/master/PackageLicenseFileExample)。</span><span class="sxs-lookup"><span data-stu-id="e672a-287">[License life sample](#https://github.com/NuGet/Samples/tree/master/PackageLicenseFileExample).</span></span>

### <a name="istool"></a><span data-ttu-id="e672a-288">IsTool</span><span class="sxs-lookup"><span data-stu-id="e672a-288">IsTool</span></span>

<span data-ttu-id="e672a-289">使用 `MSBuild -t:pack -p:IsTool=true` 时，所有输出文件（如[输出程序集](#output-assemblies)方案中所指定）都被复制到 `tools` 文件夹，而不是 `lib` 文件夹。</span><span class="sxs-lookup"><span data-stu-id="e672a-289">When using `MSBuild -t:pack -p:IsTool=true`, all output files, as specified in the [Output Assemblies](#output-assemblies) scenario, are copied to the `tools` folder instead of the `lib` folder.</span></span> <span data-ttu-id="e672a-290">请注意，这不同于 `DotNetCliTool`，后者通过在 `.csproj` 文件中设置 `PackageType` 进行指定。</span><span class="sxs-lookup"><span data-stu-id="e672a-290">Note that this is different from a `DotNetCliTool` which is specified by setting the `PackageType` in `.csproj` file.</span></span>

### <a name="packing-using-a-nuspec"></a><span data-ttu-id="e672a-291">使用 .nuspec 打包</span><span class="sxs-lookup"><span data-stu-id="e672a-291">Packing using a .nuspec</span></span>

<span data-ttu-id="e672a-292">可以使用`.nuspec`文件打包项目，假设具有一个 SDK 项目文件导入`NuGet.Build.Tasks.Pack.targets`，以便可以执行包任务。</span><span class="sxs-lookup"><span data-stu-id="e672a-292">You can use a `.nuspec` file to pack your project provided that you have a SDK project file to import `NuGet.Build.Tasks.Pack.targets` so that the pack task can be executed.</span></span> <span data-ttu-id="e672a-293">仍需要将项目还原之前能够打包 nuspec 文件。</span><span class="sxs-lookup"><span data-stu-id="e672a-293">You still need to restore the project before you can pack a nuspec file.</span></span> <span data-ttu-id="e672a-294">项目文件的目标框架是不相关和打包 nuspec 时不使用。</span><span class="sxs-lookup"><span data-stu-id="e672a-294">The target framework of the project file is irrelevant and not used when packing a nuspec.</span></span> <span data-ttu-id="e672a-295">以下三个 MSBuild 属性与使用 `.nuspec` 的打包相关：</span><span class="sxs-lookup"><span data-stu-id="e672a-295">The following three MSBuild properties are relevant to packing using a `.nuspec`:</span></span>

1. <span data-ttu-id="e672a-296">`NuspecFile`：用于打包的 `.nuspec` 文件的相对或绝对路径。</span><span class="sxs-lookup"><span data-stu-id="e672a-296">`NuspecFile`: relative or absolute path to the `.nuspec` file being used for packing.</span></span>
1. <span data-ttu-id="e672a-297">`NuspecProperties`：键=值对的分号分隔列表。</span><span class="sxs-lookup"><span data-stu-id="e672a-297">`NuspecProperties`: a semicolon-separated list of key=value pairs.</span></span> <span data-ttu-id="e672a-298">由于 MSBuild 命令行分析工作的方式，必须指定多个属性，如下所示：`-p:NuspecProperties=\"key1=value1;key2=value2\"`。</span><span class="sxs-lookup"><span data-stu-id="e672a-298">Due to the way MSBuild command-line parsing works, multiple properties must be specified as follows: `-p:NuspecProperties=\"key1=value1;key2=value2\"`.</span></span>  
1. <span data-ttu-id="e672a-299">`NuspecBasePath`：`.nuspec` 文件的基路径。</span><span class="sxs-lookup"><span data-stu-id="e672a-299">`NuspecBasePath`: Base path for the `.nuspec` file.</span></span>

<span data-ttu-id="e672a-300">如果使用 `dotnet.exe` 打包项目，请使用类似于下面的命令：</span><span class="sxs-lookup"><span data-stu-id="e672a-300">If using `dotnet.exe` to pack your project, use a command like the following:</span></span>

```cli
dotnet pack <path to .csproj file> -p:NuspecFile=<path to nuspec file> -p:NuspecProperties=<> -p:NuspecBasePath=<Base path> 
```

<span data-ttu-id="e672a-301">如果使用 MSBuild 打包项目，请使用类似于下面的命令：</span><span class="sxs-lookup"><span data-stu-id="e672a-301">If using MSBuild to pack your project, use a command like the following:</span></span>

```cli
msbuild -t:pack <path to .csproj file> -p:NuspecFile=<path to nuspec file> -p:NuspecProperties=<> -p:NuspecBasePath=<Base path> 
```

<span data-ttu-id="e672a-302">请注意，打包 nuspec 使用 dotnet.exe 或 msbuild 还会导致默认情况下生成项目。</span><span class="sxs-lookup"><span data-stu-id="e672a-302">Please note that packing a nuspec using dotnet.exe or msbuild also leads to building the project by default.</span></span> <span data-ttu-id="e672a-303">这可以避免通过传递```--no-build```属性设置为等同于设置的 dotnet.exe```<NoBuild>true</NoBuild> ```在项目文件中，以及设置```<IncludeBuildOutput>false</IncludeBuildOutput> ```项目文件中</span><span class="sxs-lookup"><span data-stu-id="e672a-303">This can be avoided by passing ```--no-build``` property to dotnet.exe, which is the equivalent of setting ```<NoBuild>true</NoBuild> ``` in your project file, along with setting ```<IncludeBuildOutput>false</IncludeBuildOutput> ``` in the project file</span></span>

<span data-ttu-id="e672a-304">要打包的 nuspec 文件的 csproj 文件的一个示例是：</span><span class="sxs-lookup"><span data-stu-id="e672a-304">An example of a csproj file to pack a nuspec file is:</span></span>

```xml
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

### <a name="advanced-extension-points-to-create-customized-package"></a><span data-ttu-id="e672a-305">高级扩展点来创建自定义安装包</span><span class="sxs-lookup"><span data-stu-id="e672a-305">Advanced extension points to create customized package</span></span>

<span data-ttu-id="e672a-306">`pack`目标提供了在内部，目标框架特定生成中运行的两个扩展点。</span><span class="sxs-lookup"><span data-stu-id="e672a-306">The `pack` target provides two extension points that run in the inner, target framework specific build.</span></span> <span data-ttu-id="e672a-307">包括目标框架特定内容和程序集放在一个程序包支持的扩展点：</span><span class="sxs-lookup"><span data-stu-id="e672a-307">The extension points support including target framework specific content and assemblies into a package:</span></span>

- <span data-ttu-id="e672a-308">`TargetsForTfmSpecificBuildOutput` 目标： 用于文件内`lib`文件夹或使用指定的文件夹`BuildOutputTargetFolder`。</span><span class="sxs-lookup"><span data-stu-id="e672a-308">`TargetsForTfmSpecificBuildOutput` target: Use for files inside the `lib` folder or a folder specified using `BuildOutputTargetFolder`.</span></span>
- <span data-ttu-id="e672a-309">`TargetsForTfmSpecificContentInPackage` 目标： 之外的文件的使用`BuildOutputTargetFolder`。</span><span class="sxs-lookup"><span data-stu-id="e672a-309">`TargetsForTfmSpecificContentInPackage` target: Use for files outside the `BuildOutputTargetFolder`.</span></span>

#### <a name="targetsfortfmspecificbuildoutput"></a><span data-ttu-id="e672a-310">TargetsForTfmSpecificBuildOutput</span><span class="sxs-lookup"><span data-stu-id="e672a-310">TargetsForTfmSpecificBuildOutput</span></span>

<span data-ttu-id="e672a-311">编写自定义目标和指定的值为`$(TargetsForTfmSpecificBuildOutput)`属性。</span><span class="sxs-lookup"><span data-stu-id="e672a-311">Write a custom target and specify it as the value of the `$(TargetsForTfmSpecificBuildOutput)` property.</span></span> <span data-ttu-id="e672a-312">转到所需的所有文件`BuildOutputTargetFolder`(默认情况下为 lib)，目标应将这些文件写入到 ItemGroup`BuildOutputInPackage`并设置以下两个元数据值：</span><span class="sxs-lookup"><span data-stu-id="e672a-312">For any files that need to go into the `BuildOutputTargetFolder` (lib by default), the target should write those files into the ItemGroup `BuildOutputInPackage` and set the following two metadata values:</span></span>

- <span data-ttu-id="e672a-313">`FinalOutputPath`: 该文件; 绝对路径如果未提供，标识用于评估源路径。</span><span class="sxs-lookup"><span data-stu-id="e672a-313">`FinalOutputPath`: The absolute path of the file; if not provided, the Identity is used to evaluate source path.</span></span>
- <span data-ttu-id="e672a-314">`TargetPath`: （可选) 设置时需要转到子文件夹内文件`lib\<TargetFramework>`，像在其各自的区域性文件夹下，所涉及的附属资源程序集。</span><span class="sxs-lookup"><span data-stu-id="e672a-314">`TargetPath`:  (Optional) Set when the file needs to go into a subfolder within `lib\<TargetFramework>` , like satellite assemblies that go under their respective culture folders.</span></span> <span data-ttu-id="e672a-315">默认值为的文件的名称。</span><span class="sxs-lookup"><span data-stu-id="e672a-315">Defaults to the name of the file.</span></span>

<span data-ttu-id="e672a-316">示例:</span><span class="sxs-lookup"><span data-stu-id="e672a-316">Example:</span></span>

```xml
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

#### <a name="targetsfortfmspecificcontentinpackage"></a><span data-ttu-id="e672a-317">TargetsForTfmSpecificContentInPackage</span><span class="sxs-lookup"><span data-stu-id="e672a-317">TargetsForTfmSpecificContentInPackage</span></span>

<span data-ttu-id="e672a-318">编写自定义目标和指定的值为`$(TargetsForTfmSpecificContentInPackage)`属性。</span><span class="sxs-lookup"><span data-stu-id="e672a-318">Write a custom target and specify it as the value of the `$(TargetsForTfmSpecificContentInPackage)` property.</span></span> <span data-ttu-id="e672a-319">若要在包中包含任何文件，目标应将这些文件写入 ItemGroup`TfmSpecificPackageFile`并设置以下可选元数据：</span><span class="sxs-lookup"><span data-stu-id="e672a-319">For any files to include in the package, the target should write those files into the ItemGroup `TfmSpecificPackageFile` and set the following optional metadata:</span></span>

- <span data-ttu-id="e672a-320">`PackagePath`： 该文件应位于包中的输出路径。</span><span class="sxs-lookup"><span data-stu-id="e672a-320">`PackagePath`: Path where the file should be output in the package.</span></span> <span data-ttu-id="e672a-321">如果多个文件添加到相同的包路径，NuGet 会发出警告。</span><span class="sxs-lookup"><span data-stu-id="e672a-321">NuGet issues a warning if more than one file is added to the same package path.</span></span>
- <span data-ttu-id="e672a-322">`BuildAction`: 生成操作以将分配到该文件，才是必需的包路径是否在`contentFiles`文件夹。</span><span class="sxs-lookup"><span data-stu-id="e672a-322">`BuildAction`: The build action to assign to the file, required only if the package path is in the `contentFiles` folder.</span></span> <span data-ttu-id="e672a-323">默认值为"None"。</span><span class="sxs-lookup"><span data-stu-id="e672a-323">Defaults to "None".</span></span>

<span data-ttu-id="e672a-324">示例：</span><span class="sxs-lookup"><span data-stu-id="e672a-324">An example:</span></span>
```xml
<PropertyGroup>
  <TargetsForTfmSpecificContentInPackage>$(TargetsForTfmSpecificContentInPackage);CustomContentTarget</TargetsForTfmSpecificContentInPackage>
</PropertyGroup>

<Target Name="CustomContentTarget">
  <ItemGroup>
    <TfmSpecificPackageFile Include="abc.txt">
      <PackagePath>mycontent/$(TargetFramework)</PackagePath>
    </TfmSpecificPackageFile>
    <TfmSpecificPackageFile Include="Extensions/ext.txt" Condition="'$(TargetFramework)' == 'net46'">
      <PackagePath>net46content</PackagePath>
    </TfmSpecificPackageFile>  
  </ItemGroup>
</Target>  
```

## <a name="restore-target"></a><span data-ttu-id="e672a-325">还原目标</span><span class="sxs-lookup"><span data-stu-id="e672a-325">restore target</span></span>

<span data-ttu-id="e672a-326">`MSBuild -t:restore`（`nuget restore` 和 `dotnet restore` 与 .NET Core 项目一起使用）会还原项目文件中引用的包，如下所示：</span><span class="sxs-lookup"><span data-stu-id="e672a-326">`MSBuild -t:restore` (which `nuget restore` and `dotnet restore` use with .NET Core projects), restores packages referenced in the project file as follows:</span></span>

1. <span data-ttu-id="e672a-327">读取所有项目到项目的引用</span><span class="sxs-lookup"><span data-stu-id="e672a-327">Read all project to project references</span></span>
1. <span data-ttu-id="e672a-328">读取项目属性以查找中间文件夹和目标框架</span><span class="sxs-lookup"><span data-stu-id="e672a-328">Read the project properties to find the intermediate folder and target frameworks</span></span>
1. <span data-ttu-id="e672a-329">将 msbuild 数据传递到 NuGet.Build.Tasks.dll</span><span class="sxs-lookup"><span data-stu-id="e672a-329">Pass msbuild data to NuGet.Build.Tasks.dll</span></span>
1. <span data-ttu-id="e672a-330">运行还原</span><span class="sxs-lookup"><span data-stu-id="e672a-330">Run restore</span></span>
1. <span data-ttu-id="e672a-331">下载包</span><span class="sxs-lookup"><span data-stu-id="e672a-331">Download packages</span></span>
1. <span data-ttu-id="e672a-332">编写资产文件、目标和属性</span><span class="sxs-lookup"><span data-stu-id="e672a-332">Write assets file, targets, and props</span></span>

<span data-ttu-id="e672a-333">`restore`目标的工作原理**仅**对于使用 PackageReference 格式的项目。</span><span class="sxs-lookup"><span data-stu-id="e672a-333">The `restore` target works **only** for projects using the PackageReference format.</span></span> <span data-ttu-id="e672a-334">与其**不**都可以为使用项目`packages.config`格式设置; 使用[nuget 还原](../tools/cli-ref-restore.md)相反。</span><span class="sxs-lookup"><span data-stu-id="e672a-334">It does **not** work for projects using the `packages.config` format; use [nuget restore](../tools/cli-ref-restore.md) instead.</span></span>

### <a name="restore-properties"></a><span data-ttu-id="e672a-335">还原属性</span><span class="sxs-lookup"><span data-stu-id="e672a-335">Restore properties</span></span>

<span data-ttu-id="e672a-336">其他的还原设置可能来自项目文件中的 MSBuild 属性。</span><span class="sxs-lookup"><span data-stu-id="e672a-336">Additional restore settings may come from MSBuild properties in the project file.</span></span> <span data-ttu-id="e672a-337">还可以从命令行使用 `-p:` 开关设置值（请参阅以下示例）。</span><span class="sxs-lookup"><span data-stu-id="e672a-337">Values can also be set from the command line using the `-p:` switch (see Examples below).</span></span>

| <span data-ttu-id="e672a-338">属性</span><span class="sxs-lookup"><span data-stu-id="e672a-338">Property</span></span> | <span data-ttu-id="e672a-339">描述</span><span class="sxs-lookup"><span data-stu-id="e672a-339">Description</span></span> |
|--------|--------|
| <span data-ttu-id="e672a-340">RestoreSources</span><span class="sxs-lookup"><span data-stu-id="e672a-340">RestoreSources</span></span> | <span data-ttu-id="e672a-341">以分号分隔的包源列表。</span><span class="sxs-lookup"><span data-stu-id="e672a-341">Semicolon-delimited list of package sources.</span></span> |
| <span data-ttu-id="e672a-342">RestorePackagesPath</span><span class="sxs-lookup"><span data-stu-id="e672a-342">RestorePackagesPath</span></span> | <span data-ttu-id="e672a-343">用户包文件夹路径。</span><span class="sxs-lookup"><span data-stu-id="e672a-343">User packages folder path.</span></span> |
| <span data-ttu-id="e672a-344">RestoreDisableParallel</span><span class="sxs-lookup"><span data-stu-id="e672a-344">RestoreDisableParallel</span></span> | <span data-ttu-id="e672a-345">将下载限制为一次一个。</span><span class="sxs-lookup"><span data-stu-id="e672a-345">Limit downloads to one at a time.</span></span> |
| <span data-ttu-id="e672a-346">RestoreConfigFile</span><span class="sxs-lookup"><span data-stu-id="e672a-346">RestoreConfigFile</span></span> | <span data-ttu-id="e672a-347">要应用的 `Nuget.Config` 文件的路径。</span><span class="sxs-lookup"><span data-stu-id="e672a-347">Path to a `Nuget.Config` file to apply.</span></span> |
| <span data-ttu-id="e672a-348">RestoreNoCache</span><span class="sxs-lookup"><span data-stu-id="e672a-348">RestoreNoCache</span></span> | <span data-ttu-id="e672a-349">如果为 true，可避免使用缓存的包。</span><span class="sxs-lookup"><span data-stu-id="e672a-349">If true, avoids using cached packages.</span></span> <span data-ttu-id="e672a-350">请参阅[管理全局包和缓存文件夹](../consume-packages/managing-the-global-packages-and-cache-folders.md)。</span><span class="sxs-lookup"><span data-stu-id="e672a-350">See [Managing the global packages and cache folders](../consume-packages/managing-the-global-packages-and-cache-folders.md).</span></span> |
| <span data-ttu-id="e672a-351">RestoreIgnoreFailedSources</span><span class="sxs-lookup"><span data-stu-id="e672a-351">RestoreIgnoreFailedSources</span></span> | <span data-ttu-id="e672a-352">如果为“true”，则忽略失败或丢失的包源。</span><span class="sxs-lookup"><span data-stu-id="e672a-352">If true, ignores failing or missing package sources.</span></span> |
| <span data-ttu-id="e672a-353">RestoreTaskAssemblyFile</span><span class="sxs-lookup"><span data-stu-id="e672a-353">RestoreTaskAssemblyFile</span></span> | <span data-ttu-id="e672a-354">`NuGet.Build.Tasks.dll` 的路径。</span><span class="sxs-lookup"><span data-stu-id="e672a-354">Path to `NuGet.Build.Tasks.dll`.</span></span> |
| <span data-ttu-id="e672a-355">RestoreGraphProjectInput</span><span class="sxs-lookup"><span data-stu-id="e672a-355">RestoreGraphProjectInput</span></span> | <span data-ttu-id="e672a-356">要还原的以分号分隔的项目列表，其中应包含绝对路径。</span><span class="sxs-lookup"><span data-stu-id="e672a-356">Semicolon-delimited list of projects to restore, which should contain absolute paths.</span></span> |
| <span data-ttu-id="e672a-357">RestoreOutputPath</span><span class="sxs-lookup"><span data-stu-id="e672a-357">RestoreOutputPath</span></span> | <span data-ttu-id="e672a-358">输出文件夹，默认为 `obj` 文件夹。</span><span class="sxs-lookup"><span data-stu-id="e672a-358">Output folder, defaulting to the `obj` folder.</span></span> |

#### <a name="examples"></a><span data-ttu-id="e672a-359">示例</span><span class="sxs-lookup"><span data-stu-id="e672a-359">Examples</span></span>

<span data-ttu-id="e672a-360">命令行：</span><span class="sxs-lookup"><span data-stu-id="e672a-360">Command line:</span></span>

```cli
msbuild -t:restore -p:RestoreConfigFile=<path>
```

<span data-ttu-id="e672a-361">项目文件：</span><span class="sxs-lookup"><span data-stu-id="e672a-361">Project file:</span></span>

```xml
<PropertyGroup>
    <RestoreIgnoreFailedSource>true</RestoreIgnoreFailedSource>
</PropertyGroup>
```

### <a name="restore-outputs"></a><span data-ttu-id="e672a-362">还原输出</span><span class="sxs-lookup"><span data-stu-id="e672a-362">Restore outputs</span></span>

<span data-ttu-id="e672a-363">还原会在生成 `obj` 文件夹中创建以下文件：</span><span class="sxs-lookup"><span data-stu-id="e672a-363">Restore creates the following files in the build `obj` folder:</span></span>

| <span data-ttu-id="e672a-364">文件</span><span class="sxs-lookup"><span data-stu-id="e672a-364">File</span></span> | <span data-ttu-id="e672a-365">描述</span><span class="sxs-lookup"><span data-stu-id="e672a-365">Description</span></span> |
|--------|--------|
| `project.assets.json` | <span data-ttu-id="e672a-366">包含的所有包引用的依赖项关系图。</span><span class="sxs-lookup"><span data-stu-id="e672a-366">Contains the dependency graph of all package references.</span></span> |
| `{projectName}.projectFileExtension.nuget.g.props` | <span data-ttu-id="e672a-367">包中包含的对 MSBuild 属性的引用</span><span class="sxs-lookup"><span data-stu-id="e672a-367">References to MSBuild props contained in packages</span></span> |
| `{projectName}.projectFileExtension.nuget.g.targets` | <span data-ttu-id="e672a-368">包中包含的对 MSBuild 目标的引用</span><span class="sxs-lookup"><span data-stu-id="e672a-368">References to MSBuild targets contained in packages</span></span> |

### <a name="packagetargetfallback"></a><span data-ttu-id="e672a-369">PackageTargetFallback</span><span class="sxs-lookup"><span data-stu-id="e672a-369">PackageTargetFallback</span></span>

<span data-ttu-id="e672a-370">`PackageTargetFallback` 元素可用于指定要在还原包时使用的一组兼容目标。</span><span class="sxs-lookup"><span data-stu-id="e672a-370">The `PackageTargetFallback` element allows you to specify a set of compatible targets to be used when restoring packages.</span></span> <span data-ttu-id="e672a-371">旨在允许使用 dotnet [TxM](../reference/target-frameworks.md) 的包与未声明 dotnet TxM 的兼容包结合使用。</span><span class="sxs-lookup"><span data-stu-id="e672a-371">It's designed to allow packages that use a dotnet [TxM](../reference/target-frameworks.md) to work with compatible packages that don't declare a dotnet TxM.</span></span> <span data-ttu-id="e672a-372">也就是说，如果项目使用 dotnet TxM，那么所依赖的所有包也必须有 dotnet TxM，除非将 `<PackageTargetFallback>` 添加到项目中，以允许非 dotnet 平台与 dotnet 兼容。</span><span class="sxs-lookup"><span data-stu-id="e672a-372">That is, if your project uses the dotnet TxM, then all the packages it depends on must also have a dotnet TxM, unless you add the `<PackageTargetFallback>` to your project in order to allow non-dotnet platforms to be compatible with dotnet.</span></span>

<span data-ttu-id="e672a-373">例如，如果项目使用的是 `netstandard1.6` TxM，且从属包仅包含 `lib/net45/a.dll` 和 `lib/portable-net45+win81/a.dll`，则项目将无法生成。</span><span class="sxs-lookup"><span data-stu-id="e672a-373">For example, if the project is using the `netstandard1.6` TxM, and a dependent package contains only `lib/net45/a.dll` and `lib/portable-net45+win81/a.dll`, then the project will fail to build.</span></span> <span data-ttu-id="e672a-374">如果需要的是后一种 DLL，则可以按照如下所示添加 `PackageTargetFallback`，声明 `portable-net45+win81` DLL 是兼容的：</span><span class="sxs-lookup"><span data-stu-id="e672a-374">If what you want to bring in is the latter DLL, then you can add a `PackageTargetFallback` as follows to say that the `portable-net45+win81` DLL is compatible:</span></span>

```xml
<PackageTargetFallback Condition="'$(TargetFramework)'=='netstandard1.6'">
    portable-net45+win81
</PackageTargetFallback>
```

<span data-ttu-id="e672a-375">若要声明项目中所有目标的回退，请停止 `Condition` 属性。</span><span class="sxs-lookup"><span data-stu-id="e672a-375">To declare a fallback for all targets in your project, leave off the `Condition` attribute.</span></span> <span data-ttu-id="e672a-376">还可以通过包括 `$(PackageTargetFallback)` 扩展任何现有 `PackageTargetFallback`，如下所示：</span><span class="sxs-lookup"><span data-stu-id="e672a-376">You can also extend any existing `PackageTargetFallback` by including `$(PackageTargetFallback)` as shown here:</span></span>

```xml
<PackageTargetFallback>
    $(PackageTargetFallback);portable-net45+win81
</PackageTargetFallback >
```

### <a name="replacing-one-library-from-a-restore-graph"></a><span data-ttu-id="e672a-377">从还原图中替换一个库</span><span class="sxs-lookup"><span data-stu-id="e672a-377">Replacing one library from a restore graph</span></span>

<span data-ttu-id="e672a-378">如果还原引入了错误的程序集，可以排除包默认选项，并将其替换为自己的选项。</span><span class="sxs-lookup"><span data-stu-id="e672a-378">If a restore is bringing the wrong assembly, it's possible to exclude that packages default choice, and replace it with your own choice.</span></span> <span data-ttu-id="e672a-379">首先使用顶级 `PackageReference`，排除所有资产：</span><span class="sxs-lookup"><span data-stu-id="e672a-379">First with a top level `PackageReference`, exclude all assets:</span></span>

```xml
<PackageReference Include="Newtonsoft.Json" Version="9.0.1">
  <ExcludeAssets>All</ExcludeAssets>
</PackageReference>
```

<span data-ttu-id="e672a-380">接下来，将自己的引用添加到适当的 DLL 本地副本：</span><span class="sxs-lookup"><span data-stu-id="e672a-380">Next, add your own reference to the appropriate local copy of the DLL:</span></span>

```xml
<Reference Include="Newtonsoft.Json.dll" />
```
