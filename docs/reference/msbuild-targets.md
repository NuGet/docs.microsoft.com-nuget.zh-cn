---
title: 作为 MSBuild 目标的 NuGet 包和还原
description: NuGet 包和还原可作为 MSBuild 目标直接用于 NuGet 4.0+。
author: karann-msft
ms.author: karann
ms.date: 03/23/2018
ms.topic: conceptual
ms.openlocfilehash: 16b8ff532b87a3e3f96029e77dd166eb39294c0b
ms.sourcegitcommit: 5a741f025e816b684ffe44a81ef7d3fbd2800039
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/09/2019
ms.locfileid: "70815346"
---
# <a name="nuget-pack-and-restore-as-msbuild-targets"></a><span data-ttu-id="82450-103">作为 MSBuild 目标的 NuGet 包和还原</span><span class="sxs-lookup"><span data-stu-id="82450-103">NuGet pack and restore as MSBuild targets</span></span>

<span data-ttu-id="82450-104">NuGet 4.0+</span><span class="sxs-lookup"><span data-stu-id="82450-104">*NuGet 4.0+*</span></span>

<span data-ttu-id="82450-105">使用[PackageReference](../consume-packages/package-references-in-project-files.md)格式，NuGet 4.0 + 可以直接将所有清单元数据存储在项目文件中，而不是`.nuspec`使用单独的文件。</span><span class="sxs-lookup"><span data-stu-id="82450-105">With the [PackageReference](../consume-packages/package-references-in-project-files.md) format, NuGet 4.0+ can store all manifest metadata directly within a project file rather than using a separate `.nuspec` file.</span></span>

<span data-ttu-id="82450-106">如下所述，对于 MSBuild 15.1+，NuGet 还是具有 `pack` 目标和 `restore` 目标的一等 MSBuild 公民。</span><span class="sxs-lookup"><span data-stu-id="82450-106">With MSBuild 15.1+, NuGet is also a first-class MSBuild citizen with the `pack` and `restore` targets as described below.</span></span> <span data-ttu-id="82450-107">借助这些目标，你可以像使用任何其他 MSBuild 任务或目标一样使用 NuGet。</span><span class="sxs-lookup"><span data-stu-id="82450-107">These targets allow you to work with NuGet as you would with any other MSBuild task or target.</span></span> <span data-ttu-id="82450-108">有关使用 MSBuild 创建 NuGet 包的说明，请参阅[使用 Msbuild 创建 nuget 包](../create-packages/creating-a-package-msbuild.md)。</span><span class="sxs-lookup"><span data-stu-id="82450-108">For instructions creating a NuGet package using MSBuild, see [Create a NuGet package using MSBuild](../create-packages/creating-a-package-msbuild.md).</span></span> <span data-ttu-id="82450-109">（对于 Nuget 3.x 及更早版本，通过 NuGet CLI 使用 [pack](../reference/cli-reference/cli-ref-pack.md) 和 [restore](../reference/cli-reference/cli-ref-restore.md) 命令。）</span><span class="sxs-lookup"><span data-stu-id="82450-109">(For NuGet 3.x and earlier, you use the [pack](../reference/cli-reference/cli-ref-pack.md) and [restore](../reference/cli-reference/cli-ref-restore.md) commands through the NuGet CLI instead.)</span></span>

## <a name="target-build-order"></a><span data-ttu-id="82450-110">目标生成顺序</span><span class="sxs-lookup"><span data-stu-id="82450-110">Target build order</span></span>

<span data-ttu-id="82450-111">由于 `pack` 和 `restore` 为 MSBuild 目标，因此可以访问它们以增强工作流。</span><span class="sxs-lookup"><span data-stu-id="82450-111">Because `pack` and `restore` are  MSBuild targets, you can access them to enhance your workflow.</span></span> <span data-ttu-id="82450-112">例如，假设希望在打包后将包复制到网络共享。</span><span class="sxs-lookup"><span data-stu-id="82450-112">For example, let’s say you want to copy your package to a network share after packing it.</span></span> <span data-ttu-id="82450-113">此操作可通过向项目文件中添加以下内容来完成：</span><span class="sxs-lookup"><span data-stu-id="82450-113">You can do that by adding the following in your project file:</span></span>

```xml
<Target Name="CopyPackage" AfterTargets="Pack">
  <Copy
    SourceFiles="$(OutputPath)..\$(PackageId).$(PackageVersion).nupkg"
    DestinationFolder="\\myshare\packageshare\"
    />
</Target>
```

<span data-ttu-id="82450-114">同样，你可以编写 MSBuild 任务、编写自己的目标并使用 MSBuild 任务中的 NuGet 属性。</span><span class="sxs-lookup"><span data-stu-id="82450-114">Similarly, you can write an MSBuild task, write your own target and consume NuGet properties in the MSBuild task.</span></span>

> [!NOTE]
> <span data-ttu-id="82450-115">`$(OutputPath)`是相对的，需要从项目根目录运行命令。</span><span class="sxs-lookup"><span data-stu-id="82450-115">`$(OutputPath)` is relative and expects that you are running the command from the project root.</span></span>

## <a name="pack-target"></a><span data-ttu-id="82450-116">包目标</span><span class="sxs-lookup"><span data-stu-id="82450-116">pack target</span></span>

<span data-ttu-id="82450-117">对于使用 PackageReference 格式的 .NET Standard 项目，使用`msbuild -t:pack`可以从项目文件绘制输入，以在创建 NuGet 包时使用。</span><span class="sxs-lookup"><span data-stu-id="82450-117">For .NET Standard projects using the PackageReference format, using `msbuild -t:pack` draws inputs from the project file to use in creating a NuGet package.</span></span>

<span data-ttu-id="82450-118">下表描述了可以添加到项目文件第一个 `<PropertyGroup>` 节点中的 MSBuild 属性。</span><span class="sxs-lookup"><span data-stu-id="82450-118">The table below describes the MSBuild properties that can be added to a project file within the first `<PropertyGroup>` node.</span></span> <span data-ttu-id="82450-119">在 Visual Studio 2017 及更高版本中，通过右键单击项目并选择上下文菜单上的“编辑 {project_name}”，即可轻松进行这些编辑。</span><span class="sxs-lookup"><span data-stu-id="82450-119">You can make these edits easily in Visual Studio 2017 and later by right-clicking the project and selecting **Edit {project_name}** on the context menu.</span></span> <span data-ttu-id="82450-120">为方便起见，表由 [`.nuspec` 文件](../reference/nuspec.md)中的等效属性组织。</span><span class="sxs-lookup"><span data-stu-id="82450-120">For convenience the table is organized by the equivalent property in a [`.nuspec` file](../reference/nuspec.md).</span></span>

<span data-ttu-id="82450-121">请注意，`.nuspec` 的 `Owners` 和 `Summary` 属性不受 MSBuild 支持。</span><span class="sxs-lookup"><span data-stu-id="82450-121">Note that the `Owners` and `Summary` properties from `.nuspec` are not supported with MSBuild.</span></span>

