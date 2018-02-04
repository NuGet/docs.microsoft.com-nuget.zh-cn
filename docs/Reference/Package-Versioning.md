---
title: "NuGet 程序包版本引用 |Microsoft 文档"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 12/08/2017
ms.topic: reference
ms.prod: nuget
ms.technology: 
description: "指定版本号和其他包 NuGet 包依赖，和如何安装依赖关系后的范围的准确详细信息。"
keywords: "版本控制、 NuGet 包依赖项、 NuGet 依赖项版本、 NuGet 版本数字、 NuGet 程序包版本、 版本范围、 版本规范、 规范化的版本号"
ms.reviewer:
- anandr
- karann-msft
- unniravindranathan
ms.openlocfilehash: 70472d7d97d073009237a047e0fdf528b221dfd0
ms.sourcegitcommit: 4651b16a3a08f6711669fc4577f5d63b600f8f58
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/02/2018
---
# <a name="package-versioning"></a><span data-ttu-id="dfdee-104">包版本控制</span><span class="sxs-lookup"><span data-stu-id="dfdee-104">Package versioning</span></span>

<span data-ttu-id="dfdee-105">特定包始终指使用其包标识符和确切的版本号。</span><span class="sxs-lookup"><span data-stu-id="dfdee-105">A specific package is always referred to using its package identifier and an exact version number.</span></span> <span data-ttu-id="dfdee-106">例如，[实体框架](https://www.nuget.org/packages/EntityFramework/)nuget.org 上具有多个装入数十： 特定包可用，范围从版本*4.1.10311*到版本*6.1.3* （最新稳定释放） 等各种预发行版本，以及将*6.2.0-beta1*。</span><span class="sxs-lookup"><span data-stu-id="dfdee-106">For example, [Entity Framework](https://www.nuget.org/packages/EntityFramework/) on nuget.org has several dozen specific packages available, ranging from version *4.1.10311* to version *6.1.3* (the latest stable release) and a variety of pre-release versions like *6.2.0-beta1*.</span></span>

<span data-ttu-id="dfdee-107">创建包时，则指定可选的预发行版文本后缀的特定版本号。</span><span class="sxs-lookup"><span data-stu-id="dfdee-107">When creating a package, you assign a specific version number with an optional pre-release text suffix.</span></span> <span data-ttu-id="dfdee-108">另一方面，在使用包，可以指定确切的版本号或一系列可接受的版本。</span><span class="sxs-lookup"><span data-stu-id="dfdee-108">When consuming packages, on the other hand, you can specify either an exact version number or a range of acceptable versions.</span></span>

<span data-ttu-id="dfdee-109">本主题内容：</span><span class="sxs-lookup"><span data-stu-id="dfdee-109">In this topic:</span></span>

- <span data-ttu-id="dfdee-110">[版本基础知识](#version-basics)包括预发行后缀。</span><span class="sxs-lookup"><span data-stu-id="dfdee-110">[Version basics](#version-basics) including pre-release suffixes.</span></span>
- [<span data-ttu-id="dfdee-111">版本范围和通配符</span><span class="sxs-lookup"><span data-stu-id="dfdee-111">Version ranges and wildcards</span></span>](#version-ranges-and-wildcards)
- [<span data-ttu-id="dfdee-112">规范化的版本号</span><span class="sxs-lookup"><span data-stu-id="dfdee-112">Normalized version numbers</span></span>](#normalized-version-numbers)

## <a name="version-basics"></a><span data-ttu-id="dfdee-113">版本基础知识</span><span class="sxs-lookup"><span data-stu-id="dfdee-113">Version basics</span></span>

<span data-ttu-id="dfdee-114">在窗体中的特定版本号是*Major.Minor.Patch [-后缀]*，其中的组件具有以下含义：</span><span class="sxs-lookup"><span data-stu-id="dfdee-114">A specific version number is in the form *Major.Minor.Patch[-Suffix]*, where the components have the following meanings:</span></span>

- <span data-ttu-id="dfdee-115">*主要*： 重大更改</span><span class="sxs-lookup"><span data-stu-id="dfdee-115">*Major*: Breaking changes</span></span>
- <span data-ttu-id="dfdee-116">*次要*： 新功能，但向后兼容</span><span class="sxs-lookup"><span data-stu-id="dfdee-116">*Minor*: New features, but backwards compatible</span></span>
- <span data-ttu-id="dfdee-117">*修补程序*： 向后兼容 bug 修复</span><span class="sxs-lookup"><span data-stu-id="dfdee-117">*Patch*: Backwards compatible bug fixes only</span></span>
- <span data-ttu-id="dfdee-118">*-后缀*（可选）： 连字符后跟表示的预发行版本字符串 (以下[语义版本控制或 SemVer 1.0 约定](http://semver.org/spec/v1.0.0.html))。</span><span class="sxs-lookup"><span data-stu-id="dfdee-118">*-Suffix* (optional): a hyphen followed by a string denoting a pre-release version (following the [Semantic Versioning or SemVer 1.0 convention](http://semver.org/spec/v1.0.0.html)).</span></span>

<span data-ttu-id="dfdee-119">**示例：**</span><span class="sxs-lookup"><span data-stu-id="dfdee-119">**Examples:**</span></span>

    1.0.1
    6.11.1231
    4.3.1-rc
    2.2.44-beta1

> [!Important]
> <span data-ttu-id="dfdee-120">nuget.org 拒绝任何缺少的确切的版本号的程序包上载。</span><span class="sxs-lookup"><span data-stu-id="dfdee-120">nuget.org rejects any package upload that lacks an exact version number.</span></span> <span data-ttu-id="dfdee-121">必须在指定的版本`.nuspec`或用于创建包的项目文件。</span><span class="sxs-lookup"><span data-stu-id="dfdee-121">The version must be specified in the `.nuspec` or project file used to create the package.</span></span>

### <a name="pre-release-versions"></a><span data-ttu-id="dfdee-122">预发布版本</span><span class="sxs-lookup"><span data-stu-id="dfdee-122">Pre-release versions</span></span>

<span data-ttu-id="dfdee-123">从技术角度讲，包创建者可以使用任何字符串作为后缀来表示的预发行版本，NuGet 将视为预发行版的任何此类版本，会不使任何其他解释。</span><span class="sxs-lookup"><span data-stu-id="dfdee-123">Technically speaking, package creators can use any string as a suffix to denote a pre-release version, as NuGet treats any such version as pre-release and makes no other interpretation.</span></span> <span data-ttu-id="dfdee-124">也就是说，涉及 NuGet 显示任何 UI 中的完整版本字符串，请保留的后缀含义任何解释为使用者。</span><span class="sxs-lookup"><span data-stu-id="dfdee-124">That is, NuGet displays the full version string in whatever UI is involved, leaving any interpretation of the suffix's meaning to the consumer.</span></span>

<span data-ttu-id="dfdee-125">话虽如此，但包开发人员通常遵循识别的命名约定：</span><span class="sxs-lookup"><span data-stu-id="dfdee-125">That said, package developers generally follow recognized naming conventions:</span></span>

- <span data-ttu-id="dfdee-126">`-alpha`: Alpha 版本中，通常用于工作进度和实验。</span><span class="sxs-lookup"><span data-stu-id="dfdee-126">`-alpha`: Alpha release, typically used for work-in-progress and experimentation.</span></span>
- <span data-ttu-id="dfdee-127">`-beta`：Beta 版本，通常指可用于下一计划版本的功能完整的版本，但可能包含已知 bug。</span><span class="sxs-lookup"><span data-stu-id="dfdee-127">`-beta`: Beta release, typically one that is feature complete for the next planned release, but may contain known bugs.</span></span>
- <span data-ttu-id="dfdee-128">`-rc`：候选发布，通常可能为最终（稳定）版本，除非出现重大 bug。</span><span class="sxs-lookup"><span data-stu-id="dfdee-128">`-rc`: Release candidate, typically a release that's potentially final (stable) unless significant bugs emerge.</span></span>

> [!Note]
> <span data-ttu-id="dfdee-129">NuGet 4.3.0+ 支持[SemVer 2.0.0](http://semver.org/spec/v2.0.0.html)，它支持使用点表示法的预发行版号作为 in *1.0.1-build.23*。</span><span class="sxs-lookup"><span data-stu-id="dfdee-129">NuGet 4.3.0+ supports [SemVer 2.0.0](http://semver.org/spec/v2.0.0.html), which supports pre-release numbers with dot notation, as in *1.0.1-build.23*.</span></span> <span data-ttu-id="dfdee-130">与之前 4.3.0 的 NuGet 版本不支持点表示法。</span><span class="sxs-lookup"><span data-stu-id="dfdee-130">Dot notation is not supported with NuGet versions before 4.3.0.</span></span> <span data-ttu-id="dfdee-131">你可以使用窗体为*1.0.1-build23*。</span><span class="sxs-lookup"><span data-stu-id="dfdee-131">You can use a form like *1.0.1-build23*.</span></span>

<span data-ttu-id="dfdee-132">当解决包引用和多个包版本的差异仅在于后缀，NuGet 首先，选择不带后缀的版本，然后应用优先预发行版本按反向字母顺序。</span><span class="sxs-lookup"><span data-stu-id="dfdee-132">When resolving package references and multiple package versions differ only by suffix, NuGet chooses a version without a suffix first, then applies precedence to pre-release versions in reverse alphabetical order.</span></span> <span data-ttu-id="dfdee-133">例如，将显示的确切顺序选择以下版本：</span><span class="sxs-lookup"><span data-stu-id="dfdee-133">For example, the following versions would be chosen in the exact order shown:</span></span>

    1.0.1
    1.0.1-zzz
    1.0.1-rc
    1.0.1-open
    1.0.1-beta
    1.0.1-alpha2
    1.0.1-alpha
    1.0.1-aaa

## <a name="semantic-versioning-200"></a><span data-ttu-id="dfdee-134">语义版本控制 2.0.0</span><span class="sxs-lookup"><span data-stu-id="dfdee-134">Semantic Versioning 2.0.0</span></span>

<span data-ttu-id="dfdee-135">使用 NuGet 4.3.0+ 和 Visual Studio 2017 15.3 以上版本，支持 NuGet[语义版本控制 2.0.0](http://semver.org/spec/v2.0.0.html)。</span><span class="sxs-lookup"><span data-stu-id="dfdee-135">With NuGet 4.3.0+ and Visual Studio 2017 version 15.3+, NuGet supports [Semantic Versioning 2.0.0](http://semver.org/spec/v2.0.0.html).</span></span>

<span data-ttu-id="dfdee-136">在较旧的客户端中不支持某些语义 SemVer 2.0.0 版。</span><span class="sxs-lookup"><span data-stu-id="dfdee-136">Certain semantics of SemVer v2.0.0 are not supported in older clients.</span></span> <span data-ttu-id="dfdee-137">NuGet 要考虑为特定的 SemVer 2.0.0 版，如果以下语句之一为 true 的包版本：</span><span class="sxs-lookup"><span data-stu-id="dfdee-137">NuGet considers a package version to be SemVer v2.0.0 specific if either of the following statements is true:</span></span>

- <span data-ttu-id="dfdee-138">预发行版标签是点分隔的例如， *1.0.0-alpha.1*</span><span class="sxs-lookup"><span data-stu-id="dfdee-138">The pre-release label is dot-separated, for example, *1.0.0-alpha.1*</span></span>
- <span data-ttu-id="dfdee-139">例如，扩展的版本具有生成的元数据， *1.0.0+githash*</span><span class="sxs-lookup"><span data-stu-id="dfdee-139">The version has build-metadata, for example, *1.0.0+githash*</span></span>

<span data-ttu-id="dfdee-140">对于 nuget.org，包被定义为 SemVer 2.0.0 版包中，如果以下语句之一为 true:</span><span class="sxs-lookup"><span data-stu-id="dfdee-140">For nuget.org, a package is defined as a SemVer v2.0.0 package if either of the following statements is true:</span></span>

- <span data-ttu-id="dfdee-141">包的版本是符合 SemVer 2.0.0 版，但不是 SemVer v1.0.0 符合，如上文所定义。</span><span class="sxs-lookup"><span data-stu-id="dfdee-141">The package's own version is SemVer v2.0.0 compliant but not SemVer v1.0.0 compliant, as defined above.</span></span>
- <span data-ttu-id="dfdee-142">任何包的依赖项版本范围必须是符合 SemVer 2.0.0 版，但不是符合，SemVer v1.0.0; 上面定义的最小值或最大版本例如， *[1.0.0-alpha.1,)*。</span><span class="sxs-lookup"><span data-stu-id="dfdee-142">Any of the package's dependency version ranges has a minimum or maximum version that is SemVer v2.0.0 compliant but not SemVer v1.0.0 compliant, defined above; for example, *[1.0.0-alpha.1, )*.</span></span>

<span data-ttu-id="dfdee-143">如果将 SemVer 2.0.0 版特定包上载到 nuget.org 中时，包已向旧客户端不可见并且可用于仅以下 NuGet 客户端：</span><span class="sxs-lookup"><span data-stu-id="dfdee-143">If you upload a SemVer v2.0.0-specific package to nuget.org, the package is invisible to older clients and available to only the following NuGet clients:</span></span>

- <span data-ttu-id="dfdee-144">NuGet 4.3.0+</span><span class="sxs-lookup"><span data-stu-id="dfdee-144">NuGet 4.3.0+</span></span>
- <span data-ttu-id="dfdee-145">Visual Studio 2017 version 15.3+</span><span class="sxs-lookup"><span data-stu-id="dfdee-145">Visual Studio 2017 version 15.3+</span></span>
- <span data-ttu-id="dfdee-146">Visual Studio 2015 [NuGet VSIX v3.6.0](https://dist.nuget.org/visualstudio-2015-vsix/latest/NuGet.Tools.vsix)</span><span class="sxs-lookup"><span data-stu-id="dfdee-146">Visual Studio 2015 with [NuGet VSIX v3.6.0](https://dist.nuget.org/visualstudio-2015-vsix/latest/NuGet.Tools.vsix)</span></span>
- <span data-ttu-id="dfdee-147">dotnet.exe (.NET SDK 2.0.0+)</span><span class="sxs-lookup"><span data-stu-id="dfdee-147">dotnet.exe (.NET SDK 2.0.0+)</span></span>

<span data-ttu-id="dfdee-148">第三方客户端：</span><span class="sxs-lookup"><span data-stu-id="dfdee-148">Third-party clients:</span></span>

- <span data-ttu-id="dfdee-149">JetBrains 附件</span><span class="sxs-lookup"><span data-stu-id="dfdee-149">JetBrains Rider</span></span>
- <span data-ttu-id="dfdee-150">Paket 版本 5.0 +</span><span class="sxs-lookup"><span data-stu-id="dfdee-150">Paket version 5.0+</span></span>

<!-- For compatibility with previous dependency-versions page -->
<a name="version-ranges"></a>

## <a name="version-ranges-and-wildcards"></a><span data-ttu-id="dfdee-151">版本范围和通配符</span><span class="sxs-lookup"><span data-stu-id="dfdee-151">Version ranges and wildcards</span></span>

<span data-ttu-id="dfdee-152">当引用包的依赖项，NuGet 将支持使用间隔表示法指定版本范围，汇总为如下：</span><span class="sxs-lookup"><span data-stu-id="dfdee-152">When referring to package dependencies, NuGet supports using interval notation for specifying version ranges, summarized as follows:</span></span>

| <span data-ttu-id="dfdee-153">Notation</span><span class="sxs-lookup"><span data-stu-id="dfdee-153">Notation</span></span> | <span data-ttu-id="dfdee-154">已应用的规则</span><span class="sxs-lookup"><span data-stu-id="dfdee-154">Applied rule</span></span> | <span data-ttu-id="dfdee-155">描述</span><span class="sxs-lookup"><span data-stu-id="dfdee-155">Description</span></span> |
|----------|--------------|-------------|
| <span data-ttu-id="dfdee-156">1.0</span><span class="sxs-lookup"><span data-stu-id="dfdee-156">1.0</span></span> | <span data-ttu-id="dfdee-157">1.0 ≤ x</span><span class="sxs-lookup"><span data-stu-id="dfdee-157">1.0 ≤ x</span></span> | <span data-ttu-id="dfdee-158">非独占的最低版本</span><span class="sxs-lookup"><span data-stu-id="dfdee-158">Minimum version, inclusive</span></span> |
| <span data-ttu-id="dfdee-159">(1.0,)</span><span class="sxs-lookup"><span data-stu-id="dfdee-159">(1.0,)</span></span> | <span data-ttu-id="dfdee-160">1.0 < x</span><span class="sxs-lookup"><span data-stu-id="dfdee-160">1.0 < x</span></span> | <span data-ttu-id="dfdee-161">独占的最低版本</span><span class="sxs-lookup"><span data-stu-id="dfdee-161">Minimum version, exclusive</span></span> |
| <span data-ttu-id="dfdee-162">[1.0]</span><span class="sxs-lookup"><span data-stu-id="dfdee-162">[1.0]</span></span> | <span data-ttu-id="dfdee-163">x == 1.0</span><span class="sxs-lookup"><span data-stu-id="dfdee-163">x == 1.0</span></span> | <span data-ttu-id="dfdee-164">精确版本匹配</span><span class="sxs-lookup"><span data-stu-id="dfdee-164">Exact version match</span></span> |
| <span data-ttu-id="dfdee-165">(,1.0]</span><span class="sxs-lookup"><span data-stu-id="dfdee-165">(,1.0]</span></span> | <span data-ttu-id="dfdee-166">x ≤ 1.0</span><span class="sxs-lookup"><span data-stu-id="dfdee-166">x ≤ 1.0</span></span> | <span data-ttu-id="dfdee-167">非独占的最高版本</span><span class="sxs-lookup"><span data-stu-id="dfdee-167">Maximum version, inclusive</span></span> |
| <span data-ttu-id="dfdee-168">(,1.0)</span><span class="sxs-lookup"><span data-stu-id="dfdee-168">(,1.0)</span></span> | <span data-ttu-id="dfdee-169">x < 1.0</span><span class="sxs-lookup"><span data-stu-id="dfdee-169">x < 1.0</span></span> | <span data-ttu-id="dfdee-170">独占的最高版本</span><span class="sxs-lookup"><span data-stu-id="dfdee-170">Maximum version, exclusive</span></span> |
| <span data-ttu-id="dfdee-171">[1.0,2.0]</span><span class="sxs-lookup"><span data-stu-id="dfdee-171">[1.0,2.0]</span></span> | <span data-ttu-id="dfdee-172">1.0 ≤ x ≤ 2.0</span><span class="sxs-lookup"><span data-stu-id="dfdee-172">1.0 ≤ x ≤ 2.0</span></span> | <span data-ttu-id="dfdee-173">非独占的确切范围</span><span class="sxs-lookup"><span data-stu-id="dfdee-173">Exact range, inclusive</span></span> |
| <span data-ttu-id="dfdee-174">(1.0,2.0)</span><span class="sxs-lookup"><span data-stu-id="dfdee-174">(1.0,2.0)</span></span> | <span data-ttu-id="dfdee-175">1.0 < x < 2.0</span><span class="sxs-lookup"><span data-stu-id="dfdee-175">1.0 < x < 2.0</span></span> | <span data-ttu-id="dfdee-176">确切的范围独占</span><span class="sxs-lookup"><span data-stu-id="dfdee-176">Exact range, exclusive</span></span> |
| <span data-ttu-id="dfdee-177">[1.0,2.0)</span><span class="sxs-lookup"><span data-stu-id="dfdee-177">[1.0,2.0)</span></span> | <span data-ttu-id="dfdee-178">1.0 ≤ x < 2.0</span><span class="sxs-lookup"><span data-stu-id="dfdee-178">1.0 ≤ x < 2.0</span></span> | <span data-ttu-id="dfdee-179">混合的非独占最小值和独占最高版本</span><span class="sxs-lookup"><span data-stu-id="dfdee-179">Mixed inclusive minimum and exclusive maximum version</span></span> |
| <span data-ttu-id="dfdee-180">(1.0)</span><span class="sxs-lookup"><span data-stu-id="dfdee-180">(1.0)</span></span>    | <span data-ttu-id="dfdee-181">无效</span><span class="sxs-lookup"><span data-stu-id="dfdee-181">invalid</span></span> | <span data-ttu-id="dfdee-182">无效</span><span class="sxs-lookup"><span data-stu-id="dfdee-182">invalid</span></span> |

<span data-ttu-id="dfdee-183">使用 PackageReference 格式时，NuGet 还支持使用通配符表示法， \*、 主要、 次要、 修补程序，和的数的预发行后缀部分。</span><span class="sxs-lookup"><span data-stu-id="dfdee-183">When using the PackageReference format, NuGet also supports using a wildcard notation, \*, for Major, Minor, Patch, and pre-release suffix parts of the number.</span></span> <span data-ttu-id="dfdee-184">不支持通配符`packages.config`格式。</span><span class="sxs-lookup"><span data-stu-id="dfdee-184">Wildcards are not supported with the `packages.config` format.</span></span>

> [!Note]
> <span data-ttu-id="dfdee-185">在解析版本范围时，将不包括预发行版本。</span><span class="sxs-lookup"><span data-stu-id="dfdee-185">Pre-release versions are not included when resolving version ranges.</span></span> <span data-ttu-id="dfdee-186">预发布版本*是*时使用通配符，包括 (\*)。</span><span class="sxs-lookup"><span data-stu-id="dfdee-186">Pre-release versions *are* included when using a wildcard (\*).</span></span> <span data-ttu-id="dfdee-187">版本范围*[1.0,2.0]*，例如，不包括 2.0 beta，但通配符表示法_2.0-\*_未。</span><span class="sxs-lookup"><span data-stu-id="dfdee-187">The version range *[1.0,2.0]*, for example, does not include 2.0-beta, but the wildcard notation _2.0-\*_ does.</span></span> <span data-ttu-id="dfdee-188">请参阅[发出 912](https://github.com/NuGet/Home/issues/912)有关预发行通配符的进一步讨论。</span><span class="sxs-lookup"><span data-stu-id="dfdee-188">See [issue 912](https://github.com/NuGet/Home/issues/912) for further discussion on pre-release wildcards.</span></span>

### <a name="examples"></a><span data-ttu-id="dfdee-189">示例</span><span class="sxs-lookup"><span data-stu-id="dfdee-189">Examples</span></span>

<span data-ttu-id="dfdee-190">始终在项目文件中指定某个版本或包的依赖项的版本范围`packages.config`文件，和`.nuspec`文件。</span><span class="sxs-lookup"><span data-stu-id="dfdee-190">Always specify a version or version range for package dependencies in project files, `packages.config` files, and `.nuspec` files.</span></span> <span data-ttu-id="dfdee-191">不带版本或版本范围，NuGet 2.8.x 和前面选择的最新的可用程序包版本时解决一个依赖项，而 NuGet 3.x 和更高版本选择的最低的包版本。</span><span class="sxs-lookup"><span data-stu-id="dfdee-191">Without a version or version range, NuGet 2.8.x and earlier chooses the latest available package version when resolving a dependency, whereas NuGet 3.x and later chooses the lowest package version.</span></span> <span data-ttu-id="dfdee-192">指定的版本或范围可避免这种不确定性的版本。</span><span class="sxs-lookup"><span data-stu-id="dfdee-192">Specifying a version or version range avoids this uncertainty.</span></span>

#### <a name="references-in-project-files-packagereference"></a><span data-ttu-id="dfdee-193">在项目文件 (PackageReference) 中的引用</span><span class="sxs-lookup"><span data-stu-id="dfdee-193">References in project files (PackageReference)</span></span>

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

<!-- Accepts 1.3.2 up to 1.4.x, but not 1.5 and higher. -->
<PackageReference Include="ExamplePackage" Version="[1.3.2,1.5)" />
```

<span data-ttu-id="dfdee-194">**在引用`packages.config`:**</span><span class="sxs-lookup"><span data-stu-id="dfdee-194">**References in `packages.config`:**</span></span>

<span data-ttu-id="dfdee-195">在`packages.config`，每个依赖项列出与确切`version`在还原包时使用的属性。</span><span class="sxs-lookup"><span data-stu-id="dfdee-195">In `packages.config`, every dependency is listed with an exact `version` attribute that's used when restoring packages.</span></span> <span data-ttu-id="dfdee-196">`allowedVersions`属性仅在更新操作期间使用来约束可能会向其更新的包的版本。</span><span class="sxs-lookup"><span data-stu-id="dfdee-196">The `allowedVersions` attribute is used only during update operations to constrain the versions to which the package might be updated.</span></span>

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

<span data-ttu-id="dfdee-197">**在引用`.nuspec`文件**</span><span class="sxs-lookup"><span data-stu-id="dfdee-197">**References in `.nuspec` files**</span></span>

<span data-ttu-id="dfdee-198">`version`属性中`<dependency>`元素描述的某个依赖项可接受的范围版本。</span><span class="sxs-lookup"><span data-stu-id="dfdee-198">The `version` attribute in a `<dependency>` element describes the range versions that are acceptable for a dependency.</span></span>

```xml
<!-- Accepts any version 6.1 and above. -->
<dependency id="ExamplePackage" version="6.1" />

<!-- Accepts any 6.x.y version. -->
<dependency id="ExamplePackage" version="6.*" />

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

## <a name="normalized-version-numbers"></a><span data-ttu-id="dfdee-199">规范化的版本号</span><span class="sxs-lookup"><span data-stu-id="dfdee-199">Normalized version numbers</span></span>

> [!Note]
> <span data-ttu-id="dfdee-200">这是一项重大更改 NuGet 3.4 及更高版本。</span><span class="sxs-lookup"><span data-stu-id="dfdee-200">This is a breaking change for NuGet 3.4 and later.</span></span>

<span data-ttu-id="dfdee-201">当包从存储库获取期间安装，请重新安装，或还原操作，NuGet 3.4 +，如下所示处理版本号：</span><span class="sxs-lookup"><span data-stu-id="dfdee-201">When obtaining packages from a repository during install, reinstall, or restore operations, NuGet 3.4+ treats version numbers as follows:</span></span>

- <span data-ttu-id="dfdee-202">前导零会从版本号：</span><span class="sxs-lookup"><span data-stu-id="dfdee-202">Leading zeroes are removed from version numbers:</span></span>

        1.00 is treated as 1.0
        1.01.1 is treated as 1.1.1
        1.00.0.1 is treated as 1.0.0.1

- <span data-ttu-id="dfdee-203">将省略的版本号的第四个部分中零</span><span class="sxs-lookup"><span data-stu-id="dfdee-203">A zero in the fourth part of the version number will be omitted</span></span>

        1.0.0.0 is treated as 1.0.0
        1.0.01.0 is treated as 1.0.1

<span data-ttu-id="dfdee-204">此正则化不会影响包本身; 中的版本号它会影响仅如何 NuGet 版本时匹配解析的依赖关系。</span><span class="sxs-lookup"><span data-stu-id="dfdee-204">This normalization does not affect the version numbers in the packages themselves; it affects only how NuGet matches versions when resolving dependencies.</span></span>

<span data-ttu-id="dfdee-205">但是，NuGet 包存储库必须作为 NuGet 相同方式来防止包版本重复处理这些值。</span><span class="sxs-lookup"><span data-stu-id="dfdee-205">However, NuGet package repositories must treat these values in the same way as NuGet to prevent package version duplication.</span></span> <span data-ttu-id="dfdee-206">因此的存储库包含版本*1.0*的包不还会托管版本*1.0.0*以分别进行不同的包的形式。</span><span class="sxs-lookup"><span data-stu-id="dfdee-206">Thus a repository that contains version *1.0* of a package should not also host version *1.0.0* as a separate and different package.</span></span>
