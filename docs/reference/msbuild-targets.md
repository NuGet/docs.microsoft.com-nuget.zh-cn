---
title: 作为 MSBuild 目标的 NuGet 包和还原
description: NuGet 包和还原可作为 MSBuild 目标直接用于 NuGet 4.0+。
author: nkolev92
ms.author: nikolev
ms.date: 03/23/2018
ms.topic: conceptual
ms.openlocfilehash: 0c32978baf6146f10c262ba7af94f61fee22272d
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/26/2021
ms.locfileid: "98777715"
---
# <a name="nuget-pack-and-restore-as-msbuild-targets"></a><span data-ttu-id="4dba6-103">作为 MSBuild 目标的 NuGet 包和还原</span><span class="sxs-lookup"><span data-stu-id="4dba6-103">NuGet pack and restore as MSBuild targets</span></span>

<span data-ttu-id="4dba6-104">NuGet 4.0+</span><span class="sxs-lookup"><span data-stu-id="4dba6-104">*NuGet 4.0+*</span></span>

<span data-ttu-id="4dba6-105">使用 [PackageReference](../consume-packages/package-references-in-project-files.md) 格式，NuGet 4.0 + 可以直接将所有清单元数据存储在项目文件中，而不是使用单独的 `.nuspec` 文件。</span><span class="sxs-lookup"><span data-stu-id="4dba6-105">With the [PackageReference](../consume-packages/package-references-in-project-files.md) format, NuGet 4.0+ can store all manifest metadata directly within a project file rather than using a separate `.nuspec` file.</span></span>

<span data-ttu-id="4dba6-106">如下所述，对于 MSBuild 15.1+，NuGet 还是具有 `pack` 目标和 `restore` 目标的一等 MSBuild 公民。</span><span class="sxs-lookup"><span data-stu-id="4dba6-106">With MSBuild 15.1+, NuGet is also a first-class MSBuild citizen with the `pack` and `restore` targets as described below.</span></span> <span data-ttu-id="4dba6-107">借助这些目标，你可以像使用任何其他 MSBuild 任务或目标一样使用 NuGet。</span><span class="sxs-lookup"><span data-stu-id="4dba6-107">These targets allow you to work with NuGet as you would with any other MSBuild task or target.</span></span> <span data-ttu-id="4dba6-108">有关使用 MSBuild 创建 NuGet 包的说明，请参阅 [使用 Msbuild 创建 nuget 包](../create-packages/creating-a-package-msbuild.md)。</span><span class="sxs-lookup"><span data-stu-id="4dba6-108">For instructions creating a NuGet package using MSBuild, see [Create a NuGet package using MSBuild](../create-packages/creating-a-package-msbuild.md).</span></span> <span data-ttu-id="4dba6-109">（对于 Nuget 3.x 及更早版本，通过 NuGet CLI 使用 [pack](../reference/cli-reference/cli-ref-pack.md) 和 [restore](../reference/cli-reference/cli-ref-restore.md) 命令。）</span><span class="sxs-lookup"><span data-stu-id="4dba6-109">(For NuGet 3.x and earlier, you use the [pack](../reference/cli-reference/cli-ref-pack.md) and [restore](../reference/cli-reference/cli-ref-restore.md) commands through the NuGet CLI instead.)</span></span>

## <a name="target-build-order"></a><span data-ttu-id="4dba6-110">目标生成顺序</span><span class="sxs-lookup"><span data-stu-id="4dba6-110">Target build order</span></span>

<span data-ttu-id="4dba6-111">由于 `pack` 和 `restore` 为 MSBuild 目标，因此可以访问它们以增强工作流。</span><span class="sxs-lookup"><span data-stu-id="4dba6-111">Because `pack` and `restore` are  MSBuild targets, you can access them to enhance your workflow.</span></span> <span data-ttu-id="4dba6-112">例如，假设希望在打包后将包复制到网络共享。</span><span class="sxs-lookup"><span data-stu-id="4dba6-112">For example, let’s say you want to copy your package to a network share after packing it.</span></span> <span data-ttu-id="4dba6-113">此操作可通过向项目文件中添加以下内容来完成：</span><span class="sxs-lookup"><span data-stu-id="4dba6-113">You can do that by adding the following in your project file:</span></span>

```xml
<Target Name="CopyPackage" AfterTargets="Pack">
  <Copy
    SourceFiles="$(OutputPath)..\$(PackageId).$(PackageVersion).nupkg"
    DestinationFolder="\\myshare\packageshare\"
    />
</Target>
```

<span data-ttu-id="4dba6-114">同样，你可以编写 MSBuild 任务、编写自己的目标并使用 MSBuild 任务中的 NuGet 属性。</span><span class="sxs-lookup"><span data-stu-id="4dba6-114">Similarly, you can write an MSBuild task, write your own target and consume NuGet properties in the MSBuild task.</span></span>

> [!NOTE]
> <span data-ttu-id="4dba6-115">`$(OutputPath)` 是相对的，需要从项目根目录运行命令。</span><span class="sxs-lookup"><span data-stu-id="4dba6-115">`$(OutputPath)` is relative and expects that you are running the command from the project root.</span></span>

## <a name="pack-target"></a><span data-ttu-id="4dba6-116">包目标</span><span class="sxs-lookup"><span data-stu-id="4dba6-116">pack target</span></span>

<span data-ttu-id="4dba6-117">对于使用格式的 .NET 项目 `PackageReference` ，使用 `msbuild -t:pack` 可以从项目文件中绘制输入，以在创建 NuGet 包时使用。</span><span class="sxs-lookup"><span data-stu-id="4dba6-117">For .NET projects that use the `PackageReference` format, using `msbuild -t:pack` draws inputs from the project file to use in creating a NuGet package.</span></span>

<span data-ttu-id="4dba6-118">下表描述了可添加到第一个节点内的项目文件中的 MSBuild 属性 `<PropertyGroup>` 。</span><span class="sxs-lookup"><span data-stu-id="4dba6-118">The following table describes the MSBuild properties that can be added to a project file within the first `<PropertyGroup>` node.</span></span> <span data-ttu-id="4dba6-119">在 Visual Studio 2017 及更高版本中，通过右键单击项目并选择上下文菜单上的“编辑 {project_name}”，即可轻松进行这些编辑。</span><span class="sxs-lookup"><span data-stu-id="4dba6-119">You can make these edits easily in Visual Studio 2017 and later by right-clicking the project and selecting **Edit {project_name}** on the context menu.</span></span> <span data-ttu-id="4dba6-120">为方便起见，表按[ `.nuspec` 文件](../reference/nuspec.md)中的等效属性进行组织。</span><span class="sxs-lookup"><span data-stu-id="4dba6-120">For convenience, the table is organized by the equivalent property in a [`.nuspec` file](../reference/nuspec.md).</span></span>

<span data-ttu-id="4dba6-121">请注意，`.nuspec` 的 `Owners` 和 `Summary` 属性不受 MSBuild 支持。</span><span class="sxs-lookup"><span data-stu-id="4dba6-121">Note that the `Owners` and `Summary` properties from `.nuspec` are not supported with MSBuild.</span></span>

