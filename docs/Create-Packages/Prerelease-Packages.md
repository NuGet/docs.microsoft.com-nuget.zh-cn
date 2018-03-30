---
title: NuGet 包中的预发行版本 | Microsoft Docs
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 08/14/2017
ms.topic: article
ms.prod: nuget
ms.technology: ''
description: 用于生成预发行包的指南
keywords: 版本控制, NuGet 包版本控制, NuGet 预发行版本, NuGet 预发行包, 预览包版本, RC 包版本, Beta 包版本, NuGet 语义化版本控制
ms.reviewer:
- karann-msft
- unniravindranathan
ms.workload:
- dotnet
- aspnet
ms.openlocfilehash: 57f59e3906e2d49b6b6e078f530885a601553b06
ms.sourcegitcommit: beb229893559824e8abd6ab16707fd5fe1c6ac26
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/28/2018
---
# <a name="building-pre-release-packages"></a><span data-ttu-id="613ba-104">生成预发行包</span><span class="sxs-lookup"><span data-stu-id="613ba-104">Building pre-release packages</span></span>

<span data-ttu-id="613ba-105">每当发布具有新版本号的更新包时，NuGet 将其视为所示的“最新稳定版本”，以 Visual Studio 中的包管理器 UI 为例：</span><span class="sxs-lookup"><span data-stu-id="613ba-105">Whenever you release an updated package with a new version number, NuGet considers that one as the "latest stable release" as shown, for example in the Package Manager UI within Visual Studio:</span></span>

![显示最新稳定版本的包管理器 UI](media/Prerelease_01-LatestStable.png)

<span data-ttu-id="613ba-107">稳定版本是指被视为足够可靠，可在生产中使用的版本。</span><span class="sxs-lookup"><span data-stu-id="613ba-107">A stable release is one that's considered reliable enough to be used in production.</span></span> <span data-ttu-id="613ba-108">最新稳定版本也指作为包更新安装或在包还原期间安装的版本（受制于[重新安装和更新包](../consume-packages/reinstalling-and-updating-packages.md)中所述的约束）。</span><span class="sxs-lookup"><span data-stu-id="613ba-108">The latest stable release is also the one that will be installed as a package update or during package restore (subject to constraints as described in [Reinstalling and updating packages](../consume-packages/reinstalling-and-updating-packages.md)).</span></span>

