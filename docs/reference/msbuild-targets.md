---
title: 作为 MSBuild 目标的 NuGet 包和还原
description: NuGet 包和还原可作为 MSBuild 目标直接用于 NuGet 4.0+。
author: nkolev92
ms.author: nikolev
ms.date: 03/23/2018
ms.topic: conceptual
ms.openlocfilehash: 66df4e0e4739300608fd5f9e44eea5bcd00079c8
ms.sourcegitcommit: 53b06e27bcfef03500a69548ba2db069b55837f1
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/19/2020
ms.locfileid: "97699891"
---
# <a name="nuget-pack-and-restore-as-msbuild-targets"></a><span data-ttu-id="e5428-103">作为 MSBuild 目标的 NuGet 包和还原</span><span class="sxs-lookup"><span data-stu-id="e5428-103">NuGet pack and restore as MSBuild targets</span></span>

<span data-ttu-id="e5428-104">NuGet 4.0+</span><span class="sxs-lookup"><span data-stu-id="e5428-104">*NuGet 4.0+*</span></span>

<span data-ttu-id="e5428-105">使用 [PackageReference](../consume-packages/package-references-in-project-files.md) 格式，NuGet 4.0 + 可以直接将所有清单元数据存储在项目文件中，而不是使用单独的 `.nuspec` 文件。</span><span class="sxs-lookup"><span data-stu-id="e5428-105">With the [PackageReference](../consume-packages/package-references-in-project-files.md) format, NuGet 4.0+ can store all manifest metadata directly within a project file rather than using a separate `.nuspec` file.</span></span>

<span data-ttu-id="e5428-106">如下所述，对于 MSBuild 15.1+，NuGet 还是具有 `pack` 目标和 `restore` 目标的一等 MSBuild 公民。</span><span class="sxs-lookup"><span data-stu-id="e5428-106">With MSBuild 15.1+, NuGet is also a first-class MSBuild citizen with the `pack` and `restore` targets as described below.</span></span> <span data-ttu-id="e5428-107">借助这些目标，你可以像使用任何其他 MSBuild 任务或目标一样使用 NuGet。</span><span class="sxs-lookup"><span data-stu-id="e5428-107">These targets allow you to work with NuGet as you would with any other MSBuild task or target.</span></span> <span data-ttu-id="e5428-108">有关使用 MSBuild 创建 NuGet 包的说明，请参阅 [使用 Msbuild 创建 nuget 包](../create-packages/creating-a-package-msbuild.md)。</span><span class="sxs-lookup"><span data-stu-id="e5428-108">For instructions creating a NuGet package using MSBuild, see [Create a NuGet package using MSBuild](../create-packages/creating-a-package-msbuild.md).</span></span> <span data-ttu-id="e5428-109">（对于 Nuget 3.x 及更早版本，通过 NuGet CLI 使用 [pack](../reference/cli-reference/cli-ref-pack.md) 和 [restore](../reference/cli-reference/cli-ref-restore.md) 命令。）</span><span class="sxs-lookup"><span data-stu-id="e5428-109">(For NuGet 3.x and earlier, you use the [pack](../reference/cli-reference/cli-ref-pack.md) and [restore](../reference/cli-reference/cli-ref-restore.md) commands through the NuGet CLI instead.)</span></span>

## <a name="target-build-order"></a><span data-ttu-id="e5428-110">目标生成顺序</span><span class="sxs-lookup"><span data-stu-id="e5428-110">Target build order</span></span>

<span data-ttu-id="e5428-111">由于 `pack` 和 `restore` 为 MSBuild 目标，因此可以访问它们以增强工作流。</span><span class="sxs-lookup"><span data-stu-id="e5428-111">Because `pack` and `restore` are  MSBuild targets, you can access them to enhance your workflow.</span></span> <span data-ttu-id="e5428-112">例如，假设希望在打包后将包复制到网络共享。</span><span class="sxs-lookup"><span data-stu-id="e5428-112">For example, let’s say you want to copy your package to a network share after packing it.</span></span> <span data-ttu-id="e5428-113">此操作可通过向项目文件中添加以下内容来完成：</span><span class="sxs-lookup"><span data-stu-id="e5428-113">You can do that by adding the following in your project file:</span></span>

```xml
<Target Name="CopyPackage" AfterTargets="Pack">
  <Copy
    SourceFiles="$(OutputPath)..\$(PackageId).$(PackageVersion).nupkg"
    DestinationFolder="\\myshare\packageshare\"
    />
</Target>
```

<span data-ttu-id="e5428-114">同样，你可以编写 MSBuild 任务、编写自己的目标并使用 MSBuild 任务中的 NuGet 属性。</span><span class="sxs-lookup"><span data-stu-id="e5428-114">Similarly, you can write an MSBuild task, write your own target and consume NuGet properties in the MSBuild task.</span></span>

> [!NOTE]
> <span data-ttu-id="e5428-115">`$(OutputPath)` 是相对的，需要从项目根目录运行命令。</span><span class="sxs-lookup"><span data-stu-id="e5428-115">`$(OutputPath)` is relative and expects that you are running the command from the project root.</span></span>

## <a name="pack-target"></a><span data-ttu-id="e5428-116">包目标</span><span class="sxs-lookup"><span data-stu-id="e5428-116">pack target</span></span>

<span data-ttu-id="e5428-117">对于使用 PackageReference 格式的 .NET Standard 项目，使用 `msbuild -t:pack` 可以从项目文件绘制输入，以在创建 NuGet 包时使用。</span><span class="sxs-lookup"><span data-stu-id="e5428-117">For .NET Standard projects using the PackageReference format, using `msbuild -t:pack` draws inputs from the project file to use in creating a NuGet package.</span></span>

<span data-ttu-id="e5428-118">下表描述了可以添加到项目文件第一个 `<PropertyGroup>` 节点中的 MSBuild 属性。</span><span class="sxs-lookup"><span data-stu-id="e5428-118">The table below describes the MSBuild properties that can be added to a project file within the first `<PropertyGroup>` node.</span></span> <span data-ttu-id="e5428-119">在 Visual Studio 2017 及更高版本中，通过右键单击项目并选择上下文菜单上的“编辑 {project_name}”，即可轻松进行这些编辑。</span><span class="sxs-lookup"><span data-stu-id="e5428-119">You can make these edits easily in Visual Studio 2017 and later by right-clicking the project and selecting **Edit {project_name}** on the context menu.</span></span> <span data-ttu-id="e5428-120">为方便起见，表按[ `.nuspec` 文件](../reference/nuspec.md)中的等效属性进行组织。</span><span class="sxs-lookup"><span data-stu-id="e5428-120">For convenience the table is organized by the equivalent property in a [`.nuspec` file](../reference/nuspec.md).</span></span>

<span data-ttu-id="e5428-121">请注意，`.nuspec` 的 `Owners` 和 `Summary` 属性不受 MSBuild 支持。</span><span class="sxs-lookup"><span data-stu-id="e5428-121">Note that the `Owners` and `Summary` properties from `.nuspec` are not supported with MSBuild.</span></span>

