---
title: NuGet 包版本引用
description: 详细介绍如何为 NuGet 包所依赖的其他包指定版本号和范围以及如何安装依赖项的确切信息。
author: karann-msft
ms.author: karann
ms.date: 03/23/2018
ms.topic: reference
ms.reviewer: anangaur
ms.openlocfilehash: e0014a812ea591ef40c961e13864652d75ebdf6c
ms.sourcegitcommit: 39f2ae79fbbc308e06acf67ee8e24cfcdb2c831b
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/05/2019
ms.locfileid: "73610993"
---
# <a name="package-versioning"></a><span data-ttu-id="c92a2-103">包版本控制</span><span class="sxs-lookup"><span data-stu-id="c92a2-103">Package versioning</span></span>

<span data-ttu-id="c92a2-104">始终使用特定包的包标识符和确切的版本号来引用该包。</span><span class="sxs-lookup"><span data-stu-id="c92a2-104">A specific package is always referred to using its package identifier and an exact version number.</span></span> <span data-ttu-id="c92a2-105">例如，nuget.org 上的[实体框架](https://www.nuget.org/packages/EntityFramework/)提供了数十个特定包，范围从版本 4.1.10311 到版本 6.1.3（最新稳定版）以及各种预发布版本（例如 6.2.0-beta1）    。</span><span class="sxs-lookup"><span data-stu-id="c92a2-105">For example, [Entity Framework](https://www.nuget.org/packages/EntityFramework/) on nuget.org has several dozen specific packages available, ranging from version *4.1.10311* to version *6.1.3* (the latest stable release) and a variety of pre-release versions like *6.2.0-beta1*.</span></span>

<span data-ttu-id="c92a2-106">创建包时，可以分配带有可选预发布文本后缀的特定版本号。</span><span class="sxs-lookup"><span data-stu-id="c92a2-106">When creating a package, you assign a specific version number with an optional pre-release text suffix.</span></span> <span data-ttu-id="c92a2-107">另一方面，使用包时，可以指定确切的版本号或可接受的版本范围。</span><span class="sxs-lookup"><span data-stu-id="c92a2-107">When consuming packages, on the other hand, you can specify either an exact version number or a range of acceptable versions.</span></span>

<span data-ttu-id="c92a2-108">本主题内容：</span><span class="sxs-lookup"><span data-stu-id="c92a2-108">In this topic:</span></span>

- <span data-ttu-id="c92a2-109">[版本基础知识](#version-basics)，包括预发布后缀。</span><span class="sxs-lookup"><span data-stu-id="c92a2-109">[Version basics](#version-basics) including pre-release suffixes.</span></span>
- [<span data-ttu-id="c92a2-110">版本范围和通配符</span><span class="sxs-lookup"><span data-stu-id="c92a2-110">Version ranges and wildcards</span></span>](#version-ranges-and-wildcards)
- [<span data-ttu-id="c92a2-111">规范化的版本号</span><span class="sxs-lookup"><span data-stu-id="c92a2-111">Normalized version numbers</span></span>](#normalized-version-numbers)

## <a name="version-basics"></a><span data-ttu-id="c92a2-112">版本基础知识</span><span class="sxs-lookup"><span data-stu-id="c92a2-112">Version basics</span></span>

<span data-ttu-id="c92a2-113">特定版本号的格式为 Major.Minor.Patch[-Suffix]  ，其中的组件具有以下含义：</span><span class="sxs-lookup"><span data-stu-id="c92a2-113">A specific version number is in the form *Major.Minor.Patch[-Suffix]*, where the components have the following meanings:</span></span>

- <span data-ttu-id="c92a2-114">*Major*：重大更改</span><span class="sxs-lookup"><span data-stu-id="c92a2-114">*Major*: Breaking changes</span></span>
- <span data-ttu-id="c92a2-115">*Minor*：新增功能，但可向后兼容</span><span class="sxs-lookup"><span data-stu-id="c92a2-115">*Minor*: New features, but backwards compatible</span></span>
- <span data-ttu-id="c92a2-116">*Patch*：仅可向后兼容的 bug 修复</span><span class="sxs-lookup"><span data-stu-id="c92a2-116">*Patch*: Backwards compatible bug fixes only</span></span>
- <span data-ttu-id="c92a2-117">*-Suffix*（可选）：连字符后跟字符串，表示预发布版本（遵循[语义化版本控制或 SemVer 1.0 约定](https://semver.org/spec/v1.0.0.html)）。</span><span class="sxs-lookup"><span data-stu-id="c92a2-117">*-Suffix* (optional): a hyphen followed by a string denoting a pre-release version (following the [Semantic Versioning or SemVer 1.0 convention](https://semver.org/spec/v1.0.0.html)).</span></span>

<span data-ttu-id="c92a2-118">**示例：**</span><span class="sxs-lookup"><span data-stu-id="c92a2-118">**Examples:**</span></span>

    1.0.1
    6.11.1231
    4.3.1-rc
    2.2.44-beta1

> [!Important]
> <span data-ttu-id="c92a2-119">nuget.org 拒绝缺少确切版本号的任何包上传。</span><span class="sxs-lookup"><span data-stu-id="c92a2-119">nuget.org rejects any package upload that lacks an exact version number.</span></span> <span data-ttu-id="c92a2-120">必须在用于创建包的 `.nuspec` 或项目文件中指定版本。</span><span class="sxs-lookup"><span data-stu-id="c92a2-120">The version must be specified in the `.nuspec` or project file used to create the package.</span></span>

### <a name="pre-release-versions"></a><span data-ttu-id="c92a2-121">预发布版本</span><span class="sxs-lookup"><span data-stu-id="c92a2-121">Pre-release versions</span></span>

<span data-ttu-id="c92a2-122">从技术上讲，包创建者可以将任何字符串用作后缀来表示预发布版本，因为 NuGet 会将任何此类版本视为预发布版本，而不进行任何其他解释。</span><span class="sxs-lookup"><span data-stu-id="c92a2-122">Technically speaking, package creators can use any string as a suffix to denote a pre-release version, as NuGet treats any such version as pre-release and makes no other interpretation.</span></span> <span data-ttu-id="c92a2-123">也就是说，NuGet 在任何涉及的 UI 中显示完整版本字符串，并让使用者自行理解后缀的含义。</span><span class="sxs-lookup"><span data-stu-id="c92a2-123">That is, NuGet displays the full version string in whatever UI is involved, leaving any interpretation of the suffix's meaning to the consumer.</span></span>

<span data-ttu-id="c92a2-124">综上所述，包开发人员通常遵循识别的命名约定：</span><span class="sxs-lookup"><span data-stu-id="c92a2-124">That said, package developers generally follow recognized naming conventions:</span></span>

- <span data-ttu-id="c92a2-125">`-alpha`：Alpha 版本，通常用于在制品和试验品。</span><span class="sxs-lookup"><span data-stu-id="c92a2-125">`-alpha`: Alpha release, typically used for work-in-progress and experimentation.</span></span>
- <span data-ttu-id="c92a2-126">`-beta`：Beta 版本，通常指可用于下一计划版本的功能完整的版本，但可能包含已知 bug。</span><span class="sxs-lookup"><span data-stu-id="c92a2-126">`-beta`: Beta release, typically one that is feature complete for the next planned release, but may contain known bugs.</span></span>
- <span data-ttu-id="c92a2-127">`-rc`：候选发布，通常可能为最终（稳定）版本，除非出现重大 bug。</span><span class="sxs-lookup"><span data-stu-id="c92a2-127">`-rc`: Release candidate, typically a release that's potentially final (stable) unless significant bugs emerge.</span></span>

> [!Note]
> <span data-ttu-id="c92a2-128">NuGet 4.3.0+ 支持 [SemVer 2.0.0](https://semver.org/spec/v2.0.0.html)，后者支持采用点表示法的预发布号，如 1.0.1-build.23  中所示。</span><span class="sxs-lookup"><span data-stu-id="c92a2-128">NuGet 4.3.0+ supports [SemVer 2.0.0](https://semver.org/spec/v2.0.0.html), which supports pre-release numbers with dot notation, as in *1.0.1-build.23*.</span></span> <span data-ttu-id="c92a2-129">NuGet 4.3.0 之前的版本不支持点表示法。</span><span class="sxs-lookup"><span data-stu-id="c92a2-129">Dot notation is not supported with NuGet versions before 4.3.0.</span></span> <span data-ttu-id="c92a2-130">可以使用类似于 1.0.1-build23 的形式  。</span><span class="sxs-lookup"><span data-stu-id="c92a2-130">You can use a form like *1.0.1-build23*.</span></span>

<span data-ttu-id="c92a2-131">解析包引用时，如果多个包版本只有后缀不同，NuGet 会首先选择不带后缀的版本，然后按反向字母顺序来排列预发布版本的优先顺序。</span><span class="sxs-lookup"><span data-stu-id="c92a2-131">When resolving package references and multiple package versions differ only by suffix, NuGet chooses a version without a suffix first, then applies precedence to pre-release versions in reverse alphabetical order.</span></span> <span data-ttu-id="c92a2-132">例如，将按显示的确切顺序选择以下版本：</span><span class="sxs-lookup"><span data-stu-id="c92a2-132">For example, the following versions would be chosen in the exact order shown:</span></span>

    1.0.1
    1.0.1-zzz
    1.0.1-rc
    1.0.1-open
    1.0.1-beta
    1.0.1-alpha2
    1.0.1-alpha
    1.0.1-aaa

## <a name="semantic-versioning-200"></a><span data-ttu-id="c92a2-133">语义化版本控制 2.0.0</span><span class="sxs-lookup"><span data-stu-id="c92a2-133">Semantic Versioning 2.0.0</span></span>

<span data-ttu-id="c92a2-134">借助 NuGet 4.3.0+ 和 Visual Studio 2017 版本 15.3+，NuGet 支持[语义化版本控制 2.0.0](https://semver.org/spec/v2.0.0.html)。</span><span class="sxs-lookup"><span data-stu-id="c92a2-134">With NuGet 4.3.0+ and Visual Studio 2017 version 15.3+, NuGet supports [Semantic Versioning 2.0.0](https://semver.org/spec/v2.0.0.html).</span></span>

<span data-ttu-id="c92a2-135">旧客户端不支持 SemVer v2.0.0 的某些语义。</span><span class="sxs-lookup"><span data-stu-id="c92a2-135">Certain semantics of SemVer v2.0.0 are not supported in older clients.</span></span> <span data-ttu-id="c92a2-136">在以下任意一种情况下，NuGet 会将包版本视为特定于 SemVer v2.0.0：</span><span class="sxs-lookup"><span data-stu-id="c92a2-136">NuGet considers a package version to be SemVer v2.0.0 specific if either of the following statements is true:</span></span>

- <span data-ttu-id="c92a2-137">预发布标签以点分隔，例如，1.0.0-alpha.1 </span><span class="sxs-lookup"><span data-stu-id="c92a2-137">The pre-release label is dot-separated, for example, *1.0.0-alpha.1*</span></span>
- <span data-ttu-id="c92a2-138">版本具有生成元数据，例如，1.0.0+githash </span><span class="sxs-lookup"><span data-stu-id="c92a2-138">The version has build-metadata, for example, *1.0.0+githash*</span></span>

<span data-ttu-id="c92a2-139">对于 nuget.org，在以下任意一种情况下，会将包定义为 SemVer v2.0.0 包：</span><span class="sxs-lookup"><span data-stu-id="c92a2-139">For nuget.org, a package is defined as a SemVer v2.0.0 package if either of the following statements is true:</span></span>

- <span data-ttu-id="c92a2-140">按照上述定义，包自己的版本与 SemVer v2.0.0 兼容，但与 SemVer v1.0.0 不兼容。</span><span class="sxs-lookup"><span data-stu-id="c92a2-140">The package's own version is SemVer v2.0.0 compliant but not SemVer v1.0.0 compliant, as defined above.</span></span>
- <span data-ttu-id="c92a2-141">按照上述定义，包的任何依赖项版本范围都具有与 SemVer v2.0.0 兼容但与 SemVer v1.0.0 不兼容的最低版本或最高版本；例如，[1.0.0-alpha.1, )  。</span><span class="sxs-lookup"><span data-stu-id="c92a2-141">Any of the package's dependency version ranges has a minimum or maximum version that is SemVer v2.0.0 compliant but not SemVer v1.0.0 compliant, defined above; for example, *[1.0.0-alpha.1, )*.</span></span>

<span data-ttu-id="c92a2-142">如果将 SemVer v2.0.0 特定包上传到 nuget.org，则该包对较旧的客户端不可见，并且仅可用于以下 NuGet 客户端：</span><span class="sxs-lookup"><span data-stu-id="c92a2-142">If you upload a SemVer v2.0.0-specific package to nuget.org, the package is invisible to older clients and available to only the following NuGet clients:</span></span>

- <span data-ttu-id="c92a2-143">NuGet 4.3.0+</span><span class="sxs-lookup"><span data-stu-id="c92a2-143">NuGet 4.3.0+</span></span>
- <span data-ttu-id="c92a2-144">Visual Studio 2017 版本 15.3+</span><span class="sxs-lookup"><span data-stu-id="c92a2-144">Visual Studio 2017 version 15.3+</span></span>
- <span data-ttu-id="c92a2-145">带有 [NuGet VSIX v3.6.0](https://dist.nuget.org/visualstudio-2015-vsix/latest/NuGet.Tools.vsix) 的 Visual Studio 2015</span><span class="sxs-lookup"><span data-stu-id="c92a2-145">Visual Studio 2015 with [NuGet VSIX v3.6.0](https://dist.nuget.org/visualstudio-2015-vsix/latest/NuGet.Tools.vsix)</span></span>
- <span data-ttu-id="c92a2-146">dotnet</span><span class="sxs-lookup"><span data-stu-id="c92a2-146">dotnet</span></span>
  - <span data-ttu-id="c92a2-147">dotnetcore.exe (.NET SDK 2.0.0+)</span><span class="sxs-lookup"><span data-stu-id="c92a2-147">dotnetcore.exe (.NET SDK 2.0.0+)</span></span>

<span data-ttu-id="c92a2-148">第三方客户端：</span><span class="sxs-lookup"><span data-stu-id="c92a2-148">Third-party clients:</span></span>

- <span data-ttu-id="c92a2-149">JetBrains Rider</span><span class="sxs-lookup"><span data-stu-id="c92a2-149">JetBrains Rider</span></span>
- <span data-ttu-id="c92a2-150">Paket 版本 5.0+</span><span class="sxs-lookup"><span data-stu-id="c92a2-150">Paket version 5.0+</span></span>

<!-- For compatibility with previous dependency-versions page -->
<a name="version-ranges"></a>

## <a name="version-ranges-and-wildcards"></a><span data-ttu-id="c92a2-151">版本范围和通配符</span><span class="sxs-lookup"><span data-stu-id="c92a2-151">Version ranges and wildcards</span></span>

<span data-ttu-id="c92a2-152">引用包依赖项时，NuGet 支持使用间隔表示法来指定版本范围，汇总如下：</span><span class="sxs-lookup"><span data-stu-id="c92a2-152">When referring to package dependencies, NuGet supports using interval notation for specifying version ranges, summarized as follows:</span></span>

| <span data-ttu-id="c92a2-153">Notation</span><span class="sxs-lookup"><span data-stu-id="c92a2-153">Notation</span></span> | <span data-ttu-id="c92a2-154">应用的规则</span><span class="sxs-lookup"><span data-stu-id="c92a2-154">Applied rule</span></span> | <span data-ttu-id="c92a2-155">说明</span><span class="sxs-lookup"><span data-stu-id="c92a2-155">Description</span></span> |
|----------|--------------|-------------|
| <span data-ttu-id="c92a2-156">1.0</span><span class="sxs-lookup"><span data-stu-id="c92a2-156">1.0</span></span> | <span data-ttu-id="c92a2-157">x ≥ 1.0</span><span class="sxs-lookup"><span data-stu-id="c92a2-157">x ≥ 1.0</span></span> | <span data-ttu-id="c92a2-158">最低版本（包含）</span><span class="sxs-lookup"><span data-stu-id="c92a2-158">Minimum version, inclusive</span></span> |
| <span data-ttu-id="c92a2-159">(1.0,)</span><span class="sxs-lookup"><span data-stu-id="c92a2-159">(1.0,)</span></span> | <span data-ttu-id="c92a2-160">x > 1.0</span><span class="sxs-lookup"><span data-stu-id="c92a2-160">x > 1.0</span></span> | <span data-ttu-id="c92a2-161">最低版本（独占）</span><span class="sxs-lookup"><span data-stu-id="c92a2-161">Minimum version, exclusive</span></span> |
| <span data-ttu-id="c92a2-162">[1.0]</span><span class="sxs-lookup"><span data-stu-id="c92a2-162">[1.0]</span></span> | <span data-ttu-id="c92a2-163">x == 1.0</span><span class="sxs-lookup"><span data-stu-id="c92a2-163">x == 1.0</span></span> | <span data-ttu-id="c92a2-164">精确的版本匹配</span><span class="sxs-lookup"><span data-stu-id="c92a2-164">Exact version match</span></span> |
| <span data-ttu-id="c92a2-165">(,1.0]</span><span class="sxs-lookup"><span data-stu-id="c92a2-165">(,1.0]</span></span> | <span data-ttu-id="c92a2-166">x ≤ 1.0</span><span class="sxs-lookup"><span data-stu-id="c92a2-166">x ≤ 1.0</span></span> | <span data-ttu-id="c92a2-167">最高版本（包含）</span><span class="sxs-lookup"><span data-stu-id="c92a2-167">Maximum version, inclusive</span></span> |
| <span data-ttu-id="c92a2-168">(,1.0)</span><span class="sxs-lookup"><span data-stu-id="c92a2-168">(,1.0)</span></span> | <span data-ttu-id="c92a2-169">x < 1.0</span><span class="sxs-lookup"><span data-stu-id="c92a2-169">x < 1.0</span></span> | <span data-ttu-id="c92a2-170">最高版本（独占）</span><span class="sxs-lookup"><span data-stu-id="c92a2-170">Maximum version, exclusive</span></span> |
| <span data-ttu-id="c92a2-171">[1.0,2.0]</span><span class="sxs-lookup"><span data-stu-id="c92a2-171">[1.0,2.0]</span></span> | <span data-ttu-id="c92a2-172">1.0 ≤ x ≤ 2.0</span><span class="sxs-lookup"><span data-stu-id="c92a2-172">1.0 ≤ x ≤ 2.0</span></span> | <span data-ttu-id="c92a2-173">精确范围（包含）</span><span class="sxs-lookup"><span data-stu-id="c92a2-173">Exact range, inclusive</span></span> |
| <span data-ttu-id="c92a2-174">(1.0,2.0)</span><span class="sxs-lookup"><span data-stu-id="c92a2-174">(1.0,2.0)</span></span> | <span data-ttu-id="c92a2-175">1.0 < x < 2.0</span><span class="sxs-lookup"><span data-stu-id="c92a2-175">1.0 < x < 2.0</span></span> | <span data-ttu-id="c92a2-176">精确范围（独占）</span><span class="sxs-lookup"><span data-stu-id="c92a2-176">Exact range, exclusive</span></span> |
| <span data-ttu-id="c92a2-177">[1.0,2.0)</span><span class="sxs-lookup"><span data-stu-id="c92a2-177">[1.0,2.0)</span></span> | <span data-ttu-id="c92a2-178">1.0 ≤ x < 2.0</span><span class="sxs-lookup"><span data-stu-id="c92a2-178">1.0 ≤ x < 2.0</span></span> | <span data-ttu-id="c92a2-179">混合了最低版本（包含）和最高版本（独占）</span><span class="sxs-lookup"><span data-stu-id="c92a2-179">Mixed inclusive minimum and exclusive maximum version</span></span> |
| <span data-ttu-id="c92a2-180">(1.0)</span><span class="sxs-lookup"><span data-stu-id="c92a2-180">(1.0)</span></span>    | <span data-ttu-id="c92a2-181">无效</span><span class="sxs-lookup"><span data-stu-id="c92a2-181">invalid</span></span> | <span data-ttu-id="c92a2-182">无效</span><span class="sxs-lookup"><span data-stu-id="c92a2-182">invalid</span></span> |

<span data-ttu-id="c92a2-183">使用 PackageReference 格式时，NuGet 还支持使用通配符表示法 \* 来表示版本号的主要、次要、修补程序和预发布后缀部分。</span><span class="sxs-lookup"><span data-stu-id="c92a2-183">When using the PackageReference format, NuGet also supports using a wildcard notation, \*, for Major, Minor, Patch, and pre-release suffix parts of the number.</span></span> <span data-ttu-id="c92a2-184">`packages.config` 格式不支持使用通配符。</span><span class="sxs-lookup"><span data-stu-id="c92a2-184">Wildcards are not supported with the `packages.config` format.</span></span>

> [!Note]
> <span data-ttu-id="c92a2-185">PackageReference 中的版本范围包括预发布版本。</span><span class="sxs-lookup"><span data-stu-id="c92a2-185">Version ranges in PackageReference include pre-release versions.</span></span> <span data-ttu-id="c92a2-186">按照设计，可变版本不会解析预发布版本，除非选择加入。</span><span class="sxs-lookup"><span data-stu-id="c92a2-186">By design, floating versions do not resolve prerelease versions unless opted into.</span></span> <span data-ttu-id="c92a2-187">有关相关功能请求的状态，请参阅[问题 6434](https://github.com/NuGet/Home/issues/6434#issuecomment-358782297)。</span><span class="sxs-lookup"><span data-stu-id="c92a2-187">For the status of the related feature request, see [issue 6434](https://github.com/NuGet/Home/issues/6434#issuecomment-358782297).</span></span>

### <a name="examples"></a><span data-ttu-id="c92a2-188">示例</span><span class="sxs-lookup"><span data-stu-id="c92a2-188">Examples</span></span>

<span data-ttu-id="c92a2-189">始终指定项目文件、`packages.config` 文件和 `.nuspec` 文件中的包依赖项的版本或版本范围。</span><span class="sxs-lookup"><span data-stu-id="c92a2-189">Always specify a version or version range for package dependencies in project files, `packages.config` files, and `.nuspec` files.</span></span> <span data-ttu-id="c92a2-190">如果没有版本或版本范围，NuGet 2.8. x 及更早版本会在解析依赖项时选择最新的可用包版本，而 NuGet 3.x 及更高版本会选择最低的包版本。</span><span class="sxs-lookup"><span data-stu-id="c92a2-190">Without a version or version range, NuGet 2.8.x and earlier chooses the latest available package version when resolving a dependency, whereas NuGet 3.x and later chooses the lowest package version.</span></span> <span data-ttu-id="c92a2-191">指定版本或版本范围可以避免这种不确定性。</span><span class="sxs-lookup"><span data-stu-id="c92a2-191">Specifying a version or version range avoids this uncertainty.</span></span>

#### <a name="references-in-project-files-packagereference"></a><span data-ttu-id="c92a2-192">项目文件中的引用 (PackageReference)</span><span class="sxs-lookup"><span data-stu-id="c92a2-192">References in project files (PackageReference)</span></span>

```xml
<!-- Accepts any version 6.1 and above. -->
<PackageReference Include="ExamplePackage" Version="6.1" />

<!-- Accepts any 6.x.y version. -->
<PackageReference Include="ExamplePackage" Version="6.*" />
<PackageReference Include="ExamplePackage" Version="[6,7)" />

<!-- Accepts any version above, but not including 4.1.3. Could be
     used to guarantee a dependency with a specific bug fix. -->
<PackageReference Include="ExamplePackage" Version="(4.1.3,)" />

<!-- Accepts any version up below 5.x, which might be used to prevent pulling in a later
     version of a dependency that changed its interface. However, this form is not
     recommended because it can be difficult to determine the lowest version. -->
<PackageReference Include="ExamplePackage" Version="(,5.0)" />

<!-- Accepts any 1.x or 2.x version, but not 0.x or 3.x and higher. -->
<PackageReference Include="ExamplePackage" Version="[1,3)" />

<!-- Accepts 1.3.2 up to 1.4.x, but not 1.5 and higher. -->
<PackageReference Include="ExamplePackage" Version="[1.3.2,1.5)" />
```

<span data-ttu-id="c92a2-193">**`packages.config` 中的引用：**</span><span class="sxs-lookup"><span data-stu-id="c92a2-193">**References in `packages.config`:**</span></span>

<span data-ttu-id="c92a2-194">在 `packages.config` 中，通过还原包时使用的确切 `version` 属性列出每个依赖项。</span><span class="sxs-lookup"><span data-stu-id="c92a2-194">In `packages.config`, every dependency is listed with an exact `version` attribute that's used when restoring packages.</span></span> <span data-ttu-id="c92a2-195">`allowedVersions` 属性仅在更新操作过程中用于将版本约束到包可能更新到的版本。</span><span class="sxs-lookup"><span data-stu-id="c92a2-195">The `allowedVersions` attribute is used only during update operations to constrain the versions to which the package might be updated.</span></span>

```xml
<!-- Install/restore version 6.1.0, accept any version 6.1.0 and above on update. -->
<package id="ExamplePackage" version="6.1.0" allowedVersions="6.1.0" />

<!-- Install/restore version 6.1.0, and do not change during update. -->
<package id="ExamplePackage" version="6.1.0" allowedVersions="[6.1.0]" />

<!-- Install/restore version 6.1.0, accept any 6.x version during update. -->
<package id="ExamplePackage" version="6.1.0" allowedVersions="[6,7)" />

<!-- Install/restore version 4.1.4, accept any version above, but not including, 4.1.3.
     Could be used to guarantee a dependency with a specific bug fix. -->
<package id="ExamplePackage" version="4.1.4" allowedVersions="(4.1.3,)" />

<!-- Install/restore version 3.1.2, accept any version up below 5.x on update, which might be
     used to prevent pulling in a later version of a dependency that changed its interface.
     However, this form is not recommended because it can be difficult to determine the lowest version. -->
<package id="ExamplePackage" version="3.1.2" allowedVersions="(,5.0)" />

<!-- Install/restore version 1.1.4, accept any 1.x or 2.x version on update, but not
     0.x or 3.x and higher. -->
<package id="ExamplePackage" version="1.1.4" allowedVersions="[1,3)" />

<!-- Install/restore version 1.3.5, accepts 1.3.2 up to 1.4.x on update, but not 1.5 and higher. -->
<package id="ExamplePackage" version="1.3.5" allowedVersions="[1.3.2,1.5)" />
```

<span data-ttu-id="c92a2-196">**`.nuspec` 文件中的引用**</span><span class="sxs-lookup"><span data-stu-id="c92a2-196">**References in `.nuspec` files**</span></span>

<span data-ttu-id="c92a2-197">`<dependency>` 元素中的 `version` 属性描述了依赖项可接受的范围版本。</span><span class="sxs-lookup"><span data-stu-id="c92a2-197">The `version` attribute in a `<dependency>` element describes the range versions that are acceptable for a dependency.</span></span>

```xml
<!-- Accepts any version 6.1 and above. -->
<dependency id="ExamplePackage" version="6.1" />

<!-- Accepts any version above, but not including 4.1.3. Could be
     used to guarantee a dependency with a specific bug fix. -->
<dependency id="ExamplePackage" version="(4.1.3,)" />

<!-- Accepts any version up below 5.x, which might be used to prevent pulling in a later
     version of a dependency that changed its interface. However, this form is not
     recommended because it can be difficult to determine the lowest version. -->
<dependency id="ExamplePackage" version="(,5.0)" />

<!-- Accepts any 1.x or 2.x version, but not 0.x or 3.x and higher. -->
<dependency id="ExamplePackage" version="[1,3)" />

<!-- Accepts 1.3.2 up to 1.4.x, but not 1.5 and higher. -->
<dependency id="ExamplePackage" version="[1.3.2,1.5)" />
```

## <a name="normalized-version-numbers"></a><span data-ttu-id="c92a2-198">规范化的版本号</span><span class="sxs-lookup"><span data-stu-id="c92a2-198">Normalized version numbers</span></span>

> [!Note]
> <span data-ttu-id="c92a2-199">这是 NuGet 3.4 及更高版本的重大更改。</span><span class="sxs-lookup"><span data-stu-id="c92a2-199">This is a breaking change for NuGet 3.4 and later.</span></span>

<span data-ttu-id="c92a2-200">当在安装、重新安装或还原操作过程中从存储库获取包时，NuGet 3.4+ 会按如下所示处理版本号：</span><span class="sxs-lookup"><span data-stu-id="c92a2-200">When obtaining packages from a repository during install, reinstall, or restore operations, NuGet 3.4+ treats version numbers as follows:</span></span>

- <span data-ttu-id="c92a2-201">从版本号中删除前导零：</span><span class="sxs-lookup"><span data-stu-id="c92a2-201">Leading zeroes are removed from version numbers:</span></span>

        1.00 is treated as 1.0
        1.01.1 is treated as 1.1.1
        1.00.0.1 is treated as 1.0.0.1

- <span data-ttu-id="c92a2-202">将忽略版本号第四部分中的零</span><span class="sxs-lookup"><span data-stu-id="c92a2-202">A zero in the fourth part of the version number will be omitted</span></span>

        1.0.0.0 is treated as 1.0.0
        1.0.01.0 is treated as 1.0.1

<span data-ttu-id="c92a2-203">`pack` 和 `restore` 操作可尽可能规范化版本。</span><span class="sxs-lookup"><span data-stu-id="c92a2-203">`pack` and `restore` operations normalize versions whenever possible.</span></span> <span data-ttu-id="c92a2-204">对于已生成的包，此规范化不会影响包本身的版本号；仅影响 NuGet 在解析依赖项时匹配版本的方式。</span><span class="sxs-lookup"><span data-stu-id="c92a2-204">For packages already built, this normalization does not affect the version numbers in the packages themselves; it affects only how NuGet matches versions when resolving dependencies.</span></span>

<span data-ttu-id="c92a2-205">但是，NuGet 包存储库必须以与 NuGet 相同的方式处理这些值，以防止包版本重复。</span><span class="sxs-lookup"><span data-stu-id="c92a2-205">However, NuGet package repositories must treat these values in the same way as NuGet to prevent package version duplication.</span></span> <span data-ttu-id="c92a2-206">因此，包含包版本 1.0 的存储库还不应将版本 1.0.0 作为单独的不同包进行托管   。</span><span class="sxs-lookup"><span data-stu-id="c92a2-206">Thus a repository that contains version *1.0* of a package should not also host version *1.0.0* as a separate and different package.</span></span>