| <span data-ttu-id="4dba6-122">属性/NuSpec 值</span><span class="sxs-lookup"><span data-stu-id="4dba6-122">Attribute/NuSpec Value</span></span> | <span data-ttu-id="4dba6-123">MSBuild 属性</span><span class="sxs-lookup"><span data-stu-id="4dba6-123">MSBuild Property</span></span> | <span data-ttu-id="4dba6-124">默认</span><span class="sxs-lookup"><span data-stu-id="4dba6-124">Default</span></span> | <span data-ttu-id="4dba6-125">说明</span><span class="sxs-lookup"><span data-stu-id="4dba6-125">Notes</span></span> |
|--------|--------|--------|--------|
| <span data-ttu-id="4dba6-126">ID</span><span class="sxs-lookup"><span data-stu-id="4dba6-126">Id</span></span> | <span data-ttu-id="4dba6-127">PackageId</span><span class="sxs-lookup"><span data-stu-id="4dba6-127">PackageId</span></span> | <span data-ttu-id="4dba6-128">AssemblyName</span><span class="sxs-lookup"><span data-stu-id="4dba6-128">AssemblyName</span></span> | <span data-ttu-id="4dba6-129">MSBuild 的 $(AssemblyName)</span><span class="sxs-lookup"><span data-stu-id="4dba6-129">$(AssemblyName) from MSBuild</span></span> |
| <span data-ttu-id="4dba6-130">版本</span><span class="sxs-lookup"><span data-stu-id="4dba6-130">Version</span></span> | <span data-ttu-id="4dba6-131">PackageVersion</span><span class="sxs-lookup"><span data-stu-id="4dba6-131">PackageVersion</span></span> | <span data-ttu-id="4dba6-132">版本</span><span class="sxs-lookup"><span data-stu-id="4dba6-132">Version</span></span> | <span data-ttu-id="4dba6-133">这与 SemVer 兼容，例如，“1.0.0”、“1.0.0-beta”或“1.0.0-beta-00345”</span><span class="sxs-lookup"><span data-stu-id="4dba6-133">This is semver compatible, for example “1.0.0”, “1.0.0-beta”, or “1.0.0-beta-00345”</span></span> |
| <span data-ttu-id="4dba6-134">VersionPrefix</span><span class="sxs-lookup"><span data-stu-id="4dba6-134">VersionPrefix</span></span> | <span data-ttu-id="4dba6-135">PackageVersionPrefix</span><span class="sxs-lookup"><span data-stu-id="4dba6-135">PackageVersionPrefix</span></span> | <span data-ttu-id="4dba6-136">empty</span><span class="sxs-lookup"><span data-stu-id="4dba6-136">empty</span></span> | <span data-ttu-id="4dba6-137">设置 PackageVersion 会覆盖 PackageVersionPrefix</span><span class="sxs-lookup"><span data-stu-id="4dba6-137">Setting PackageVersion overwrites PackageVersionPrefix</span></span> |
| <span data-ttu-id="4dba6-138">VersionSuffix</span><span class="sxs-lookup"><span data-stu-id="4dba6-138">VersionSuffix</span></span> | <span data-ttu-id="4dba6-139">PackageVersionSuffix</span><span class="sxs-lookup"><span data-stu-id="4dba6-139">PackageVersionSuffix</span></span> | <span data-ttu-id="4dba6-140">empty</span><span class="sxs-lookup"><span data-stu-id="4dba6-140">empty</span></span> | <span data-ttu-id="4dba6-141">MSBuild 的 $(VersionSuffix)。</span><span class="sxs-lookup"><span data-stu-id="4dba6-141">$(VersionSuffix) from MSBuild.</span></span> <span data-ttu-id="4dba6-142">设置 PackageVersion 会覆盖 PackageVersionSuffix</span><span class="sxs-lookup"><span data-stu-id="4dba6-142">Setting PackageVersion overwrites PackageVersionSuffix</span></span> |
| <span data-ttu-id="4dba6-143">Authors</span><span class="sxs-lookup"><span data-stu-id="4dba6-143">Authors</span></span> | <span data-ttu-id="4dba6-144">Authors</span><span class="sxs-lookup"><span data-stu-id="4dba6-144">Authors</span></span> | <span data-ttu-id="4dba6-145">当前用户的用户名</span><span class="sxs-lookup"><span data-stu-id="4dba6-145">Username of the current user</span></span> | <span data-ttu-id="4dba6-146">其中名称以分号分隔的包作者列表，其中名称与 nuget.org 上的配置文件名称匹配。这些信息显示在 nuget.org 上的 NuGet 库中，并用于交叉引用同一作者的包。</span><span class="sxs-lookup"><span data-stu-id="4dba6-146">A semicolon-separated list of packages authors, matching the profile names on nuget.org. These are displayed in the NuGet Gallery on nuget.org and are used to cross-reference packages by the same authors.</span></span> |
| <span data-ttu-id="4dba6-147">所有者</span><span class="sxs-lookup"><span data-stu-id="4dba6-147">Owners</span></span> | <span data-ttu-id="4dba6-148">空值</span><span class="sxs-lookup"><span data-stu-id="4dba6-148">N/A</span></span> | <span data-ttu-id="4dba6-149">NuSpec 中不存在</span><span class="sxs-lookup"><span data-stu-id="4dba6-149">Not present in NuSpec</span></span> | |
| <span data-ttu-id="4dba6-150">标题</span><span class="sxs-lookup"><span data-stu-id="4dba6-150">Title</span></span> | <span data-ttu-id="4dba6-151">标题</span><span class="sxs-lookup"><span data-stu-id="4dba6-151">Title</span></span> | <span data-ttu-id="4dba6-152">PackageId</span><span class="sxs-lookup"><span data-stu-id="4dba6-152">The PackageId</span></span>| <span data-ttu-id="4dba6-153">明了易用的包标题，通常用在 UI 显示中，如 nuget.org 上和 Visual Studio 中包管理器上的那样。</span><span class="sxs-lookup"><span data-stu-id="4dba6-153">A human-friendly title of the package, typically used in UI displays as on nuget.org and the Package Manager in Visual Studio.</span></span> |
| <span data-ttu-id="4dba6-154">说明</span><span class="sxs-lookup"><span data-stu-id="4dba6-154">Description</span></span> | <span data-ttu-id="4dba6-155">说明</span><span class="sxs-lookup"><span data-stu-id="4dba6-155">Description</span></span> | <span data-ttu-id="4dba6-156">“包描述”</span><span class="sxs-lookup"><span data-stu-id="4dba6-156">"Package Description"</span></span> | <span data-ttu-id="4dba6-157">程序集的详细说明。</span><span class="sxs-lookup"><span data-stu-id="4dba6-157">A long description for the assembly.</span></span> <span data-ttu-id="4dba6-158">如果未指定 `PackageDescription`，则此属性还可用作包的说明。</span><span class="sxs-lookup"><span data-stu-id="4dba6-158">If `PackageDescription` is not specified, then this property is also used as the description of the package.</span></span> |
| <span data-ttu-id="4dba6-159">Copyright</span><span class="sxs-lookup"><span data-stu-id="4dba6-159">Copyright</span></span> | <span data-ttu-id="4dba6-160">Copyright</span><span class="sxs-lookup"><span data-stu-id="4dba6-160">Copyright</span></span> | <span data-ttu-id="4dba6-161">empty</span><span class="sxs-lookup"><span data-stu-id="4dba6-161">empty</span></span> | <span data-ttu-id="4dba6-162">包的版权详细信息。</span><span class="sxs-lookup"><span data-stu-id="4dba6-162">Copyright details for the package.</span></span> |
| <span data-ttu-id="4dba6-163">RequireLicenseAcceptance</span><span class="sxs-lookup"><span data-stu-id="4dba6-163">RequireLicenseAcceptance</span></span> | <span data-ttu-id="4dba6-164">PackageRequireLicenseAcceptance</span><span class="sxs-lookup"><span data-stu-id="4dba6-164">PackageRequireLicenseAcceptance</span></span> | <span data-ttu-id="4dba6-165">false</span><span class="sxs-lookup"><span data-stu-id="4dba6-165">false</span></span> | <span data-ttu-id="4dba6-166">一个布尔值，指定客户端是否必须提示使用者接受包许可证后才可安装包。</span><span class="sxs-lookup"><span data-stu-id="4dba6-166">A Boolean value that specifies whether the client must prompt the consumer to accept the package license before installing the package.</span></span> |
| <span data-ttu-id="4dba6-167">license</span><span class="sxs-lookup"><span data-stu-id="4dba6-167">license</span></span> | <span data-ttu-id="4dba6-168">PackageLicenseExpression</span><span class="sxs-lookup"><span data-stu-id="4dba6-168">PackageLicenseExpression</span></span> | <span data-ttu-id="4dba6-169">empty</span><span class="sxs-lookup"><span data-stu-id="4dba6-169">empty</span></span> | <span data-ttu-id="4dba6-170">对应到 `<license type="expression">`。</span><span class="sxs-lookup"><span data-stu-id="4dba6-170">Corresponds to `<license type="expression">`.</span></span> <span data-ttu-id="4dba6-171">请参阅 [打包许可证表达式或许可证文件](#packing-a-license-expression-or-a-license-file)。</span><span class="sxs-lookup"><span data-stu-id="4dba6-171">See [Packing a license expression or a license file](#packing-a-license-expression-or-a-license-file).</span></span> |
| <span data-ttu-id="4dba6-172">license</span><span class="sxs-lookup"><span data-stu-id="4dba6-172">license</span></span> | <span data-ttu-id="4dba6-173">PackageLicenseFile</span><span class="sxs-lookup"><span data-stu-id="4dba6-173">PackageLicenseFile</span></span> | <span data-ttu-id="4dba6-174">empty</span><span class="sxs-lookup"><span data-stu-id="4dba6-174">empty</span></span> | <span data-ttu-id="4dba6-175">如果使用的是未分配 SPDX 标识符的自定义许可证或许可证，则为包内的许可证文件的路径。</span><span class="sxs-lookup"><span data-stu-id="4dba6-175">Path to a license file within the package if you're using a custom license or a license that hasn't been assigned an SPDX identifier.</span></span> <span data-ttu-id="4dba6-176">需要显式打包所引用的许可证文件。</span><span class="sxs-lookup"><span data-stu-id="4dba6-176">You need to explicitly pack the referenced license file.</span></span> <span data-ttu-id="4dba6-177">对应到 `<license type="file">`。</span><span class="sxs-lookup"><span data-stu-id="4dba6-177">Corresponds to `<license type="file">`.</span></span> <span data-ttu-id="4dba6-178">请参阅 [打包许可证表达式或许可证文件](#packing-a-license-expression-or-a-license-file)。</span><span class="sxs-lookup"><span data-stu-id="4dba6-178">See [Packing a license expression or a license file](#packing-a-license-expression-or-a-license-file).</span></span> |
| <span data-ttu-id="4dba6-179">LicenseUrl</span><span class="sxs-lookup"><span data-stu-id="4dba6-179">LicenseUrl</span></span> | <span data-ttu-id="4dba6-180">PackageLicenseUrl</span><span class="sxs-lookup"><span data-stu-id="4dba6-180">PackageLicenseUrl</span></span> | <span data-ttu-id="4dba6-181">empty</span><span class="sxs-lookup"><span data-stu-id="4dba6-181">empty</span></span> | <span data-ttu-id="4dba6-182">`PackageLicenseUrl` 已弃用。</span><span class="sxs-lookup"><span data-stu-id="4dba6-182">`PackageLicenseUrl` is deprecated.</span></span> <span data-ttu-id="4dba6-183">请改用 `PackageLicenseExpression` 或 `PackageLicenseFile`。</span><span class="sxs-lookup"><span data-stu-id="4dba6-183">Use `PackageLicenseExpression` or `PackageLicenseFile` instead.</span></span> |
| <span data-ttu-id="4dba6-184">ProjectUrl</span><span class="sxs-lookup"><span data-stu-id="4dba6-184">ProjectUrl</span></span> | <span data-ttu-id="4dba6-185">PackageProjectUrl</span><span class="sxs-lookup"><span data-stu-id="4dba6-185">PackageProjectUrl</span></span> | <span data-ttu-id="4dba6-186">empty</span><span class="sxs-lookup"><span data-stu-id="4dba6-186">empty</span></span> | |
| <span data-ttu-id="4dba6-187">图标</span><span class="sxs-lookup"><span data-stu-id="4dba6-187">Icon</span></span> | <span data-ttu-id="4dba6-188">PackageIcon</span><span class="sxs-lookup"><span data-stu-id="4dba6-188">PackageIcon</span></span> | <span data-ttu-id="4dba6-189">empty</span><span class="sxs-lookup"><span data-stu-id="4dba6-189">empty</span></span> | <span data-ttu-id="4dba6-190">包中要用作包图标的图像的路径。</span><span class="sxs-lookup"><span data-stu-id="4dba6-190">A path to an image in the package to use as a package icon.</span></span> <span data-ttu-id="4dba6-191">需要显式打包所引用的图标图像文件。</span><span class="sxs-lookup"><span data-stu-id="4dba6-191">You need to explicitly pack the referenced icon image file.</span></span> <span data-ttu-id="4dba6-192">有关详细信息，请参阅[打包图标图像文件](#packing-an-icon-image-file)和[ `icon` 元数据](/nuget/reference/nuspec#icon)。</span><span class="sxs-lookup"><span data-stu-id="4dba6-192">For more information, see [Packing an icon image file](#packing-an-icon-image-file) and [`icon` metadata](/nuget/reference/nuspec#icon).</span></span> |
| <span data-ttu-id="4dba6-193">IconUrl</span><span class="sxs-lookup"><span data-stu-id="4dba6-193">IconUrl</span></span> | <span data-ttu-id="4dba6-194">PackageIconUrl</span><span class="sxs-lookup"><span data-stu-id="4dba6-194">PackageIconUrl</span></span> | <span data-ttu-id="4dba6-195">empty</span><span class="sxs-lookup"><span data-stu-id="4dba6-195">empty</span></span> | <span data-ttu-id="4dba6-196">`PackageIconUrl` 对于，已弃用 `PackageIcon` 。</span><span class="sxs-lookup"><span data-stu-id="4dba6-196">`PackageIconUrl` is deprecated in favor of `PackageIcon`.</span></span> <span data-ttu-id="4dba6-197">但是，为了获得最佳的下层体验，除了指定外，还应该指定 `PackageIconUrl` `PackageIcon` 。</span><span class="sxs-lookup"><span data-stu-id="4dba6-197">However, for the best downlevel experience, you should specify `PackageIconUrl` in addition to `PackageIcon`.</span></span> |
| <span data-ttu-id="4dba6-198">Tags</span><span class="sxs-lookup"><span data-stu-id="4dba6-198">Tags</span></span> | <span data-ttu-id="4dba6-199">PackageTags</span><span class="sxs-lookup"><span data-stu-id="4dba6-199">PackageTags</span></span> | <span data-ttu-id="4dba6-200">empty</span><span class="sxs-lookup"><span data-stu-id="4dba6-200">empty</span></span> | <span data-ttu-id="4dba6-201">标记的分号分隔列表，这些标记用于指定包。</span><span class="sxs-lookup"><span data-stu-id="4dba6-201">A semicolon-delimited list of tags that designates the package.</span></span> |
| <span data-ttu-id="4dba6-202">ReleaseNotes</span><span class="sxs-lookup"><span data-stu-id="4dba6-202">ReleaseNotes</span></span> | <span data-ttu-id="4dba6-203">PackageReleaseNotes</span><span class="sxs-lookup"><span data-stu-id="4dba6-203">PackageReleaseNotes</span></span> | <span data-ttu-id="4dba6-204">empty</span><span class="sxs-lookup"><span data-stu-id="4dba6-204">empty</span></span> | <span data-ttu-id="4dba6-205">包的发行说明。</span><span class="sxs-lookup"><span data-stu-id="4dba6-205">Release notes for the package.</span></span> |
| <span data-ttu-id="4dba6-206">存储库/Url</span><span class="sxs-lookup"><span data-stu-id="4dba6-206">Repository/Url</span></span> | <span data-ttu-id="4dba6-207">RepositoryUrl</span><span class="sxs-lookup"><span data-stu-id="4dba6-207">RepositoryUrl</span></span> | <span data-ttu-id="4dba6-208">empty</span><span class="sxs-lookup"><span data-stu-id="4dba6-208">empty</span></span> | <span data-ttu-id="4dba6-209">用于克隆或检索源代码的存储库 URL。</span><span class="sxs-lookup"><span data-stu-id="4dba6-209">Repository URL used to clone or retrieve source code.</span></span> <span data-ttu-id="4dba6-210">示例： *https://github.com/NuGet/NuGet.Client.git* 。</span><span class="sxs-lookup"><span data-stu-id="4dba6-210">Example: *https://github.com/NuGet/NuGet.Client.git*.</span></span> |
| <span data-ttu-id="4dba6-211">存储库/类型</span><span class="sxs-lookup"><span data-stu-id="4dba6-211">Repository/Type</span></span> | <span data-ttu-id="4dba6-212">RepositoryType</span><span class="sxs-lookup"><span data-stu-id="4dba6-212">RepositoryType</span></span> | <span data-ttu-id="4dba6-213">empty</span><span class="sxs-lookup"><span data-stu-id="4dba6-213">empty</span></span> | <span data-ttu-id="4dba6-214">存储库类型。</span><span class="sxs-lookup"><span data-stu-id="4dba6-214">Repository type.</span></span> <span data-ttu-id="4dba6-215">示例： `git` (默认) ， `tfs` 。</span><span class="sxs-lookup"><span data-stu-id="4dba6-215">Examples: `git` (default), `tfs`.</span></span> |
| <span data-ttu-id="4dba6-216">存储库/分支</span><span class="sxs-lookup"><span data-stu-id="4dba6-216">Repository/Branch</span></span> | <span data-ttu-id="4dba6-217">RepositoryBranch</span><span class="sxs-lookup"><span data-stu-id="4dba6-217">RepositoryBranch</span></span> | <span data-ttu-id="4dba6-218">empty</span><span class="sxs-lookup"><span data-stu-id="4dba6-218">empty</span></span> | <span data-ttu-id="4dba6-219">可选存储库分支信息。</span><span class="sxs-lookup"><span data-stu-id="4dba6-219">Optional repository branch information.</span></span> <span data-ttu-id="4dba6-220">还必须指定 `RepositoryUrl` 才能包含此属性。</span><span class="sxs-lookup"><span data-stu-id="4dba6-220">`RepositoryUrl` must also be specified for this property to be included.</span></span> <span data-ttu-id="4dba6-221">示例： *master* (NuGet 4.7.0 +) 。</span><span class="sxs-lookup"><span data-stu-id="4dba6-221">Example: *master* (NuGet 4.7.0+).</span></span> |
| <span data-ttu-id="4dba6-222">存储库/提交</span><span class="sxs-lookup"><span data-stu-id="4dba6-222">Repository/Commit</span></span> | <span data-ttu-id="4dba6-223">RepositoryCommit</span><span class="sxs-lookup"><span data-stu-id="4dba6-223">RepositoryCommit</span></span> | <span data-ttu-id="4dba6-224">empty</span><span class="sxs-lookup"><span data-stu-id="4dba6-224">empty</span></span> | <span data-ttu-id="4dba6-225">可选的存储库提交或更改集，指示针对其生成包的源。</span><span class="sxs-lookup"><span data-stu-id="4dba6-225">Optional repository commit or changeset to indicate which source the package was built against.</span></span> <span data-ttu-id="4dba6-226">还必须指定 `RepositoryUrl` 才能包含此属性。</span><span class="sxs-lookup"><span data-stu-id="4dba6-226">`RepositoryUrl` must also be specified for this property to be included.</span></span> <span data-ttu-id="4dba6-227">示例： *0e4d1b598f350b3dc675018d539114d1328189ef* (NuGet 4.7.0 +) 。</span><span class="sxs-lookup"><span data-stu-id="4dba6-227">Example: *0e4d1b598f350b3dc675018d539114d1328189ef* (NuGet 4.7.0+).</span></span> |
| <span data-ttu-id="4dba6-228">PackageType</span><span class="sxs-lookup"><span data-stu-id="4dba6-228">PackageType</span></span> | `<PackageType>DotNetCliTool, 1.0.0.0;Dependency, 2.0.0.0</PackageType>` | | |
| <span data-ttu-id="4dba6-229">总结</span><span class="sxs-lookup"><span data-stu-id="4dba6-229">Summary</span></span> | <span data-ttu-id="4dba6-230">不支持</span><span class="sxs-lookup"><span data-stu-id="4dba6-230">Not supported</span></span> | | |

### <a name="pack-target-inputs"></a><span data-ttu-id="4dba6-231">包目标输入</span><span class="sxs-lookup"><span data-stu-id="4dba6-231">pack target inputs</span></span>

| <span data-ttu-id="4dba6-232">properties</span><span class="sxs-lookup"><span data-stu-id="4dba6-232">Property</span></span> | <span data-ttu-id="4dba6-233">说明</span><span class="sxs-lookup"><span data-stu-id="4dba6-233">Description</span></span> |
| - | - |
| <span data-ttu-id="4dba6-234">IsPackable</span><span class="sxs-lookup"><span data-stu-id="4dba6-234">IsPackable</span></span> | <span data-ttu-id="4dba6-235">一个指定能否打包项目的布尔值。</span><span class="sxs-lookup"><span data-stu-id="4dba6-235">A Boolean value that specifies whether the project can be packed.</span></span> <span data-ttu-id="4dba6-236">默认值为 `true`。</span><span class="sxs-lookup"><span data-stu-id="4dba6-236">The default value is `true`.</span></span> |
| <span data-ttu-id="4dba6-237">SuppressDependenciesWhenPacking</span><span class="sxs-lookup"><span data-stu-id="4dba6-237">SuppressDependenciesWhenPacking</span></span> | <span data-ttu-id="4dba6-238">设置为 `true` 以从生成的 NuGet 包中取消包依赖项。</span><span class="sxs-lookup"><span data-stu-id="4dba6-238">Set to `true` to suppress package dependencies from the generated NuGet package.</span></span> |
| <span data-ttu-id="4dba6-239">PackageVersion</span><span class="sxs-lookup"><span data-stu-id="4dba6-239">PackageVersion</span></span> | <span data-ttu-id="4dba6-240">指定生成的包所具有的版本。</span><span class="sxs-lookup"><span data-stu-id="4dba6-240">Specifies the version that the resulting package will have.</span></span> <span data-ttu-id="4dba6-241">接受所有形式的 NuGet 版本字符串。</span><span class="sxs-lookup"><span data-stu-id="4dba6-241">Accepts all forms of NuGet version string.</span></span> <span data-ttu-id="4dba6-242">默认为值 `$(Version)`，即项目中 `Version` 属性的值。</span><span class="sxs-lookup"><span data-stu-id="4dba6-242">Default is the value of `$(Version)`, that is, of the property `Version` in the project.</span></span> |
| <span data-ttu-id="4dba6-243">PackageId</span><span class="sxs-lookup"><span data-stu-id="4dba6-243">PackageId</span></span> | <span data-ttu-id="4dba6-244">指定生成的包的名称。</span><span class="sxs-lookup"><span data-stu-id="4dba6-244">Specifies the name for the resulting package.</span></span> <span data-ttu-id="4dba6-245">如果未指定，`pack` 操作将默认使用 `AssemblyName` 或目录名称作为包的名称。</span><span class="sxs-lookup"><span data-stu-id="4dba6-245">If not specified, the `pack` operation will default to using the `AssemblyName` or directory name as the name of the package.</span></span> |
| <span data-ttu-id="4dba6-246">PackageDescription</span><span class="sxs-lookup"><span data-stu-id="4dba6-246">PackageDescription</span></span> | <span data-ttu-id="4dba6-247">用于 UI 显示的包的详细说明。</span><span class="sxs-lookup"><span data-stu-id="4dba6-247">A long description of the package for UI display.</span></span> |
| <span data-ttu-id="4dba6-248">Authors</span><span class="sxs-lookup"><span data-stu-id="4dba6-248">Authors</span></span> | <span data-ttu-id="4dba6-249">其中名称以分号分隔的包作者列表，其中名称与 nuget.org 上的配置文件名称匹配。这些信息显示在 nuget.org 上的 NuGet 库中，并用于交叉引用同一作者的包。</span><span class="sxs-lookup"><span data-stu-id="4dba6-249">A semicolon-separated list of packages authors, matching the profile names on nuget.org. These are displayed in the NuGet Gallery on nuget.org and are used to cross-reference packages by the same authors.</span></span> |
| <span data-ttu-id="4dba6-250">Description</span><span class="sxs-lookup"><span data-stu-id="4dba6-250">Description</span></span> | <span data-ttu-id="4dba6-251">程序集的详细说明。</span><span class="sxs-lookup"><span data-stu-id="4dba6-251">A long description for the assembly.</span></span> <span data-ttu-id="4dba6-252">如果未指定 `PackageDescription`，则此属性还可用作包的说明。</span><span class="sxs-lookup"><span data-stu-id="4dba6-252">If `PackageDescription` is not specified, then this property is also used as the description of the package.</span></span> |
| <span data-ttu-id="4dba6-253">Copyright</span><span class="sxs-lookup"><span data-stu-id="4dba6-253">Copyright</span></span> | <span data-ttu-id="4dba6-254">包的版权详细信息。</span><span class="sxs-lookup"><span data-stu-id="4dba6-254">Copyright details for the package.</span></span> |
| <span data-ttu-id="4dba6-255">PackageRequireLicenseAcceptance</span><span class="sxs-lookup"><span data-stu-id="4dba6-255">PackageRequireLicenseAcceptance</span></span> | <span data-ttu-id="4dba6-256">一个布尔值，指定客户端是否必须提示使用者接受包许可证后才可安装包。</span><span class="sxs-lookup"><span data-stu-id="4dba6-256">A Boolean value that specifies whether the client must prompt the consumer to accept the package license before installing the package.</span></span> <span data-ttu-id="4dba6-257">默认值为 `false`。</span><span class="sxs-lookup"><span data-stu-id="4dba6-257">The default is `false`.</span></span> |
| <span data-ttu-id="4dba6-258">DevelopmentDependency</span><span class="sxs-lookup"><span data-stu-id="4dba6-258">DevelopmentDependency</span></span> | <span data-ttu-id="4dba6-259">一个布尔值，用于指定包是否被标记为仅开发依赖项，从而防止包作为依赖项包含到其他包中。</span><span class="sxs-lookup"><span data-stu-id="4dba6-259">A Boolean value that specifies whether the package is marked as a development-only dependency, which prevents the package from being included as a dependency in other packages.</span></span> <span data-ttu-id="4dba6-260">在 `PackageReference` (NuGet 4.8 +) 中，此标志还意味着编译时资产将从编译中排除。</span><span class="sxs-lookup"><span data-stu-id="4dba6-260">With `PackageReference` (NuGet 4.8+), this flag also means that compile-time assets are excluded from compilation.</span></span> <span data-ttu-id="4dba6-261">有关详细信息，请参阅 [PackageReference 的 DevelopmentDependency 支持](https://github.com/NuGet/Home/wiki/DevelopmentDependency-support-for-PackageReference)。</span><span class="sxs-lookup"><span data-stu-id="4dba6-261">For more information, see [DevelopmentDependency support for PackageReference](https://github.com/NuGet/Home/wiki/DevelopmentDependency-support-for-PackageReference).</span></span> |
| <span data-ttu-id="4dba6-262">PackageLicenseExpression</span><span class="sxs-lookup"><span data-stu-id="4dba6-262">PackageLicenseExpression</span></span> | <span data-ttu-id="4dba6-263">[SPDX 许可证标识符](https://spdx.org/licenses/)或表达式，例如 `Apache-2.0` 。</span><span class="sxs-lookup"><span data-stu-id="4dba6-263">An [SPDX license identifier](https://spdx.org/licenses/) or expression, for example, `Apache-2.0`.</span></span> <span data-ttu-id="4dba6-264">有关详细信息，请参阅 [打包许可证表达式或许可证文件](#packing-a-license-expression-or-a-license-file)。</span><span class="sxs-lookup"><span data-stu-id="4dba6-264">For more information, see [Packing a license expression or a license file](#packing-a-license-expression-or-a-license-file).</span></span> |
| <span data-ttu-id="4dba6-265">PackageLicenseFile</span><span class="sxs-lookup"><span data-stu-id="4dba6-265">PackageLicenseFile</span></span> | <span data-ttu-id="4dba6-266">如果使用的是未分配 SPDX 标识符的自定义许可证或许可证，则为包内的许可证文件的路径。</span><span class="sxs-lookup"><span data-stu-id="4dba6-266">Path to a license file within the package if you're using a custom license or a license that hasn't been assigned an SPDX identifier.</span></span> |
| <span data-ttu-id="4dba6-267">PackageLicenseUrl</span><span class="sxs-lookup"><span data-stu-id="4dba6-267">PackageLicenseUrl</span></span> | <span data-ttu-id="4dba6-268">`PackageLicenseUrl` 已弃用。</span><span class="sxs-lookup"><span data-stu-id="4dba6-268">`PackageLicenseUrl` is deprecated.</span></span> <span data-ttu-id="4dba6-269">请改用 `PackageLicenseExpression` 或 `PackageLicenseFile`。</span><span class="sxs-lookup"><span data-stu-id="4dba6-269">Use `PackageLicenseExpression` or `PackageLicenseFile` instead.</span></span> |
| <span data-ttu-id="4dba6-270">PackageProjectUrl</span><span class="sxs-lookup"><span data-stu-id="4dba6-270">PackageProjectUrl</span></span> | |
| <span data-ttu-id="4dba6-271">PackageIcon</span><span class="sxs-lookup"><span data-stu-id="4dba6-271">PackageIcon</span></span> | <span data-ttu-id="4dba6-272">指定相对于包根的包图标路径。</span><span class="sxs-lookup"><span data-stu-id="4dba6-272">Specifies the package icon path, relative to the root of the package.</span></span> <span data-ttu-id="4dba6-273">有关详细信息，请参阅对 [图标图像文件进行打包](#packing-an-icon-image-file)。</span><span class="sxs-lookup"><span data-stu-id="4dba6-273">For more information, see [Packing an icon image file](#packing-an-icon-image-file).</span></span> |
| <span data-ttu-id="4dba6-274">PackageReleaseNotes</span><span class="sxs-lookup"><span data-stu-id="4dba6-274">PackageReleaseNotes</span></span>| <span data-ttu-id="4dba6-275">包的发行说明。</span><span class="sxs-lookup"><span data-stu-id="4dba6-275">Release notes for the package.</span></span> |
| <span data-ttu-id="4dba6-276">PackageTags</span><span class="sxs-lookup"><span data-stu-id="4dba6-276">PackageTags</span></span> | <span data-ttu-id="4dba6-277">标记的分号分隔列表，这些标记用于指定包。</span><span class="sxs-lookup"><span data-stu-id="4dba6-277">A semicolon-delimited list of tags that designates the package.</span></span> |
| <span data-ttu-id="4dba6-278">PackageOutputPath</span><span class="sxs-lookup"><span data-stu-id="4dba6-278">PackageOutputPath</span></span> | <span data-ttu-id="4dba6-279">确定用于已打包的包的输出路径。</span><span class="sxs-lookup"><span data-stu-id="4dba6-279">Determines the output path in which the packed package will be dropped.</span></span> <span data-ttu-id="4dba6-280">默认值为 `$(OutputPath)`。</span><span class="sxs-lookup"><span data-stu-id="4dba6-280">Default is `$(OutputPath)`.</span></span> |
| <span data-ttu-id="4dba6-281">IncludeSymbols</span><span class="sxs-lookup"><span data-stu-id="4dba6-281">IncludeSymbols</span></span> | <span data-ttu-id="4dba6-282">此布尔值指示在打包项目时，包是否应创建一个附加的符号包。</span><span class="sxs-lookup"><span data-stu-id="4dba6-282">This Boolean value indicates whether the package should create an additional symbols package when the project is packed.</span></span> <span data-ttu-id="4dba6-283">符号包的格式由 `SymbolPackageFormat` 属性控制。</span><span class="sxs-lookup"><span data-stu-id="4dba6-283">The symbols package's format is controlled by the `SymbolPackageFormat` property.</span></span> <span data-ttu-id="4dba6-284">有关详细信息，请参阅 [IncludeSymbols](#includesymbols)。</span><span class="sxs-lookup"><span data-stu-id="4dba6-284">For more information, see [IncludeSymbols](#includesymbols).</span></span> |
| <span data-ttu-id="4dba6-285">IncludeSource</span><span class="sxs-lookup"><span data-stu-id="4dba6-285">IncludeSource</span></span> | <span data-ttu-id="4dba6-286">此布尔值指示包进程是否应创建源包。</span><span class="sxs-lookup"><span data-stu-id="4dba6-286">This Boolean value indicates whether the pack process should create a source package.</span></span> <span data-ttu-id="4dba6-287">源包中包含库的源代码以及 PDB 文件。</span><span class="sxs-lookup"><span data-stu-id="4dba6-287">The source package contains the library's source code as well as PDB files.</span></span> <span data-ttu-id="4dba6-288">源文件置于生成的包文件中的 `src/ProjectName` 目录下。</span><span class="sxs-lookup"><span data-stu-id="4dba6-288">Source files are put under the `src/ProjectName` directory in the resulting package file.</span></span> <span data-ttu-id="4dba6-289">有关详细信息，请参阅 [IncludeSource](#includesource)。</span><span class="sxs-lookup"><span data-stu-id="4dba6-289">For more information, see [IncludeSource](#includesource).</span></span> |
| <span data-ttu-id="4dba6-290">PackageTypes</span><span class="sxs-lookup"><span data-stu-id="4dba6-290">PackageTypes</span></span>
| <span data-ttu-id="4dba6-291">IsTool</span><span class="sxs-lookup"><span data-stu-id="4dba6-291">IsTool</span></span> | <span data-ttu-id="4dba6-292">指定是否将所有输出文件复制到 *tools* 文件夹，而不是 *lib* 文件夹。</span><span class="sxs-lookup"><span data-stu-id="4dba6-292">Specifies whether all output files are copied to the *tools* folder instead of the *lib* folder.</span></span> <span data-ttu-id="4dba6-293">有关详细信息，请参阅 [IsTool](#istool)。</span><span class="sxs-lookup"><span data-stu-id="4dba6-293">For more information, see [IsTool](#istool).</span></span> |
| <span data-ttu-id="4dba6-294">RepositoryUrl</span><span class="sxs-lookup"><span data-stu-id="4dba6-294">RepositoryUrl</span></span> | <span data-ttu-id="4dba6-295">用于克隆或检索源代码的存储库 URL。</span><span class="sxs-lookup"><span data-stu-id="4dba6-295">Repository URL used to clone or retrieve source code.</span></span> <span data-ttu-id="4dba6-296">示例： *https://github.com/NuGet/NuGet.Client.git* 。</span><span class="sxs-lookup"><span data-stu-id="4dba6-296">Example: *https://github.com/NuGet/NuGet.Client.git*.</span></span> |
| <span data-ttu-id="4dba6-297">RepositoryType</span><span class="sxs-lookup"><span data-stu-id="4dba6-297">RepositoryType</span></span> | <span data-ttu-id="4dba6-298">存储库类型。</span><span class="sxs-lookup"><span data-stu-id="4dba6-298">Repository type.</span></span> <span data-ttu-id="4dba6-299">示例： `git` (默认) ， `tfs` 。</span><span class="sxs-lookup"><span data-stu-id="4dba6-299">Examples: `git` (default), `tfs`.</span></span> |
| <span data-ttu-id="4dba6-300">RepositoryBranch</span><span class="sxs-lookup"><span data-stu-id="4dba6-300">RepositoryBranch</span></span> | <span data-ttu-id="4dba6-301">可选存储库分支信息。</span><span class="sxs-lookup"><span data-stu-id="4dba6-301">Optional repository branch information.</span></span> <span data-ttu-id="4dba6-302">还必须指定 `RepositoryUrl` 才能包含此属性。</span><span class="sxs-lookup"><span data-stu-id="4dba6-302">`RepositoryUrl` must also be specified for this property to be included.</span></span> <span data-ttu-id="4dba6-303">示例： *master* (NuGet 4.7.0 +) 。</span><span class="sxs-lookup"><span data-stu-id="4dba6-303">Example: *master* (NuGet 4.7.0+).</span></span> |
| <span data-ttu-id="4dba6-304">RepositoryCommit</span><span class="sxs-lookup"><span data-stu-id="4dba6-304">RepositoryCommit</span></span> | <span data-ttu-id="4dba6-305">可选的存储库提交或更改集，指示针对其生成包的源。</span><span class="sxs-lookup"><span data-stu-id="4dba6-305">Optional repository commit or changeset to indicate which source the package was built against.</span></span> <span data-ttu-id="4dba6-306">还必须指定 `RepositoryUrl` 才能包含此属性。</span><span class="sxs-lookup"><span data-stu-id="4dba6-306">`RepositoryUrl` must also be specified for this property to be included.</span></span> <span data-ttu-id="4dba6-307">示例： *0e4d1b598f350b3dc675018d539114d1328189ef* (NuGet 4.7.0 +) 。</span><span class="sxs-lookup"><span data-stu-id="4dba6-307">Example: *0e4d1b598f350b3dc675018d539114d1328189ef* (NuGet 4.7.0+).</span></span> |
| <span data-ttu-id="4dba6-308">SymbolPackageFormat</span><span class="sxs-lookup"><span data-stu-id="4dba6-308">SymbolPackageFormat</span></span> | <span data-ttu-id="4dba6-309">指定符号包的格式。</span><span class="sxs-lookup"><span data-stu-id="4dba6-309">Specifies the format of the symbols package.</span></span> <span data-ttu-id="4dba6-310">如果是 "nupkg"，则会使用 *nupkg* 扩展（其中包含 Pdb、dll 和其他输出文件）创建旧的符号包。</span><span class="sxs-lookup"><span data-stu-id="4dba6-310">If "symbols.nupkg", a legacy symbols package is created with a *.symbols.nupkg* extension containing PDBs, DLLs, and other output files.</span></span> <span data-ttu-id="4dba6-311">如果是 "snupkg"，则会创建包含可移植 Pdb 的 snupkg 符号包。</span><span class="sxs-lookup"><span data-stu-id="4dba6-311">If "snupkg", a snupkg symbol package is created containing the portable PDBs.</span></span> <span data-ttu-id="4dba6-312">默认值为 "nupkg"。</span><span class="sxs-lookup"><span data-stu-id="4dba6-312">The default is "symbols.nupkg".</span></span> |
| <span data-ttu-id="4dba6-313">NoPackageAnalysis</span><span class="sxs-lookup"><span data-stu-id="4dba6-313">NoPackageAnalysis</span></span> | <span data-ttu-id="4dba6-314">指定 `pack` 不应在生成包后运行包分析。</span><span class="sxs-lookup"><span data-stu-id="4dba6-314">Specifies that `pack` should not run package analysis after building the package.</span></span> |
| <span data-ttu-id="4dba6-315">MinClientVersion</span><span class="sxs-lookup"><span data-stu-id="4dba6-315">MinClientVersion</span></span> | <span data-ttu-id="4dba6-316">指定可安装此包的最低 NuGet 客户端版本，并由 nuget.exe 和 Visual Studio 程序包管理器强制实施。</span><span class="sxs-lookup"><span data-stu-id="4dba6-316">Specifies the minimum version of the NuGet client that can install this package, enforced by nuget.exe and the Visual Studio Package Manager.</span></span> |
| <span data-ttu-id="4dba6-317">IncludeBuildOutput</span><span class="sxs-lookup"><span data-stu-id="4dba6-317">IncludeBuildOutput</span></span> | <span data-ttu-id="4dba6-318">此布尔值指定是否应将生成输出程序集打包到 .nupkg 文件中  。</span><span class="sxs-lookup"><span data-stu-id="4dba6-318">This Boolean value specifies whether the build output assemblies should be packed into the *.nupkg* file or not.</span></span> |
| <span data-ttu-id="4dba6-319">IncludeContentInPack</span><span class="sxs-lookup"><span data-stu-id="4dba6-319">IncludeContentInPack</span></span> | <span data-ttu-id="4dba6-320">此布尔值指定是否 `Content` 自动在生成的包中包含类型为的任何项。</span><span class="sxs-lookup"><span data-stu-id="4dba6-320">This Boolean value specifies whether any items that have a type of `Content` are included in the resulting package automatically.</span></span> <span data-ttu-id="4dba6-321">默认值为 `true`。</span><span class="sxs-lookup"><span data-stu-id="4dba6-321">The default is `true`.</span></span> |
| <span data-ttu-id="4dba6-322">BuildOutputTargetFolder</span><span class="sxs-lookup"><span data-stu-id="4dba6-322">BuildOutputTargetFolder</span></span> | <span data-ttu-id="4dba6-323">指定放置输出程序集的文件夹。</span><span class="sxs-lookup"><span data-stu-id="4dba6-323">Specifies the folder where to place the output assemblies.</span></span> <span data-ttu-id="4dba6-324">输出程序集（和其他输出文件）会复制到各自的框架文件夹中。</span><span class="sxs-lookup"><span data-stu-id="4dba6-324">The output assemblies (and other output files) are copied into their respective framework folders.</span></span> <span data-ttu-id="4dba6-325">有关详细信息，请参阅 [输出程序集](#output-assemblies)。</span><span class="sxs-lookup"><span data-stu-id="4dba6-325">For more information, see [Output assemblies](#output-assemblies).</span></span> |
| <span data-ttu-id="4dba6-326">ContentTargetFolders</span><span class="sxs-lookup"><span data-stu-id="4dba6-326">ContentTargetFolders</span></span> | <span data-ttu-id="4dba6-327">指定不为其指定所有内容文件的默认位置 `PackagePath` 。</span><span class="sxs-lookup"><span data-stu-id="4dba6-327">Specifies the default location of where all the content files should go if `PackagePath` is not specified for them.</span></span> <span data-ttu-id="4dba6-328">默认值为“content;contentFiles”。</span><span class="sxs-lookup"><span data-stu-id="4dba6-328">The default value is "content;contentFiles".</span></span> <span data-ttu-id="4dba6-329">有关详细信息，请参阅[在包中包含内容](#including-content-in-a-package)。</span><span class="sxs-lookup"><span data-stu-id="4dba6-329">For more information, see [Including content in a package](#including-content-in-a-package).</span></span> |
| <span data-ttu-id="4dba6-330">NuspecFile</span><span class="sxs-lookup"><span data-stu-id="4dba6-330">NuspecFile</span></span> | <span data-ttu-id="4dba6-331">用于打包的 *.nuspec* 文件的相对或绝对路径。</span><span class="sxs-lookup"><span data-stu-id="4dba6-331">Relative or absolute path to the *.nuspec* file being used for packing.</span></span> <span data-ttu-id="4dba6-332">如果已指定，则将 **专用** 于打包信息，并且不使用项目中的任何信息。</span><span class="sxs-lookup"><span data-stu-id="4dba6-332">If specified, it's used **exclusively** for packaging information, and any information in the projects is not used.</span></span> <span data-ttu-id="4dba6-333">有关详细信息，请参阅 [使用 Nuspec 打包](#packing-using-a-nuspec)。</span><span class="sxs-lookup"><span data-stu-id="4dba6-333">For more information, see [Packing using a .nuspec](#packing-using-a-nuspec).</span></span> |
| <span data-ttu-id="4dba6-334">NuspecBasePath</span><span class="sxs-lookup"><span data-stu-id="4dba6-334">NuspecBasePath</span></span> | <span data-ttu-id="4dba6-335">*.nuspec* 文件的基路径。</span><span class="sxs-lookup"><span data-stu-id="4dba6-335">Base path for the *.nuspec* file.</span></span> <span data-ttu-id="4dba6-336">有关详细信息，请参阅 [使用 Nuspec 打包](#packing-using-a-nuspec)。</span><span class="sxs-lookup"><span data-stu-id="4dba6-336">For more information, see [Packing using a .nuspec](#packing-using-a-nuspec).</span></span> |
| <span data-ttu-id="4dba6-337">NuspecProperties</span><span class="sxs-lookup"><span data-stu-id="4dba6-337">NuspecProperties</span></span> | <span data-ttu-id="4dba6-338">键=值对的分号分隔列表。</span><span class="sxs-lookup"><span data-stu-id="4dba6-338">Semicolon separated list of key=value pairs.</span></span> <span data-ttu-id="4dba6-339">有关详细信息，请参阅 [使用 Nuspec 打包](#packing-using-a-nuspec)。</span><span class="sxs-lookup"><span data-stu-id="4dba6-339">For more information, see [Packing using a .nuspec](#packing-using-a-nuspec).</span></span> |

## <a name="pack-scenarios"></a><span data-ttu-id="4dba6-340">包方案</span><span class="sxs-lookup"><span data-stu-id="4dba6-340">pack scenarios</span></span>

### <a name="suppress-dependencies"></a><span data-ttu-id="4dba6-341">禁止依赖项</span><span class="sxs-lookup"><span data-stu-id="4dba6-341">Suppress dependencies</span></span>

<span data-ttu-id="4dba6-342">若要取消生成的 NuGet 包中的包依赖项，请将设置 `SuppressDependenciesWhenPacking` 为， `true` 将允许跳过生成的 nupkg 文件中的所有依赖项。</span><span class="sxs-lookup"><span data-stu-id="4dba6-342">To suppress package dependencies from generated NuGet package, set `SuppressDependenciesWhenPacking` to `true` which will allow skipping all the dependencies from generated nupkg file.</span></span>

### <a name="packageiconurl"></a><span data-ttu-id="4dba6-343">PackageIconUrl</span><span class="sxs-lookup"><span data-stu-id="4dba6-343">PackageIconUrl</span></span>

<span data-ttu-id="4dba6-344">`PackageIconUrl` 对属性的支持已弃用 [`PackageIcon`](#packageicon) 。</span><span class="sxs-lookup"><span data-stu-id="4dba6-344">`PackageIconUrl` is deprecated in favor of the [`PackageIcon`](#packageicon) property.</span></span> <span data-ttu-id="4dba6-345">从 NuGet 5.3 和 Visual Studio 2019 版本16.3 开始， `pack` 如果包元数据仅指定了，则会引发 [NU5048](./errors-and-warnings/nu5048.md) 警告 `PackageIconUrl` 。</span><span class="sxs-lookup"><span data-stu-id="4dba6-345">Starting with NuGet 5.3 and Visual Studio 2019 version 16.3, `pack` raises the [NU5048](./errors-and-warnings/nu5048.md) warning if the package metadata only specifies `PackageIconUrl`.</span></span>

### <a name="packageicon"></a><span data-ttu-id="4dba6-346">PackageIcon</span><span class="sxs-lookup"><span data-stu-id="4dba6-346">PackageIcon</span></span>

> [!Tip]
> <span data-ttu-id="4dba6-347">若要保持与尚不支持的客户端和源的向后兼容性 `PackageIcon` ，请同时指定 `PackageIcon` 和 `PackageIconUrl` 。</span><span class="sxs-lookup"><span data-stu-id="4dba6-347">To maintain backward compatibility with clients and sources that don't yet support `PackageIcon`, specify both `PackageIcon` and `PackageIconUrl`.</span></span> <span data-ttu-id="4dba6-348">Visual Studio 支持来自 `PackageIcon` 基于文件夹的源的包。</span><span class="sxs-lookup"><span data-stu-id="4dba6-348">Visual Studio supports `PackageIcon` for packages coming from a folder-based source.</span></span>

#### <a name="packing-an-icon-image-file"></a><span data-ttu-id="4dba6-349">打包图标图像文件</span><span class="sxs-lookup"><span data-stu-id="4dba6-349">Packing an icon image file</span></span>

<span data-ttu-id="4dba6-350">打包图标图像文件时，请使用 `PackageIcon` 属性来指定图标文件路径，该路径相对于包的根。</span><span class="sxs-lookup"><span data-stu-id="4dba6-350">When packing an icon image file, use `PackageIcon` property to specify the icon file path, relative to the root of the package.</span></span> <span data-ttu-id="4dba6-351">此外，请确保该文件已包含在包中。</span><span class="sxs-lookup"><span data-stu-id="4dba6-351">In addition, make sure that the file is included in the package.</span></span> <span data-ttu-id="4dba6-352">图像文件大小限制为 1 MB。</span><span class="sxs-lookup"><span data-stu-id="4dba6-352">Image file size is limited to 1 MB.</span></span> <span data-ttu-id="4dba6-353">支持的文件格式包括 JPEG 和 PNG。</span><span class="sxs-lookup"><span data-stu-id="4dba6-353">Supported file formats include JPEG and PNG.</span></span> <span data-ttu-id="4dba6-354">建议使用128x128 的图像分辨率。</span><span class="sxs-lookup"><span data-stu-id="4dba6-354">We recommend an image resolution of 128x128.</span></span>

<span data-ttu-id="4dba6-355">例如：</span><span class="sxs-lookup"><span data-stu-id="4dba6-355">For example:</span></span>

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

<span data-ttu-id="4dba6-356">[包图标示例](https://github.com/NuGet/Samples/tree/master/PackageIconExample)。</span><span class="sxs-lookup"><span data-stu-id="4dba6-356">[Package Icon sample](https://github.com/NuGet/Samples/tree/master/PackageIconExample).</span></span>

<span data-ttu-id="4dba6-357">对于 nuspec 等效项，请查看 [图标的 nuspec 参考](nuspec.md#icon)。</span><span class="sxs-lookup"><span data-stu-id="4dba6-357">For the nuspec equivalent, take a look at [nuspec reference for icon](nuspec.md#icon).</span></span>

### <a name="output-assemblies"></a><span data-ttu-id="4dba6-358">输出程序集</span><span class="sxs-lookup"><span data-stu-id="4dba6-358">Output assemblies</span></span>

<span data-ttu-id="4dba6-359">`nuget pack` 会复制扩展名为 `.exe`、`.dll`、`.xml`、`.winmd`、`.json` 和 `.pri` 的输出文件。</span><span class="sxs-lookup"><span data-stu-id="4dba6-359">`nuget pack` copies output files with extensions `.exe`, `.dll`, `.xml`, `.winmd`, `.json`, and `.pri`.</span></span> <span data-ttu-id="4dba6-360">复制的输出文件取决于 MSBuild 从 `BuiltOutputProjectGroup` 目标提供的内容。</span><span class="sxs-lookup"><span data-stu-id="4dba6-360">The output files that are copied depend on what MSBuild provides from the `BuiltOutputProjectGroup` target.</span></span>

<span data-ttu-id="4dba6-361">在项目文件或命令行中，有两种 MSBuild 属性可用于控制输出程序集的位置：</span><span class="sxs-lookup"><span data-stu-id="4dba6-361">There are two MSBuild  properties that you can use in your project file or command line to control where output assemblies go:</span></span>

- <span data-ttu-id="4dba6-362">`IncludeBuildOutput`：确定包中是否应包括生成输出程序集的布尔值。</span><span class="sxs-lookup"><span data-stu-id="4dba6-362">`IncludeBuildOutput`: A boolean that determines whether the build output assemblies should be included in the package.</span></span>
- <span data-ttu-id="4dba6-363">`BuildOutputTargetFolder`：指定应放置输出程序集的文件夹。</span><span class="sxs-lookup"><span data-stu-id="4dba6-363">`BuildOutputTargetFolder`: Specifies the folder in which the output assemblies should be placed.</span></span> <span data-ttu-id="4dba6-364">输出程序集（和其他输出文件）会复制到各自的框架文件夹中。</span><span class="sxs-lookup"><span data-stu-id="4dba6-364">The output assemblies (and other output files) are copied into their respective framework folders.</span></span>

### <a name="package-references"></a><span data-ttu-id="4dba6-365">包引用</span><span class="sxs-lookup"><span data-stu-id="4dba6-365">Package references</span></span>

<span data-ttu-id="4dba6-366">请参阅[项目文件中的包引用](../consume-packages/package-references-in-project-files.md)</span><span class="sxs-lookup"><span data-stu-id="4dba6-366">See [Package References in Project Files](../consume-packages/package-references-in-project-files.md).</span></span>

### <a name="project-to-project-references"></a><span data-ttu-id="4dba6-367">项目到项目的引用</span><span class="sxs-lookup"><span data-stu-id="4dba6-367">Project to project references</span></span>

<span data-ttu-id="4dba6-368">默认情况下，项目到项目的引用被视为 nuget 包引用，例如：</span><span class="sxs-lookup"><span data-stu-id="4dba6-368">Project to project references are considered by default as nuget package references, for example:</span></span>

```xml
<ProjectReference Include="..\UwpLibrary2\UwpLibrary2.csproj"/>
```

<span data-ttu-id="4dba6-369">也可将以下元数据添加到项目引用：</span><span class="sxs-lookup"><span data-stu-id="4dba6-369">You can also add the following metadata to your project reference:</span></span>

```xml
<IncludeAssets>
<ExcludeAssets>
<PrivateAssets>
```

### <a name="including-content-in-a-package"></a><span data-ttu-id="4dba6-370">在包中添加内容</span><span class="sxs-lookup"><span data-stu-id="4dba6-370">Including content in a package</span></span>

<span data-ttu-id="4dba6-371">若要添加内容，请将额外的元数据添加到现有的 `<Content>` 项。</span><span class="sxs-lookup"><span data-stu-id="4dba6-371">To include content, add extra metadata to the existing `<Content>` item.</span></span> <span data-ttu-id="4dba6-372">默认情况下，类型“Content”的所有内容都包括在包中，除非使用以下条目替代：</span><span class="sxs-lookup"><span data-stu-id="4dba6-372">By default everything of type "Content" gets included in the package unless you override with entries like the following:</span></span>

 ```xml
<Content Include="..\win7-x64\libuv.txt">
  <Pack>false</Pack>
</Content>
 ```

<span data-ttu-id="4dba6-373">默认情况下，所有内容都添加到包中 `content` 和 `contentFiles\any\<target_framework>` 文件夹根目录，并保留相对文件夹结构，除非指定包路径：</span><span class="sxs-lookup"><span data-stu-id="4dba6-373">By default, everything gets added to the root of the `content` and `contentFiles\any\<target_framework>` folder within a package and preserves the relative folder structure, unless you specify a package path:</span></span>

```xml
<Content Include="..\win7-x64\libuv.txt">
  <Pack>true</Pack>
  <PackagePath>content\myfiles\</PackagePath>
</Content>
```

<span data-ttu-id="4dba6-374">如果仅希望将所有内容都复制到特定根文件夹（而不是 `content` 和 `contentFiles`），可使用 MSBuild 属性 `ContentTargetFolders`，其默认值为“content;contentFiles”，但可以设置为任何其他文件夹名称。</span><span class="sxs-lookup"><span data-stu-id="4dba6-374">If you want to copy all your content to only a specific root folder(s) (instead of `content` and `contentFiles` both), you can use the MSBuild property `ContentTargetFolders`, which defaults to "content;contentFiles" but can be set to any other folder names.</span></span> <span data-ttu-id="4dba6-375">请注意，基于 `buildAction`，仅在 `ContentTargetFolders` 中指定“contentFiles”会将文件置于 `contentFiles\any\<target_framework>` 或 `contentFiles\<language>\<target_framework>` 下。</span><span class="sxs-lookup"><span data-stu-id="4dba6-375">Note that just specifying "contentFiles" in `ContentTargetFolders` puts files under `contentFiles\any\<target_framework>` or `contentFiles\<language>\<target_framework>` based on `buildAction`.</span></span>

<span data-ttu-id="4dba6-376">`PackagePath` 可以是一组以分号分隔的目标路径。</span><span class="sxs-lookup"><span data-stu-id="4dba6-376">`PackagePath` can be a semicolon-delimited set of target paths.</span></span> <span data-ttu-id="4dba6-377">指定空的包路径会将文件添加到包的根目录。</span><span class="sxs-lookup"><span data-stu-id="4dba6-377">Specifying an empty package path would add the file to the root of the package.</span></span> <span data-ttu-id="4dba6-378">例如，以下操作会将 `libuv.txt` 添加到 `content\myfiles`、`content\samples` 和包的根目录：</span><span class="sxs-lookup"><span data-stu-id="4dba6-378">For example, the following adds `libuv.txt` to `content\myfiles`, `content\samples`, and the package root:</span></span>

```xml
<Content Include="..\win7-x64\libuv.txt">
  <Pack>true</Pack>
  <PackagePath>content\myfiles;content\sample;;</PackagePath>
</Content>
```

<span data-ttu-id="4dba6-379">另外还有 MSBuild 属性 `$(IncludeContentInPack)`，默认值为 `true`。</span><span class="sxs-lookup"><span data-stu-id="4dba6-379">There is also an MSBuild property `$(IncludeContentInPack)`, which defaults to `true`.</span></span> <span data-ttu-id="4dba6-380">如果在任何项目中将此值设置为 `false`，则该项目的内容不会包括在 nuget 包中。</span><span class="sxs-lookup"><span data-stu-id="4dba6-380">If this is set to `false` on any project, then the content from that project are not included in the nuget package.</span></span>

<span data-ttu-id="4dba6-381">其他可在任何上述项上设置的特定于包的元数据包括 ```<PackageCopyToOutput>``` 和 ```<PackageFlatten>```，后者在输出 nuspec 中的 ```contentFiles``` 条目上设置 ```CopyToOutput``` 和 ```Flatten``` 值。</span><span class="sxs-lookup"><span data-stu-id="4dba6-381">Other pack specific metadata that you can set on any of the above items includes ```<PackageCopyToOutput>``` and ```<PackageFlatten>``` which sets ```CopyToOutput``` and ```Flatten``` values on the ```contentFiles``` entry in the output nuspec.</span></span>

> [!Note]
> <span data-ttu-id="4dba6-382">除了“Content”项，`<Pack>` 和 `<PackagePath>` 元数据还可以在具有 Compile、EmbeddedResource、ApplicationDefinition、Page、Resource、SplashScreen、DesignData、DesignDataWithDesignTimeCreateableTypes、CodeAnalysisDictionary、AndroidAsset、AndroidResource、BundleResource 或 None 生成操作的文件上进行设置。</span><span class="sxs-lookup"><span data-stu-id="4dba6-382">Apart from Content items, the `<Pack>` and `<PackagePath>` metadata can also be set on files with a build action of Compile, EmbeddedResource, ApplicationDefinition, Page, Resource, SplashScreen, DesignData, DesignDataWithDesignTimeCreateableTypes, CodeAnalysisDictionary, AndroidAsset, AndroidResource, BundleResource or None.</span></span>
>
> <span data-ttu-id="4dba6-383">使用通配模式时，对于将包的文件名追加到包路径，包路径必须以文件夹分隔符结尾，否则包路径将被视为包括文件名的完整路径。</span><span class="sxs-lookup"><span data-stu-id="4dba6-383">For pack to append the filename to your package path when using globbing patterns, your package path must end with the folder separator character, otherwise the package path is treated as the full path including the file name.</span></span>

### <a name="includesymbols"></a><span data-ttu-id="4dba6-384">IncludeSymbols</span><span class="sxs-lookup"><span data-stu-id="4dba6-384">IncludeSymbols</span></span>

<span data-ttu-id="4dba6-385">使用 `MSBuild -t:pack -p:IncludeSymbols=true` 时，相应的 `.pdb` 文件将随其他输出文件（`.dll`、`.exe`、`.winmd`、`.xml`、`.json`、`.pri`）一起复制。</span><span class="sxs-lookup"><span data-stu-id="4dba6-385">When using `MSBuild -t:pack -p:IncludeSymbols=true`, the corresponding `.pdb` files are copied along with other output files (`.dll`, `.exe`, `.winmd`, `.xml`, `.json`, `.pri`).</span></span> <span data-ttu-id="4dba6-386">请注意，设置 `IncludeSymbols=true` 会创建常规包和符号包。</span><span class="sxs-lookup"><span data-stu-id="4dba6-386">Note that setting `IncludeSymbols=true` creates a regular package *and* a symbols package.</span></span>

### <a name="includesource"></a><span data-ttu-id="4dba6-387">IncludeSource</span><span class="sxs-lookup"><span data-stu-id="4dba6-387">IncludeSource</span></span>

<span data-ttu-id="4dba6-388">这与 `IncludeSymbols` 相同，但它还会连同 `.pdb` 文件复制源文件。</span><span class="sxs-lookup"><span data-stu-id="4dba6-388">This is the same as `IncludeSymbols`, except that it copies source files along with `.pdb` files as well.</span></span> <span data-ttu-id="4dba6-389">类型为 `Compile` 的所有文件都会复制到 `src\<ProjectName>\`，并保留生成包中的相对路径文件夹结构。</span><span class="sxs-lookup"><span data-stu-id="4dba6-389">All files of type `Compile` are copied over to `src\<ProjectName>\` preserving the relative path folder structure in the resulting package.</span></span> <span data-ttu-id="4dba6-390">对于将 `TreatAsPackageReference` 设置为 `false` 的任何 `ProjectReference` 的源文件也是如此。</span><span class="sxs-lookup"><span data-stu-id="4dba6-390">The same also happens for source files of any `ProjectReference` which has `TreatAsPackageReference` set to `false`.</span></span>

<span data-ttu-id="4dba6-391">如果类型为 Compile 的文件位于项目文件夹外，则它只添加到了 `src\<ProjectName>\`。</span><span class="sxs-lookup"><span data-stu-id="4dba6-391">If a file of type Compile, is outside the project folder, then it's just added to `src\<ProjectName>\`.</span></span>

### <a name="packing-a-license-expression-or-a-license-file"></a><span data-ttu-id="4dba6-392">打包许可证表达式或许可证文件</span><span class="sxs-lookup"><span data-stu-id="4dba6-392">Packing a license expression or a license file</span></span>

<span data-ttu-id="4dba6-393">使用许可证表达式时，请使用 `PackageLicenseExpression` 属性。</span><span class="sxs-lookup"><span data-stu-id="4dba6-393">When using a license expression, use the `PackageLicenseExpression` property.</span></span> <span data-ttu-id="4dba6-394">有关示例，请参阅 [许可证表达式示例](https://github.com/NuGet/Samples/tree/master/PackageLicenseExpressionExample)。</span><span class="sxs-lookup"><span data-stu-id="4dba6-394">For a sample, see [License expression sample](https://github.com/NuGet/Samples/tree/master/PackageLicenseExpressionExample).</span></span>

```xml
<PropertyGroup>
    <PackageLicenseExpression>MIT</PackageLicenseExpression>
</PropertyGroup>
```

<span data-ttu-id="4dba6-395">若要了解有关 NuGet.org 所接受的许可证表达式和许可证的详细信息，请参阅 [许可证元数据](nuspec.md#license)。</span><span class="sxs-lookup"><span data-stu-id="4dba6-395">To learn more about license expressions and licenses that are accepted by NuGet.org, see [license metadata](nuspec.md#license).</span></span>

<span data-ttu-id="4dba6-396">打包许可证文件时，请使用 `PackageLicenseFile` 属性来指定包路径，相对于包的根。</span><span class="sxs-lookup"><span data-stu-id="4dba6-396">When packing a license file, use `PackageLicenseFile` property to specify the package path, relative to the root of the package.</span></span> <span data-ttu-id="4dba6-397">此外，请确保该文件已包含在包中。</span><span class="sxs-lookup"><span data-stu-id="4dba6-397">In addition, make sure that the file is included in the package.</span></span> <span data-ttu-id="4dba6-398">例如：</span><span class="sxs-lookup"><span data-stu-id="4dba6-398">For example:</span></span>

```xml
<PropertyGroup>
    <PackageLicenseFile>LICENSE.txt</PackageLicenseFile>
</PropertyGroup>

<ItemGroup>
    <None Include="licenses\LICENSE.txt" Pack="true" PackagePath=""/>
</ItemGroup>
```

<span data-ttu-id="4dba6-399">有关示例，请参阅 [许可证文件示例](https://github.com/NuGet/Samples/tree/master/PackageLicenseFileExample)。</span><span class="sxs-lookup"><span data-stu-id="4dba6-399">For a sample, see [License file sample](https://github.com/NuGet/Samples/tree/master/PackageLicenseFileExample).</span></span>

> [!NOTE]
> <span data-ttu-id="4dba6-400">`PackageLicenseExpression`一次只能指定、和中的一个 `PackageLicenseFile` `PackageLicenseUrl` 。</span><span class="sxs-lookup"><span data-stu-id="4dba6-400">Only one of `PackageLicenseExpression`, `PackageLicenseFile`, and `PackageLicenseUrl` can be specified at a time.</span></span>

### <a name="packing-a-file-without-an-extension"></a><span data-ttu-id="4dba6-401">打包不带扩展名的文件</span><span class="sxs-lookup"><span data-stu-id="4dba6-401">Packing a file without an extension</span></span>

<span data-ttu-id="4dba6-402">在某些情况下（如打包许可证文件时），可能需要包含不带扩展名的文件。</span><span class="sxs-lookup"><span data-stu-id="4dba6-402">In some scenarios, like when packing a license file, you might want to include a file without an extension.</span></span>
<span data-ttu-id="4dba6-403">由于历史原因，NuGet & MSBuild 将没有扩展的路径视为目录。</span><span class="sxs-lookup"><span data-stu-id="4dba6-403">For historical reasons, NuGet & MSBuild treat paths without an extension as directories.</span></span>

```xml
  <PropertyGroup>
    <TargetFrameworks>netstandard2.0</TargetFrameworks>
    <PackageLicenseFile>LICENSE</PackageLicenseFile>
  </PropertyGroup>

  <ItemGroup>
    <None Include="LICENSE" Pack="true" PackagePath=""/>
  </ItemGroup>  
```

<span data-ttu-id="4dba6-404">[不带扩展的文件示例](https://github.com/NuGet/Samples/blob/master/PackageLicenseFileExtensionlessExample/)。</span><span class="sxs-lookup"><span data-stu-id="4dba6-404">[File without an extension sample](https://github.com/NuGet/Samples/blob/master/PackageLicenseFileExtensionlessExample/).</span></span>
### <a name="istool"></a><span data-ttu-id="4dba6-405">IsTool</span><span class="sxs-lookup"><span data-stu-id="4dba6-405">IsTool</span></span>

<span data-ttu-id="4dba6-406">使用 `MSBuild -t:pack -p:IsTool=true` 时，所有输出文件（如[输出程序集](#output-assemblies)方案中所指定）都被复制到 `tools` 文件夹，而不是 `lib` 文件夹。</span><span class="sxs-lookup"><span data-stu-id="4dba6-406">When using `MSBuild -t:pack -p:IsTool=true`, all output files, as specified in the [Output Assemblies](#output-assemblies) scenario, are copied to the `tools` folder instead of the `lib` folder.</span></span> <span data-ttu-id="4dba6-407">请注意，这不同于 `DotNetCliTool`，后者通过在 `.csproj` 文件中设置 `PackageType` 进行指定。</span><span class="sxs-lookup"><span data-stu-id="4dba6-407">Note that this is different from a `DotNetCliTool` which is specified by setting the `PackageType` in `.csproj` file.</span></span>

### <a name="packing-using-a-nuspec"></a><span data-ttu-id="4dba6-408">使用 .nuspec 打包</span><span class="sxs-lookup"><span data-stu-id="4dba6-408">Packing using a .nuspec</span></span>

<span data-ttu-id="4dba6-409">尽管建议你改为在项目文件中包含通常在文件中的 [所有属性](../reference/msbuild-targets.md#pack-target) `.nuspec` ，但你可以选择使用 `.nuspec` 文件打包项目。</span><span class="sxs-lookup"><span data-stu-id="4dba6-409">Although it is recommended that you [include all the properties](../reference/msbuild-targets.md#pack-target) that are usually in the `.nuspec` file in the project file instead, you can choose to use a `.nuspec` file to pack your project.</span></span> <span data-ttu-id="4dba6-410">对于使用的非 SDK 样式项目 `PackageReference` ，必须导入， `NuGet.Build.Tasks.Pack.targets` 以便可以执行 pack 任务。</span><span class="sxs-lookup"><span data-stu-id="4dba6-410">For a non-SDK-style project that uses `PackageReference`, you must import `NuGet.Build.Tasks.Pack.targets` so that the pack task can be executed.</span></span> <span data-ttu-id="4dba6-411">你仍需要还原项目，然后才能打包 nuspec 文件。</span><span class="sxs-lookup"><span data-stu-id="4dba6-411">You still need to restore the project before you can pack a nuspec file.</span></span> <span data-ttu-id="4dba6-412">默认情况下，SDK 样式项目 (包含包目标。 ) </span><span class="sxs-lookup"><span data-stu-id="4dba6-412">(An SDK-style project includes the pack targets by default.)</span></span>

<span data-ttu-id="4dba6-413">项目文件的目标框架不相关，并且不会在对 nuspec 进行打包时使用。</span><span class="sxs-lookup"><span data-stu-id="4dba6-413">The target framework of the project file is irrelevant and not used when packing a nuspec.</span></span> <span data-ttu-id="4dba6-414">以下三个 MSBuild 属性与使用 `.nuspec` 的打包相关：</span><span class="sxs-lookup"><span data-stu-id="4dba6-414">The following three MSBuild properties are relevant to packing using a `.nuspec`:</span></span>

1. <span data-ttu-id="4dba6-415">`NuspecFile`：用于打包的 `.nuspec` 文件的相对或绝对路径。</span><span class="sxs-lookup"><span data-stu-id="4dba6-415">`NuspecFile`: relative or absolute path to the `.nuspec` file being used for packing.</span></span>
1. <span data-ttu-id="4dba6-416">`NuspecProperties`：键=值对的分号分隔列表。</span><span class="sxs-lookup"><span data-stu-id="4dba6-416">`NuspecProperties`: a semicolon-separated list of key=value pairs.</span></span> <span data-ttu-id="4dba6-417">由于 MSBuild 命令行分析工作的方式，必须指定多个属性，如下所示：`-p:NuspecProperties="key1=value1;key2=value2"`。</span><span class="sxs-lookup"><span data-stu-id="4dba6-417">Due to the way MSBuild command-line parsing works, multiple properties must be specified as follows: `-p:NuspecProperties="key1=value1;key2=value2"`.</span></span>  
1. <span data-ttu-id="4dba6-418">`NuspecBasePath`：`.nuspec` 文件的基路径。</span><span class="sxs-lookup"><span data-stu-id="4dba6-418">`NuspecBasePath`: Base path for the `.nuspec` file.</span></span>

<span data-ttu-id="4dba6-419">如果使用 `dotnet.exe` 打包项目，请使用类似于下面的命令：</span><span class="sxs-lookup"><span data-stu-id="4dba6-419">If using `dotnet.exe` to pack your project, use a command like the following:</span></span>

```dotnetcli
dotnet pack <path to .csproj file> -p:NuspecFile=<path to nuspec file> -p:NuspecProperties=<> -p:NuspecBasePath=<Base path> 
```

<span data-ttu-id="4dba6-420">如果使用 MSBuild 打包项目，请使用类似于下面的命令：</span><span class="sxs-lookup"><span data-stu-id="4dba6-420">If using MSBuild to pack your project, use a command like the following:</span></span>

```cli
msbuild -t:pack <path to .csproj file> -p:NuspecFile=<path to nuspec file> -p:NuspecProperties=<> -p:NuspecBasePath=<Base path> 
```

<span data-ttu-id="4dba6-421">请注意，默认情况下，使用 dotnet.exe 或 msbuild 打包 nuspec 也会导致生成项目。</span><span class="sxs-lookup"><span data-stu-id="4dba6-421">Please note that packing a nuspec using dotnet.exe or msbuild also leads to building the project by default.</span></span> <span data-ttu-id="4dba6-422">可以通过将属性传递给 dotnet.exe 来避免这种情况，这与项目文件中的 ```--no-build``` 设置 ```<NoBuild>true</NoBuild> ``` 以及项目文件中的设置等效 ```<IncludeBuildOutput>false</IncludeBuildOutput> ``` 。</span><span class="sxs-lookup"><span data-stu-id="4dba6-422">This can be avoided by passing ```--no-build``` property to dotnet.exe, which is the equivalent of setting ```<NoBuild>true</NoBuild> ``` in your project file, along with setting ```<IncludeBuildOutput>false</IncludeBuildOutput> ``` in the project file.</span></span>

<span data-ttu-id="4dba6-423">用于打包 nuspec 文件的 *.csproj* 文件的示例如下：</span><span class="sxs-lookup"><span data-stu-id="4dba6-423">An example of a *.csproj* file to pack a nuspec file is:</span></span>

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

### <a name="advanced-extension-points-to-create-customized-package"></a><span data-ttu-id="4dba6-424">用于创建自定义包的高级扩展点</span><span class="sxs-lookup"><span data-stu-id="4dba6-424">Advanced extension points to create customized package</span></span>

<span data-ttu-id="4dba6-425">`pack`目标提供两个扩展点，这些点在内部特定于目标框架的生成中运行。</span><span class="sxs-lookup"><span data-stu-id="4dba6-425">The `pack` target provides two extension points that run in the inner, target framework specific build.</span></span> <span data-ttu-id="4dba6-426">扩展点支持包括特定于目标框架的内容和程序集到包中：</span><span class="sxs-lookup"><span data-stu-id="4dba6-426">The extension points support including target framework specific content and assemblies into a package:</span></span>

- <span data-ttu-id="4dba6-427">`TargetsForTfmSpecificBuildOutput` 目标：用于文件夹内的文件 `lib` 或使用指定的文件夹 `BuildOutputTargetFolder` 。</span><span class="sxs-lookup"><span data-stu-id="4dba6-427">`TargetsForTfmSpecificBuildOutput` target: Use for files inside the `lib` folder or a folder specified using `BuildOutputTargetFolder`.</span></span>
- <span data-ttu-id="4dba6-428">`TargetsForTfmSpecificContentInPackage` 目标：用于之外的文件 `BuildOutputTargetFolder` 。</span><span class="sxs-lookup"><span data-stu-id="4dba6-428">`TargetsForTfmSpecificContentInPackage` target: Use for files outside the `BuildOutputTargetFolder`.</span></span>

#### <a name="targetsfortfmspecificbuildoutput"></a><span data-ttu-id="4dba6-429">TargetsForTfmSpecificBuildOutput</span><span class="sxs-lookup"><span data-stu-id="4dba6-429">TargetsForTfmSpecificBuildOutput</span></span>

<span data-ttu-id="4dba6-430">编写自定义目标并将其指定为属性的值 `$(TargetsForTfmSpecificBuildOutput)` 。</span><span class="sxs-lookup"><span data-stu-id="4dba6-430">Write a custom target and specify it as the value of the `$(TargetsForTfmSpecificBuildOutput)` property.</span></span> <span data-ttu-id="4dba6-431">对于任何需要在 `BuildOutputTargetFolder` 默认情况下进入 (lib 的文件) ，目标应将这些文件写入 ItemGroup， `BuildOutputInPackage` 并设置以下两个元数据值：</span><span class="sxs-lookup"><span data-stu-id="4dba6-431">For any files that need to go into the `BuildOutputTargetFolder` (lib by default), the target should write those files into the ItemGroup `BuildOutputInPackage` and set the following two metadata values:</span></span>

- <span data-ttu-id="4dba6-432">`FinalOutputPath`：文件的绝对路径;如果未提供，则标识用于计算源路径。</span><span class="sxs-lookup"><span data-stu-id="4dba6-432">`FinalOutputPath`: The absolute path of the file; if not provided, the Identity is used to evaluate source path.</span></span>
- <span data-ttu-id="4dba6-433">`TargetPath`：当文件需要进入中的子文件夹时， (可选) 设置 `lib\<TargetFramework>` ，如位于其各自区域性文件夹下的附属程序集。</span><span class="sxs-lookup"><span data-stu-id="4dba6-433">`TargetPath`:  (Optional) Set when the file needs to go into a subfolder within `lib\<TargetFramework>` , like satellite assemblies that go under their respective culture folders.</span></span> <span data-ttu-id="4dba6-434">默认为文件的名称。</span><span class="sxs-lookup"><span data-stu-id="4dba6-434">Defaults to the name of the file.</span></span>

<span data-ttu-id="4dba6-435">示例：</span><span class="sxs-lookup"><span data-stu-id="4dba6-435">Example:</span></span>

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

#### <a name="targetsfortfmspecificcontentinpackage"></a><span data-ttu-id="4dba6-436">TargetsForTfmSpecificContentInPackage</span><span class="sxs-lookup"><span data-stu-id="4dba6-436">TargetsForTfmSpecificContentInPackage</span></span>

<span data-ttu-id="4dba6-437">编写自定义目标并将其指定为属性的值 `$(TargetsForTfmSpecificContentInPackage)` 。</span><span class="sxs-lookup"><span data-stu-id="4dba6-437">Write a custom target and specify it as the value of the `$(TargetsForTfmSpecificContentInPackage)` property.</span></span> <span data-ttu-id="4dba6-438">对于要包含在包中的任何文件，目标应将这些文件写入 ItemGroup `TfmSpecificPackageFile` ，并设置以下可选的元数据：</span><span class="sxs-lookup"><span data-stu-id="4dba6-438">For any files to include in the package, the target should write those files into the ItemGroup `TfmSpecificPackageFile` and set the following optional metadata:</span></span>

- <span data-ttu-id="4dba6-439">`PackagePath`：应在包中输出文件的路径。</span><span class="sxs-lookup"><span data-stu-id="4dba6-439">`PackagePath`: Path where the file should be output in the package.</span></span> <span data-ttu-id="4dba6-440">如果将多个文件添加到同一个包路径，NuGet 将发出警告。</span><span class="sxs-lookup"><span data-stu-id="4dba6-440">NuGet issues a warning if more than one file is added to the same package path.</span></span>
- <span data-ttu-id="4dba6-441">`BuildAction`：要分配给文件的生成操作，只有当包路径在文件夹中时才是必需的 `contentFiles` 。</span><span class="sxs-lookup"><span data-stu-id="4dba6-441">`BuildAction`: The build action to assign to the file, required only if the package path is in the `contentFiles` folder.</span></span> <span data-ttu-id="4dba6-442">默认值为 "None"。</span><span class="sxs-lookup"><span data-stu-id="4dba6-442">Defaults to "None".</span></span>

<span data-ttu-id="4dba6-443">示例：</span><span class="sxs-lookup"><span data-stu-id="4dba6-443">An example:</span></span>
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

## <a name="restore-target"></a><span data-ttu-id="4dba6-444">还原目标</span><span class="sxs-lookup"><span data-stu-id="4dba6-444">restore target</span></span>

<span data-ttu-id="4dba6-445">`MSBuild -t:restore`（`nuget restore` 和 `dotnet restore` 与 .NET Core 项目一起使用）会还原项目文件中引用的包，如下所示：</span><span class="sxs-lookup"><span data-stu-id="4dba6-445">`MSBuild -t:restore` (which `nuget restore` and `dotnet restore` use with .NET Core projects), restores packages referenced in the project file as follows:</span></span>

1. <span data-ttu-id="4dba6-446">读取所有项目到项目的引用</span><span class="sxs-lookup"><span data-stu-id="4dba6-446">Read all project to project references</span></span>
1. <span data-ttu-id="4dba6-447">读取项目属性以查找中间文件夹和目标框架</span><span class="sxs-lookup"><span data-stu-id="4dba6-447">Read the project properties to find the intermediate folder and target frameworks</span></span>
1. <span data-ttu-id="4dba6-448">将 MSBuild 数据传递到 NuGet.Build.Tasks.dll</span><span class="sxs-lookup"><span data-stu-id="4dba6-448">Pass MSBuild data to NuGet.Build.Tasks.dll</span></span>
1. <span data-ttu-id="4dba6-449">运行还原</span><span class="sxs-lookup"><span data-stu-id="4dba6-449">Run restore</span></span>
1. <span data-ttu-id="4dba6-450">下载包</span><span class="sxs-lookup"><span data-stu-id="4dba6-450">Download packages</span></span>
1. <span data-ttu-id="4dba6-451">编写资产文件、目标和属性</span><span class="sxs-lookup"><span data-stu-id="4dba6-451">Write assets file, targets, and props</span></span>

<span data-ttu-id="4dba6-452">`restore`目标适用于使用 PackageReference 格式的项目。</span><span class="sxs-lookup"><span data-stu-id="4dba6-452">The `restore` target works for projects using the PackageReference format.</span></span>
<span data-ttu-id="4dba6-453">`MSBuild 16.5+` 还具有对格式的 [选择支持](#restoring-packagereference-and-packagesconfig-with-msbuild) `packages.config` 。</span><span class="sxs-lookup"><span data-stu-id="4dba6-453">`MSBuild 16.5+` also has [opt-in support](#restoring-packagereference-and-packagesconfig-with-msbuild) for the `packages.config` format.</span></span>

> [!NOTE]
> <span data-ttu-id="4dba6-454">`restore`目标[不应](#restoring-and-building-with-one-msbuild-command)与目标组合运行 `build` 。</span><span class="sxs-lookup"><span data-stu-id="4dba6-454">The `restore` target [should not be run](#restoring-and-building-with-one-msbuild-command) in combination with the `build` target.</span></span>

### <a name="restore-properties"></a><span data-ttu-id="4dba6-455">还原属性</span><span class="sxs-lookup"><span data-stu-id="4dba6-455">Restore properties</span></span>

<span data-ttu-id="4dba6-456">其他的还原设置可能来自项目文件中的 MSBuild 属性。</span><span class="sxs-lookup"><span data-stu-id="4dba6-456">Additional restore settings may come from MSBuild properties in the project file.</span></span> <span data-ttu-id="4dba6-457">还可以从命令行使用 `-p:` 开关设置值（请参阅以下示例）。</span><span class="sxs-lookup"><span data-stu-id="4dba6-457">Values can also be set from the command line using the `-p:` switch (see Examples below).</span></span>

| <span data-ttu-id="4dba6-458">properties</span><span class="sxs-lookup"><span data-stu-id="4dba6-458">Property</span></span> | <span data-ttu-id="4dba6-459">说明</span><span class="sxs-lookup"><span data-stu-id="4dba6-459">Description</span></span> |
|--------|--------|
| <span data-ttu-id="4dba6-460">RestoreSources</span><span class="sxs-lookup"><span data-stu-id="4dba6-460">RestoreSources</span></span> | <span data-ttu-id="4dba6-461">以分号分隔的包源列表。</span><span class="sxs-lookup"><span data-stu-id="4dba6-461">Semicolon-delimited list of package sources.</span></span> |
| <span data-ttu-id="4dba6-462">RestorePackagesPath</span><span class="sxs-lookup"><span data-stu-id="4dba6-462">RestorePackagesPath</span></span> | <span data-ttu-id="4dba6-463">用户包文件夹路径。</span><span class="sxs-lookup"><span data-stu-id="4dba6-463">User packages folder path.</span></span> |
| <span data-ttu-id="4dba6-464">RestoreDisableParallel</span><span class="sxs-lookup"><span data-stu-id="4dba6-464">RestoreDisableParallel</span></span> | <span data-ttu-id="4dba6-465">将下载限制为一次一个。</span><span class="sxs-lookup"><span data-stu-id="4dba6-465">Limit downloads to one at a time.</span></span> |
| <span data-ttu-id="4dba6-466">RestoreConfigFile</span><span class="sxs-lookup"><span data-stu-id="4dba6-466">RestoreConfigFile</span></span> | <span data-ttu-id="4dba6-467">要应用的 `Nuget.Config` 文件的路径。</span><span class="sxs-lookup"><span data-stu-id="4dba6-467">Path to a `Nuget.Config` file to apply.</span></span> |
| <span data-ttu-id="4dba6-468">RestoreNoCache</span><span class="sxs-lookup"><span data-stu-id="4dba6-468">RestoreNoCache</span></span> | <span data-ttu-id="4dba6-469">如果为 true，则避免使用缓存的包。</span><span class="sxs-lookup"><span data-stu-id="4dba6-469">If true, avoids using cached packages.</span></span> <span data-ttu-id="4dba6-470">请参阅 [管理全局包和缓存文件夹](../consume-packages/managing-the-global-packages-and-cache-folders.md)。</span><span class="sxs-lookup"><span data-stu-id="4dba6-470">See [Managing the global packages and cache folders](../consume-packages/managing-the-global-packages-and-cache-folders.md).</span></span> |
| <span data-ttu-id="4dba6-471">RestoreIgnoreFailedSources</span><span class="sxs-lookup"><span data-stu-id="4dba6-471">RestoreIgnoreFailedSources</span></span> | <span data-ttu-id="4dba6-472">如果为“true”，则忽略失败或丢失的包源。</span><span class="sxs-lookup"><span data-stu-id="4dba6-472">If true, ignores failing or missing package sources.</span></span> |
| <span data-ttu-id="4dba6-473">RestoreFallbackFolders</span><span class="sxs-lookup"><span data-stu-id="4dba6-473">RestoreFallbackFolders</span></span> | <span data-ttu-id="4dba6-474">后备文件夹，其使用方式与使用 "用户包" 文件夹的方式相同。</span><span class="sxs-lookup"><span data-stu-id="4dba6-474">Fallback folders, used in the same way the user packages folder is used.</span></span> |
| <span data-ttu-id="4dba6-475">RestoreAdditionalProjectSources</span><span class="sxs-lookup"><span data-stu-id="4dba6-475">RestoreAdditionalProjectSources</span></span> | <span data-ttu-id="4dba6-476">要在还原期间使用的其他源。</span><span class="sxs-lookup"><span data-stu-id="4dba6-476">Additional sources to use during restore.</span></span> |
| <span data-ttu-id="4dba6-477">RestoreAdditionalProjectFallbackFolders</span><span class="sxs-lookup"><span data-stu-id="4dba6-477">RestoreAdditionalProjectFallbackFolders</span></span> | <span data-ttu-id="4dba6-478">要在还原期间使用的其他回退文件夹。</span><span class="sxs-lookup"><span data-stu-id="4dba6-478">Additional fallback folders to use during restore.</span></span> |
| <span data-ttu-id="4dba6-479">RestoreAdditionalProjectFallbackFoldersExcludes</span><span class="sxs-lookup"><span data-stu-id="4dba6-479">RestoreAdditionalProjectFallbackFoldersExcludes</span></span> | <span data-ttu-id="4dba6-480">排除其中指定的回退文件夹 `RestoreAdditionalProjectFallbackFolders`</span><span class="sxs-lookup"><span data-stu-id="4dba6-480">Excludes fallback folders specified in `RestoreAdditionalProjectFallbackFolders`</span></span> |
| <span data-ttu-id="4dba6-481">RestoreTaskAssemblyFile</span><span class="sxs-lookup"><span data-stu-id="4dba6-481">RestoreTaskAssemblyFile</span></span> | <span data-ttu-id="4dba6-482">`NuGet.Build.Tasks.dll` 的路径。</span><span class="sxs-lookup"><span data-stu-id="4dba6-482">Path to `NuGet.Build.Tasks.dll`.</span></span> |
| <span data-ttu-id="4dba6-483">RestoreGraphProjectInput</span><span class="sxs-lookup"><span data-stu-id="4dba6-483">RestoreGraphProjectInput</span></span> | <span data-ttu-id="4dba6-484">要还原的以分号分隔的项目列表，其中应包含绝对路径。</span><span class="sxs-lookup"><span data-stu-id="4dba6-484">Semicolon-delimited list of projects to restore, which should contain absolute paths.</span></span> |
| <span data-ttu-id="4dba6-485">RestoreUseSkipNonexistentTargets</span><span class="sxs-lookup"><span data-stu-id="4dba6-485">RestoreUseSkipNonexistentTargets</span></span>  | <span data-ttu-id="4dba6-486">通过 MSBuild 收集项目后，它将确定是否使用优化来收集这些项目 `SkipNonexistentTargets` 。</span><span class="sxs-lookup"><span data-stu-id="4dba6-486">When the projects are collected via MSBuild it determines whether they are collected using the `SkipNonexistentTargets` optimization.</span></span> <span data-ttu-id="4dba6-487">如果未设置，则默认为 `true` 。</span><span class="sxs-lookup"><span data-stu-id="4dba6-487">When not set, defaults to `true`.</span></span> <span data-ttu-id="4dba6-488">如果无法导入项目的目标，则结果是一个故障快速的行为。</span><span class="sxs-lookup"><span data-stu-id="4dba6-488">The consequence is a fail-fast behavior when a project's targets cannot be imported.</span></span> |
| <span data-ttu-id="4dba6-489">MSBuildProjectExtensionsPath</span><span class="sxs-lookup"><span data-stu-id="4dba6-489">MSBuildProjectExtensionsPath</span></span> | <span data-ttu-id="4dba6-490">Output 文件夹，默认为 `BaseIntermediateOutputPath` 和 `obj` 文件夹。</span><span class="sxs-lookup"><span data-stu-id="4dba6-490">Output folder, defaulting to `BaseIntermediateOutputPath` and the `obj` folder.</span></span> |
| <span data-ttu-id="4dba6-491">RestoreForce</span><span class="sxs-lookup"><span data-stu-id="4dba6-491">RestoreForce</span></span> | <span data-ttu-id="4dba6-492">在基于 PackageReference 的项目中，将强制解析所有依赖项，即使上次还原已成功。</span><span class="sxs-lookup"><span data-stu-id="4dba6-492">In PackageReference based projects, forces all dependencies to be resolved even if the last restore was successful.</span></span> <span data-ttu-id="4dba6-493">指定此标志与删除 `project.assets.json` 文件类似。</span><span class="sxs-lookup"><span data-stu-id="4dba6-493">Specifying this flag is similar to deleting the `project.assets.json` file.</span></span> <span data-ttu-id="4dba6-494">这不会绕过 http 缓存。</span><span class="sxs-lookup"><span data-stu-id="4dba6-494">This does not bypass the http-cache.</span></span> |
| <span data-ttu-id="4dba6-495">RestorePackagesWithLockFile</span><span class="sxs-lookup"><span data-stu-id="4dba6-495">RestorePackagesWithLockFile</span></span> | <span data-ttu-id="4dba6-496">选择使用锁定文件。</span><span class="sxs-lookup"><span data-stu-id="4dba6-496">Opts into the usage of a lock file.</span></span> |
| <span data-ttu-id="4dba6-497">RestoreLockedMode</span><span class="sxs-lookup"><span data-stu-id="4dba6-497">RestoreLockedMode</span></span> | <span data-ttu-id="4dba6-498">在锁定模式下运行还原。</span><span class="sxs-lookup"><span data-stu-id="4dba6-498">Run restore in locked mode.</span></span> <span data-ttu-id="4dba6-499">这意味着，还原将不会重新评估依赖关系。</span><span class="sxs-lookup"><span data-stu-id="4dba6-499">This means that restore will not reevaluate the dependencies.</span></span> |
| <span data-ttu-id="4dba6-500">NuGetLockFilePath</span><span class="sxs-lookup"><span data-stu-id="4dba6-500">NuGetLockFilePath</span></span> | <span data-ttu-id="4dba6-501">锁定文件的自定义位置。</span><span class="sxs-lookup"><span data-stu-id="4dba6-501">A custom location for the lock file.</span></span> <span data-ttu-id="4dba6-502">默认位置为项目旁边，名为 `packages.lock.json` 。</span><span class="sxs-lookup"><span data-stu-id="4dba6-502">The default location is next to the project and is named `packages.lock.json`.</span></span> |
| <span data-ttu-id="4dba6-503">RestoreForceEvaluate</span><span class="sxs-lookup"><span data-stu-id="4dba6-503">RestoreForceEvaluate</span></span> | <span data-ttu-id="4dba6-504">强制执行还原，重新计算依赖项并更新锁定文件，而不会出现任何警告。</span><span class="sxs-lookup"><span data-stu-id="4dba6-504">Forces restore to recompute the dependencies and update the lock file without any warning.</span></span> |
| <span data-ttu-id="4dba6-505">RestorePackagesConfig</span><span class="sxs-lookup"><span data-stu-id="4dba6-505">RestorePackagesConfig</span></span> | <span data-ttu-id="4dba6-506">一种选择使用开关，用 packages.config 还原项目。仅支持 `MSBuild -t:restore` 。</span><span class="sxs-lookup"><span data-stu-id="4dba6-506">An opt-in switch, that restores projects with packages.config. Support with `MSBuild -t:restore` only.</span></span> |
| <span data-ttu-id="4dba6-507">RestoreUseStaticGraphEvaluation</span><span class="sxs-lookup"><span data-stu-id="4dba6-507">RestoreUseStaticGraphEvaluation</span></span> | <span data-ttu-id="4dba6-508">选择使用静态图形 MSBuild 计算，而不是标准计算。</span><span class="sxs-lookup"><span data-stu-id="4dba6-508">An opt-in switch to use static graph MSBuild evaluation instead of the standard evaluation.</span></span> <span data-ttu-id="4dba6-509">静态图形评估是一项试验性功能，它对于大型存储库和解决方案的速度显著提高。</span><span class="sxs-lookup"><span data-stu-id="4dba6-509">Static graph evaluation is an experimental feature that's significantly faster for large repos and solutions.</span></span> |

#### <a name="examples"></a><span data-ttu-id="4dba6-510">示例</span><span class="sxs-lookup"><span data-stu-id="4dba6-510">Examples</span></span>

<span data-ttu-id="4dba6-511">命令行：</span><span class="sxs-lookup"><span data-stu-id="4dba6-511">Command line:</span></span>

```cli
msbuild -t:restore -p:RestoreConfigFile=<path>
```

<span data-ttu-id="4dba6-512">项目文件：</span><span class="sxs-lookup"><span data-stu-id="4dba6-512">Project file:</span></span>

```xml
<PropertyGroup>
    <RestoreIgnoreFailedSource>true</RestoreIgnoreFailedSource>
</PropertyGroup>
```

### <a name="restore-outputs"></a><span data-ttu-id="4dba6-513">还原输出</span><span class="sxs-lookup"><span data-stu-id="4dba6-513">Restore outputs</span></span>

<span data-ttu-id="4dba6-514">还原会在生成 `obj` 文件夹中创建以下文件：</span><span class="sxs-lookup"><span data-stu-id="4dba6-514">Restore creates the following files in the build `obj` folder:</span></span>

| <span data-ttu-id="4dba6-515">文件</span><span class="sxs-lookup"><span data-stu-id="4dba6-515">File</span></span> | <span data-ttu-id="4dba6-516">说明</span><span class="sxs-lookup"><span data-stu-id="4dba6-516">Description</span></span> |
|--------|--------|
| `project.assets.json` | <span data-ttu-id="4dba6-517">包含所有包引用的依赖项关系图。</span><span class="sxs-lookup"><span data-stu-id="4dba6-517">Contains the dependency graph of all package references.</span></span> |
| `{projectName}.projectFileExtension.nuget.g.props` | <span data-ttu-id="4dba6-518">包中包含的对 MSBuild 属性的引用</span><span class="sxs-lookup"><span data-stu-id="4dba6-518">References to MSBuild props contained in packages</span></span> |
| `{projectName}.projectFileExtension.nuget.g.targets` | <span data-ttu-id="4dba6-519">包中包含的对 MSBuild 目标的引用</span><span class="sxs-lookup"><span data-stu-id="4dba6-519">References to MSBuild targets contained in packages</span></span> |

### <a name="restoring-and-building-with-one-msbuild-command"></a><span data-ttu-id="4dba6-520">通过一个 MSBuild 命令进行还原和生成</span><span class="sxs-lookup"><span data-stu-id="4dba6-520">Restoring and building with one MSBuild command</span></span>

<span data-ttu-id="4dba6-521">由于 NuGet 可以还原引入 MSBuild 目标和属性的包，因此，还原和生成评估将以不同的全局属性运行。</span><span class="sxs-lookup"><span data-stu-id="4dba6-521">Due to the fact that NuGet can restore packages that bring down MSBuild targets and props, the restore and build evaluations are run with different global properties.</span></span>
<span data-ttu-id="4dba6-522">这意味着，以下操作将具有不可预测且通常不正确的行为。</span><span class="sxs-lookup"><span data-stu-id="4dba6-522">This means that the following will have an unpredictable and often incorrect behavior.</span></span>

```cli
msbuild -t:restore,build
```

 <span data-ttu-id="4dba6-523">相反，推荐的方法是：</span><span class="sxs-lookup"><span data-stu-id="4dba6-523">Instead the recommended approach is:</span></span>

```cli
msbuild -t:build -restore
```

<span data-ttu-id="4dba6-524">相同的逻辑也适用于类似于的其他目标 `build` 。</span><span class="sxs-lookup"><span data-stu-id="4dba6-524">The same logic applies to other targets similar to `build`.</span></span>

### <a name="restoring-packagereference-and-packagesconfig-with-msbuild"></a><span data-ttu-id="4dba6-525">通过 MSBuild 还原 PackageReference 和 packages.config</span><span class="sxs-lookup"><span data-stu-id="4dba6-525">Restoring PackageReference and packages.config with MSBuild</span></span>

<span data-ttu-id="4dba6-526">对于 MSBuild 16.5 +，还支持 packages.config `msbuild -t:restore` 。</span><span class="sxs-lookup"><span data-stu-id="4dba6-526">With MSBuild 16.5+, packages.config are also supported for `msbuild -t:restore`.</span></span>

```cli
msbuild -t:restore -p:RestorePackagesConfig=true
```

> [!NOTE]
> <span data-ttu-id="4dba6-527">`packages.config` restore 仅适用于 `MSBuild 16.5+` ，而不适用于 `dotnet.exe`</span><span class="sxs-lookup"><span data-stu-id="4dba6-527">`packages.config` restore is only available with `MSBuild 16.5+`, and not with `dotnet.exe`</span></span>

### <a name="restoring-with-msbuild-static-graph-evaluation"></a><span data-ttu-id="4dba6-528">通过 MSBuild 静态图形计算进行还原</span><span class="sxs-lookup"><span data-stu-id="4dba6-528">Restoring with MSBuild static graph evaluation</span></span>

> [!NOTE]
> <span data-ttu-id="4dba6-529">使用 MSBuild 16.6 +，NuGet 添加了一项试验性功能，可用于从命令行使用静态图形计算，从而大幅缩短大型存储库的还原时间。</span><span class="sxs-lookup"><span data-stu-id="4dba6-529">With MSBuild 16.6+, NuGet has added an experimental feature to use static graph evaluation from the command line that significantly improves the restore time for large repositories.</span></span>

```cli
msbuild -t:restore -p:RestoreUseStaticGraphEvaluation=true
```

<span data-ttu-id="4dba6-530">也可以通过设置属性中的属性来启用它。</span><span class="sxs-lookup"><span data-stu-id="4dba6-530">Alternatively you can enable it by setting the property in a Directory.Build.Props.</span></span>

```xml
<Project>
  <PropertyGroup>
    <RestoreUseStaticGraphEvaluation>true</RestoreUseStaticGraphEvaluation>
  </PropertyGroup>
</Project>
```

> [!NOTE]
> <span data-ttu-id="4dba6-531">从 Visual Studio 2019. x 和 NuGet 1.x 中，此功能被视为实验性并选择加入。</span><span class="sxs-lookup"><span data-stu-id="4dba6-531">As of Visual Studio 2019.x and NuGet 5.x, this feature is considered experimental and opt-in.</span></span> <span data-ttu-id="4dba6-532">有关默认情况下何时启用此功能的详细信息，请遵循 [NuGet/Home # 9803](https://github.com/NuGet/Home/issues/9803) 。</span><span class="sxs-lookup"><span data-stu-id="4dba6-532">Follow [NuGet/Home#9803](https://github.com/NuGet/Home/issues/9803) for details on when this feature will be enabled by default.</span></span>

<span data-ttu-id="4dba6-533">静态图形还原更改还原的 msbuild 部分、项目读取和评估，但不更改还原算法！</span><span class="sxs-lookup"><span data-stu-id="4dba6-533">Static graph restore changes the msbuild part of restore, the project reading and evaluation, but not the restore algorithm!</span></span> <span data-ttu-id="4dba6-534">所有 NuGet 工具 ( # A0、MSBuild.exe、dotnet.exe 和 Visual Studio) 中的还原算法都是相同的。</span><span class="sxs-lookup"><span data-stu-id="4dba6-534">The restore algorithm is the same across all NuGet tools (NuGet.exe, MSBuild.exe, dotnet.exe and Visual Studio).</span></span>

<span data-ttu-id="4dba6-535">在极少数情况下，静态图形还原的行为可能与当前还原不同，并且某些声明的 PackageReferences 或 Projectreference 可能已丢失。</span><span class="sxs-lookup"><span data-stu-id="4dba6-535">In very few scenarios, static graph restore may behave differently from current restore and certain declared PackageReferences or ProjectReferences might be missing.</span></span>

<span data-ttu-id="4dba6-536">若要轻松地在迁移到静态图形时进行一次检查，请考虑运行：</span><span class="sxs-lookup"><span data-stu-id="4dba6-536">To ease your mind, as a one time check, when migrating to static graph restore, consider running:</span></span>

```cli
msbuild.exe -t:restore -p:RestoreUseStaticGraphEvaluation
msbuild.exe -t:restore
```

<span data-ttu-id="4dba6-537">NuGet *不* 应报告任何更改。</span><span class="sxs-lookup"><span data-stu-id="4dba6-537">NuGet should *not* report any changes.</span></span> <span data-ttu-id="4dba6-538">如果看不到差异，请在 [NuGet/Home](https://github.com/nuget/home/issues/new)上发布问题。</span><span class="sxs-lookup"><span data-stu-id="4dba6-538">If you do see a discrepancy, please file an issue at [NuGet/Home](https://github.com/nuget/home/issues/new).</span></span>

### <a name="replacing-one-library-from-a-restore-graph"></a><span data-ttu-id="4dba6-539">从还原图中替换一个库</span><span class="sxs-lookup"><span data-stu-id="4dba6-539">Replacing one library from a restore graph</span></span>

<span data-ttu-id="4dba6-540">如果还原引入了错误的程序集，可以排除包默认选项，并将其替换为自己的选项。</span><span class="sxs-lookup"><span data-stu-id="4dba6-540">If a restore is bringing the wrong assembly, it's possible to exclude that packages default choice, and replace it with your own choice.</span></span> <span data-ttu-id="4dba6-541">首先使用顶级 `PackageReference`，排除所有资产：</span><span class="sxs-lookup"><span data-stu-id="4dba6-541">First with a top level `PackageReference`, exclude all assets:</span></span>

```xml
<PackageReference Include="Newtonsoft.Json" Version="9.0.1">
  <ExcludeAssets>All</ExcludeAssets>
</PackageReference>
```

<span data-ttu-id="4dba6-542">接下来，将自己的引用添加到适当的 DLL 本地副本：</span><span class="sxs-lookup"><span data-stu-id="4dba6-542">Next, add your own reference to the appropriate local copy of the DLL:</span></span>

```xml
<Reference Include="Newtonsoft.Json.dll" />
```
