---
title: 适用于 NuGet 的.nuspec 文件引用
description: .nuspec 文件包含生成包时使用的，并向包使用者提供信息的包元数据。
author: karann-msft
ms.author: karann
ms.date: 05/24/2019
ms.topic: reference
ms.reviewer: anangaur
ms.openlocfilehash: fd6ecab05a392a2a0b4ddf1ac15eb108f2653703
ms.sourcegitcommit: 0dea3b153ef823230a9d5f38351b7cef057cb299
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/12/2019
ms.locfileid: "67842403"
---
# <a name="nuspec-reference"></a><span data-ttu-id="d9b93-103">.nuspec 引用</span><span class="sxs-lookup"><span data-stu-id="d9b93-103">.nuspec reference</span></span>

<span data-ttu-id="d9b93-104">`.nuspec` 文件是包含包元数据的 XML 清单。</span><span class="sxs-lookup"><span data-stu-id="d9b93-104">A `.nuspec` file is an XML manifest that contains package metadata.</span></span> <span data-ttu-id="d9b93-105">此清单同时用于生成包以及为使用者提供信息。</span><span class="sxs-lookup"><span data-stu-id="d9b93-105">This manifest is used both to build the package and to provide information to consumers.</span></span> <span data-ttu-id="d9b93-106">清单始终包含在包中。</span><span class="sxs-lookup"><span data-stu-id="d9b93-106">The manifest is always included in a package.</span></span>

<span data-ttu-id="d9b93-107">本主题内容：</span><span class="sxs-lookup"><span data-stu-id="d9b93-107">In this topic:</span></span>