<span data-ttu-id="613ba-109">为了支持软件的版本生命周期，NuGet 1.6 及更高版本允许分配预发行包，其中的版本号包括语义化版本控制后缀，如 `-alpha`、`-beta` 或 `-rc`。</span><span class="sxs-lookup"><span data-stu-id="613ba-109">To support the software release lifecycle, NuGet 1.6 and later allows for the distribution of pre-release packages, where the version number includes a semantic versioning suffix such as `-alpha`, `-beta`, or `-rc`.</span></span> <span data-ttu-id="613ba-110">有关详细信息，请参阅[包版本控制](../reference/package-versioning.md#pre-release-versions)。</span><span class="sxs-lookup"><span data-stu-id="613ba-110">For more information, see [Package versioning](../reference/package-versioning.md#pre-release-versions).</span></span>

<span data-ttu-id="613ba-111">可通过以下两种方式指定此类版本：</span><span class="sxs-lookup"><span data-stu-id="613ba-111">You can specify such versions in two ways:</span></span>

- <span data-ttu-id="613ba-112">`.nuspec` 文件：在 `version` 元素中包括语义化版本后缀：</span><span class="sxs-lookup"><span data-stu-id="613ba-112">`.nuspec` file: include the semantic version suffix in the `version` element:</span></span>

    ```xml
    <version>1.0.1-alpha</version>
    ```

- <span data-ttu-id="613ba-113">程序集属性：生成 Visual Studio 项目的包（`.csproj` 或 `.vbproj`）时，使用 `AssemblyInformationalVersionAttribute` 指定版本：</span><span class="sxs-lookup"><span data-stu-id="613ba-113">Assembly attributes: when building a package from a Visual Studio project (`.csproj` or `.vbproj`), use the `AssemblyInformationalVersionAttribute` to specify the version:</span></span>

    ```cs
    [assembly: AssemblyInformationalVersion("1.0.1-beta")]
    ```

    <span data-ttu-id="613ba-114">NuGet 选取此值，而不是在 `AssemblyVersion` 属性中指定的不支持语义化版本控制的值。</span><span class="sxs-lookup"><span data-stu-id="613ba-114">NuGet picks up this value instead of the one specified in the `AssemblyVersion` attribute, which does not support semantic versioning.</span></span>

<span data-ttu-id="613ba-115">做好发布稳定版本的准备后，只需删除后缀，该包便优先于任何预发行版本。</span><span class="sxs-lookup"><span data-stu-id="613ba-115">When you’re ready to release a stable version, just remove the suffix and the package takes precedence over any pre-release versions.</span></span> <span data-ttu-id="613ba-116">同样，请参阅[包版本控制](../reference/package-versioning.md#pre-release-versions)。</span><span class="sxs-lookup"><span data-stu-id="613ba-116">Again, see [Package versioning](../reference/package-versioning.md#pre-release-versions).</span></span>

## <a name="installing-and-updating-pre-release-packages"></a><span data-ttu-id="613ba-117">安装和更新预发行包</span><span class="sxs-lookup"><span data-stu-id="613ba-117">Installing and updating pre-release packages</span></span>

<span data-ttu-id="613ba-118">默认情况下，NuGet 在处理包时不会包括预发行版本，但按照下文所述方法可更改此行为：</span><span class="sxs-lookup"><span data-stu-id="613ba-118">By default, NuGet does not include pre-release versions when working with packages, but you can change this behavior as follows:</span></span>

- <span data-ttu-id="613ba-119">Visual Studio 中的包管理器 UI：在“管理 NuGet 包”UI 中，选中“包括预发行版”框：</span><span class="sxs-lookup"><span data-stu-id="613ba-119">**Package Manager UI in Visual Studio**: In the **Manage NuGet Packages** UI, check the **Include prerelease** box:</span></span>

    ![Visual Studio 中的“包括预发行版”复选框](media/Prerelease_02-CheckPrerelease.png)

    <span data-ttu-id="613ba-121">设置或清除此框将刷新包管理器 UI 和可安装的可用版本的列表。</span><span class="sxs-lookup"><span data-stu-id="613ba-121">Setting or clearing this box will refresh the Package Manager UI and the list of available versions you can install.</span></span>

- <span data-ttu-id="613ba-122">**包管理器控制台**：将 `-IncludePrerelease` 开关与 `Find-Package`、`Get-Package`、`Install-Package`、`Sync-Package` 和 `Update-Package` 命令配合使用。</span><span class="sxs-lookup"><span data-stu-id="613ba-122">**Package Manager Console**: Use the `-IncludePrerelease` switch with the `Find-Package`, `Get-Package`, `Install-Package`, `Sync-Package`, and `Update-Package` commands.</span></span> <span data-ttu-id="613ba-123">请参阅 [PowerShell 参考](../tools/powershell-reference.md)。</span><span class="sxs-lookup"><span data-stu-id="613ba-123">Refer to the [PowerShell Reference](../tools/powershell-reference.md).</span></span>

- <span data-ttu-id="613ba-124">**NuGet CLI**：将 `-prerelease` 开关与 `install`、`update`、`delete` 和 `mirror` 命令配合使用。</span><span class="sxs-lookup"><span data-stu-id="613ba-124">**NuGet CLI**: Use the `-prerelease` switch with the `install`, `update`, `delete`, and `mirror` commands.</span></span> <span data-ttu-id="613ba-125">请参阅 [NuGet CLI 参考](../tools/nuget-exe-cli-reference.md)</span><span class="sxs-lookup"><span data-stu-id="613ba-125">Refer to the [NuGet CLI reference](../tools/nuget-exe-cli-reference.md)</span></span>

## <a name="semantic-versioning"></a><span data-ttu-id="613ba-126">语义化版本控制</span><span class="sxs-lookup"><span data-stu-id="613ba-126">Semantic versioning</span></span>

<span data-ttu-id="613ba-127">[语义化版本控制或 SemVer 约定](http://semver.org/spec/v1.0.0.html)介绍如何利用版本号中的字符串传达基础代码的含义。</span><span class="sxs-lookup"><span data-stu-id="613ba-127">The [Semantic Versioning or SemVer convention](http://semver.org/spec/v1.0.0.html) describes how to utilize strings in version numbers to convey they meaning of the underlying code.</span></span>

<span data-ttu-id="613ba-128">在此约定中，每个版本由三部分组成，即 `Major.Minor.Patch`，其含义分别是：</span><span class="sxs-lookup"><span data-stu-id="613ba-128">In this convention, each version has three parts, `Major.Minor.Patch`, with the following meaning:</span></span>

- <span data-ttu-id="613ba-129">`Major`：重大更改</span><span class="sxs-lookup"><span data-stu-id="613ba-129">`Major`: Breaking changes</span></span>
- <span data-ttu-id="613ba-130">`Minor`：新增功能，但可向后兼容</span><span class="sxs-lookup"><span data-stu-id="613ba-130">`Minor`: New features, but backwards compatible</span></span>
- <span data-ttu-id="613ba-131">`Patch`：仅可向后兼容的 bug 修复</span><span class="sxs-lookup"><span data-stu-id="613ba-131">`Patch`: Backwards compatible bug fixes only</span></span>

<span data-ttu-id="613ba-132">然后，通过在修补程序编号后追加连字符和字符串表示预发行版本。</span><span class="sxs-lookup"><span data-stu-id="613ba-132">Pre-release versions are then denoted by appending a hyphen and a string after the patch number.</span></span> <span data-ttu-id="613ba-133">从技术上说，可在连字符后使用任意字符串，NuGet 都会将包视为预发行版。</span><span class="sxs-lookup"><span data-stu-id="613ba-133">Technically speaking, you can use *any *string after the hyphen and NuGet will treat the package as pre-release.</span></span> <span data-ttu-id="613ba-134">然后，NuGet 在适用的 UI 中显示完整的版本号，供使用者自己解读其含义。</span><span class="sxs-lookup"><span data-stu-id="613ba-134">NuGet then displays the full version number in the applicable UI, leaving consumers to interpret the meaning for themselves.</span></span>

<span data-ttu-id="613ba-135">出于这种考虑，通常最好遵照如下所示的公认命名约定：</span><span class="sxs-lookup"><span data-stu-id="613ba-135">With this in mind, it's generally good to follow recognized naming conventions such as the following:</span></span>

- <span data-ttu-id="613ba-136">`-alpha`：Alpha 版本，通常用于在制品和试验品</span><span class="sxs-lookup"><span data-stu-id="613ba-136">`-alpha`: Alpha release, typically used for work-in-progress and experimentation</span></span>
- <span data-ttu-id="613ba-137">`-beta`：Beta 版本，通常指可用于下一计划版本的功能完整的版本，但可能包含已知 bug。</span><span class="sxs-lookup"><span data-stu-id="613ba-137">`-beta`: Beta release, typically one that is feature complete for the next planned release, but may contain known bugs.</span></span>
- <span data-ttu-id="613ba-138">`-rc`：候选发布，通常可能为最终（稳定）版本，除非出现重大 bug。</span><span class="sxs-lookup"><span data-stu-id="613ba-138">`-rc`: Release candidate, typically a release that's potentially final (stable) unless significant bugs emerge.</span></span>

> [!Note]
> <span data-ttu-id="613ba-139">NuGet 4.3.0+ 支持[语义化版本控制 v2.0.0](http://semver.org/spec/v2.0.0.html)，后者支持采用点表示法的预发布号，如 `1.0.1-build.23` 中所示。</span><span class="sxs-lookup"><span data-stu-id="613ba-139">NuGet 4.3.0+ supports [Semantic Versioning v2.0.0](http://semver.org/spec/v2.0.0.html), which supports pre-release numbers with dot notation, as in `1.0.1-build.23`.</span></span> <span data-ttu-id="613ba-140">NuGet 4.3.0 之前的版本不支持点表示法。</span><span class="sxs-lookup"><span data-stu-id="613ba-140">Dot notation is not supported with NuGet versions before 4.3.0.</span></span> <span data-ttu-id="613ba-141">在 NuGet 的早期版本中，可以使用 `1.0.1-build23` 之类的格式，但这始终被视为预发布版本。</span><span class="sxs-lookup"><span data-stu-id="613ba-141">In earlier versions of NuGet, you could use a form like `1.0.1-build23` but this was always considered a pre-release version.</span></span>

<span data-ttu-id="613ba-142">但是，无论使用何种后缀，NuGet 都会按照反向字母顺序向它们赋予优先级：</span><span class="sxs-lookup"><span data-stu-id="613ba-142">Whatever suffixes you use, however, NuGet will give them precedence in reverse alphabetical order:</span></span>

    1.0.1
    1.0.1-zzz
    1.0.1-rc
    1.0.1-open
    1.0.1-beta12
    1.0.1-beta05
    1.0.1-beta
    1.0.1-alpha2
    1.0.1-alpha

<span data-ttu-id="613ba-143">如上所示，没有任何后缀的版本始终优先于预发行版本。</span><span class="sxs-lookup"><span data-stu-id="613ba-143">As shown, the version without any suffix will always take precedence over pre-release versions.</span></span> <span data-ttu-id="613ba-144">另请注意，如果在可能使用两位数（或更多数字）的预发行版本标记中使用数字后缀，请使用前导零，如 beta01 和 beta05，以便确保数字增大时，可以正确地进行排序。</span><span class="sxs-lookup"><span data-stu-id="613ba-144">Note also that if you use numerical suffixes with pre-release tags that might use double-digit numbers (or more), use leading zeroes as in beta01 and beta05 to ensure that they sort correctly when the numbers get larger.</span></span>