| <span data-ttu-id="e5428-122">属性/NuSpec 值</span><span class="sxs-lookup"><span data-stu-id="e5428-122">Attribute/NuSpec Value</span></span> | <span data-ttu-id="e5428-123">MSBuild 属性</span><span class="sxs-lookup"><span data-stu-id="e5428-123">MSBuild Property</span></span> | <span data-ttu-id="e5428-124">默认</span><span class="sxs-lookup"><span data-stu-id="e5428-124">Default</span></span> | <span data-ttu-id="e5428-125">说明</span><span class="sxs-lookup"><span data-stu-id="e5428-125">Notes</span></span> |
|--------|--------|--------|--------|
| <span data-ttu-id="e5428-126">ID</span><span class="sxs-lookup"><span data-stu-id="e5428-126">Id</span></span> | <span data-ttu-id="e5428-127">PackageId</span><span class="sxs-lookup"><span data-stu-id="e5428-127">PackageId</span></span> | <span data-ttu-id="e5428-128">AssemblyName</span><span class="sxs-lookup"><span data-stu-id="e5428-128">AssemblyName</span></span> | <span data-ttu-id="e5428-129">MSBuild 的 $(AssemblyName)</span><span class="sxs-lookup"><span data-stu-id="e5428-129">$(AssemblyName) from MSBuild</span></span> |
| <span data-ttu-id="e5428-130">版本</span><span class="sxs-lookup"><span data-stu-id="e5428-130">Version</span></span> | <span data-ttu-id="e5428-131">PackageVersion</span><span class="sxs-lookup"><span data-stu-id="e5428-131">PackageVersion</span></span> | <span data-ttu-id="e5428-132">版本</span><span class="sxs-lookup"><span data-stu-id="e5428-132">Version</span></span> | <span data-ttu-id="e5428-133">这与 SemVer 兼容，例如，“1.0.0”、“1.0.0-beta”或“1.0.0-beta-00345”</span><span class="sxs-lookup"><span data-stu-id="e5428-133">This is semver compatible, for example “1.0.0”, “1.0.0-beta”, or “1.0.0-beta-00345”</span></span> |
| <span data-ttu-id="e5428-134">VersionPrefix</span><span class="sxs-lookup"><span data-stu-id="e5428-134">VersionPrefix</span></span> | <span data-ttu-id="e5428-135">PackageVersionPrefix</span><span class="sxs-lookup"><span data-stu-id="e5428-135">PackageVersionPrefix</span></span> | <span data-ttu-id="e5428-136">empty</span><span class="sxs-lookup"><span data-stu-id="e5428-136">empty</span></span> | <span data-ttu-id="e5428-137">设置 PackageVersion 会覆盖 PackageVersionPrefix</span><span class="sxs-lookup"><span data-stu-id="e5428-137">Setting PackageVersion overwrites PackageVersionPrefix</span></span> |
| <span data-ttu-id="e5428-138">VersionSuffix</span><span class="sxs-lookup"><span data-stu-id="e5428-138">VersionSuffix</span></span> | <span data-ttu-id="e5428-139">PackageVersionSuffix</span><span class="sxs-lookup"><span data-stu-id="e5428-139">PackageVersionSuffix</span></span> | <span data-ttu-id="e5428-140">empty</span><span class="sxs-lookup"><span data-stu-id="e5428-140">empty</span></span> | <span data-ttu-id="e5428-141">MSBuild 的 $(VersionSuffix)。</span><span class="sxs-lookup"><span data-stu-id="e5428-141">$(VersionSuffix) from MSBuild.</span></span> <span data-ttu-id="e5428-142">设置 PackageVersion 会覆盖 PackageVersionSuffix</span><span class="sxs-lookup"><span data-stu-id="e5428-142">Setting PackageVersion overwrites PackageVersionSuffix</span></span> |
| <span data-ttu-id="e5428-143">Authors</span><span class="sxs-lookup"><span data-stu-id="e5428-143">Authors</span></span> | <span data-ttu-id="e5428-144">Authors</span><span class="sxs-lookup"><span data-stu-id="e5428-144">Authors</span></span> | <span data-ttu-id="e5428-145">当前用户的用户名</span><span class="sxs-lookup"><span data-stu-id="e5428-145">Username of the current user</span></span> | |
| <span data-ttu-id="e5428-146">所有者</span><span class="sxs-lookup"><span data-stu-id="e5428-146">Owners</span></span> | <span data-ttu-id="e5428-147">空值</span><span class="sxs-lookup"><span data-stu-id="e5428-147">N/A</span></span> | <span data-ttu-id="e5428-148">NuSpec 中不存在</span><span class="sxs-lookup"><span data-stu-id="e5428-148">Not present in NuSpec</span></span> | |
| <span data-ttu-id="e5428-149">Title</span><span class="sxs-lookup"><span data-stu-id="e5428-149">Title</span></span> | <span data-ttu-id="e5428-150">Title</span><span class="sxs-lookup"><span data-stu-id="e5428-150">Title</span></span> | <span data-ttu-id="e5428-151">PackageId</span><span class="sxs-lookup"><span data-stu-id="e5428-151">The PackageId</span></span>| |
| <span data-ttu-id="e5428-152">说明</span><span class="sxs-lookup"><span data-stu-id="e5428-152">Description</span></span> | <span data-ttu-id="e5428-153">说明</span><span class="sxs-lookup"><span data-stu-id="e5428-153">Description</span></span> | <span data-ttu-id="e5428-154">“包描述”</span><span class="sxs-lookup"><span data-stu-id="e5428-154">"Package Description"</span></span> | |
| <span data-ttu-id="e5428-155">Copyright</span><span class="sxs-lookup"><span data-stu-id="e5428-155">Copyright</span></span> | <span data-ttu-id="e5428-156">Copyright</span><span class="sxs-lookup"><span data-stu-id="e5428-156">Copyright</span></span> | <span data-ttu-id="e5428-157">empty</span><span class="sxs-lookup"><span data-stu-id="e5428-157">empty</span></span> | |
| <span data-ttu-id="e5428-158">RequireLicenseAcceptance</span><span class="sxs-lookup"><span data-stu-id="e5428-158">RequireLicenseAcceptance</span></span> | <span data-ttu-id="e5428-159">PackageRequireLicenseAcceptance</span><span class="sxs-lookup"><span data-stu-id="e5428-159">PackageRequireLicenseAcceptance</span></span> | <span data-ttu-id="e5428-160">false</span><span class="sxs-lookup"><span data-stu-id="e5428-160">false</span></span> | |
| <span data-ttu-id="e5428-161">license</span><span class="sxs-lookup"><span data-stu-id="e5428-161">license</span></span> | <span data-ttu-id="e5428-162">PackageLicenseExpression</span><span class="sxs-lookup"><span data-stu-id="e5428-162">PackageLicenseExpression</span></span> | <span data-ttu-id="e5428-163">empty</span><span class="sxs-lookup"><span data-stu-id="e5428-163">empty</span></span> | <span data-ttu-id="e5428-164">与 `<license type="expression">`</span><span class="sxs-lookup"><span data-stu-id="e5428-164">Corresponds to `<license type="expression">`</span></span> |
| <span data-ttu-id="e5428-165">license</span><span class="sxs-lookup"><span data-stu-id="e5428-165">license</span></span> | <span data-ttu-id="e5428-166">PackageLicenseFile</span><span class="sxs-lookup"><span data-stu-id="e5428-166">PackageLicenseFile</span></span> | <span data-ttu-id="e5428-167">empty</span><span class="sxs-lookup"><span data-stu-id="e5428-167">empty</span></span> | <span data-ttu-id="e5428-168">对应到 `<license type="file">`。</span><span class="sxs-lookup"><span data-stu-id="e5428-168">Corresponds to `<license type="file">`.</span></span> <span data-ttu-id="e5428-169">需要显式打包所引用的许可证文件。</span><span class="sxs-lookup"><span data-stu-id="e5428-169">You need to explicitly pack the referenced license file.</span></span> |
| <span data-ttu-id="e5428-170">LicenseUrl</span><span class="sxs-lookup"><span data-stu-id="e5428-170">LicenseUrl</span></span> | <span data-ttu-id="e5428-171">PackageLicenseUrl</span><span class="sxs-lookup"><span data-stu-id="e5428-171">PackageLicenseUrl</span></span> | <span data-ttu-id="e5428-172">empty</span><span class="sxs-lookup"><span data-stu-id="e5428-172">empty</span></span> | <span data-ttu-id="e5428-173">`PackageLicenseUrl` 已弃用，请使用 PackageLicenseExpression 或 PackageLicenseFile 属性</span><span class="sxs-lookup"><span data-stu-id="e5428-173">`PackageLicenseUrl` is deprecated, use the PackageLicenseExpression or PackageLicenseFile property</span></span> |
| <span data-ttu-id="e5428-174">ProjectUrl</span><span class="sxs-lookup"><span data-stu-id="e5428-174">ProjectUrl</span></span> | <span data-ttu-id="e5428-175">PackageProjectUrl</span><span class="sxs-lookup"><span data-stu-id="e5428-175">PackageProjectUrl</span></span> | <span data-ttu-id="e5428-176">empty</span><span class="sxs-lookup"><span data-stu-id="e5428-176">empty</span></span> | |
| <span data-ttu-id="e5428-177">图标</span><span class="sxs-lookup"><span data-stu-id="e5428-177">Icon</span></span> | <span data-ttu-id="e5428-178">PackageIcon</span><span class="sxs-lookup"><span data-stu-id="e5428-178">PackageIcon</span></span> | <span data-ttu-id="e5428-179">empty</span><span class="sxs-lookup"><span data-stu-id="e5428-179">empty</span></span> | <span data-ttu-id="e5428-180">需要显式打包所引用的图标图像文件。</span><span class="sxs-lookup"><span data-stu-id="e5428-180">You need to explicitly pack the referenced icon image file.</span></span>|
| <span data-ttu-id="e5428-181">IconUrl</span><span class="sxs-lookup"><span data-stu-id="e5428-181">IconUrl</span></span> | <span data-ttu-id="e5428-182">PackageIconUrl</span><span class="sxs-lookup"><span data-stu-id="e5428-182">PackageIconUrl</span></span> | <span data-ttu-id="e5428-183">empty</span><span class="sxs-lookup"><span data-stu-id="e5428-183">empty</span></span> | <span data-ttu-id="e5428-184">为了获得最佳的下层体验， `PackageIconUrl` 除了指定外，还应该指定 `PackageIcon` 。</span><span class="sxs-lookup"><span data-stu-id="e5428-184">For the best downlevel experience, `PackageIconUrl` should be specified in addition to `PackageIcon`.</span></span> <span data-ttu-id="e5428-185">长期， `PackageIconUrl` 将被弃用。</span><span class="sxs-lookup"><span data-stu-id="e5428-185">Longer term, `PackageIconUrl` will be deprecated.</span></span> |
| <span data-ttu-id="e5428-186">标记</span><span class="sxs-lookup"><span data-stu-id="e5428-186">Tags</span></span> | <span data-ttu-id="e5428-187">PackageTags</span><span class="sxs-lookup"><span data-stu-id="e5428-187">PackageTags</span></span> | <span data-ttu-id="e5428-188">empty</span><span class="sxs-lookup"><span data-stu-id="e5428-188">empty</span></span> | <span data-ttu-id="e5428-189">使用分号分隔标记。</span><span class="sxs-lookup"><span data-stu-id="e5428-189">Tags are semi-colon delimited.</span></span> |
| <span data-ttu-id="e5428-190">ReleaseNotes</span><span class="sxs-lookup"><span data-stu-id="e5428-190">ReleaseNotes</span></span> | <span data-ttu-id="e5428-191">PackageReleaseNotes</span><span class="sxs-lookup"><span data-stu-id="e5428-191">PackageReleaseNotes</span></span> | <span data-ttu-id="e5428-192">empty</span><span class="sxs-lookup"><span data-stu-id="e5428-192">empty</span></span> | |
| <span data-ttu-id="e5428-193">存储库/Url</span><span class="sxs-lookup"><span data-stu-id="e5428-193">Repository/Url</span></span> | <span data-ttu-id="e5428-194">RepositoryUrl</span><span class="sxs-lookup"><span data-stu-id="e5428-194">RepositoryUrl</span></span> | <span data-ttu-id="e5428-195">empty</span><span class="sxs-lookup"><span data-stu-id="e5428-195">empty</span></span> | <span data-ttu-id="e5428-196">用于克隆或检索源代码的存储库 URL。</span><span class="sxs-lookup"><span data-stu-id="e5428-196">Repository URL used to clone or retrieve source code.</span></span> <span data-ttu-id="e5428-197">实例 *https://github.com/NuGet/NuGet.Client.git*</span><span class="sxs-lookup"><span data-stu-id="e5428-197">Example: *https://github.com/NuGet/NuGet.Client.git*</span></span> |
| <span data-ttu-id="e5428-198">存储库/类型</span><span class="sxs-lookup"><span data-stu-id="e5428-198">Repository/Type</span></span> | <span data-ttu-id="e5428-199">RepositoryType</span><span class="sxs-lookup"><span data-stu-id="e5428-199">RepositoryType</span></span> | <span data-ttu-id="e5428-200">empty</span><span class="sxs-lookup"><span data-stu-id="e5428-200">empty</span></span> | <span data-ttu-id="e5428-201">存储库类型。</span><span class="sxs-lookup"><span data-stu-id="e5428-201">Repository type.</span></span> <span data-ttu-id="e5428-202">示例： *git*、 *tfs*。</span><span class="sxs-lookup"><span data-stu-id="e5428-202">Examples: *git*, *tfs*.</span></span> |
| <span data-ttu-id="e5428-203">存储库/分支</span><span class="sxs-lookup"><span data-stu-id="e5428-203">Repository/Branch</span></span> | <span data-ttu-id="e5428-204">RepositoryBranch</span><span class="sxs-lookup"><span data-stu-id="e5428-204">RepositoryBranch</span></span> | <span data-ttu-id="e5428-205">empty</span><span class="sxs-lookup"><span data-stu-id="e5428-205">empty</span></span> | <span data-ttu-id="e5428-206">可选存储库分支信息。</span><span class="sxs-lookup"><span data-stu-id="e5428-206">Optional repository branch information.</span></span> <span data-ttu-id="e5428-207">还必须为此属性指定要包含的 *RepositoryUrl* 。</span><span class="sxs-lookup"><span data-stu-id="e5428-207">*RepositoryUrl* must also be specified for this property to be included.</span></span> <span data-ttu-id="e5428-208">示例： *master* (NuGet 4.7.0 +) </span><span class="sxs-lookup"><span data-stu-id="e5428-208">Example: *master* (NuGet 4.7.0+)</span></span> |
| <span data-ttu-id="e5428-209">存储库/提交</span><span class="sxs-lookup"><span data-stu-id="e5428-209">Repository/Commit</span></span> | <span data-ttu-id="e5428-210">RepositoryCommit</span><span class="sxs-lookup"><span data-stu-id="e5428-210">RepositoryCommit</span></span> | <span data-ttu-id="e5428-211">empty</span><span class="sxs-lookup"><span data-stu-id="e5428-211">empty</span></span> | <span data-ttu-id="e5428-212">可选的存储库提交或更改集，指示针对其生成包的源。</span><span class="sxs-lookup"><span data-stu-id="e5428-212">Optional repository commit or changeset to indicate which source the package was built against.</span></span> <span data-ttu-id="e5428-213">还必须为此属性指定要包含的 *RepositoryUrl* 。</span><span class="sxs-lookup"><span data-stu-id="e5428-213">*RepositoryUrl* must also be specified for this property to be included.</span></span> <span data-ttu-id="e5428-214">示例： *0e4d1b598f350b3dc675018d539114d1328189ef* (NuGet 4.7.0 +) </span><span class="sxs-lookup"><span data-stu-id="e5428-214">Example: *0e4d1b598f350b3dc675018d539114d1328189ef* (NuGet 4.7.0+)</span></span> |
| <span data-ttu-id="e5428-215">PackageType</span><span class="sxs-lookup"><span data-stu-id="e5428-215">PackageType</span></span> | `<PackageType>DotNetCliTool, 1.0.0.0;Dependency, 2.0.0.0</PackageType>` | | |
| <span data-ttu-id="e5428-216">总结</span><span class="sxs-lookup"><span data-stu-id="e5428-216">Summary</span></span> | <span data-ttu-id="e5428-217">不支持</span><span class="sxs-lookup"><span data-stu-id="e5428-217">Not supported</span></span> | | |

