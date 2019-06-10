---
title: 适用于 NuGet 的.nuspec 文件引用
description: .nuspec 文件包含生成包时使用的，并向包使用者提供信息的包元数据。
author: karann-msft
ms.author: karann
ms.date: 05/24/2019
ms.topic: reference
ms.reviewer: anangaur
ms.openlocfilehash: 6c545ddeddb0c5909f57e879912eaeed744e42d5
ms.sourcegitcommit: b8c63744252a5a37a2843f6bc1d5917496ee40dd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/07/2019
ms.locfileid: "66812924"
---
# <a name="nuspec-reference"></a><span data-ttu-id="ae2a5-103">.nuspec 引用</span><span class="sxs-lookup"><span data-stu-id="ae2a5-103">.nuspec reference</span></span>

<span data-ttu-id="ae2a5-104">`.nuspec` 文件是包含包元数据的 XML 清单。</span><span class="sxs-lookup"><span data-stu-id="ae2a5-104">A `.nuspec` file is an XML manifest that contains package metadata.</span></span> <span data-ttu-id="ae2a5-105">此清单同时用于生成包以及为使用者提供信息。</span><span class="sxs-lookup"><span data-stu-id="ae2a5-105">This manifest is used both to build the package and to provide information to consumers.</span></span> <span data-ttu-id="ae2a5-106">清单始终包含在包中。</span><span class="sxs-lookup"><span data-stu-id="ae2a5-106">The manifest is always included in a package.</span></span>

<span data-ttu-id="ae2a5-107">本主题内容：</span><span class="sxs-lookup"><span data-stu-id="ae2a5-107">In this topic:</span></span>