- [<span data-ttu-id="d9b93-108">常规形式和架构</span><span class="sxs-lookup"><span data-stu-id="d9b93-108">General form and schema</span></span>](#general-form-and-schema)
- <span data-ttu-id="d9b93-109">[替换令牌](#replacement-tokens)（用于 Visual Studio 项目时）</span><span class="sxs-lookup"><span data-stu-id="d9b93-109">[Replacement tokens](#replacement-tokens) (when used with a Visual Studio project)</span></span>
- [<span data-ttu-id="d9b93-110">依赖项</span><span class="sxs-lookup"><span data-stu-id="d9b93-110">Dependencies</span></span>](#dependencies)
- [<span data-ttu-id="d9b93-111">显式程序集引用</span><span class="sxs-lookup"><span data-stu-id="d9b93-111">Explicit assembly references</span></span>](#explicit-assembly-references)
- [<span data-ttu-id="d9b93-112">Framework 程序集引用</span><span class="sxs-lookup"><span data-stu-id="d9b93-112">Framework assembly references</span></span>](#framework-assembly-references)
- [<span data-ttu-id="d9b93-113">包括程序集文件</span><span class="sxs-lookup"><span data-stu-id="d9b93-113">Including assembly files</span></span>](#including-assembly-files)
- [<span data-ttu-id="d9b93-114">包括内容文件</span><span class="sxs-lookup"><span data-stu-id="d9b93-114">Including content files</span></span>](#including-content-files)
- [<span data-ttu-id="d9b93-115">示例 nuspec 文件</span><span class="sxs-lookup"><span data-stu-id="d9b93-115">Example nuspec files</span></span>](#example-nuspec-files)

## <a name="project-type-compatibility"></a><span data-ttu-id="d9b93-116">项目类型兼容性</span><span class="sxs-lookup"><span data-stu-id="d9b93-116">Project type compatibility</span></span>

- <span data-ttu-id="d9b93-117">使用`.nuspec`与`nuget.exe pack`非 SDK 样式项目使用`packages.config`。</span><span class="sxs-lookup"><span data-stu-id="d9b93-117">Use `.nuspec` with `nuget.exe pack` for non-SDK-style projects that use `packages.config`.</span></span>

- <span data-ttu-id="d9b93-118">一个`.nuspec`创建的包不需要文件[SDK 样式项目](../resources/check-project-format.md)(.NET Core 和.NET Standard 项目使用的通常[SDK 属性](/dotnet/core/tools/csproj#additions))。</span><span class="sxs-lookup"><span data-stu-id="d9b93-118">A `.nuspec` file is not required to create packages for [SDK-style projects](../resources/check-project-format.md) (typically .NET Core and .NET Standard projects that use the [SDK attribute](/dotnet/core/tools/csproj#additions)).</span></span> <span data-ttu-id="d9b93-119">(请注意，`.nuspec`创建包时生成。)</span><span class="sxs-lookup"><span data-stu-id="d9b93-119">(Note that a `.nuspec` is generated when you create the package.)</span></span>

   <span data-ttu-id="d9b93-120">如果要创建包使用`dotnet.exe pack`或`msbuild pack target`，我们建议您[包含的所有属性](../reference/msbuild-targets.md#pack-target)是通常在`.nuspec`改为文件在项目文件中。</span><span class="sxs-lookup"><span data-stu-id="d9b93-120">If you are creating a package using `dotnet.exe pack` or `msbuild pack target`, we recommend that you [include all the properties](../reference/msbuild-targets.md#pack-target) that are usually in the `.nuspec` file in the project file instead.</span></span> <span data-ttu-id="d9b93-121">但是，你也可以选择向[使用`.nuspec`文件打包使用`dotnet.exe`或`msbuild pack target` ](../reference/msbuild-targets.md#packing-using-a-nuspec)。</span><span class="sxs-lookup"><span data-stu-id="d9b93-121">However, you can instead choose to [use a `.nuspec` file to pack using `dotnet.exe` or `msbuild pack target`](../reference/msbuild-targets.md#packing-using-a-nuspec).</span></span>

- <span data-ttu-id="d9b93-122">有关从迁移的项目`packages.config`到[PackageReference](../consume-packages/package-references-in-project-files.md)、`.nuspec`文件不需要创建包。</span><span class="sxs-lookup"><span data-stu-id="d9b93-122">For projects migrated from `packages.config` to [PackageReference](../consume-packages/package-references-in-project-files.md), a `.nuspec` file is not required to create the package.</span></span> <span data-ttu-id="d9b93-123">请改用[msbuild 包](../reference/migrate-packages-config-to-package-reference.md#create-a-package-after-migration)。</span><span class="sxs-lookup"><span data-stu-id="d9b93-123">Instead, use [msbuild pack](../reference/migrate-packages-config-to-package-reference.md#create-a-package-after-migration).</span></span>

## <a name="general-form-and-schema"></a><span data-ttu-id="d9b93-124">常规形式和架构</span><span class="sxs-lookup"><span data-stu-id="d9b93-124">General form and schema</span></span>

<span data-ttu-id="d9b93-125">当前 `nuspec.xsd` 架构文件可在 [NuGet GitHub 存储库](https://github.com/NuGet/NuGet.Client/blob/dev/src/NuGet.Core/NuGet.Packaging/compiler/resources/nuspec.xsd)中找到。</span><span class="sxs-lookup"><span data-stu-id="d9b93-125">The current `nuspec.xsd` schema file can be found in the [NuGet GitHub repository](https://github.com/NuGet/NuGet.Client/blob/dev/src/NuGet.Core/NuGet.Packaging/compiler/resources/nuspec.xsd).</span></span>

<span data-ttu-id="d9b93-126">在此构架中，`.nuspec` 文件具有以下常规形式：</span><span class="sxs-lookup"><span data-stu-id="d9b93-126">Within this schema, a `.nuspec` file has the following general form:</span></span>

```xml
<?xml version="1.0" encoding="utf-8"?>
<package xmlns="http://schemas.microsoft.com/packaging/2010/07/nuspec.xsd">
    <metadata>
        <!-- Required elements-->
        <id></id>
        <version></version>
        <description></description>
        <authors></authors>

        <!-- Optional elements -->
        <!-- ... -->
    </metadata>
    <!-- Optional 'files' node -->
</package>
```

<span data-ttu-id="d9b93-127">有关架构的清晰可视表示形式，请在 Visual Studio 中以“设计”模式打开架构文件，然后单击“XML 架构资源管理器”链接  。</span><span class="sxs-lookup"><span data-stu-id="d9b93-127">For a clear visual representation of the schema, open the schema file in Visual Studio in Design mode and click on the **XML Schema Explorer** link.</span></span> <span data-ttu-id="d9b93-128">或者，将该文件作为代码打开，在编辑器中右键单击，然后选择“显示 XML 架构资源管理器”  。</span><span class="sxs-lookup"><span data-stu-id="d9b93-128">Alternately, open the file as code, right-click in the editor, and select **Show XML Schema Explorer**.</span></span> <span data-ttu-id="d9b93-129">无论哪种方式，都会获得如下所示的视图（大多数部件都处于扩展状态）：</span><span class="sxs-lookup"><span data-stu-id="d9b93-129">Either way you get a view like the one below (when mostly expanded):</span></span>

![nuspec.xsd 打开时的 Visual Studio 架构资源管理器](media/SchemaExplorer.png)

### <a name="required-metadata-elements"></a><span data-ttu-id="d9b93-131">所需的元数据元素</span><span class="sxs-lookup"><span data-stu-id="d9b93-131">Required metadata elements</span></span>

<span data-ttu-id="d9b93-132">尽管以下元素是包的最低要求，但应该考虑添加[可选元数据元素](#optional-metadata-elements)以改善开发人员对包的整体体验。</span><span class="sxs-lookup"><span data-stu-id="d9b93-132">Although the following elements are the minimum requirements for a package, you should consider adding the [optional metadata elements](#optional-metadata-elements) to improve the overall experience developers have with your package.</span></span> 

<span data-ttu-id="d9b93-133">这些元素必须出现在 `<metadata>` 元素中。</span><span class="sxs-lookup"><span data-stu-id="d9b93-133">These elements must appear within a `<metadata>` element.</span></span>

#### <a name="id"></a><span data-ttu-id="d9b93-134">id</span><span class="sxs-lookup"><span data-stu-id="d9b93-134">id</span></span> 
<span data-ttu-id="d9b93-135">不区分大小写的包标识符，在 nuget.org 或包驻留的任意库中必须是唯一的。</span><span class="sxs-lookup"><span data-stu-id="d9b93-135">The case-insensitive package identifier, which must be unique across nuget.org or whatever gallery the package resides in.</span></span> <span data-ttu-id="d9b93-136">ID 不得包含空格或对 URL 无效的字符，通常遵循 .NET 命名空间规则。</span><span class="sxs-lookup"><span data-stu-id="d9b93-136">IDs may not contain spaces or characters that are not valid for a URL, and generally follow .NET namespace rules.</span></span> <span data-ttu-id="d9b93-137">有关指南，请参阅[选择唯一的包标识符](../create-packages/creating-a-package.md#choose-a-unique-package-identifier-and-setting-the-version-number)。</span><span class="sxs-lookup"><span data-stu-id="d9b93-137">See [Choosing a unique package identifier](../create-packages/creating-a-package.md#choose-a-unique-package-identifier-and-setting-the-version-number) for guidance.</span></span>
#### <a name="version"></a><span data-ttu-id="d9b93-138">version</span><span class="sxs-lookup"><span data-stu-id="d9b93-138">version</span></span>
<span data-ttu-id="d9b93-139">遵循 major.minor.patch 模式的包版本  。</span><span class="sxs-lookup"><span data-stu-id="d9b93-139">The version of the package, following the *major.minor.patch* pattern.</span></span> <span data-ttu-id="d9b93-140">版本号可能包括预发布后缀，如[包版本控制](../reference/package-versioning.md#pre-release-versions)中所述。</span><span class="sxs-lookup"><span data-stu-id="d9b93-140">Version numbers may include a pre-release suffix as described in [Package versioning](../reference/package-versioning.md#pre-release-versions).</span></span> 
#### <a name="description"></a><span data-ttu-id="d9b93-141">description</span><span class="sxs-lookup"><span data-stu-id="d9b93-141">description</span></span>
<span data-ttu-id="d9b93-142">用于 UI 显示的包的详细说明。</span><span class="sxs-lookup"><span data-stu-id="d9b93-142">A long description of the package for UI display.</span></span> 
#### <a name="authors"></a><span data-ttu-id="d9b93-143">作者</span><span class="sxs-lookup"><span data-stu-id="d9b93-143">authors</span></span>
<span data-ttu-id="d9b93-144">包创建者的逗号分隔列表，与 nuget.org 上的配置文件名称一致。这些信息显示在 nuget.org 上的 NuGet 库中，并用于交叉引用同一作者的包。</span><span class="sxs-lookup"><span data-stu-id="d9b93-144">A comma-separated list of packages authors, matching the profile names on nuget.org. These are displayed in the NuGet Gallery on nuget.org and are used to cross-reference packages by the same authors.</span></span> 

### <a name="optional-metadata-elements"></a><span data-ttu-id="d9b93-145">可选元数据元素</span><span class="sxs-lookup"><span data-stu-id="d9b93-145">Optional metadata elements</span></span>

#### <a name="owners"></a><span data-ttu-id="d9b93-146">所有者</span><span class="sxs-lookup"><span data-stu-id="d9b93-146">owners</span></span>
<span data-ttu-id="d9b93-147">使用 nuget.org 上的配置文件名称的包创建者的逗号分隔列表。这通常和 `authors` 中的列表相同，将包上传到 nuget.org 时被忽略。请参阅[在 nuget.org 上管理包所有者](../nuget-org/publish-a-package.md#managing-package-owners-on-nugetorg)。</span><span class="sxs-lookup"><span data-stu-id="d9b93-147">A comma-separated list of the package creators using profile names on nuget.org. This is often the same list as in `authors`, and is ignored when uploading the package to nuget.org. See [Managing package owners on nuget.org](../nuget-org/publish-a-package.md#managing-package-owners-on-nugetorg).</span></span> 

#### <a name="projecturl"></a><span data-ttu-id="d9b93-148">projectUrl</span><span class="sxs-lookup"><span data-stu-id="d9b93-148">projectUrl</span></span>
<span data-ttu-id="d9b93-149">包的主页 URL，通常显示在 UI 中以及 nuget.org 中。</span><span class="sxs-lookup"><span data-stu-id="d9b93-149">A URL for the package's home page, often shown in UI displays as well as nuget.org.</span></span> 

#### <a name="licenseurl"></a><span data-ttu-id="d9b93-150">licenseUrl</span><span class="sxs-lookup"><span data-stu-id="d9b93-150">licenseUrl</span></span>
> [!Important]
> <span data-ttu-id="d9b93-151">将弃用 licenseUrl。</span><span class="sxs-lookup"><span data-stu-id="d9b93-151">licenseUrl is being deprecated.</span></span> <span data-ttu-id="d9b93-152">改为使用许可证。</span><span class="sxs-lookup"><span data-stu-id="d9b93-152">Use license instead.</span></span>

<span data-ttu-id="d9b93-153">包的许可证 URL，通常显示在 Ui 中 nuget.org 等。</span><span class="sxs-lookup"><span data-stu-id="d9b93-153">A URL for the package's license, often shown in UIs like nuget.org.</span></span>

#### <a name="license"></a><span data-ttu-id="d9b93-154">许可证</span><span class="sxs-lookup"><span data-stu-id="d9b93-154">license</span></span>
<span data-ttu-id="d9b93-155">一个 SPDX 许可证表达式或通常显示在 Ui 中，如 nuget.org 的包中的许可证文件的路径。如果要许可的常见许可，如 MIT 或 BSD 2 子句，包使用关联[SPDX 许可证标识符](https://spdx.org/licenses/)。</span><span class="sxs-lookup"><span data-stu-id="d9b93-155">An SPDX license expression or path to a license file within the package, often shown in UIs like nuget.org. If you're licensing the package under a common license, like MIT or BSD-2-Clause, use the associated [SPDX license identifier](https://spdx.org/licenses/).</span></span> <span data-ttu-id="d9b93-156">例如:</span><span class="sxs-lookup"><span data-stu-id="d9b93-156">For example:</span></span>

`<license type="expression">MIT</license>`

> [!Note]
> <span data-ttu-id="d9b93-157">NuGet.org 只接受由开放源计划或免费软件基金会批准的许可证表达式。</span><span class="sxs-lookup"><span data-stu-id="d9b93-157">NuGet.org only accepts license expressions that are approved by the Open Source Initiative or the Free Software Foundation.</span></span>

<span data-ttu-id="d9b93-158">如果您的包常见的多个许可证的许可，则可以指定复合许可证 using [SPDX 表达式语法版本 2.0](https://spdx.org/spdx-specification-21-web-version#h.jxpfx0ykyb60)。</span><span class="sxs-lookup"><span data-stu-id="d9b93-158">If your package is licensed under multiple common licenses, you can specify a composite license using the [SPDX expression syntax version 2.0](https://spdx.org/spdx-specification-21-web-version#h.jxpfx0ykyb60).</span></span> <span data-ttu-id="d9b93-159">例如:</span><span class="sxs-lookup"><span data-stu-id="d9b93-159">For example:</span></span>

`<license type="expression">BSD-2-Clause OR MIT</license>`

<span data-ttu-id="d9b93-160">如果使用不受许可证表达式的自定义许可证，你可以将打包`.txt`或`.md`具有许可证的文本的文件。</span><span class="sxs-lookup"><span data-stu-id="d9b93-160">If you use a custom license that isn't supported by license expressions, you can package a `.txt` or `.md` file with the license's text.</span></span> <span data-ttu-id="d9b93-161">例如:</span><span class="sxs-lookup"><span data-stu-id="d9b93-161">For example:</span></span>

```xml
<package>
  <metadata>
    ...
    <license type="file">LICENSE.txt</license>
    ...
  </metadata>
  <files>
    ...
    <file src="licenses\LICENSE.txt" target="" />
    ...
  </files>
</package>
```

<span data-ttu-id="d9b93-162">为 MSBuild 等效的看一看[装箱许可证表达式或许可证文件](msbuild-targets.md#packing-a-license-expression-or-a-license-file)。</span><span class="sxs-lookup"><span data-stu-id="d9b93-162">For the MSBuild equivalent, take a look at [Packing a license expression or a license file](msbuild-targets.md#packing-a-license-expression-or-a-license-file).</span></span>

<span data-ttu-id="d9b93-163">NuGet 的许可证表达式的确切语法是下面中所述[ABNF](https://tools.ietf.org/html/rfc5234)。</span><span class="sxs-lookup"><span data-stu-id="d9b93-163">The exact syntax of NuGet's license expressions is described below in [ABNF](https://tools.ietf.org/html/rfc5234).</span></span>
```cli
license-id            = <short form license identifier from https://spdx.org/spdx-specification-21-web-version#h.luq9dgcle9mo>

license-exception-id  = <short form license exception identifier from https://spdx.org/spdx-specification-21-web-version#h.ruv3yl8g6czd>

simple-expression = license-id / license-id”+”

compound-expression =  1*1(simple-expression /
                simple-expression "WITH" license-exception-id /
                compound-expression "AND" compound-expression /
                compound-expression "OR" compound-expression ) /                
                "(" compound-expression ")" )

license-expression =  1*1(simple-expression / compound-expression / UNLICENSED)
```

#### <a name="iconurl"></a><span data-ttu-id="d9b93-164">iconUrl</span><span class="sxs-lookup"><span data-stu-id="d9b93-164">iconUrl</span></span>
<span data-ttu-id="d9b93-165">64x64 透明背景图像的 URL，用作 UI 显示中包的图标。</span><span class="sxs-lookup"><span data-stu-id="d9b93-165">A URL for a 64x64 image with transparency background to use as the icon for the package in UI display.</span></span> <span data-ttu-id="d9b93-166">请确保此元素包含直接图像 URL，而不是包含图像的网页的 URL  。</span><span class="sxs-lookup"><span data-stu-id="d9b93-166">Be sure this element contains the *direct image URL* and not the URL of a web page containing the image.</span></span> <span data-ttu-id="d9b93-167">例如，若要使用 GitHub 中的图像，可使用原始文件 URL，如<em>https://github.com/\<username\>/\<repository\>/raw/\<branch\>/\<logo.png\></em>。</span><span class="sxs-lookup"><span data-stu-id="d9b93-167">For example, to use an image from GitHub, use the raw file URL like <em>https://github.com/\<username\>/\<repository\>/raw/\<branch\>/\<logo.png\></em>.</span></span> 

#### <a name="requirelicenseacceptance"></a><span data-ttu-id="d9b93-168">requireLicenseAcceptance</span><span class="sxs-lookup"><span data-stu-id="d9b93-168">requireLicenseAcceptance</span></span>
<span data-ttu-id="d9b93-169">一个布尔值，用于指定客户端是否必须提示使用者接受包许可证后才可安装包。</span><span class="sxs-lookup"><span data-stu-id="d9b93-169">A Boolean value specifying whether the client must prompt the consumer to accept the package license before installing the package.</span></span>

#### <a name="developmentdependency"></a><span data-ttu-id="d9b93-170">developmentDependency</span><span class="sxs-lookup"><span data-stu-id="d9b93-170">developmentDependency</span></span>
<span data-ttu-id="d9b93-171">(2.8+) 一个布尔值，用于指定包是否被标记为仅开发依赖项，从而防止包作为依赖项包含到其他包中  。</span><span class="sxs-lookup"><span data-stu-id="d9b93-171">*(2.8+)* A Boolean value specifying whether the package is be marked as a development-only-dependency, which prevents the package from being included as a dependency in other packages.</span></span> <span data-ttu-id="d9b93-172">使用 PackageReference (NuGet 4.8 +)，此标志也意味着它将从编译排除编译时资产。</span><span class="sxs-lookup"><span data-stu-id="d9b93-172">With PackageReference (NuGet 4.8+), this flag also means that it will exclude compile-time assets from compilation.</span></span> <span data-ttu-id="d9b93-173">请参阅[DevelopmentDependency 支持 PackageReference](https://github.com/NuGet/Home/wiki/DevelopmentDependency-support-for-PackageReference)</span><span class="sxs-lookup"><span data-stu-id="d9b93-173">See [DevelopmentDependency support for PackageReference](https://github.com/NuGet/Home/wiki/DevelopmentDependency-support-for-PackageReference)</span></span>

#### <a name="summary"></a><span data-ttu-id="d9b93-174">摘要</span><span class="sxs-lookup"><span data-stu-id="d9b93-174">summary</span></span>
<span data-ttu-id="d9b93-175">用于 UI 显示的包的简要说明。</span><span class="sxs-lookup"><span data-stu-id="d9b93-175">A short description of the package for UI display.</span></span> <span data-ttu-id="d9b93-176">如果省略，则使用 `description` 的截断版本。</span><span class="sxs-lookup"><span data-stu-id="d9b93-176">If omitted, a truncated version of `description` is used.</span></span>

#### <a name="releasenotes"></a><span data-ttu-id="d9b93-177">releaseNotes</span><span class="sxs-lookup"><span data-stu-id="d9b93-177">releaseNotes</span></span>
<span data-ttu-id="d9b93-178">(1.5+) 此版本包中所作更改的说明，通常代替包说明用在 UI 中，如 Visual Studio 包管理器的“更新”选项卡   。</span><span class="sxs-lookup"><span data-stu-id="d9b93-178">*(1.5+)* A description of the changes made in this release of the package, often used in UI like the **Updates** tab of the Visual Studio Package Manager in place of the package description.</span></span>

#### <a name="copyright"></a><span data-ttu-id="d9b93-179">copyright</span><span class="sxs-lookup"><span data-stu-id="d9b93-179">copyright</span></span>
<span data-ttu-id="d9b93-180">(1.5+) 包的版权详细信息  。</span><span class="sxs-lookup"><span data-stu-id="d9b93-180">*(1.5+)* Copyright details for the package.</span></span>

#### <a name="language"></a><span data-ttu-id="d9b93-181">语言</span><span class="sxs-lookup"><span data-stu-id="d9b93-181">language</span></span>
<span data-ttu-id="d9b93-182">包的区域设置 ID。</span><span class="sxs-lookup"><span data-stu-id="d9b93-182">The locale ID for the package.</span></span> <span data-ttu-id="d9b93-183">请参阅[创建本地化包](../create-packages/creating-localized-packages.md)。</span><span class="sxs-lookup"><span data-stu-id="d9b93-183">See [Creating localized packages](../create-packages/creating-localized-packages.md).</span></span>

#### <a name="tags"></a><span data-ttu-id="d9b93-184">标记</span><span class="sxs-lookup"><span data-stu-id="d9b93-184">tags</span></span>
<span data-ttu-id="d9b93-185">以空格分隔的标记和关键字列表，描述包并通过搜索和筛选辅助包的可发现性。</span><span class="sxs-lookup"><span data-stu-id="d9b93-185">A space-delimited list of tags and keywords that describe the package and aid discoverability of packages through search and filtering.</span></span> 

#### <a name="serviceable"></a><span data-ttu-id="d9b93-186">可维护性</span><span class="sxs-lookup"><span data-stu-id="d9b93-186">serviceable</span></span> 
<span data-ttu-id="d9b93-187">(3.3+) 仅限内部使用  。</span><span class="sxs-lookup"><span data-stu-id="d9b93-187">*(3.3+)* For internal NuGet use only.</span></span>

#### <a name="repository"></a><span data-ttu-id="d9b93-188">储存库</span><span class="sxs-lookup"><span data-stu-id="d9b93-188">repository</span></span>
<span data-ttu-id="d9b93-189">存储库的元数据，包括四个可选属性：*类型*并*url* *（4.0 +）* ，以及*分支*和*提交* *（4.6 +）* 。</span><span class="sxs-lookup"><span data-stu-id="d9b93-189">Repository metadata, consisting of four optional attributes: *type* and *url* *(4.0+)*, and *branch* and *commit* *(4.6+)*.</span></span> <span data-ttu-id="d9b93-190">这些特性，你可以将.nupkg 映射到存储库可能会获取与生成它，作为单独的分支或包生成的提交进行了详细说明。</span><span class="sxs-lookup"><span data-stu-id="d9b93-190">These attributes allow you to map the .nupkg to the repository that built it, with the potential to get as detailed as the individual branch or commit that built the package.</span></span> <span data-ttu-id="d9b93-191">这应该是版本控制软件可以直接调用的公开发布 url。</span><span class="sxs-lookup"><span data-stu-id="d9b93-191">This should be a publicly available url that can be invoked directly by a version control software.</span></span> <span data-ttu-id="d9b93-192">它不应为 html 页，因为这意味着计算机。</span><span class="sxs-lookup"><span data-stu-id="d9b93-192">It should not be an html page as this is meant for the computer.</span></span> <span data-ttu-id="d9b93-193">对于链接到项目页，使用`projectUrl`字段，而是。</span><span class="sxs-lookup"><span data-stu-id="d9b93-193">For linking to project page, use the `projectUrl` field, instead.</span></span>

#### <a name="minclientversion"></a><span data-ttu-id="d9b93-194">minClientVersion</span><span class="sxs-lookup"><span data-stu-id="d9b93-194">minClientVersion</span></span>
<span data-ttu-id="d9b93-195">指定可安装此包的最低 NuGet 客户端版本，并由 nuget.exe 和 Visual Studio 程序包管理器强制实施。</span><span class="sxs-lookup"><span data-stu-id="d9b93-195">Specifies the minimum version of the NuGet client that can install this package, enforced by nuget.exe and the Visual Studio Package Manager.</span></span> <span data-ttu-id="d9b93-196">只要包依赖于特定 NuGet 客户端版本中添加的 `.nuspec` 文件的特定功能，就会使用此功能。</span><span class="sxs-lookup"><span data-stu-id="d9b93-196">This is used whenever the package depends on specific features of the `.nuspec` file that were added in a particular version of the NuGet client.</span></span> <span data-ttu-id="d9b93-197">例如，使用 `developmentDependency` 特性的包应为 `minClientVersion` 指定“2.8”。</span><span class="sxs-lookup"><span data-stu-id="d9b93-197">For example, a package using the `developmentDependency` attribute should specify "2.8" for `minClientVersion`.</span></span> <span data-ttu-id="d9b93-198">同样，使用 `contentFiles` 元素（请参阅下一部分）的包应将 `minClientVersion` 设置为“3.3”。</span><span class="sxs-lookup"><span data-stu-id="d9b93-198">Similarly, a package using the `contentFiles` element (see the next section) should set `minClientVersion` to "3.3".</span></span> <span data-ttu-id="d9b93-199">另请注意，早于 2.5 的 NuGet 客户端无法识别此标记，所以无论 `minClientVersion` 包含什么内容，它们总是拒绝安装该包  。</span><span class="sxs-lookup"><span data-stu-id="d9b93-199">Note also that because NuGet clients prior to 2.5 do not recognize this flag, they *always* refuse to install the package no matter what `minClientVersion` contains.</span></span>

#### <a name="title"></a><span data-ttu-id="d9b93-200">标题</span><span class="sxs-lookup"><span data-stu-id="d9b93-200">title</span></span>
<span data-ttu-id="d9b93-201">显示了可以在一些 UI 中使用的包的用户友好标题。</span><span class="sxs-lookup"><span data-stu-id="d9b93-201">A human-friendly title of the package which may be used in some UI displays.</span></span> <span data-ttu-id="d9b93-202">（nuget.org 和 Visual Studio 中的包管理器不显示标题）</span><span class="sxs-lookup"><span data-stu-id="d9b93-202">(nuget.org and the Package Manager in Visual Studio do not show title)</span></span>

#### <a name="collection-elements"></a><span data-ttu-id="d9b93-203">集合元素</span><span class="sxs-lookup"><span data-stu-id="d9b93-203">Collection elements</span></span>

#### <a name="packagetypes"></a><span data-ttu-id="d9b93-204">packageTypes</span><span class="sxs-lookup"><span data-stu-id="d9b93-204">packageTypes</span></span>
<span data-ttu-id="d9b93-205">*(3.5+)* 如果不是传统的依赖项包，则为指定包类型的包括零个或多个 `<packageType>` 元素的集合。</span><span class="sxs-lookup"><span data-stu-id="d9b93-205">*(3.5+)* A collection of zero or more `<packageType>` elements specifying the type of the package if other than a traditional dependency package.</span></span> <span data-ttu-id="d9b93-206">每个 packageType 都具有 name 和 version 特性   。</span><span class="sxs-lookup"><span data-stu-id="d9b93-206">Each packageType has attributes of *name* and *version*.</span></span> <span data-ttu-id="d9b93-207">请参阅[设置包类型](../create-packages/set-package-type.md)。</span><span class="sxs-lookup"><span data-stu-id="d9b93-207">See [Setting a package type](../create-packages/set-package-type.md).</span></span>
#### <a name="dependencies"></a><span data-ttu-id="d9b93-208">依赖项</span><span class="sxs-lookup"><span data-stu-id="d9b93-208">dependencies</span></span>
<span data-ttu-id="d9b93-209">零个或多个 `<dependency>` 元素的集合，用来指定包的依赖项。</span><span class="sxs-lookup"><span data-stu-id="d9b93-209">A collection of zero or more `<dependency>` elements specifying the dependencies for the package.</span></span> <span data-ttu-id="d9b93-210">每个 dependency 都具有 id、version、include (3.x+) 和 exclude (3.x+) 特性     。</span><span class="sxs-lookup"><span data-stu-id="d9b93-210">Each dependency has attributes of *id*, *version*, *include* (3.x+), and *exclude* (3.x+).</span></span> <span data-ttu-id="d9b93-211">请参阅下面的[依赖项](#dependencies-element)。</span><span class="sxs-lookup"><span data-stu-id="d9b93-211">See [Dependencies](#dependencies-element) below.</span></span>
#### <a name="frameworkassemblies"></a><span data-ttu-id="d9b93-212">frameworkAssemblies</span><span class="sxs-lookup"><span data-stu-id="d9b93-212">frameworkAssemblies</span></span>
<span data-ttu-id="d9b93-213">(1.2+) 零个或多个 `<frameworkAssembly>` 元素的集合，用来标识此包要求的 .NET Framework 程序集引用，从而确保引用添加到使用该包的项目  。</span><span class="sxs-lookup"><span data-stu-id="d9b93-213">*(1.2+)* A collection of zero or more `<frameworkAssembly>` elements identifying .NET Framework assembly references that this package requires, which ensures that references are added to projects consuming the package.</span></span> <span data-ttu-id="d9b93-214">每个 frameworkAssembly 都具有 assemblyName 和 targetFramework 特性   。</span><span class="sxs-lookup"><span data-stu-id="d9b93-214">Each frameworkAssembly has *assemblyName* and *targetFramework* attributes.</span></span> <span data-ttu-id="d9b93-215">请参阅下面的[指定 Framework 程序集引用 GAC](#specifying-framework-assembly-references-gac)。</span><span class="sxs-lookup"><span data-stu-id="d9b93-215">See [Specifying framework assembly references GAC](#specifying-framework-assembly-references-gac) below.</span></span> |
#### <a name="references"></a><span data-ttu-id="d9b93-216">引用</span><span class="sxs-lookup"><span data-stu-id="d9b93-216">references</span></span>
<span data-ttu-id="d9b93-217">(1.5+) 零个或多个 `<reference>` 元素的集合，用来指定包的 `lib` 文件夹中添加为项目引用的程序集  。</span><span class="sxs-lookup"><span data-stu-id="d9b93-217">*(1.5+)* A collection of zero or more `<reference>` elements naming assemblies in the package's `lib` folder that are added as project references.</span></span> <span data-ttu-id="d9b93-218">每个 reference 都具有 file 特性  。</span><span class="sxs-lookup"><span data-stu-id="d9b93-218">Each reference has a *file* attribute.</span></span> <span data-ttu-id="d9b93-219">`<references>` 也可包含具有 targetFramework 特性的 `<group>` 元素，然后包含 `<reference>` 元素  。</span><span class="sxs-lookup"><span data-stu-id="d9b93-219">`<references>` can also contain a `<group>` element with a *targetFramework* attribute, that then contains `<reference>` elements.</span></span> <span data-ttu-id="d9b93-220">如果省略，则包含 `lib` 中的全部引用。</span><span class="sxs-lookup"><span data-stu-id="d9b93-220">If omitted, all references in `lib` are included.</span></span> <span data-ttu-id="d9b93-221">请参阅下面的[指定显式程序集引用](#specifying-explicit-assembly-references)。</span><span class="sxs-lookup"><span data-stu-id="d9b93-221">See [Specifying explicit assembly references](#specifying-explicit-assembly-references) below.</span></span>
#### <a name="contentfiles"></a><span data-ttu-id="d9b93-222">contentFiles</span><span class="sxs-lookup"><span data-stu-id="d9b93-222">contentFiles</span></span>
<span data-ttu-id="d9b93-223">(3.3+) `<files>` 元素的集合，用来标识包含在使用项目中的内容文件  。</span><span class="sxs-lookup"><span data-stu-id="d9b93-223">*(3.3+)* A collection of `<files>` elements that identify content files to include in the consuming project.</span></span> <span data-ttu-id="d9b93-224">这些文件用一组特性指定，用于描述如何在项目系统中使用这些文件。</span><span class="sxs-lookup"><span data-stu-id="d9b93-224">These files are specified with a set of attributes that describe how they should be used within the project system.</span></span> <span data-ttu-id="d9b93-225">请参阅下面的[指定包含在包中的文件](#specifying-files-to-include-in-the-package)。</span><span class="sxs-lookup"><span data-stu-id="d9b93-225">See [Specifying files to include in the package](#specifying-files-to-include-in-the-package) below.</span></span>
#### <a name="files"></a><span data-ttu-id="d9b93-226">文件</span><span class="sxs-lookup"><span data-stu-id="d9b93-226">files</span></span> 
<span data-ttu-id="d9b93-227">`<package>`节点可能包含`<files>`节点的同级`<metadata>`，和一个`<contentFiles>`下的子`<metadata>`，以指定要在包中包含的程序集和内容文件。</span><span class="sxs-lookup"><span data-stu-id="d9b93-227">The `<package>` node may contain a `<files>` node as a sibling to `<metadata>`, and a `<contentFiles>` child under `<metadata>`, to specify which assembly and content files to include in the package.</span></span> <span data-ttu-id="d9b93-228">有关详细信息，请参阅本主题后面的[包含程序集文件](#including-assembly-files)和[包含内容文件](#including-content-files)。</span><span class="sxs-lookup"><span data-stu-id="d9b93-228">See [Including assembly files](#including-assembly-files) and [Including content files](#including-content-files) later in this topic for details.</span></span>

## <a name="replacement-tokens"></a><span data-ttu-id="d9b93-229">替换令牌</span><span class="sxs-lookup"><span data-stu-id="d9b93-229">Replacement tokens</span></span>

<span data-ttu-id="d9b93-230">创建包时，[`nuget pack` 命令](../tools/cli-ref-pack.md)使用来自项目文件的值或 `pack` 命令的 `-properties` 开关来替换 `.nuspec` 文件的 `<metadata>` 节点中带 $ 分隔符的令牌。</span><span class="sxs-lookup"><span data-stu-id="d9b93-230">When creating a package, the [`nuget pack` command](../tools/cli-ref-pack.md) replaces $-delimited tokens in the `.nuspec` file's `<metadata>` node with values that come from either a project file or the `pack` command's `-properties` switch.</span></span>

<span data-ttu-id="d9b93-231">在命令行中，可使用 `nuget pack -properties <name>=<value>;<name>=<value>` 指定令牌值。</span><span class="sxs-lookup"><span data-stu-id="d9b93-231">On the command line, you specify token values with `nuget pack -properties <name>=<value>;<name>=<value>`.</span></span> <span data-ttu-id="d9b93-232">例如，可使用 `.nuspec` 中的 `$owners$` 和 `$desc$` 令牌，并在封装时提供值，如下所示：</span><span class="sxs-lookup"><span data-stu-id="d9b93-232">For example, you can use a token such as `$owners$` and `$desc$` in the `.nuspec` and provide the values at packing time as follows:</span></span>

```ps
nuget pack MyProject.csproj -properties
    owners=janedoe,harikm,kimo,xiaop;desc="Awesome app logger utility"
```

<span data-ttu-id="d9b93-233">如要使用项目中的值，请指定下表中描述的令牌（AssemblyInfo 指的是 `Properties` 中的文件，如 `AssemblyInfo.cs` 或 `AssemblyInfo.vb`）。</span><span class="sxs-lookup"><span data-stu-id="d9b93-233">To use values from a project, specify the tokens described in the table below (AssemblyInfo refers to the file in `Properties` such as `AssemblyInfo.cs` or `AssemblyInfo.vb`).</span></span>

<span data-ttu-id="d9b93-234">若要使用这些令牌，请通过项目文件而不仅仅是 `.nuspec` 来运行 `nuget pack`。</span><span class="sxs-lookup"><span data-stu-id="d9b93-234">To use these tokens, run `nuget pack` with the project file rather than just the `.nuspec`.</span></span> <span data-ttu-id="d9b93-235">例如，使用以下命令时，`.nuspec` 文件中的 `$id$` 和 `$version$` 令牌会被替换为项目的 `AssemblyName` 和 `AssemblyVersion` 值：</span><span class="sxs-lookup"><span data-stu-id="d9b93-235">For example, when using the following command, the `$id$` and `$version$` tokens in a `.nuspec` file are replaced with the project's `AssemblyName` and `AssemblyVersion` values:</span></span>

```ps
nuget pack MyProject.csproj
```

<span data-ttu-id="d9b93-236">通常情况下，如果已有项目，最初会使用自动包含一些标准令牌的 `nuget spec MyProject.csproj` 创建 `.nuspec`。</span><span class="sxs-lookup"><span data-stu-id="d9b93-236">Typically, when you have a project, you create the `.nuspec` initially using `nuget spec MyProject.csproj` which automatically includes some of these standard tokens.</span></span> <span data-ttu-id="d9b93-237">然而，如果项目缺少要求的 `.nuspec` 元素的值，那么 `nuget pack` 失败。</span><span class="sxs-lookup"><span data-stu-id="d9b93-237">However, if a project lacks values for required `.nuspec` elements, then `nuget pack` fails.</span></span> <span data-ttu-id="d9b93-238">此外，如果更改项目值，请确定在创建包之前重新生成，可通过 pack 命令的 `build` 开关方便地完成此操作。</span><span class="sxs-lookup"><span data-stu-id="d9b93-238">Furthermore, if you change project values, be sure to rebuild before creating the package; this can be done conveniently with the pack command's `build` switch.</span></span>

<span data-ttu-id="d9b93-239">除 `$configuration$` 外，项目中的值优先于在命令行上分配给相同令牌的任何值。</span><span class="sxs-lookup"><span data-stu-id="d9b93-239">With the exception of `$configuration$`, values in the project are used in preference to any assigned to the same token on the command line.</span></span>

| <span data-ttu-id="d9b93-240">标记</span><span class="sxs-lookup"><span data-stu-id="d9b93-240">Token</span></span> | <span data-ttu-id="d9b93-241">值来源</span><span class="sxs-lookup"><span data-stu-id="d9b93-241">Value source</span></span> | <span data-ttu-id="d9b93-242">值</span><span class="sxs-lookup"><span data-stu-id="d9b93-242">Value</span></span>
| --- | --- | ---
| <span data-ttu-id="d9b93-243">**$id$**</span><span class="sxs-lookup"><span data-stu-id="d9b93-243">**$id$**</span></span> | <span data-ttu-id="d9b93-244">项目文件</span><span class="sxs-lookup"><span data-stu-id="d9b93-244">Project file</span></span> | <span data-ttu-id="d9b93-245">项目文件中的 AssemblyName （标题）</span><span class="sxs-lookup"><span data-stu-id="d9b93-245">AssemblyName (title) from the project file</span></span> |
| <span data-ttu-id="d9b93-246">**$version$**</span><span class="sxs-lookup"><span data-stu-id="d9b93-246">**$version$**</span></span> | <span data-ttu-id="d9b93-247">AssemblyInfo</span><span class="sxs-lookup"><span data-stu-id="d9b93-247">AssemblyInfo</span></span> | <span data-ttu-id="d9b93-248">AssemblyInformationalVersion（如果存在），否则为 AssemblyVersion</span><span class="sxs-lookup"><span data-stu-id="d9b93-248">AssemblyInformationalVersion if present, otherwise AssemblyVersion</span></span> |
| <span data-ttu-id="d9b93-249">**$author$**</span><span class="sxs-lookup"><span data-stu-id="d9b93-249">**$author$**</span></span> | <span data-ttu-id="d9b93-250">AssemblyInfo</span><span class="sxs-lookup"><span data-stu-id="d9b93-250">AssemblyInfo</span></span> | <span data-ttu-id="d9b93-251">AssemblyCompany</span><span class="sxs-lookup"><span data-stu-id="d9b93-251">AssemblyCompany</span></span> |
| <span data-ttu-id="d9b93-252">**$title$**</span><span class="sxs-lookup"><span data-stu-id="d9b93-252">**$title$**</span></span> | <span data-ttu-id="d9b93-253">AssemblyInfo</span><span class="sxs-lookup"><span data-stu-id="d9b93-253">AssemblyInfo</span></span> | <span data-ttu-id="d9b93-254">AssemblyTitle</span><span class="sxs-lookup"><span data-stu-id="d9b93-254">AssemblyTitle</span></span> |
| <span data-ttu-id="d9b93-255">**$description$**</span><span class="sxs-lookup"><span data-stu-id="d9b93-255">**$description$**</span></span> | <span data-ttu-id="d9b93-256">AssemblyInfo</span><span class="sxs-lookup"><span data-stu-id="d9b93-256">AssemblyInfo</span></span> | <span data-ttu-id="d9b93-257">AssemblyDescription</span><span class="sxs-lookup"><span data-stu-id="d9b93-257">AssemblyDescription</span></span> |
| <span data-ttu-id="d9b93-258">**$copyright$**</span><span class="sxs-lookup"><span data-stu-id="d9b93-258">**$copyright$**</span></span> | <span data-ttu-id="d9b93-259">AssemblyInfo</span><span class="sxs-lookup"><span data-stu-id="d9b93-259">AssemblyInfo</span></span> | <span data-ttu-id="d9b93-260">AssemblyCopyright</span><span class="sxs-lookup"><span data-stu-id="d9b93-260">AssemblyCopyright</span></span> |
| <span data-ttu-id="d9b93-261">**$configuration$**</span><span class="sxs-lookup"><span data-stu-id="d9b93-261">**$configuration$**</span></span> | <span data-ttu-id="d9b93-262">程序集 DLL</span><span class="sxs-lookup"><span data-stu-id="d9b93-262">Assembly DLL</span></span> | <span data-ttu-id="d9b93-263">用于生成程序集的配置，默认为 Debug。</span><span class="sxs-lookup"><span data-stu-id="d9b93-263">Configuration used to build the assembly, defaulting to Debug.</span></span> <span data-ttu-id="d9b93-264">请注意，若要使用 Release 配置创建包，应始终在命令行上使用 `-properties Configuration=Release`。</span><span class="sxs-lookup"><span data-stu-id="d9b93-264">Note that to create a package using a Release configuration, you always use `-properties Configuration=Release` on the command line.</span></span> |

<span data-ttu-id="d9b93-265">包含[程序集文件](#including-assembly-files)和[内容文件](#including-content-files)时，令牌也可用于解析路径。</span><span class="sxs-lookup"><span data-stu-id="d9b93-265">Tokens can also be used to resolve paths when you include [assembly files](#including-assembly-files) and [content files](#including-content-files).</span></span> <span data-ttu-id="d9b93-266">这些令牌与 MSBuild 属性具有相同的名称，因此可根据当前生成配置来选择要包含的文件。</span><span class="sxs-lookup"><span data-stu-id="d9b93-266">The tokens have the same names as the MSBuild properties, making it possible to select files to be included depending on the current build configuration.</span></span> <span data-ttu-id="d9b93-267">例如，如果在 `.nuspec` 文件中使用以下令牌：</span><span class="sxs-lookup"><span data-stu-id="d9b93-267">For example, if you use the following tokens in the `.nuspec` file:</span></span>

```xml
<files>
    <file src="bin\$configuration$\$id$.pdb" target="lib\net40" />
</files>
```

<span data-ttu-id="d9b93-268">在 MSBuild 中生成具有 `Release` 配置且 `AssemblyName` 为 `LoggingLibrary` 的程序集，包中 `.nuspec` 文件中的结果行如下所示：</span><span class="sxs-lookup"><span data-stu-id="d9b93-268">And you build an assembly whose `AssemblyName` is `LoggingLibrary` with the `Release` configuration in MSBuild, the resulting lines in the `.nuspec` file in the package is as follows:</span></span>

```xml
<files>
    <file src="bin\Release\LoggingLibrary.pdb" target="lib\net40" />
</files>
```

## <a name="dependencies-element"></a><span data-ttu-id="d9b93-269">依赖关系元素</span><span class="sxs-lookup"><span data-stu-id="d9b93-269">Dependencies element</span></span>

<span data-ttu-id="d9b93-270">`<metadata>` 中的 `<dependencies>` 元素包含任意数量的 `<dependency>` 元素，用来标识顶级包所依赖的其他包。</span><span class="sxs-lookup"><span data-stu-id="d9b93-270">The `<dependencies>` element within `<metadata>` contains any number of `<dependency>` elements that identify other packages upon which the top-level package depends.</span></span> <span data-ttu-id="d9b93-271">每个 `<dependency>` 的特性如下所示：</span><span class="sxs-lookup"><span data-stu-id="d9b93-271">The attributes for each `<dependency>` are as follows:</span></span>

| <span data-ttu-id="d9b93-272">特性</span><span class="sxs-lookup"><span data-stu-id="d9b93-272">Attribute</span></span> | <span data-ttu-id="d9b93-273">描述</span><span class="sxs-lookup"><span data-stu-id="d9b93-273">Description</span></span> |
| --- | --- |
| `id` | <span data-ttu-id="d9b93-274">（必须）依赖项的包 ID，如“EntityFramework”和“NUnit”，同时也是 nuget.org 在包页面上显示的包名称。</span><span class="sxs-lookup"><span data-stu-id="d9b93-274">(Required) The package ID of the dependency, such as "EntityFramework" and "NUnit", which is the name of the package nuget.org shows on a package page.</span></span> |
| `version` | <span data-ttu-id="d9b93-275">（必需）可接受作为依赖项的版本范围。</span><span class="sxs-lookup"><span data-stu-id="d9b93-275">(Required) The range of versions acceptable as a dependency.</span></span> <span data-ttu-id="d9b93-276">有关准确语法，请参阅[包版本控制](../reference/package-versioning.md#version-ranges-and-wildcards)。</span><span class="sxs-lookup"><span data-stu-id="d9b93-276">See [Package versioning](../reference/package-versioning.md#version-ranges-and-wildcards) for exact syntax.</span></span> |
| <span data-ttu-id="d9b93-277">include</span><span class="sxs-lookup"><span data-stu-id="d9b93-277">include</span></span> | <span data-ttu-id="d9b93-278">包括/排除标记的逗号分隔列表（见下文），指示要包含在最终包中的依赖项。</span><span class="sxs-lookup"><span data-stu-id="d9b93-278">A comma-delimited list of include/exclude tags (see below) indicating of the dependency to include in the final package.</span></span> <span data-ttu-id="d9b93-279">默认值为 `all`。</span><span class="sxs-lookup"><span data-stu-id="d9b93-279">The default value is `all`.</span></span> |
| <span data-ttu-id="d9b93-280">exclude</span><span class="sxs-lookup"><span data-stu-id="d9b93-280">exclude</span></span> | <span data-ttu-id="d9b93-281">包括/排除标记的逗号分隔列表（见下文），指示要排除在最终包外的依赖项。</span><span class="sxs-lookup"><span data-stu-id="d9b93-281">A comma-delimited list of include/exclude tags (see below) indicating of the dependency to exclude in the final package.</span></span> <span data-ttu-id="d9b93-282">默认值是`build,analyzers`，可以覆盖。</span><span class="sxs-lookup"><span data-stu-id="d9b93-282">The  default value is `build,analyzers` which can be over-written.</span></span> <span data-ttu-id="d9b93-283">但`content/ ContentFiles`还将隐式排除无法覆盖在最终包中。</span><span class="sxs-lookup"><span data-stu-id="d9b93-283">But `content/ ContentFiles` are also implicitly excluded in the final package which can't be over-written.</span></span> <span data-ttu-id="d9b93-284">用 `exclude` 指定的标记优先于用 `include` 指定的标记。</span><span class="sxs-lookup"><span data-stu-id="d9b93-284">Tags specified with `exclude` take precedence over those specified with `include`.</span></span> <span data-ttu-id="d9b93-285">例如，`include="runtime, compile" exclude="compile"` 和 `include="runtime"` 相同。</span><span class="sxs-lookup"><span data-stu-id="d9b93-285">For example, `include="runtime, compile" exclude="compile"` is the same as `include="runtime"`.</span></span> |

| <span data-ttu-id="d9b93-286">包括/排除标记</span><span class="sxs-lookup"><span data-stu-id="d9b93-286">Include/Exclude tag</span></span> | <span data-ttu-id="d9b93-287">受影响的目标文件夹</span><span class="sxs-lookup"><span data-stu-id="d9b93-287">Affected folders of the target</span></span> |
| --- | --- |
| <span data-ttu-id="d9b93-288">contentFiles</span><span class="sxs-lookup"><span data-stu-id="d9b93-288">contentFiles</span></span> | <span data-ttu-id="d9b93-289">内容</span><span class="sxs-lookup"><span data-stu-id="d9b93-289">Content</span></span> |
| <span data-ttu-id="d9b93-290">Runtime — 运行时</span><span class="sxs-lookup"><span data-stu-id="d9b93-290">runtime</span></span> | <span data-ttu-id="d9b93-291">运行时、资源和 FrameworkAssemblies</span><span class="sxs-lookup"><span data-stu-id="d9b93-291">Runtime, Resources, and FrameworkAssemblies</span></span> |
| <span data-ttu-id="d9b93-292">编译</span><span class="sxs-lookup"><span data-stu-id="d9b93-292">compile</span></span> | <span data-ttu-id="d9b93-293">lib</span><span class="sxs-lookup"><span data-stu-id="d9b93-293">lib</span></span> |
| <span data-ttu-id="d9b93-294">生成</span><span class="sxs-lookup"><span data-stu-id="d9b93-294">build</span></span> | <span data-ttu-id="d9b93-295">生成（MSBuild 属性和目标）</span><span class="sxs-lookup"><span data-stu-id="d9b93-295">build (MSBuild props and targets)</span></span> |
| <span data-ttu-id="d9b93-296">本机</span><span class="sxs-lookup"><span data-stu-id="d9b93-296">native</span></span> | <span data-ttu-id="d9b93-297">本机</span><span class="sxs-lookup"><span data-stu-id="d9b93-297">native</span></span> |
| <span data-ttu-id="d9b93-298">无</span><span class="sxs-lookup"><span data-stu-id="d9b93-298">none</span></span> | <span data-ttu-id="d9b93-299">无文件夹</span><span class="sxs-lookup"><span data-stu-id="d9b93-299">No folders</span></span> |
| <span data-ttu-id="d9b93-300">全部</span><span class="sxs-lookup"><span data-stu-id="d9b93-300">all</span></span> | <span data-ttu-id="d9b93-301">全部文件夹</span><span class="sxs-lookup"><span data-stu-id="d9b93-301">All folders</span></span> |

<span data-ttu-id="d9b93-302">例如，以下行指示 `PackageA` 版本 1.1.0 或更高版本，以及 `PackageB` 版本 1.x 的依赖项。</span><span class="sxs-lookup"><span data-stu-id="d9b93-302">For example, the following lines indicate dependencies on `PackageA` version 1.1.0 or higher, and `PackageB` version 1.x.</span></span>

```xml
<dependencies>
    <dependency id="PackageA" version="1.1.0" />
    <dependency id="PackageB" version="[1,2)" />
</dependencies>
```

<span data-ttu-id="d9b93-303">以下行指示相同包上的依赖项，但指定包括 `PackageA` 的 `contentFiles` 和 `build` 文件夹，以及除 `PackageB` 的 `native` 和 `compile` 文件夹以外的所有文件夹。</span><span class="sxs-lookup"><span data-stu-id="d9b93-303">The following lines indicate dependencies on the same packages, but specify to include the `contentFiles` and `build` folders of `PackageA` and everything but the `native` and `compile` folders of `PackageB`"</span></span>

```xml
<dependencies>
    <dependency id="PackageA" version="1.1.0" include="contentFiles, build" />
    <dependency id="PackageB" version="[1,2)" exclude="native, compile" />
</dependencies>
```

<span data-ttu-id="d9b93-304">注意:创建时`.nuspec`从项目使用`nuget spec`，在该项目中存在的依赖关系自动包含在生成`.nuspec`文件。</span><span class="sxs-lookup"><span data-stu-id="d9b93-304">Note: When creating a `.nuspec` from a project using `nuget spec`, dependencies that exist in that project are automatically included in the resulting `.nuspec` file.</span></span>

### <a name="dependency-groups"></a><span data-ttu-id="d9b93-305">依赖项组</span><span class="sxs-lookup"><span data-stu-id="d9b93-305">Dependency groups</span></span>

<span data-ttu-id="d9b93-306">版本 2.0+ </span><span class="sxs-lookup"><span data-stu-id="d9b93-306">*Version 2.0+*</span></span>

<span data-ttu-id="d9b93-307">作为单个简单列表的替代方法，可使用 `<dependencies>` 中的 `<group>` 元素根据目标项目的框架配置文件指定依赖项。</span><span class="sxs-lookup"><span data-stu-id="d9b93-307">As an alternative to a single flat list, dependencies can be specified according to the framework profile of the target project using `<group>` elements within `<dependencies>`.</span></span>

<span data-ttu-id="d9b93-308">每个组都有一个名为 `targetFramework` 的特性，并包含零个或多个 `<dependency>` 元素。</span><span class="sxs-lookup"><span data-stu-id="d9b93-308">Each group has an attribute named `targetFramework` and contains zero or more `<dependency>` elements.</span></span> <span data-ttu-id="d9b93-309">当目标框架与项目的框架配置文件兼容时，将会一起安装这些依赖项。</span><span class="sxs-lookup"><span data-stu-id="d9b93-309">Those dependencies are installed together when  the target framework is compatible with the project's framework profile.</span></span>

<span data-ttu-id="d9b93-310">无 `targetFramework` 特性的 `<group>` 元素被用作依赖项的默认列表或回退列表。</span><span class="sxs-lookup"><span data-stu-id="d9b93-310">The `<group>` element without a `targetFramework` attribute is used as the default or fallback list of dependencies.</span></span> <span data-ttu-id="d9b93-311">有关确切的框架标识符，请参阅[目标框架](../reference/target-frameworks.md)。</span><span class="sxs-lookup"><span data-stu-id="d9b93-311">See [Target frameworks](../reference/target-frameworks.md) for the exact framework identifiers.</span></span>

> [!Important]
> <span data-ttu-id="d9b93-312">组格式不能与简单列表混合使用。</span><span class="sxs-lookup"><span data-stu-id="d9b93-312">The group format cannot be intermixed with a flat list.</span></span>

<span data-ttu-id="d9b93-313">以下示例显示了 `<group>` 元素的不同变体：</span><span class="sxs-lookup"><span data-stu-id="d9b93-313">The following example shows different variations of the `<group>` element:</span></span>

```xml
<dependencies>
    <group>
        <dependency id="RouteMagic" version="1.1.0" />
    </group>

    <group targetFramework="net40">
        <dependency id="jQuery" />
        <dependency id="WebActivator" />
    </group>

    <group targetFramework="sl30">
    </group>
</dependencies>
```

<a name="specifying-explicit-assembly-references"></a>

## <a name="explicit-assembly-references"></a><span data-ttu-id="d9b93-314">显式程序集引用</span><span class="sxs-lookup"><span data-stu-id="d9b93-314">Explicit assembly references</span></span>

<span data-ttu-id="d9b93-315">`<references>`元素可供使用的项目`packages.config`显式指定目标项目使用包时应引用的程序集。</span><span class="sxs-lookup"><span data-stu-id="d9b93-315">The `<references>` element is used by projects using `packages.config` to explicitly specify the assemblies that the target project should reference when using the package.</span></span> <span data-ttu-id="d9b93-316">显式引用通常用于仅设计时程序集。</span><span class="sxs-lookup"><span data-stu-id="d9b93-316">Explicit references are typically used for design-time only assemblies.</span></span> <span data-ttu-id="d9b93-317">有关详细信息，请参阅 》 上页面[选择项目引用的程序集](../create-packages/select-assemblies-referenced-by-projects.md)有关详细信息。</span><span class="sxs-lookup"><span data-stu-id="d9b93-317">For more information, see the page on [selecting assemblies referenced by projects](../create-packages/select-assemblies-referenced-by-projects.md) for more information.</span></span>

<span data-ttu-id="d9b93-318">例如，以下 `<references>` 元素指示 NuGet 仅对 `xunit.dll` 和 `xunit.extensions.dll` 添加引用，即使包中还有其他程序集：</span><span class="sxs-lookup"><span data-stu-id="d9b93-318">For example, the following `<references>` element instructs NuGet to add references to only `xunit.dll` and `xunit.extensions.dll` even if there are additional assemblies in the package:</span></span>

```xml
<references>
    <reference file="xunit.dll" />
    <reference file="xunit.extensions.dll" />
</references>
```

### <a name="reference-groups"></a><span data-ttu-id="d9b93-319">引用组</span><span class="sxs-lookup"><span data-stu-id="d9b93-319">Reference groups</span></span>

<span data-ttu-id="d9b93-320">作为单个简单列表的替代方法，可使用 `<references>` 中的 `<group>` 元素根据目标项目的框架配置文件指定引用。</span><span class="sxs-lookup"><span data-stu-id="d9b93-320">As an alternative to a single flat list, references can be specified according to the framework profile of the target project using `<group>` elements within `<references>`.</span></span>

<span data-ttu-id="d9b93-321">每个组都有一个名为 `targetFramework` 的特性，并包含零个或多个 `<reference>` 元素。</span><span class="sxs-lookup"><span data-stu-id="d9b93-321">Each group has an attribute named `targetFramework` and contains zero or more `<reference>` elements.</span></span> <span data-ttu-id="d9b93-322">当目标框架与项目的框架配置文件兼容时，会将引用添加到项目中。</span><span class="sxs-lookup"><span data-stu-id="d9b93-322">Those references are added to a project when the target framework is compatible with the project's framework profile.</span></span>

<span data-ttu-id="d9b93-323">无 `targetFramework` 特性的 `<group>` 元素被用作引用的默认列表或回退列表。</span><span class="sxs-lookup"><span data-stu-id="d9b93-323">The `<group>` element without a `targetFramework` attribute is used as the default or fallback list of references.</span></span> <span data-ttu-id="d9b93-324">有关确切的框架标识符，请参阅[目标框架](../reference/target-frameworks.md)。</span><span class="sxs-lookup"><span data-stu-id="d9b93-324">See [Target frameworks](../reference/target-frameworks.md) for the exact framework identifiers.</span></span>

> [!Important]
> <span data-ttu-id="d9b93-325">组格式不能与简单列表混合使用。</span><span class="sxs-lookup"><span data-stu-id="d9b93-325">The group format cannot be intermixed with a flat list.</span></span>

<span data-ttu-id="d9b93-326">以下示例显示了 `<group>` 元素的不同变体：</span><span class="sxs-lookup"><span data-stu-id="d9b93-326">The following example shows different variations of the `<group>` element:</span></span>

```xml
<references>
    <group>
        <reference file="a.dll" />
    </group>

    <group targetFramework="net45">
        <reference file="b45.dll" />
    </group>

    <group targetFramework="netcore45">
        <reference file="bcore45.dll" />
    </group>
</references>
```

<a name="specifying-framework-assembly-references-gac"></a>

## <a name="framework-assembly-references"></a><span data-ttu-id="d9b93-327">Framework 程序集引用</span><span class="sxs-lookup"><span data-stu-id="d9b93-327">Framework assembly references</span></span>

<span data-ttu-id="d9b93-328">Framework 程序集是 .NET Framework 的一部分，并已存在于任何给定计算机的全局程序集缓存 (GAC) 中。</span><span class="sxs-lookup"><span data-stu-id="d9b93-328">Framework assemblies are those that are part of the .NET framework and should already be in the global assembly cache (GAC) for any given machine.</span></span> <span data-ttu-id="d9b93-329">通过在 `<frameworkAssemblies>` 元素中标识这些程序集，包可确保在项目尚未具有此类引用的情况下，将必需的引用添加到项目中。</span><span class="sxs-lookup"><span data-stu-id="d9b93-329">By identifying those assemblies within the `<frameworkAssemblies>` element, a package can ensure that required references are added to a project in the event that the project doesn't have such references already.</span></span> <span data-ttu-id="d9b93-330">当然，此类程序集不直接包含在包中。</span><span class="sxs-lookup"><span data-stu-id="d9b93-330">Such assemblies, of course, are not included in a package directly.</span></span>

<span data-ttu-id="d9b93-331">`<frameworkAssemblies>` 元素包含零个或多个 `<frameworkAssembly>` 元素，这些元素指定以下特性：</span><span class="sxs-lookup"><span data-stu-id="d9b93-331">The `<frameworkAssemblies>` element contains zero or more `<frameworkAssembly>` elements, each of which specifies the following attributes:</span></span>

| <span data-ttu-id="d9b93-332">特性</span><span class="sxs-lookup"><span data-stu-id="d9b93-332">Attribute</span></span> | <span data-ttu-id="d9b93-333">描述</span><span class="sxs-lookup"><span data-stu-id="d9b93-333">Description</span></span> |
| --- | --- |
| <span data-ttu-id="d9b93-334">**assemblyName**</span><span class="sxs-lookup"><span data-stu-id="d9b93-334">**assemblyName**</span></span> | <span data-ttu-id="d9b93-335">（必需）完全限定程序集名称。</span><span class="sxs-lookup"><span data-stu-id="d9b93-335">(Required) The fully qualified assembly name.</span></span> |
| <span data-ttu-id="d9b93-336">**targetFramework**</span><span class="sxs-lookup"><span data-stu-id="d9b93-336">**targetFramework**</span></span> | <span data-ttu-id="d9b93-337">（可选）指定此引用适用的目标框架。</span><span class="sxs-lookup"><span data-stu-id="d9b93-337">(Optional) Specifies the target framework to which this reference applies.</span></span> <span data-ttu-id="d9b93-338">如果省略，则表示该引用适用于全部框架。</span><span class="sxs-lookup"><span data-stu-id="d9b93-338">If omitted, indicates that the reference applies to all frameworks.</span></span> <span data-ttu-id="d9b93-339">有关确切的框架标识符，请参阅[目标框架](../reference/target-frameworks.md)。</span><span class="sxs-lookup"><span data-stu-id="d9b93-339">See [Target frameworks](../reference/target-frameworks.md) for the exact framework identifiers.</span></span> |

<span data-ttu-id="d9b93-340">以下示例显示了对全部目标框架的 `System.Net` 的引用，以及对仅用于 .NET Framework 4.0 的 `System.ServiceModel` 的引用：</span><span class="sxs-lookup"><span data-stu-id="d9b93-340">The following example shows a reference to `System.Net` for all target frameworks, and a reference to `System.ServiceModel` for .NET Framework 4.0 only:</span></span>

```xml
<frameworkAssemblies>
    <frameworkAssembly assemblyName="System.Net"  />

    <frameworkAssembly assemblyName="System.ServiceModel" targetFramework="net40" />
</frameworkAssemblies>
```

<a name="specifying-files-to-include-in-the-package"></a>

## <a name="including-assembly-files"></a><span data-ttu-id="d9b93-341">包含程序集文件</span><span class="sxs-lookup"><span data-stu-id="d9b93-341">Including assembly files</span></span>

<span data-ttu-id="d9b93-342">如果遵循[创建包](../create-packages/creating-a-package.md)中介绍的约定，则不必在 `.nuspec` 文件中显式指定文件列表。</span><span class="sxs-lookup"><span data-stu-id="d9b93-342">If you follow the conventions described in [Creating a Package](../create-packages/creating-a-package.md), you do not have to explicitly specify a list of files in the `.nuspec` file.</span></span> <span data-ttu-id="d9b93-343">`nuget pack` 命令自动选取所需的文件。</span><span class="sxs-lookup"><span data-stu-id="d9b93-343">The `nuget pack` command automatically picks up the necessary files.</span></span>

> [!Important]
> <span data-ttu-id="d9b93-344">当包安装到项目中时，NuGet 自动将程序集引用添加到包的 DLL，不包括命名为 `.resources.dll` 的内容，因为它们被假定为本地化的附属程序集  。</span><span class="sxs-lookup"><span data-stu-id="d9b93-344">When a package is installed into a project, NuGet automatically adds assembly references to the package's DLLs, *excluding* those that are named `.resources.dll` because they are assumed to be localized satellite assemblies.</span></span> <span data-ttu-id="d9b93-345">为此，请避免对包含基本包代码的文件使用 `.resources.dll`。</span><span class="sxs-lookup"><span data-stu-id="d9b93-345">For this reason, avoid using `.resources.dll` for files that otherwise contain essential package code.</span></span>

<span data-ttu-id="d9b93-346">若要绕过此自动行为，并显式控制包中包含的文件，请将 `<files>` 元素作为 `<package>` 的子元素（和 `<metadata>` 的同级元素），并使用单独的 `<file>` 元素标识每个文件。</span><span class="sxs-lookup"><span data-stu-id="d9b93-346">To bypass this automatic behavior and explicitly control which files are included in a package, place a `<files>` element as a child of `<package>` (and a sibling of `<metadata>`), identifying each file with a separate `<file>` element.</span></span> <span data-ttu-id="d9b93-347">例如：</span><span class="sxs-lookup"><span data-stu-id="d9b93-347">For example:</span></span>

```xml
<files>
    <file src="bin\Debug\*.dll" target="lib" />
    <file src="bin\Debug\*.pdb" target="lib" />
    <file src="tools\**\*.*" exclude="**\*.log" />
</files>
```

<span data-ttu-id="d9b93-348">在 NuGet 2.x 及更早版本中，如果项目使用 `packages.config`，在安装包时，`<files>` 元素也用于包含不可变的内容文件。</span><span class="sxs-lookup"><span data-stu-id="d9b93-348">With NuGet 2.x and earlier, and projects using `packages.config`, the `<files>` element is also used to include immutable content files when a package is installed.</span></span> <span data-ttu-id="d9b93-349">通过 NuGet 3.3+ 和项目 PackageReference，将改为使用 `<contentFiles>` 元素。</span><span class="sxs-lookup"><span data-stu-id="d9b93-349">With NuGet 3.3+ and projects PackageReference, the `<contentFiles>` element is used instead.</span></span> <span data-ttu-id="d9b93-350">有关详细信息，请参阅下面的[包含内容文件](#including-content-files)。</span><span class="sxs-lookup"><span data-stu-id="d9b93-350">See [Including content files](#including-content-files) below for details.</span></span>

### <a name="file-element-attributes"></a><span data-ttu-id="d9b93-351">文件元素特性</span><span class="sxs-lookup"><span data-stu-id="d9b93-351">File element attributes</span></span>

<span data-ttu-id="d9b93-352">每个 `<file>` 元素指定以下特性：</span><span class="sxs-lookup"><span data-stu-id="d9b93-352">Each `<file>` element specifies the following attributes:</span></span>

| <span data-ttu-id="d9b93-353">特性</span><span class="sxs-lookup"><span data-stu-id="d9b93-353">Attribute</span></span> | <span data-ttu-id="d9b93-354">描述</span><span class="sxs-lookup"><span data-stu-id="d9b93-354">Description</span></span> |
| --- | --- |
| <span data-ttu-id="d9b93-355">**src**</span><span class="sxs-lookup"><span data-stu-id="d9b93-355">**src**</span></span> | <span data-ttu-id="d9b93-356">文件或要包含的文件位置，受 `exclude` 特性指定排除规则约束。</span><span class="sxs-lookup"><span data-stu-id="d9b93-356">The location of the file or files to include, subject to exclusions specified by the `exclude` attribute.</span></span> <span data-ttu-id="d9b93-357">路径是相对于 `.nuspec` 文件的路径，除非指定了绝对路径。</span><span class="sxs-lookup"><span data-stu-id="d9b93-357">The path is relative to the `.nuspec` file unless an absolute path is specified.</span></span> <span data-ttu-id="d9b93-358">允许使用通配符 `*`，双通配符 `**` 意味着递归文件夹搜索。</span><span class="sxs-lookup"><span data-stu-id="d9b93-358">The wildcard character `*` is allowed, and the double wildcard `**` implies a recursive folder search.</span></span> |
| <span data-ttu-id="d9b93-359">**target**</span><span class="sxs-lookup"><span data-stu-id="d9b93-359">**target**</span></span> | <span data-ttu-id="d9b93-360">放置源文件的包中文件夹的相对路径，必须以 `lib`、`content`、`build` 或 `tools` 开头。</span><span class="sxs-lookup"><span data-stu-id="d9b93-360">The relative path to the folder within the package where the source files are placed, which must begin with `lib`, `content`, `build`, or `tools`.</span></span> <span data-ttu-id="d9b93-361">请参阅[从基于约定的工作目录创建 .nuspec](../create-packages/creating-a-package.md#from-a-convention-based-working-directory)。</span><span class="sxs-lookup"><span data-stu-id="d9b93-361">See [Creating a .nuspec from a convention-based working directory](../create-packages/creating-a-package.md#from-a-convention-based-working-directory).</span></span> |
| <span data-ttu-id="d9b93-362">**exclude**</span><span class="sxs-lookup"><span data-stu-id="d9b93-362">**exclude**</span></span> | <span data-ttu-id="d9b93-363">要从 `src` 位置排除的文件或文件模式的分号分隔列表。</span><span class="sxs-lookup"><span data-stu-id="d9b93-363">A semicolon-delimited list of files or file patterns to exclude from the `src` location.</span></span> <span data-ttu-id="d9b93-364">允许使用通配符 `*`，双通配符 `**` 意味着递归文件夹搜索。</span><span class="sxs-lookup"><span data-stu-id="d9b93-364">The wildcard character `*` is allowed, and the double wildcard `**` implies a recursive folder search.</span></span> |

### <a name="examples"></a><span data-ttu-id="d9b93-365">示例</span><span class="sxs-lookup"><span data-stu-id="d9b93-365">Examples</span></span>

<span data-ttu-id="d9b93-366">**单个程序集**</span><span class="sxs-lookup"><span data-stu-id="d9b93-366">**Single assembly**</span></span>

    Source file:
        library.dll

    .nuspec entry:
        <file src="library.dll" target="lib" />

    Packaged result:
        lib\library.dll

<span data-ttu-id="d9b93-367">**特定于目标框架的单个程序集**</span><span class="sxs-lookup"><span data-stu-id="d9b93-367">**Single assembly specific to a target framework**</span></span>

    Source file:
        library.dll

    .nuspec entry:
        <file src="assemblies\net40\library.dll" target="lib\net40" />

    Packaged result:
        lib\net40\library.dll

<span data-ttu-id="d9b93-368">**使用通配符的 DLL 集**</span><span class="sxs-lookup"><span data-stu-id="d9b93-368">**Set of DLLs using a wildcard**</span></span>

    Source files:
        bin\release\libraryA.dll
        bin\release\libraryB.dll

    .nuspec entry:
        <file src="bin\release\*.dll" target="lib" />

    Packaged result:
        lib\libraryA.dll
        lib\libraryB.dll

<span data-ttu-id="d9b93-369">**适用于不同框架的 DLL**</span><span class="sxs-lookup"><span data-stu-id="d9b93-369">**DLLs for different frameworks**</span></span>

    Source files:
        lib\net40\library.dll
        lib\net20\library.dll

    .nuspec entry (using ** recursive search):
        <file src="lib\**" target="lib" />

    Packaged result:
        lib\net40\library.dll
        lib\net20\library.dll

<span data-ttu-id="d9b93-370">**排除文件**</span><span class="sxs-lookup"><span data-stu-id="d9b93-370">**Excluding files**</span></span>

    Source files:
        \tools\fileA.bak
        \tools\fileB.bak
        \tools\fileA.log
        \tools\build\fileB.log

    .nuspec entries:
        <file src="tools\*.*" target="tools" exclude="tools\*.bak" />
        <file src="tools\**\*.*" target="tools" exclude="**\*.log" />

    Package result:
        (no files)

## <a name="including-content-files"></a><span data-ttu-id="d9b93-371">包含内容文件</span><span class="sxs-lookup"><span data-stu-id="d9b93-371">Including content files</span></span>

<span data-ttu-id="d9b93-372">内容文件是包需要包含在项目中的不可变文件。</span><span class="sxs-lookup"><span data-stu-id="d9b93-372">Content files are immutable files that a package needs to include in a project.</span></span> <span data-ttu-id="d9b93-373">不可变文件指的是使用项目不会修改的文件。</span><span class="sxs-lookup"><span data-stu-id="d9b93-373">Being immutable, they are not intended to be modified by the consuming project.</span></span> <span data-ttu-id="d9b93-374">内容文件示例包括：</span><span class="sxs-lookup"><span data-stu-id="d9b93-374">Example content files include:</span></span>

- <span data-ttu-id="d9b93-375">作为资源嵌入的图像</span><span class="sxs-lookup"><span data-stu-id="d9b93-375">Images that are embedded as resources</span></span>
- <span data-ttu-id="d9b93-376">已编译的源文件</span><span class="sxs-lookup"><span data-stu-id="d9b93-376">Source files that are already compiled</span></span>
- <span data-ttu-id="d9b93-377">需要包含在项目的生成输出中的脚本</span><span class="sxs-lookup"><span data-stu-id="d9b93-377">Scripts that need to be included with the build output of the project</span></span>
- <span data-ttu-id="d9b93-378">需要包含在项目中，但不需要进行任何项目特定的更改的包的配置文件</span><span class="sxs-lookup"><span data-stu-id="d9b93-378">Configuration files for the package that need to be included in the project but don't need any project-specific changes</span></span>

<span data-ttu-id="d9b93-379">内容文件使用 `<files>` 元素包含在包中，并在 `target` 特性中指定 `content` 文件夹。</span><span class="sxs-lookup"><span data-stu-id="d9b93-379">Content files are included in a package using the `<files>` element, specifying the `content` folder in the `target` attribute.</span></span> <span data-ttu-id="d9b93-380">但是，使用 PackageReference（而不是使用 `<contentFiles>` 元素）将包安装到项目中时，将忽略这些文件。</span><span class="sxs-lookup"><span data-stu-id="d9b93-380">However, such files are ignored when the package is installed in a project using PackageReference, which instead uses the `<contentFiles>` element.</span></span>

<span data-ttu-id="d9b93-381">为了最大限度地兼容使用项目，一个包最好在两个元素中指定内容文件。</span><span class="sxs-lookup"><span data-stu-id="d9b93-381">For maximum compatibility with consuming projects, a package ideally specifies the content files in both elements.</span></span>

### <a name="using-the-files-element-for-content-files"></a><span data-ttu-id="d9b93-382">对内容文件使用文件元素</span><span class="sxs-lookup"><span data-stu-id="d9b93-382">Using the files element for content files</span></span>

<span data-ttu-id="d9b93-383">对于内容文件，只需使用与程序集文件相同的格式，但应在 `target` 属性中将 `content` 指定为基本文件夹，如以下示例所示。</span><span class="sxs-lookup"><span data-stu-id="d9b93-383">For content files, simply use the same format as for assembly files, but specify `content` as the base folder in the `target` attribute as shown in the following examples.</span></span>

<span data-ttu-id="d9b93-384">**基本内容文件**</span><span class="sxs-lookup"><span data-stu-id="d9b93-384">**Basic content files**</span></span>

    Source files:
        css\mobile\style1.css
        css\mobile\style2.css

    .nuspec entry:
        <file src="css\mobile\*.css" target="content\css\mobile" />

    Packaged result:
        content\css\mobile\style1.css
        content\css\mobile\style2.css

<span data-ttu-id="d9b93-385">**具有目录结构的内容文件**</span><span class="sxs-lookup"><span data-stu-id="d9b93-385">**Content files with directory structure**</span></span>

    Source files:
        css\mobile\style.css
        css\mobile\wp7\style.css
        css\browser\style.css

    .nuspec entry:
        <file src="css\**\*.css" target="content\css" />

    Packaged result:
        content\css\mobile\style.css
        content\css\mobile\wp7\style.css
        content\css\browser\style.css

<span data-ttu-id="d9b93-386">**特定于目标框架的内容文件**</span><span class="sxs-lookup"><span data-stu-id="d9b93-386">**Content file specific to a target framework**</span></span>

    Source file:
        css\cool\style.css

    .nuspec entry
        <file src="css\cool\style.css" target="Content" />

    Packaged result:
        content\style.css

<span data-ttu-id="d9b93-387">**复制到名称中带点的文件夹的内容文件**</span><span class="sxs-lookup"><span data-stu-id="d9b93-387">**Content file copied to a folder with dot in name**</span></span>

<span data-ttu-id="d9b93-388">在此情况下，NuGet 发现 `target` 中的扩展名与 `src` 中的扩展名不匹配，因此将 `target` 中名称的该部分作为文件夹：</span><span class="sxs-lookup"><span data-stu-id="d9b93-388">In this case, NuGet sees that the extension in `target` does not match the extension in `src` and thus treats that part of the name in `target` as a folder:</span></span>

    Source file:
        images\picture.png

    .nuspec entry:
        <file src="images\picture.png" target="Content\images\package.icons" />

    Packaged result:
        content\images\package.icons\picture.png

<span data-ttu-id="d9b93-389">**不具有扩展名的内容文件**</span><span class="sxs-lookup"><span data-stu-id="d9b93-389">**Content files without extensions**</span></span>

<span data-ttu-id="d9b93-390">若要包含不具有扩展名的文件，请使用 `*` 或 `**` 通配符：</span><span class="sxs-lookup"><span data-stu-id="d9b93-390">To include files without an extension, use the `*` or `**` wildcards:</span></span>

    Source file:
        flags\installed

    .nuspec entry:
        <file src="flags\**" target="flags" />

    Packaged result:
        flags\installed

<span data-ttu-id="d9b93-391">**具有深层路径和深层目标的内容文件**</span><span class="sxs-lookup"><span data-stu-id="d9b93-391">**Content files with deep path and deep target**</span></span>

<span data-ttu-id="d9b93-392">在此情况下，由于源文件和目标文件的扩展名匹配，NuGet 假定目标是文件名而不是文件夹：</span><span class="sxs-lookup"><span data-stu-id="d9b93-392">In this case, because the file extensions of the source and target match, NuGet assumes that the target is a file name and not a folder:</span></span>

    Source file:
        css\cool\style.css

    .nuspec entry:
        <file src="css\cool\style.css" target="Content\css\cool" />
        or:
        <file src="css\cool\style.css" target="Content\css\cool\style.css" />

    Packaged result:
        content\css\cool\style.css

<span data-ttu-id="d9b93-393">**重命名包中的内容文件**</span><span class="sxs-lookup"><span data-stu-id="d9b93-393">**Renaming a content file in the package**</span></span>

    Source file:
        ie\css\style.css

    .nuspec entry:
        <file src="ie\css\style.css" target="Content\css\ie.css" />

    Packaged result:
        content\css\ie.css

<span data-ttu-id="d9b93-394">**排除文件**</span><span class="sxs-lookup"><span data-stu-id="d9b93-394">**Excluding files**</span></span>

    Source file:
        docs\*.txt (multiple files)

    .nuspec entry:
        <file src="docs\*.txt" target="content\docs" exclude="docs\admin.txt" />
        or
        <file src="*.txt" target="content\docs" exclude="admin.txt;log.txt" />

    Packaged result:
        All .txt files from docs except admin.txt (first example)
        All .txt files from docs except admin.txt and log.txt (second example)

<a name="using-contentfiles-element-for-content-files"></a>

### <a name="using-the-contentfiles-element-for-content-files"></a><span data-ttu-id="d9b93-395">对内容文件使用 contentFiles 元素</span><span class="sxs-lookup"><span data-stu-id="d9b93-395">Using the contentFiles element for content files</span></span>

<span data-ttu-id="d9b93-396">*NuGet 4.0+ 与 PackageReference*</span><span class="sxs-lookup"><span data-stu-id="d9b93-396">*NuGet 4.0+ with PackageReference*</span></span>

<span data-ttu-id="d9b93-397">默认情况下，包将内容放置在 `contentFiles` 文件夹中（见下文），`nuget pack` 使用默认特性将全部文件包含在该文件夹中。</span><span class="sxs-lookup"><span data-stu-id="d9b93-397">By default, a package places content in a `contentFiles` folder (see below) and `nuget pack` included all files in that folder using default attributes.</span></span> <span data-ttu-id="d9b93-398">在此情况下，根本没有必要在 `.nuspec` 中包含 `contentFiles` 节点。</span><span class="sxs-lookup"><span data-stu-id="d9b93-398">In this case it's not necessary to include a `contentFiles` node in the `.nuspec` at all.</span></span>

<span data-ttu-id="d9b93-399">若要控制包含哪些文件，`<contentFiles>` 元素指定是 `<files>` 元素的集合，可标识包含的确切文件。</span><span class="sxs-lookup"><span data-stu-id="d9b93-399">To control which files are included, the `<contentFiles>` element specifies is a collection of `<files>` elements that identify the exact files include.</span></span>

<span data-ttu-id="d9b93-400">这些文件用一组特性指定，用于描述如何在项目系统中使用这些文件：</span><span class="sxs-lookup"><span data-stu-id="d9b93-400">These files are specified with a set of attributes that describe how they should be used within the project system:</span></span>

| <span data-ttu-id="d9b93-401">特性</span><span class="sxs-lookup"><span data-stu-id="d9b93-401">Attribute</span></span> | <span data-ttu-id="d9b93-402">描述</span><span class="sxs-lookup"><span data-stu-id="d9b93-402">Description</span></span> |
| --- | --- |
| <span data-ttu-id="d9b93-403">**include**</span><span class="sxs-lookup"><span data-stu-id="d9b93-403">**include**</span></span> | <span data-ttu-id="d9b93-404">（必需）文件或要包含的文件位置，受 `exclude` 特性指定的排除规则约束。</span><span class="sxs-lookup"><span data-stu-id="d9b93-404">(Required) The location of the file or files to include, subject to exclusions specified by the `exclude` attribute.</span></span> <span data-ttu-id="d9b93-405">路径是相对于 `.nuspec` 文件的路径，除非指定了绝对路径。</span><span class="sxs-lookup"><span data-stu-id="d9b93-405">The path is relative to the `.nuspec` file unless an absolute path is specified.</span></span> <span data-ttu-id="d9b93-406">允许使用通配符 `*`，双通配符 `**` 意味着递归文件夹搜索。</span><span class="sxs-lookup"><span data-stu-id="d9b93-406">The wildcard character `*` is allowed, and the double wildcard `**` implies a recursive folder search.</span></span> |
| <span data-ttu-id="d9b93-407">**exclude**</span><span class="sxs-lookup"><span data-stu-id="d9b93-407">**exclude**</span></span> | <span data-ttu-id="d9b93-408">要从 `src` 位置排除的文件或文件模式的分号分隔列表。</span><span class="sxs-lookup"><span data-stu-id="d9b93-408">A semicolon-delimited list of files or file patterns to exclude from the `src` location.</span></span> <span data-ttu-id="d9b93-409">允许使用通配符 `*`，双通配符 `**` 意味着递归文件夹搜索。</span><span class="sxs-lookup"><span data-stu-id="d9b93-409">The wildcard character `*` is allowed, and the double wildcard `**` implies a recursive folder search.</span></span> |
| <span data-ttu-id="d9b93-410">**buildAction**</span><span class="sxs-lookup"><span data-stu-id="d9b93-410">**buildAction**</span></span> | <span data-ttu-id="d9b93-411">生成操作，用于分配到 MSBuild 的内容项（如 `Content`、`None`、`Embedded Resource`、`Compile` 等）。默认值为 `Compile`。</span><span class="sxs-lookup"><span data-stu-id="d9b93-411">The build action to assign to the content item for MSBuild, such as `Content`, `None`, `Embedded Resource`, `Compile`, etc. The default is `Compile`.</span></span> |
| <span data-ttu-id="d9b93-412">**copyToOutput**</span><span class="sxs-lookup"><span data-stu-id="d9b93-412">**copyToOutput**</span></span> | <span data-ttu-id="d9b93-413">布尔值，该值指示是否将内容项复制到生成 （或发布） 输出文件夹。</span><span class="sxs-lookup"><span data-stu-id="d9b93-413">A Boolean indicating whether to copy content items to the build (or publish) output folder.</span></span> <span data-ttu-id="d9b93-414">默认值为 false。</span><span class="sxs-lookup"><span data-stu-id="d9b93-414">The default is false.</span></span> |
| <span data-ttu-id="d9b93-415">**flatten**</span><span class="sxs-lookup"><span data-stu-id="d9b93-415">**flatten**</span></span> | <span data-ttu-id="d9b93-416">一个布尔值，用于指示是将内容项复制到生成输出中的单个文件夹 (true)，还是保留包中的文件夹结构 (false)。</span><span class="sxs-lookup"><span data-stu-id="d9b93-416">A Boolean indicating whether to copy content items to a single folder in the build output (true), or to preserve the folder structure in the package (false).</span></span> <span data-ttu-id="d9b93-417">此标志仅在 copyToOutput 标志设置为 true 时才有效。</span><span class="sxs-lookup"><span data-stu-id="d9b93-417">This flag only works when copyToOutput flag is set to true.</span></span> <span data-ttu-id="d9b93-418">默认值为 false。</span><span class="sxs-lookup"><span data-stu-id="d9b93-418">The default is false.</span></span> |

<span data-ttu-id="d9b93-419">安装包时，NuGet 从上到下应用 `<contentFiles>` 的子元素。</span><span class="sxs-lookup"><span data-stu-id="d9b93-419">When installing a package, NuGet applies the child elements of `<contentFiles>` from top to bottom.</span></span> <span data-ttu-id="d9b93-420">如果多个条目与相同的文件匹配，那么应用全部条目。</span><span class="sxs-lookup"><span data-stu-id="d9b93-420">If multiple entries match the same file then all entries are applied.</span></span> <span data-ttu-id="d9b93-421">如果相同特性发生冲突，则最上面的条目将替代靠下的条目。</span><span class="sxs-lookup"><span data-stu-id="d9b93-421">The top-most entry overrides the lower entries if there is a conflict for the same attribute.</span></span>

#### <a name="package-folder-structure"></a><span data-ttu-id="d9b93-422">包文件夹结构</span><span class="sxs-lookup"><span data-stu-id="d9b93-422">Package folder structure</span></span>

<span data-ttu-id="d9b93-423">包项目应使用以下模式构建内容结构：</span><span class="sxs-lookup"><span data-stu-id="d9b93-423">The package project should structure content using the following pattern:</span></span>

    /contentFiles/{codeLanguage}/{TxM}/{any?}

- <span data-ttu-id="d9b93-424">`codeLanguages` 可以是 `cs`、`vb`、`fs`、`any` 或给定 `$(ProjectLanguage)` 的小写等效形式</span><span class="sxs-lookup"><span data-stu-id="d9b93-424">`codeLanguages` may be `cs`, `vb`, `fs`, `any`, or the lowercase equivalent of a given `$(ProjectLanguage)`</span></span>
- <span data-ttu-id="d9b93-425">`TxM` 是 NuGet 支持的任何合法目标框架名字对象（请参阅[目标框架](../reference/target-frameworks.md)）。</span><span class="sxs-lookup"><span data-stu-id="d9b93-425">`TxM` is any legal target framework moniker that NuGet supports (see [Target frameworks](../reference/target-frameworks.md)).</span></span>
- <span data-ttu-id="d9b93-426">任何文件夹结构都可以附加到此语法的末尾。</span><span class="sxs-lookup"><span data-stu-id="d9b93-426">Any folder structure may be appended to the end of this syntax.</span></span>

<span data-ttu-id="d9b93-427">例如：</span><span class="sxs-lookup"><span data-stu-id="d9b93-427">For example:</span></span>

    Language- and framework-agnostic:
        /contentFiles/any/any/config.xml

    net45 content for all languages
        /contentFiles/any/net45/config.xml

    C#-specific content for net45 and up
        /contentFiles/cs/net45/sample.cs

<span data-ttu-id="d9b93-428">空文件夹可以使用 `.` 来选择不提供特定语言和 TxM 组合的内容，例如：</span><span class="sxs-lookup"><span data-stu-id="d9b93-428">Empty folders can use `.` to opt out of providing content for certain combinations of language and TxM, for example:</span></span>

    /contentFiles/vb/any/code.vb
    /contentFiles/cs/any/.

#### <a name="example-contentfiles-section"></a><span data-ttu-id="d9b93-429">contentFiles 部分示例</span><span class="sxs-lookup"><span data-stu-id="d9b93-429">Example contentFiles section</span></span>

```xml
<?xml version="1.0" encoding="utf-8"?>
<package xmlns="http://schemas.microsoft.com/packaging/2010/07/nuspec.xsd">
    <metadata>
        ...
        <contentFiles>
            <!-- Embed image resources -->
            <files include="any/any/images/dnf.png" buildAction="EmbeddedResource" />
            <files include="any/any/images/ui.png" buildAction="EmbeddedResource" />

            <!-- Embed all image resources under contentFiles/cs/ -->
            <files include="cs/**/*.png" buildAction="EmbeddedResource" />

            <!-- Copy config.xml to the root of the output folder -->
            <files include="cs/uap/config/config.xml" buildAction="None" copyToOutput="true" flatten="true" />

            <!-- Copy run.cmd to the output folder and keep the directory structure -->
            <files include="cs/commands/run.cmd" buildAction="None" copyToOutput="true" flatten="false" />

            <!-- Include everything in the scripts folder except exe files -->
            <files include="cs/net45/scripts/*" exclude="**/*.exe"  buildAction="None" copyToOutput="true" />
        </contentFiles>
        </metadata>
</package>
```

## <a name="example-nuspec-files"></a><span data-ttu-id="d9b93-430">示例 nuspec 文件</span><span class="sxs-lookup"><span data-stu-id="d9b93-430">Example nuspec files</span></span>

<span data-ttu-id="d9b93-431">**未指定依赖项或文件的简单 `.nuspec`**</span><span class="sxs-lookup"><span data-stu-id="d9b93-431">**A simple `.nuspec` that does not specify dependencies or files**</span></span>

```xml
<?xml version="1.0" encoding="utf-8"?>
<package xmlns="http://schemas.microsoft.com/packaging/2010/07/nuspec.xsd">
    <metadata>
        <id>sample</id>
        <version>1.2.3</version>
        <authors>Kim Abercrombie, Franck Halmaert</authors>
        <description>Sample exists only to show a sample .nuspec file.</description>
        <language>en-US</language>
        <projectUrl>http://xunit.codeplex.com/</projectUrl>
        <license type="expression">MIT</license>
    </metadata>
</package>
```

<span data-ttu-id="d9b93-432">**具有依赖项的 `.nuspec`**</span><span class="sxs-lookup"><span data-stu-id="d9b93-432">**A `.nuspec` with dependencies**</span></span>

```xml
<?xml version="1.0" encoding="utf-8"?>
<package xmlns="http://schemas.microsoft.com/packaging/2010/07/nuspec.xsd">
    <metadata>
        <id>sample</id>
        <version>1.0.0</version>
        <authors>Microsoft</authors>
        <dependencies>
            <dependency id="another-package" version="3.0.0" />
            <dependency id="yet-another-package" version="1.0.0" />
        </dependencies>
    </metadata>
</package>
```

<span data-ttu-id="d9b93-433">**具有文件的 `.nuspec`**</span><span class="sxs-lookup"><span data-stu-id="d9b93-433">**A `.nuspec` with files**</span></span>

```xml
<?xml version="1.0"?>
<package xmlns="http://schemas.microsoft.com/packaging/2010/07/nuspec.xsd">
    <metadata>
        <id>routedebugger</id>
        <version>1.0.0</version>
        <authors>Jay Hamlin</authors>
        <requireLicenseAcceptance>false</requireLicenseAcceptance>
        <description>Route Debugger is a little utility I wrote...</description>
    </metadata>
    <files>
        <file src="bin\Debug\*.dll" target="lib" />
    </files>
</package>
```

<span data-ttu-id="d9b93-434">**具有 Framework 程序集的 `.nuspec`**</span><span class="sxs-lookup"><span data-stu-id="d9b93-434">**A `.nuspec` with framework assemblies**</span></span>

```xml
<?xml version="1.0"?>
<package xmlns="http://schemas.microsoft.com/packaging/2010/07/nuspec.xsd">
    <metadata>
        <id>PackageWithGacReferences</id>
        <version>1.0</version>
        <authors>Author here</authors>
        <requireLicenseAcceptance>false</requireLicenseAcceptance>
        <description>
            A package that has framework assemblyReferences depending
            on the target framework.
        </description>
        <frameworkAssemblies>
            <frameworkAssembly assemblyName="System.Web" targetFramework="net40" />
            <frameworkAssembly assemblyName="System.Net" targetFramework="net40-client, net40" />
            <frameworkAssembly assemblyName="Microsoft.Devices.Sensors" targetFramework="sl4-wp" />
            <frameworkAssembly assemblyName="System.Json" targetFramework="sl3" />
        </frameworkAssemblies>
    </metadata>
</package>
```

<span data-ttu-id="d9b93-435">在此示例中，为特定的项目目标安装了以下内容：</span><span class="sxs-lookup"><span data-stu-id="d9b93-435">In this example, the following are installed for specific project targets:</span></span>

- <span data-ttu-id="d9b93-436">.NET4 -> `System.Web``System.Net`</span><span class="sxs-lookup"><span data-stu-id="d9b93-436">.NET4 -> `System.Web`, `System.Net`</span></span>
- <span data-ttu-id="d9b93-437">.NET4 Client Profile -> `System.Net`</span><span class="sxs-lookup"><span data-stu-id="d9b93-437">.NET4 Client Profile -> `System.Net`</span></span>
- <span data-ttu-id="d9b93-438">Silverlight 3 -> `System.Json`</span><span class="sxs-lookup"><span data-stu-id="d9b93-438">Silverlight 3 -> `System.Json`</span></span>
- <span data-ttu-id="d9b93-439">WindowsPhone -> `Microsoft.Devices.Sensors`</span><span class="sxs-lookup"><span data-stu-id="d9b93-439">WindowsPhone -> `Microsoft.Devices.Sensors`</span></span>