### <a name="pack-target-inputs"></a><span data-ttu-id="e5428-218">包目标输入</span><span class="sxs-lookup"><span data-stu-id="e5428-218">pack target inputs</span></span>

- <span data-ttu-id="e5428-219">IsPackable</span><span class="sxs-lookup"><span data-stu-id="e5428-219">IsPackable</span></span>
- <span data-ttu-id="e5428-220">SuppressDependenciesWhenPacking</span><span class="sxs-lookup"><span data-stu-id="e5428-220">SuppressDependenciesWhenPacking</span></span>
- <span data-ttu-id="e5428-221">PackageVersion</span><span class="sxs-lookup"><span data-stu-id="e5428-221">PackageVersion</span></span>
- <span data-ttu-id="e5428-222">PackageId</span><span class="sxs-lookup"><span data-stu-id="e5428-222">PackageId</span></span>
- <span data-ttu-id="e5428-223">Authors</span><span class="sxs-lookup"><span data-stu-id="e5428-223">Authors</span></span>
- <span data-ttu-id="e5428-224">说明</span><span class="sxs-lookup"><span data-stu-id="e5428-224">Description</span></span>
- <span data-ttu-id="e5428-225">Copyright</span><span class="sxs-lookup"><span data-stu-id="e5428-225">Copyright</span></span>
- <span data-ttu-id="e5428-226">PackageRequireLicenseAcceptance</span><span class="sxs-lookup"><span data-stu-id="e5428-226">PackageRequireLicenseAcceptance</span></span>
- <span data-ttu-id="e5428-227">DevelopmentDependency</span><span class="sxs-lookup"><span data-stu-id="e5428-227">DevelopmentDependency</span></span>
- <span data-ttu-id="e5428-228">PackageLicenseExpression</span><span class="sxs-lookup"><span data-stu-id="e5428-228">PackageLicenseExpression</span></span>
- <span data-ttu-id="e5428-229">PackageLicenseFile</span><span class="sxs-lookup"><span data-stu-id="e5428-229">PackageLicenseFile</span></span>
- <span data-ttu-id="e5428-230">PackageLicenseUrl</span><span class="sxs-lookup"><span data-stu-id="e5428-230">PackageLicenseUrl</span></span>
- <span data-ttu-id="e5428-231">PackageProjectUrl</span><span class="sxs-lookup"><span data-stu-id="e5428-231">PackageProjectUrl</span></span>
- <span data-ttu-id="e5428-232">PackageIconUrl</span><span class="sxs-lookup"><span data-stu-id="e5428-232">PackageIconUrl</span></span>
- <span data-ttu-id="e5428-233">PackageReleaseNotes</span><span class="sxs-lookup"><span data-stu-id="e5428-233">PackageReleaseNotes</span></span>
- <span data-ttu-id="e5428-234">PackageTags</span><span class="sxs-lookup"><span data-stu-id="e5428-234">PackageTags</span></span>
- <span data-ttu-id="e5428-235">PackageOutputPath</span><span class="sxs-lookup"><span data-stu-id="e5428-235">PackageOutputPath</span></span>
- <span data-ttu-id="e5428-236">IncludeSymbols</span><span class="sxs-lookup"><span data-stu-id="e5428-236">IncludeSymbols</span></span>
- <span data-ttu-id="e5428-237">IncludeSource</span><span class="sxs-lookup"><span data-stu-id="e5428-237">IncludeSource</span></span>
- <span data-ttu-id="e5428-238">PackageTypes</span><span class="sxs-lookup"><span data-stu-id="e5428-238">PackageTypes</span></span>
- <span data-ttu-id="e5428-239">IsTool</span><span class="sxs-lookup"><span data-stu-id="e5428-239">IsTool</span></span>
- <span data-ttu-id="e5428-240">RepositoryUrl</span><span class="sxs-lookup"><span data-stu-id="e5428-240">RepositoryUrl</span></span>
- <span data-ttu-id="e5428-241">RepositoryType</span><span class="sxs-lookup"><span data-stu-id="e5428-241">RepositoryType</span></span>
- <span data-ttu-id="e5428-242">RepositoryBranch</span><span class="sxs-lookup"><span data-stu-id="e5428-242">RepositoryBranch</span></span>
- <span data-ttu-id="e5428-243">RepositoryCommit</span><span class="sxs-lookup"><span data-stu-id="e5428-243">RepositoryCommit</span></span>
- <span data-ttu-id="e5428-244">NoPackageAnalysis</span><span class="sxs-lookup"><span data-stu-id="e5428-244">NoPackageAnalysis</span></span>
- <span data-ttu-id="e5428-245">MinClientVersion</span><span class="sxs-lookup"><span data-stu-id="e5428-245">MinClientVersion</span></span>
- <span data-ttu-id="e5428-246">IncludeBuildOutput</span><span class="sxs-lookup"><span data-stu-id="e5428-246">IncludeBuildOutput</span></span>
- <span data-ttu-id="e5428-247">IncludeContentInPack</span><span class="sxs-lookup"><span data-stu-id="e5428-247">IncludeContentInPack</span></span>
- <span data-ttu-id="e5428-248">BuildOutputTargetFolder</span><span class="sxs-lookup"><span data-stu-id="e5428-248">BuildOutputTargetFolder</span></span>
- <span data-ttu-id="e5428-249">ContentTargetFolders</span><span class="sxs-lookup"><span data-stu-id="e5428-249">ContentTargetFolders</span></span>
- <span data-ttu-id="e5428-250">NuspecFile</span><span class="sxs-lookup"><span data-stu-id="e5428-250">NuspecFile</span></span>
- <span data-ttu-id="e5428-251">NuspecBasePath</span><span class="sxs-lookup"><span data-stu-id="e5428-251">NuspecBasePath</span></span>
- <span data-ttu-id="e5428-252">NuspecProperties</span><span class="sxs-lookup"><span data-stu-id="e5428-252">NuspecProperties</span></span>

## <a name="pack-scenarios"></a><span data-ttu-id="e5428-253">包方案</span><span class="sxs-lookup"><span data-stu-id="e5428-253">pack scenarios</span></span>

### <a name="suppress-dependencies"></a><span data-ttu-id="e5428-254">禁止依赖项</span><span class="sxs-lookup"><span data-stu-id="e5428-254">Suppress dependencies</span></span>

<span data-ttu-id="e5428-255">若要取消生成的 NuGet 包中的包依赖项，请将设置 `SuppressDependenciesWhenPacking` 为， `true` 将允许跳过生成的 nupkg 文件中的所有依赖项。</span><span class="sxs-lookup"><span data-stu-id="e5428-255">To suppress package dependencies from generated NuGet package, set `SuppressDependenciesWhenPacking` to `true` which will allow skipping all the dependencies from generated nupkg file.</span></span>

### <a name="packageiconurl"></a><span data-ttu-id="e5428-256">PackageIconUrl</span><span class="sxs-lookup"><span data-stu-id="e5428-256">PackageIconUrl</span></span>

