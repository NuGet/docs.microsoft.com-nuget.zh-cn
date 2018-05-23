---
title: NuGet 错误和警告参考
description: 针对警告和错误各种 NuGet 操作过程中从 NuGet 发出的完整参考。
author: kraigb
ms.author: kraigb
manager: douge
ms.date: 05/18/2018
ms.topic: reference
ms.reviewer: anangaur
f1_keywords:
- NU1000
- NU1001
- NU1002
- NU1003
- NU1100
- NU1101
- NU1102
- NU1103
- NU1104
- NU1105
- NU1106
- NU1107
- NU1108
- NU1201
- NU1202
- NU1203
- NU1401
- NU1500
- NU1501
- NU1502
- NU1503
- NU1601
- NU1602
- NU1603
- NU1604
- NU1605
- NU1608
- NU1701
- NU1801
- NU3000
- NU3001
- NU3002
- NU3004
- NU3008
- NU3018
- NU3028
ms.openlocfilehash: 748c2746a61886617e2eefe3e6c4a2e2a5b9d4d3
ms.sourcegitcommit: 8127dd73ff8481a1a01acd9b7004dd131a9d84e7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/22/2018
---
# <a name="errors-and-warnings"></a><span data-ttu-id="f35d1-103">错误和警告</span><span class="sxs-lookup"><span data-stu-id="f35d1-103">Errors and warnings</span></span>

<span data-ttu-id="f35d1-104">在 NuGet 4.3.0+ 错误和警告本主题中所述进行编号，并提供帮助您解决所涉及的问题详细的信息。</span><span class="sxs-lookup"><span data-stu-id="f35d1-104">In NuGet 4.3.0+, errors and warnings are numbered as described in this topic and provide detailed information to help you address the issues involved.</span></span>

<span data-ttu-id="f35d1-105">错误和警告在此处列出是仅适用于[PackageReference 基于](../consume-packages/package-references-in-project-files.md)项目和 NuGet 4.3.0+。</span><span class="sxs-lookup"><span data-stu-id="f35d1-105">The errors and warnings listed here are available only with [PackageReference-based](../consume-packages/package-references-in-project-files.md) projects and NuGet 4.3.0+.</span></span> <span data-ttu-id="f35d1-106">NuGet 也服从 MSBuild 属性，以禁止显示警告或将它们提升到错误。</span><span class="sxs-lookup"><span data-stu-id="f35d1-106">NuGet also honors MSBuild properties to suppress warnings or elevate them to errors.</span></span> <span data-ttu-id="f35d1-107">有关详细信息，请参阅[如何： 禁止显示编译器警告](/visualstudio/ide/how-to-suppress-compiler-warnings)Visual Studio 文档中。</span><span class="sxs-lookup"><span data-stu-id="f35d1-107">For more information, see [How to: Suppress Compiler Warnings](/visualstudio/ide/how-to-suppress-compiler-warnings) in the Visual Studio documentation.</span></span>

<span data-ttu-id="f35d1-108">**错误**</span><span class="sxs-lookup"><span data-stu-id="f35d1-108">**Errors**</span></span>