| <span data-ttu-id="82450-122">属性/NuSpec 值</span><span class="sxs-lookup"><span data-stu-id="82450-122">Attribute/NuSpec Value</span></span> | <span data-ttu-id="82450-123">MSBuild 属性</span><span class="sxs-lookup"><span data-stu-id="82450-123">MSBuild Property</span></span> | <span data-ttu-id="82450-124">默认</span><span class="sxs-lookup"><span data-stu-id="82450-124">Default</span></span> | <span data-ttu-id="82450-125">说明</span><span class="sxs-lookup"><span data-stu-id="82450-125">Notes</span></span> |
|--------|--------|--------|--------|
| <span data-ttu-id="82450-126">Id</span><span class="sxs-lookup"><span data-stu-id="82450-126">Id</span></span> | <span data-ttu-id="82450-127">PackageId</span><span class="sxs-lookup"><span data-stu-id="82450-127">PackageId</span></span> | <span data-ttu-id="82450-128">AssemblyName</span><span class="sxs-lookup"><span data-stu-id="82450-128">AssemblyName</span></span> | <span data-ttu-id="82450-129">MSBuild 的 $(AssemblyName)</span><span class="sxs-lookup"><span data-stu-id="82450-129">$(AssemblyName) from MSBuild</span></span> |
| <span data-ttu-id="82450-130">Version</span><span class="sxs-lookup"><span data-stu-id="82450-130">Version</span></span> | <span data-ttu-id="82450-131">PackageVersion</span><span class="sxs-lookup"><span data-stu-id="82450-131">PackageVersion</span></span> | <span data-ttu-id="82450-132">Version</span><span class="sxs-lookup"><span data-stu-id="82450-132">Version</span></span> | <span data-ttu-id="82450-133">这与 SemVer 兼容，例如，“1.0.0”、“1.0.0-beta”或“1.0.0-beta-00345”</span><span class="sxs-lookup"><span data-stu-id="82450-133">This is semver compatible, for example “1.0.0”, “1.0.0-beta”, or “1.0.0-beta-00345”</span></span> |
| <span data-ttu-id="82450-134">VersionPrefix</span><span class="sxs-lookup"><span data-stu-id="82450-134">VersionPrefix</span></span> | <span data-ttu-id="82450-135">PackageVersionPrefix</span><span class="sxs-lookup"><span data-stu-id="82450-135">PackageVersionPrefix</span></span> | <span data-ttu-id="82450-136">空</span><span class="sxs-lookup"><span data-stu-id="82450-136">empty</span></span> | <span data-ttu-id="82450-137">设置 PackageVersion 会覆盖 PackageVersionPrefix</span><span class="sxs-lookup"><span data-stu-id="82450-137">Setting PackageVersion overwrites PackageVersionPrefix</span></span> |
| <span data-ttu-id="82450-138">VersionSuffix</span><span class="sxs-lookup"><span data-stu-id="82450-138">VersionSuffix</span></span> | <span data-ttu-id="82450-139">PackageVersionSuffix</span><span class="sxs-lookup"><span data-stu-id="82450-139">PackageVersionSuffix</span></span> | <span data-ttu-id="82450-140">空</span><span class="sxs-lookup"><span data-stu-id="82450-140">empty</span></span> | <span data-ttu-id="82450-141">MSBuild 的 $(VersionSuffix)。</span><span class="sxs-lookup"><span data-stu-id="82450-141">$(VersionSuffix) from MSBuild.</span></span> <span data-ttu-id="82450-142">设置 PackageVersion 会覆盖 PackageVersionSuffix</span><span class="sxs-lookup"><span data-stu-id="82450-142">Setting PackageVersion overwrites PackageVersionSuffix</span></span> |
| <span data-ttu-id="82450-143">Authors</span><span class="sxs-lookup"><span data-stu-id="82450-143">Authors</span></span> | <span data-ttu-id="82450-144">Authors</span><span class="sxs-lookup"><span data-stu-id="82450-144">Authors</span></span> | <span data-ttu-id="82450-145">当前用户的用户名</span><span class="sxs-lookup"><span data-stu-id="82450-145">Username of the current user</span></span> | |
| <span data-ttu-id="82450-146">Owners</span><span class="sxs-lookup"><span data-stu-id="82450-146">Owners</span></span> | <span data-ttu-id="82450-147">不可用</span><span class="sxs-lookup"><span data-stu-id="82450-147">N/A</span></span> | <span data-ttu-id="82450-148">NuSpec 中不存在</span><span class="sxs-lookup"><span data-stu-id="82450-148">Not present in NuSpec</span></span> | |
| <span data-ttu-id="82450-149">标题</span><span class="sxs-lookup"><span data-stu-id="82450-149">Title</span></span> | <span data-ttu-id="82450-150">标题</span><span class="sxs-lookup"><span data-stu-id="82450-150">Title</span></span> | <span data-ttu-id="82450-151">PackageId</span><span class="sxs-lookup"><span data-stu-id="82450-151">The PackageId</span></span>| |
| <span data-ttu-id="82450-152">描述</span><span class="sxs-lookup"><span data-stu-id="82450-152">Description</span></span> | <span data-ttu-id="82450-153">描述</span><span class="sxs-lookup"><span data-stu-id="82450-153">Description</span></span> | <span data-ttu-id="82450-154">“包描述”</span><span class="sxs-lookup"><span data-stu-id="82450-154">"Package Description"</span></span> | |
| <span data-ttu-id="82450-155">Copyright</span><span class="sxs-lookup"><span data-stu-id="82450-155">Copyright</span></span> | <span data-ttu-id="82450-156">Copyright</span><span class="sxs-lookup"><span data-stu-id="82450-156">Copyright</span></span> | <span data-ttu-id="82450-157">空</span><span class="sxs-lookup"><span data-stu-id="82450-157">empty</span></span> | |
| <span data-ttu-id="82450-158">requireLicenseAcceptance</span><span class="sxs-lookup"><span data-stu-id="82450-158">RequireLicenseAcceptance</span></span> | <span data-ttu-id="82450-159">PackageRequireLicenseAcceptance</span><span class="sxs-lookup"><span data-stu-id="82450-159">PackageRequireLicenseAcceptance</span></span> | <span data-ttu-id="82450-160">假</span><span class="sxs-lookup"><span data-stu-id="82450-160">false</span></span> | |
| <span data-ttu-id="82450-161">照</span><span class="sxs-lookup"><span data-stu-id="82450-161">license</span></span> | <span data-ttu-id="82450-162">PackageLicenseExpression</span><span class="sxs-lookup"><span data-stu-id="82450-162">PackageLicenseExpression</span></span> | <span data-ttu-id="82450-163">空</span><span class="sxs-lookup"><span data-stu-id="82450-163">empty</span></span> | <span data-ttu-id="82450-164">对应于`<license type="expression">`</span><span class="sxs-lookup"><span data-stu-id="82450-164">Corresponds to `<license type="expression">`</span></span> |
| <span data-ttu-id="82450-165">照</span><span class="sxs-lookup"><span data-stu-id="82450-165">license</span></span> | <span data-ttu-id="82450-166">PackageLicenseFile</span><span class="sxs-lookup"><span data-stu-id="82450-166">PackageLicenseFile</span></span> | <span data-ttu-id="82450-167">空</span><span class="sxs-lookup"><span data-stu-id="82450-167">empty</span></span> | <span data-ttu-id="82450-168">对应到 `<license type="file">`。</span><span class="sxs-lookup"><span data-stu-id="82450-168">Corresponds to `<license type="file">`.</span></span> <span data-ttu-id="82450-169">可能需要显式打包所引用的许可证文件。</span><span class="sxs-lookup"><span data-stu-id="82450-169">You may need to explicitly pack the referenced license file.</span></span> |
| <span data-ttu-id="82450-170">LicenseUrl</span><span class="sxs-lookup"><span data-stu-id="82450-170">LicenseUrl</span></span> | <span data-ttu-id="82450-171">PackageLicenseUrl</span><span class="sxs-lookup"><span data-stu-id="82450-171">PackageLicenseUrl</span></span> | <span data-ttu-id="82450-172">空</span><span class="sxs-lookup"><span data-stu-id="82450-172">empty</span></span> | <span data-ttu-id="82450-173">`PackageLicenseUrl`已弃用，请使用 PackageLicenseExpression 或 PackageLicenseFile 属性</span><span class="sxs-lookup"><span data-stu-id="82450-173">`PackageLicenseUrl` is deprecated, use the PackageLicenseExpression or PackageLicenseFile property</span></span> |
| <span data-ttu-id="82450-174">ProjectUrl</span><span class="sxs-lookup"><span data-stu-id="82450-174">ProjectUrl</span></span> | <span data-ttu-id="82450-175">PackageProjectUrl</span><span class="sxs-lookup"><span data-stu-id="82450-175">PackageProjectUrl</span></span> | <span data-ttu-id="82450-176">空</span><span class="sxs-lookup"><span data-stu-id="82450-176">empty</span></span> | |
| <span data-ttu-id="82450-177">图标</span><span class="sxs-lookup"><span data-stu-id="82450-177">Icon</span></span> | <span data-ttu-id="82450-178">PackageIcon</span><span class="sxs-lookup"><span data-stu-id="82450-178">PackageIcon</span></span> | <span data-ttu-id="82450-179">空</span><span class="sxs-lookup"><span data-stu-id="82450-179">empty</span></span> | <span data-ttu-id="82450-180">可能需要显式打包所引用的图标图像文件。</span><span class="sxs-lookup"><span data-stu-id="82450-180">You may need to explicitly pack the referenced icon image file.</span></span>|
| <span data-ttu-id="82450-181">IconUrl</span><span class="sxs-lookup"><span data-stu-id="82450-181">IconUrl</span></span> | <span data-ttu-id="82450-182">PackageIconUrl</span><span class="sxs-lookup"><span data-stu-id="82450-182">PackageIconUrl</span></span> | <span data-ttu-id="82450-183">空</span><span class="sxs-lookup"><span data-stu-id="82450-183">empty</span></span> | <span data-ttu-id="82450-184">`PackageIconUrl`已弃用，请使用 PackageIcon 属性</span><span class="sxs-lookup"><span data-stu-id="82450-184">`PackageIconUrl` is deprecated, use the PackageIcon property</span></span> |
| <span data-ttu-id="82450-185">Tags</span><span class="sxs-lookup"><span data-stu-id="82450-185">Tags</span></span> | <span data-ttu-id="82450-186">PackageTags</span><span class="sxs-lookup"><span data-stu-id="82450-186">PackageTags</span></span> | <span data-ttu-id="82450-187">空</span><span class="sxs-lookup"><span data-stu-id="82450-187">empty</span></span> | <span data-ttu-id="82450-188">使用分号分隔标记。</span><span class="sxs-lookup"><span data-stu-id="82450-188">Tags are semi-colon delimited.</span></span> |
| <span data-ttu-id="82450-189">ReleaseNotes</span><span class="sxs-lookup"><span data-stu-id="82450-189">ReleaseNotes</span></span> | <span data-ttu-id="82450-190">PackageReleaseNotes</span><span class="sxs-lookup"><span data-stu-id="82450-190">PackageReleaseNotes</span></span> | <span data-ttu-id="82450-191">空</span><span class="sxs-lookup"><span data-stu-id="82450-191">empty</span></span> | |
| <span data-ttu-id="82450-192">存储库/Url</span><span class="sxs-lookup"><span data-stu-id="82450-192">Repository/Url</span></span> | <span data-ttu-id="82450-193">RepositoryUrl</span><span class="sxs-lookup"><span data-stu-id="82450-193">RepositoryUrl</span></span> | <span data-ttu-id="82450-194">空</span><span class="sxs-lookup"><span data-stu-id="82450-194">empty</span></span> | <span data-ttu-id="82450-195">用于克隆或检索源代码的存储库 URL。</span><span class="sxs-lookup"><span data-stu-id="82450-195">Repository URL used to clone or retrieve source code.</span></span> <span data-ttu-id="82450-196">实例 *https://github.com/NuGet/NuGet.Client.git*</span><span class="sxs-lookup"><span data-stu-id="82450-196">Example: *https://github.com/NuGet/NuGet.Client.git*</span></span> |
| <span data-ttu-id="82450-197">存储库/类型</span><span class="sxs-lookup"><span data-stu-id="82450-197">Repository/Type</span></span> | <span data-ttu-id="82450-198">RepositoryType</span><span class="sxs-lookup"><span data-stu-id="82450-198">RepositoryType</span></span> | <span data-ttu-id="82450-199">空</span><span class="sxs-lookup"><span data-stu-id="82450-199">empty</span></span> | <span data-ttu-id="82450-200">存储库类型。</span><span class="sxs-lookup"><span data-stu-id="82450-200">Repository type.</span></span> <span data-ttu-id="82450-201">示例： *git*、 *tfs*。</span><span class="sxs-lookup"><span data-stu-id="82450-201">Examples: *git*, *tfs*.</span></span> |
| <span data-ttu-id="82450-202">存储库/分支</span><span class="sxs-lookup"><span data-stu-id="82450-202">Repository/Branch</span></span> | <span data-ttu-id="82450-203">RepositoryBranch</span><span class="sxs-lookup"><span data-stu-id="82450-203">RepositoryBranch</span></span> | <span data-ttu-id="82450-204">空</span><span class="sxs-lookup"><span data-stu-id="82450-204">empty</span></span> | <span data-ttu-id="82450-205">可选存储库分支信息。</span><span class="sxs-lookup"><span data-stu-id="82450-205">Optional repository branch information.</span></span> <span data-ttu-id="82450-206">还必须为此属性指定要包含的*RepositoryUrl* 。</span><span class="sxs-lookup"><span data-stu-id="82450-206">*RepositoryUrl* must also be specified for this property to be included.</span></span> <span data-ttu-id="82450-207">示例： *master* （NuGet 4.7.0 +）</span><span class="sxs-lookup"><span data-stu-id="82450-207">Example: *master* (NuGet 4.7.0+)</span></span> |
| <span data-ttu-id="82450-208">存储库/提交</span><span class="sxs-lookup"><span data-stu-id="82450-208">Repository/Commit</span></span> | <span data-ttu-id="82450-209">RepositoryCommit</span><span class="sxs-lookup"><span data-stu-id="82450-209">RepositoryCommit</span></span> | <span data-ttu-id="82450-210">空</span><span class="sxs-lookup"><span data-stu-id="82450-210">empty</span></span> | <span data-ttu-id="82450-211">可选存储库提交或变更集，以指示生成包时所依据的源。</span><span class="sxs-lookup"><span data-stu-id="82450-211">Optional repository commit or changeset to indicate which source the package was built against.</span></span> <span data-ttu-id="82450-212">还必须为此属性指定要包含的*RepositoryUrl* 。</span><span class="sxs-lookup"><span data-stu-id="82450-212">*RepositoryUrl* must also be specified for this property to be included.</span></span> <span data-ttu-id="82450-213">示例：*0e4d1b598f350b3dc675018d539114d1328189ef* (NuGet 4.7.0+)</span><span class="sxs-lookup"><span data-stu-id="82450-213">Example: *0e4d1b598f350b3dc675018d539114d1328189ef* (NuGet 4.7.0+)</span></span> |
| <span data-ttu-id="82450-214">PackageType</span><span class="sxs-lookup"><span data-stu-id="82450-214">PackageType</span></span> | `<PackageType>DotNetCliTool, 1.0.0.0;Dependency, 2.0.0.0</PackageType>` | | |
| <span data-ttu-id="82450-215">总结</span><span class="sxs-lookup"><span data-stu-id="82450-215">Summary</span></span> | <span data-ttu-id="82450-216">不支持</span><span class="sxs-lookup"><span data-stu-id="82450-216">Not supported</span></span> | | |

