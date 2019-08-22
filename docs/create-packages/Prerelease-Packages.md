---
title: NuGet 包中的预发行版本
description: 用于生成预发行包的指南
author: karann-msft
ms.author: karann
ms.date: 08/14/2017
ms.topic: conceptual
ms.openlocfilehash: a7d07da30daf3f94db99476b88d9abaad1bb8a07
ms.sourcegitcommit: 7441f12f06ca380feb87c6192ec69f6108f43ee3
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/15/2019
ms.locfileid: "69488856"
---
# <a name="building-pre-release-packages"></a><span data-ttu-id="342cc-103">生成预发行包</span><span class="sxs-lookup"><span data-stu-id="342cc-103">Building pre-release packages</span></span>

<span data-ttu-id="342cc-104">每当发布具有新版本号的更新包时，NuGet 将其视为所示的“最新稳定版本”，以 Visual Studio 中的包管理器 UI 为例：</span><span class="sxs-lookup"><span data-stu-id="342cc-104">Whenever you release an updated package with a new version number, NuGet considers that one as the "latest stable release" as shown, for example in the Package Manager UI within Visual Studio:</span></span>

![显示最新稳定版本的包管理器 UI](media/Prerelease_01-LatestStable.png)

<span data-ttu-id="342cc-106">稳定版本是指被视为足够可靠，可在生产中使用的版本。</span><span class="sxs-lookup"><span data-stu-id="342cc-106">A stable release is one that's considered reliable enough to be used in production.</span></span> <span data-ttu-id="342cc-107">最新稳定版本也指作为包更新安装或在包还原期间安装的版本（受制于[重新安装和更新包](../consume-packages/reinstalling-and-updating-packages.md)中所述的约束）。</span><span class="sxs-lookup"><span data-stu-id="342cc-107">The latest stable release is also the one that will be installed as a package update or during package restore (subject to constraints as described in [Reinstalling and updating packages](../consume-packages/reinstalling-and-updating-packages.md)).</span></span>