| <span data-ttu-id="f35d1-109">Group</span><span class="sxs-lookup"><span data-stu-id="f35d1-109">Group</span></span> | <span data-ttu-id="f35d1-110">错误号</span><span class="sxs-lookup"><span data-stu-id="f35d1-110">Error Numbers</span></span> |
| --- | --- |
| [<span data-ttu-id="f35d1-111">无效的输入的错误</span><span class="sxs-lookup"><span data-stu-id="f35d1-111">Invalid input errors</span></span>](#invalid-input-errors) | <span data-ttu-id="f35d1-112">[NU1001](#nu1001)， [NU1002](#nu1002)， [NU1003](#nu1003)</span><span class="sxs-lookup"><span data-stu-id="f35d1-112">[NU1001](#nu1001), [NU1002](#nu1002), [NU1003](#nu1003)</span></span> |
| [<span data-ttu-id="f35d1-113">缺少的包和项目错误</span><span class="sxs-lookup"><span data-stu-id="f35d1-113">Missing package and project errors</span></span>](#missing-package-and-project-errors) | <span data-ttu-id="f35d1-114">[NU1100](#nu1100)， [NU1101](#nu1101)， [NU1102](#nu1102)， [NU1103](#nu1103)， [NU1104](#nu1104)， [NU1105](#nu1105)， [NU1106](#nu1106)， [NU1107](#nu1107) (以前 NU1607) [NU1108](#nu1108) (以前 NU1606)</span><span class="sxs-lookup"><span data-stu-id="f35d1-114">[NU1100](#nu1100), [NU1101](#nu1101), [NU1102](#nu1102), [NU1103](#nu1103), [NU1104](#nu1104), [NU1105](#nu1105), [NU1106](#nu1106), [NU1107](#nu1107) (previously NU1607), [NU1108](#nu1108) (previously NU1606)</span></span> |
| [<span data-ttu-id="f35d1-115">兼容性错误</span><span class="sxs-lookup"><span data-stu-id="f35d1-115">Compatibility errors</span></span>](#compatibility-errors) | <span data-ttu-id="f35d1-116">[NU1201](#nu1201)， [NU1202](#nu1202)， [NU1203](#nu1203)， [NU1401](#nu1401)</span><span class="sxs-lookup"><span data-stu-id="f35d1-116">[NU1201](#nu1201), [NU1202](#nu1202), [NU1203](#nu1203), [NU1401](#nu1401)</span></span> |

<span data-ttu-id="f35d1-117">**警告**</span><span class="sxs-lookup"><span data-stu-id="f35d1-117">**Warnings**</span></span>

| <span data-ttu-id="f35d1-118">Group</span><span class="sxs-lookup"><span data-stu-id="f35d1-118">Group</span></span> | <span data-ttu-id="f35d1-119">警告编号</span><span class="sxs-lookup"><span data-stu-id="f35d1-119">Warning numbers</span></span> |
| --- | --- |
| [<span data-ttu-id="f35d1-120">无效的输入的警告</span><span class="sxs-lookup"><span data-stu-id="f35d1-120">Invalid input warnings</span></span>](#invalid-input-warnings) | <span data-ttu-id="f35d1-121">[NU1501](#nu1501)， [NU1502](#nu1502)， [NU1503](#nu1503)</span><span class="sxs-lookup"><span data-stu-id="f35d1-121">[NU1501](#nu1501), [NU1502](#nu1502), [NU1503](#nu1503)</span></span> |
| [<span data-ttu-id="f35d1-122">意外的包版本警告</span><span class="sxs-lookup"><span data-stu-id="f35d1-122">Unexpected package version warnings</span></span>](#unexpected-package-version-warnings) | <span data-ttu-id="f35d1-123">[NU1601](#nu1601)， [NU1602](#nu1602)， [NU1603](#nu1603)， [NU1604](#nu1604)， [NU1605](#nu1605)</span><span class="sxs-lookup"><span data-stu-id="f35d1-123">[NU1601](#nu1601), [NU1602](#nu1602), [NU1603](#nu1603), [NU1604](#nu1604), [NU1605](#nu1605)</span></span> |
| [<span data-ttu-id="f35d1-124">冲突解决程序冲突警告</span><span class="sxs-lookup"><span data-stu-id="f35d1-124">Resolver conflict warnings</span></span>](#resolver-conflict-warnings) | [<span data-ttu-id="f35d1-125">NU1608</span><span class="sxs-lookup"><span data-stu-id="f35d1-125">NU1608</span></span>](#nu1608) |
| [<span data-ttu-id="f35d1-126">包回退警告</span><span class="sxs-lookup"><span data-stu-id="f35d1-126">Package fallback warnings</span></span>](#package-fallback-warnings) | [<span data-ttu-id="f35d1-127">NU1701</span><span class="sxs-lookup"><span data-stu-id="f35d1-127">NU1701</span></span>](#nu1701) |
| [<span data-ttu-id="f35d1-128">源警告</span><span class="sxs-lookup"><span data-stu-id="f35d1-128">Feed warnings</span></span>](#feed-warnings) | [<span data-ttu-id="f35d1-129">NU1801</span><span class="sxs-lookup"><span data-stu-id="f35d1-129">NU1801</span></span>](#nu1801) |
| [<span data-ttu-id="f35d1-130">NuGet 内部错误和警告</span><span class="sxs-lookup"><span data-stu-id="f35d1-130">NuGet internal errors and warnings</span></span>](#nuget-internal-errors-and-warnings) | <span data-ttu-id="f35d1-131">[NU1000](#nu1000)， [NU1500](#nu1500)</span><span class="sxs-lookup"><span data-stu-id="f35d1-131">[NU1000](#nu1000), [NU1500](#nu1500)</span></span> |
| [<span data-ttu-id="f35d1-132">已签名的软件包 （创建和验证）</span><span class="sxs-lookup"><span data-stu-id="f35d1-132">Signed packages (creation and verification)</span></span>](#signed-packages-creation-and-verification)| <span data-ttu-id="f35d1-133">[NU3000](#nu3000)， [NU3001](#nu3001)， [NU3002](#nu3002)， [NU3004](#nu3004)， [NU3008](#nu3008)， [NU3018](#nu3018)， [NU3028](#nu3028)</span><span class="sxs-lookup"><span data-stu-id="f35d1-133">[NU3000](#nu3000), [NU3001](#nu3001), [NU3002](#nu3002), [NU3004](#nu3004), [NU3008](#nu3008), [NU3018](#nu3018), [NU3028](#nu3028)</span></span> |

## <a name="invalid-input-errors"></a><span data-ttu-id="f35d1-134">无效的输入的错误</span><span class="sxs-lookup"><span data-stu-id="f35d1-134">Invalid input errors</span></span>

<span data-ttu-id="f35d1-135">[NU1001](#nu1001) | [NU1002](#nu1002) | [NU1003](#nu1003)</span><span class="sxs-lookup"><span data-stu-id="f35d1-135">[NU1001](#nu1001) | [NU1002](#nu1002) | [NU1003](#nu1003)</span></span>

### <a name="nu1001"></a><span data-ttu-id="f35d1-136">NU1001</span><span class="sxs-lookup"><span data-stu-id="f35d1-136">NU1001</span></span>

| | |
| --- | --- |
| <span data-ttu-id="f35d1-137">**问题**</span><span class="sxs-lookup"><span data-stu-id="f35d1-137">**Issue**</span></span> | <span data-ttu-id="f35d1-138">项目不包含一个或多个框架。</span><span class="sxs-lookup"><span data-stu-id="f35d1-138">The project doesn't contain one or more frameworks.</span></span> |
| <span data-ttu-id="f35d1-139">**示例消息**</span><span class="sxs-lookup"><span data-stu-id="f35d1-139">**Example message**</span></span> | <span data-ttu-id="f35d1-140">*项目 projA c:\tmp\projA.csproj 中未指定任何目标框架*</span><span class="sxs-lookup"><span data-stu-id="f35d1-140">*The project projA does not specify any target frameworks in c:\tmp\projA.csproj*</span></span> |
| <span data-ttu-id="f35d1-141">**解决方案**</span><span class="sxs-lookup"><span data-stu-id="f35d1-141">**Solution**</span></span> | <span data-ttu-id="f35d1-142">添加`TargetFramework`或`TargetFrameworks`属性设置为指定的项目文件。</span><span class="sxs-lookup"><span data-stu-id="f35d1-142">Add a `TargetFramework` or `TargetFrameworks` property to the specified project file.</span></span> |

### <a name="nu1002"></a><span data-ttu-id="f35d1-143">NU1002</span><span class="sxs-lookup"><span data-stu-id="f35d1-143">NU1002</span></span>

| | |
| --- | --- |
| <span data-ttu-id="f35d1-144">**问题**</span><span class="sxs-lookup"><span data-stu-id="f35d1-144">**Issue**</span></span> | <span data-ttu-id="f35d1-145">无效的输入以及清除关键字的组合。</span><span class="sxs-lookup"><span data-stu-id="f35d1-145">Invalid combination of inputs along with a CLEAR keyword.</span></span> |
| <span data-ttu-id="f35d1-146">**示例消息**</span><span class="sxs-lookup"><span data-stu-id="f35d1-146">**Example message**</span></span> | <span data-ttu-id="f35d1-147">*清除不能在与其他值一起使用*</span><span class="sxs-lookup"><span data-stu-id="f35d1-147">*'CLEAR' cannot be used in conjunction with other values*</span></span> |
| <span data-ttu-id="f35d1-148">**解决方案**</span><span class="sxs-lookup"><span data-stu-id="f35d1-148">**Solution**</span></span> | <span data-ttu-id="f35d1-149">清除自行使用，而忽略所有其他输入。</span><span class="sxs-lookup"><span data-stu-id="f35d1-149">Use CLEAR by itself and omit all other inputs.</span></span> |

### <a name="nu1003"></a><span data-ttu-id="f35d1-150">NU1003</span><span class="sxs-lookup"><span data-stu-id="f35d1-150">NU1003</span></span>

| | |
| --- | --- |
| <span data-ttu-id="f35d1-151">**问题**</span><span class="sxs-lookup"><span data-stu-id="f35d1-151">**Issue**</span></span> | <span data-ttu-id="f35d1-152">`PackageTargetFallback` 和`AssetTargetFallback`用于选择资产提供不同的行为和不能一起使用。</span><span class="sxs-lookup"><span data-stu-id="f35d1-152">`PackageTargetFallback` and `AssetTargetFallback` provide different behavior for selecting assets and cannot be used together.</span></span> |
| <span data-ttu-id="f35d1-153">**示例消息**</span><span class="sxs-lookup"><span data-stu-id="f35d1-153">**Example message**</span></span> | <span data-ttu-id="f35d1-154">*PackageTargetFallback 和 AssetTargetFallback 不能一起使用。从项目环境删除 PackageTargetFallback(deprecated) 的引用。*</span><span class="sxs-lookup"><span data-stu-id="f35d1-154">*PackageTargetFallback and AssetTargetFallback cannot be used together. Remove PackageTargetFallback(deprecated) references from the project environment.*</span></span> |
| <span data-ttu-id="f35d1-155">**解决方案**</span><span class="sxs-lookup"><span data-stu-id="f35d1-155">**Solution**</span></span> | <span data-ttu-id="f35d1-156">删除不推荐使用`PackageTargetFallback`从项目的元素。</span><span class="sxs-lookup"><span data-stu-id="f35d1-156">Remove the deprecated `PackageTargetFallback` element from the project.</span></span> |

## <a name="missing-package-and-project-errors"></a><span data-ttu-id="f35d1-157">缺少的包和项目错误</span><span class="sxs-lookup"><span data-stu-id="f35d1-157">Missing package and project errors</span></span>

<span data-ttu-id="f35d1-158">[NU1100](#nu1100) | [NU1101](#nu1101) | [NU1102](#nu1102) | [NU1103](#nu1103) | [NU1104](#nu1104) | [NU1105](#nu1105) | [NU1106](#nu1106)</span><span class="sxs-lookup"><span data-stu-id="f35d1-158">[NU1100](#nu1100) | [NU1101](#nu1101) | [NU1102](#nu1102) | [NU1103](#nu1103) | [NU1104](#nu1104) | [NU1105](#nu1105) | [NU1106](#nu1106)</span></span>

### <a name="nu1100"></a><span data-ttu-id="f35d1-159">NU1100</span><span class="sxs-lookup"><span data-stu-id="f35d1-159">NU1100</span></span>

| | |
| --- | --- |
| <span data-ttu-id="f35d1-160">**问题**</span><span class="sxs-lookup"><span data-stu-id="f35d1-160">**Issue**</span></span> | <span data-ttu-id="f35d1-161">依赖关系组不被解析。</span><span class="sxs-lookup"><span data-stu-id="f35d1-161">A dependency group not be resolved.</span></span> <span data-ttu-id="f35d1-162">这是一个泛型类型不是包或项目的问题。</span><span class="sxs-lookup"><span data-stu-id="f35d1-162">This is a generic issue for types that are not packages or projects.</span></span> |
| <span data-ttu-id="f35d1-163">**示例消息**</span><span class="sxs-lookup"><span data-stu-id="f35d1-163">**Example message**</span></span> | <span data-ttu-id="f35d1-164">*无法解析 net45 System.Missing*</span><span class="sxs-lookup"><span data-stu-id="f35d1-164">*Unable to resolve System.Missing for net45*</span></span> |
| <span data-ttu-id="f35d1-165">**解决方案**</span><span class="sxs-lookup"><span data-stu-id="f35d1-165">**Solution**</span></span> | <span data-ttu-id="f35d1-166">打开项目文件并检查其依赖项列表。</span><span class="sxs-lookup"><span data-stu-id="f35d1-166">Open the project file and examine the list of its dependencies.</span></span> <span data-ttu-id="f35d1-167">检查在你使用的包源上存在每个依赖关系和包支持项目的目标框架。</span><span class="sxs-lookup"><span data-stu-id="f35d1-167">Check that each dependency exists on the package sources you're using, and that the package supports the project's target framework.</span></span> |

### <a name="nu1101"></a><span data-ttu-id="f35d1-168">NU1101</span><span class="sxs-lookup"><span data-stu-id="f35d1-168">NU1101</span></span>

| | |
| --- | --- |
| <span data-ttu-id="f35d1-169">**问题**</span><span class="sxs-lookup"><span data-stu-id="f35d1-169">**Issue**</span></span> | <span data-ttu-id="f35d1-170">在任何源上找不到包。</span><span class="sxs-lookup"><span data-stu-id="f35d1-170">The package cannot be found on any sources.</span></span> |
| <span data-ttu-id="f35d1-171">**示例消息**</span><span class="sxs-lookup"><span data-stu-id="f35d1-171">**Example message**</span></span> | <span data-ttu-id="f35d1-172">*找不到程序包 System.Missing。具有此 id 在源中存在的任何包： dotnet 核心、 dotnet roslyn、 nuget.org*</span><span class="sxs-lookup"><span data-stu-id="f35d1-172">*Unable to find package System.Missing. No packages exist with this id in source(s): dotnet-core, dotnet-roslyn, nuget.org*</span></span> |
| <span data-ttu-id="f35d1-173">**解决方案**</span><span class="sxs-lookup"><span data-stu-id="f35d1-173">**Solution**</span></span> | <span data-ttu-id="f35d1-174">检查以确保使用正确的包标识符和版本号数目的 Visual Studio 中的项目的依赖关系。</span><span class="sxs-lookup"><span data-stu-id="f35d1-174">Examine the project's dependencies in Visual Studio to be sure you're using the correct package identifier and version number.</span></span> <span data-ttu-id="f35d1-175">此外检查[NuGet 配置](../consume-packages/Configuring-NuGet-Behavior.md)标识的包源你希望使用。</span><span class="sxs-lookup"><span data-stu-id="f35d1-175">Also check that the [NuGet configuration](../consume-packages/Configuring-NuGet-Behavior.md) identifies the package sources your expect to be using.</span></span> <span data-ttu-id="f35d1-176">如果你使用具有的包[语义版本控制 2.0.0](../reference/package-versioning.md#semantic-versioning-200)，请确保你使用的源，V3`https://api.nuget.org/v3/index.json`中[NuGet 配置](../consume-packages/Configuring-NuGet-Behavior.md)。</span><span class="sxs-lookup"><span data-stu-id="f35d1-176">If you use packages that have [Semantic Versioning 2.0.0](../reference/package-versioning.md#semantic-versioning-200), please make sure that you are using the V3 feed, `https://api.nuget.org/v3/index.json`, in the [NuGet configuration](../consume-packages/Configuring-NuGet-Behavior.md).</span></span> |

### <a name="nu1102"></a><span data-ttu-id="f35d1-177">NU1102</span><span class="sxs-lookup"><span data-stu-id="f35d1-177">NU1102</span></span>

| | |
| --- | --- |
| <span data-ttu-id="f35d1-178">**问题**</span><span class="sxs-lookup"><span data-stu-id="f35d1-178">**Issue**</span></span> | <span data-ttu-id="f35d1-179">找到的包标识符，但在任何源上找不到指定的依赖范围内的版本。</span><span class="sxs-lookup"><span data-stu-id="f35d1-179">The package identifier is found but a version within the specified dependency range cannot be found on any of the sources.</span></span> <span data-ttu-id="f35d1-180">可能由包和不是用户指定的范围。</span><span class="sxs-lookup"><span data-stu-id="f35d1-180">The range might be specified by a package and not the user.</span></span> |
| <span data-ttu-id="f35d1-181">**示例消息**</span><span class="sxs-lookup"><span data-stu-id="f35d1-181">**Example message**</span></span> | <span data-ttu-id="f35d1-182">*找不到版本包 NuGet.Versioning (> = 9.0.1)<br/> -于 nuget.org 中的找到 30 版本 [最接近的版本： 4.0.0]<br/> -dotnet buildtools 中找到的 10 版本 [最接近的版本： 4.0.0-rc-2129]<br/> -找到 9在 NuGetVolatile 版本 [最接近的版本： 3.0.0-beta-00032]<br/> -0 版本位于 dotnet 核心<br/>-0 版本位于 dotnet roslyn*</span><span class="sxs-lookup"><span data-stu-id="f35d1-182">*Unable to find package NuGet.Versioning with version (>= 9.0.1)<br/>  - Found 30 version(s) in nuget.org [ Nearest version: 4.0.0 ]<br/>  - Found 10 version(s) in dotnet-buildtools [ Nearest version: 4.0.0-rc-2129 ]<br/>  - Found 9 version(s) in NuGetVolatile [ Nearest version: 3.0.0-beta-00032 ]<br/>  - Found 0 version(s) in dotnet-core<br/>  - Found 0 version(s) in dotnet-roslyn*</span></span> |
| <span data-ttu-id="f35d1-183">**解决方案**</span><span class="sxs-lookup"><span data-stu-id="f35d1-183">**Solution**</span></span> | <span data-ttu-id="f35d1-184">编辑项目文件以更正包版本。</span><span class="sxs-lookup"><span data-stu-id="f35d1-184">Edit the project file to correct the package version.</span></span> <span data-ttu-id="f35d1-185">此外检查[NuGet 配置](../consume-packages/Configuring-NuGet-Behavior.md)标识的包源你希望使用。</span><span class="sxs-lookup"><span data-stu-id="f35d1-185">Also check that the [NuGet configuration](../consume-packages/Configuring-NuGet-Behavior.md) identifies the package sources your expect to be using.</span></span> <span data-ttu-id="f35d1-186">你可能需要更改 requeted 版本，如果此包被直接引用该项目。</span><span class="sxs-lookup"><span data-stu-id="f35d1-186">You may need to change the requeted version if this package is referenced by the project directly.</span></span> |

### <a name="nu1103"></a><span data-ttu-id="f35d1-187">NU1103</span><span class="sxs-lookup"><span data-stu-id="f35d1-187">NU1103</span></span>

| | |
| --- | --- |
| <span data-ttu-id="f35d1-188">**问题**</span><span class="sxs-lookup"><span data-stu-id="f35d1-188">**Issue**</span></span> | <span data-ttu-id="f35d1-189">项目指定了依赖项的范围，稳定版本，但不稳定版本找该范围内。</span><span class="sxs-lookup"><span data-stu-id="f35d1-189">The project specified a stable version for the dependency range, but no stable versions were found in that range.</span></span> <span data-ttu-id="f35d1-190">预发行版本未找到，但不是允许。</span><span class="sxs-lookup"><span data-stu-id="f35d1-190">Pre-release versions were found but are not allowed.</span></span> |
| <span data-ttu-id="f35d1-191">**示例消息**</span><span class="sxs-lookup"><span data-stu-id="f35d1-191">**Example message**</span></span> | <span data-ttu-id="f35d1-192">*找不到稳定的包 NuGet.Versioning 随版本 (> = 3.0.0)<br/> -dotnet buildtools 中找到的 10 版本 [最接近的版本： 4.0.0-rc-2129]<br/> -NuGetVolatile 中的找到 9 版本 [最接近的版本： 3.0.0-beta-00032]<br/> -0 版本位于 dotnet 核心<br/>-0 版本位于 dotnet roslyn*</span><span class="sxs-lookup"><span data-stu-id="f35d1-192">*Unable to find a stable package NuGet.Versioning with version (>= 3.0.0)<br/>  - Found 10 version(s) in dotnet-buildtools [ Nearest version: 4.0.0-rc-2129 ]<br/>  - Found 9 version(s) in NuGetVolatile [ Nearest version: 3.0.0-beta-00032 ]<br/>  - Found 0 version(s) in dotnet-core<br/>  - Found 0 version(s) in dotnet-roslyn*</span></span> |
| <span data-ttu-id="f35d1-193">**解决方案**</span><span class="sxs-lookup"><span data-stu-id="f35d1-193">**Solution**</span></span> |  <span data-ttu-id="f35d1-194">编辑项目文件以包括预发行版本中的版本范围。</span><span class="sxs-lookup"><span data-stu-id="f35d1-194">Edit the version range in the project file to include pre-release versions.</span></span> <span data-ttu-id="f35d1-195">请参阅[包版本控制](../reference/Package-Versioning.md)。</span><span class="sxs-lookup"><span data-stu-id="f35d1-195">See [Package versioning](../reference/Package-Versioning.md).</span></span> |

### <a name="nu1104"></a><span data-ttu-id="f35d1-196">NU1104</span><span class="sxs-lookup"><span data-stu-id="f35d1-196">NU1104</span></span>

| | |
| --- | --- |
| <span data-ttu-id="f35d1-197">**问题**</span><span class="sxs-lookup"><span data-stu-id="f35d1-197">**Issue**</span></span> | <span data-ttu-id="f35d1-198">ProjectReference 指向不存在的文件。</span><span class="sxs-lookup"><span data-stu-id="f35d1-198">A ProjectReference points to a file that doesn't exist.</span></span> |
| <span data-ttu-id="f35d1-199">**示例消息**</span><span class="sxs-lookup"><span data-stu-id="f35d1-199">**Example message**</span></span> | <span data-ttu-id="f35d1-200">*项目引用不存在 c:\a.csproj。检查项目引用有效以及项目文件是否存在。*</span><span class="sxs-lookup"><span data-stu-id="f35d1-200">*Project reference does not exist 'c:\a.csproj'. Check that the project reference is valid and that the project file exists.*</span></span> |
| <span data-ttu-id="f35d1-201">**解决方案**</span><span class="sxs-lookup"><span data-stu-id="f35d1-201">**Solution**</span></span> | <span data-ttu-id="f35d1-202">编辑项目文件以更正引用的项目的路径，或若要删除的引用一起删除，如果不再需要。</span><span class="sxs-lookup"><span data-stu-id="f35d1-202">Edit the project file to either correct the path to the referenced project or to remove the reference altogether if it's no longer needed.</span></span> |

### <a name="nu1105"></a><span data-ttu-id="f35d1-203">NU1105</span><span class="sxs-lookup"><span data-stu-id="f35d1-203">NU1105</span></span>

| | |
| --- | --- |
| <span data-ttu-id="f35d1-204">**问题**</span><span class="sxs-lookup"><span data-stu-id="f35d1-204">**Issue**</span></span> | <span data-ttu-id="f35d1-205">项目文件存在，但不还原信息已为其提供。</span><span class="sxs-lookup"><span data-stu-id="f35d1-205">The project file exists but no restore information was provided for it.</span></span> |
| <span data-ttu-id="f35d1-206">**示例消息**</span><span class="sxs-lookup"><span data-stu-id="f35d1-206">**Example message**</span></span> | <span data-ttu-id="f35d1-207">*无法读取 c:\a.csproj 的项目信息。项目文件可能无效或缺少所需的还原的目标。*</span><span class="sxs-lookup"><span data-stu-id="f35d1-207">*Unable to read project information for 'c:\a.csproj'. The project file may be invalid or missing targets required for restore.*</span></span> |
| <span data-ttu-id="f35d1-208">**解决方案**</span><span class="sxs-lookup"><span data-stu-id="f35d1-208">**Solution**</span></span> | <span data-ttu-id="f35d1-209">在 Visual Studio 中，该错误可能意味着该项目已卸载，在这种情况下重新加载项目。</span><span class="sxs-lookup"><span data-stu-id="f35d1-209">In Visual Studio, the error could mean that the project is unloaded, in which case reload the project.</span></span> <span data-ttu-id="f35d1-210">从命令行这可能表示该文件已损坏或，它不包含"之后导入"自定义所需的还原，以便读取项目的目标。</span><span class="sxs-lookup"><span data-stu-id="f35d1-210">From the command line this could mean that the file is corrupt or that it doesn't contain the custom "after imports" target needed for restore to read the project.</span></span> <span data-ttu-id="f35d1-211">检查项目文件有效以及包含"之后导入"目标。</span><span class="sxs-lookup"><span data-stu-id="f35d1-211">Check that the project file is valid and contains an "after imports" target.</span></span> |

### <a name="nu1106"></a><span data-ttu-id="f35d1-212">NU1106</span><span class="sxs-lookup"><span data-stu-id="f35d1-212">NU1106</span></span>

| | |
| --- | --- |
| <span data-ttu-id="f35d1-213">**问题**</span><span class="sxs-lookup"><span data-stu-id="f35d1-213">**Issue**</span></span> | <span data-ttu-id="f35d1-214">无法解析依赖项约束。</span><span class="sxs-lookup"><span data-stu-id="f35d1-214">Dependency constraints cannot be resolved.</span></span> |
| <span data-ttu-id="f35d1-215">**示例消息**</span><span class="sxs-lookup"><span data-stu-id="f35d1-215">**Example message**</span></span> | <span data-ttu-id="f35d1-216">*无法满足 {id} 互相冲突的请求: {冲突路径} Framework: {目标关系图}*</span><span class="sxs-lookup"><span data-stu-id="f35d1-216">*Unable to satisfy conflicting requests for {id}: {conflict path} Framework: {target graph}*</span></span> |
| <span data-ttu-id="f35d1-217">**解决方案**</span><span class="sxs-lookup"><span data-stu-id="f35d1-217">**Solution**</span></span> | <span data-ttu-id="f35d1-218">编辑项目文件以指定的依赖项而不是准确的版本更自由范围。</span><span class="sxs-lookup"><span data-stu-id="f35d1-218">Edit the project file to specify more open-ended ranges for the dependency rather than an exact version.</span></span> |
|

<a name="nu1107"></a>

### <a name="nu1107-previously-nu1607"></a><span data-ttu-id="f35d1-219">NU1107 (以前 NU1607)</span><span class="sxs-lookup"><span data-stu-id="f35d1-219">NU1107 (Previously NU1607)</span></span>

| | |
| --- | --- |
| <span data-ttu-id="f35d1-220">**问题**</span><span class="sxs-lookup"><span data-stu-id="f35d1-220">**Issue**</span></span> | <span data-ttu-id="f35d1-221">无法解析包之间的依赖关系约束。</span><span class="sxs-lookup"><span data-stu-id="f35d1-221">Unable to resolve dependency constraints between packages.</span></span> |
| <span data-ttu-id="f35d1-222">**示例消息**</span><span class="sxs-lookup"><span data-stu-id="f35d1-222">**Example message**</span></span> | <span data-ttu-id="f35d1-223">*NuGet.Versioning 检测到的版本冲突。若要解决此问题的项目中直接引用包。<br/>NuGet.Packaging 3.5.0-> （= 3.5.0） NuGet.Versioning<br/> NuGet.Configuration 4.0.0-> 的 NuGet.Versioning （= 4.0.0）*</span><span class="sxs-lookup"><span data-stu-id="f35d1-223">*Version conflict detected for NuGet.Versioning. Reference the package directly from the project to resolve this issue.<br/>  NuGet.Packaging 3.5.0 -> NuGet.Versioning (= 3.5.0)<br/>  NuGet.Configuration 4.0.0 -> NuGet.Versioning (= 4.0.0)*</span></span> |
| <span data-ttu-id="f35d1-224">**解决方案**</span><span class="sxs-lookup"><span data-stu-id="f35d1-224">**Solution**</span></span> | <span data-ttu-id="f35d1-225">依赖项与上的约束的确切版本的包不允许其他包以根据需要增大版本号。</span><span class="sxs-lookup"><span data-stu-id="f35d1-225">Packages with dependency constraints on exact versions do not allow other packages to increase the version if needed.</span></span> <span data-ttu-id="f35d1-226">添加具有所需的确切版本对直接 （在项目文件中） 项目的引用。</span><span class="sxs-lookup"><span data-stu-id="f35d1-226">Add a reference to the project directly (in the project file) with the exact version required.</span></span> |

<a name="nu1108"></a>

### <a name="nu1108-previously-nu1606"></a><span data-ttu-id="f35d1-227">NU1108 (以前 NU1606)</span><span class="sxs-lookup"><span data-stu-id="f35d1-227">NU1108 (Previously NU1606)</span></span>

| | |
| --- | --- |
| <span data-ttu-id="f35d1-228">**问题**</span><span class="sxs-lookup"><span data-stu-id="f35d1-228">**Issue**</span></span> | <span data-ttu-id="f35d1-229">检测到循环依赖关系。</span><span class="sxs-lookup"><span data-stu-id="f35d1-229">A circular dependency was detected.</span></span> |
| <span data-ttu-id="f35d1-230">**示例消息**</span><span class="sxs-lookup"><span data-stu-id="f35d1-230">**Example message**</span></span> | <span data-ttu-id="f35d1-231">*检测到循环： A-> B-> A*</span><span class="sxs-lookup"><span data-stu-id="f35d1-231">*Cycle detected: A -> B -> A*</span></span> |
| <span data-ttu-id="f35d1-232">**解决方案**</span><span class="sxs-lookup"><span data-stu-id="f35d1-232">**Solution**</span></span> | <span data-ttu-id="f35d1-233">不正确; 创作包请与联系软件包所有者以更正 bug。</span><span class="sxs-lookup"><span data-stu-id="f35d1-233">The package is authored incorrectly; contact the package owner to correct the bug.</span></span> |

## <a name="compatibility-errors"></a><span data-ttu-id="f35d1-234">兼容性错误</span><span class="sxs-lookup"><span data-stu-id="f35d1-234">Compatibility errors</span></span>

<span data-ttu-id="f35d1-235">[NU1201](#nu1201) | [NU1202](#nu1202) | [NU1203](#nu1203) | [NU1401](#nu1401)</span><span class="sxs-lookup"><span data-stu-id="f35d1-235">[NU1201](#nu1201) | [NU1202](#nu1202) | [NU1203](#nu1203) | [NU1401](#nu1401)</span></span>

### <a name="nu1201"></a><span data-ttu-id="f35d1-236">NU1201</span><span class="sxs-lookup"><span data-stu-id="f35d1-236">NU1201</span></span>

| | |
| --- | --- |
| <span data-ttu-id="f35d1-237">**问题**</span><span class="sxs-lookup"><span data-stu-id="f35d1-237">**Issue**</span></span> | <span data-ttu-id="f35d1-238">依赖项项目不包含与当前项目兼容的框架。</span><span class="sxs-lookup"><span data-stu-id="f35d1-238">A dependency project doesn't contain a framework compatible with the current project.</span></span> <span data-ttu-id="f35d1-239">通常情况下，项目的目标框架是比使用项目的更高版本。</span><span class="sxs-lookup"><span data-stu-id="f35d1-239">Typically, the project's target framework is a higher version than the consuming project.</span></span> |
| <span data-ttu-id="f35d1-240">**示例消息**</span><span class="sxs-lookup"><span data-stu-id="f35d1-240">**Example message**</span></span> | <span data-ttu-id="f35d1-241">*项目 ServerWeb 与不兼容 netstandard1.3 (。NETStandard，Version = v1.3)。项目 ServerWeb 支持：<br/> -netstandard1.6 (。NETStandard，Version = v1.6)<br/> -netcoreapp1.0 (。NETCoreApp，Version = v1.0)*</span><span class="sxs-lookup"><span data-stu-id="f35d1-241">*Project ServerWeb is not compatible with netstandard1.3 (.NETStandard,Version=v1.3). Project ServerWeb supports:<br/>  - netstandard1.6 (.NETStandard,Version=v1.6)<br/>  - netcoreapp1.0 (.NETCoreApp,Version=v1.0)*</span></span> |
| <span data-ttu-id="f35d1-242">**解决方案**</span><span class="sxs-lookup"><span data-stu-id="f35d1-242">**Solution**</span></span> | <span data-ttu-id="f35d1-243">将项目的目标框架更改为使用项目的相等或更低版本。</span><span class="sxs-lookup"><span data-stu-id="f35d1-243">Change the project's target framework to an equal or lower version than the consuming project.</span></span> |

### <a name="nu1202"></a><span data-ttu-id="f35d1-244">NU1202</span><span class="sxs-lookup"><span data-stu-id="f35d1-244">NU1202</span></span>

| | |
| --- | --- |
| <span data-ttu-id="f35d1-245">**问题**</span><span class="sxs-lookup"><span data-stu-id="f35d1-245">**Issue**</span></span> | <span data-ttu-id="f35d1-246">依赖项包不包含任何与项目兼容的资产。</span><span class="sxs-lookup"><span data-stu-id="f35d1-246">A dependency package doesn't contain any assets compatible with the project.</span></span> |
| <span data-ttu-id="f35d1-247">**示例消息**</span><span class="sxs-lookup"><span data-stu-id="f35d1-247">**Example message**</span></span> | <span data-ttu-id="f35d1-248">*包 System.ComponentModel.EventBasedAsync 4.0.11 与不兼容 netstandard1.3 (。NETStandard，Version = v1.3)。打包 System.ComponentModel.EventBasedAsync 4.0.11 支持：<br/> -monoandroid10 (MonoAndroid，Version = v1.0)<br/> -monotouch10 (MonoTouch，Version = v1.0)<br/> -net45 (。NETFramework，Version = v4.5)<br/> -netcore50 (。NETCore，Version = 5.0 版)<br/> -netstandard1.0 (。NETStandard，Version = v1.0)<br/> -可移植 net45 + win8 + wp8 + wpa81 (。NETPortable，Version = v0.0，配置文件 = Profile259)<br/> -win8 (Windows、 版本 = v8.0)<br/> -wp8 (WindowsPhone，Version = v8.0)<br/> -wpa81 (WindowsPhoneApp，Version = v8.1)<br/> -xamarinios10 (Xamarin.iOS,Version=v1.0)<br/> -xamarinmac20 (Xamarin.Mac,Version=v2.0)<br/> -xamarintvos10 (Xamarin.TVOS,Version=v1.0)<br/> -xamarinwatchos10 (Xamarin.WatchOS,Version=v1.0)*</span><span class="sxs-lookup"><span data-stu-id="f35d1-248">*Package System.ComponentModel.EventBasedAsync 4.0.11 is not compatible with netstandard1.3 (.NETStandard,Version=v1.3). Package System.ComponentModel.EventBasedAsync 4.0.11 supports:<br/>  - monoandroid10 (MonoAndroid,Version=v1.0)<br/>  - monotouch10 (MonoTouch,Version=v1.0)<br/>  - net45 (.NETFramework,Version=v4.5)<br/>  - netcore50 (.NETCore,Version=v5.0)<br/>  - netstandard1.0 (.NETStandard,Version=v1.0)<br/>  - portable-net45+win8+wp8+wpa81 (.NETPortable,Version=v0.0,Profile=Profile259)<br/>  - win8 (Windows,Version=v8.0)<br/>  - wp8 (WindowsPhone,Version=v8.0)<br/>  - wpa81 (WindowsPhoneApp,Version=v8.1)<br/>  - xamarinios10 (Xamarin.iOS,Version=v1.0)<br/>  - xamarinmac20 (Xamarin.Mac,Version=v2.0)<br/>  - xamarintvos10 (Xamarin.TVOS,Version=v1.0)<br/>  - xamarinwatchos10 (Xamarin.WatchOS,Version=v1.0)*</span></span>|
| <span data-ttu-id="f35d1-249">**解决方案**</span><span class="sxs-lookup"><span data-stu-id="f35d1-249">**Solution**</span></span> | <span data-ttu-id="f35d1-250">将项目的目标框架更改为另一个包支持。</span><span class="sxs-lookup"><span data-stu-id="f35d1-250">Change the project's target framework to one that the package supports.</span></span> |

### <a name="nu1203"></a><span data-ttu-id="f35d1-251">NU1203</span><span class="sxs-lookup"><span data-stu-id="f35d1-251">NU1203</span></span>

| | |
| --- | --- |
| <span data-ttu-id="f35d1-252">**问题**</span><span class="sxs-lookup"><span data-stu-id="f35d1-252">**Issue**</span></span> | <span data-ttu-id="f35d1-253">包不支持项目的`RuntimeIdentifier`。</span><span class="sxs-lookup"><span data-stu-id="f35d1-253">The package doesn't support the project's `RuntimeIdentifier`.</span></span> |
| <span data-ttu-id="f35d1-254">**示例消息**</span><span class="sxs-lookup"><span data-stu-id="f35d1-254">**Example message**</span></span> | <span data-ttu-id="f35d1-255">*System.Example 1.0.0 提供 a.dll 的编译时引用程序集上 net461，但没有兼容的运行时程序集。*</span><span class="sxs-lookup"><span data-stu-id="f35d1-255">*System.Example 1.0.0 provides a compile-time reference assembly for a.dll on net461, but there is no compatible run-time assembly.*</span></span> |
| <span data-ttu-id="f35d1-256">**解决方案**</span><span class="sxs-lookup"><span data-stu-id="f35d1-256">**Solution**</span></span> | <span data-ttu-id="f35d1-257">更改`RuntimeIdentifier`根据需要在项目中使用的值。</span><span class="sxs-lookup"><span data-stu-id="f35d1-257">Change the `RuntimeIdentifier` values used in the project as needed.</span></span> |

### <a name="nu1401"></a><span data-ttu-id="f35d1-258">NU1401</span><span class="sxs-lookup"><span data-stu-id="f35d1-258">NU1401</span></span>

| | |
| --- | --- |
| <span data-ttu-id="f35d1-259">**问题**</span><span class="sxs-lookup"><span data-stu-id="f35d1-259">**Issue**</span></span> | <span data-ttu-id="f35d1-260">包需要功能或框架当前不支持安装的 NuGet 版本。</span><span class="sxs-lookup"><span data-stu-id="f35d1-260">The package requires features or frameworks not currently supported by the installed version of NuGet.</span></span> |
| <span data-ttu-id="f35d1-261">**示例消息**</span><span class="sxs-lookup"><span data-stu-id="f35d1-261">**Example message**</span></span> | <span data-ttu-id="f35d1-262">*NuGet.Versioning 程序包需要 NuGet 客户端版本"5.0.0"或更高版本，但是当前 NuGet 版本为"4.3.0"。*</span><span class="sxs-lookup"><span data-stu-id="f35d1-262">*The 'NuGet.Versioning' package requires NuGet client version '5.0.0' or above, but the current NuGet version is '4.3.0'.*</span></span> |
| <span data-ttu-id="f35d1-263">**解决方案**</span><span class="sxs-lookup"><span data-stu-id="f35d1-263">**Solution**</span></span> | <span data-ttu-id="f35d1-264">安装较新版本的 NuGet。</span><span class="sxs-lookup"><span data-stu-id="f35d1-264">Install a newer version of NuGet.</span></span> <span data-ttu-id="f35d1-265">请参阅[安装 NuGet 客户端工具](../install-nuget-client-tools.md)。</span><span class="sxs-lookup"><span data-stu-id="f35d1-265">See [Installing NuGet client tools](../install-nuget-client-tools.md).</span></span> |

## <a name="invalid-input-warnings"></a><span data-ttu-id="f35d1-266">无效的输入的警告</span><span class="sxs-lookup"><span data-stu-id="f35d1-266">Invalid input warnings</span></span>

<span data-ttu-id="f35d1-267">[NU1501](#nu1501) | [NU1502](#nu1502) | [NU1503](#nu1503)</span><span class="sxs-lookup"><span data-stu-id="f35d1-267">[NU1501](#nu1501) | [NU1502](#nu1502) | [NU1503](#nu1503)</span></span>

### <a name="nu1501"></a><span data-ttu-id="f35d1-268">NU1501</span><span class="sxs-lookup"><span data-stu-id="f35d1-268">NU1501</span></span>

| | |
| --- | --- |
| <span data-ttu-id="f35d1-269">**问题**</span><span class="sxs-lookup"><span data-stu-id="f35d1-269">**Issue**</span></span> | <span data-ttu-id="f35d1-270">项目还原尝试运行在未找到。</span><span class="sxs-lookup"><span data-stu-id="f35d1-270">The project restore is attempting to operate on was not found.</span></span> |
| <span data-ttu-id="f35d1-271">**示例消息**</span><span class="sxs-lookup"><span data-stu-id="f35d1-271">**Example message**</span></span> | <span data-ttu-id="f35d1-272">*文件夹 c:\projects\a 不包含要还原的项目。*</span><span class="sxs-lookup"><span data-stu-id="f35d1-272">*The folder 'c:\projects\a' does not contain a project to restore.*</span></span> |
| <span data-ttu-id="f35d1-273">**解决方案**</span><span class="sxs-lookup"><span data-stu-id="f35d1-273">**Solution**</span></span> | <span data-ttu-id="f35d1-274">在包含项目的文件夹中运行 nuget 还原。</span><span class="sxs-lookup"><span data-stu-id="f35d1-274">Run nuget restore in a folder that contains a project.</span></span> |

### <a name="nu1502"></a><span data-ttu-id="f35d1-275">NU1502</span><span class="sxs-lookup"><span data-stu-id="f35d1-275">NU1502</span></span>

| | |
| --- | --- |
| <span data-ttu-id="f35d1-276">**问题**</span><span class="sxs-lookup"><span data-stu-id="f35d1-276">**Issue**</span></span> | <span data-ttu-id="f35d1-277">`RuntimeSupports` 包含无效的配置文件。</span><span class="sxs-lookup"><span data-stu-id="f35d1-277">`RuntimeSupports` contains an invalid profile.</span></span> <span data-ttu-id="f35d1-278">通常情况下，支持配置文件中找不`runtime.json`从当前的依赖项包文件。</span><span class="sxs-lookup"><span data-stu-id="f35d1-278">Typically, the supports profile was not found in a `runtime.json` file from the current dependency packages.</span></span>|
| <span data-ttu-id="f35d1-279">**示例消息**</span><span class="sxs-lookup"><span data-stu-id="f35d1-279">**Example message**</span></span> | <span data-ttu-id="f35d1-280">*未知的兼容性配置文件： aaa*</span><span class="sxs-lookup"><span data-stu-id="f35d1-280">*Unknown Compatibility Profile: aaa*</span></span> |
| <span data-ttu-id="f35d1-281">**解决方案**</span><span class="sxs-lookup"><span data-stu-id="f35d1-281">**Solution**</span></span> | <span data-ttu-id="f35d1-282">检查`RuntimeSupports`项目中的值。</span><span class="sxs-lookup"><span data-stu-id="f35d1-282">Check the `RuntimeSupports` value in your project.</span></span> |

### <a name="nu1503"></a><span data-ttu-id="f35d1-283">NU1503</span><span class="sxs-lookup"><span data-stu-id="f35d1-283">NU1503</span></span>

| | |
| --- | --- |
| <span data-ttu-id="f35d1-284">**问题**</span><span class="sxs-lookup"><span data-stu-id="f35d1-284">**Issue**</span></span> | <span data-ttu-id="f35d1-285">依赖项项目不能导入 NuGet 的恢复目标。</span><span class="sxs-lookup"><span data-stu-id="f35d1-285">A dependency project doesn't import NuGet's restore targets.</span></span> <span data-ttu-id="f35d1-286">这是类似于 NU1105 但此处项目，将跳过并忽略而不是导致所有还原失败。</span><span class="sxs-lookup"><span data-stu-id="f35d1-286">This is similar to NU1105 but here the project is skipped and ignored instead of causing all of restore to fail.</span></span> <span data-ttu-id="f35d1-287">在复杂的解决方案通常有其他类型的可能不支持还原的项目中。</span><span class="sxs-lookup"><span data-stu-id="f35d1-287">In complex solutions there are often other types of projects that may not support restore.</span></span> |
| <span data-ttu-id="f35d1-288">**示例消息**</span><span class="sxs-lookup"><span data-stu-id="f35d1-288">**Example message**</span></span> | <span data-ttu-id="f35d1-289">*正在跳过还原项目 c:\a.csproj。项目文件可能无效或缺少所需的还原的目标。*</span><span class="sxs-lookup"><span data-stu-id="f35d1-289">*Skipping restore for project 'c:\a.csproj'. The project file may be invalid or missing targets required for restore.*</span></span> |
| <span data-ttu-id="f35d1-290">**解决方案**</span><span class="sxs-lookup"><span data-stu-id="f35d1-290">**Solution**</span></span> | <span data-ttu-id="f35d1-291">这可能会导致不导入公共属性/目标的自动导入还原的项目。</span><span class="sxs-lookup"><span data-stu-id="f35d1-291">This can happen for projects that do not import common props/targets which automatically import restore.</span></span> <span data-ttu-id="f35d1-292">如果项目不需要还原这可予以忽视。</span><span class="sxs-lookup"><span data-stu-id="f35d1-292">If the project doesn't need to be restored this can be ignored.</span></span> <span data-ttu-id="f35d1-293">否则，编辑受影响的项目添加为还原的目标。</span><span class="sxs-lookup"><span data-stu-id="f35d1-293">Otherwise, edit the affected project to add targets for restore.</span></span> |

## <a name="unexpected-package-version-warnings"></a><span data-ttu-id="f35d1-294">意外的包版本警告</span><span class="sxs-lookup"><span data-stu-id="f35d1-294">Unexpected package version warnings</span></span>

<span data-ttu-id="f35d1-295">[NU1601](#nu1601) | [NU1602](#nu1602) | [NU1603](#nu1603) | [NU1604](#nu1604) | [NU1605](#nu1605)</span><span class="sxs-lookup"><span data-stu-id="f35d1-295">[NU1601](#nu1601) | [NU1602](#nu1602) | [NU1603](#nu1603) | [NU1604](#nu1604) | [NU1605](#nu1605)</span></span>

### <a name="nu1601"></a><span data-ttu-id="f35d1-296">NU1601</span><span class="sxs-lookup"><span data-stu-id="f35d1-296">NU1601</span></span>

| | |
| --- | --- |
| <span data-ttu-id="f35d1-297">**问题**</span><span class="sxs-lookup"><span data-stu-id="f35d1-297">**Issue**</span></span> | <span data-ttu-id="f35d1-298">直接项目依赖项已解除了一个为更高版本比指定的项目。</span><span class="sxs-lookup"><span data-stu-id="f35d1-298">A direct project dependency was bumped to a higher version than the project specified.</span></span> |
| <span data-ttu-id="f35d1-299">**示例消息**</span><span class="sxs-lookup"><span data-stu-id="f35d1-299">**Example message**</span></span> | <span data-ttu-id="f35d1-300">*指定的依赖项已 NuGet.Versioning (> = 3.5.0) 但最终的 NuGet.Versioning 4.0.0。*</span><span class="sxs-lookup"><span data-stu-id="f35d1-300">*Dependency specified was NuGet.Versioning (>= 3.5.0) but ended up with NuGet.Versioning 4.0.0.*</span></span> |
| <span data-ttu-id="f35d1-301">**解决方案**</span><span class="sxs-lookup"><span data-stu-id="f35d1-301">**Solution**</span></span> | <span data-ttu-id="f35d1-302">更新到适当版本的项目中的依赖关系。</span><span class="sxs-lookup"><span data-stu-id="f35d1-302">Update the dependency in the project to an appropriate version.</span></span> |

### <a name="nu1602"></a><span data-ttu-id="f35d1-303">NU1602</span><span class="sxs-lookup"><span data-stu-id="f35d1-303">NU1602</span></span>

| | |
| --- | --- |
| <span data-ttu-id="f35d1-304">**问题**</span><span class="sxs-lookup"><span data-stu-id="f35d1-304">**Issue**</span></span> | <span data-ttu-id="f35d1-305">包依赖项缺少零下限。</span><span class="sxs-lookup"><span data-stu-id="f35d1-305">A package dependency is missing a lower bound.</span></span> <span data-ttu-id="f35d1-306">这不允许还原，以便查找*最佳匹配*。</span><span class="sxs-lookup"><span data-stu-id="f35d1-306">This doesn't allow restore to find the *best match*.</span></span> <span data-ttu-id="f35d1-307">每个还原将浮动向下尝试查找可以使用较低版本。</span><span class="sxs-lookup"><span data-stu-id="f35d1-307">Each restore will float downwards trying to find a lower version that can be used.</span></span> <span data-ttu-id="f35d1-308">这意味着此恢复将进入联机状态，以检查每个时间而不是在用户程序包文件夹中使用已存在的包的所有源。</span><span class="sxs-lookup"><span data-stu-id="f35d1-308">This means that restore goes online to check all sources each time instead of using the packages that already exist in the user package folder.</span></span> |
| <span data-ttu-id="f35d1-309">**示例消息**</span><span class="sxs-lookup"><span data-stu-id="f35d1-309">**Example message**</span></span> | <span data-ttu-id="f35d1-310">*NuGet.Packaging 4.0.0 不依赖项 NuGet.Versioning (> 3.5.0) 提供包含下限。3.6.0 的近似最佳匹配已解决。*</span><span class="sxs-lookup"><span data-stu-id="f35d1-310">*NuGet.Packaging 4.0.0 does not provide an inclusive lower bound for dependency NuGet.Versioning (> 3.5.0). An approximate best match of 3.6.0 was resolved.*</span></span> |
| <span data-ttu-id="f35d1-311">**解决方案**</span><span class="sxs-lookup"><span data-stu-id="f35d1-311">**Solution**</span></span> | <span data-ttu-id="f35d1-312">这通常是创作错误的包。</span><span class="sxs-lookup"><span data-stu-id="f35d1-312">This is usually a package authoring error.</span></span> <span data-ttu-id="f35d1-313">请联系程序包作者以解决此问题。</span><span class="sxs-lookup"><span data-stu-id="f35d1-313">Contact the package author to resolve the issue.</span></span> |

### <a name="nu1603"></a><span data-ttu-id="f35d1-314">NU1603</span><span class="sxs-lookup"><span data-stu-id="f35d1-314">NU1603</span></span>

| | |
| --- | --- |
| <span data-ttu-id="f35d1-315">**问题**</span><span class="sxs-lookup"><span data-stu-id="f35d1-315">**Issue**</span></span> | <span data-ttu-id="f35d1-316">包依赖项指定未找到的版本。</span><span class="sxs-lookup"><span data-stu-id="f35d1-316">A package dependency specified a version that could not be found.</span></span> <span data-ttu-id="f35d1-317">通常情况下，包源中不包含预期的下限版本。</span><span class="sxs-lookup"><span data-stu-id="f35d1-317">Typically, the package sources do not contain the expected lower bound version.</span></span> <span data-ttu-id="f35d1-318">与它不同的包编写针对相反，使用更高版本。</span><span class="sxs-lookup"><span data-stu-id="f35d1-318">A higher version was used instead, which differs from what the package was authored against.</span></span><br/><br/><span data-ttu-id="f35d1-319">这意味着找不到该还原*最佳匹配*。</span><span class="sxs-lookup"><span data-stu-id="f35d1-319">This means that restore did not find the *best match*.</span></span> <span data-ttu-id="f35d1-320">每个还原将浮动向下尝试查找可以使用较低版本。</span><span class="sxs-lookup"><span data-stu-id="f35d1-320">Each restore will float downwards trying to find a lower version that can be used.</span></span> <span data-ttu-id="f35d1-321">这意味着此恢复将进入联机状态，以检查每个时间而不是在用户程序包文件夹中使用已存在的包的所有源。</span><span class="sxs-lookup"><span data-stu-id="f35d1-321">This means that restore goes online to check all sources each time instead of using the packages that already exist in the user package folder.</span></span> |
| <span data-ttu-id="f35d1-322">**示例消息**</span><span class="sxs-lookup"><span data-stu-id="f35d1-322">**Example message**</span></span> | <span data-ttu-id="f35d1-323">NuGet.Packaging 4.0.0 取决于 NuGet.Versioning (> = 4.0.0) 但找不到 4.0.0。</span><span class="sxs-lookup"><span data-stu-id="f35d1-323">NuGet.Packaging 4.0.0 depends on NuGet.Versioning (>= 4.0.0) but 4.0.0 was not found.</span></span> <span data-ttu-id="f35d1-324">5.0.0 的近似最佳匹配已解决。</span><span class="sxs-lookup"><span data-stu-id="f35d1-324">An approximate best match of 5.0.0 was resolved.</span></span> |
| <span data-ttu-id="f35d1-325">**解决方案**</span><span class="sxs-lookup"><span data-stu-id="f35d1-325">**Solution**</span></span> | <span data-ttu-id="f35d1-326">如果尚未释放预期包，这可能是包创作错误。</span><span class="sxs-lookup"><span data-stu-id="f35d1-326">If the package expected has not been released then this may be a package authoring error.</span></span> <span data-ttu-id="f35d1-327">请联系程序包作者以解决此问题。</span><span class="sxs-lookup"><span data-stu-id="f35d1-327">Contact the package author to resolve the issue.</span></span> <span data-ttu-id="f35d1-328">如果已发布包，然后检查它是否可用上正在使用的包源。</span><span class="sxs-lookup"><span data-stu-id="f35d1-328">If the package has been released, then check that it's available on the package sources you're using.</span></span> <span data-ttu-id="f35d1-329">如果使用私有源时，你可能需要更新上的源的包。</span><span class="sxs-lookup"><span data-stu-id="f35d1-329">If using a private source, you may need to update the package on that feed.</span></span> |

### <a name="nu1604"></a><span data-ttu-id="f35d1-330">NU1604</span><span class="sxs-lookup"><span data-stu-id="f35d1-330">NU1604</span></span>

| | |
| --- | --- |
| <span data-ttu-id="f35d1-331">**问题**</span><span class="sxs-lookup"><span data-stu-id="f35d1-331">**Issue**</span></span> | <span data-ttu-id="f35d1-332">项目依赖项未定义零下限。</span><span class="sxs-lookup"><span data-stu-id="f35d1-332">A project dependency doesn't define a lower bound.</span></span><br/><br/><span data-ttu-id="f35d1-333">这意味着找不到该还原*最佳匹配*。</span><span class="sxs-lookup"><span data-stu-id="f35d1-333">This means that restore did not find the *best match*.</span></span> <span data-ttu-id="f35d1-334">每个还原将浮动向下尝试查找可以使用较低版本。</span><span class="sxs-lookup"><span data-stu-id="f35d1-334">Each restore will float downwards trying to find a lower version that can be used.</span></span> <span data-ttu-id="f35d1-335">这意味着此恢复将进入联机状态，以检查每个时间而不是在用户程序包文件夹中使用已存在的包的所有源。</span><span class="sxs-lookup"><span data-stu-id="f35d1-335">This means that restore goes online to check all sources each time instead of using the packages that already exist in the user package folder.</span></span> |
| <span data-ttu-id="f35d1-336">**示例消息**</span><span class="sxs-lookup"><span data-stu-id="f35d1-336">**Example message**</span></span> | <span data-ttu-id="f35d1-337">*项目依赖项 NuGet.Versioning (< = 9.0.0) doe 不包含包含下限。依赖项版本以确保一致还原结果中包括零下限。*</span><span class="sxs-lookup"><span data-stu-id="f35d1-337">*Project dependency NuGet.Versioning (<= 9.0.0) doe not contain an inclusive lower bound. Include a lower bound in the dependency version to ensure consistent restore results.*</span></span> |
| <span data-ttu-id="f35d1-338">**解决方案**</span><span class="sxs-lookup"><span data-stu-id="f35d1-338">**Solution**</span></span> | <span data-ttu-id="f35d1-339">更新项目的`PackageReference``Version`属性以包括零下限。</span><span class="sxs-lookup"><span data-stu-id="f35d1-339">Update the project's `PackageReference` `Version` attribute to include a lower bound.</span></span> |

### <a name="nu1605"></a><span data-ttu-id="f35d1-340">NU1605</span><span class="sxs-lookup"><span data-stu-id="f35d1-340">NU1605</span></span>

| | |
| --- | --- |
| <span data-ttu-id="f35d1-341">**问题**</span><span class="sxs-lookup"><span data-stu-id="f35d1-341">**Issue**</span></span> | <span data-ttu-id="f35d1-342">依赖项包指定比还原最终解决更高版本的包的版本约束。</span><span class="sxs-lookup"><span data-stu-id="f35d1-342">A dependency package specified a version constraint on a higher version of a package than restore ultimately resolved.</span></span> <span data-ttu-id="f35d1-343">也就是说，"最接近的 wins"规则在解析包时，由于在图中的最近包可能已重写相距包。</span><span class="sxs-lookup"><span data-stu-id="f35d1-343">That is, because of the "nearest wins" rule when resolving packages, a nearer package in the graph may have overridden a distant package.</span></span> |
| <span data-ttu-id="f35d1-344">**示例消息**</span><span class="sxs-lookup"><span data-stu-id="f35d1-344">**Example message**</span></span> | <span data-ttu-id="f35d1-345">*检测到包降级： NuGet.Versioning 从 4.0.0 到 3.5.0。要选择的不同版本的项目中直接引用包。<br/>NuGet.Packaging 3.5.0-> NuGet.Versioning 3.5.0<br/> NuGet.Commands 4.0.0-> NuGet.Configuration 4.0.0-> NuGet.Versioning 4.0.0*</span><span class="sxs-lookup"><span data-stu-id="f35d1-345">*Detected package downgrade: NuGet.Versioning from 4.0.0 to 3.5.0. Reference the package directly from the project to select a different version.<br/>  NuGet.Packaging 3.5.0 -> NuGet.Versioning 3.5.0<br/>  NuGet.Commands 4.0.0 -> NuGet.Configuration 4.0.0 -> NuGet.Versioning 4.0.0*</span></span> |
| <span data-ttu-id="f35d1-346">**解决方案**</span><span class="sxs-lookup"><span data-stu-id="f35d1-346">**Solution**</span></span> | <span data-ttu-id="f35d1-347">添加到你想要使用的包的更高版本的项目的直接引用。</span><span class="sxs-lookup"><span data-stu-id="f35d1-347">Add a direct reference to the project for the higher version of the package that you want to use.</span></span> |

## <a name="resolver-conflict-warnings"></a><span data-ttu-id="f35d1-348">冲突解决程序冲突警告</span><span class="sxs-lookup"><span data-stu-id="f35d1-348">Resolver conflict warnings</span></span>

### <a name="nu1608"></a><span data-ttu-id="f35d1-349">NU1608</span><span class="sxs-lookup"><span data-stu-id="f35d1-349">NU1608</span></span>

| | |
| --- | --- |
| <span data-ttu-id="f35d1-350">**问题**</span><span class="sxs-lookup"><span data-stu-id="f35d1-350">**Issue**</span></span> | <span data-ttu-id="f35d1-351">解决的包是不是依赖项约束允许，更高版本。</span><span class="sxs-lookup"><span data-stu-id="f35d1-351">A resolved package is higher than a dependency constraint allows.</span></span> <span data-ttu-id="f35d1-352">这意味着项目直接引用的包将从其他包的依赖项约束重写。</span><span class="sxs-lookup"><span data-stu-id="f35d1-352">This means that a package referenced directly by a project overrides dependency constraints from other packages.</span></span>|
| <span data-ttu-id="f35d1-353">**示例消息**</span><span class="sxs-lookup"><span data-stu-id="f35d1-353">**Example message**</span></span> | <span data-ttu-id="f35d1-354">*外部依赖关系约束的检测到的包版本： x 1.0.0 要求的 y （= 1.0.0），但版本 y 2.0.0 为已解决。*</span><span class="sxs-lookup"><span data-stu-id="f35d1-354">*Detected package version outside of dependency constraint: x 1.0.0 requires y (= 1.0.0) but version y 2.0.0 was resolved.*</span></span> |
| <span data-ttu-id="f35d1-355">**解决方案**</span><span class="sxs-lookup"><span data-stu-id="f35d1-355">**Solution**</span></span> | <span data-ttu-id="f35d1-356">在某些情况下，这是有意，可以禁止显示警告。</span><span class="sxs-lookup"><span data-stu-id="f35d1-356">In some cases this is intentional and the warning can be suppressed.</span></span> <span data-ttu-id="f35d1-357">否则，更改以扩大其版本约束的包项目的引用。</span><span class="sxs-lookup"><span data-stu-id="f35d1-357">Otherwise, change the project's reference to the package to widen its version constraints.</span></span> |

## <a name="package-fallback-warnings"></a><span data-ttu-id="f35d1-358">包回退警告</span><span class="sxs-lookup"><span data-stu-id="f35d1-358">Package fallback warnings</span></span>

### <a name="nu1701"></a><span data-ttu-id="f35d1-359">NU1701</span><span class="sxs-lookup"><span data-stu-id="f35d1-359">NU1701</span></span>

| | |
| --- | --- |
| <span data-ttu-id="f35d1-360">**问题**</span><span class="sxs-lookup"><span data-stu-id="f35d1-360">**Issue**</span></span> | <span data-ttu-id="f35d1-361">`PackageTargetFallback` / `AssetTargetFallback` 用来从包选择资产。</span><span class="sxs-lookup"><span data-stu-id="f35d1-361">`PackageTargetFallback` / `AssetTargetFallback` was used to select assets from a package.</span></span> <span data-ttu-id="f35d1-362">警告让用户知道资产可能不兼容的 100%。</span><span class="sxs-lookup"><span data-stu-id="f35d1-362">The warning let users know that the assets may not be 100% compatible.</span></span> |
| <span data-ttu-id="f35d1-363">**示例消息**</span><span class="sxs-lookup"><span data-stu-id="f35d1-363">**Example message**</span></span> | <span data-ttu-id="f35d1-364">*包 NuGet.Versioning 已还原可移植 net45 + win8 改为使用项目目标框架 netstandard1.5。此程序包并不一定与你的项目完全兼容。*</span><span class="sxs-lookup"><span data-stu-id="f35d1-364">*Package 'NuGet.Versioning' was restored using 'portable-net45+win8' instead the project target framework 'netstandard1.5'. This package may not be fully compatible with your project.*</span></span> |
| <span data-ttu-id="f35d1-365">**解决方案**</span><span class="sxs-lookup"><span data-stu-id="f35d1-365">**Solution**</span></span> | <span data-ttu-id="f35d1-366">将项目的目标框架更改为另一个包支持。</span><span class="sxs-lookup"><span data-stu-id="f35d1-366">Change the project's target framework to one that the package supports.</span></span> |

## <a name="feed-warnings"></a><span data-ttu-id="f35d1-367">源警告</span><span class="sxs-lookup"><span data-stu-id="f35d1-367">Feed warnings</span></span>

### <a name="nu1801"></a><span data-ttu-id="f35d1-368">NU1801</span><span class="sxs-lookup"><span data-stu-id="f35d1-368">NU1801</span></span>

| | |
| --- | --- |
| <span data-ttu-id="f35d1-369">**问题**</span><span class="sxs-lookup"><span data-stu-id="f35d1-369">**Issue**</span></span> | <span data-ttu-id="f35d1-370">读取源时出错时`IgnoreFailedSources`设置为 true，将其转换为非致命性警告。</span><span class="sxs-lookup"><span data-stu-id="f35d1-370">An error occurred when reading the feed when `IgnoreFailedSources` is set to true, converting it to a non-fatal warning.</span></span> <span data-ttu-id="f35d1-371">这可能包含的任何消息，并为泛型。</span><span class="sxs-lookup"><span data-stu-id="f35d1-371">This could contain any message and is generic.</span></span> |
| <span data-ttu-id="f35d1-372">**示例消息**</span><span class="sxs-lookup"><span data-stu-id="f35d1-372">**Example message**</span></span> | <span data-ttu-id="f35d1-373">n/a</span><span class="sxs-lookup"><span data-stu-id="f35d1-373">n/a</span></span> |
| <span data-ttu-id="f35d1-374">**解决方案**</span><span class="sxs-lookup"><span data-stu-id="f35d1-374">**Solution**</span></span> | <span data-ttu-id="f35d1-375">编辑你的配置来指定有效的源。</span><span class="sxs-lookup"><span data-stu-id="f35d1-375">Edit your configuration to specify valid sources.</span></span> |

## <a name="nuget-internal-errors-and-warnings"></a><span data-ttu-id="f35d1-376">NuGet 内部错误和警告</span><span class="sxs-lookup"><span data-stu-id="f35d1-376">NuGet internal errors and warnings</span></span>

<span data-ttu-id="f35d1-377">[NU1000](#nu1000) | [NU1500](#nu1500)</span><span class="sxs-lookup"><span data-stu-id="f35d1-377">[NU1000](#nu1000) | [NU1500](#nu1500)</span></span>

### <a name="nu1000"></a><span data-ttu-id="f35d1-378">NU1000</span><span class="sxs-lookup"><span data-stu-id="f35d1-378">NU1000</span></span>

| | |
| --- | --- |
| <span data-ttu-id="f35d1-379">**问题**</span><span class="sxs-lookup"><span data-stu-id="f35d1-379">**Issue**</span></span> | <span data-ttu-id="f35d1-380">从 NuGet 非特定的内部错误。</span><span class="sxs-lookup"><span data-stu-id="f35d1-380">A non specific internal error from NuGet.</span></span> |
| <span data-ttu-id="f35d1-381">**解决方案**</span><span class="sxs-lookup"><span data-stu-id="f35d1-381">**Solution**</span></span> | <span data-ttu-id="f35d1-382">检查日志以了解更多信息</span><span class="sxs-lookup"><span data-stu-id="f35d1-382">Check the logs for more information</span></span> |

### <a name="nu1500"></a><span data-ttu-id="f35d1-383">NU1500</span><span class="sxs-lookup"><span data-stu-id="f35d1-383">NU1500</span></span>

| | |
| --- | --- |
| <span data-ttu-id="f35d1-384">**问题**</span><span class="sxs-lookup"><span data-stu-id="f35d1-384">**Issue**</span></span> | <span data-ttu-id="f35d1-385">从 NuGet 内部非特定警告。</span><span class="sxs-lookup"><span data-stu-id="f35d1-385">A non specific internal warning from NuGet.</span></span> |
| <span data-ttu-id="f35d1-386">**解决方案**</span><span class="sxs-lookup"><span data-stu-id="f35d1-386">**Solution**</span></span> | <span data-ttu-id="f35d1-387">检查日志以了解更多信息</span><span class="sxs-lookup"><span data-stu-id="f35d1-387">Check the logs for more information</span></span> |

## <a name="signed-packages-creation-and-verification"></a><span data-ttu-id="f35d1-388">已签名的软件包 （创建和验证）</span><span class="sxs-lookup"><span data-stu-id="f35d1-388">Signed packages (creation and verification)</span></span>

<span data-ttu-id="f35d1-389">*NuGet 4.6.0+*</span><span class="sxs-lookup"><span data-stu-id="f35d1-389">*NuGet 4.6.0+*</span></span>

<span data-ttu-id="f35d1-390">[NU3000](#nu3000) | [NU3001](#nu3001) | [NU3002](#nu3002) | [NU3004](#nu3004) | [NU3008](#nu3008) | [NU3018](#nu3018) | [NU3028](#nu3028)</span><span class="sxs-lookup"><span data-stu-id="f35d1-390">[NU3000](#nu3000) | [NU3001](#nu3001) | [NU3002](#nu3002) | [NU3004](#nu3004) | [NU3008](#nu3008) | [NU3018](#nu3018) | [NU3028](#nu3028)</span></span>

### <a name="nu3000"></a><span data-ttu-id="f35d1-391">NU3000</span><span class="sxs-lookup"><span data-stu-id="f35d1-391">NU3000</span></span>

| | |
| --- | --- |
| <span data-ttu-id="f35d1-392">**问题**</span><span class="sxs-lookup"><span data-stu-id="f35d1-392">**Issue**</span></span> | <span data-ttu-id="f35d1-393">非特定错误相关的包签名和签名包验证。</span><span class="sxs-lookup"><span data-stu-id="f35d1-393">A non-specific error related to package signing and signed package verification.</span></span> |
| <span data-ttu-id="f35d1-394">**解决方案**</span><span class="sxs-lookup"><span data-stu-id="f35d1-394">**Solution**</span></span> | <span data-ttu-id="f35d1-395">请检查日志以了解更多信息。</span><span class="sxs-lookup"><span data-stu-id="f35d1-395">Check the logs for more information.</span></span> |

### <a name="nu3001"></a><span data-ttu-id="f35d1-396">NU3001</span><span class="sxs-lookup"><span data-stu-id="f35d1-396">NU3001</span></span>

| | |
| --- | --- |
| <span data-ttu-id="f35d1-397">**问题**</span><span class="sxs-lookup"><span data-stu-id="f35d1-397">**Issue**</span></span> | <span data-ttu-id="f35d1-398">无效的自变量为[登录命令](../tools/cli-ref-sign.md)或[验证命令](../tools/cli-ref-verify.md)。</span><span class="sxs-lookup"><span data-stu-id="f35d1-398">Invalid arguments to either the [sign command](../tools/cli-ref-sign.md) or the [verify command](../tools/cli-ref-verify.md).</span></span> |
| <span data-ttu-id="f35d1-399">**解决方案**</span><span class="sxs-lookup"><span data-stu-id="f35d1-399">**Solution**</span></span> | <span data-ttu-id="f35d1-400">检查并更正提供的自变量。</span><span class="sxs-lookup"><span data-stu-id="f35d1-400">Check and correct the arguments provided.</span></span> |

### <a name="nu3002"></a><span data-ttu-id="f35d1-401">NU3002</span><span class="sxs-lookup"><span data-stu-id="f35d1-401">NU3002</span></span>

| | |
| --- | --- |
| <span data-ttu-id="f35d1-402">**问题**</span><span class="sxs-lookup"><span data-stu-id="f35d1-402">**Issue**</span></span> | <span data-ttu-id="f35d1-403">`-Timestamper`选项未指定与[nuget 登录命令](../tools/cli-ref-sign.md)。</span><span class="sxs-lookup"><span data-stu-id="f35d1-403">The `-Timestamper` option was not specified with the [nuget sign command](../tools/cli-ref-sign.md).</span></span> |
| <span data-ttu-id="f35d1-404">**示例消息**</span><span class="sxs-lookup"><span data-stu-id="f35d1-404">**Example message**</span></span> | <span data-ttu-id="f35d1-405">*-Timestamper 未提供选项。签名的包不会加盖时间戳。*</span><span class="sxs-lookup"><span data-stu-id="f35d1-405">*The '-Timestamper' option was not provided. The signed package will not be timestamped.*</span></span> |
| <span data-ttu-id="f35d1-406">**解决方案**</span><span class="sxs-lookup"><span data-stu-id="f35d1-406">**Solution**</span></span> | <span data-ttu-id="f35d1-407">指定`-Timestamper`选项与`nuget sign`。</span><span class="sxs-lookup"><span data-stu-id="f35d1-407">Specify the `-Timestamper` option with `nuget sign`.</span></span> |

### <a name="nu3004"></a><span data-ttu-id="f35d1-408">NU3004</span><span class="sxs-lookup"><span data-stu-id="f35d1-408">NU3004</span></span>

| | |
| --- | --- |
| <span data-ttu-id="f35d1-409">**问题**</span><span class="sxs-lookup"><span data-stu-id="f35d1-409">**Issue**</span></span> | <span data-ttu-id="f35d1-410">未签名的软件包提供给[nuget 验证命令](../tools/cli-ref-verify.md)。</span><span class="sxs-lookup"><span data-stu-id="f35d1-410">An unsigned package was provided to the [nuget verify command](../tools/cli-ref-verify.md).</span></span> |
| <span data-ttu-id="f35d1-411">**解决方案**</span><span class="sxs-lookup"><span data-stu-id="f35d1-411">**Solution**</span></span> | <span data-ttu-id="f35d1-412">运行`nuget verify`与已签名的包。</span><span class="sxs-lookup"><span data-stu-id="f35d1-412">Run `nuget verify` with a signed package.</span></span> <span data-ttu-id="f35d1-413">请参阅[对包签名](../create-packages/Sign-a-Package.md)。</span><span class="sxs-lookup"><span data-stu-id="f35d1-413">See [Sign a package](../create-packages/Sign-a-Package.md).</span></span> |

### <a name="nu3008"></a><span data-ttu-id="f35d1-414">NU3008</span><span class="sxs-lookup"><span data-stu-id="f35d1-414">NU3008</span></span>

| | |
| --- | --- |
| <span data-ttu-id="f35d1-415">**问题**</span><span class="sxs-lookup"><span data-stu-id="f35d1-415">**Issue**</span></span> | <span data-ttu-id="f35d1-416">包完整性检查失败，这意味着已签名的包已被篡改因为正进行签名。</span><span class="sxs-lookup"><span data-stu-id="f35d1-416">The package integrity check failed, meaning that a signed package was tampered with since being signed.</span></span> |
| <span data-ttu-id="f35d1-417">**解决方案**</span><span class="sxs-lookup"><span data-stu-id="f35d1-417">**Solution**</span></span> | <span data-ttu-id="f35d1-418">扫描计算机中的与防病毒软件。</span><span class="sxs-lookup"><span data-stu-id="f35d1-418">Scan your computer with anti-virus software.</span></span> <span data-ttu-id="f35d1-419">然后从计算机中删除包、 重新安装它，和重试该操作。</span><span class="sxs-lookup"><span data-stu-id="f35d1-419">Then remove the package from the computer, reinstall it, and try the operation again.</span></span> <span data-ttu-id="f35d1-420">如果问题仍然存在，请联系的包源的所有者和包所有者。</span><span class="sxs-lookup"><span data-stu-id="f35d1-420">If the problem persists, contact the owner of the package source and the package owner.</span></span> |

### <a name="nu3018"></a><span data-ttu-id="f35d1-421">NU3018</span><span class="sxs-lookup"><span data-stu-id="f35d1-421">NU3018</span></span>

| | |
| --- | --- |
| <span data-ttu-id="f35d1-422">**问题**</span><span class="sxs-lookup"><span data-stu-id="f35d1-422">**Issue**</span></span> | <span data-ttu-id="f35d1-423">证书链生成失败主签名。</span><span class="sxs-lookup"><span data-stu-id="f35d1-423">Certificate chain building failed for the primary signature.</span></span> <span data-ttu-id="f35d1-424">主签名证书不受信任，被吊销，或者该证书的吊销信息不可用。</span><span class="sxs-lookup"><span data-stu-id="f35d1-424">The primary signing certificate is untrusted, revoked, or revocation information for the certificate is unavailable.</span></span> |
| <span data-ttu-id="f35d1-425">**示例消息**</span><span class="sxs-lookup"><span data-stu-id="f35d1-425">**Example message**</span></span> | <span data-ttu-id="f35d1-426">*警告： NU3018： 吊销功能无法检查吊销证书。*</span><span class="sxs-lookup"><span data-stu-id="f35d1-426">*WARNING: NU3018: The revocation function was unable to check revocation for the certificate.*</span></span> |
| <span data-ttu-id="f35d1-427">**解决方案**</span><span class="sxs-lookup"><span data-stu-id="f35d1-427">**Solution**</span></span> | <span data-ttu-id="f35d1-428">使用一个受信任且有效的证书。</span><span class="sxs-lookup"><span data-stu-id="f35d1-428">Use a trusted and valid certificate.</span></span> <span data-ttu-id="f35d1-429">检查 internet 连接。</span><span class="sxs-lookup"><span data-stu-id="f35d1-429">Check internet connectivity.</span></span> |

### <a name="nu3028"></a><span data-ttu-id="f35d1-430">NU3028</span><span class="sxs-lookup"><span data-stu-id="f35d1-430">NU3028</span></span>

| | |
| --- | --- |
| <span data-ttu-id="f35d1-431">**问题**</span><span class="sxs-lookup"><span data-stu-id="f35d1-431">**Issue**</span></span> | <span data-ttu-id="f35d1-432">证书链生成失败的时间戳签名。</span><span class="sxs-lookup"><span data-stu-id="f35d1-432">Certificate chain building failed for the timestamp signature.</span></span> <span data-ttu-id="f35d1-433">时间戳签名证书不受信任，被吊销，或者该证书的吊销信息不可用。</span><span class="sxs-lookup"><span data-stu-id="f35d1-433">The timestamp signing certificate is untrusted, revoked, or revocation information for the certificate is unavailable.</span></span> |
| <span data-ttu-id="f35d1-434">**示例消息**</span><span class="sxs-lookup"><span data-stu-id="f35d1-434">**Example message**</span></span> | <span data-ttu-id="f35d1-435">*警告： NU3028： 吊销功能无法检查吊销证书。*</span><span class="sxs-lookup"><span data-stu-id="f35d1-435">*WARNING: NU3028: The revocation function was unable to check revocation for the certificate.*</span></span> |
| <span data-ttu-id="f35d1-436">**解决方案**</span><span class="sxs-lookup"><span data-stu-id="f35d1-436">**Solution**</span></span> | <span data-ttu-id="f35d1-437">使用一个受信任且有效的证书。</span><span class="sxs-lookup"><span data-stu-id="f35d1-437">Use a trusted and valid certificate.</span></span> <span data-ttu-id="f35d1-438">检查 internet 连接。</span><span class="sxs-lookup"><span data-stu-id="f35d1-438">Check internet connectivity.</span></span> |