### <a name="pack-target-inputs"></a><span data-ttu-id="82450-217">包目标输入</span><span class="sxs-lookup"><span data-stu-id="82450-217">pack target inputs</span></span>

- <span data-ttu-id="82450-218">IsPackable</span><span class="sxs-lookup"><span data-stu-id="82450-218">IsPackable</span></span>
- <span data-ttu-id="82450-219">SuppressDependenciesWhenPacking</span><span class="sxs-lookup"><span data-stu-id="82450-219">SuppressDependenciesWhenPacking</span></span>
- <span data-ttu-id="82450-220">PackageVersion</span><span class="sxs-lookup"><span data-stu-id="82450-220">PackageVersion</span></span>
- <span data-ttu-id="82450-221">PackageId</span><span class="sxs-lookup"><span data-stu-id="82450-221">PackageId</span></span>
- <span data-ttu-id="82450-222">Authors</span><span class="sxs-lookup"><span data-stu-id="82450-222">Authors</span></span>
- <span data-ttu-id="82450-223">描述</span><span class="sxs-lookup"><span data-stu-id="82450-223">Description</span></span>
- <span data-ttu-id="82450-224">Copyright</span><span class="sxs-lookup"><span data-stu-id="82450-224">Copyright</span></span>
- <span data-ttu-id="82450-225">PackageRequireLicenseAcceptance</span><span class="sxs-lookup"><span data-stu-id="82450-225">PackageRequireLicenseAcceptance</span></span>
- <span data-ttu-id="82450-226">DevelopmentDependency</span><span class="sxs-lookup"><span data-stu-id="82450-226">DevelopmentDependency</span></span>
- <span data-ttu-id="82450-227">PackageLicenseExpression</span><span class="sxs-lookup"><span data-stu-id="82450-227">PackageLicenseExpression</span></span>
- <span data-ttu-id="82450-228">PackageLicenseFile</span><span class="sxs-lookup"><span data-stu-id="82450-228">PackageLicenseFile</span></span>
- <span data-ttu-id="82450-229">PackageLicenseUrl</span><span class="sxs-lookup"><span data-stu-id="82450-229">PackageLicenseUrl</span></span>
- <span data-ttu-id="82450-230">PackageProjectUrl</span><span class="sxs-lookup"><span data-stu-id="82450-230">PackageProjectUrl</span></span>
- <span data-ttu-id="82450-231">PackageIconUrl</span><span class="sxs-lookup"><span data-stu-id="82450-231">PackageIconUrl</span></span>
- <span data-ttu-id="82450-232">PackageReleaseNotes</span><span class="sxs-lookup"><span data-stu-id="82450-232">PackageReleaseNotes</span></span>
- <span data-ttu-id="82450-233">PackageTags</span><span class="sxs-lookup"><span data-stu-id="82450-233">PackageTags</span></span>
- <span data-ttu-id="82450-234">PackageOutputPath</span><span class="sxs-lookup"><span data-stu-id="82450-234">PackageOutputPath</span></span>
- <span data-ttu-id="82450-235">IncludeSymbols</span><span class="sxs-lookup"><span data-stu-id="82450-235">IncludeSymbols</span></span>
- <span data-ttu-id="82450-236">IncludeSource</span><span class="sxs-lookup"><span data-stu-id="82450-236">IncludeSource</span></span>
- <span data-ttu-id="82450-237">PackageTypes</span><span class="sxs-lookup"><span data-stu-id="82450-237">PackageTypes</span></span>
- <span data-ttu-id="82450-238">IsTool</span><span class="sxs-lookup"><span data-stu-id="82450-238">IsTool</span></span>
- <span data-ttu-id="82450-239">RepositoryUrl</span><span class="sxs-lookup"><span data-stu-id="82450-239">RepositoryUrl</span></span>
- <span data-ttu-id="82450-240">RepositoryType</span><span class="sxs-lookup"><span data-stu-id="82450-240">RepositoryType</span></span>
- <span data-ttu-id="82450-241">RepositoryBranch</span><span class="sxs-lookup"><span data-stu-id="82450-241">RepositoryBranch</span></span>
- <span data-ttu-id="82450-242">RepositoryCommit</span><span class="sxs-lookup"><span data-stu-id="82450-242">RepositoryCommit</span></span>
- <span data-ttu-id="82450-243">NoPackageAnalysis</span><span class="sxs-lookup"><span data-stu-id="82450-243">NoPackageAnalysis</span></span>
- <span data-ttu-id="82450-244">MinClientVersion</span><span class="sxs-lookup"><span data-stu-id="82450-244">MinClientVersion</span></span>
- <span data-ttu-id="82450-245">IncludeBuildOutput</span><span class="sxs-lookup"><span data-stu-id="82450-245">IncludeBuildOutput</span></span>
- <span data-ttu-id="82450-246">IncludeContentInPack</span><span class="sxs-lookup"><span data-stu-id="82450-246">IncludeContentInPack</span></span>
- <span data-ttu-id="82450-247">BuildOutputTargetFolder</span><span class="sxs-lookup"><span data-stu-id="82450-247">BuildOutputTargetFolder</span></span>
- <span data-ttu-id="82450-248">ContentTargetFolders</span><span class="sxs-lookup"><span data-stu-id="82450-248">ContentTargetFolders</span></span>
- <span data-ttu-id="82450-249">NuspecFile</span><span class="sxs-lookup"><span data-stu-id="82450-249">NuspecFile</span></span>
- <span data-ttu-id="82450-250">NuspecBasePath</span><span class="sxs-lookup"><span data-stu-id="82450-250">NuspecBasePath</span></span>
- <span data-ttu-id="82450-251">NuspecProperties</span><span class="sxs-lookup"><span data-stu-id="82450-251">NuspecProperties</span></span>
- <span data-ttu-id="82450-252">Deterministic</span><span class="sxs-lookup"><span data-stu-id="82450-252">Deterministic</span></span>

## <a name="pack-scenarios"></a><span data-ttu-id="82450-253">包方案</span><span class="sxs-lookup"><span data-stu-id="82450-253">pack scenarios</span></span>

### <a name="suppress-dependencies"></a><span data-ttu-id="82450-254">禁止依赖项</span><span class="sxs-lookup"><span data-stu-id="82450-254">Suppress dependencies</span></span>

<span data-ttu-id="82450-255">若要取消生成的 NuGet 包中的包`SuppressDependenciesWhenPacking`依赖`true`项，请将设置为，将允许跳过生成的 nupkg 文件中的所有依赖项。</span><span class="sxs-lookup"><span data-stu-id="82450-255">To suppress package dependencies from generated NuGet package, set `SuppressDependenciesWhenPacking` to `true` which will allow skipping all the dependencies from generated nupkg file.</span></span>