<span data-ttu-id="e5428-257">`PackageIconUrl` 将不推荐使用新 [`PackageIcon`](#packageicon) 属性。</span><span class="sxs-lookup"><span data-stu-id="e5428-257">`PackageIconUrl` will be deprecated in favor of the new [`PackageIcon`](#packageicon) property.</span></span>

<span data-ttu-id="e5428-258">从 NuGet 5.3 & Visual Studio 2019 版本16.3 开始， `pack` 如果包元数据仅指定，则将引发 [NU5048](./errors-and-warnings/nu5048.md) 警告 `PackageIconUrl` 。</span><span class="sxs-lookup"><span data-stu-id="e5428-258">Starting with NuGet 5.3 & Visual Studio 2019 version 16.3, `pack` will raise [NU5048](./errors-and-warnings/nu5048.md) warning if the package metadata only specifies `PackageIconUrl`.</span></span>

### <a name="packageicon"></a><span data-ttu-id="e5428-259">PackageIcon</span><span class="sxs-lookup"><span data-stu-id="e5428-259">PackageIcon</span></span>

> [!Tip]
> <span data-ttu-id="e5428-260">你应同时指定 `PackageIcon` 和， `PackageIconUrl` 以便保持与尚不支持的客户端和源的向后兼容性 `PackageIcon` 。</span><span class="sxs-lookup"><span data-stu-id="e5428-260">You should specify both `PackageIcon` and `PackageIconUrl` to maintain backward compatibility with clients and sources that do not yet support `PackageIcon`.</span></span> <span data-ttu-id="e5428-261">`PackageIcon`在未来版本中，Visual Studio 将支持来自基于文件夹的源的包。</span><span class="sxs-lookup"><span data-stu-id="e5428-261">Visual Studio will support `PackageIcon` for packages coming from a folder-based source in a future release.</span></span>

#### <a name="packing-an-icon-image-file"></a><span data-ttu-id="e5428-262">打包图标图像文件</span><span class="sxs-lookup"><span data-stu-id="e5428-262">Packing an icon image file</span></span>

<span data-ttu-id="e5428-263">打包图标图像文件时，需要使用 `PackageIcon` 属性来指定包路径，相对于包的根。</span><span class="sxs-lookup"><span data-stu-id="e5428-263">When packing an icon image file, you need to use `PackageIcon` property to specify the package path, relative to the root of the package.</span></span> <span data-ttu-id="e5428-264">此外，还需要确保文件已包含在包中。</span><span class="sxs-lookup"><span data-stu-id="e5428-264">In addition, you need to make sure that the file is included in the package.</span></span> <span data-ttu-id="e5428-265">图像文件大小限制为 1 MB。</span><span class="sxs-lookup"><span data-stu-id="e5428-265">Image file size is limited to 1 MB.</span></span> <span data-ttu-id="e5428-266">支持的文件格式包括 JPEG 和 PNG。</span><span class="sxs-lookup"><span data-stu-id="e5428-266">Supported file formats include JPEG and PNG.</span></span> <span data-ttu-id="e5428-267">建议使用128x128 的图像分辨率。</span><span class="sxs-lookup"><span data-stu-id="e5428-267">We recommend an image resolution of 128x128.</span></span>

<span data-ttu-id="e5428-268">例如：</span><span class="sxs-lookup"><span data-stu-id="e5428-268">For example:</span></span>

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

<span data-ttu-id="e5428-269">[包图标示例](https://github.com/NuGet/Samples/tree/master/PackageIconExample)。</span><span class="sxs-lookup"><span data-stu-id="e5428-269">[Package Icon sample](https://github.com/NuGet/Samples/tree/master/PackageIconExample).</span></span>

<span data-ttu-id="e5428-270">对于 nuspec 等效项，请查看 [图标的 nuspec 参考](nuspec.md#icon)。</span><span class="sxs-lookup"><span data-stu-id="e5428-270">For the nuspec equivalent, take a look at [nuspec reference for icon](nuspec.md#icon).</span></span>

### <a name="output-assemblies"></a><span data-ttu-id="e5428-271">输出程序集</span><span class="sxs-lookup"><span data-stu-id="e5428-271">Output assemblies</span></span>

<span data-ttu-id="e5428-272">`nuget pack` 会复制扩展名为 `.exe`、`.dll`、`.xml`、`.winmd`、`.json` 和 `.pri` 的输出文件。</span><span class="sxs-lookup"><span data-stu-id="e5428-272">`nuget pack` copies output files with extensions `.exe`, `.dll`, `.xml`, `.winmd`, `.json`, and `.pri`.</span></span> <span data-ttu-id="e5428-273">复制的输出文件取决于 MSBuild 从 `BuiltOutputProjectGroup` 目标提供的内容。</span><span class="sxs-lookup"><span data-stu-id="e5428-273">The output files that are copied depend on what MSBuild provides from the `BuiltOutputProjectGroup` target.</span></span>

<span data-ttu-id="e5428-274">在项目文件或命令行中，有两种 MSBuild 属性可用于控制输出程序集的位置：</span><span class="sxs-lookup"><span data-stu-id="e5428-274">There are two MSBuild  properties that you can use in your project file or command line to control where output assemblies go:</span></span>

- <span data-ttu-id="e5428-275">`IncludeBuildOutput`：确定包中是否应包括生成输出程序集的布尔值。</span><span class="sxs-lookup"><span data-stu-id="e5428-275">`IncludeBuildOutput`: A boolean that determines whether the build output assemblies should be included in the package.</span></span>
- <span data-ttu-id="e5428-276">`BuildOutputTargetFolder`：指定应放置输出程序集的文件夹。</span><span class="sxs-lookup"><span data-stu-id="e5428-276">`BuildOutputTargetFolder`: Specifies the folder in which the output assemblies should be placed.</span></span> <span data-ttu-id="e5428-277">输出程序集（和其他输出文件）会复制到各自的框架文件夹中。</span><span class="sxs-lookup"><span data-stu-id="e5428-277">The output assemblies (and other output files) are copied into their respective framework folders.</span></span>

### <a name="package-references"></a><span data-ttu-id="e5428-278">包引用</span><span class="sxs-lookup"><span data-stu-id="e5428-278">Package references</span></span>

<span data-ttu-id="e5428-279">请参阅[项目文件中的包引用](../consume-packages/package-references-in-project-files.md)</span><span class="sxs-lookup"><span data-stu-id="e5428-279">See [Package References in Project Files](../consume-packages/package-references-in-project-files.md).</span></span>

### <a name="project-to-project-references"></a><span data-ttu-id="e5428-280">项目到项目的引用</span><span class="sxs-lookup"><span data-stu-id="e5428-280">Project to project references</span></span>

<span data-ttu-id="e5428-281">默认情况下，项目到项目的引用被视为 nuget 包引用，例如：</span><span class="sxs-lookup"><span data-stu-id="e5428-281">Project to project references are considered by default as nuget package references, for example:</span></span>

```xml
<ProjectReference Include="..\UwpLibrary2\UwpLibrary2.csproj"/>
```

<span data-ttu-id="e5428-282">也可将以下元数据添加到项目引用：</span><span class="sxs-lookup"><span data-stu-id="e5428-282">You can also add the following metadata to your project reference:</span></span>

```xml
<IncludeAssets>
<ExcludeAssets>
<PrivateAssets>
```

### <a name="including-content-in-a-package"></a><span data-ttu-id="e5428-283">在包中添加内容</span><span class="sxs-lookup"><span data-stu-id="e5428-283">Including content in a package</span></span>

<span data-ttu-id="e5428-284">若要添加内容，请将额外的元数据添加到现有的 `<Content>` 项。</span><span class="sxs-lookup"><span data-stu-id="e5428-284">To include content, add extra metadata to the existing `<Content>` item.</span></span> <span data-ttu-id="e5428-285">默认情况下，类型“Content”的所有内容都包括在包中，除非使用以下条目替代：</span><span class="sxs-lookup"><span data-stu-id="e5428-285">By default everything of type "Content" gets included in the package unless you override with entries like the following:</span></span>

 ```xml
<Content Include="..\win7-x64\libuv.txt">
  <Pack>false</Pack>
</Content>
 ```

<span data-ttu-id="e5428-286">默认情况下，所有内容都添加到包中 `content` 和 `contentFiles\any\<target_framework>` 文件夹根目录，并保留相对文件夹结构，除非指定包路径：</span><span class="sxs-lookup"><span data-stu-id="e5428-286">By default, everything gets added to the root of the `content` and `contentFiles\any\<target_framework>` folder within a package and preserves the relative folder structure, unless you specify a package path:</span></span>

```xml
<Content Include="..\win7-x64\libuv.txt">
  <Pack>true</Pack>
  <PackagePath>content\myfiles\</PackagePath>
</Content>
```

<span data-ttu-id="e5428-287">如果仅希望将所有内容都复制到特定根文件夹（而不是 `content` 和 `contentFiles`），可使用 MSBuild 属性 `ContentTargetFolders`，其默认值为“content;contentFiles”，但可以设置为任何其他文件夹名称。</span><span class="sxs-lookup"><span data-stu-id="e5428-287">If you want to copy all your content to only a specific root folder(s) (instead of `content` and `contentFiles` both), you can use the MSBuild property `ContentTargetFolders`, which defaults to "content;contentFiles" but can be set to any other folder names.</span></span> <span data-ttu-id="e5428-288">请注意，基于 `buildAction`，仅在 `ContentTargetFolders` 中指定“contentFiles”会将文件置于 `contentFiles\any\<target_framework>` 或 `contentFiles\<language>\<target_framework>` 下。</span><span class="sxs-lookup"><span data-stu-id="e5428-288">Note that just specifying "contentFiles" in `ContentTargetFolders` puts files under `contentFiles\any\<target_framework>` or `contentFiles\<language>\<target_framework>` based on `buildAction`.</span></span>

<span data-ttu-id="e5428-289">`PackagePath` 可以是一组以分号分隔的目标路径。</span><span class="sxs-lookup"><span data-stu-id="e5428-289">`PackagePath` can be a semicolon-delimited set of target paths.</span></span> <span data-ttu-id="e5428-290">指定空的包路径会将文件添加到包的根目录。</span><span class="sxs-lookup"><span data-stu-id="e5428-290">Specifying an empty package path would add the file to the root of the package.</span></span> <span data-ttu-id="e5428-291">例如，以下操作会将 `libuv.txt` 添加到 `content\myfiles`、`content\samples` 和包的根目录：</span><span class="sxs-lookup"><span data-stu-id="e5428-291">For example, the following adds `libuv.txt` to `content\myfiles`, `content\samples`, and the package root:</span></span>

```xml
<Content Include="..\win7-x64\libuv.txt">
  <Pack>true</Pack>
  <PackagePath>content\myfiles;content\sample;;</PackagePath>
</Content>
```

<span data-ttu-id="e5428-292">另外还有 MSBuild 属性 `$(IncludeContentInPack)`，默认值为 `true`。</span><span class="sxs-lookup"><span data-stu-id="e5428-292">There is also an MSBuild property `$(IncludeContentInPack)`, which defaults to `true`.</span></span> <span data-ttu-id="e5428-293">如果在任何项目中将此值设置为 `false`，则该项目的内容不会包括在 nuget 包中。</span><span class="sxs-lookup"><span data-stu-id="e5428-293">If this is set to `false` on any project, then the content from that project are not included in the nuget package.</span></span>

<span data-ttu-id="e5428-294">其他可在任何上述项上设置的特定于包的元数据包括 ```<PackageCopyToOutput>``` 和 ```<PackageFlatten>```，后者在输出 nuspec 中的 ```contentFiles``` 条目上设置 ```CopyToOutput``` 和 ```Flatten``` 值。</span><span class="sxs-lookup"><span data-stu-id="e5428-294">Other pack specific metadata that you can set on any of the above items includes ```<PackageCopyToOutput>``` and ```<PackageFlatten>``` which sets ```CopyToOutput``` and ```Flatten``` values on the ```contentFiles``` entry in the output nuspec.</span></span>

> [!Note]
> <span data-ttu-id="e5428-295">除了“Content”项，`<Pack>` 和 `<PackagePath>` 元数据还可以在具有 Compile、EmbeddedResource、ApplicationDefinition、Page、Resource、SplashScreen、DesignData、DesignDataWithDesignTimeCreateableTypes、CodeAnalysisDictionary、AndroidAsset、AndroidResource、BundleResource 或 None 生成操作的文件上进行设置。</span><span class="sxs-lookup"><span data-stu-id="e5428-295">Apart from Content items, the `<Pack>` and `<PackagePath>` metadata can also be set on files with a build action of Compile, EmbeddedResource, ApplicationDefinition, Page, Resource, SplashScreen, DesignData, DesignDataWithDesignTimeCreateableTypes, CodeAnalysisDictionary, AndroidAsset, AndroidResource, BundleResource or None.</span></span>
>
> <span data-ttu-id="e5428-296">使用通配模式时，对于将包的文件名追加到包路径，包路径必须以文件夹分隔符结尾，否则包路径将被视为包括文件名的完整路径。</span><span class="sxs-lookup"><span data-stu-id="e5428-296">For pack to append the filename to your package path when using globbing patterns, your package path must end with the folder separator character, otherwise the package path is treated as the full path including the file name.</span></span>

### <a name="includesymbols"></a><span data-ttu-id="e5428-297">IncludeSymbols</span><span class="sxs-lookup"><span data-stu-id="e5428-297">IncludeSymbols</span></span>

<span data-ttu-id="e5428-298">使用 `MSBuild -t:pack -p:IncludeSymbols=true` 时，相应的 `.pdb` 文件将随其他输出文件（`.dll`、`.exe`、`.winmd`、`.xml`、`.json`、`.pri`）一起复制。</span><span class="sxs-lookup"><span data-stu-id="e5428-298">When using `MSBuild -t:pack -p:IncludeSymbols=true`, the corresponding `.pdb` files are copied along with other output files (`.dll`, `.exe`, `.winmd`, `.xml`, `.json`, `.pri`).</span></span> <span data-ttu-id="e5428-299">请注意，设置 `IncludeSymbols=true` 会创建常规包和符号包。</span><span class="sxs-lookup"><span data-stu-id="e5428-299">Note that setting `IncludeSymbols=true` creates a regular package *and* a symbols package.</span></span>

### <a name="includesource"></a><span data-ttu-id="e5428-300">IncludeSource</span><span class="sxs-lookup"><span data-stu-id="e5428-300">IncludeSource</span></span>

<span data-ttu-id="e5428-301">这与 `IncludeSymbols` 相同，但它还会连同 `.pdb` 文件复制源文件。</span><span class="sxs-lookup"><span data-stu-id="e5428-301">This is the same as `IncludeSymbols`, except that it copies source files along with `.pdb` files as well.</span></span> <span data-ttu-id="e5428-302">类型为 `Compile` 的所有文件都会复制到 `src\<ProjectName>\`，并保留生成包中的相对路径文件夹结构。</span><span class="sxs-lookup"><span data-stu-id="e5428-302">All files of type `Compile` are copied over to `src\<ProjectName>\` preserving the relative path folder structure in the resulting package.</span></span> <span data-ttu-id="e5428-303">对于将 `TreatAsPackageReference` 设置为 `false` 的任何 `ProjectReference` 的源文件也是如此。</span><span class="sxs-lookup"><span data-stu-id="e5428-303">The same also happens for source files of any `ProjectReference` which has `TreatAsPackageReference` set to `false`.</span></span>

<span data-ttu-id="e5428-304">如果类型为 Compile 的文件位于项目文件夹外，则它只添加到了 `src\<ProjectName>\`。</span><span class="sxs-lookup"><span data-stu-id="e5428-304">If a file of type Compile, is outside the project folder, then it's just added to `src\<ProjectName>\`.</span></span>

### <a name="packing-a-license-expression-or-a-license-file"></a><span data-ttu-id="e5428-305">打包许可证表达式或许可证文件</span><span class="sxs-lookup"><span data-stu-id="e5428-305">Packing a license expression or a license file</span></span>

<span data-ttu-id="e5428-306">使用许可证表达式时，应使用 PackageLicenseExpression 属性。</span><span class="sxs-lookup"><span data-stu-id="e5428-306">When using a license expression, the PackageLicenseExpression property should be used.</span></span> 
<span data-ttu-id="e5428-307">[许可证表达式示例](https://github.com/NuGet/Samples/tree/master/PackageLicenseExpressionExample)。</span><span class="sxs-lookup"><span data-stu-id="e5428-307">[License expression sample](https://github.com/NuGet/Samples/tree/master/PackageLicenseExpressionExample).</span></span>

```xml
<PropertyGroup>
    <PackageLicenseExpression>MIT</PackageLicenseExpression>
</PropertyGroup>
```

<span data-ttu-id="e5428-308">[了解有关 NuGet.org 所接受的许可证表达式和许可证的详细信息](nuspec.md#license)。</span><span class="sxs-lookup"><span data-stu-id="e5428-308">[Learn more about license expressions and licenses that are accepted by NuGet.org](nuspec.md#license).</span></span>

<span data-ttu-id="e5428-309">打包许可证文件时，需要使用 PackageLicenseFile 属性来指定相对于包根的包路径。</span><span class="sxs-lookup"><span data-stu-id="e5428-309">When packing a license file, you need to use PackageLicenseFile property to specify the package path, relative to the root of the package.</span></span> <span data-ttu-id="e5428-310">此外，还需要确保文件已包含在包中。</span><span class="sxs-lookup"><span data-stu-id="e5428-310">In addition, you need to make sure that the file is included in the package.</span></span> <span data-ttu-id="e5428-311">例如：</span><span class="sxs-lookup"><span data-stu-id="e5428-311">For example:</span></span>

```xml
<PropertyGroup>
    <PackageLicenseFile>LICENSE.txt</PackageLicenseFile>
</PropertyGroup>

<ItemGroup>
    <None Include="licenses\LICENSE.txt" Pack="true" PackagePath=""/>
</ItemGroup>
```

<span data-ttu-id="e5428-312">[许可证文件示例](https://github.com/NuGet/Samples/tree/master/PackageLicenseFileExample)。</span><span class="sxs-lookup"><span data-stu-id="e5428-312">[License file sample](https://github.com/NuGet/Samples/tree/master/PackageLicenseFileExample).</span></span>

### <a name="packing-a-file-without-an-extension"></a><span data-ttu-id="e5428-313">打包不带扩展名的文件</span><span class="sxs-lookup"><span data-stu-id="e5428-313">Packing a file without an extension</span></span>

<span data-ttu-id="e5428-314">在某些情况下（如打包许可证文件时），可能需要包含不带扩展名的文件。</span><span class="sxs-lookup"><span data-stu-id="e5428-314">In some scenarios, like when packing a license file, you might want to include a file without an extension.</span></span>
<span data-ttu-id="e5428-315">由于历史原因，NuGet & MSBuild 将没有扩展的路径视为目录。</span><span class="sxs-lookup"><span data-stu-id="e5428-315">For historical reasons, NuGet & MSBuild treat paths without an extension as directories.</span></span>

```xml
  <PropertyGroup>
    <TargetFrameworks>netstandard2.0</TargetFrameworks>
    <PackageLicenseFile>LICENSE</PackageLicenseFile>
  </PropertyGroup>

  <ItemGroup>
    <None Include="LICENSE" Pack="true" PackagePath=""/>
  </ItemGroup>  
```

<span data-ttu-id="e5428-316">[不带扩展的文件示例](https://github.com/NuGet/Samples/blob/master/PackageLicenseFileExtensionlessExample/)。</span><span class="sxs-lookup"><span data-stu-id="e5428-316">[File without an extension sample](https://github.com/NuGet/Samples/blob/master/PackageLicenseFileExtensionlessExample/).</span></span>
### <a name="istool"></a><span data-ttu-id="e5428-317">IsTool</span><span class="sxs-lookup"><span data-stu-id="e5428-317">IsTool</span></span>

<span data-ttu-id="e5428-318">使用 `MSBuild -t:pack -p:IsTool=true` 时，所有输出文件（如[输出程序集](#output-assemblies)方案中所指定）都被复制到 `tools` 文件夹，而不是 `lib` 文件夹。</span><span class="sxs-lookup"><span data-stu-id="e5428-318">When using `MSBuild -t:pack -p:IsTool=true`, all output files, as specified in the [Output Assemblies](#output-assemblies) scenario, are copied to the `tools` folder instead of the `lib` folder.</span></span> <span data-ttu-id="e5428-319">请注意，这不同于 `DotNetCliTool`，后者通过在 `.csproj` 文件中设置 `PackageType` 进行指定。</span><span class="sxs-lookup"><span data-stu-id="e5428-319">Note that this is different from a `DotNetCliTool` which is specified by setting the `PackageType` in `.csproj` file.</span></span>

### <a name="packing-using-a-nuspec"></a><span data-ttu-id="e5428-320">使用 .nuspec 打包</span><span class="sxs-lookup"><span data-stu-id="e5428-320">Packing using a .nuspec</span></span>

<span data-ttu-id="e5428-321">尽管建议你改为在项目文件中包含通常在文件中的 [所有属性](../reference/msbuild-targets.md#pack-target) `.nuspec` ，但你可以选择使用 `.nuspec` 文件打包项目。</span><span class="sxs-lookup"><span data-stu-id="e5428-321">Although it is recommended that you [include all the properties](../reference/msbuild-targets.md#pack-target) that are usually in the `.nuspec` file in the project file instead, you can choose to use a `.nuspec` file to pack your project.</span></span> <span data-ttu-id="e5428-322">对于使用的非 SDK 样式项目 `PackageReference` ，必须导入， `NuGet.Build.Tasks.Pack.targets` 以便可以执行 pack 任务。</span><span class="sxs-lookup"><span data-stu-id="e5428-322">For a non-SDK-style project that uses `PackageReference`, you must import `NuGet.Build.Tasks.Pack.targets` so that the pack task can be executed.</span></span> <span data-ttu-id="e5428-323">你仍需要还原项目，然后才能打包 nuspec 文件。</span><span class="sxs-lookup"><span data-stu-id="e5428-323">You still need to restore the project before you can pack a nuspec file.</span></span> <span data-ttu-id="e5428-324">默认情况下，SDK 样式项目 (包含包目标。 ) </span><span class="sxs-lookup"><span data-stu-id="e5428-324">(An SDK-style project includes the pack targets by default.)</span></span>

<span data-ttu-id="e5428-325">项目文件的目标框架不相关，并且不会在对 nuspec 进行打包时使用。</span><span class="sxs-lookup"><span data-stu-id="e5428-325">The target framework of the project file is irrelevant and not used when packing a nuspec.</span></span> <span data-ttu-id="e5428-326">以下三个 MSBuild 属性与使用 `.nuspec` 的打包相关：</span><span class="sxs-lookup"><span data-stu-id="e5428-326">The following three MSBuild properties are relevant to packing using a `.nuspec`:</span></span>

1. <span data-ttu-id="e5428-327">`NuspecFile`：用于打包的 `.nuspec` 文件的相对或绝对路径。</span><span class="sxs-lookup"><span data-stu-id="e5428-327">`NuspecFile`: relative or absolute path to the `.nuspec` file being used for packing.</span></span>
1. <span data-ttu-id="e5428-328">`NuspecProperties`：键=值对的分号分隔列表。</span><span class="sxs-lookup"><span data-stu-id="e5428-328">`NuspecProperties`: a semicolon-separated list of key=value pairs.</span></span> <span data-ttu-id="e5428-329">由于 MSBuild 命令行分析工作的方式，必须指定多个属性，如下所示：`-p:NuspecProperties="key1=value1;key2=value2"`。</span><span class="sxs-lookup"><span data-stu-id="e5428-329">Due to the way MSBuild command-line parsing works, multiple properties must be specified as follows: `-p:NuspecProperties="key1=value1;key2=value2"`.</span></span>  
1. <span data-ttu-id="e5428-330">`NuspecBasePath`：`.nuspec` 文件的基路径。</span><span class="sxs-lookup"><span data-stu-id="e5428-330">`NuspecBasePath`: Base path for the `.nuspec` file.</span></span>

<span data-ttu-id="e5428-331">如果使用 `dotnet.exe` 打包项目，请使用类似于下面的命令：</span><span class="sxs-lookup"><span data-stu-id="e5428-331">If using `dotnet.exe` to pack your project, use a command like the following:</span></span>

```dotnetcli
dotnet pack <path to .csproj file> -p:NuspecFile=<path to nuspec file> -p:NuspecProperties=<> -p:NuspecBasePath=<Base path> 
```

<span data-ttu-id="e5428-332">如果使用 MSBuild 打包项目，请使用类似于下面的命令：</span><span class="sxs-lookup"><span data-stu-id="e5428-332">If using MSBuild to pack your project, use a command like the following:</span></span>

```cli
msbuild -t:pack <path to .csproj file> -p:NuspecFile=<path to nuspec file> -p:NuspecProperties=<> -p:NuspecBasePath=<Base path> 
```

<span data-ttu-id="e5428-333">请注意，默认情况下，使用 dotnet.exe 或 msbuild 打包 nuspec 也会导致生成项目。</span><span class="sxs-lookup"><span data-stu-id="e5428-333">Please note that packing a nuspec using dotnet.exe or msbuild also leads to building the project by default.</span></span> <span data-ttu-id="e5428-334">可以通过将属性传递给 dotnet.exe 来避免这种情况，这与项目文件中的 ```--no-build``` 设置 ```<NoBuild>true</NoBuild> ``` 以及项目文件中的设置等效 ```<IncludeBuildOutput>false</IncludeBuildOutput> ``` 。</span><span class="sxs-lookup"><span data-stu-id="e5428-334">This can be avoided by passing ```--no-build``` property to dotnet.exe, which is the equivalent of setting ```<NoBuild>true</NoBuild> ``` in your project file, along with setting ```<IncludeBuildOutput>false</IncludeBuildOutput> ``` in the project file.</span></span>

<span data-ttu-id="e5428-335">用于打包 nuspec 文件的 *.csproj* 文件的示例如下：</span><span class="sxs-lookup"><span data-stu-id="e5428-335">An example of a *.csproj* file to pack a nuspec file is:</span></span>

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

### <a name="advanced-extension-points-to-create-customized-package"></a><span data-ttu-id="e5428-336">用于创建自定义包的高级扩展点</span><span class="sxs-lookup"><span data-stu-id="e5428-336">Advanced extension points to create customized package</span></span>

<span data-ttu-id="e5428-337">`pack`目标提供两个扩展点，这些点在内部特定于目标框架的生成中运行。</span><span class="sxs-lookup"><span data-stu-id="e5428-337">The `pack` target provides two extension points that run in the inner, target framework specific build.</span></span> <span data-ttu-id="e5428-338">扩展点支持包括特定于目标框架的内容和程序集到包中：</span><span class="sxs-lookup"><span data-stu-id="e5428-338">The extension points support including target framework specific content and assemblies into a package:</span></span>

- <span data-ttu-id="e5428-339">`TargetsForTfmSpecificBuildOutput` 目标：用于文件夹内的文件 `lib` 或使用指定的文件夹 `BuildOutputTargetFolder` 。</span><span class="sxs-lookup"><span data-stu-id="e5428-339">`TargetsForTfmSpecificBuildOutput` target: Use for files inside the `lib` folder or a folder specified using `BuildOutputTargetFolder`.</span></span>
- <span data-ttu-id="e5428-340">`TargetsForTfmSpecificContentInPackage` 目标：用于之外的文件 `BuildOutputTargetFolder` 。</span><span class="sxs-lookup"><span data-stu-id="e5428-340">`TargetsForTfmSpecificContentInPackage` target: Use for files outside the `BuildOutputTargetFolder`.</span></span>

#### <a name="targetsfortfmspecificbuildoutput"></a><span data-ttu-id="e5428-341">TargetsForTfmSpecificBuildOutput</span><span class="sxs-lookup"><span data-stu-id="e5428-341">TargetsForTfmSpecificBuildOutput</span></span>

<span data-ttu-id="e5428-342">编写自定义目标并将其指定为属性的值 `$(TargetsForTfmSpecificBuildOutput)` 。</span><span class="sxs-lookup"><span data-stu-id="e5428-342">Write a custom target and specify it as the value of the `$(TargetsForTfmSpecificBuildOutput)` property.</span></span> <span data-ttu-id="e5428-343">对于任何需要在 `BuildOutputTargetFolder` 默认情况下进入 (lib 的文件) ，目标应将这些文件写入 ItemGroup， `BuildOutputInPackage` 并设置以下两个元数据值：</span><span class="sxs-lookup"><span data-stu-id="e5428-343">For any files that need to go into the `BuildOutputTargetFolder` (lib by default), the target should write those files into the ItemGroup `BuildOutputInPackage` and set the following two metadata values:</span></span>

- <span data-ttu-id="e5428-344">`FinalOutputPath`：文件的绝对路径;如果未提供，则标识用于计算源路径。</span><span class="sxs-lookup"><span data-stu-id="e5428-344">`FinalOutputPath`: The absolute path of the file; if not provided, the Identity is used to evaluate source path.</span></span>
- <span data-ttu-id="e5428-345">`TargetPath`：当文件需要进入中的子文件夹时， (可选) 设置 `lib\<TargetFramework>` ，如位于其各自区域性文件夹下的附属程序集。</span><span class="sxs-lookup"><span data-stu-id="e5428-345">`TargetPath`:  (Optional) Set when the file needs to go into a subfolder within `lib\<TargetFramework>` , like satellite assemblies that go under their respective culture folders.</span></span> <span data-ttu-id="e5428-346">默认为文件的名称。</span><span class="sxs-lookup"><span data-stu-id="e5428-346">Defaults to the name of the file.</span></span>

<span data-ttu-id="e5428-347">示例：</span><span class="sxs-lookup"><span data-stu-id="e5428-347">Example:</span></span>

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

#### <a name="targetsfortfmspecificcontentinpackage"></a><span data-ttu-id="e5428-348">TargetsForTfmSpecificContentInPackage</span><span class="sxs-lookup"><span data-stu-id="e5428-348">TargetsForTfmSpecificContentInPackage</span></span>

<span data-ttu-id="e5428-349">编写自定义目标并将其指定为属性的值 `$(TargetsForTfmSpecificContentInPackage)` 。</span><span class="sxs-lookup"><span data-stu-id="e5428-349">Write a custom target and specify it as the value of the `$(TargetsForTfmSpecificContentInPackage)` property.</span></span> <span data-ttu-id="e5428-350">对于要包含在包中的任何文件，目标应将这些文件写入 ItemGroup `TfmSpecificPackageFile` ，并设置以下可选的元数据：</span><span class="sxs-lookup"><span data-stu-id="e5428-350">For any files to include in the package, the target should write those files into the ItemGroup `TfmSpecificPackageFile` and set the following optional metadata:</span></span>

- <span data-ttu-id="e5428-351">`PackagePath`：应在包中输出文件的路径。</span><span class="sxs-lookup"><span data-stu-id="e5428-351">`PackagePath`: Path where the file should be output in the package.</span></span> <span data-ttu-id="e5428-352">如果将多个文件添加到同一个包路径，NuGet 将发出警告。</span><span class="sxs-lookup"><span data-stu-id="e5428-352">NuGet issues a warning if more than one file is added to the same package path.</span></span>
- <span data-ttu-id="e5428-353">`BuildAction`：要分配给文件的生成操作，只有当包路径在文件夹中时才是必需的 `contentFiles` 。</span><span class="sxs-lookup"><span data-stu-id="e5428-353">`BuildAction`: The build action to assign to the file, required only if the package path is in the `contentFiles` folder.</span></span> <span data-ttu-id="e5428-354">默认值为 "None"。</span><span class="sxs-lookup"><span data-stu-id="e5428-354">Defaults to "None".</span></span>

<span data-ttu-id="e5428-355">示例：</span><span class="sxs-lookup"><span data-stu-id="e5428-355">An example:</span></span>
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

## <a name="restore-target"></a><span data-ttu-id="e5428-356">还原目标</span><span class="sxs-lookup"><span data-stu-id="e5428-356">restore target</span></span>

<span data-ttu-id="e5428-357">`MSBuild -t:restore`（`nuget restore` 和 `dotnet restore` 与 .NET Core 项目一起使用）会还原项目文件中引用的包，如下所示：</span><span class="sxs-lookup"><span data-stu-id="e5428-357">`MSBuild -t:restore` (which `nuget restore` and `dotnet restore` use with .NET Core projects), restores packages referenced in the project file as follows:</span></span>

1. <span data-ttu-id="e5428-358">读取所有项目到项目的引用</span><span class="sxs-lookup"><span data-stu-id="e5428-358">Read all project to project references</span></span>
1. <span data-ttu-id="e5428-359">读取项目属性以查找中间文件夹和目标框架</span><span class="sxs-lookup"><span data-stu-id="e5428-359">Read the project properties to find the intermediate folder and target frameworks</span></span>
1. <span data-ttu-id="e5428-360">将 MSBuild 数据传递到 NuGet.Build.Tasks.dll</span><span class="sxs-lookup"><span data-stu-id="e5428-360">Pass MSBuild data to NuGet.Build.Tasks.dll</span></span>
1. <span data-ttu-id="e5428-361">运行还原</span><span class="sxs-lookup"><span data-stu-id="e5428-361">Run restore</span></span>
1. <span data-ttu-id="e5428-362">下载包</span><span class="sxs-lookup"><span data-stu-id="e5428-362">Download packages</span></span>
1. <span data-ttu-id="e5428-363">编写资产文件、目标和属性</span><span class="sxs-lookup"><span data-stu-id="e5428-363">Write assets file, targets, and props</span></span>

<span data-ttu-id="e5428-364">`restore`目标适用于使用 PackageReference 格式的项目。</span><span class="sxs-lookup"><span data-stu-id="e5428-364">The `restore` target works for projects using the PackageReference format.</span></span>
<span data-ttu-id="e5428-365">`MSBuild 16.5+` 还具有对格式的 [选择支持](#restoring-packagereference-and-packagesconfig-with-msbuild) `packages.config` 。</span><span class="sxs-lookup"><span data-stu-id="e5428-365">`MSBuild 16.5+` also has [opt-in support](#restoring-packagereference-and-packagesconfig-with-msbuild) for the `packages.config` format.</span></span>

> [!NOTE]
> <span data-ttu-id="e5428-366">`restore`目标[不应](#restoring-and-building-with-one-msbuild-command)与目标组合运行 `build` 。</span><span class="sxs-lookup"><span data-stu-id="e5428-366">The `restore` target [should not be run](#restoring-and-building-with-one-msbuild-command) in combination with the `build` target.</span></span>

### <a name="restore-properties"></a><span data-ttu-id="e5428-367">还原属性</span><span class="sxs-lookup"><span data-stu-id="e5428-367">Restore properties</span></span>

<span data-ttu-id="e5428-368">其他的还原设置可能来自项目文件中的 MSBuild 属性。</span><span class="sxs-lookup"><span data-stu-id="e5428-368">Additional restore settings may come from MSBuild properties in the project file.</span></span> <span data-ttu-id="e5428-369">还可以从命令行使用 `-p:` 开关设置值（请参阅以下示例）。</span><span class="sxs-lookup"><span data-stu-id="e5428-369">Values can also be set from the command line using the `-p:` switch (see Examples below).</span></span>

| <span data-ttu-id="e5428-370">属性</span><span class="sxs-lookup"><span data-stu-id="e5428-370">Property</span></span> | <span data-ttu-id="e5428-371">说明</span><span class="sxs-lookup"><span data-stu-id="e5428-371">Description</span></span> |
|--------|--------|
| <span data-ttu-id="e5428-372">RestoreSources</span><span class="sxs-lookup"><span data-stu-id="e5428-372">RestoreSources</span></span> | <span data-ttu-id="e5428-373">以分号分隔的包源列表。</span><span class="sxs-lookup"><span data-stu-id="e5428-373">Semicolon-delimited list of package sources.</span></span> |
| <span data-ttu-id="e5428-374">RestorePackagesPath</span><span class="sxs-lookup"><span data-stu-id="e5428-374">RestorePackagesPath</span></span> | <span data-ttu-id="e5428-375">用户包文件夹路径。</span><span class="sxs-lookup"><span data-stu-id="e5428-375">User packages folder path.</span></span> |
| <span data-ttu-id="e5428-376">RestoreDisableParallel</span><span class="sxs-lookup"><span data-stu-id="e5428-376">RestoreDisableParallel</span></span> | <span data-ttu-id="e5428-377">将下载限制为一次一个。</span><span class="sxs-lookup"><span data-stu-id="e5428-377">Limit downloads to one at a time.</span></span> |
| <span data-ttu-id="e5428-378">RestoreConfigFile</span><span class="sxs-lookup"><span data-stu-id="e5428-378">RestoreConfigFile</span></span> | <span data-ttu-id="e5428-379">要应用的 `Nuget.Config` 文件的路径。</span><span class="sxs-lookup"><span data-stu-id="e5428-379">Path to a `Nuget.Config` file to apply.</span></span> |
| <span data-ttu-id="e5428-380">RestoreNoCache</span><span class="sxs-lookup"><span data-stu-id="e5428-380">RestoreNoCache</span></span> | <span data-ttu-id="e5428-381">如果为 true，则避免使用缓存的包。</span><span class="sxs-lookup"><span data-stu-id="e5428-381">If true, avoids using cached packages.</span></span> <span data-ttu-id="e5428-382">请参阅 [管理全局包和缓存文件夹](../consume-packages/managing-the-global-packages-and-cache-folders.md)。</span><span class="sxs-lookup"><span data-stu-id="e5428-382">See [Managing the global packages and cache folders](../consume-packages/managing-the-global-packages-and-cache-folders.md).</span></span> |
| <span data-ttu-id="e5428-383">RestoreIgnoreFailedSources</span><span class="sxs-lookup"><span data-stu-id="e5428-383">RestoreIgnoreFailedSources</span></span> | <span data-ttu-id="e5428-384">如果为“true”，则忽略失败或丢失的包源。</span><span class="sxs-lookup"><span data-stu-id="e5428-384">If true, ignores failing or missing package sources.</span></span> |
| <span data-ttu-id="e5428-385">RestoreFallbackFolders</span><span class="sxs-lookup"><span data-stu-id="e5428-385">RestoreFallbackFolders</span></span> | <span data-ttu-id="e5428-386">后备文件夹，其使用方式与使用 "用户包" 文件夹的方式相同。</span><span class="sxs-lookup"><span data-stu-id="e5428-386">Fallback folders, used in the same way the user packages folder is used.</span></span> |
| <span data-ttu-id="e5428-387">RestoreAdditionalProjectSources</span><span class="sxs-lookup"><span data-stu-id="e5428-387">RestoreAdditionalProjectSources</span></span> | <span data-ttu-id="e5428-388">要在还原期间使用的其他源。</span><span class="sxs-lookup"><span data-stu-id="e5428-388">Additional sources to use during restore.</span></span> |
| <span data-ttu-id="e5428-389">RestoreAdditionalProjectFallbackFolders</span><span class="sxs-lookup"><span data-stu-id="e5428-389">RestoreAdditionalProjectFallbackFolders</span></span> | <span data-ttu-id="e5428-390">要在还原期间使用的其他回退文件夹。</span><span class="sxs-lookup"><span data-stu-id="e5428-390">Additional fallback folders to use during restore.</span></span> |
| <span data-ttu-id="e5428-391">RestoreAdditionalProjectFallbackFoldersExcludes</span><span class="sxs-lookup"><span data-stu-id="e5428-391">RestoreAdditionalProjectFallbackFoldersExcludes</span></span> | <span data-ttu-id="e5428-392">排除其中指定的回退文件夹 `RestoreAdditionalProjectFallbackFolders`</span><span class="sxs-lookup"><span data-stu-id="e5428-392">Excludes fallback folders specified in `RestoreAdditionalProjectFallbackFolders`</span></span> |
| <span data-ttu-id="e5428-393">RestoreTaskAssemblyFile</span><span class="sxs-lookup"><span data-stu-id="e5428-393">RestoreTaskAssemblyFile</span></span> | <span data-ttu-id="e5428-394">`NuGet.Build.Tasks.dll` 的路径。</span><span class="sxs-lookup"><span data-stu-id="e5428-394">Path to `NuGet.Build.Tasks.dll`.</span></span> |
| <span data-ttu-id="e5428-395">RestoreGraphProjectInput</span><span class="sxs-lookup"><span data-stu-id="e5428-395">RestoreGraphProjectInput</span></span> | <span data-ttu-id="e5428-396">要还原的以分号分隔的项目列表，其中应包含绝对路径。</span><span class="sxs-lookup"><span data-stu-id="e5428-396">Semicolon-delimited list of projects to restore, which should contain absolute paths.</span></span> |
| <span data-ttu-id="e5428-397">RestoreUseSkipNonexistentTargets</span><span class="sxs-lookup"><span data-stu-id="e5428-397">RestoreUseSkipNonexistentTargets</span></span>  | <span data-ttu-id="e5428-398">通过 MSBuild 收集项目后，它将确定是否使用优化来收集这些项目 `SkipNonexistentTargets` 。</span><span class="sxs-lookup"><span data-stu-id="e5428-398">When the projects are collected via MSBuild it determines whether they are collected using the `SkipNonexistentTargets` optimization.</span></span> <span data-ttu-id="e5428-399">如果未设置，则默认为 `true` 。</span><span class="sxs-lookup"><span data-stu-id="e5428-399">When not set, defaults to `true`.</span></span> <span data-ttu-id="e5428-400">如果无法导入项目的目标，则结果是一个故障快速的行为。</span><span class="sxs-lookup"><span data-stu-id="e5428-400">The consequence is a fail-fast behavior when a project's targets cannot be imported.</span></span> |
| <span data-ttu-id="e5428-401">MSBuildProjectExtensionsPath</span><span class="sxs-lookup"><span data-stu-id="e5428-401">MSBuildProjectExtensionsPath</span></span> | <span data-ttu-id="e5428-402">Output 文件夹，默认为 `BaseIntermediateOutputPath` 和 `obj` 文件夹。</span><span class="sxs-lookup"><span data-stu-id="e5428-402">Output folder, defaulting to `BaseIntermediateOutputPath` and the `obj` folder.</span></span> |
| <span data-ttu-id="e5428-403">RestoreForce</span><span class="sxs-lookup"><span data-stu-id="e5428-403">RestoreForce</span></span> | <span data-ttu-id="e5428-404">在基于 PackageReference 的项目中，将强制解析所有依赖项，即使上次还原已成功。</span><span class="sxs-lookup"><span data-stu-id="e5428-404">In PackageReference based projects, forces all dependencies to be resolved even if the last restore was successful.</span></span> <span data-ttu-id="e5428-405">指定此标志与删除 `project.assets.json` 文件类似。</span><span class="sxs-lookup"><span data-stu-id="e5428-405">Specifying this flag is similar to deleting the `project.assets.json` file.</span></span> <span data-ttu-id="e5428-406">这不会绕过 http 缓存。</span><span class="sxs-lookup"><span data-stu-id="e5428-406">This does not bypass the http-cache.</span></span> |
| <span data-ttu-id="e5428-407">RestorePackagesWithLockFile</span><span class="sxs-lookup"><span data-stu-id="e5428-407">RestorePackagesWithLockFile</span></span> | <span data-ttu-id="e5428-408">选择使用锁定文件。</span><span class="sxs-lookup"><span data-stu-id="e5428-408">Opts into the usage of a lock file.</span></span> |
| <span data-ttu-id="e5428-409">RestoreLockedMode</span><span class="sxs-lookup"><span data-stu-id="e5428-409">RestoreLockedMode</span></span> | <span data-ttu-id="e5428-410">在锁定模式下运行还原。</span><span class="sxs-lookup"><span data-stu-id="e5428-410">Run restore in locked mode.</span></span> <span data-ttu-id="e5428-411">这意味着，还原将不会重新评估依赖关系。</span><span class="sxs-lookup"><span data-stu-id="e5428-411">This means that restore will not reevaluate the dependencies.</span></span> |
| <span data-ttu-id="e5428-412">NuGetLockFilePath</span><span class="sxs-lookup"><span data-stu-id="e5428-412">NuGetLockFilePath</span></span> | <span data-ttu-id="e5428-413">锁定文件的自定义位置。</span><span class="sxs-lookup"><span data-stu-id="e5428-413">A custom location for the lock file.</span></span> <span data-ttu-id="e5428-414">默认位置为项目旁边，名为 `packages.lock.json` 。</span><span class="sxs-lookup"><span data-stu-id="e5428-414">The default location is next to the project and is named `packages.lock.json`.</span></span> |
| <span data-ttu-id="e5428-415">RestoreForceEvaluate</span><span class="sxs-lookup"><span data-stu-id="e5428-415">RestoreForceEvaluate</span></span> | <span data-ttu-id="e5428-416">强制执行还原，重新计算依赖项并更新锁定文件，而不会出现任何警告。</span><span class="sxs-lookup"><span data-stu-id="e5428-416">Forces restore to recompute the dependencies and update the lock file without any warning.</span></span> |
| <span data-ttu-id="e5428-417">RestorePackagesConfig</span><span class="sxs-lookup"><span data-stu-id="e5428-417">RestorePackagesConfig</span></span> | <span data-ttu-id="e5428-418">一个选择使用开关，用 packages.config 还原项目。仅支持 `MSBuild -t:restore` 。</span><span class="sxs-lookup"><span data-stu-id="e5428-418">An opt in switch, that restores projects with packages.config. Support with `MSBuild -t:restore` only.</span></span> |

#### <a name="examples"></a><span data-ttu-id="e5428-419">示例</span><span class="sxs-lookup"><span data-stu-id="e5428-419">Examples</span></span>

<span data-ttu-id="e5428-420">命令行：</span><span class="sxs-lookup"><span data-stu-id="e5428-420">Command line:</span></span>

```cli
msbuild -t:restore -p:RestoreConfigFile=<path>
```

<span data-ttu-id="e5428-421">项目文件：</span><span class="sxs-lookup"><span data-stu-id="e5428-421">Project file:</span></span>

```xml
<PropertyGroup>
    <RestoreIgnoreFailedSource>true</RestoreIgnoreFailedSource>
</PropertyGroup>
```

### <a name="restore-outputs"></a><span data-ttu-id="e5428-422">还原输出</span><span class="sxs-lookup"><span data-stu-id="e5428-422">Restore outputs</span></span>

<span data-ttu-id="e5428-423">还原会在生成 `obj` 文件夹中创建以下文件：</span><span class="sxs-lookup"><span data-stu-id="e5428-423">Restore creates the following files in the build `obj` folder:</span></span>

| <span data-ttu-id="e5428-424">文件</span><span class="sxs-lookup"><span data-stu-id="e5428-424">File</span></span> | <span data-ttu-id="e5428-425">说明</span><span class="sxs-lookup"><span data-stu-id="e5428-425">Description</span></span> |
|--------|--------|
| `project.assets.json` | <span data-ttu-id="e5428-426">包含所有包引用的依赖项关系图。</span><span class="sxs-lookup"><span data-stu-id="e5428-426">Contains the dependency graph of all package references.</span></span> |
| `{projectName}.projectFileExtension.nuget.g.props` | <span data-ttu-id="e5428-427">包中包含的对 MSBuild 属性的引用</span><span class="sxs-lookup"><span data-stu-id="e5428-427">References to MSBuild props contained in packages</span></span> |
| `{projectName}.projectFileExtension.nuget.g.targets` | <span data-ttu-id="e5428-428">包中包含的对 MSBuild 目标的引用</span><span class="sxs-lookup"><span data-stu-id="e5428-428">References to MSBuild targets contained in packages</span></span> |

### <a name="restoring-and-building-with-one-msbuild-command"></a><span data-ttu-id="e5428-429">通过一个 MSBuild 命令进行还原和生成</span><span class="sxs-lookup"><span data-stu-id="e5428-429">Restoring and building with one MSBuild command</span></span>

<span data-ttu-id="e5428-430">由于 NuGet 可以还原引入 MSBuild 目标和属性的包，因此，还原和生成评估将以不同的全局属性运行。</span><span class="sxs-lookup"><span data-stu-id="e5428-430">Due to the fact that NuGet can restore packages that bring down MSBuild targets and props, the restore and build evaluations are run with different global properties.</span></span>
<span data-ttu-id="e5428-431">这意味着，以下操作将具有不可预测且通常不正确的行为。</span><span class="sxs-lookup"><span data-stu-id="e5428-431">This means that the following will have an unpredictable and often incorrect behavior.</span></span>

```cli
msbuild -t:restore,build
```

 <span data-ttu-id="e5428-432">相反，推荐的方法是：</span><span class="sxs-lookup"><span data-stu-id="e5428-432">Instead the recommended approach is:</span></span>

```cli
msbuild -t:build -restore
```

<span data-ttu-id="e5428-433">相同的逻辑也适用于类似于的其他目标 `build` 。</span><span class="sxs-lookup"><span data-stu-id="e5428-433">The same logic applies to other targets similar to `build`.</span></span>

### <a name="restoring-packagereference-and-packagesconfig-with-msbuild"></a><span data-ttu-id="e5428-434">通过 MSBuild 还原 PackageReference 和 packages.config</span><span class="sxs-lookup"><span data-stu-id="e5428-434">Restoring PackageReference and packages.config with MSBuild</span></span>

<span data-ttu-id="e5428-435">对于 MSBuild 16.5 +，还支持 packages.config `msbuild -t:restore` 。</span><span class="sxs-lookup"><span data-stu-id="e5428-435">With MSBuild 16.5+, packages.config are also supported for `msbuild -t:restore`.</span></span>

```cli
msbuild -t:restore -p:RestorePackagesConfig=true
```

> [!NOTE]
> <span data-ttu-id="e5428-436">`packages.config` restore 仅适用于 `MSBuild 16.5+` ，而不适用于 `dotnet.exe`</span><span class="sxs-lookup"><span data-stu-id="e5428-436">`packages.config` restore is only available with `MSBuild 16.5+`, and not with `dotnet.exe`</span></span>

### <a name="packagetargetfallback"></a><span data-ttu-id="e5428-437">PackageTargetFallback</span><span class="sxs-lookup"><span data-stu-id="e5428-437">PackageTargetFallback</span></span>

<span data-ttu-id="e5428-438">`PackageTargetFallback` 元素可用于指定要在还原包时使用的一组兼容目标。</span><span class="sxs-lookup"><span data-stu-id="e5428-438">The `PackageTargetFallback` element allows you to specify a set of compatible targets to be used when restoring packages.</span></span> <span data-ttu-id="e5428-439">旨在允许使用 dotnet [TxM](../reference/target-frameworks.md) 的包与未声明 dotnet TxM 的兼容包结合使用。</span><span class="sxs-lookup"><span data-stu-id="e5428-439">It's designed to allow packages that use a dotnet [TxM](../reference/target-frameworks.md) to work with compatible packages that don't declare a dotnet TxM.</span></span> <span data-ttu-id="e5428-440">也就是说，如果项目使用 dotnet TxM，那么所依赖的所有包也必须有 dotnet TxM，除非将 `<PackageTargetFallback>` 添加到项目中，以允许非 dotnet 平台与 dotnet 兼容。</span><span class="sxs-lookup"><span data-stu-id="e5428-440">That is, if your project uses the dotnet TxM, then all the packages it depends on must also have a dotnet TxM, unless you add the `<PackageTargetFallback>` to your project in order to allow non-dotnet platforms to be compatible with dotnet.</span></span>

<span data-ttu-id="e5428-441">例如，如果项目使用的是 `netstandard1.6` TxM，且从属包仅包含 `lib/net45/a.dll` 和 `lib/portable-net45+win81/a.dll`，则项目将无法生成。</span><span class="sxs-lookup"><span data-stu-id="e5428-441">For example, if the project is using the `netstandard1.6` TxM, and a dependent package contains only `lib/net45/a.dll` and `lib/portable-net45+win81/a.dll`, then the project will fail to build.</span></span> <span data-ttu-id="e5428-442">如果需要的是后一种 DLL，则可以按照如下所示添加 `PackageTargetFallback`，声明 `portable-net45+win81` DLL 是兼容的：</span><span class="sxs-lookup"><span data-stu-id="e5428-442">If what you want to bring in is the latter DLL, then you can add a `PackageTargetFallback` as follows to say that the `portable-net45+win81` DLL is compatible:</span></span>

```xml
<PackageTargetFallback Condition="'$(TargetFramework)'=='netstandard1.6'">
    portable-net45+win81
</PackageTargetFallback>
```

<span data-ttu-id="e5428-443">若要声明项目中所有目标的回退，请停止 `Condition` 属性。</span><span class="sxs-lookup"><span data-stu-id="e5428-443">To declare a fallback for all targets in your project, leave off the `Condition` attribute.</span></span> <span data-ttu-id="e5428-444">还可以通过包括 `$(PackageTargetFallback)` 扩展任何现有 `PackageTargetFallback`，如下所示：</span><span class="sxs-lookup"><span data-stu-id="e5428-444">You can also extend any existing `PackageTargetFallback` by including `$(PackageTargetFallback)` as shown here:</span></span>

```xml
<PackageTargetFallback>
    $(PackageTargetFallback);portable-net45+win81
</PackageTargetFallback >
```

### <a name="replacing-one-library-from-a-restore-graph"></a><span data-ttu-id="e5428-445">从还原图中替换一个库</span><span class="sxs-lookup"><span data-stu-id="e5428-445">Replacing one library from a restore graph</span></span>

<span data-ttu-id="e5428-446">如果还原引入了错误的程序集，可以排除包默认选项，并将其替换为自己的选项。</span><span class="sxs-lookup"><span data-stu-id="e5428-446">If a restore is bringing the wrong assembly, it's possible to exclude that packages default choice, and replace it with your own choice.</span></span> <span data-ttu-id="e5428-447">首先使用顶级 `PackageReference`，排除所有资产：</span><span class="sxs-lookup"><span data-stu-id="e5428-447">First with a top level `PackageReference`, exclude all assets:</span></span>

```xml
<PackageReference Include="Newtonsoft.Json" Version="9.0.1">
  <ExcludeAssets>All</ExcludeAssets>
</PackageReference>
```

<span data-ttu-id="e5428-448">接下来，将自己的引用添加到适当的 DLL 本地副本：</span><span class="sxs-lookup"><span data-stu-id="e5428-448">Next, add your own reference to the appropriate local copy of the DLL:</span></span>

```xml
<Reference Include="Newtonsoft.Json.dll" />
```