<span data-ttu-id="342cc-108">为了支持软件的版本生命周期，NuGet 1.6 及更高版本允许分配预发行包，其中的版本号包括语义化版本控制后缀，如 `-alpha`、`-beta` 或 `-rc`。</span><span class="sxs-lookup"><span data-stu-id="342cc-108">To support the software release lifecycle, NuGet 1.6 and later allows for the distribution of pre-release packages, where the version number includes a semantic versioning suffix such as `-alpha`, `-beta`, or `-rc`.</span></span> <span data-ttu-id="342cc-109">有关详细信息，请参阅[包版本控制](../concepts/package-versioning.md#pre-release-versions)。</span><span class="sxs-lookup"><span data-stu-id="342cc-109">For more information, see [Package versioning](../concepts/package-versioning.md#pre-release-versions).</span></span>

<span data-ttu-id="342cc-110">可以使用以下方法之一来指定此类版本：</span><span class="sxs-lookup"><span data-stu-id="342cc-110">You can specify such versions using one of the following ways:</span></span>

- <span data-ttu-id="342cc-111">**如果项目使用 [`PackageReference`](../consume-packages/package-references-in-project-files.md)** ：在 `.csproj` 文件的 [`PackageVersion`](/dotnet/core/tools/csproj.md#packageversion) 元素中添加语义版本后缀：</span><span class="sxs-lookup"><span data-stu-id="342cc-111">**If your project uses [`PackageReference`](../consume-packages/package-references-in-project-files.md)**: include the semantic version suffix in the `.csproj` file's [`PackageVersion`](/dotnet/core/tools/csproj.md#packageversion) element:</span></span>

    ```xml
    <PropertyGroup>
        <PackageVersion>1.0.1-alpha</PackageVersion>
    </PropertyGroup>
    ```

- <span data-ttu-id="342cc-112">**如果项目使用 [`packages.config`](../reference/packages-config.md) 文件**：在 [`.nuspec`](../reference/nuspec.md) 文件的 [`version`](../reference/nuspec.md#version) 元素中添加语义版本后缀：</span><span class="sxs-lookup"><span data-stu-id="342cc-112">**If your project has a [`packages.config`](../reference/packages-config.md) file**: include the semantic version suffix in the [`.nuspec`](../reference/nuspec.md) file's [`version`](../reference/nuspec.md#version) element:</span></span>

    ```xml
    <version>1.0.1-alpha</version>
    ```

<span data-ttu-id="342cc-113">在准备好发布稳定版本后，只需删除后缀，此包便会优先于任何预发行版本。</span><span class="sxs-lookup"><span data-stu-id="342cc-113">When you're ready to release a stable version, just remove the suffix and the package takes precedence over any pre-release versions.</span></span> <span data-ttu-id="342cc-114">同样，请参阅[包版本控制](../concepts/package-versioning.md#pre-release-versions)。</span><span class="sxs-lookup"><span data-stu-id="342cc-114">Again, see [Package versioning](../concepts/package-versioning.md#pre-release-versions).</span></span>

## <a name="installing-and-updating-pre-release-packages"></a><span data-ttu-id="342cc-115">安装和更新预发行包</span><span class="sxs-lookup"><span data-stu-id="342cc-115">Installing and updating pre-release packages</span></span>

<span data-ttu-id="342cc-116">默认情况下，NuGet 在处理包时不会包括预发行版本，但按照下文所述方法可更改此行为：</span><span class="sxs-lookup"><span data-stu-id="342cc-116">By default, NuGet does not include pre-release versions when working with packages, but you can change this behavior as follows:</span></span>

- <span data-ttu-id="342cc-117">**Visual Studio 中的包管理器 UI**：在“管理 NuGet 包”  UI 中，选中“包括预发行版”  框：</span><span class="sxs-lookup"><span data-stu-id="342cc-117">**Package Manager UI in Visual Studio**: In the **Manage NuGet Packages** UI, check the **Include prerelease** box:</span></span>

    ![Visual Studio 中的“包括预发行版”复选框](media/Prerelease_02-CheckPrerelease.png)

    <span data-ttu-id="342cc-119">设置或清除此框将刷新包管理器 UI 和可安装的可用版本的列表。</span><span class="sxs-lookup"><span data-stu-id="342cc-119">Setting or clearing this box will refresh the Package Manager UI and the list of available versions you can install.</span></span>

- <span data-ttu-id="342cc-120">**包管理器控制台**：将 `-IncludePrerelease` 开关与 `Find-Package`、`Get-Package`、`Install-Package``Sync-Package` 和 `Update-Package` 命令配合使用。</span><span class="sxs-lookup"><span data-stu-id="342cc-120">**Package Manager Console**: Use the `-IncludePrerelease` switch with the `Find-Package`, `Get-Package`, `Install-Package`, `Sync-Package`, and `Update-Package` commands.</span></span> <span data-ttu-id="342cc-121">请参阅 [PowerShell 参考](../reference/powershell-reference.md)。</span><span class="sxs-lookup"><span data-stu-id="342cc-121">Refer to the [PowerShell Reference](../reference/powershell-reference.md).</span></span>

- <span data-ttu-id="342cc-122">**NuGet CLI**：将 `-prerelease` 开关与 `install`、`update`、`delete` 和 `mirror` 命令配合使用。</span><span class="sxs-lookup"><span data-stu-id="342cc-122">**NuGet CLI**: Use the `-prerelease` switch with the `install`, `update`, `delete`, and `mirror` commands.</span></span> <span data-ttu-id="342cc-123">请参阅 [NuGet CLI 参考](../reference/nuget-exe-cli-reference.md)</span><span class="sxs-lookup"><span data-stu-id="342cc-123">Refer to the [NuGet CLI reference](../reference/nuget-exe-cli-reference.md)</span></span>

## <a name="semantic-versioning"></a><span data-ttu-id="342cc-124">语义化版本控制</span><span class="sxs-lookup"><span data-stu-id="342cc-124">Semantic versioning</span></span>

<span data-ttu-id="342cc-125">[语义化版本控制或 SemVer 约定](http://semver.org/spec/v1.0.0.html)介绍如何利用版本号中的字符串传达基础代码的含义。</span><span class="sxs-lookup"><span data-stu-id="342cc-125">The [Semantic Versioning or SemVer convention](http://semver.org/spec/v1.0.0.html) describes how to utilize strings in version numbers to convey the meaning of the underlying code.</span></span>

<span data-ttu-id="342cc-126">在此约定中，每个版本由三部分组成，即 `Major.Minor.Patch`，其含义分别是：</span><span class="sxs-lookup"><span data-stu-id="342cc-126">In this convention, each version has three parts, `Major.Minor.Patch`, with the following meaning:</span></span>

- <span data-ttu-id="342cc-127">`Major`：重大更改</span><span class="sxs-lookup"><span data-stu-id="342cc-127">`Major`: Breaking changes</span></span>
- <span data-ttu-id="342cc-128">`Minor`：新增功能，但可向后兼容</span><span class="sxs-lookup"><span data-stu-id="342cc-128">`Minor`: New features, but backwards compatible</span></span>
- <span data-ttu-id="342cc-129">`Patch`：仅可向后兼容的 bug 修复</span><span class="sxs-lookup"><span data-stu-id="342cc-129">`Patch`: Backwards compatible bug fixes only</span></span>

<span data-ttu-id="342cc-130">然后，通过在修补程序编号后追加连字符和字符串表示预发行版本。</span><span class="sxs-lookup"><span data-stu-id="342cc-130">Pre-release versions are then denoted by appending a hyphen and a string after the patch number.</span></span> <span data-ttu-id="342cc-131">从技术上说，可在连字符后使用任意  字符串，NuGet 都会将包视为预发行版。</span><span class="sxs-lookup"><span data-stu-id="342cc-131">Technically speaking, you can use *any* string after the hyphen and NuGet will treat the package as pre-release.</span></span> <span data-ttu-id="342cc-132">然后，NuGet 在适用的 UI 中显示完整的版本号，供使用者自己解读其含义。</span><span class="sxs-lookup"><span data-stu-id="342cc-132">NuGet then displays the full version number in the applicable UI, leaving consumers to interpret the meaning for themselves.</span></span>

<span data-ttu-id="342cc-133">出于这种考虑，通常最好遵照如下所示的公认命名约定：</span><span class="sxs-lookup"><span data-stu-id="342cc-133">With this in mind, it's generally good to follow recognized naming conventions such as the following:</span></span>

- <span data-ttu-id="342cc-134">`-alpha`：Alpha 版本，通常用于在制品和试验品</span><span class="sxs-lookup"><span data-stu-id="342cc-134">`-alpha`: Alpha release, typically used for work-in-progress and experimentation</span></span>
- <span data-ttu-id="342cc-135">`-beta`：Beta 版本，通常指可用于下一计划版本的功能完整的版本，但可能包含已知 bug。</span><span class="sxs-lookup"><span data-stu-id="342cc-135">`-beta`: Beta release, typically one that is feature complete for the next planned release, but may contain known bugs.</span></span>
- <span data-ttu-id="342cc-136">`-rc`：候选发布，通常可能为最终（稳定）版本，除非出现重大 bug。</span><span class="sxs-lookup"><span data-stu-id="342cc-136">`-rc`: Release candidate, typically a release that's potentially final (stable) unless significant bugs emerge.</span></span>

> [!Note]
> <span data-ttu-id="342cc-137">NuGet 4.3.0+ 支持[语义化版本控制 v2.0.0](http://semver.org/spec/v2.0.0.html)，后者支持采用点表示法的预发布号，如 `1.0.1-build.23` 中所示。</span><span class="sxs-lookup"><span data-stu-id="342cc-137">NuGet 4.3.0+ supports [Semantic Versioning v2.0.0](http://semver.org/spec/v2.0.0.html), which supports pre-release numbers with dot notation, as in `1.0.1-build.23`.</span></span> <span data-ttu-id="342cc-138">NuGet 4.3.0 之前的版本不支持点表示法。</span><span class="sxs-lookup"><span data-stu-id="342cc-138">Dot notation is not supported with NuGet versions before 4.3.0.</span></span> <span data-ttu-id="342cc-139">在 NuGet 的早期版本中，可以使用 `1.0.1-build23` 之类的格式，但这始终被视为预发布版本。</span><span class="sxs-lookup"><span data-stu-id="342cc-139">In earlier versions of NuGet, you could use a form like `1.0.1-build23` but this was always considered a pre-release version.</span></span>

<span data-ttu-id="342cc-140">但是，无论使用何种后缀，NuGet 都会按照反向字母顺序向它们赋予优先级：</span><span class="sxs-lookup"><span data-stu-id="342cc-140">Whatever suffixes you use, however, NuGet will give them precedence in reverse alphabetical order:</span></span>

    1.0.1
    1.0.1-zzz
    1.0.1-rc
    1.0.1-open
    1.0.1-beta.12
    1.0.1-beta.5
    1.0.1-beta
    1.0.1-alpha.2
    1.0.1-alpha

<span data-ttu-id="342cc-141">如上所示，没有任何后缀的版本始终优先于预发行版本。</span><span class="sxs-lookup"><span data-stu-id="342cc-141">As shown, the version without any suffix will always take precedence over pre-release versions.</span></span>

<span data-ttu-id="342cc-142">semver2 不需要前导 0，但它们与旧版本架构一致。</span><span class="sxs-lookup"><span data-stu-id="342cc-142">Leading 0s are not needed with semver2, but they are with the old version schema.</span></span> <span data-ttu-id="342cc-143">如果在可能使用两位数（或更多数字）的预发行版本标记中使用数字后缀，请使用前导零，如 beta.01 和 beta.05，以便确保数字增大时，可以正确地进行排序。</span><span class="sxs-lookup"><span data-stu-id="342cc-143">If you use numerical suffixes with pre-release tags that might use double-digit numbers (or more), use leading zeroes as in beta.01 and beta.05 to ensure that they sort correctly when the numbers get larger.</span></span> <span data-ttu-id="342cc-144">此建议仅适用于旧版架构。</span><span class="sxs-lookup"><span data-stu-id="342cc-144">This recommendation only applies to the old version schema.</span></span>