### <a name="packageiconurl"></a><span data-ttu-id="82450-256">PackageIconUrl</span><span class="sxs-lookup"><span data-stu-id="82450-256">PackageIconUrl</span></span>

> [!Important]
> <span data-ttu-id="82450-257">PackageIconUrl 已被弃用。</span><span class="sxs-lookup"><span data-stu-id="82450-257">PackageIconUrl is deprecated.</span></span> <span data-ttu-id="82450-258">改用[PackageIcon](#packing-an-icon-image-file) 。</span><span class="sxs-lookup"><span data-stu-id="82450-258">Use [PackageIcon](#packing-an-icon-image-file) instead.</span></span>

### <a name="packing-an-icon-image-file"></a><span data-ttu-id="82450-259">打包图标图像文件</span><span class="sxs-lookup"><span data-stu-id="82450-259">Packing an icon image file</span></span>

<span data-ttu-id="82450-260">打包图标图像文件时，需要使用 PackageIcon 属性来指定相对于包根的包路径。</span><span class="sxs-lookup"><span data-stu-id="82450-260">When packing an icon image file, you need to use PackageIcon property to specify the package path, relative to the root of the package.</span></span> <span data-ttu-id="82450-261">此外，还需要确保文件已包含在包中。</span><span class="sxs-lookup"><span data-stu-id="82450-261">In addition, you need to make sure that the file is included in the package.</span></span> <span data-ttu-id="82450-262">图像文件大小限制为 1 MB。</span><span class="sxs-lookup"><span data-stu-id="82450-262">Image file size is limited to 1 MB.</span></span> <span data-ttu-id="82450-263">支持的文件格式包括 JPEG 和 PNG。</span><span class="sxs-lookup"><span data-stu-id="82450-263">Supported file formats include JPEG and PNG.</span></span> <span data-ttu-id="82450-264">建议使用64x64 的图像分辨率。</span><span class="sxs-lookup"><span data-stu-id="82450-264">We recommend an image resolution of 64x64.</span></span>

<span data-ttu-id="82450-265">例如:</span><span class="sxs-lookup"><span data-stu-id="82450-265">For example:</span></span>

```xml
<PropertyGroup>
    ...
    <PackageIcon>icon.png</PackageIcon>
    ...
</PropertyGroup>

<ItemGroup>
    ...
    <None Include="images\icon.png" Pack="true" PackagePath="\"/>
    ...
</ItemGroup>
```

<span data-ttu-id="82450-266">[包图标示例](https://github.com/NuGet/Samples/tree/master/PackageIconExample)。</span><span class="sxs-lookup"><span data-stu-id="82450-266">[Package Icon sample](https://github.com/NuGet/Samples/tree/master/PackageIconExample).</span></span>

<span data-ttu-id="82450-267">对于 nuspec 等效项，请查看[图标的 nuspec 参考](nuspec.md#icon)。</span><span class="sxs-lookup"><span data-stu-id="82450-267">For the nuspec equivalent, take a look at [nuspec reference for icon](nuspec.md#icon).</span></span>

### <a name="output-assemblies"></a><span data-ttu-id="82450-268">输出程序集</span><span class="sxs-lookup"><span data-stu-id="82450-268">Output assemblies</span></span>

<span data-ttu-id="82450-269">`nuget pack` 会复制扩展名为 `.exe`、`.dll`、`.xml`、`.winmd`、`.json` 和 `.pri` 的输出文件。</span><span class="sxs-lookup"><span data-stu-id="82450-269">`nuget pack` copies output files with extensions `.exe`, `.dll`, `.xml`, `.winmd`, `.json`, and `.pri`.</span></span> <span data-ttu-id="82450-270">复制的输出文件取决于 MSBuild 从 `BuiltOutputProjectGroup` 目标提供的内容。</span><span class="sxs-lookup"><span data-stu-id="82450-270">The output files that are copied depend on what MSBuild provides from the `BuiltOutputProjectGroup` target.</span></span>

<span data-ttu-id="82450-271">在项目文件或命令行中，有两种 MSBuild 属性可用于控制输出程序集的位置：</span><span class="sxs-lookup"><span data-stu-id="82450-271">There are two MSBuild  properties that you can use in your project file or command line to control where output assemblies go:</span></span>

- <span data-ttu-id="82450-272">`IncludeBuildOutput`：确定生成输出程序集是否应包含在包中的布尔值。</span><span class="sxs-lookup"><span data-stu-id="82450-272">`IncludeBuildOutput`: A boolean that determines whether the build output assemblies should be included in the package.</span></span>
- <span data-ttu-id="82450-273">`BuildOutputTargetFolder`：指定应在其中放置输出程序集的文件夹。</span><span class="sxs-lookup"><span data-stu-id="82450-273">`BuildOutputTargetFolder`: Specifies the folder in which the output assemblies should be placed.</span></span> <span data-ttu-id="82450-274">输出程序集（和其他输出文件）会复制到各自的框架文件夹中。</span><span class="sxs-lookup"><span data-stu-id="82450-274">The output assemblies (and other output files) are copied into their respective framework folders.</span></span>

### <a name="package-references"></a><span data-ttu-id="82450-275">包引用</span><span class="sxs-lookup"><span data-stu-id="82450-275">Package references</span></span>

<span data-ttu-id="82450-276">请参阅[项目文件中的包引用](../consume-packages/package-references-in-project-files.md)</span><span class="sxs-lookup"><span data-stu-id="82450-276">See [Package References in Project Files](../consume-packages/package-references-in-project-files.md).</span></span>

### <a name="project-to-project-references"></a><span data-ttu-id="82450-277">项目到项目的引用</span><span class="sxs-lookup"><span data-stu-id="82450-277">Project to project references</span></span>

<span data-ttu-id="82450-278">默认情况下，项目到项目的引用被视为 nuget 包引用，例如：</span><span class="sxs-lookup"><span data-stu-id="82450-278">Project to project references are considered by default as nuget package references, for example:</span></span>

```xml
<ProjectReference Include="..\UwpLibrary2\UwpLibrary2.csproj"/>
```

<span data-ttu-id="82450-279">也可将以下元数据添加到项目引用：</span><span class="sxs-lookup"><span data-stu-id="82450-279">You can also add the following metadata to your project reference:</span></span>

```xml
<IncludeAssets>
<ExcludeAssets>
<PrivateAssets>
```

### <a name="deterministic"></a><span data-ttu-id="82450-280">Deterministic</span><span class="sxs-lookup"><span data-stu-id="82450-280">Deterministic</span></span>

<span data-ttu-id="82450-281">使用`MSBuild -t:pack -p:Deterministic=true`时，包目标的多个调用将生成完全相同的包。</span><span class="sxs-lookup"><span data-stu-id="82450-281">When using `MSBuild -t:pack -p:Deterministic=true`, multiple invocations of the the pack target will generate the exact same package.</span></span>
<span data-ttu-id="82450-282">Pack 命令的输出不受计算机的环境状态影响。</span><span class="sxs-lookup"><span data-stu-id="82450-282">The output of the pack command is not affected by the ambient state of the machine.</span></span> <span data-ttu-id="82450-283">特别是 zip 条目的时间戳为1980-01-01。</span><span class="sxs-lookup"><span data-stu-id="82450-283">Specifically zip entries will be timestamped as 1980-01-01.</span></span> <span data-ttu-id="82450-284">若要实现完全确定性，应通过相应的编译器选项（[确定性](/dotnet/csharp/language-reference/compiler-options/deterministic-compiler-option)）生成程序集。</span><span class="sxs-lookup"><span data-stu-id="82450-284">To achieve full determinism, the assemblies should be built with the respective compiler option [-deterministic](/dotnet/csharp/language-reference/compiler-options/deterministic-compiler-option).</span></span>
<span data-ttu-id="82450-285">建议指定如下所示的确定性属性，以便编译器和 NuGet 都遵守此类属性。</span><span class="sxs-lookup"><span data-stu-id="82450-285">It is recommended that you specify the deterministic property like following, so both the compiler and NuGet will respect it.</span></span>

```xml
<PropertyGroup>
  <Deterministic>true</Deterministic>
</PropertyGroup>
```

### <a name="including-content-in-a-package"></a><span data-ttu-id="82450-286">在包中添加内容</span><span class="sxs-lookup"><span data-stu-id="82450-286">Including content in a package</span></span>

<span data-ttu-id="82450-287">若要添加内容，请将额外的元数据添加到现有的 `<Content>` 项。</span><span class="sxs-lookup"><span data-stu-id="82450-287">To include content, add extra metadata to the existing `<Content>` item.</span></span> <span data-ttu-id="82450-288">默认情况下，类型“Content”的所有内容都包括在包中，除非使用以下条目替代：</span><span class="sxs-lookup"><span data-stu-id="82450-288">By default everything of type "Content" gets included in the package unless you override with entries like the following:</span></span>

 ```xml
<Content Include="..\win7-x64\libuv.txt">
  <Pack>false</Pack>
</Content>
 ```

<span data-ttu-id="82450-289">默认情况下，所有内容都添加到包中 `content` 和 `contentFiles\any\<target_framework>` 文件夹根目录，并保留相对文件夹结构，除非指定包路径：</span><span class="sxs-lookup"><span data-stu-id="82450-289">By default, everything gets added to the root of the `content` and `contentFiles\any\<target_framework>` folder within a package and preserves the relative folder structure, unless you specify a package path:</span></span>

```xml
<Content Include="..\win7-x64\libuv.txt">
  <Pack>true</Pack>
  <PackagePath>content\myfiles\</PackagePath>
</Content>
```

<span data-ttu-id="82450-290">如果仅希望将所有内容都复制到特定根文件夹（而不是 `content` 和 `contentFiles`），可使用 MSBuild 属性 `ContentTargetFolders`，其默认值为“content;contentFiles”，但可以设置为任何其他文件夹名称。</span><span class="sxs-lookup"><span data-stu-id="82450-290">If you want to copy all your content to only a specific root folder(s) (instead of `content` and `contentFiles` both), you can use the MSBuild property `ContentTargetFolders`, which defaults to "content;contentFiles" but can be set to any other folder names.</span></span> <span data-ttu-id="82450-291">请注意，基于 `buildAction`，仅在 `ContentTargetFolders` 中指定“contentFiles”会将文件置于 `contentFiles\any\<target_framework>` 或 `contentFiles\<language>\<target_framework>` 下。</span><span class="sxs-lookup"><span data-stu-id="82450-291">Note that just specifying "contentFiles" in `ContentTargetFolders` puts files under `contentFiles\any\<target_framework>` or `contentFiles\<language>\<target_framework>` based on `buildAction`.</span></span>

<span data-ttu-id="82450-292">`PackagePath` 可以是一组以分号分隔的目标路径。</span><span class="sxs-lookup"><span data-stu-id="82450-292">`PackagePath` can be a semicolon-delimited set of target paths.</span></span> <span data-ttu-id="82450-293">指定空的包路径会将文件添加到包的根目录。</span><span class="sxs-lookup"><span data-stu-id="82450-293">Specifying an empty package path would add the file to the root of the package.</span></span> <span data-ttu-id="82450-294">例如，以下操作会将 `libuv.txt` 添加到 `content\myfiles`、`content\samples` 和包的根目录：</span><span class="sxs-lookup"><span data-stu-id="82450-294">For example, the following adds `libuv.txt` to `content\myfiles`, `content\samples`, and the package root:</span></span>

```xml
<Content Include="..\win7-x64\libuv.txt">
  <Pack>true</Pack>
  <PackagePath>content\myfiles;content\sample;;</PackagePath>
</Content>
```

<span data-ttu-id="82450-295">另外还有 MSBuild 属性 `$(IncludeContentInPack)`，默认值为 `true`。</span><span class="sxs-lookup"><span data-stu-id="82450-295">There is also an MSBuild property `$(IncludeContentInPack)`, which defaults to `true`.</span></span> <span data-ttu-id="82450-296">如果在任何项目中将此值设置为 `false`，则该项目的内容不会包括在 nuget 包中。</span><span class="sxs-lookup"><span data-stu-id="82450-296">If this is set to `false` on any project, then the content from that project are not included in the nuget package.</span></span>

<span data-ttu-id="82450-297">其他可在任何上述项上设置的特定于包的元数据包括 ```<PackageCopyToOutput>``` 和 ```<PackageFlatten>```，后者在输出 nuspec 中的 ```contentFiles``` 条目上设置 ```CopyToOutput``` 和 ```Flatten``` 值。</span><span class="sxs-lookup"><span data-stu-id="82450-297">Other pack specific metadata that you can set on any of the above items includes ```<PackageCopyToOutput>``` and ```<PackageFlatten>``` which sets ```CopyToOutput``` and ```Flatten``` values on the ```contentFiles``` entry in the output nuspec.</span></span>

> [!Note]
> <span data-ttu-id="82450-298">除了“Content”项，`<Pack>` 和 `<PackagePath>` 元数据还可以在具有 Compile、EmbeddedResource、ApplicationDefinition、Page、Resource、SplashScreen、DesignData、DesignDataWithDesignTimeCreateableTypes、CodeAnalysisDictionary、AndroidAsset、AndroidResource、BundleResource 或 None 生成操作的文件上进行设置。</span><span class="sxs-lookup"><span data-stu-id="82450-298">Apart from Content items, the `<Pack>` and `<PackagePath>` metadata can also be set on files with a build action of Compile, EmbeddedResource, ApplicationDefinition, Page, Resource, SplashScreen, DesignData, DesignDataWithDesignTimeCreateableTypes, CodeAnalysisDictionary, AndroidAsset, AndroidResource, BundleResource or None.</span></span>
>
> <span data-ttu-id="82450-299">使用通配模式时，对于将包的文件名追加到包路径，包路径必须以文件夹分隔符结尾，否则包路径将被视为包括文件名的完整路径。</span><span class="sxs-lookup"><span data-stu-id="82450-299">For pack to append the filename to your package path when using globbing patterns, your package path must end with the folder separator character, otherwise the package path is treated as the full path including the file name.</span></span>

### <a name="includesymbols"></a><span data-ttu-id="82450-300">IncludeSymbols</span><span class="sxs-lookup"><span data-stu-id="82450-300">IncludeSymbols</span></span>

<span data-ttu-id="82450-301">使用 `MSBuild -t:pack -p:IncludeSymbols=true` 时，相应的 `.pdb` 文件将随其他输出文件（`.dll`、`.exe`、`.winmd`、`.xml`、`.json`、`.pri`）一起复制。</span><span class="sxs-lookup"><span data-stu-id="82450-301">When using `MSBuild -t:pack -p:IncludeSymbols=true`, the corresponding `.pdb` files are copied along with other output files (`.dll`, `.exe`, `.winmd`, `.xml`, `.json`, `.pri`).</span></span> <span data-ttu-id="82450-302">请注意，设置 `IncludeSymbols=true` 会创建常规包和符号包。</span><span class="sxs-lookup"><span data-stu-id="82450-302">Note that setting `IncludeSymbols=true` creates a regular package *and* a symbols package.</span></span>

### <a name="includesource"></a><span data-ttu-id="82450-303">IncludeSource</span><span class="sxs-lookup"><span data-stu-id="82450-303">IncludeSource</span></span>

<span data-ttu-id="82450-304">这与 `IncludeSymbols` 相同，但它还会连同 `.pdb` 文件复制源文件。</span><span class="sxs-lookup"><span data-stu-id="82450-304">This is the same as `IncludeSymbols`, except that it copies source files along with `.pdb` files as well.</span></span> <span data-ttu-id="82450-305">类型为 `Compile` 的所有文件都会复制到 `src\<ProjectName>\`，并保留生成包中的相对路径文件夹结构。</span><span class="sxs-lookup"><span data-stu-id="82450-305">All files of type `Compile` are copied over to `src\<ProjectName>\` preserving the relative path folder structure in the resulting package.</span></span> <span data-ttu-id="82450-306">对于将 `TreatAsPackageReference` 设置为 `false` 的任何 `ProjectReference` 的源文件也是如此。</span><span class="sxs-lookup"><span data-stu-id="82450-306">The same also happens for source files of any `ProjectReference` which has `TreatAsPackageReference` set to `false`.</span></span>

<span data-ttu-id="82450-307">如果类型为 Compile 的文件位于项目文件夹外，则它只添加到了 `src\<ProjectName>\`。</span><span class="sxs-lookup"><span data-stu-id="82450-307">If a file of type Compile, is outside the project folder, then it's just added to `src\<ProjectName>\`.</span></span>

### <a name="packing-a-license-expression-or-a-license-file"></a><span data-ttu-id="82450-308">打包许可证表达式或许可证文件</span><span class="sxs-lookup"><span data-stu-id="82450-308">Packing a license expression or a license file</span></span>

<span data-ttu-id="82450-309">使用许可证表达式时，应使用 PackageLicenseExpression 属性。</span><span class="sxs-lookup"><span data-stu-id="82450-309">When using a license expression, the PackageLicenseExpression property should be used.</span></span> 
<span data-ttu-id="82450-310">[许可证表达式示例](https://github.com/NuGet/Samples/tree/master/PackageLicenseExpressionExample)。</span><span class="sxs-lookup"><span data-stu-id="82450-310">[License expression sample](https://github.com/NuGet/Samples/tree/master/PackageLicenseExpressionExample).</span></span>

```xml
<PropertyGroup>
    <PackageLicenseExpression>MIT</PackageLicenseExpression>
</PropertyGroup>
```

<span data-ttu-id="82450-311">[了解有关 NuGet.org 所接受的许可证表达式和许可证的详细信息](nuspec.md#license)。</span><span class="sxs-lookup"><span data-stu-id="82450-311">[Learn more about license expressions and licenses that are accepted by NuGet.org](nuspec.md#license).</span></span>

<span data-ttu-id="82450-312">打包许可证文件时，需要使用 PackageLicenseFile 属性来指定相对于包根的包路径。</span><span class="sxs-lookup"><span data-stu-id="82450-312">When packing a license file, you need to use PackageLicenseFile property to specify the package path, relative to the root of the package.</span></span> <span data-ttu-id="82450-313">此外，还需要确保文件已包含在包中。</span><span class="sxs-lookup"><span data-stu-id="82450-313">In addition, you need to make sure that the file is included in the package.</span></span> <span data-ttu-id="82450-314">例如：</span><span class="sxs-lookup"><span data-stu-id="82450-314">For example:</span></span>

```xml
<PropertyGroup>
    <PackageLicenseFile>LICENSE.txt</PackageLicenseFile>
</PropertyGroup>

<ItemGroup>
    <None Include="licenses\LICENSE.txt" Pack="true" PackagePath=""/>
</ItemGroup>
```

<span data-ttu-id="82450-315">[许可证文件示例](https://github.com/NuGet/Samples/tree/master/PackageLicenseFileExample)。</span><span class="sxs-lookup"><span data-stu-id="82450-315">[License file sample](https://github.com/NuGet/Samples/tree/master/PackageLicenseFileExample).</span></span>

### <a name="istool"></a><span data-ttu-id="82450-316">IsTool</span><span class="sxs-lookup"><span data-stu-id="82450-316">IsTool</span></span>

<span data-ttu-id="82450-317">使用 `MSBuild -t:pack -p:IsTool=true` 时，所有输出文件（如[输出程序集](#output-assemblies)方案中所指定）都被复制到 `tools` 文件夹，而不是 `lib` 文件夹。</span><span class="sxs-lookup"><span data-stu-id="82450-317">When using `MSBuild -t:pack -p:IsTool=true`, all output files, as specified in the [Output Assemblies](#output-assemblies) scenario, are copied to the `tools` folder instead of the `lib` folder.</span></span> <span data-ttu-id="82450-318">请注意，这不同于 `DotNetCliTool`，后者通过在 `.csproj` 文件中设置 `PackageType` 进行指定。</span><span class="sxs-lookup"><span data-stu-id="82450-318">Note that this is different from a `DotNetCliTool` which is specified by setting the `PackageType` in `.csproj` file.</span></span>

### <a name="packing-using-a-nuspec"></a><span data-ttu-id="82450-319">使用 .nuspec 打包</span><span class="sxs-lookup"><span data-stu-id="82450-319">Packing using a .nuspec</span></span>

<span data-ttu-id="82450-320">尽管建议你改为在项目文件中包含通常在`.nuspec`文件中的[所有属性](../reference/msbuild-targets.md#pack-target)，但你可以`.nuspec`选择使用文件打包项目。</span><span class="sxs-lookup"><span data-stu-id="82450-320">Although it is recommended that you [include all the properties](../reference/msbuild-targets.md#pack-target) that are usually in the `.nuspec` file in the project file instead, you can choose to use a `.nuspec` file to pack your project.</span></span> <span data-ttu-id="82450-321">对于使用`PackageReference`的非 SDK 样式项目，必须导入`NuGet.Build.Tasks.Pack.targets` ，以便可以执行 pack 任务。</span><span class="sxs-lookup"><span data-stu-id="82450-321">For a non-SDK-style project that uses `PackageReference`, you must import `NuGet.Build.Tasks.Pack.targets` so that the pack task can be executed.</span></span> <span data-ttu-id="82450-322">你仍需要还原项目，然后才能打包 nuspec 文件。</span><span class="sxs-lookup"><span data-stu-id="82450-322">You still need to restore the project before you can pack a nuspec file.</span></span> <span data-ttu-id="82450-323">（默认情况下，SDK 样式项目包括包目标。）</span><span class="sxs-lookup"><span data-stu-id="82450-323">(An SDK-style project includes the pack targets by default.)</span></span>

<span data-ttu-id="82450-324">项目文件的目标框架不相关，并且不会在对 nuspec 进行打包时使用。</span><span class="sxs-lookup"><span data-stu-id="82450-324">The target framework of the project file is irrelevant and not used when packing a nuspec.</span></span> <span data-ttu-id="82450-325">以下三个 MSBuild 属性与使用 `.nuspec` 的打包相关：</span><span class="sxs-lookup"><span data-stu-id="82450-325">The following three MSBuild properties are relevant to packing using a `.nuspec`:</span></span>

1. <span data-ttu-id="82450-326">`NuspecFile`：用于打包的 `.nuspec` 文件的相对或绝对路径。</span><span class="sxs-lookup"><span data-stu-id="82450-326">`NuspecFile`: relative or absolute path to the `.nuspec` file being used for packing.</span></span>
1. <span data-ttu-id="82450-327">`NuspecProperties`：键=值对的分号分隔列表。</span><span class="sxs-lookup"><span data-stu-id="82450-327">`NuspecProperties`: a semicolon-separated list of key=value pairs.</span></span> <span data-ttu-id="82450-328">由于 MSBuild 命令行分析工作的方式，必须指定多个属性，如下所示：`-p:NuspecProperties=\"key1=value1;key2=value2\"`。</span><span class="sxs-lookup"><span data-stu-id="82450-328">Due to the way MSBuild command-line parsing works, multiple properties must be specified as follows: `-p:NuspecProperties=\"key1=value1;key2=value2\"`.</span></span>  
1. <span data-ttu-id="82450-329">`NuspecBasePath`：`.nuspec`文件的基路径。</span><span class="sxs-lookup"><span data-stu-id="82450-329">`NuspecBasePath`: Base path for the `.nuspec` file.</span></span>

<span data-ttu-id="82450-330">如果使用 `dotnet.exe` 打包项目，请使用类似于下面的命令：</span><span class="sxs-lookup"><span data-stu-id="82450-330">If using `dotnet.exe` to pack your project, use a command like the following:</span></span>

```cli
dotnet pack <path to .csproj file> -p:NuspecFile=<path to nuspec file> -p:NuspecProperties=<> -p:NuspecBasePath=<Base path> 
```

<span data-ttu-id="82450-331">如果使用 MSBuild 打包项目，请使用类似于下面的命令：</span><span class="sxs-lookup"><span data-stu-id="82450-331">If using MSBuild to pack your project, use a command like the following:</span></span>

```cli
msbuild -t:pack <path to .csproj file> -p:NuspecFile=<path to nuspec file> -p:NuspecProperties=<> -p:NuspecBasePath=<Base path> 
```

<span data-ttu-id="82450-332">请注意，使用 dotnet 或 msbuild 打包 nuspec 在默认情况下也会导致生成项目。</span><span class="sxs-lookup"><span data-stu-id="82450-332">Please note that packing a nuspec using dotnet.exe or msbuild also leads to building the project by default.</span></span> <span data-ttu-id="82450-333">通过将属性传递```--no-build```给 dotnet，可以避免这种情况，它与```<IncludeBuildOutput>false</IncludeBuildOutput> ```项目文件中```<NoBuild>true</NoBuild> ```的设置以及项目文件中的设置等效。</span><span class="sxs-lookup"><span data-stu-id="82450-333">This can be avoided by passing ```--no-build``` property to dotnet.exe, which is the equivalent of setting ```<NoBuild>true</NoBuild> ``` in your project file, along with setting ```<IncludeBuildOutput>false</IncludeBuildOutput> ``` in the project file.</span></span>

<span data-ttu-id="82450-334">用于打包 nuspec 文件的 *.csproj*文件的示例如下：</span><span class="sxs-lookup"><span data-stu-id="82450-334">An example of a *.csproj* file to pack a nuspec file is:</span></span>

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

### <a name="advanced-extension-points-to-create-customized-package"></a><span data-ttu-id="82450-335">用于创建自定义包的高级扩展点</span><span class="sxs-lookup"><span data-stu-id="82450-335">Advanced extension points to create customized package</span></span>

<span data-ttu-id="82450-336">`pack`目标提供两个扩展点，这些点在内部特定于目标框架的生成中运行。</span><span class="sxs-lookup"><span data-stu-id="82450-336">The `pack` target provides two extension points that run in the inner, target framework specific build.</span></span> <span data-ttu-id="82450-337">扩展点支持包括特定于目标框架的内容和程序集到包中：</span><span class="sxs-lookup"><span data-stu-id="82450-337">The extension points support including target framework specific content and assemblies into a package:</span></span>

- <span data-ttu-id="82450-338">`TargetsForTfmSpecificBuildOutput`靶使用`lib`文件夹中的文件或使用`BuildOutputTargetFolder`指定的文件夹。</span><span class="sxs-lookup"><span data-stu-id="82450-338">`TargetsForTfmSpecificBuildOutput` target: Use for files inside the `lib` folder or a folder specified using `BuildOutputTargetFolder`.</span></span>
- <span data-ttu-id="82450-339">`TargetsForTfmSpecificContentInPackage`靶用于之外`BuildOutputTargetFolder`的文件。</span><span class="sxs-lookup"><span data-stu-id="82450-339">`TargetsForTfmSpecificContentInPackage` target: Use for files outside the `BuildOutputTargetFolder`.</span></span>

#### <a name="targetsfortfmspecificbuildoutput"></a><span data-ttu-id="82450-340">TargetsForTfmSpecificBuildOutput</span><span class="sxs-lookup"><span data-stu-id="82450-340">TargetsForTfmSpecificBuildOutput</span></span>

<span data-ttu-id="82450-341">编写自定义目标并将其指定为`$(TargetsForTfmSpecificBuildOutput)`属性的值。</span><span class="sxs-lookup"><span data-stu-id="82450-341">Write a custom target and specify it as the value of the `$(TargetsForTfmSpecificBuildOutput)` property.</span></span> <span data-ttu-id="82450-342">对于需要进入的`BuildOutputTargetFolder`任何文件（默认情况下为 lib），目标应将这些文件写入 ItemGroup `BuildOutputInPackage` ，并设置以下两个元数据值：</span><span class="sxs-lookup"><span data-stu-id="82450-342">For any files that need to go into the `BuildOutputTargetFolder` (lib by default), the target should write those files into the ItemGroup `BuildOutputInPackage` and set the following two metadata values:</span></span>

- <span data-ttu-id="82450-343">`FinalOutputPath`：文件的绝对路径;如果未提供，则标识用于计算源路径。</span><span class="sxs-lookup"><span data-stu-id="82450-343">`FinalOutputPath`: The absolute path of the file; if not provided, the Identity is used to evaluate source path.</span></span>
- <span data-ttu-id="82450-344">`TargetPath`：可有可无当文件需要进入中`lib\<TargetFramework>`的子文件夹时设置，就像在其各自的区域性文件夹下的附属程序集。</span><span class="sxs-lookup"><span data-stu-id="82450-344">`TargetPath`:  (Optional) Set when the file needs to go into a subfolder within `lib\<TargetFramework>` , like satellite assemblies that go under their respective culture folders.</span></span> <span data-ttu-id="82450-345">默认为文件的名称。</span><span class="sxs-lookup"><span data-stu-id="82450-345">Defaults to the name of the file.</span></span>

<span data-ttu-id="82450-346">示例：</span><span class="sxs-lookup"><span data-stu-id="82450-346">Example:</span></span>

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

#### <a name="targetsfortfmspecificcontentinpackage"></a><span data-ttu-id="82450-347">TargetsForTfmSpecificContentInPackage</span><span class="sxs-lookup"><span data-stu-id="82450-347">TargetsForTfmSpecificContentInPackage</span></span>

<span data-ttu-id="82450-348">编写自定义目标并将其指定为`$(TargetsForTfmSpecificContentInPackage)`属性的值。</span><span class="sxs-lookup"><span data-stu-id="82450-348">Write a custom target and specify it as the value of the `$(TargetsForTfmSpecificContentInPackage)` property.</span></span> <span data-ttu-id="82450-349">对于要包含在包中的任何文件，目标应将这些文件写入 ItemGroup `TfmSpecificPackageFile` ，并设置以下可选的元数据：</span><span class="sxs-lookup"><span data-stu-id="82450-349">For any files to include in the package, the target should write those files into the ItemGroup `TfmSpecificPackageFile` and set the following optional metadata:</span></span>

- <span data-ttu-id="82450-350">`PackagePath`：包中应输出文件的路径。</span><span class="sxs-lookup"><span data-stu-id="82450-350">`PackagePath`: Path where the file should be output in the package.</span></span> <span data-ttu-id="82450-351">如果将多个文件添加到同一个包路径，NuGet 将发出警告。</span><span class="sxs-lookup"><span data-stu-id="82450-351">NuGet issues a warning if more than one file is added to the same package path.</span></span>
- <span data-ttu-id="82450-352">`BuildAction`：要分配给文件的生成操作，只有当包路径在`contentFiles`文件夹中时才是必需的。</span><span class="sxs-lookup"><span data-stu-id="82450-352">`BuildAction`: The build action to assign to the file, required only if the package path is in the `contentFiles` folder.</span></span> <span data-ttu-id="82450-353">默认值为 "None"。</span><span class="sxs-lookup"><span data-stu-id="82450-353">Defaults to "None".</span></span>

<span data-ttu-id="82450-354">例如：</span><span class="sxs-lookup"><span data-stu-id="82450-354">An example:</span></span>
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

## <a name="restore-target"></a><span data-ttu-id="82450-355">还原目标</span><span class="sxs-lookup"><span data-stu-id="82450-355">restore target</span></span>

<span data-ttu-id="82450-356">`MSBuild -t:restore`（`nuget restore` 和 `dotnet restore` 与 .NET Core 项目一起使用）会还原项目文件中引用的包，如下所示：</span><span class="sxs-lookup"><span data-stu-id="82450-356">`MSBuild -t:restore` (which `nuget restore` and `dotnet restore` use with .NET Core projects), restores packages referenced in the project file as follows:</span></span>

1. <span data-ttu-id="82450-357">读取所有项目到项目的引用</span><span class="sxs-lookup"><span data-stu-id="82450-357">Read all project to project references</span></span>
1. <span data-ttu-id="82450-358">读取项目属性以查找中间文件夹和目标框架</span><span class="sxs-lookup"><span data-stu-id="82450-358">Read the project properties to find the intermediate folder and target frameworks</span></span>
1. <span data-ttu-id="82450-359">将 MSBuild 数据传递到 NuGet。生成 .dll</span><span class="sxs-lookup"><span data-stu-id="82450-359">Pass MSBuild data to NuGet.Build.Tasks.dll</span></span>
1. <span data-ttu-id="82450-360">运行还原</span><span class="sxs-lookup"><span data-stu-id="82450-360">Run restore</span></span>
1. <span data-ttu-id="82450-361">下载包</span><span class="sxs-lookup"><span data-stu-id="82450-361">Download packages</span></span>
1. <span data-ttu-id="82450-362">编写资产文件、目标和属性</span><span class="sxs-lookup"><span data-stu-id="82450-362">Write assets file, targets, and props</span></span>

<span data-ttu-id="82450-363">目标仅适用于使用 PackageReference 格式的项目。 `restore`</span><span class="sxs-lookup"><span data-stu-id="82450-363">The `restore` target works **only** for projects using the PackageReference format.</span></span> <span data-ttu-id="82450-364">它不适**用于**使用`packages.config`格式的项目; 请改用[nuget 还原](../reference/cli-reference/cli-ref-restore.md)。</span><span class="sxs-lookup"><span data-stu-id="82450-364">It does **not** work for projects using the `packages.config` format; use [nuget restore](../reference/cli-reference/cli-ref-restore.md) instead.</span></span>

### <a name="restore-properties"></a><span data-ttu-id="82450-365">还原属性</span><span class="sxs-lookup"><span data-stu-id="82450-365">Restore properties</span></span>

<span data-ttu-id="82450-366">其他的还原设置可能来自项目文件中的 MSBuild 属性。</span><span class="sxs-lookup"><span data-stu-id="82450-366">Additional restore settings may come from MSBuild properties in the project file.</span></span> <span data-ttu-id="82450-367">还可以从命令行使用 `-p:` 开关设置值（请参阅以下示例）。</span><span class="sxs-lookup"><span data-stu-id="82450-367">Values can also be set from the command line using the `-p:` switch (see Examples below).</span></span>

| <span data-ttu-id="82450-368">Property</span><span class="sxs-lookup"><span data-stu-id="82450-368">Property</span></span> | <span data-ttu-id="82450-369">描述</span><span class="sxs-lookup"><span data-stu-id="82450-369">Description</span></span> |
|--------|--------|
| <span data-ttu-id="82450-370">RestoreSources</span><span class="sxs-lookup"><span data-stu-id="82450-370">RestoreSources</span></span> | <span data-ttu-id="82450-371">以分号分隔的包源列表。</span><span class="sxs-lookup"><span data-stu-id="82450-371">Semicolon-delimited list of package sources.</span></span> |
| <span data-ttu-id="82450-372">RestorePackagesPath</span><span class="sxs-lookup"><span data-stu-id="82450-372">RestorePackagesPath</span></span> | <span data-ttu-id="82450-373">用户包文件夹路径。</span><span class="sxs-lookup"><span data-stu-id="82450-373">User packages folder path.</span></span> |
| <span data-ttu-id="82450-374">RestoreDisableParallel</span><span class="sxs-lookup"><span data-stu-id="82450-374">RestoreDisableParallel</span></span> | <span data-ttu-id="82450-375">将下载限制为一次一个。</span><span class="sxs-lookup"><span data-stu-id="82450-375">Limit downloads to one at a time.</span></span> |
| <span data-ttu-id="82450-376">RestoreConfigFile</span><span class="sxs-lookup"><span data-stu-id="82450-376">RestoreConfigFile</span></span> | <span data-ttu-id="82450-377">要应用的 `Nuget.Config` 文件的路径。</span><span class="sxs-lookup"><span data-stu-id="82450-377">Path to a `Nuget.Config` file to apply.</span></span> |
| <span data-ttu-id="82450-378">RestoreNoCache</span><span class="sxs-lookup"><span data-stu-id="82450-378">RestoreNoCache</span></span> | <span data-ttu-id="82450-379">如果为 true，则避免使用缓存的包。</span><span class="sxs-lookup"><span data-stu-id="82450-379">If true, avoids using cached packages.</span></span> <span data-ttu-id="82450-380">请参阅[管理全局包和缓存文件夹](../consume-packages/managing-the-global-packages-and-cache-folders.md)。</span><span class="sxs-lookup"><span data-stu-id="82450-380">See [Managing the global packages and cache folders](../consume-packages/managing-the-global-packages-and-cache-folders.md).</span></span> |
| <span data-ttu-id="82450-381">RestoreIgnoreFailedSources</span><span class="sxs-lookup"><span data-stu-id="82450-381">RestoreIgnoreFailedSources</span></span> | <span data-ttu-id="82450-382">如果为“true”，则忽略失败或丢失的包源。</span><span class="sxs-lookup"><span data-stu-id="82450-382">If true, ignores failing or missing package sources.</span></span> |
| <span data-ttu-id="82450-383">RestoreFallbackFolders</span><span class="sxs-lookup"><span data-stu-id="82450-383">RestoreFallbackFolders</span></span> | <span data-ttu-id="82450-384">后备文件夹，其使用方式与使用 "用户包" 文件夹的方式相同。</span><span class="sxs-lookup"><span data-stu-id="82450-384">Fallback folders, used in the same way the user packages folder is used.</span></span> |
| <span data-ttu-id="82450-385">RestoreAdditionalProjectSources</span><span class="sxs-lookup"><span data-stu-id="82450-385">RestoreAdditionalProjectSources</span></span> | <span data-ttu-id="82450-386">要在还原期间使用的其他源。</span><span class="sxs-lookup"><span data-stu-id="82450-386">Additional sources to use during restore.</span></span> |
| <span data-ttu-id="82450-387">RestoreAdditionalProjectFallbackFolders</span><span class="sxs-lookup"><span data-stu-id="82450-387">RestoreAdditionalProjectFallbackFolders</span></span> | <span data-ttu-id="82450-388">要在还原期间使用的其他回退文件夹。</span><span class="sxs-lookup"><span data-stu-id="82450-388">Additional fallback folders to use during restore.</span></span> |
| <span data-ttu-id="82450-389">RestoreAdditionalProjectFallbackFoldersExcludes</span><span class="sxs-lookup"><span data-stu-id="82450-389">RestoreAdditionalProjectFallbackFoldersExcludes</span></span> | <span data-ttu-id="82450-390">排除其中指定的回退文件夹`RestoreAdditionalProjectFallbackFolders`</span><span class="sxs-lookup"><span data-stu-id="82450-390">Excludes fallback folders specified in `RestoreAdditionalProjectFallbackFolders`</span></span> |
| <span data-ttu-id="82450-391">RestoreTaskAssemblyFile</span><span class="sxs-lookup"><span data-stu-id="82450-391">RestoreTaskAssemblyFile</span></span> | <span data-ttu-id="82450-392">`NuGet.Build.Tasks.dll` 的路径。</span><span class="sxs-lookup"><span data-stu-id="82450-392">Path to `NuGet.Build.Tasks.dll`.</span></span> |
| <span data-ttu-id="82450-393">RestoreGraphProjectInput</span><span class="sxs-lookup"><span data-stu-id="82450-393">RestoreGraphProjectInput</span></span> | <span data-ttu-id="82450-394">要还原的以分号分隔的项目列表，其中应包含绝对路径。</span><span class="sxs-lookup"><span data-stu-id="82450-394">Semicolon-delimited list of projects to restore, which should contain absolute paths.</span></span> |
| <span data-ttu-id="82450-395">RestoreUseSkipNonexistentTargets</span><span class="sxs-lookup"><span data-stu-id="82450-395">RestoreUseSkipNonexistentTargets</span></span>  | <span data-ttu-id="82450-396">通过 MSBuild 收集项目后，它将确定是否使用`SkipNonexistentTargets`优化来收集这些项目。</span><span class="sxs-lookup"><span data-stu-id="82450-396">When the projects are collected via MSBuild it determines whether they are collected using the `SkipNonexistentTargets` optimization.</span></span> <span data-ttu-id="82450-397">如果未设置，则默认`true`为。</span><span class="sxs-lookup"><span data-stu-id="82450-397">When not set, defaults to `true`.</span></span> <span data-ttu-id="82450-398">如果无法导入项目的目标，则结果是一个故障快速的行为。</span><span class="sxs-lookup"><span data-stu-id="82450-398">The consequence is a fail-fast behavior when a project's targets cannot be imported.</span></span> |
| <span data-ttu-id="82450-399">MSBuildProjectExtensionsPath</span><span class="sxs-lookup"><span data-stu-id="82450-399">MSBuildProjectExtensionsPath</span></span> | <span data-ttu-id="82450-400">Output 文件夹，默认为`BaseIntermediateOutputPath` `obj`和文件夹。</span><span class="sxs-lookup"><span data-stu-id="82450-400">Output folder, defaulting to `BaseIntermediateOutputPath` and the `obj` folder.</span></span> |

#### <a name="examples"></a><span data-ttu-id="82450-401">示例</span><span class="sxs-lookup"><span data-stu-id="82450-401">Examples</span></span>

<span data-ttu-id="82450-402">命令行：</span><span class="sxs-lookup"><span data-stu-id="82450-402">Command line:</span></span>

```cli
msbuild -t:restore -p:RestoreConfigFile=<path>
```

<span data-ttu-id="82450-403">项目文件：</span><span class="sxs-lookup"><span data-stu-id="82450-403">Project file:</span></span>

```xml
<PropertyGroup>
    <RestoreIgnoreFailedSource>true</RestoreIgnoreFailedSource>
</PropertyGroup>
```

### <a name="restore-outputs"></a><span data-ttu-id="82450-404">还原输出</span><span class="sxs-lookup"><span data-stu-id="82450-404">Restore outputs</span></span>

<span data-ttu-id="82450-405">还原会在生成 `obj` 文件夹中创建以下文件：</span><span class="sxs-lookup"><span data-stu-id="82450-405">Restore creates the following files in the build `obj` folder:</span></span>

| <span data-ttu-id="82450-406">文件</span><span class="sxs-lookup"><span data-stu-id="82450-406">File</span></span> | <span data-ttu-id="82450-407">描述</span><span class="sxs-lookup"><span data-stu-id="82450-407">Description</span></span> |
|--------|--------|
| `project.assets.json` | <span data-ttu-id="82450-408">包含所有包引用的依赖项关系图。</span><span class="sxs-lookup"><span data-stu-id="82450-408">Contains the dependency graph of all package references.</span></span> |
| `{projectName}.projectFileExtension.nuget.g.props` | <span data-ttu-id="82450-409">包中包含的对 MSBuild 属性的引用</span><span class="sxs-lookup"><span data-stu-id="82450-409">References to MSBuild props contained in packages</span></span> |
| `{projectName}.projectFileExtension.nuget.g.targets` | <span data-ttu-id="82450-410">包中包含的对 MSBuild 目标的引用</span><span class="sxs-lookup"><span data-stu-id="82450-410">References to MSBuild targets contained in packages</span></span> |

### <a name="restoring-and-building-with-one-msbuild-command"></a><span data-ttu-id="82450-411">通过一个 MSBuild 命令进行还原和生成</span><span class="sxs-lookup"><span data-stu-id="82450-411">Restoring and building with one MSBuild command</span></span>

<span data-ttu-id="82450-412">由于 NuGet 可以还原引入 MSBuild 目标和属性的包，因此，还原和生成评估将以不同的全局属性运行。</span><span class="sxs-lookup"><span data-stu-id="82450-412">Due to the fact that NuGet can restore packages that bring down MSBuild targets and props, the restore and build evaluations are run with different global properties.</span></span>
<span data-ttu-id="82450-413">这意味着，以下操作将具有不可预测且通常不正确的行为。</span><span class="sxs-lookup"><span data-stu-id="82450-413">This means that the following will have an unpredictable and often incorrect behavior.</span></span>

```cli
msbuild -t:restore,build
```

 <span data-ttu-id="82450-414">相反，推荐的方法是：</span><span class="sxs-lookup"><span data-stu-id="82450-414">Instead the recommended approach is:</span></span>

```cli
msbuild -t:build -restore
```

<span data-ttu-id="82450-415">相同的逻辑也适用于类似于`build`的其他目标。</span><span class="sxs-lookup"><span data-stu-id="82450-415">The same logic applies to other targets similar to `build`.</span></span>

### <a name="packagetargetfallback"></a><span data-ttu-id="82450-416">PackageTargetFallback</span><span class="sxs-lookup"><span data-stu-id="82450-416">PackageTargetFallback</span></span>

<span data-ttu-id="82450-417">`PackageTargetFallback` 元素可用于指定要在还原包时使用的一组兼容目标。</span><span class="sxs-lookup"><span data-stu-id="82450-417">The `PackageTargetFallback` element allows you to specify a set of compatible targets to be used when restoring packages.</span></span> <span data-ttu-id="82450-418">旨在允许使用 dotnet [TxM](../reference/target-frameworks.md) 的包与未声明 dotnet TxM 的兼容包结合使用。</span><span class="sxs-lookup"><span data-stu-id="82450-418">It's designed to allow packages that use a dotnet [TxM](../reference/target-frameworks.md) to work with compatible packages that don't declare a dotnet TxM.</span></span> <span data-ttu-id="82450-419">也就是说，如果项目使用 dotnet TxM，那么所依赖的所有包也必须有 dotnet TxM，除非将 `<PackageTargetFallback>` 添加到项目中，以允许非 dotnet 平台与 dotnet 兼容。</span><span class="sxs-lookup"><span data-stu-id="82450-419">That is, if your project uses the dotnet TxM, then all the packages it depends on must also have a dotnet TxM, unless you add the `<PackageTargetFallback>` to your project in order to allow non-dotnet platforms to be compatible with dotnet.</span></span>

<span data-ttu-id="82450-420">例如，如果项目使用的是 `netstandard1.6` TxM，且从属包仅包含 `lib/net45/a.dll` 和 `lib/portable-net45+win81/a.dll`，则项目将无法生成。</span><span class="sxs-lookup"><span data-stu-id="82450-420">For example, if the project is using the `netstandard1.6` TxM, and a dependent package contains only `lib/net45/a.dll` and `lib/portable-net45+win81/a.dll`, then the project will fail to build.</span></span> <span data-ttu-id="82450-421">如果需要的是后一种 DLL，则可以按照如下所示添加 `PackageTargetFallback`，声明 `portable-net45+win81` DLL 是兼容的：</span><span class="sxs-lookup"><span data-stu-id="82450-421">If what you want to bring in is the latter DLL, then you can add a `PackageTargetFallback` as follows to say that the `portable-net45+win81` DLL is compatible:</span></span>

```xml
<PackageTargetFallback Condition="'$(TargetFramework)'=='netstandard1.6'">
    portable-net45+win81
</PackageTargetFallback>
```

<span data-ttu-id="82450-422">若要声明项目中所有目标的回退，请停止 `Condition` 属性。</span><span class="sxs-lookup"><span data-stu-id="82450-422">To declare a fallback for all targets in your project, leave off the `Condition` attribute.</span></span> <span data-ttu-id="82450-423">还可以通过包括 `$(PackageTargetFallback)` 扩展任何现有 `PackageTargetFallback`，如下所示：</span><span class="sxs-lookup"><span data-stu-id="82450-423">You can also extend any existing `PackageTargetFallback` by including `$(PackageTargetFallback)` as shown here:</span></span>

```xml
<PackageTargetFallback>
    $(PackageTargetFallback);portable-net45+win81
</PackageTargetFallback >
```

### <a name="replacing-one-library-from-a-restore-graph"></a><span data-ttu-id="82450-424">从还原图中替换一个库</span><span class="sxs-lookup"><span data-stu-id="82450-424">Replacing one library from a restore graph</span></span>

<span data-ttu-id="82450-425">如果还原引入了错误的程序集，可以排除包默认选项，并将其替换为自己的选项。</span><span class="sxs-lookup"><span data-stu-id="82450-425">If a restore is bringing the wrong assembly, it's possible to exclude that packages default choice, and replace it with your own choice.</span></span> <span data-ttu-id="82450-426">首先使用顶级 `PackageReference`，排除所有资产：</span><span class="sxs-lookup"><span data-stu-id="82450-426">First with a top level `PackageReference`, exclude all assets:</span></span>

```xml
<PackageReference Include="Newtonsoft.Json" Version="9.0.1">
  <ExcludeAssets>All</ExcludeAssets>
</PackageReference>
```

<span data-ttu-id="82450-427">接下来，将自己的引用添加到适当的 DLL 本地副本：</span><span class="sxs-lookup"><span data-stu-id="82450-427">Next, add your own reference to the appropriate local copy of the DLL:</span></span>

```xml
<Reference Include="Newtonsoft.Json.dll" />
```