- [<span data-ttu-id="ae2a5-108">常规形式和架构</span><span class="sxs-lookup"><span data-stu-id="ae2a5-108">General form and schema</span></span>](#general-form-and-schema)
- <span data-ttu-id="ae2a5-109">[替换令牌](#replacement-tokens)（用于 Visual Studio 项目时）</span><span class="sxs-lookup"><span data-stu-id="ae2a5-109">[Replacement tokens](#replacement-tokens) (when used with a Visual Studio project)</span></span>
- [<span data-ttu-id="ae2a5-110">依赖项</span><span class="sxs-lookup"><span data-stu-id="ae2a5-110">Dependencies</span></span>](#dependencies)
- [<span data-ttu-id="ae2a5-111">显式程序集引用</span><span class="sxs-lookup"><span data-stu-id="ae2a5-111">Explicit assembly references</span></span>](#explicit-assembly-references)
- [<span data-ttu-id="ae2a5-112">Framework 程序集引用</span><span class="sxs-lookup"><span data-stu-id="ae2a5-112">Framework assembly references</span></span>](#framework-assembly-references)
- [<span data-ttu-id="ae2a5-113">包括程序集文件</span><span class="sxs-lookup"><span data-stu-id="ae2a5-113">Including assembly files</span></span>](#including-assembly-files)
- [<span data-ttu-id="ae2a5-114">包括内容文件</span><span class="sxs-lookup"><span data-stu-id="ae2a5-114">Including content files</span></span>](#including-content-files)
- [<span data-ttu-id="ae2a5-115">示例 nuspec 文件</span><span class="sxs-lookup"><span data-stu-id="ae2a5-115">Example nuspec files</span></span>](#example-nuspec-files)

## <a name="project-type-compatibility"></a><span data-ttu-id="ae2a5-116">项目类型兼容性</span><span class="sxs-lookup"><span data-stu-id="ae2a5-116">Project type compatibility</span></span>

- <span data-ttu-id="ae2a5-117">使用`.nuspec`与`nuget.exe pack`非 SDK 样式项目使用`packages.config`。</span><span class="sxs-lookup"><span data-stu-id="ae2a5-117">Use `.nuspec` with `nuget.exe pack` for non-SDK-style projects that use `packages.config`.</span></span>

- <span data-ttu-id="ae2a5-118">一个`.nuspec`文件不需要为 SDK 样式项目创建包 (.NET Core 和.NET Standard 项目，使用[SDK 属性](/dotnet/core/tools/csproj#additions))。</span><span class="sxs-lookup"><span data-stu-id="ae2a5-118">A `.nuspec` file is not required to create packages for SDK-style projects (.NET Core and .NET Standard projects that use the [SDK attribute](/dotnet/core/tools/csproj#additions)).</span></span> <span data-ttu-id="ae2a5-119">(请注意，`.nuspec`创建包时生成。)</span><span class="sxs-lookup"><span data-stu-id="ae2a5-119">(Note that a `.nuspec` is generated when you create the package.)</span></span>

   <span data-ttu-id="ae2a5-120">如果要创建包使用`dotnet.exe pack`或`msbuild pack target`，我们建议您[包含的所有属性](../reference/msbuild-targets.md#pack-target)是通常在`.nuspec`改为文件在项目文件中。</span><span class="sxs-lookup"><span data-stu-id="ae2a5-120">If you are creating a package using `dotnet.exe pack` or `msbuild pack target`, we recommend that you [include all the properties](../reference/msbuild-targets.md#pack-target) that are usually in the `.nuspec` file in the project file instead.</span></span> <span data-ttu-id="ae2a5-121">但是，你也可以选择向[使用`.nuspec`文件打包使用`dotnet.exe`或`msbuild pack target` ](../reference/msbuild-targets.md#packing-using-a-nuspec)。</span><span class="sxs-lookup"><span data-stu-id="ae2a5-121">However, you can instead choose to [use a `.nuspec` file to pack using `dotnet.exe` or `msbuild pack target`](../reference/msbuild-targets.md#packing-using-a-nuspec).</span></span>

- <span data-ttu-id="ae2a5-122">有关从迁移的项目`packages.config`到[PackageReference](../consume-packages/package-references-in-project-files.md)、`.nuspec`文件不需要创建包。</span><span class="sxs-lookup"><span data-stu-id="ae2a5-122">For projects migrated from `packages.config` to [PackageReference](../consume-packages/package-references-in-project-files.md), a `.nuspec` file is not required to create the package.</span></span> <span data-ttu-id="ae2a5-123">请改用[msbuild 包](../reference/migrate-packages-config-to-package-reference.md#create-a-package-after-migration)。</span><span class="sxs-lookup"><span data-stu-id="ae2a5-123">Instead, use [msbuild pack](../reference/migrate-packages-config-to-package-reference.md#create-a-package-after-migration).</span></span>

## <a name="general-form-and-schema"></a><span data-ttu-id="ae2a5-124">常规形式和架构</span><span class="sxs-lookup"><span data-stu-id="ae2a5-124">General form and schema</span></span>

<span data-ttu-id="ae2a5-125">当前 `nuspec.xsd` 架构文件可在 [NuGet GitHub 存储库](https://github.com/NuGet/NuGet.Client/blob/dev/src/NuGet.Core/NuGet.Packaging/compiler/resources/nuspec.xsd)中找到。</span><span class="sxs-lookup"><span data-stu-id="ae2a5-125">The current `nuspec.xsd` schema file can be found in the [NuGet GitHub repository](https://github.com/NuGet/NuGet.Client/blob/dev/src/NuGet.Core/NuGet.Packaging/compiler/resources/nuspec.xsd).</span></span>

<span data-ttu-id="ae2a5-126">在此构架中，`.nuspec` 文件具有以下常规形式：</span><span class="sxs-lookup"><span data-stu-id="ae2a5-126">Within this schema, a `.nuspec` file has the following general form:</span></span>

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

<span data-ttu-id="ae2a5-127">有关架构的清晰可视表示形式，请在 Visual Studio 中以“设计”模式打开架构文件，然后单击“XML 架构资源管理器”链接  。</span><span class="sxs-lookup"><span data-stu-id="ae2a5-127">For a clear visual representation of the schema, open the schema file in Visual Studio in Design mode and click on the **XML Schema Explorer** link.</span></span> <span data-ttu-id="ae2a5-128">或者，将该文件作为代码打开，在编辑器中右键单击，然后选择“显示 XML 架构资源管理器”  。</span><span class="sxs-lookup"><span data-stu-id="ae2a5-128">Alternately, open the file as code, right-click in the editor, and select **Show XML Schema Explorer**.</span></span> <span data-ttu-id="ae2a5-129">无论哪种方式，都会获得如下所示的视图（大多数部件都处于扩展状态）：</span><span class="sxs-lookup"><span data-stu-id="ae2a5-129">Either way you get a view like the one below (when mostly expanded):</span></span>

![nuspec.xsd 打开时的 Visual Studio 架构资源管理器](media/SchemaExplorer.png)

### <a name="required-metadata-elements"></a><span data-ttu-id="ae2a5-131">所需的元数据元素</span><span class="sxs-lookup"><span data-stu-id="ae2a5-131">Required metadata elements</span></span>

<span data-ttu-id="ae2a5-132">尽管以下元素是包的最低要求，但应该考虑添加[可选元数据元素](#optional-metadata-elements)以改善开发人员对包的整体体验。</span><span class="sxs-lookup"><span data-stu-id="ae2a5-132">Although the following elements are the minimum requirements for a package, you should consider adding the [optional metadata elements](#optional-metadata-elements) to improve the overall experience developers have with your package.</span></span> 

<span data-ttu-id="ae2a5-133">这些元素必须出现在 `<metadata>` 元素中。</span><span class="sxs-lookup"><span data-stu-id="ae2a5-133">These elements must appear within a `<metadata>` element.</span></span>

#### <a name="id"></a><span data-ttu-id="ae2a5-134">id</span><span class="sxs-lookup"><span data-stu-id="ae2a5-134">id</span></span> 
<span data-ttu-id="ae2a5-135">不区分大小写的包标识符，在 nuget.org 或包驻留的任意库中必须是唯一的。</span><span class="sxs-lookup"><span data-stu-id="ae2a5-135">The case-insensitive package identifier, which must be unique across nuget.org or whatever gallery the package resides in.</span></span> <span data-ttu-id="ae2a5-136">ID 不得包含空格或对 URL 无效的字符，通常遵循 .NET 命名空间规则。</span><span class="sxs-lookup"><span data-stu-id="ae2a5-136">IDs may not contain spaces or characters that are not valid for a URL, and generally follow .NET namespace rules.</span></span> <span data-ttu-id="ae2a5-137">有关指南，请参阅[选择唯一的包标识符](../create-packages/creating-a-package.md#choosing-a-unique-package-identifier-and-setting-the-version-number)。</span><span class="sxs-lookup"><span data-stu-id="ae2a5-137">See [Choosing a unique package identifier](../create-packages/creating-a-package.md#choosing-a-unique-package-identifier-and-setting-the-version-number) for guidance.</span></span>
#### <a name="version"></a><span data-ttu-id="ae2a5-138">version</span><span class="sxs-lookup"><span data-stu-id="ae2a5-138">version</span></span>
<span data-ttu-id="ae2a5-139">遵循 major.minor.patch 模式的包版本  。</span><span class="sxs-lookup"><span data-stu-id="ae2a5-139">The version of the package, following the *major.minor.patch* pattern.</span></span> <span data-ttu-id="ae2a5-140">版本号可能包括预发布后缀，如[包版本控制](../reference/package-versioning.md#pre-release-versions)中所述。</span><span class="sxs-lookup"><span data-stu-id="ae2a5-140">Version numbers may include a pre-release suffix as described in [Package versioning](../reference/package-versioning.md#pre-release-versions).</span></span> 
#### <a name="description"></a><span data-ttu-id="ae2a5-141">说明</span><span class="sxs-lookup"><span data-stu-id="ae2a5-141">description</span></span>
<span data-ttu-id="ae2a5-142">用于 UI 显示的包的详细说明。</span><span class="sxs-lookup"><span data-stu-id="ae2a5-142">A long description of the package for UI display.</span></span> 
#### <a name="authors"></a><span data-ttu-id="ae2a5-143">作者</span><span class="sxs-lookup"><span data-stu-id="ae2a5-143">authors</span></span>
<span data-ttu-id="ae2a5-144">包创建者的逗号分隔列表，与 nuget.org 上的配置文件名称一致。这些信息显示在 nuget.org 上的 NuGet 库中，并用于交叉引用同一作者的包。</span><span class="sxs-lookup"><span data-stu-id="ae2a5-144">A comma-separated list of packages authors, matching the profile names on nuget.org. These are displayed in the NuGet Gallery on nuget.org and are used to cross-reference packages by the same authors.</span></span> 

### <a name="optional-metadata-elements"></a><span data-ttu-id="ae2a5-145">可选元数据元素</span><span class="sxs-lookup"><span data-stu-id="ae2a5-145">Optional metadata elements</span></span>

#### <a name="title"></a><span data-ttu-id="ae2a5-146">标题</span><span class="sxs-lookup"><span data-stu-id="ae2a5-146">title</span></span>
<span data-ttu-id="ae2a5-147">明了易用的包标题，通常用在 UI 显示中，如 nuget.org 上和 Visual Studio 中包管理器上的那样。</span><span class="sxs-lookup"><span data-stu-id="ae2a5-147">A human-friendly title of the package, typically used in UI displays as on nuget.org and the Package Manager in Visual Studio.</span></span> <span data-ttu-id="ae2a5-148">如果未指定，则使用包 ID。</span><span class="sxs-lookup"><span data-stu-id="ae2a5-148">If not specified, the package ID is used.</span></span> 
#### <a name="owners"></a><span data-ttu-id="ae2a5-149">所有者</span><span class="sxs-lookup"><span data-stu-id="ae2a5-149">owners</span></span>
<span data-ttu-id="ae2a5-150">使用 nuget.org 上的配置文件名称的包创建者的逗号分隔列表。这通常和 `authors` 中的列表相同，将包上传到 nuget.org 时被忽略。请参阅[在 nuget.org 上管理包所有者](../create-packages/publish-a-package.md#managing-package-owners-on-nugetorg)。</span><span class="sxs-lookup"><span data-stu-id="ae2a5-150">A comma-separated list of the package creators using profile names on nuget.org. This is often the same list as in `authors`, and is ignored when uploading the package to nuget.org. See [Managing package owners on nuget.org](../create-packages/publish-a-package.md#managing-package-owners-on-nugetorg).</span></span> 
#### <a name="projecturl"></a><span data-ttu-id="ae2a5-151">projectUrl</span><span class="sxs-lookup"><span data-stu-id="ae2a5-151">projectUrl</span></span>
<span data-ttu-id="ae2a5-152">包的主页 URL，通常显示在 UI 中以及 nuget.org 中。</span><span class="sxs-lookup"><span data-stu-id="ae2a5-152">A URL for the package's home page, often shown in UI displays as well as nuget.org.</span></span> 
#### <a name="licenseurl"></a><span data-ttu-id="ae2a5-153">licenseUrl</span><span class="sxs-lookup"><span data-stu-id="ae2a5-153">licenseUrl</span></span>
> [!Important]
> <span data-ttu-id="ae2a5-154">将弃用 licenseUrl。</span><span class="sxs-lookup"><span data-stu-id="ae2a5-154">licenseUrl is being deprecated.</span></span> <span data-ttu-id="ae2a5-155">改为使用许可证。</span><span class="sxs-lookup"><span data-stu-id="ae2a5-155">Use license instead.</span></span>

<span data-ttu-id="ae2a5-156">包的许可证 URL，通常显示在 UI 和 nuget.org 中。</span><span class="sxs-lookup"><span data-stu-id="ae2a5-156">A URL for the package's license, often shown in UI displays as well as nuget.org.</span></span>
#### <a name="license"></a><span data-ttu-id="ae2a5-157">许可证</span><span class="sxs-lookup"><span data-stu-id="ae2a5-157">license</span></span>
<span data-ttu-id="ae2a5-158">SPDX 许可证表达式或包中许可证文件的路径，通常显示在 UI 和 nuget.org 中。如果许可包在常见如 BSD 2 子句或 MIT 许可证下的使用关联的 SPDX 许可证标识符。</span><span class="sxs-lookup"><span data-stu-id="ae2a5-158">An SPDX license expression or path to a license file within the package, often shown in UI displays as well as nuget.org. If you’re licensing the package under a common license such as BSD-2-Clause or MIT, use the associated SPDX license identifier.</span></span><br><span data-ttu-id="ae2a5-159">例如： `<license type="expression">MIT</license>`</span><span class="sxs-lookup"><span data-stu-id="ae2a5-159">For example: `<license type="expression">MIT</license>`</span></span>

<span data-ttu-id="ae2a5-160">下面是 [SPDX 许可证标识符](https://spdx.org/licenses/)的完整列表。</span><span class="sxs-lookup"><span data-stu-id="ae2a5-160">Here is the complete list of [SPDX license identifiers](https://spdx.org/licenses/).</span></span> <span data-ttu-id="ae2a5-161">NuGet.org 在使用许可证类型表达式时只接受 OSI 或 FSF 批准的许可证。</span><span class="sxs-lookup"><span data-stu-id="ae2a5-161">NuGet.org accepts only OSI or FSF approved licenses when using license type expression.</span></span>

<span data-ttu-id="ae2a5-162">如果您的包常见的多个许可证的许可，则可以指定复合许可证 using [SPDX 表达式语法版本 2.0](https://spdx.org/spdx-specification-21-web-version#h.jxpfx0ykyb60)。</span><span class="sxs-lookup"><span data-stu-id="ae2a5-162">If your package is licensed under multiple common licenses, you can specify a composite license using the [SPDX expression syntax version 2.0](https://spdx.org/spdx-specification-21-web-version#h.jxpfx0ykyb60).</span></span><br><span data-ttu-id="ae2a5-163">例如： `<license type="expression">BSD-2-Clause OR MIT</license>`</span><span class="sxs-lookup"><span data-stu-id="ae2a5-163">For example: `<license type="expression">BSD-2-Clause OR MIT</license>`</span></span>

<span data-ttu-id="ae2a5-164">如果正在使用许可证尚未分配 SPDX 标识符，或者它是自定义许可证，你可以将打包文件 (仅`.txt`或`.md`) 使用的许可证文本。</span><span class="sxs-lookup"><span data-stu-id="ae2a5-164">If you are using a license that hasn’t been assigned an SPDX identifier, or it is a custom license, you can package a file (only `.txt` or `.md`) with the license text.</span></span> <span data-ttu-id="ae2a5-165">例如：</span><span class="sxs-lookup"><span data-stu-id="ae2a5-165">For example:</span></span>
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

<span data-ttu-id="ae2a5-166">为 MSBuild 等效的看一看[装箱许可证表达式或许可证文件](msbuild-targets.md#packing-a-license-expression-or-a-license-file)。</span><span class="sxs-lookup"><span data-stu-id="ae2a5-166">For the MSBuild equivalent, take a look at [Packing a license expression or a license file](msbuild-targets.md#packing-a-license-expression-or-a-license-file).</span></span>

<span data-ttu-id="ae2a5-167">NuGet 的许可证表达式的确切语法是下面中所述[ABNF](https://tools.ietf.org/html/rfc5234)。</span><span class="sxs-lookup"><span data-stu-id="ae2a5-167">The exact syntax of NuGet's license expressions is described below in [ABNF](https://tools.ietf.org/html/rfc5234).</span></span>
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

#### <a name="iconurl"></a><span data-ttu-id="ae2a5-168">iconUrl</span><span class="sxs-lookup"><span data-stu-id="ae2a5-168">iconUrl</span></span>
<span data-ttu-id="ae2a5-169">64x64 透明背景图像的 URL，用作 UI 显示中包的图标。</span><span class="sxs-lookup"><span data-stu-id="ae2a5-169">A URL for a 64x64 image with transparency background to use as the icon for the package in UI display.</span></span> <span data-ttu-id="ae2a5-170">请确保此元素包含直接图像 URL，而不是包含图像的网页的 URL  。</span><span class="sxs-lookup"><span data-stu-id="ae2a5-170">Be sure this element contains the *direct image URL* and not the URL of a web page containing the image.</span></span> <span data-ttu-id="ae2a5-171">例如，若要使用 GitHub 中的图像，可使用原始文件 URL，如<em>https://github.com/\<username\>/\<repository\>/raw/\<branch\>/\<logo.png\></em>。</span><span class="sxs-lookup"><span data-stu-id="ae2a5-171">For example, to use an image from GitHub, use the raw file URL like <em>https://github.com/\<username\>/\<repository\>/raw/\<branch\>/\<logo.png\></em>.</span></span> 

#### <a name="requirelicenseacceptance"></a><span data-ttu-id="ae2a5-172">requireLicenseAcceptance</span><span class="sxs-lookup"><span data-stu-id="ae2a5-172">requireLicenseAcceptance</span></span>
<span data-ttu-id="ae2a5-173">一个布尔值，用于指定客户端是否必须提示使用者接受包许可证后才可安装包。</span><span class="sxs-lookup"><span data-stu-id="ae2a5-173">A Boolean value specifying whether the client must prompt the consumer to accept the package license before installing the package.</span></span>
#### <a name="developmentdependency"></a><span data-ttu-id="ae2a5-174">developmentDependency</span><span class="sxs-lookup"><span data-stu-id="ae2a5-174">developmentDependency</span></span>
<span data-ttu-id="ae2a5-175">(2.8+) 一个布尔值，用于指定包是否被标记为仅开发依赖项，从而防止包作为依赖项包含到其他包中  。</span><span class="sxs-lookup"><span data-stu-id="ae2a5-175">*(2.8+)* A Boolean value specifying whether the package is be marked as a development-only-dependency, which prevents the package from being included as a dependency in other packages.</span></span> <span data-ttu-id="ae2a5-176">使用 PackageReference (NuGet 4.8 +)，此标志也意味着它将从编译排除编译时资产。</span><span class="sxs-lookup"><span data-stu-id="ae2a5-176">With PackageReference (NuGet 4.8+), this flag also means that it will exclude compile-time assets from compilation.</span></span> <span data-ttu-id="ae2a5-177">请参阅[DevelopmentDependency 支持 PackageReference](https://github.com/NuGet/Home/wiki/DevelopmentDependency-support-for-PackageReference)</span><span class="sxs-lookup"><span data-stu-id="ae2a5-177">See [DevelopmentDependency support for PackageReference](https://github.com/NuGet/Home/wiki/DevelopmentDependency-support-for-PackageReference)</span></span>
#### <a name="summary"></a><span data-ttu-id="ae2a5-178">摘要</span><span class="sxs-lookup"><span data-stu-id="ae2a5-178">summary</span></span>
<span data-ttu-id="ae2a5-179">用于 UI 显示的包的简要说明。</span><span class="sxs-lookup"><span data-stu-id="ae2a5-179">A short description of the package for UI display.</span></span> <span data-ttu-id="ae2a5-180">如果省略，则使用 `description` 的截断版本。</span><span class="sxs-lookup"><span data-stu-id="ae2a5-180">If omitted, a truncated version of `description` is used.</span></span>
#### <a name="releasenotes"></a><span data-ttu-id="ae2a5-181">releaseNotes</span><span class="sxs-lookup"><span data-stu-id="ae2a5-181">releaseNotes</span></span>
<span data-ttu-id="ae2a5-182">(1.5+) 此版本包中所作更改的说明，通常代替包说明用在 UI 中，如 Visual Studio 包管理器的“更新”选项卡   。</span><span class="sxs-lookup"><span data-stu-id="ae2a5-182">*(1.5+)* A description of the changes made in this release of the package, often used in UI like the **Updates** tab of the Visual Studio Package Manager in place of the package description.</span></span>
#### <a name="copyright"></a><span data-ttu-id="ae2a5-183">copyright</span><span class="sxs-lookup"><span data-stu-id="ae2a5-183">copyright</span></span>
<span data-ttu-id="ae2a5-184">(1.5+) 包的版权详细信息  。</span><span class="sxs-lookup"><span data-stu-id="ae2a5-184">*(1.5+)* Copyright details for the package.</span></span>
#### <a name="language"></a><span data-ttu-id="ae2a5-185">语言</span><span class="sxs-lookup"><span data-stu-id="ae2a5-185">language</span></span>
<span data-ttu-id="ae2a5-186">包的区域设置 ID。</span><span class="sxs-lookup"><span data-stu-id="ae2a5-186">The locale ID for the package.</span></span> <span data-ttu-id="ae2a5-187">请参阅[创建本地化包](../create-packages/creating-localized-packages.md)。</span><span class="sxs-lookup"><span data-stu-id="ae2a5-187">See [Creating localized packages](../create-packages/creating-localized-packages.md).</span></span>
#### <a name="tags"></a><span data-ttu-id="ae2a5-188">标记</span><span class="sxs-lookup"><span data-stu-id="ae2a5-188">tags</span></span>
<span data-ttu-id="ae2a5-189">以空格分隔的标记和关键字列表，描述包并通过搜索和筛选辅助包的可发现性。</span><span class="sxs-lookup"><span data-stu-id="ae2a5-189">A space-delimited list of tags and keywords that describe the package and aid discoverability of packages through search and filtering.</span></span> 
#### <a name="serviceable"></a><span data-ttu-id="ae2a5-190">可维护性</span><span class="sxs-lookup"><span data-stu-id="ae2a5-190">serviceable</span></span> 
<span data-ttu-id="ae2a5-191">(3.3+) 仅限内部使用  。</span><span class="sxs-lookup"><span data-stu-id="ae2a5-191">*(3.3+)* For internal NuGet use only.</span></span>
#### <a name="repository"></a><span data-ttu-id="ae2a5-192">储存库</span><span class="sxs-lookup"><span data-stu-id="ae2a5-192">repository</span></span>
<span data-ttu-id="ae2a5-193">存储库的元数据，包括四个可选属性：*类型*并*url* *（4.0 +）* ，以及*分支*和*提交* *（4.6 +）* 。</span><span class="sxs-lookup"><span data-stu-id="ae2a5-193">Repository metadata, consisting of four optional attributes: *type* and *url* *(4.0+)*, and *branch* and *commit* *(4.6+)*.</span></span> <span data-ttu-id="ae2a5-194">这些特性，你可以将.nupkg 映射到存储库可能会获取与生成它，作为单独的分支或包生成的提交进行了详细说明。</span><span class="sxs-lookup"><span data-stu-id="ae2a5-194">These attributes allow you to map the .nupkg to the repository that built it, with the potential to get as detailed as the individual branch or commit that built the package.</span></span> <span data-ttu-id="ae2a5-195">这应该是版本控制软件可以直接调用的公开发布 url。</span><span class="sxs-lookup"><span data-stu-id="ae2a5-195">This should be a publicly available url that can be invoked directly by a version control software.</span></span> <span data-ttu-id="ae2a5-196">它不应为 html 页，因为这意味着计算机。</span><span class="sxs-lookup"><span data-stu-id="ae2a5-196">It should not be an html page as this is meant for the computer.</span></span> <span data-ttu-id="ae2a5-197">对于链接到项目页，使用`projectUrl`字段，而是。</span><span class="sxs-lookup"><span data-stu-id="ae2a5-197">For linking to project page, use the `projectUrl` field, instead.</span></span>

#### <a name="minclientversion"></a><span data-ttu-id="ae2a5-198">minClientVersion</span><span class="sxs-lookup"><span data-stu-id="ae2a5-198">minClientVersion</span></span>
<span data-ttu-id="ae2a5-199">指定可安装此包的最低 NuGet 客户端版本，并由 nuget.exe 和 Visual Studio 程序包管理器强制实施。</span><span class="sxs-lookup"><span data-stu-id="ae2a5-199">Specifies the minimum version of the NuGet client that can install this package, enforced by nuget.exe and the Visual Studio Package Manager.</span></span> <span data-ttu-id="ae2a5-200">只要包依赖于特定 NuGet 客户端版本中添加的 `.nuspec` 文件的特定功能，就会使用此功能。</span><span class="sxs-lookup"><span data-stu-id="ae2a5-200">This is used whenever the package depends on specific features of the `.nuspec` file that were added in a particular version of the NuGet client.</span></span> <span data-ttu-id="ae2a5-201">例如，使用 `developmentDependency` 特性的包应为 `minClientVersion` 指定“2.8”。</span><span class="sxs-lookup"><span data-stu-id="ae2a5-201">For example, a package using the `developmentDependency` attribute should specify "2.8" for `minClientVersion`.</span></span> <span data-ttu-id="ae2a5-202">同样，使用 `contentFiles` 元素（请参阅下一部分）的包应将 `minClientVersion` 设置为“3.3”。</span><span class="sxs-lookup"><span data-stu-id="ae2a5-202">Similarly, a package using the `contentFiles` element (see the next section) should set `minClientVersion` to "3.3".</span></span> <span data-ttu-id="ae2a5-203">另请注意，早于 2.5 的 NuGet 客户端无法识别此标记，所以无论 `minClientVersion` 包含什么内容，它们总是拒绝安装该包  。</span><span class="sxs-lookup"><span data-stu-id="ae2a5-203">Note also that because NuGet clients prior to 2.5 do not recognize this flag, they *always* refuse to install the package no matter what `minClientVersion` contains.</span></span>

#### <a name="collection-elements"></a><span data-ttu-id="ae2a5-204">集合元素</span><span class="sxs-lookup"><span data-stu-id="ae2a5-204">Collection elements</span></span>

#### <a name="packagetypes"></a><span data-ttu-id="ae2a5-205">packageTypes</span><span class="sxs-lookup"><span data-stu-id="ae2a5-205">packageTypes</span></span>
<span data-ttu-id="ae2a5-206">*(3.5+)* 如果不是传统的依赖项包，则为指定包类型的包括零个或多个 `<packageType>` 元素的集合。</span><span class="sxs-lookup"><span data-stu-id="ae2a5-206">*(3.5+)* A collection of zero or more `<packageType>` elements specifying the type of the package if other than a traditional dependency package.</span></span> <span data-ttu-id="ae2a5-207">每个 packageType 都具有 name 和 version 特性   。</span><span class="sxs-lookup"><span data-stu-id="ae2a5-207">Each packageType has attributes of *name* and *version*.</span></span> <span data-ttu-id="ae2a5-208">请参阅[设置包类型](../create-packages/creating-a-package.md#setting-a-package-type)。</span><span class="sxs-lookup"><span data-stu-id="ae2a5-208">See [Setting a package type](../create-packages/creating-a-package.md#setting-a-package-type).</span></span>
#### <a name="dependencies"></a><span data-ttu-id="ae2a5-209">依赖项</span><span class="sxs-lookup"><span data-stu-id="ae2a5-209">dependencies</span></span>
<span data-ttu-id="ae2a5-210">零个或多个 `<dependency>` 元素的集合，用来指定包的依赖项。</span><span class="sxs-lookup"><span data-stu-id="ae2a5-210">A collection of zero or more `<dependency>` elements specifying the dependencies for the package.</span></span> <span data-ttu-id="ae2a5-211">每个 dependency 都具有 id、version、include (3.x+) 和 exclude (3.x+) 特性     。</span><span class="sxs-lookup"><span data-stu-id="ae2a5-211">Each dependency has attributes of *id*, *version*, *include* (3.x+), and *exclude* (3.x+).</span></span> <span data-ttu-id="ae2a5-212">请参阅下面的[依赖项](#dependencies-element)。</span><span class="sxs-lookup"><span data-stu-id="ae2a5-212">See [Dependencies](#dependencies-element) below.</span></span>
#### <a name="frameworkassemblies"></a><span data-ttu-id="ae2a5-213">frameworkAssemblies</span><span class="sxs-lookup"><span data-stu-id="ae2a5-213">frameworkAssemblies</span></span>
<span data-ttu-id="ae2a5-214">(1.2+) 零个或多个 `<frameworkAssembly>` 元素的集合，用来标识此包要求的 .NET Framework 程序集引用，从而确保引用添加到使用该包的项目  。</span><span class="sxs-lookup"><span data-stu-id="ae2a5-214">*(1.2+)* A collection of zero or more `<frameworkAssembly>` elements identifying .NET Framework assembly references that this package requires, which ensures that references are added to projects consuming the package.</span></span> <span data-ttu-id="ae2a5-215">每个 frameworkAssembly 都具有 assemblyName 和 targetFramework 特性   。</span><span class="sxs-lookup"><span data-stu-id="ae2a5-215">Each frameworkAssembly has *assemblyName* and *targetFramework* attributes.</span></span> <span data-ttu-id="ae2a5-216">请参阅下面的[指定 Framework 程序集引用 GAC](#specifying-framework-assembly-references-gac)。</span><span class="sxs-lookup"><span data-stu-id="ae2a5-216">See [Specifying framework assembly references GAC](#specifying-framework-assembly-references-gac) below.</span></span> |
#### <a name="references"></a><span data-ttu-id="ae2a5-217">引用</span><span class="sxs-lookup"><span data-stu-id="ae2a5-217">references</span></span>
<span data-ttu-id="ae2a5-218">(1.5+) 零个或多个 `<reference>` 元素的集合，用来指定包的 `lib` 文件夹中添加为项目引用的程序集  。</span><span class="sxs-lookup"><span data-stu-id="ae2a5-218">*(1.5+)* A collection of zero or more `<reference>` elements naming assemblies in the package's `lib` folder that are added as project references.</span></span> <span data-ttu-id="ae2a5-219">每个 reference 都具有 file 特性  。</span><span class="sxs-lookup"><span data-stu-id="ae2a5-219">Each reference has a *file* attribute.</span></span> <span data-ttu-id="ae2a5-220">`<references>` 也可包含具有 targetFramework 特性的 `<group>` 元素，然后包含 `<reference>` 元素  。</span><span class="sxs-lookup"><span data-stu-id="ae2a5-220">`<references>` can also contain a `<group>` element with a *targetFramework* attribute, that then contains `<reference>` elements.</span></span> <span data-ttu-id="ae2a5-221">如果省略，则包含 `lib` 中的全部引用。</span><span class="sxs-lookup"><span data-stu-id="ae2a5-221">If omitted, all references in `lib` are included.</span></span> <span data-ttu-id="ae2a5-222">请参阅下面的[指定显式程序集引用](#specifying-explicit-assembly-references)。</span><span class="sxs-lookup"><span data-stu-id="ae2a5-222">See [Specifying explicit assembly references](#specifying-explicit-assembly-references) below.</span></span>
#### <a name="contentfiles"></a><span data-ttu-id="ae2a5-223">contentFiles</span><span class="sxs-lookup"><span data-stu-id="ae2a5-223">contentFiles</span></span>
<span data-ttu-id="ae2a5-224">(3.3+) `<files>` 元素的集合，用来标识包含在使用项目中的内容文件  。</span><span class="sxs-lookup"><span data-stu-id="ae2a5-224">*(3.3+)* A collection of `<files>` elements that identify content files to include in the consuming project.</span></span> <span data-ttu-id="ae2a5-225">这些文件用一组特性指定，用于描述如何在项目系统中使用这些文件。</span><span class="sxs-lookup"><span data-stu-id="ae2a5-225">These files are specified with a set of attributes that describe how they should be used within the project system.</span></span> <span data-ttu-id="ae2a5-226">请参阅下面的[指定包含在包中的文件](#specifying-files-to-include-in-the-package)。</span><span class="sxs-lookup"><span data-stu-id="ae2a5-226">See [Specifying files to include in the package](#specifying-files-to-include-in-the-package) below.</span></span>
#### <a name="files"></a><span data-ttu-id="ae2a5-227">文件</span><span class="sxs-lookup"><span data-stu-id="ae2a5-227">files</span></span> 
<span data-ttu-id="ae2a5-228">`<package>`节点可能包含`<files>`节点的同级`<metadata>`，和一个`<contentFiles>`下的子`<metadata>`，以指定要在包中包含的程序集和内容文件。</span><span class="sxs-lookup"><span data-stu-id="ae2a5-228">The `<package>` node may contain a `<files>` node as a sibling to `<metadata>`, and a `<contentFiles>` child under `<metadata>`, to specify which assembly and content files to include in the package.</span></span> <span data-ttu-id="ae2a5-229">有关详细信息，请参阅本主题后面的[包含程序集文件](#including-assembly-files)和[包含内容文件](#including-content-files)。</span><span class="sxs-lookup"><span data-stu-id="ae2a5-229">See [Including assembly files](#including-assembly-files) and [Including content files](#including-content-files) later in this topic for details.</span></span>

## <a name="replacement-tokens"></a><span data-ttu-id="ae2a5-230">替换令牌</span><span class="sxs-lookup"><span data-stu-id="ae2a5-230">Replacement tokens</span></span>

<span data-ttu-id="ae2a5-231">创建包时，[`nuget pack` 命令](../tools/cli-ref-pack.md)使用来自项目文件的值或 `pack` 命令的 `-properties` 开关来替换 `.nuspec` 文件的 `<metadata>` 节点中带 $ 分隔符的令牌。</span><span class="sxs-lookup"><span data-stu-id="ae2a5-231">When creating a package, the [`nuget pack` command](../tools/cli-ref-pack.md) replaces $-delimited tokens in the `.nuspec` file's `<metadata>` node with values that come from either a project file or the `pack` command's `-properties` switch.</span></span>

<span data-ttu-id="ae2a5-232">在命令行中，可使用 `nuget pack -properties <name>=<value>;<name>=<value>` 指定令牌值。</span><span class="sxs-lookup"><span data-stu-id="ae2a5-232">On the command line, you specify token values with `nuget pack -properties <name>=<value>;<name>=<value>`.</span></span> <span data-ttu-id="ae2a5-233">例如，可使用 `.nuspec` 中的 `$owners$` 和 `$desc$` 令牌，并在封装时提供值，如下所示：</span><span class="sxs-lookup"><span data-stu-id="ae2a5-233">For example, you can use a token such as `$owners$` and `$desc$` in the `.nuspec` and provide the values at packing time as follows:</span></span>

```ps
nuget pack MyProject.csproj -properties
    owners=janedoe,harikm,kimo,xiaop;desc="Awesome app logger utility"
```

<span data-ttu-id="ae2a5-234">如要使用项目中的值，请指定下表中描述的令牌（AssemblyInfo 指的是 `Properties` 中的文件，如 `AssemblyInfo.cs` 或 `AssemblyInfo.vb`）。</span><span class="sxs-lookup"><span data-stu-id="ae2a5-234">To use values from a project, specify the tokens described in the table below (AssemblyInfo refers to the file in `Properties` such as `AssemblyInfo.cs` or `AssemblyInfo.vb`).</span></span>

<span data-ttu-id="ae2a5-235">若要使用这些令牌，请通过项目文件而不仅仅是 `.nuspec` 来运行 `nuget pack`。</span><span class="sxs-lookup"><span data-stu-id="ae2a5-235">To use these tokens, run `nuget pack` with the project file rather than just the `.nuspec`.</span></span> <span data-ttu-id="ae2a5-236">例如，使用以下命令时，`.nuspec` 文件中的 `$id$` 和 `$version$` 令牌会被替换为项目的 `AssemblyName` 和 `AssemblyVersion` 值：</span><span class="sxs-lookup"><span data-stu-id="ae2a5-236">For example, when using the following command, the `$id$` and `$version$` tokens in a `.nuspec` file are replaced with the project's `AssemblyName` and `AssemblyVersion` values:</span></span>

```ps
nuget pack MyProject.csproj
```

<span data-ttu-id="ae2a5-237">通常情况下，如果已有项目，最初会使用自动包含一些标准令牌的 `nuget spec MyProject.csproj` 创建 `.nuspec`。</span><span class="sxs-lookup"><span data-stu-id="ae2a5-237">Typically, when you have a project, you create the `.nuspec` initially using `nuget spec MyProject.csproj` which automatically includes some of these standard tokens.</span></span> <span data-ttu-id="ae2a5-238">然而，如果项目缺少要求的 `.nuspec` 元素的值，那么 `nuget pack` 失败。</span><span class="sxs-lookup"><span data-stu-id="ae2a5-238">However, if a project lacks values for required `.nuspec` elements, then `nuget pack` fails.</span></span> <span data-ttu-id="ae2a5-239">此外，如果更改项目值，请确定在创建包之前重新生成，可通过 pack 命令的 `build` 开关方便地完成此操作。</span><span class="sxs-lookup"><span data-stu-id="ae2a5-239">Furthermore, if you change project values, be sure to rebuild before creating the package; this can be done conveniently with the pack command's `build` switch.</span></span>

<span data-ttu-id="ae2a5-240">除 `$configuration$` 外，项目中的值优先于在命令行上分配给相同令牌的任何值。</span><span class="sxs-lookup"><span data-stu-id="ae2a5-240">With the exception of `$configuration$`, values in the project are used in preference to any assigned to the same token on the command line.</span></span>

| <span data-ttu-id="ae2a5-241">标记</span><span class="sxs-lookup"><span data-stu-id="ae2a5-241">Token</span></span> | <span data-ttu-id="ae2a5-242">值来源</span><span class="sxs-lookup"><span data-stu-id="ae2a5-242">Value source</span></span> | <span data-ttu-id="ae2a5-243">值</span><span class="sxs-lookup"><span data-stu-id="ae2a5-243">Value</span></span>
| --- | --- | ---
| <span data-ttu-id="ae2a5-244">**$id$**</span><span class="sxs-lookup"><span data-stu-id="ae2a5-244">**$id$**</span></span> | <span data-ttu-id="ae2a5-245">项目文件</span><span class="sxs-lookup"><span data-stu-id="ae2a5-245">Project file</span></span> | <span data-ttu-id="ae2a5-246">项目文件中的 AssemblyName （标题）</span><span class="sxs-lookup"><span data-stu-id="ae2a5-246">AssemblyName (title) from the project file</span></span> |
| <span data-ttu-id="ae2a5-247">**$version$**</span><span class="sxs-lookup"><span data-stu-id="ae2a5-247">**$version$**</span></span> | <span data-ttu-id="ae2a5-248">AssemblyInfo</span><span class="sxs-lookup"><span data-stu-id="ae2a5-248">AssemblyInfo</span></span> | <span data-ttu-id="ae2a5-249">AssemblyInformationalVersion（如果存在），否则为 AssemblyVersion</span><span class="sxs-lookup"><span data-stu-id="ae2a5-249">AssemblyInformationalVersion if present, otherwise AssemblyVersion</span></span> |
| <span data-ttu-id="ae2a5-250">**$author$**</span><span class="sxs-lookup"><span data-stu-id="ae2a5-250">**$author$**</span></span> | <span data-ttu-id="ae2a5-251">AssemblyInfo</span><span class="sxs-lookup"><span data-stu-id="ae2a5-251">AssemblyInfo</span></span> | <span data-ttu-id="ae2a5-252">AssemblyCompany</span><span class="sxs-lookup"><span data-stu-id="ae2a5-252">AssemblyCompany</span></span> |
| <span data-ttu-id="ae2a5-253">**$title$**</span><span class="sxs-lookup"><span data-stu-id="ae2a5-253">**$title$**</span></span> | <span data-ttu-id="ae2a5-254">AssemblyInfo</span><span class="sxs-lookup"><span data-stu-id="ae2a5-254">AssemblyInfo</span></span> | <span data-ttu-id="ae2a5-255">AssemblyTitle</span><span class="sxs-lookup"><span data-stu-id="ae2a5-255">AssemblyTitle</span></span> |
| <span data-ttu-id="ae2a5-256">**$description$**</span><span class="sxs-lookup"><span data-stu-id="ae2a5-256">**$description$**</span></span> | <span data-ttu-id="ae2a5-257">AssemblyInfo</span><span class="sxs-lookup"><span data-stu-id="ae2a5-257">AssemblyInfo</span></span> | <span data-ttu-id="ae2a5-258">AssemblyDescription</span><span class="sxs-lookup"><span data-stu-id="ae2a5-258">AssemblyDescription</span></span> |
| <span data-ttu-id="ae2a5-259">**$copyright$**</span><span class="sxs-lookup"><span data-stu-id="ae2a5-259">**$copyright$**</span></span> | <span data-ttu-id="ae2a5-260">AssemblyInfo</span><span class="sxs-lookup"><span data-stu-id="ae2a5-260">AssemblyInfo</span></span> | <span data-ttu-id="ae2a5-261">AssemblyCopyright</span><span class="sxs-lookup"><span data-stu-id="ae2a5-261">AssemblyCopyright</span></span> |
| <span data-ttu-id="ae2a5-262">**$configuration$**</span><span class="sxs-lookup"><span data-stu-id="ae2a5-262">**$configuration$**</span></span> | <span data-ttu-id="ae2a5-263">程序集 DLL</span><span class="sxs-lookup"><span data-stu-id="ae2a5-263">Assembly DLL</span></span> | <span data-ttu-id="ae2a5-264">用于生成程序集的配置，默认为 Debug。</span><span class="sxs-lookup"><span data-stu-id="ae2a5-264">Configuration used to build the assembly, defaulting to Debug.</span></span> <span data-ttu-id="ae2a5-265">请注意，若要使用 Release 配置创建包，应始终在命令行上使用 `-properties Configuration=Release`。</span><span class="sxs-lookup"><span data-stu-id="ae2a5-265">Note that to create a package using a Release configuration, you always use `-properties Configuration=Release` on the command line.</span></span> |

<span data-ttu-id="ae2a5-266">包含[程序集文件](#including-assembly-files)和[内容文件](#including-content-files)时，令牌也可用于解析路径。</span><span class="sxs-lookup"><span data-stu-id="ae2a5-266">Tokens can also be used to resolve paths when you include [assembly files](#including-assembly-files) and [content files](#including-content-files).</span></span> <span data-ttu-id="ae2a5-267">这些令牌与 MSBuild 属性具有相同的名称，因此可根据当前生成配置来选择要包含的文件。</span><span class="sxs-lookup"><span data-stu-id="ae2a5-267">The tokens have the same names as the MSBuild properties, making it possible to select files to be included depending on the current build configuration.</span></span> <span data-ttu-id="ae2a5-268">例如，如果在 `.nuspec` 文件中使用以下令牌：</span><span class="sxs-lookup"><span data-stu-id="ae2a5-268">For example, if you use the following tokens in the `.nuspec` file:</span></span>

```xml
<files>
    <file src="bin\$configuration$\$id$.pdb" target="lib\net40" />
</files>
```

<span data-ttu-id="ae2a5-269">在 MSBuild 中生成具有 `Release` 配置且 `AssemblyName` 为 `LoggingLibrary` 的程序集，包中 `.nuspec` 文件中的结果行如下所示：</span><span class="sxs-lookup"><span data-stu-id="ae2a5-269">And you build an assembly whose `AssemblyName` is `LoggingLibrary` with the `Release` configuration in MSBuild, the resulting lines in the `.nuspec` file in the package is as follows:</span></span>

```xml
<files>
    <file src="bin\Release\LoggingLibrary.pdb" target="lib\net40" />
</files>
```

## <a name="dependencies-element"></a><span data-ttu-id="ae2a5-270">依赖关系元素</span><span class="sxs-lookup"><span data-stu-id="ae2a5-270">Dependencies element</span></span>

<span data-ttu-id="ae2a5-271">`<metadata>` 中的 `<dependencies>` 元素包含任意数量的 `<dependency>` 元素，用来标识顶级包所依赖的其他包。</span><span class="sxs-lookup"><span data-stu-id="ae2a5-271">The `<dependencies>` element within `<metadata>` contains any number of `<dependency>` elements that identify other packages upon which the top-level package depends.</span></span> <span data-ttu-id="ae2a5-272">每个 `<dependency>` 的特性如下所示：</span><span class="sxs-lookup"><span data-stu-id="ae2a5-272">The attributes for each `<dependency>` are as follows:</span></span>

| <span data-ttu-id="ae2a5-273">特性</span><span class="sxs-lookup"><span data-stu-id="ae2a5-273">Attribute</span></span> | <span data-ttu-id="ae2a5-274">描述</span><span class="sxs-lookup"><span data-stu-id="ae2a5-274">Description</span></span> |
| --- | --- |
| `id` | <span data-ttu-id="ae2a5-275">（必须）依赖项的包 ID，如“EntityFramework”和“NUnit”，同时也是 nuget.org 在包页面上显示的包名称。</span><span class="sxs-lookup"><span data-stu-id="ae2a5-275">(Required) The package ID of the dependency, such as "EntityFramework" and "NUnit", which is the name of the package nuget.org shows on a package page.</span></span> |
| `version` | <span data-ttu-id="ae2a5-276">（必需）可接受作为依赖项的版本范围。</span><span class="sxs-lookup"><span data-stu-id="ae2a5-276">(Required) The range of versions acceptable as a dependency.</span></span> <span data-ttu-id="ae2a5-277">有关准确语法，请参阅[包版本控制](../reference/package-versioning.md#version-ranges-and-wildcards)。</span><span class="sxs-lookup"><span data-stu-id="ae2a5-277">See [Package versioning](../reference/package-versioning.md#version-ranges-and-wildcards) for exact syntax.</span></span> |
| <span data-ttu-id="ae2a5-278">include</span><span class="sxs-lookup"><span data-stu-id="ae2a5-278">include</span></span> | <span data-ttu-id="ae2a5-279">包括/排除标记的逗号分隔列表（见下文），指示要包含在最终包中的依赖项。</span><span class="sxs-lookup"><span data-stu-id="ae2a5-279">A comma-delimited list of include/exclude tags (see below) indicating of the dependency to include in the final package.</span></span> <span data-ttu-id="ae2a5-280">默认值为 `all`。</span><span class="sxs-lookup"><span data-stu-id="ae2a5-280">The default value is `all`.</span></span> |
| <span data-ttu-id="ae2a5-281">exclude</span><span class="sxs-lookup"><span data-stu-id="ae2a5-281">exclude</span></span> | <span data-ttu-id="ae2a5-282">包括/排除标记的逗号分隔列表（见下文），指示要排除在最终包外的依赖项。</span><span class="sxs-lookup"><span data-stu-id="ae2a5-282">A comma-delimited list of include/exclude tags (see below) indicating of the dependency to exclude in the final package.</span></span> <span data-ttu-id="ae2a5-283">默认值是`build,analyzers`，可以覆盖。</span><span class="sxs-lookup"><span data-stu-id="ae2a5-283">The  default value is `build,analyzers` which can be over-written.</span></span> <span data-ttu-id="ae2a5-284">但`content/ ContentFiles`还将隐式排除无法覆盖在最终包中。</span><span class="sxs-lookup"><span data-stu-id="ae2a5-284">But `content/ ContentFiles` are also implicitly excluded in the final package which can't be over-written.</span></span> <span data-ttu-id="ae2a5-285">用 `exclude` 指定的标记优先于用 `include` 指定的标记。</span><span class="sxs-lookup"><span data-stu-id="ae2a5-285">Tags specified with `exclude` take precedence over those specified with `include`.</span></span> <span data-ttu-id="ae2a5-286">例如，`include="runtime, compile" exclude="compile"` 和 `include="runtime"` 相同。</span><span class="sxs-lookup"><span data-stu-id="ae2a5-286">For example, `include="runtime, compile" exclude="compile"` is the same as `include="runtime"`.</span></span> |

| <span data-ttu-id="ae2a5-287">包括/排除标记</span><span class="sxs-lookup"><span data-stu-id="ae2a5-287">Include/Exclude tag</span></span> | <span data-ttu-id="ae2a5-288">受影响的目标文件夹</span><span class="sxs-lookup"><span data-stu-id="ae2a5-288">Affected folders of the target</span></span> |
| --- | --- |
| <span data-ttu-id="ae2a5-289">contentFiles</span><span class="sxs-lookup"><span data-stu-id="ae2a5-289">contentFiles</span></span> | <span data-ttu-id="ae2a5-290">内容</span><span class="sxs-lookup"><span data-stu-id="ae2a5-290">Content</span></span> |
| <span data-ttu-id="ae2a5-291">Runtime — 运行时</span><span class="sxs-lookup"><span data-stu-id="ae2a5-291">runtime</span></span> | <span data-ttu-id="ae2a5-292">运行时、资源和 FrameworkAssemblies</span><span class="sxs-lookup"><span data-stu-id="ae2a5-292">Runtime, Resources, and FrameworkAssemblies</span></span> |
| <span data-ttu-id="ae2a5-293">编译</span><span class="sxs-lookup"><span data-stu-id="ae2a5-293">compile</span></span> | <span data-ttu-id="ae2a5-294">lib</span><span class="sxs-lookup"><span data-stu-id="ae2a5-294">lib</span></span> |
| <span data-ttu-id="ae2a5-295">生成</span><span class="sxs-lookup"><span data-stu-id="ae2a5-295">build</span></span> | <span data-ttu-id="ae2a5-296">生成（MSBuild 属性和目标）</span><span class="sxs-lookup"><span data-stu-id="ae2a5-296">build (MSBuild props and targets)</span></span> |
| <span data-ttu-id="ae2a5-297">本机</span><span class="sxs-lookup"><span data-stu-id="ae2a5-297">native</span></span> | <span data-ttu-id="ae2a5-298">本机</span><span class="sxs-lookup"><span data-stu-id="ae2a5-298">native</span></span> |
| <span data-ttu-id="ae2a5-299">无</span><span class="sxs-lookup"><span data-stu-id="ae2a5-299">none</span></span> | <span data-ttu-id="ae2a5-300">无文件夹</span><span class="sxs-lookup"><span data-stu-id="ae2a5-300">No folders</span></span> |
| <span data-ttu-id="ae2a5-301">全部</span><span class="sxs-lookup"><span data-stu-id="ae2a5-301">all</span></span> | <span data-ttu-id="ae2a5-302">全部文件夹</span><span class="sxs-lookup"><span data-stu-id="ae2a5-302">All folders</span></span> |

<span data-ttu-id="ae2a5-303">例如，以下行指示 `PackageA` 版本 1.1.0 或更高版本，以及 `PackageB` 版本 1.x 的依赖项。</span><span class="sxs-lookup"><span data-stu-id="ae2a5-303">For example, the following lines indicate dependencies on `PackageA` version 1.1.0 or higher, and `PackageB` version 1.x.</span></span>

```xml
<dependencies>
    <dependency id="PackageA" version="1.1.0" />
    <dependency id="PackageB" version="[1,2)" />
</dependencies>
```

<span data-ttu-id="ae2a5-304">以下行指示相同包上的依赖项，但指定包括 `PackageA` 的 `contentFiles` 和 `build` 文件夹，以及除 `PackageB` 的 `native` 和 `compile` 文件夹以外的所有文件夹。</span><span class="sxs-lookup"><span data-stu-id="ae2a5-304">The following lines indicate dependencies on the same packages, but specify to include the `contentFiles` and `build` folders of `PackageA` and everything but the `native` and `compile` folders of `PackageB`"</span></span>

```xml
<dependencies>
    <dependency id="PackageA" version="1.1.0" include="contentFiles, build" />
    <dependency id="PackageB" version="[1,2)" exclude="native, compile" />
</dependencies>
```

<span data-ttu-id="ae2a5-305">注意:创建时`.nuspec`从项目使用`nuget spec`，在该项目中存在的依赖关系自动包含在生成`.nuspec`文件。</span><span class="sxs-lookup"><span data-stu-id="ae2a5-305">Note: When creating a `.nuspec` from a project using `nuget spec`, dependencies that exist in that project are automatically included in the resulting `.nuspec` file.</span></span>

### <a name="dependency-groups"></a><span data-ttu-id="ae2a5-306">依赖项组</span><span class="sxs-lookup"><span data-stu-id="ae2a5-306">Dependency groups</span></span>

<span data-ttu-id="ae2a5-307">版本 2.0+ </span><span class="sxs-lookup"><span data-stu-id="ae2a5-307">*Version 2.0+*</span></span>

<span data-ttu-id="ae2a5-308">作为单个简单列表的替代方法，可使用 `<dependencies>` 中的 `<group>` 元素根据目标项目的框架配置文件指定依赖项。</span><span class="sxs-lookup"><span data-stu-id="ae2a5-308">As an alternative to a single flat list, dependencies can be specified according to the framework profile of the target project using `<group>` elements within `<dependencies>`.</span></span>

<span data-ttu-id="ae2a5-309">每个组都有一个名为 `targetFramework` 的特性，并包含零个或多个 `<dependency>` 元素。</span><span class="sxs-lookup"><span data-stu-id="ae2a5-309">Each group has an attribute named `targetFramework` and contains zero or more `<dependency>` elements.</span></span> <span data-ttu-id="ae2a5-310">当目标框架与项目的框架配置文件兼容时，将会一起安装这些依赖项。</span><span class="sxs-lookup"><span data-stu-id="ae2a5-310">Those dependencies are installed together when  the target framework is compatible with the project's framework profile.</span></span>

<span data-ttu-id="ae2a5-311">无 `targetFramework` 特性的 `<group>` 元素被用作依赖项的默认列表或回退列表。</span><span class="sxs-lookup"><span data-stu-id="ae2a5-311">The `<group>` element without a `targetFramework` attribute is used as the default or fallback list of dependencies.</span></span> <span data-ttu-id="ae2a5-312">有关确切的框架标识符，请参阅[目标框架](../reference/target-frameworks.md)。</span><span class="sxs-lookup"><span data-stu-id="ae2a5-312">See [Target frameworks](../reference/target-frameworks.md) for the exact framework identifiers.</span></span>

> [!Important]
> <span data-ttu-id="ae2a5-313">组格式不能与简单列表混合使用。</span><span class="sxs-lookup"><span data-stu-id="ae2a5-313">The group format cannot be intermixed with a flat list.</span></span>

<span data-ttu-id="ae2a5-314">以下示例显示了 `<group>` 元素的不同变体：</span><span class="sxs-lookup"><span data-stu-id="ae2a5-314">The following example shows different variations of the `<group>` element:</span></span>

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

## <a name="explicit-assembly-references"></a><span data-ttu-id="ae2a5-315">显式程序集引用</span><span class="sxs-lookup"><span data-stu-id="ae2a5-315">Explicit assembly references</span></span>

<span data-ttu-id="ae2a5-316">`<references>` 元素显式指定目标项目在使用包时应引用的程序集。</span><span class="sxs-lookup"><span data-stu-id="ae2a5-316">The `<references>` element explicitly specifies the assemblies that the target project should reference when using the package.</span></span> <span data-ttu-id="ae2a5-317">当此元素存在时，NuGet 仅对列出的程序集添加引用，而不会对包的 `lib` 文件夹中的任何其他程序集添加引用。</span><span class="sxs-lookup"><span data-stu-id="ae2a5-317">When this element is present, NuGet add references to only the listed assemblies; it does not add references for any other assemblies in the package's `lib` folder.</span></span>

<span data-ttu-id="ae2a5-318">例如，以下 `<references>` 元素指示 NuGet 仅对 `xunit.dll` 和 `xunit.extensions.dll` 添加引用，即使包中还有其他程序集：</span><span class="sxs-lookup"><span data-stu-id="ae2a5-318">For example, the following `<references>` element instructs NuGet to add references to only `xunit.dll` and `xunit.extensions.dll` even if there are additional assemblies in the package:</span></span>

```xml
<references>
    <reference file="xunit.dll" />
    <reference file="xunit.extensions.dll" />
</references>
```

<span data-ttu-id="ae2a5-319">显式引用通常用于仅设计时程序集。</span><span class="sxs-lookup"><span data-stu-id="ae2a5-319">Explicit references are typically used for design-time only assemblies.</span></span> <span data-ttu-id="ae2a5-320">例如，在使用 [Code Contracts](/dotnet/framework/debug-trace-profile/code-contracts)（代码协定）时，协定程序集需要放在运行时程序集的旁边进行补充，以便 Visual Studio 能够找到它们，但协定程序集不需要被项目引用或复制到项目的 `bin` 文件夹。</span><span class="sxs-lookup"><span data-stu-id="ae2a5-320">When using [Code Contracts](/dotnet/framework/debug-trace-profile/code-contracts), for example, contract assemblies need to be next to the runtime assemblies that they augment so that Visual Studio can find them, but the contract assemblies need not be referenced by the project or copied into the project's `bin` folder.</span></span>

<span data-ttu-id="ae2a5-321">同样，显式引用可用于单元测试框架（如 XUnit），其工具程序集需要位于运行时程序集的旁边，但不需要包含为项目引用。</span><span class="sxs-lookup"><span data-stu-id="ae2a5-321">Similarly, explicit references can be used for unit test frameworks, such as XUnit, which needs its tools assemblies located next to the runtime assemblies, but does not need them included as project references.</span></span>

### <a name="reference-groups"></a><span data-ttu-id="ae2a5-322">引用组</span><span class="sxs-lookup"><span data-stu-id="ae2a5-322">Reference groups</span></span>

<span data-ttu-id="ae2a5-323">作为单个简单列表的替代方法，可使用 `<references>` 中的 `<group>` 元素根据目标项目的框架配置文件指定引用。</span><span class="sxs-lookup"><span data-stu-id="ae2a5-323">As an alternative to a single flat list, references can be specified according to the framework profile of the target project using `<group>` elements within `<references>`.</span></span>

<span data-ttu-id="ae2a5-324">每个组都有一个名为 `targetFramework` 的特性，并包含零个或多个 `<reference>` 元素。</span><span class="sxs-lookup"><span data-stu-id="ae2a5-324">Each group has an attribute named `targetFramework` and contains zero or more `<reference>` elements.</span></span> <span data-ttu-id="ae2a5-325">当目标框架与项目的框架配置文件兼容时，会将引用添加到项目中。</span><span class="sxs-lookup"><span data-stu-id="ae2a5-325">Those references are added to a project when the target framework is compatible with the project's framework profile.</span></span>

<span data-ttu-id="ae2a5-326">无 `targetFramework` 特性的 `<group>` 元素被用作引用的默认列表或回退列表。</span><span class="sxs-lookup"><span data-stu-id="ae2a5-326">The `<group>` element without a `targetFramework` attribute is used as the default or fallback list of references.</span></span> <span data-ttu-id="ae2a5-327">有关确切的框架标识符，请参阅[目标框架](../reference/target-frameworks.md)。</span><span class="sxs-lookup"><span data-stu-id="ae2a5-327">See [Target frameworks](../reference/target-frameworks.md) for the exact framework identifiers.</span></span>

> [!Important]
> <span data-ttu-id="ae2a5-328">组格式不能与简单列表混合使用。</span><span class="sxs-lookup"><span data-stu-id="ae2a5-328">The group format cannot be intermixed with a flat list.</span></span>

<span data-ttu-id="ae2a5-329">以下示例显示了 `<group>` 元素的不同变体：</span><span class="sxs-lookup"><span data-stu-id="ae2a5-329">The following example shows different variations of the `<group>` element:</span></span>

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

## <a name="framework-assembly-references"></a><span data-ttu-id="ae2a5-330">Framework 程序集引用</span><span class="sxs-lookup"><span data-stu-id="ae2a5-330">Framework assembly references</span></span>

<span data-ttu-id="ae2a5-331">Framework 程序集是 .NET Framework 的一部分，并已存在于任何给定计算机的全局程序集缓存 (GAC) 中。</span><span class="sxs-lookup"><span data-stu-id="ae2a5-331">Framework assemblies are those that are part of the .NET framework and should already be in the global assembly cache (GAC) for any given machine.</span></span> <span data-ttu-id="ae2a5-332">通过在 `<frameworkAssemblies>` 元素中标识这些程序集，包可确保在项目尚未具有此类引用的情况下，将必需的引用添加到项目中。</span><span class="sxs-lookup"><span data-stu-id="ae2a5-332">By identifying those assemblies within the `<frameworkAssemblies>` element, a package can ensure that required references are added to a project in the event that the project doesn't have such references already.</span></span> <span data-ttu-id="ae2a5-333">当然，此类程序集不直接包含在包中。</span><span class="sxs-lookup"><span data-stu-id="ae2a5-333">Such assemblies, of course, are not included in a package directly.</span></span>

<span data-ttu-id="ae2a5-334">`<frameworkAssemblies>` 元素包含零个或多个 `<frameworkAssembly>` 元素，这些元素指定以下特性：</span><span class="sxs-lookup"><span data-stu-id="ae2a5-334">The `<frameworkAssemblies>` element contains zero or more `<frameworkAssembly>` elements, each of which specifies the following attributes:</span></span>

| <span data-ttu-id="ae2a5-335">特性</span><span class="sxs-lookup"><span data-stu-id="ae2a5-335">Attribute</span></span> | <span data-ttu-id="ae2a5-336">描述</span><span class="sxs-lookup"><span data-stu-id="ae2a5-336">Description</span></span> |
| --- | --- |
| <span data-ttu-id="ae2a5-337">**assemblyName**</span><span class="sxs-lookup"><span data-stu-id="ae2a5-337">**assemblyName**</span></span> | <span data-ttu-id="ae2a5-338">（必需）完全限定程序集名称。</span><span class="sxs-lookup"><span data-stu-id="ae2a5-338">(Required) The fully qualified assembly name.</span></span> |
| <span data-ttu-id="ae2a5-339">**targetFramework**</span><span class="sxs-lookup"><span data-stu-id="ae2a5-339">**targetFramework**</span></span> | <span data-ttu-id="ae2a5-340">（可选）指定此引用适用的目标框架。</span><span class="sxs-lookup"><span data-stu-id="ae2a5-340">(Optional) Specifies the target framework to which this reference applies.</span></span> <span data-ttu-id="ae2a5-341">如果省略，则表示该引用适用于全部框架。</span><span class="sxs-lookup"><span data-stu-id="ae2a5-341">If omitted, indicates that the reference applies to all frameworks.</span></span> <span data-ttu-id="ae2a5-342">有关确切的框架标识符，请参阅[目标框架](../reference/target-frameworks.md)。</span><span class="sxs-lookup"><span data-stu-id="ae2a5-342">See [Target frameworks](../reference/target-frameworks.md) for the exact framework identifiers.</span></span> |

<span data-ttu-id="ae2a5-343">以下示例显示了对全部目标框架的 `System.Net` 的引用，以及对仅用于 .NET Framework 4.0 的 `System.ServiceModel` 的引用：</span><span class="sxs-lookup"><span data-stu-id="ae2a5-343">The following example shows a reference to `System.Net` for all target frameworks, and a reference to `System.ServiceModel` for .NET Framework 4.0 only:</span></span>

```xml
<frameworkAssemblies>
    <frameworkAssembly assemblyName="System.Net"  />

    <frameworkAssembly assemblyName="System.ServiceModel" targetFramework="net40" />
</frameworkAssemblies>
```

<a name="specifying-files-to-include-in-the-package"></a>

## <a name="including-assembly-files"></a><span data-ttu-id="ae2a5-344">包含程序集文件</span><span class="sxs-lookup"><span data-stu-id="ae2a5-344">Including assembly files</span></span>

<span data-ttu-id="ae2a5-345">如果遵循[创建包](../create-packages/creating-a-package.md)中介绍的约定，则不必在 `.nuspec` 文件中显式指定文件列表。</span><span class="sxs-lookup"><span data-stu-id="ae2a5-345">If you follow the conventions described in [Creating a Package](../create-packages/creating-a-package.md), you do not have to explicitly specify a list of files in the `.nuspec` file.</span></span> <span data-ttu-id="ae2a5-346">`nuget pack` 命令自动选取所需的文件。</span><span class="sxs-lookup"><span data-stu-id="ae2a5-346">The `nuget pack` command automatically picks up the necessary files.</span></span>

> [!Important]
> <span data-ttu-id="ae2a5-347">当包安装到项目中时，NuGet 自动将程序集引用添加到包的 DLL，不包括命名为 `.resources.dll` 的内容，因为它们被假定为本地化的附属程序集  。</span><span class="sxs-lookup"><span data-stu-id="ae2a5-347">When a package is installed into a project, NuGet automatically adds assembly references to the package's DLLs, *excluding* those that are named `.resources.dll` because they are assumed to be localized satellite assemblies.</span></span> <span data-ttu-id="ae2a5-348">为此，请避免对包含基本包代码的文件使用 `.resources.dll`。</span><span class="sxs-lookup"><span data-stu-id="ae2a5-348">For this reason, avoid using `.resources.dll` for files that otherwise contain essential package code.</span></span>

<span data-ttu-id="ae2a5-349">若要绕过此自动行为，并显式控制包中包含的文件，请将 `<files>` 元素作为 `<package>` 的子元素（和 `<metadata>` 的同级元素），并使用单独的 `<file>` 元素标识每个文件。</span><span class="sxs-lookup"><span data-stu-id="ae2a5-349">To bypass this automatic behavior and explicitly control which files are included in a package, place a `<files>` element as a child of `<package>` (and a sibling of `<metadata>`), identifying each file with a separate `<file>` element.</span></span> <span data-ttu-id="ae2a5-350">例如：</span><span class="sxs-lookup"><span data-stu-id="ae2a5-350">For example:</span></span>

```xml
<files>
    <file src="bin\Debug\*.dll" target="lib" />
    <file src="bin\Debug\*.pdb" target="lib" />
    <file src="tools\**\*.*" exclude="**\*.log" />
</files>
```

<span data-ttu-id="ae2a5-351">在 NuGet 2.x 及更早版本中，如果项目使用 `packages.config`，在安装包时，`<files>` 元素也用于包含不可变的内容文件。</span><span class="sxs-lookup"><span data-stu-id="ae2a5-351">With NuGet 2.x and earlier, and projects using `packages.config`, the `<files>` element is also used to include immutable content files when a package is installed.</span></span> <span data-ttu-id="ae2a5-352">通过 NuGet 3.3+ 和项目 PackageReference，将改为使用 `<contentFiles>` 元素。</span><span class="sxs-lookup"><span data-stu-id="ae2a5-352">With NuGet 3.3+ and projects PackageReference, the `<contentFiles>` element is used instead.</span></span> <span data-ttu-id="ae2a5-353">有关详细信息，请参阅下面的[包含内容文件](#including-content-files)。</span><span class="sxs-lookup"><span data-stu-id="ae2a5-353">See [Including content files](#including-content-files) below for details.</span></span>

### <a name="file-element-attributes"></a><span data-ttu-id="ae2a5-354">文件元素特性</span><span class="sxs-lookup"><span data-stu-id="ae2a5-354">File element attributes</span></span>

<span data-ttu-id="ae2a5-355">每个 `<file>` 元素指定以下特性：</span><span class="sxs-lookup"><span data-stu-id="ae2a5-355">Each `<file>` element specifies the following attributes:</span></span>

| <span data-ttu-id="ae2a5-356">特性</span><span class="sxs-lookup"><span data-stu-id="ae2a5-356">Attribute</span></span> | <span data-ttu-id="ae2a5-357">描述</span><span class="sxs-lookup"><span data-stu-id="ae2a5-357">Description</span></span> |
| --- | --- |
| <span data-ttu-id="ae2a5-358">**src**</span><span class="sxs-lookup"><span data-stu-id="ae2a5-358">**src**</span></span> | <span data-ttu-id="ae2a5-359">文件或要包含的文件位置，受 `exclude` 特性指定排除规则约束。</span><span class="sxs-lookup"><span data-stu-id="ae2a5-359">The location of the file or files to include, subject to exclusions specified by the `exclude` attribute.</span></span> <span data-ttu-id="ae2a5-360">路径是相对于 `.nuspec` 文件的路径，除非指定了绝对路径。</span><span class="sxs-lookup"><span data-stu-id="ae2a5-360">The path is relative to the `.nuspec` file unless an absolute path is specified.</span></span> <span data-ttu-id="ae2a5-361">允许使用通配符 `*`，双通配符 `**` 意味着递归文件夹搜索。</span><span class="sxs-lookup"><span data-stu-id="ae2a5-361">The wildcard character `*` is allowed, and the double wildcard `**` implies a recursive folder search.</span></span> |
| <span data-ttu-id="ae2a5-362">**target**</span><span class="sxs-lookup"><span data-stu-id="ae2a5-362">**target**</span></span> | <span data-ttu-id="ae2a5-363">放置源文件的包中文件夹的相对路径，必须以 `lib`、`content`、`build` 或 `tools` 开头。</span><span class="sxs-lookup"><span data-stu-id="ae2a5-363">The relative path to the folder within the package where the source files are placed, which must begin with `lib`, `content`, `build`, or `tools`.</span></span> <span data-ttu-id="ae2a5-364">请参阅[从基于约定的工作目录创建 .nuspec](../create-packages/creating-a-package.md#from-a-convention-based-working-directory)。</span><span class="sxs-lookup"><span data-stu-id="ae2a5-364">See [Creating a .nuspec from a convention-based working directory](../create-packages/creating-a-package.md#from-a-convention-based-working-directory).</span></span> |
| <span data-ttu-id="ae2a5-365">**exclude**</span><span class="sxs-lookup"><span data-stu-id="ae2a5-365">**exclude**</span></span> | <span data-ttu-id="ae2a5-366">要从 `src` 位置排除的文件或文件模式的分号分隔列表。</span><span class="sxs-lookup"><span data-stu-id="ae2a5-366">A semicolon-delimited list of files or file patterns to exclude from the `src` location.</span></span> <span data-ttu-id="ae2a5-367">允许使用通配符 `*`，双通配符 `**` 意味着递归文件夹搜索。</span><span class="sxs-lookup"><span data-stu-id="ae2a5-367">The wildcard character `*` is allowed, and the double wildcard `**` implies a recursive folder search.</span></span> |

### <a name="examples"></a><span data-ttu-id="ae2a5-368">示例</span><span class="sxs-lookup"><span data-stu-id="ae2a5-368">Examples</span></span>

<span data-ttu-id="ae2a5-369">**单个程序集**</span><span class="sxs-lookup"><span data-stu-id="ae2a5-369">**Single assembly**</span></span>

    Source file:
        library.dll

    .nuspec entry:
        <file src="library.dll" target="lib" />

    Packaged result:
        lib\library.dll

<span data-ttu-id="ae2a5-370">**特定于目标框架的单个程序集**</span><span class="sxs-lookup"><span data-stu-id="ae2a5-370">**Single assembly specific to a target framework**</span></span>

    Source file:
        library.dll

    .nuspec entry:
        <file src="assemblies\net40\library.dll" target="lib\net40" />

    Packaged result:
        lib\net40\library.dll

<span data-ttu-id="ae2a5-371">**使用通配符的 DLL 集**</span><span class="sxs-lookup"><span data-stu-id="ae2a5-371">**Set of DLLs using a wildcard**</span></span>

    Source files:
        bin\release\libraryA.dll
        bin\release\libraryB.dll

    .nuspec entry:
        <file src="bin\release\*.dll" target="lib" />

    Packaged result:
        lib\libraryA.dll
        lib\libraryB.dll

<span data-ttu-id="ae2a5-372">**适用于不同框架的 DLL**</span><span class="sxs-lookup"><span data-stu-id="ae2a5-372">**DLLs for different frameworks**</span></span>

    Source files:
        lib\net40\library.dll
        lib\net20\library.dll

    .nuspec entry (using ** recursive search):
        <file src="lib\**" target="lib" />

    Packaged result:
        lib\net40\library.dll
        lib\net20\library.dll

<span data-ttu-id="ae2a5-373">**排除文件**</span><span class="sxs-lookup"><span data-stu-id="ae2a5-373">**Excluding files**</span></span>

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

## <a name="including-content-files"></a><span data-ttu-id="ae2a5-374">包含内容文件</span><span class="sxs-lookup"><span data-stu-id="ae2a5-374">Including content files</span></span>

<span data-ttu-id="ae2a5-375">内容文件是包需要包含在项目中的不可变文件。</span><span class="sxs-lookup"><span data-stu-id="ae2a5-375">Content files are immutable files that a package needs to include in a project.</span></span> <span data-ttu-id="ae2a5-376">不可变文件指的是使用项目不会修改的文件。</span><span class="sxs-lookup"><span data-stu-id="ae2a5-376">Being immutable, they are not intended to be modified by the consuming project.</span></span> <span data-ttu-id="ae2a5-377">内容文件示例包括：</span><span class="sxs-lookup"><span data-stu-id="ae2a5-377">Example content files include:</span></span>

- <span data-ttu-id="ae2a5-378">作为资源嵌入的图像</span><span class="sxs-lookup"><span data-stu-id="ae2a5-378">Images that are embedded as resources</span></span>
- <span data-ttu-id="ae2a5-379">已编译的源文件</span><span class="sxs-lookup"><span data-stu-id="ae2a5-379">Source files that are already compiled</span></span>
- <span data-ttu-id="ae2a5-380">需要包含在项目的生成输出中的脚本</span><span class="sxs-lookup"><span data-stu-id="ae2a5-380">Scripts that need to be included with the build output of the project</span></span>
- <span data-ttu-id="ae2a5-381">需要包含在项目中，但不需要进行任何项目特定的更改的包的配置文件</span><span class="sxs-lookup"><span data-stu-id="ae2a5-381">Configuration files for the package that need to be included in the project but don't need any project-specific changes</span></span>

<span data-ttu-id="ae2a5-382">内容文件使用 `<files>` 元素包含在包中，并在 `target` 特性中指定 `content` 文件夹。</span><span class="sxs-lookup"><span data-stu-id="ae2a5-382">Content files are included in a package using the `<files>` element, specifying the `content` folder in the `target` attribute.</span></span> <span data-ttu-id="ae2a5-383">但是，使用 PackageReference（而不是使用 `<contentFiles>` 元素）将包安装到项目中时，将忽略这些文件。</span><span class="sxs-lookup"><span data-stu-id="ae2a5-383">However, such files are ignored when the package is installed in a project using PackageReference, which instead uses the `<contentFiles>` element.</span></span>

<span data-ttu-id="ae2a5-384">为了最大限度地兼容使用项目，一个包最好在两个元素中指定内容文件。</span><span class="sxs-lookup"><span data-stu-id="ae2a5-384">For maximum compatibility with consuming projects, a package ideally specifies the content files in both elements.</span></span>

### <a name="using-the-files-element-for-content-files"></a><span data-ttu-id="ae2a5-385">对内容文件使用文件元素</span><span class="sxs-lookup"><span data-stu-id="ae2a5-385">Using the files element for content files</span></span>

<span data-ttu-id="ae2a5-386">对于内容文件，只需使用与程序集文件相同的格式，但应在 `target` 属性中将 `content` 指定为基本文件夹，如以下示例所示。</span><span class="sxs-lookup"><span data-stu-id="ae2a5-386">For content files, simply use the same format as for assembly files, but specify `content` as the base folder in the `target` attribute as shown in the following examples.</span></span>

<span data-ttu-id="ae2a5-387">**基本内容文件**</span><span class="sxs-lookup"><span data-stu-id="ae2a5-387">**Basic content files**</span></span>

    Source files:
        css\mobile\style1.css
        css\mobile\style2.css

    .nuspec entry:
        <file src="css\mobile\*.css" target="content\css\mobile" />

    Packaged result:
        content\css\mobile\style1.css
        content\css\mobile\style2.css

<span data-ttu-id="ae2a5-388">**具有目录结构的内容文件**</span><span class="sxs-lookup"><span data-stu-id="ae2a5-388">**Content files with directory structure**</span></span>

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

<span data-ttu-id="ae2a5-389">**特定于目标框架的内容文件**</span><span class="sxs-lookup"><span data-stu-id="ae2a5-389">**Content file specific to a target framework**</span></span>

    Source file:
        css\cool\style.css

    .nuspec entry
        <file src="css\cool\style.css" target="Content" />

    Packaged result:
        content\style.css

<span data-ttu-id="ae2a5-390">**复制到名称中带点的文件夹的内容文件**</span><span class="sxs-lookup"><span data-stu-id="ae2a5-390">**Content file copied to a folder with dot in name**</span></span>

<span data-ttu-id="ae2a5-391">在此情况下，NuGet 发现 `target` 中的扩展名与 `src` 中的扩展名不匹配，因此将 `target` 中名称的该部分作为文件夹：</span><span class="sxs-lookup"><span data-stu-id="ae2a5-391">In this case, NuGet sees that the extension in `target` does not match the extension in `src` and thus treats that part of the name in `target` as a folder:</span></span>

    Source file:
        images\picture.png

    .nuspec entry:
        <file src="images\picture.png" target="Content\images\package.icons" />

    Packaged result:
        content\images\package.icons\picture.png

<span data-ttu-id="ae2a5-392">**不具有扩展名的内容文件**</span><span class="sxs-lookup"><span data-stu-id="ae2a5-392">**Content files without extensions**</span></span>

<span data-ttu-id="ae2a5-393">若要包含不具有扩展名的文件，请使用 `*` 或 `**` 通配符：</span><span class="sxs-lookup"><span data-stu-id="ae2a5-393">To include files without an extension, use the `*` or `**` wildcards:</span></span>

    Source file:
        flags\installed

    .nuspec entry:
        <file src="flags\**" target="flags" />

    Packaged result:
        flags\installed

<span data-ttu-id="ae2a5-394">**具有深层路径和深层目标的内容文件**</span><span class="sxs-lookup"><span data-stu-id="ae2a5-394">**Content files with deep path and deep target**</span></span>

<span data-ttu-id="ae2a5-395">在此情况下，由于源文件和目标文件的扩展名匹配，NuGet 假定目标是文件名而不是文件夹：</span><span class="sxs-lookup"><span data-stu-id="ae2a5-395">In this case, because the file extensions of the source and target match, NuGet assumes that the target is a file name and not a folder:</span></span>

    Source file:
        css\cool\style.css

    .nuspec entry:
        <file src="css\cool\style.css" target="Content\css\cool" />
        or:
        <file src="css\cool\style.css" target="Content\css\cool\style.css" />

    Packaged result:
        content\css\cool\style.css

<span data-ttu-id="ae2a5-396">**重命名包中的内容文件**</span><span class="sxs-lookup"><span data-stu-id="ae2a5-396">**Renaming a content file in the package**</span></span>

    Source file:
        ie\css\style.css

    .nuspec entry:
        <file src="ie\css\style.css" target="Content\css\ie.css" />

    Packaged result:
        content\css\ie.css

<span data-ttu-id="ae2a5-397">**排除文件**</span><span class="sxs-lookup"><span data-stu-id="ae2a5-397">**Excluding files**</span></span>

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

### <a name="using-the-contentfiles-element-for-content-files"></a><span data-ttu-id="ae2a5-398">对内容文件使用 contentFiles 元素</span><span class="sxs-lookup"><span data-stu-id="ae2a5-398">Using the contentFiles element for content files</span></span>

<span data-ttu-id="ae2a5-399">*NuGet 4.0+ 与 PackageReference*</span><span class="sxs-lookup"><span data-stu-id="ae2a5-399">*NuGet 4.0+ with PackageReference*</span></span>

<span data-ttu-id="ae2a5-400">默认情况下，包将内容放置在 `contentFiles` 文件夹中（见下文），`nuget pack` 使用默认特性将全部文件包含在该文件夹中。</span><span class="sxs-lookup"><span data-stu-id="ae2a5-400">By default, a package places content in a `contentFiles` folder (see below) and `nuget pack` included all files in that folder using default attributes.</span></span> <span data-ttu-id="ae2a5-401">在此情况下，根本没有必要在 `.nuspec` 中包含 `contentFiles` 节点。</span><span class="sxs-lookup"><span data-stu-id="ae2a5-401">In this case it's not necessary to include a `contentFiles` node in the `.nuspec` at all.</span></span>

<span data-ttu-id="ae2a5-402">若要控制包含哪些文件，`<contentFiles>` 元素指定是 `<files>` 元素的集合，可标识包含的确切文件。</span><span class="sxs-lookup"><span data-stu-id="ae2a5-402">To control which files are included, the `<contentFiles>` element specifies is a collection of `<files>` elements that identify the exact files include.</span></span>

<span data-ttu-id="ae2a5-403">这些文件用一组特性指定，用于描述如何在项目系统中使用这些文件：</span><span class="sxs-lookup"><span data-stu-id="ae2a5-403">These files are specified with a set of attributes that describe how they should be used within the project system:</span></span>

| <span data-ttu-id="ae2a5-404">特性</span><span class="sxs-lookup"><span data-stu-id="ae2a5-404">Attribute</span></span> | <span data-ttu-id="ae2a5-405">描述</span><span class="sxs-lookup"><span data-stu-id="ae2a5-405">Description</span></span> |
| --- | --- |
| <span data-ttu-id="ae2a5-406">**include**</span><span class="sxs-lookup"><span data-stu-id="ae2a5-406">**include**</span></span> | <span data-ttu-id="ae2a5-407">（必需）文件或要包含的文件位置，受 `exclude` 特性指定的排除规则约束。</span><span class="sxs-lookup"><span data-stu-id="ae2a5-407">(Required) The location of the file or files to include, subject to exclusions specified by the `exclude` attribute.</span></span> <span data-ttu-id="ae2a5-408">路径是相对于 `.nuspec` 文件的路径，除非指定了绝对路径。</span><span class="sxs-lookup"><span data-stu-id="ae2a5-408">The path is relative to the `.nuspec` file unless an absolute path is specified.</span></span> <span data-ttu-id="ae2a5-409">允许使用通配符 `*`，双通配符 `**` 意味着递归文件夹搜索。</span><span class="sxs-lookup"><span data-stu-id="ae2a5-409">The wildcard character `*` is allowed, and the double wildcard `**` implies a recursive folder search.</span></span> |
| <span data-ttu-id="ae2a5-410">**exclude**</span><span class="sxs-lookup"><span data-stu-id="ae2a5-410">**exclude**</span></span> | <span data-ttu-id="ae2a5-411">要从 `src` 位置排除的文件或文件模式的分号分隔列表。</span><span class="sxs-lookup"><span data-stu-id="ae2a5-411">A semicolon-delimited list of files or file patterns to exclude from the `src` location.</span></span> <span data-ttu-id="ae2a5-412">允许使用通配符 `*`，双通配符 `**` 意味着递归文件夹搜索。</span><span class="sxs-lookup"><span data-stu-id="ae2a5-412">The wildcard character `*` is allowed, and the double wildcard `**` implies a recursive folder search.</span></span> |
| <span data-ttu-id="ae2a5-413">**buildAction**</span><span class="sxs-lookup"><span data-stu-id="ae2a5-413">**buildAction**</span></span> | <span data-ttu-id="ae2a5-414">生成操作，用于分配到 MSBuild 的内容项（如 `Content`、`None`、`Embedded Resource`、`Compile` 等）。默认值为 `Compile`。</span><span class="sxs-lookup"><span data-stu-id="ae2a5-414">The build action to assign to the content item for MSBuild, such as `Content`, `None`, `Embedded Resource`, `Compile`, etc. The default is `Compile`.</span></span> |
| <span data-ttu-id="ae2a5-415">**copyToOutput**</span><span class="sxs-lookup"><span data-stu-id="ae2a5-415">**copyToOutput**</span></span> | <span data-ttu-id="ae2a5-416">布尔值，该值指示是否将内容项复制到生成 （或发布） 输出文件夹。</span><span class="sxs-lookup"><span data-stu-id="ae2a5-416">A Boolean indicating whether to copy content items to the build (or publish) output folder.</span></span> <span data-ttu-id="ae2a5-417">默认值为 false。</span><span class="sxs-lookup"><span data-stu-id="ae2a5-417">The default is false.</span></span> |
| <span data-ttu-id="ae2a5-418">**flatten**</span><span class="sxs-lookup"><span data-stu-id="ae2a5-418">**flatten**</span></span> | <span data-ttu-id="ae2a5-419">一个布尔值，用于指示是将内容项复制到生成输出中的单个文件夹 (true)，还是保留包中的文件夹结构 (false)。</span><span class="sxs-lookup"><span data-stu-id="ae2a5-419">A Boolean indicating whether to copy content items to a single folder in the build output (true), or to preserve the folder structure in the package (false).</span></span> <span data-ttu-id="ae2a5-420">此标志仅在 copyToOutput 标志设置为 true 时才有效。</span><span class="sxs-lookup"><span data-stu-id="ae2a5-420">This flag only works when copyToOutput flag is set to true.</span></span> <span data-ttu-id="ae2a5-421">默认值为 false。</span><span class="sxs-lookup"><span data-stu-id="ae2a5-421">The default is false.</span></span> |

<span data-ttu-id="ae2a5-422">安装包时，NuGet 从上到下应用 `<contentFiles>` 的子元素。</span><span class="sxs-lookup"><span data-stu-id="ae2a5-422">When installing a package, NuGet applies the child elements of `<contentFiles>` from top to bottom.</span></span> <span data-ttu-id="ae2a5-423">如果多个条目与相同的文件匹配，那么应用全部条目。</span><span class="sxs-lookup"><span data-stu-id="ae2a5-423">If multiple entries match the same file then all entries are applied.</span></span> <span data-ttu-id="ae2a5-424">如果相同特性发生冲突，则最上面的条目将替代靠下的条目。</span><span class="sxs-lookup"><span data-stu-id="ae2a5-424">The top-most entry overrides the lower entries if there is a conflict for the same attribute.</span></span>

#### <a name="package-folder-structure"></a><span data-ttu-id="ae2a5-425">包文件夹结构</span><span class="sxs-lookup"><span data-stu-id="ae2a5-425">Package folder structure</span></span>

<span data-ttu-id="ae2a5-426">包项目应使用以下模式构建内容结构：</span><span class="sxs-lookup"><span data-stu-id="ae2a5-426">The package project should structure content using the following pattern:</span></span>

    /contentFiles/{codeLanguage}/{TxM}/{any?}

- <span data-ttu-id="ae2a5-427">`codeLanguages` 可以是 `cs`、`vb`、`fs`、`any` 或给定 `$(ProjectLanguage)` 的小写等效形式</span><span class="sxs-lookup"><span data-stu-id="ae2a5-427">`codeLanguages` may be `cs`, `vb`, `fs`, `any`, or the lowercase equivalent of a given `$(ProjectLanguage)`</span></span>
- <span data-ttu-id="ae2a5-428">`TxM` 是 NuGet 支持的任何合法目标框架名字对象（请参阅[目标框架](../reference/target-frameworks.md)）。</span><span class="sxs-lookup"><span data-stu-id="ae2a5-428">`TxM` is any legal target framework moniker that NuGet supports (see [Target frameworks](../reference/target-frameworks.md)).</span></span>
- <span data-ttu-id="ae2a5-429">任何文件夹结构都可以附加到此语法的末尾。</span><span class="sxs-lookup"><span data-stu-id="ae2a5-429">Any folder structure may be appended to the end of this syntax.</span></span>

<span data-ttu-id="ae2a5-430">例如：</span><span class="sxs-lookup"><span data-stu-id="ae2a5-430">For example:</span></span>

    Language- and framework-agnostic:
        /contentFiles/any/any/config.xml

    net45 content for all languages
        /contentFiles/any/net45/config.xml

    C#-specific content for net45 and up
        /contentFiles/cs/net45/sample.cs

<span data-ttu-id="ae2a5-431">空文件夹可以使用 `.` 来选择不提供特定语言和 TxM 组合的内容，例如：</span><span class="sxs-lookup"><span data-stu-id="ae2a5-431">Empty folders can use `.` to opt out of providing content for certain combinations of language and TxM, for example:</span></span>

    /contentFiles/vb/any/code.vb
    /contentFiles/cs/any/.

#### <a name="example-contentfiles-section"></a><span data-ttu-id="ae2a5-432">contentFiles 部分示例</span><span class="sxs-lookup"><span data-stu-id="ae2a5-432">Example contentFiles section</span></span>

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

## <a name="example-nuspec-files"></a><span data-ttu-id="ae2a5-433">示例 nuspec 文件</span><span class="sxs-lookup"><span data-stu-id="ae2a5-433">Example nuspec files</span></span>

<span data-ttu-id="ae2a5-434">**未指定依赖项或文件的简单 `.nuspec`**</span><span class="sxs-lookup"><span data-stu-id="ae2a5-434">**A simple `.nuspec` that does not specify dependencies or files**</span></span>

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

<span data-ttu-id="ae2a5-435">**具有依赖项的 `.nuspec`**</span><span class="sxs-lookup"><span data-stu-id="ae2a5-435">**A `.nuspec` with dependencies**</span></span>

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

<span data-ttu-id="ae2a5-436">**具有文件的 `.nuspec`**</span><span class="sxs-lookup"><span data-stu-id="ae2a5-436">**A `.nuspec` with files**</span></span>

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

<span data-ttu-id="ae2a5-437">**具有 Framework 程序集的 `.nuspec`**</span><span class="sxs-lookup"><span data-stu-id="ae2a5-437">**A `.nuspec` with framework assemblies**</span></span>

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

<span data-ttu-id="ae2a5-438">在此示例中，为特定的项目目标安装了以下内容：</span><span class="sxs-lookup"><span data-stu-id="ae2a5-438">In this example, the following are installed for specific project targets:</span></span>

- <span data-ttu-id="ae2a5-439">.NET4 -> `System.Web``System.Net`</span><span class="sxs-lookup"><span data-stu-id="ae2a5-439">.NET4 -> `System.Web`, `System.Net`</span></span>
- <span data-ttu-id="ae2a5-440">.NET4 Client Profile -> `System.Net`</span><span class="sxs-lookup"><span data-stu-id="ae2a5-440">.NET4 Client Profile -> `System.Net`</span></span>
- <span data-ttu-id="ae2a5-441">Silverlight 3 -> `System.Json`</span><span class="sxs-lookup"><span data-stu-id="ae2a5-441">Silverlight 3 -> `System.Json`</span></span>
- <span data-ttu-id="ae2a5-442">WindowsPhone -> `Microsoft.Devices.Sensors`</span><span class="sxs-lookup"><span data-stu-id="ae2a5-442">WindowsPhone -> `Microsoft.Devices.Sensors`</span></span>
