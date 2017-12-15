---
title: "NuGet 还原错误和警告参考 |Microsoft 文档"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 12/13/2017
ms.topic: reference
ms.prod: nuget
ms.technology: 
ms.assetid: b76b8a00-7155-4163-b533-894086d2ef78
description: "警告和错误从 NuGet 包还原期间颁发的完整参考"
keywords: "NuGet 错误、 NuGet 警告诊断"
ms.reviewer:
- anangaur
- karann-msft
- unniravindranathan
ms.openlocfilehash: 3423e30eae07ff0c70a010576b8e701be027b847
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/14/2017
---
# <a name="errors-and-warnings"></a><span data-ttu-id="b7424-104">错误和警告</span><span class="sxs-lookup"><span data-stu-id="b7424-104">Errors and warnings</span></span>

<span data-ttu-id="b7424-105">在 NuGet 4.3.0，错误和警告本主题中所述进行编号，并提供详细的信息来帮助您解决所涉及的问题。</span><span class="sxs-lookup"><span data-stu-id="b7424-105">In NuGet 4.3.0, errors and warnings are numbered as described in this topic and provide detailed information to help you address the issues involved.</span></span> 

<span data-ttu-id="b7424-106">错误和警告在此处列出是仅适用于[PackageReference 基于](../Consume-Packages/Package-References-in-Project-Files.md)项目和 NuGet 4.3.0。</span><span class="sxs-lookup"><span data-stu-id="b7424-106">The errors and warnings listed here are available only with [PackageReference-based](../Consume-Packages/Package-References-in-Project-Files.md) projects and NuGet 4.3.0.</span></span> <span data-ttu-id="b7424-107">NuGet 也服从 MSBuild 属性，以禁止显示警告或将它们提升到错误。</span><span class="sxs-lookup"><span data-stu-id="b7424-107">NuGet also honors MSBuild properties to suppress warnings or elevate them to errors.</span></span> <span data-ttu-id="b7424-108">有关详细信息，请参阅[如何： 禁止显示编译器警告](https://docs.microsoft.com/visualstudio/ide/how-to-suppress-compiler-warnings)Visual Studio 文档中。</span><span class="sxs-lookup"><span data-stu-id="b7424-108">For more information, see [How to: Suppress Compiler Warnings](https://docs.microsoft.com/visualstudio/ide/how-to-suppress-compiler-warnings) in the Visual Studio documentation.</span></span>

<span data-ttu-id="b7424-109">**错误**</span><span class="sxs-lookup"><span data-stu-id="b7424-109">**Errors**</span></span>

| <span data-ttu-id="b7424-110">Group</span><span class="sxs-lookup"><span data-stu-id="b7424-110">Group</span></span> | <span data-ttu-id="b7424-111">错误号</span><span class="sxs-lookup"><span data-stu-id="b7424-111">Error Numbers</span></span> |
| --- | --- |
| [<span data-ttu-id="b7424-112">无效的输入的错误</span><span class="sxs-lookup"><span data-stu-id="b7424-112">Invalid input errors</span></span>](#invalid-input-errors) | <span data-ttu-id="b7424-113">[NU1001](#nu1001)， [NU1002](#nu1002)， [NU1003](#nu1003)</span><span class="sxs-lookup"><span data-stu-id="b7424-113">[NU1001](#nu1001), [NU1002](#nu1002), [NU1003](#nu1003)</span></span> |
| [<span data-ttu-id="b7424-114">缺少的包和项目错误</span><span class="sxs-lookup"><span data-stu-id="b7424-114">Missing package and project errors</span></span>](#missing-package-and-project-errors) | <span data-ttu-id="b7424-115">[NU1100](#nu1100)， [NU1101](#nu1101)， [NU1102](#nu1102)， [NU1103](#nu1103)， [NU1104](#nu1104)， [NU1105](#nu1105)， [NU1106](#nu1106)， [NU1107](#nu1107) (以前 NU1607) [NU1108](#nu1107) (以前 NU1606)</span><span class="sxs-lookup"><span data-stu-id="b7424-115">[NU1100](#nu1100), [NU1101](#nu1101), [NU1102](#nu1102), [NU1103](#nu1103), [NU1104](#nu1104), [NU1105](#nu1105), [NU1106](#nu1106), [NU1107](#nu1107) (previously NU1607), [NU1108](#nu1107) (previously NU1606)</span></span> |
| [<span data-ttu-id="b7424-116">兼容性错误</span><span class="sxs-lookup"><span data-stu-id="b7424-116">Compatibility errors</span></span>](#compatibility-errors) | <span data-ttu-id="b7424-117">[NU1201](#nu1201)， [NU1202](#nu1202)， [NU1203](#nu1203)， [NU1401](#nu1401)</span><span class="sxs-lookup"><span data-stu-id="b7424-117">[NU1201](#nu1201), [NU1202](#nu1202), [NU1203](#nu1203), [NU1401](#nu1401)</span></span> |

<span data-ttu-id="b7424-118">**警告**</span><span class="sxs-lookup"><span data-stu-id="b7424-118">**Warnings**</span></span>

| <span data-ttu-id="b7424-119">Group</span><span class="sxs-lookup"><span data-stu-id="b7424-119">Group</span></span> | <span data-ttu-id="b7424-120">警告编号</span><span class="sxs-lookup"><span data-stu-id="b7424-120">Warning numbers</span></span> |
| --- | --- |
| [<span data-ttu-id="b7424-121">无效的输入的警告</span><span class="sxs-lookup"><span data-stu-id="b7424-121">Invalid input warnings</span></span>](#invalid-input-warnings) | <span data-ttu-id="b7424-122">[NU1501](#nu1501)， [NU1502](#nu1502)， [NU1503](#nu1503)</span><span class="sxs-lookup"><span data-stu-id="b7424-122">[NU1501](#nu1501), [NU1502](#nu1502), [NU1503](#nu1503)</span></span> |
| [<span data-ttu-id="b7424-123">意外的包版本警告</span><span class="sxs-lookup"><span data-stu-id="b7424-123">Unexpected package version warnings</span></span>](#unexpected-package-version-warnings) | <span data-ttu-id="b7424-124">[NU1601](#nu1601)， [NU1602](#nu1602)， [NU1603](#nu1603)， [NU1604](#nu1604)， [NU1605](#nu1605)</span><span class="sxs-lookup"><span data-stu-id="b7424-124">[NU1601](#nu1601), [NU1602](#nu1602), [NU1603](#nu1603), [NU1604](#nu1604), [NU1605](#nu1605)</span></span> |
| [<span data-ttu-id="b7424-125">冲突解决程序冲突警告</span><span class="sxs-lookup"><span data-stu-id="b7424-125">Resolver conflict warnings</span></span>](#resolver-conflict-warnings) | [<span data-ttu-id="b7424-126">NU1608</span><span class="sxs-lookup"><span data-stu-id="b7424-126">NU1608</span></span>](#nu1608) |
| [<span data-ttu-id="b7424-127">包回退警告</span><span class="sxs-lookup"><span data-stu-id="b7424-127">Package fallback warnings</span></span>](#package-fallback-warnings) | [<span data-ttu-id="b7424-128">NU1701</span><span class="sxs-lookup"><span data-stu-id="b7424-128">NU1701</span></span>](#nu1701) |
| [<span data-ttu-id="b7424-129">源警告</span><span class="sxs-lookup"><span data-stu-id="b7424-129">Feed warnings</span></span>](#feed-warnings) | [<span data-ttu-id="b7424-130">NU1801</span><span class="sxs-lookup"><span data-stu-id="b7424-130">NU1801</span></span>](#nu1801) |
| [<span data-ttu-id="b7424-131">NuGet 内部错误和警告</span><span class="sxs-lookup"><span data-stu-id="b7424-131">NuGet internal errors and warnings</span></span>](#nuget-internal-errors-and-warnings) | <span data-ttu-id="b7424-132">[NU1000](#nu1000)， [NU1500](#nu1500)</span><span class="sxs-lookup"><span data-stu-id="b7424-132">[NU1000](#nu1000), [NU1500](#nu1500)</span></span> |

## <a name="invalid-input-errors"></a><span data-ttu-id="b7424-133">无效的输入的错误</span><span class="sxs-lookup"><span data-stu-id="b7424-133">Invalid input errors</span></span>

<span data-ttu-id="b7424-134">[NU1001](#nu1001) | [NU1002](#nu1002) | [NU1003](#nu1003)</span><span class="sxs-lookup"><span data-stu-id="b7424-134">[NU1001](#nu1001) | [NU1002](#nu1002) | [NU1003](#nu1003)</span></span>

### <a name="nu1001"></a><span data-ttu-id="b7424-135">NU1001</span><span class="sxs-lookup"><span data-stu-id="b7424-135">NU1001</span></span>

| | |
| --- | --- |
| <span data-ttu-id="b7424-136">**问题**</span><span class="sxs-lookup"><span data-stu-id="b7424-136">**Issue**</span></span> | <span data-ttu-id="b7424-137">项目不包含一个或多个框架。</span><span class="sxs-lookup"><span data-stu-id="b7424-137">The project doesn't contain one or more frameworks.</span></span> |
| <span data-ttu-id="b7424-138">**常见原因**</span><span class="sxs-lookup"><span data-stu-id="b7424-138">**Common causes**</span></span> | <span data-ttu-id="b7424-139">项目不包含`TargetFramework`或`TargetFrameworks`属性。</span><span class="sxs-lookup"><span data-stu-id="b7424-139">The project doesn't contain a `TargetFramework` or `TargetFrameworks` property.</span></span> |
| <span data-ttu-id="b7424-140">**示例消息**</span><span class="sxs-lookup"><span data-stu-id="b7424-140">**Example message**</span></span> | <span data-ttu-id="b7424-141">*项目 projA c:\tmp\projA.csproj 中未指定任何目标框架*</span><span class="sxs-lookup"><span data-stu-id="b7424-141">*The project projA does not specify any target frameworks in c:\tmp\projA.csproj*</span></span> |

### <a name="nu1002"></a><span data-ttu-id="b7424-142">NU1002</span><span class="sxs-lookup"><span data-stu-id="b7424-142">NU1002</span></span>

| | |
| --- | --- |
| <span data-ttu-id="b7424-143">**问题**</span><span class="sxs-lookup"><span data-stu-id="b7424-143">**Issue**</span></span> | <span data-ttu-id="b7424-144">无效的输入以及清除关键字的组合。</span><span class="sxs-lookup"><span data-stu-id="b7424-144">Invalid combination of inputs along with a CLEAR keyword.</span></span> |
| <span data-ttu-id="b7424-145">**常见原因**</span><span class="sxs-lookup"><span data-stu-id="b7424-145">**Common causes**</span></span> | <span data-ttu-id="b7424-146">清除不能使用其他输入组合。</span><span class="sxs-lookup"><span data-stu-id="b7424-146">CLEAR may not be combined with other inputs.</span></span> |
| <span data-ttu-id="b7424-147">**示例消息**</span><span class="sxs-lookup"><span data-stu-id="b7424-147">**Example message**</span></span> | <span data-ttu-id="b7424-148">*清除不能在与其他值一起使用*</span><span class="sxs-lookup"><span data-stu-id="b7424-148">*'CLEAR' cannot be used in conjunction with other values*</span></span> |

### <a name="nu1003"></a><span data-ttu-id="b7424-149">NU1003</span><span class="sxs-lookup"><span data-stu-id="b7424-149">NU1003</span></span>

| | |
| --- | --- |
| <span data-ttu-id="b7424-150">**问题**</span><span class="sxs-lookup"><span data-stu-id="b7424-150">**Issue**</span></span> | <span data-ttu-id="b7424-151">`PackageTargetFallback`和`AssetTargetFallback`用于选择资产提供不同的行为和不能一起使用。</span><span class="sxs-lookup"><span data-stu-id="b7424-151">`PackageTargetFallback` and `AssetTargetFallback` provide different behavior for selecting assets and cannot be used together.</span></span> |
| <span data-ttu-id="b7424-152">**常见原因**</span><span class="sxs-lookup"><span data-stu-id="b7424-152">**Common causes**</span></span> | <span data-ttu-id="b7424-153">同时`PackageTargetFallback`和`AssetTargetFallback`项目中存在。</span><span class="sxs-lookup"><span data-stu-id="b7424-153">Both `PackageTargetFallback` and `AssetTargetFallback` exist in the project.</span></span> |
| <span data-ttu-id="b7424-154">**示例消息**</span><span class="sxs-lookup"><span data-stu-id="b7424-154">**Example message**</span></span> | <span data-ttu-id="b7424-155">*PackageTargetFallback 和 AssetTargetFallback 不能一起使用。从项目环境删除 PackageTargetFallback(deprecated) 的引用。*</span><span class="sxs-lookup"><span data-stu-id="b7424-155">*PackageTargetFallback and AssetTargetFallback cannot be used together. Remove PackageTargetFallback(deprecated) references from the project environment.*</span></span> |

## <a name="missing-package-and-project-errors"></a><span data-ttu-id="b7424-156">缺少的包和项目错误</span><span class="sxs-lookup"><span data-stu-id="b7424-156">Missing package and project errors</span></span>

<span data-ttu-id="b7424-157">[NU1100](#nu1100) | [NU1101](#nu1101) | [NU1102](#nu1102) | [NU1103](#nu1103) | [NU1104](#nu1104)  |  [NU1105](#nu1105) | [NU1106](#nu1106)</span><span class="sxs-lookup"><span data-stu-id="b7424-157">[NU1100](#nu1100) | [NU1101](#nu1101) | [NU1102](#nu1102) | [NU1103](#nu1103) | [NU1104](#nu1104) | [NU1105](#nu1105) | [NU1106](#nu1106)</span></span>

### <a name="nu1100"></a><span data-ttu-id="b7424-158">NU1100</span><span class="sxs-lookup"><span data-stu-id="b7424-158">NU1100</span></span>

| | |
| --- | --- |
| <span data-ttu-id="b7424-159">**问题**</span><span class="sxs-lookup"><span data-stu-id="b7424-159">**Issue**</span></span> | <span data-ttu-id="b7424-160">依赖关系组不被解析。</span><span class="sxs-lookup"><span data-stu-id="b7424-160">A dependency group not be resolved.</span></span> <span data-ttu-id="b7424-161">这是一个泛型类型不是包或项目的问题。</span><span class="sxs-lookup"><span data-stu-id="b7424-161">This is a generic issue for types that are not packages or projects.</span></span> |
| <span data-ttu-id="b7424-162">**常见原因**</span><span class="sxs-lookup"><span data-stu-id="b7424-162">**Common causes**</span></span> | <span data-ttu-id="b7424-163">项目包含依赖于不存在的项。</span><span class="sxs-lookup"><span data-stu-id="b7424-163">The project contains a dependency on an item that doesn't exist.</span></span> |
| <span data-ttu-id="b7424-164">**示例消息**</span><span class="sxs-lookup"><span data-stu-id="b7424-164">**Example message**</span></span> | <span data-ttu-id="b7424-165">*无法解析 net45 System.Missing*</span><span class="sxs-lookup"><span data-stu-id="b7424-165">*Unable to resolve System.Missing for net45*</span></span> |

### <a name="nu1101"></a><span data-ttu-id="b7424-166">NU1101</span><span class="sxs-lookup"><span data-stu-id="b7424-166">NU1101</span></span>

| | |
| --- | --- |
| <span data-ttu-id="b7424-167">**问题**</span><span class="sxs-lookup"><span data-stu-id="b7424-167">**Issue**</span></span> | <span data-ttu-id="b7424-168">在任何源上找不到包。</span><span class="sxs-lookup"><span data-stu-id="b7424-168">The package cannot be found on any sources.</span></span> |
| <span data-ttu-id="b7424-169">**常见原因**</span><span class="sxs-lookup"><span data-stu-id="b7424-169">**Common causes**</span></span> | <span data-ttu-id="b7424-170">正确的包源缺失或不正确的包标识符。</span><span class="sxs-lookup"><span data-stu-id="b7424-170">The correct package source is missing or the package identifier is incorrect.</span></span> |
| <span data-ttu-id="b7424-171">**示例消息**</span><span class="sxs-lookup"><span data-stu-id="b7424-171">**Example message**</span></span> | <span data-ttu-id="b7424-172">*找不到程序包 System.Missing。具有此 id 在源中存在的任何包： dotnet 核心、 dotnet roslyn、 nuget.org*</span><span class="sxs-lookup"><span data-stu-id="b7424-172">*Unable to find package System.Missing. No packages exist with this id in source(s): dotnet-core, dotnet-roslyn, nuget.org*</span></span> |

### <a name="nu1102"></a><span data-ttu-id="b7424-173">NU1102</span><span class="sxs-lookup"><span data-stu-id="b7424-173">NU1102</span></span>

| | |
| --- | --- |
| <span data-ttu-id="b7424-174">**问题**</span><span class="sxs-lookup"><span data-stu-id="b7424-174">**Issue**</span></span> | <span data-ttu-id="b7424-175">找到的包标识符，但在任何源上找不到指定的依赖范围内的版本。</span><span class="sxs-lookup"><span data-stu-id="b7424-175">The package identifier is found but a version within the specified dependency range cannot be found on any of the sources.</span></span> |
| <span data-ttu-id="b7424-176">**常见原因**</span><span class="sxs-lookup"><span data-stu-id="b7424-176">**Common causes**</span></span> | <span data-ttu-id="b7424-177">正确的包源缺失或依赖项范围不正确。</span><span class="sxs-lookup"><span data-stu-id="b7424-177">The correct package source is missing or the dependency range is incorrect.</span></span> <span data-ttu-id="b7424-178">可能由包和不是用户指定的范围。</span><span class="sxs-lookup"><span data-stu-id="b7424-178">The range might be specified by a package and not the user.</span></span> <span data-ttu-id="b7424-179">用户可能需要切换到可用的版本，如果此包被直接引用该项目。</span><span class="sxs-lookup"><span data-stu-id="b7424-179">The user may need to switch to an available version if this package is referenced by the project directly.</span></span> |
| <span data-ttu-id="b7424-180">**示例消息**</span><span class="sxs-lookup"><span data-stu-id="b7424-180">**Example message**</span></span> | <span data-ttu-id="b7424-181">*找不到版本包 NuGet.Versioning (> = 9.0.1)<br/> -于 nuget.org 中的找到 30 版本 [最接近的版本： 4.0.0]<br/> -dotnet buildtools 中找到的 10 版本 [最接近的版本： 4.0.0-rc-2129]<br/> -找到 9在 NuGetVolatile 版本 [最接近的版本： 3.0.0-beta-00032]<br/> -0 版本位于 dotnet 核心<br/>-0 版本位于 dotnet roslyn*</span><span class="sxs-lookup"><span data-stu-id="b7424-181">*Unable to find package NuGet.Versioning with version (>= 9.0.1)<br/>  - Found 30 version(s) in nuget.org [ Nearest version: 4.0.0 ]<br/>  - Found 10 version(s) in dotnet-buildtools [ Nearest version: 4.0.0-rc-2129 ]<br/>  - Found 9 version(s) in NuGetVolatile [ Nearest version: 3.0.0-beta-00032 ]<br/>  - Found 0 version(s) in dotnet-core<br/>  - Found 0 version(s) in dotnet-roslyn*</span></span> |

### <a name="nu1103"></a><span data-ttu-id="b7424-182">NU1103</span><span class="sxs-lookup"><span data-stu-id="b7424-182">NU1103</span></span>

| | |
| --- | --- |
| <span data-ttu-id="b7424-183">**问题**</span><span class="sxs-lookup"><span data-stu-id="b7424-183">**Issue**</span></span> | <span data-ttu-id="b7424-184">依赖项范围中发现了不稳定的版本。</span><span class="sxs-lookup"><span data-stu-id="b7424-184">No stable versions were found in the dependency range.</span></span> <span data-ttu-id="b7424-185">预发行版本未找到，但不是允许。</span><span class="sxs-lookup"><span data-stu-id="b7424-185">Pre-release versions were found but are not allowed.</span></span> |
| <span data-ttu-id="b7424-186">**常见原因**</span><span class="sxs-lookup"><span data-stu-id="b7424-186">**Common causes**</span></span> | <span data-ttu-id="b7424-187">项目指定的依赖项范围是稳定的版本。</span><span class="sxs-lookup"><span data-stu-id="b7424-187">The project specified a stable version for the dependency range.</span></span> <span data-ttu-id="b7424-188">用户需要更改该版本范围以包括预发行版本。</span><span class="sxs-lookup"><span data-stu-id="b7424-188">Users need to change the version range to include pre-release versions.</span></span> |
| <span data-ttu-id="b7424-189">**示例消息**</span><span class="sxs-lookup"><span data-stu-id="b7424-189">**Example message**</span></span> | <span data-ttu-id="b7424-190">*找不到稳定的包 NuGet.Versioning 随版本 (> = 3.0.0)<br/> -dotnet buildtools 中找到的 10 版本 [最接近的版本： 4.0.0-rc-2129]<br/> -NuGetVolatile 中的找到 9 版本 [最接近的版本： 3.0.0-beta-00032]<br/> -0 版本位于 dotnet 核心<br/>-0 版本位于 dotnet roslyn*</span><span class="sxs-lookup"><span data-stu-id="b7424-190">*Unable to find a stable package NuGet.Versioning with version (>= 3.0.0)<br/>  - Found 10 version(s) in dotnet-buildtools [ Nearest version: 4.0.0-rc-2129 ]<br/>  - Found 9 version(s) in NuGetVolatile [ Nearest version: 3.0.0-beta-00032 ]<br/>  - Found 0 version(s) in dotnet-core<br/>  - Found 0 version(s) in dotnet-roslyn*</span></span> |

### <a name="nu1104"></a><span data-ttu-id="b7424-191">NU1104</span><span class="sxs-lookup"><span data-stu-id="b7424-191">NU1104</span></span>

| | |
| --- | --- |
| <span data-ttu-id="b7424-192">**问题**</span><span class="sxs-lookup"><span data-stu-id="b7424-192">**Issue**</span></span> | <span data-ttu-id="b7424-193">ProjectReference 指向不存在的文件。</span><span class="sxs-lookup"><span data-stu-id="b7424-193">A ProjectReference points to a file that doesn't exist.</span></span> |
| <span data-ttu-id="b7424-194">**常见原因**</span><span class="sxs-lookup"><span data-stu-id="b7424-194">**Common causes**</span></span> | <span data-ttu-id="b7424-195">项目文件缺少从磁盘或引用不正确。</span><span class="sxs-lookup"><span data-stu-id="b7424-195">The project file is missing from disk or the reference is incorrect.</span></span> |
| <span data-ttu-id="b7424-196">**示例消息**</span><span class="sxs-lookup"><span data-stu-id="b7424-196">**Example message**</span></span> | <span data-ttu-id="b7424-197">*项目引用不存在 c:\a.csproj。检查项目引用有效以及项目文件是否存在。*</span><span class="sxs-lookup"><span data-stu-id="b7424-197">*Project reference does not exist 'c:\a.csproj'. Check that the project reference is valid and that the project file exists.*</span></span> |

### <a name="nu1105"></a><span data-ttu-id="b7424-198">NU1105</span><span class="sxs-lookup"><span data-stu-id="b7424-198">NU1105</span></span>

| | |
| --- | --- |
| <span data-ttu-id="b7424-199">**问题**</span><span class="sxs-lookup"><span data-stu-id="b7424-199">**Issue**</span></span> | <span data-ttu-id="b7424-200">项目文件存在，但不还原信息已为其提供。</span><span class="sxs-lookup"><span data-stu-id="b7424-200">The project file exists but no restore information was provided for it.</span></span> |
| <span data-ttu-id="b7424-201">**常见原因**</span><span class="sxs-lookup"><span data-stu-id="b7424-201">**Common causes**</span></span> | <span data-ttu-id="b7424-202">在 Visual Studio 中，这可能意味着该项目已卸载。</span><span class="sxs-lookup"><span data-stu-id="b7424-202">In Visual Studio this could mean that the project is unloaded.</span></span> <span data-ttu-id="b7424-203">从命令行中，这可能表示该文件已损坏或后进行恢复从中读取项目所需的导入目标不包含自定义。</span><span class="sxs-lookup"><span data-stu-id="b7424-203">From the command line this could mean that the file is corrupt or that it doesn't contain the custom after imports target needed for restore to read the project.</span></span> |
| <span data-ttu-id="b7424-204">**示例消息**</span><span class="sxs-lookup"><span data-stu-id="b7424-204">**Example message**</span></span> | <span data-ttu-id="b7424-205">*无法读取 c:\a.csproj 的项目信息。项目文件可能无效或缺少所需的还原的目标。*</span><span class="sxs-lookup"><span data-stu-id="b7424-205">*Unable to read project information for 'c:\a.csproj'. The project file may be invalid or missing targets required for restore.*</span></span> |

### <a name="nu1106"></a><span data-ttu-id="b7424-206">NU1106</span><span class="sxs-lookup"><span data-stu-id="b7424-206">NU1106</span></span>

| | |
| --- | --- |
| <span data-ttu-id="b7424-207">**问题**</span><span class="sxs-lookup"><span data-stu-id="b7424-207">**Issue**</span></span> | <span data-ttu-id="b7424-208">无法解析依赖项约束。</span><span class="sxs-lookup"><span data-stu-id="b7424-208">Dependency constraints cannot be resolved.</span></span> |
| <span data-ttu-id="b7424-209">**常见原因**</span><span class="sxs-lookup"><span data-stu-id="b7424-209">**Common causes**</span></span> | <span data-ttu-id="b7424-210">包包含的包而不是开放式的范围的确切版本上的依赖项。</span><span class="sxs-lookup"><span data-stu-id="b7424-210">Packages contain dependency on exact versions of a package instead of open-ended ranges.</span></span> |
| <span data-ttu-id="b7424-211">**示例消息**</span><span class="sxs-lookup"><span data-stu-id="b7424-211">**Example message**</span></span> | <span data-ttu-id="b7424-212">*无法满足 {id} 互相冲突的请求: {冲突路径} Framework: {目标关系图}*</span><span class="sxs-lookup"><span data-stu-id="b7424-212">*Unable to satisfy conflicting requests for {id}: {conflict path} Framework: {target graph}*</span></span> |

<span data-ttu-id="b7424-213">< a name ="NU1107 ></a></span><span class="sxs-lookup"><span data-stu-id="b7424-213"><a name="NU1107></a></span></span>

### <a name="nu1107-previously-nu1607"></a><span data-ttu-id="b7424-214">NU1107 (以前 NU1607)</span><span class="sxs-lookup"><span data-stu-id="b7424-214">NU1107 (Previously NU1607)</span></span>

| | |
| --- | --- |
| <span data-ttu-id="b7424-215">**问题**</span><span class="sxs-lookup"><span data-stu-id="b7424-215">**Issue**</span></span> | <span data-ttu-id="b7424-216">无法解析包之间的依赖关系约束。</span><span class="sxs-lookup"><span data-stu-id="b7424-216">Unable to resolve dependency constraints between packages.</span></span> |
| <span data-ttu-id="b7424-217">**常见原因**</span><span class="sxs-lookup"><span data-stu-id="b7424-217">**Common causes**</span></span> | <span data-ttu-id="b7424-218">依赖项与上的约束的确切版本的包不允许其他包以根据需要增大版本号。</span><span class="sxs-lookup"><span data-stu-id="b7424-218">Packages with dependency constraints on exact versions do not allow other packages to increase the version if needed.</span></span> |
| <span data-ttu-id="b7424-219">**示例消息**</span><span class="sxs-lookup"><span data-stu-id="b7424-219">**Example message**</span></span> | <span data-ttu-id="b7424-220">*NuGet.Versioning 检测到的版本冲突。若要解决此问题的项目中直接引用包。<br/>NuGet.Packaging 3.5.0-> （= 3.5.0） NuGet.Versioning<br/> NuGet.Configuration 4.0.0-> 的 NuGet.Versioning （= 4.0.0）*</span><span class="sxs-lookup"><span data-stu-id="b7424-220">*Version conflict detected for NuGet.Versioning. Reference the package directly from the project to resolve this issue.<br/>  NuGet.Packaging 3.5.0 -> NuGet.Versioning (= 3.5.0)<br/>  NuGet.Configuration 4.0.0 -> NuGet.Versioning (= 4.0.0)*</span></span> |

<span data-ttu-id="b7424-221">< a name ="NU1108 ></a></span><span class="sxs-lookup"><span data-stu-id="b7424-221"><a name="NU1108></a></span></span>

### <a name="nu1108-previously-nu1606"></a><span data-ttu-id="b7424-222">NU1108 (以前 NU1606)</span><span class="sxs-lookup"><span data-stu-id="b7424-222">NU1108 (Previously NU1606)</span></span>

| | |
| --- | --- |
| <span data-ttu-id="b7424-223">**问题**</span><span class="sxs-lookup"><span data-stu-id="b7424-223">**Issue**</span></span> | <span data-ttu-id="b7424-224">检测到循环依赖关系。</span><span class="sxs-lookup"><span data-stu-id="b7424-224">A circular dependency was detected.</span></span> |
| <span data-ttu-id="b7424-225">**常见原因**</span><span class="sxs-lookup"><span data-stu-id="b7424-225">**Common causes**</span></span> | <span data-ttu-id="b7424-226">未正确编写了包。</span><span class="sxs-lookup"><span data-stu-id="b7424-226">A package is authored incorrectly.</span></span> |
| <span data-ttu-id="b7424-227">**示例消息**</span><span class="sxs-lookup"><span data-stu-id="b7424-227">**Example message**</span></span> | <span data-ttu-id="b7424-228">*检测到循环： A-> B-> A*</span><span class="sxs-lookup"><span data-stu-id="b7424-228">*Cycle detected: A -> B -> A*</span></span> |

## <a name="compatibility-errors"></a><span data-ttu-id="b7424-229">兼容性错误</span><span class="sxs-lookup"><span data-stu-id="b7424-229">Compatibility errors</span></span>

<span data-ttu-id="b7424-230">[NU1201](#nu1201) | [NU1202](#nu1202) | [NU1203](#nu1203) | [NU1401](#nu1401)</span><span class="sxs-lookup"><span data-stu-id="b7424-230">[NU1201](#nu1201) | [NU1202](#nu1202) | [NU1203](#nu1203) | [NU1401](#nu1401)</span></span>

### <a name="nu1201"></a><span data-ttu-id="b7424-231">NU1201</span><span class="sxs-lookup"><span data-stu-id="b7424-231">NU1201</span></span>

| | |
| --- | --- |
| <span data-ttu-id="b7424-232">**问题**</span><span class="sxs-lookup"><span data-stu-id="b7424-232">**Issue**</span></span> | <span data-ttu-id="b7424-233">依赖项项目不包含与当前项目兼容的框架。</span><span class="sxs-lookup"><span data-stu-id="b7424-233">A dependency project doesn't contain a framework compatible with the current project.</span></span> |
| <span data-ttu-id="b7424-234">**常见原因**</span><span class="sxs-lookup"><span data-stu-id="b7424-234">**Common causes**</span></span> | <span data-ttu-id="b7424-235">项目的目标框架是比使用项目的更高版本。</span><span class="sxs-lookup"><span data-stu-id="b7424-235">The project's target framework is a higher version than the consuming project.</span></span> |
| <span data-ttu-id="b7424-236">**示例消息**</span><span class="sxs-lookup"><span data-stu-id="b7424-236">**Example message**</span></span> | <span data-ttu-id="b7424-237">*项目 ServerWeb 与不兼容 netstandard1.3 (。NETStandard，Version = v1.3)。项目 ServerWeb 支持：<br/> -netstandard1.6 (。NETStandard，Version = v1.6)<br/> -netcoreapp1.0 (。NETCoreApp，Version = v1.0)*</span><span class="sxs-lookup"><span data-stu-id="b7424-237">*Project ServerWeb is not compatible with netstandard1.3 (.NETStandard,Version=v1.3). Project ServerWeb supports:<br/>  - netstandard1.6 (.NETStandard,Version=v1.6)<br/>  - netcoreapp1.0 (.NETCoreApp,Version=v1.0)*</span></span> |

### <a name="nu1202"></a><span data-ttu-id="b7424-238">NU1202</span><span class="sxs-lookup"><span data-stu-id="b7424-238">NU1202</span></span>

| | |
| --- | --- |
| <span data-ttu-id="b7424-239">**问题**</span><span class="sxs-lookup"><span data-stu-id="b7424-239">**Issue**</span></span> | <span data-ttu-id="b7424-240">依赖项包不包含任何与项目兼容的资产。</span><span class="sxs-lookup"><span data-stu-id="b7424-240">A dependency package doesn't contain any assets compatible with the project.</span></span> |
| <span data-ttu-id="b7424-241">**常见原因**</span><span class="sxs-lookup"><span data-stu-id="b7424-241">**Common causes**</span></span> | <span data-ttu-id="b7424-242">包不支持项目的目标框架。</span><span class="sxs-lookup"><span data-stu-id="b7424-242">The package doesn't support the project's target framework.</span></span> |
| <span data-ttu-id="b7424-243">**示例消息**</span><span class="sxs-lookup"><span data-stu-id="b7424-243">**Example message**</span></span> | <span data-ttu-id="b7424-244">*包 System.ComponentModel.EventBasedAsync 4.0.11 与不兼容 netstandard1.3 (。NETStandard，Version = v1.3)。打包 System.ComponentModel.EventBasedAsync 4.0.11 支持：<br/> -monoandroid10 (MonoAndroid，Version = v1.0)<br/> -monotouch10 (MonoTouch，Version = v1.0)<br/> -net45 (。NETFramework，Version = v4.5)<br/> -netcore50 (。NETCore，Version = 5.0 版)<br/> -netstandard1.0 (。NETStandard，Version = v1.0)<br/> -可移植 net45 + win8 + wp8 + wpa81 (。NETPortable，Version = v0.0，配置文件 = Profile259)<br/> -win8 (Windows、 版本 = v8.0)<br/> -wp8 (WindowsPhone，Version = v8.0)<br/> -wpa81 (WindowsPhoneApp，Version = v8.1)<br/> -xamarinios10 (Xamarin.iOS,Version=v1.0)<br/> -xamarinmac20 (Xamarin.Mac,Version=v2.0)<br/> -xamarintvos10 (Xamarin.TVOS,Version=v1.0)<br/> -xamarinwatchos10 (Xamarin.WatchOS,Version=v1.0)*</span><span class="sxs-lookup"><span data-stu-id="b7424-244">*Package System.ComponentModel.EventBasedAsync 4.0.11 is not compatible with netstandard1.3 (.NETStandard,Version=v1.3). Package System.ComponentModel.EventBasedAsync 4.0.11 supports:<br/>  - monoandroid10 (MonoAndroid,Version=v1.0)<br/>  - monotouch10 (MonoTouch,Version=v1.0)<br/>  - net45 (.NETFramework,Version=v4.5)<br/>  - netcore50 (.NETCore,Version=v5.0)<br/>  - netstandard1.0 (.NETStandard,Version=v1.0)<br/>  - portable-net45+win8+wp8+wpa81 (.NETPortable,Version=v0.0,Profile=Profile259)<br/>  - win8 (Windows,Version=v8.0)<br/>  - wp8 (WindowsPhone,Version=v8.0)<br/>  - wpa81 (WindowsPhoneApp,Version=v8.1)<br/>  - xamarinios10 (Xamarin.iOS,Version=v1.0)<br/>  - xamarinmac20 (Xamarin.Mac,Version=v2.0)<br/>  - xamarintvos10 (Xamarin.TVOS,Version=v1.0)<br/>  - xamarinwatchos10 (Xamarin.WatchOS,Version=v1.0)*</span></span>|

### <a name="nu1203"></a><span data-ttu-id="b7424-245">NU1203</span><span class="sxs-lookup"><span data-stu-id="b7424-245">NU1203</span></span>

| | |
| --- | --- |
| <span data-ttu-id="b7424-246">**问题**</span><span class="sxs-lookup"><span data-stu-id="b7424-246">**Issue**</span></span> | <span data-ttu-id="b7424-247">包不支持项目的`RuntimeIdentifier`。</span><span class="sxs-lookup"><span data-stu-id="b7424-247">The package doesn't support the project's `RuntimeIdentifier`.</span></span> |
| <span data-ttu-id="b7424-248">**常见原因**</span><span class="sxs-lookup"><span data-stu-id="b7424-248">**Common causes**</span></span> | <span data-ttu-id="b7424-249">包不支持当前`RuntimeIdentifier`。</span><span class="sxs-lookup"><span data-stu-id="b7424-249">The package doesn't support the current `RuntimeIdentifier`.</span></span> <span data-ttu-id="b7424-250">更改`RuntimeIdentifier`如果需要在项目中使用的值。</span><span class="sxs-lookup"><span data-stu-id="b7424-250">Change the `RuntimeIdentifier` values used in the project if needed.</span></span> |
| <span data-ttu-id="b7424-251">**示例消息**</span><span class="sxs-lookup"><span data-stu-id="b7424-251">**Example message**</span></span> | <span data-ttu-id="b7424-252">*System.Example 1.0.0 提供 a.dll 的编译时引用程序集上 net461，但没有兼容的运行时程序集。*</span><span class="sxs-lookup"><span data-stu-id="b7424-252">*System.Example 1.0.0 provides a compile-time reference assembly for a.dll on net461, but there is no compatible run-time assembly.*</span></span> |

### <a name="nu1401"></a><span data-ttu-id="b7424-253">NU1401</span><span class="sxs-lookup"><span data-stu-id="b7424-253">NU1401</span></span>

| | |
| --- | --- |
| <span data-ttu-id="b7424-254">**问题**</span><span class="sxs-lookup"><span data-stu-id="b7424-254">**Issue**</span></span> | <span data-ttu-id="b7424-255">包需要功能或框架当前不支持安装的 NuGet 版本。</span><span class="sxs-lookup"><span data-stu-id="b7424-255">The package requires features or frameworks not currently supported by the installed version of NuGet.</span></span> |
| <span data-ttu-id="b7424-256">**常见原因**</span><span class="sxs-lookup"><span data-stu-id="b7424-256">**Common causes**</span></span> | <span data-ttu-id="b7424-257">升级 NuGet，以解决此问题。</span><span class="sxs-lookup"><span data-stu-id="b7424-257">Upgrade NuGet to fix the issue.</span></span> |
| <span data-ttu-id="b7424-258">**示例消息**</span><span class="sxs-lookup"><span data-stu-id="b7424-258">**Example message**</span></span> | <span data-ttu-id="b7424-259">*NuGet.Versioning 程序包需要 NuGet 客户端版本"5.0.0"或更高版本，但是当前 NuGet 版本为"4.3.0"。若要升级 NuGet，请转到 http://docs.nuget.org/consume/installing-nuget。*</span><span class="sxs-lookup"><span data-stu-id="b7424-259">*The 'NuGet.Versioning' package requires NuGet client version '5.0.0' or above, but the current NuGet version is '4.3.0'. To upgrade NuGet, please go to http://docs.nuget.org/consume/installing-nuget.*</span></span> |

## <a name="invalid-input-warnings"></a><span data-ttu-id="b7424-260">无效的输入的警告</span><span class="sxs-lookup"><span data-stu-id="b7424-260">Invalid input warnings</span></span>

<span data-ttu-id="b7424-261">[NU1501](#nu1501) | [NU1502](#nu1502) | [NU1503](#nu1503)</span><span class="sxs-lookup"><span data-stu-id="b7424-261">[NU1501](#nu1501) | [NU1502](#nu1502) | [NU1503](#nu1503)</span></span>

### <a name="nu1501"></a><span data-ttu-id="b7424-262">NU1501</span><span class="sxs-lookup"><span data-stu-id="b7424-262">NU1501</span></span>

| | |
| --- | --- |
| <span data-ttu-id="b7424-263">**问题**</span><span class="sxs-lookup"><span data-stu-id="b7424-263">**Issue**</span></span> | <span data-ttu-id="b7424-264">项目还原尝试运行在未找到。</span><span class="sxs-lookup"><span data-stu-id="b7424-264">The project restore is attempting to operate on was not found.</span></span> |
| <span data-ttu-id="b7424-265">**常见原因**</span><span class="sxs-lookup"><span data-stu-id="b7424-265">**Common causes**</span></span> | <span data-ttu-id="b7424-266">找不到该项目。</span><span class="sxs-lookup"><span data-stu-id="b7424-266">The project is missing.</span></span> |
| <span data-ttu-id="b7424-267">**示例消息**</span><span class="sxs-lookup"><span data-stu-id="b7424-267">**Example message**</span></span> | <span data-ttu-id="b7424-268">*文件夹 c:\projects\a 不包含要还原的项目。*</span><span class="sxs-lookup"><span data-stu-id="b7424-268">*The folder 'c:\projects\a' does not contain a project to restore.*</span></span> |

### <a name="nu1502"></a><span data-ttu-id="b7424-269">NU1502</span><span class="sxs-lookup"><span data-stu-id="b7424-269">NU1502</span></span>

| | |
| --- | --- |
| <span data-ttu-id="b7424-270">**问题**</span><span class="sxs-lookup"><span data-stu-id="b7424-270">**Issue**</span></span> | <span data-ttu-id="b7424-271">`RuntimeSupports`包含无效的配置文件。</span><span class="sxs-lookup"><span data-stu-id="b7424-271">`RuntimeSupports` contains an invalid profile.</span></span> |
| <span data-ttu-id="b7424-272">**常见原因**</span><span class="sxs-lookup"><span data-stu-id="b7424-272">**Common causes**</span></span> | <span data-ttu-id="b7424-273">中找不到支持的配置文件`runtime.json`从当前的依赖项包文件。</span><span class="sxs-lookup"><span data-stu-id="b7424-273">The supports profile was not found in a `runtime.json` file from the current dependency packages.</span></span> |
| <span data-ttu-id="b7424-274">**示例消息**</span><span class="sxs-lookup"><span data-stu-id="b7424-274">**Example message**</span></span> | <span data-ttu-id="b7424-275">*未知的兼容性配置文件： aaa*</span><span class="sxs-lookup"><span data-stu-id="b7424-275">*Unknown Compatibility Profile: aaa*</span></span> |

### <a name="nu1503"></a><span data-ttu-id="b7424-276">NU1503</span><span class="sxs-lookup"><span data-stu-id="b7424-276">NU1503</span></span>

| | |
| --- | --- |
| <span data-ttu-id="b7424-277">**问题**</span><span class="sxs-lookup"><span data-stu-id="b7424-277">**Issue**</span></span> | <span data-ttu-id="b7424-278">依赖项项目不能导入 NuGet 的恢复目标。</span><span class="sxs-lookup"><span data-stu-id="b7424-278">A dependency project doesn't import NuGet's restore targets.</span></span> <span data-ttu-id="b7424-279">这是类似于 NU1105 但此处项目，将跳过并忽略而不是导致所有还原失败。</span><span class="sxs-lookup"><span data-stu-id="b7424-279">This is similar to NU1105 but here the project is skipped and ignored instead of causing all of restore to fail.</span></span> <span data-ttu-id="b7424-280">在复杂的解决方案通常有其他类型的可能不支持还原的项目中。</span><span class="sxs-lookup"><span data-stu-id="b7424-280">In complex solutions there are often other types of projects that may not support restore.</span></span> |
| <span data-ttu-id="b7424-281">**常见原因**</span><span class="sxs-lookup"><span data-stu-id="b7424-281">**Common causes**</span></span> | <span data-ttu-id="b7424-282">这可能会导致不导入公共属性/目标的自动导入还原的项目。</span><span class="sxs-lookup"><span data-stu-id="b7424-282">This can happen for projects that do not import common props/targets which automatically import restore.</span></span> <span data-ttu-id="b7424-283">如果项目不需要还原这可予以忽视。</span><span class="sxs-lookup"><span data-stu-id="b7424-283">If the project doesn't need to be restored this can be ignored.</span></span> |
| <span data-ttu-id="b7424-284">**示例消息**</span><span class="sxs-lookup"><span data-stu-id="b7424-284">**Example message**</span></span> | <span data-ttu-id="b7424-285">*正在跳过还原项目 c:\a.csproj。项目文件可能无效或缺少所需的还原的目标。*</span><span class="sxs-lookup"><span data-stu-id="b7424-285">*Skipping restore for project 'c:\a.csproj'. The project file may be invalid or missing targets required for restore.*</span></span> |

## <a name="unexpected-package-version-warnings"></a><span data-ttu-id="b7424-286">意外的包版本警告</span><span class="sxs-lookup"><span data-stu-id="b7424-286">Unexpected package version warnings</span></span>

<span data-ttu-id="b7424-287">[NU1601](#nu1601) | [NU1602](#nu1602) | [NU1603](#nu1603) | [NU1604](#nu1604) | [NU1605](#nu1605)</span><span class="sxs-lookup"><span data-stu-id="b7424-287">[NU1601](#nu1601) | [NU1602](#nu1602) | [NU1603](#nu1603) | [NU1604](#nu1604) | [NU1605](#nu1605)</span></span>

### <a name="nu1601"></a><span data-ttu-id="b7424-288">NU1601</span><span class="sxs-lookup"><span data-stu-id="b7424-288">NU1601</span></span>

| | |
| --- | --- |
| <span data-ttu-id="b7424-289">**问题**</span><span class="sxs-lookup"><span data-stu-id="b7424-289">**Issue**</span></span> | <span data-ttu-id="b7424-290">直接项目依赖项已解除了一个为更高版本比指定的项目。</span><span class="sxs-lookup"><span data-stu-id="b7424-290">A direct project dependency was bumped to a higher version than the project specified.</span></span> |
| <span data-ttu-id="b7424-291">**常见原因**</span><span class="sxs-lookup"><span data-stu-id="b7424-291">**Common causes**</span></span> | <span data-ttu-id="b7424-292">另一个依赖项包需要更高版本，并增加包。</span><span class="sxs-lookup"><span data-stu-id="b7424-292">Another dependency package required a higher version and bumped the package up.</span></span> |
| <span data-ttu-id="b7424-293">**示例消息**</span><span class="sxs-lookup"><span data-stu-id="b7424-293">**Example message**</span></span> | <span data-ttu-id="b7424-294">*指定的依赖项已 NuGet.Versioning (> = 3.5.0) 但最终的 NuGet.Versioning 4.0.0。*</span><span class="sxs-lookup"><span data-stu-id="b7424-294">*Dependency specified was NuGet.Versioning (>= 3.5.0) but ended up with NuGet.Versioning 4.0.0.*</span></span> |

### <a name="nu1602"></a><span data-ttu-id="b7424-295">NU1602</span><span class="sxs-lookup"><span data-stu-id="b7424-295">NU1602</span></span>

| | |
| --- | --- |
| <span data-ttu-id="b7424-296">**问题**</span><span class="sxs-lookup"><span data-stu-id="b7424-296">**Issue**</span></span> | <span data-ttu-id="b7424-297">包依赖项缺少零下限。</span><span class="sxs-lookup"><span data-stu-id="b7424-297">A package dependency is missing a lower bound.</span></span> <span data-ttu-id="b7424-298">这不允许还原，以便查找*最佳匹配*。</span><span class="sxs-lookup"><span data-stu-id="b7424-298">This doesn't allow restore to find the *best match*.</span></span> <span data-ttu-id="b7424-299">每个还原将浮动向下尝试查找可以使用较低版本。</span><span class="sxs-lookup"><span data-stu-id="b7424-299">Each restore will float downwards trying to find a lower version that can be used.</span></span> <span data-ttu-id="b7424-300">这意味着此恢复将进入联机状态，以检查每个时间而不是在用户程序包文件夹中使用已存在的包的所有源。</span><span class="sxs-lookup"><span data-stu-id="b7424-300">This means that restore goes online to check all sources each time instead of using the packages that already exist in the user package folder.</span></span> |
| <span data-ttu-id="b7424-301">**常见原因**</span><span class="sxs-lookup"><span data-stu-id="b7424-301">**Common causes**</span></span> | <span data-ttu-id="b7424-302">这通常是创作错误的包。</span><span class="sxs-lookup"><span data-stu-id="b7424-302">This is usually a package authoring error.</span></span> |
| <span data-ttu-id="b7424-303">**示例消息**</span><span class="sxs-lookup"><span data-stu-id="b7424-303">**Example message**</span></span> | <span data-ttu-id="b7424-304">*NuGet.Packaging 4.0.0 不依赖项 NuGet.Versioning (> 3.5.0) 提供包含下限。3.6.0 的近似最佳匹配已解决。*</span><span class="sxs-lookup"><span data-stu-id="b7424-304">*NuGet.Packaging 4.0.0 does not provide an inclusive lower bound for dependency NuGet.Versioning (> 3.5.0). An approximate best match of 3.6.0 was resolved.*</span></span> |

### <a name="nu1603"></a><span data-ttu-id="b7424-305">NU1603</span><span class="sxs-lookup"><span data-stu-id="b7424-305">NU1603</span></span>

| | |
| --- | --- |
| <span data-ttu-id="b7424-306">**问题**</span><span class="sxs-lookup"><span data-stu-id="b7424-306">**Issue**</span></span> | <span data-ttu-id="b7424-307">包依赖项指定未找到的版本。</span><span class="sxs-lookup"><span data-stu-id="b7424-307">A package dependency specified a version that could not be found.</span></span> <span data-ttu-id="b7424-308">与它不同的包编写针对相反，使用更高版本。</span><span class="sxs-lookup"><span data-stu-id="b7424-308">A higher version was used instead, which differs from what the package was authored against.</span></span><br/><br/><span data-ttu-id="b7424-309">这意味着找不到该还原*最佳匹配*。</span><span class="sxs-lookup"><span data-stu-id="b7424-309">This means that restore did not find the *best match*.</span></span> <span data-ttu-id="b7424-310">每个还原将浮动向下尝试查找可以使用较低版本。</span><span class="sxs-lookup"><span data-stu-id="b7424-310">Each restore will float downwards trying to find a lower version that can be used.</span></span> <span data-ttu-id="b7424-311">这意味着此恢复将进入联机状态，以检查每个时间而不是在用户程序包文件夹中使用已存在的包的所有源。</span><span class="sxs-lookup"><span data-stu-id="b7424-311">This means that restore goes online to check all sources each time instead of using the packages that already exist in the user package folder.</span></span> |
| <span data-ttu-id="b7424-312">**常见原因**</span><span class="sxs-lookup"><span data-stu-id="b7424-312">**Common causes**</span></span> | <span data-ttu-id="b7424-313">包源不包含预期的下限版本。</span><span class="sxs-lookup"><span data-stu-id="b7424-313">The package sources do not contain the expected lower bound version.</span></span> <span data-ttu-id="b7424-314">如果尚未释放预期包，这可能是包创作错误。</span><span class="sxs-lookup"><span data-stu-id="b7424-314">If the package expected has not been released then this may be a package authoring error.</span></span> |
| <span data-ttu-id="b7424-315">**示例消息**</span><span class="sxs-lookup"><span data-stu-id="b7424-315">**Example message**</span></span> | <span data-ttu-id="b7424-316">NuGet.Packaging 4.0.0 取决于 NuGet.Versioning (> = 4.0.0) 但找不到 4.0.0。</span><span class="sxs-lookup"><span data-stu-id="b7424-316">NuGet.Packaging 4.0.0 depends on NuGet.Versioning (>= 4.0.0) but 4.0.0 was not found.</span></span> <span data-ttu-id="b7424-317">5.0.0 的近似最佳匹配已解决。</span><span class="sxs-lookup"><span data-stu-id="b7424-317">An approximate best match of 5.0.0 was resolved.</span></span> |

### <a name="nu1604"></a><span data-ttu-id="b7424-318">NU1604</span><span class="sxs-lookup"><span data-stu-id="b7424-318">NU1604</span></span>

| | |
| --- | --- |
| <span data-ttu-id="b7424-319">**问题**</span><span class="sxs-lookup"><span data-stu-id="b7424-319">**Issue**</span></span> | <span data-ttu-id="b7424-320">项目依赖项未定义零下限。</span><span class="sxs-lookup"><span data-stu-id="b7424-320">A project dependency doesn't define a lower bound.</span></span><br/><br/><span data-ttu-id="b7424-321">这意味着找不到该还原*最佳匹配*。</span><span class="sxs-lookup"><span data-stu-id="b7424-321">This means that restore did not find the *best match*.</span></span> <span data-ttu-id="b7424-322">每个还原将浮动向下尝试查找可以使用较低版本。</span><span class="sxs-lookup"><span data-stu-id="b7424-322">Each restore will float downwards trying to find a lower version that can be used.</span></span> <span data-ttu-id="b7424-323">这意味着此恢复将进入联机状态，以检查每个时间而不是在用户程序包文件夹中使用已存在的包的所有源。</span><span class="sxs-lookup"><span data-stu-id="b7424-323">This means that restore goes online to check all sources each time instead of using the packages that already exist in the user package folder.</span></span> |
| <span data-ttu-id="b7424-324">**常见原因**</span><span class="sxs-lookup"><span data-stu-id="b7424-324">**Common causes**</span></span> | <span data-ttu-id="b7424-325">项目的*PackageReference* *版本*应更新属性以包括零下限。</span><span class="sxs-lookup"><span data-stu-id="b7424-325">The project's *PackageReference* *Version* attribute should be updated to include a lower bound.</span></span> |
| <span data-ttu-id="b7424-326">**示例消息**</span><span class="sxs-lookup"><span data-stu-id="b7424-326">**Example message**</span></span> | <span data-ttu-id="b7424-327">*项目依赖项 NuGet.Versioning (< = 9.0.0) doe 不包含包含下限。依赖项版本以确保一致还原结果中包括零下限。*</span><span class="sxs-lookup"><span data-stu-id="b7424-327">*Project dependency NuGet.Versioning (<= 9.0.0) doe not contain an inclusive lower bound. Include a lower bound in the dependency version to ensure consistent restore results.*</span></span> |

### <a name="nu1605"></a><span data-ttu-id="b7424-328">NU1605</span><span class="sxs-lookup"><span data-stu-id="b7424-328">NU1605</span></span>

| | |
| --- | --- |
| <span data-ttu-id="b7424-329">**问题**</span><span class="sxs-lookup"><span data-stu-id="b7424-329">**Issue**</span></span> | <span data-ttu-id="b7424-330">依赖项包指定比还原最终解决更高版本的包的版本约束。</span><span class="sxs-lookup"><span data-stu-id="b7424-330">A dependency package specified a version constraint on a higher version of a package than restore ultimately resolved.</span></span> |
| <span data-ttu-id="b7424-331">**常见原因**</span><span class="sxs-lookup"><span data-stu-id="b7424-331">**Common causes**</span></span> | <span data-ttu-id="b7424-332">接近 wins 解析包时。</span><span class="sxs-lookup"><span data-stu-id="b7424-332">Nearest wins when resolving packages.</span></span> <span data-ttu-id="b7424-333">在图中的最近包可能已重写相距包。</span><span class="sxs-lookup"><span data-stu-id="b7424-333">A nearer package in the graph may have overridden a distant package.</span></span> |
| <span data-ttu-id="b7424-334">**示例消息**</span><span class="sxs-lookup"><span data-stu-id="b7424-334">**Example message**</span></span> | <span data-ttu-id="b7424-335">*检测到包降级： NuGet.Versioning 从 4.0.0 到 3.5.0。要选择的不同版本的项目中直接引用包。<br/>NuGet.Packaging 3.5.0-> NuGet.Versioning 3.5.0<br/> NuGet.Commands 4.0.0-> NuGet.Configuration 4.0.0-> NuGet.Versioning 4.0.0*</span><span class="sxs-lookup"><span data-stu-id="b7424-335">*Detected package downgrade: NuGet.Versioning from 4.0.0 to 3.5.0. Reference the package directly from the project to select a different version.<br/>  NuGet.Packaging 3.5.0 -> NuGet.Versioning 3.5.0<br/>  NuGet.Commands 4.0.0 -> NuGet.Configuration 4.0.0 -> NuGet.Versioning 4.0.0*</span></span> |

## <a name="resolver-conflict-warnings"></a><span data-ttu-id="b7424-336">冲突解决程序冲突警告</span><span class="sxs-lookup"><span data-stu-id="b7424-336">Resolver conflict warnings</span></span>

[<span data-ttu-id="b7424-337">NU1608</span><span class="sxs-lookup"><span data-stu-id="b7424-337">NU1608</span></span>](#nu1608)

### <a name="nu1608"></a><span data-ttu-id="b7424-338">NU1608</span><span class="sxs-lookup"><span data-stu-id="b7424-338">NU1608</span></span>

| | |
| --- | --- |
| <span data-ttu-id="b7424-339">**问题**</span><span class="sxs-lookup"><span data-stu-id="b7424-339">**Issue**</span></span> | <span data-ttu-id="b7424-340">解决包是不是依赖项约束允许，更高版本。</span><span class="sxs-lookup"><span data-stu-id="b7424-340">A resolve package is higher than a dependency constraint allows.</span></span> <span data-ttu-id="b7424-341">在某些情况下，这是有意，可以禁止显示警告。</span><span class="sxs-lookup"><span data-stu-id="b7424-341">In some cases this is intentional and the warning can be suppressed.</span></span> |
| <span data-ttu-id="b7424-342">**常见原因**</span><span class="sxs-lookup"><span data-stu-id="b7424-342">**Common causes**</span></span> | <span data-ttu-id="b7424-343">一个项目直接引用的包将覆盖其他包中的依赖关系约束。</span><span class="sxs-lookup"><span data-stu-id="b7424-343">A package referenced directly by a project will override dependency constraints from other packages.</span></span>   |
| <span data-ttu-id="b7424-344">**示例消息**</span><span class="sxs-lookup"><span data-stu-id="b7424-344">**Example message**</span></span> | <span data-ttu-id="b7424-345">*外部依赖关系约束的检测到的包版本： x 1.0.0 要求的 y （= 1.0.0），但版本 y 2.0.0 为已解决。*</span><span class="sxs-lookup"><span data-stu-id="b7424-345">*Detected package version outside of dependency constraint: x 1.0.0 requires y (= 1.0.0) but version y 2.0.0 was resolved.*</span></span> |

## <a name="package-fallback-warnings"></a><span data-ttu-id="b7424-346">包回退警告</span><span class="sxs-lookup"><span data-stu-id="b7424-346">Package fallback warnings</span></span>

[<span data-ttu-id="b7424-347">NU1701</span><span class="sxs-lookup"><span data-stu-id="b7424-347">NU1701</span></span>](#nu1701)

### <a name="nu1701"></a><span data-ttu-id="b7424-348">NU1701</span><span class="sxs-lookup"><span data-stu-id="b7424-348">NU1701</span></span>

| | |
| --- | --- |
| <span data-ttu-id="b7424-349">**问题**</span><span class="sxs-lookup"><span data-stu-id="b7424-349">**Issue**</span></span> | <span data-ttu-id="b7424-350">*PackageTargetFallback/AssetTargetFallback*用于从包选择资产。</span><span class="sxs-lookup"><span data-stu-id="b7424-350">*PackageTargetFallback/AssetTargetFallback* was used to select assets from a package.</span></span> <span data-ttu-id="b7424-351">这是警告，以让用户知道资产可能不兼容的 100%。</span><span class="sxs-lookup"><span data-stu-id="b7424-351">This is a warning to let the user know that the assets may not be 100% compatible.</span></span> |
| <span data-ttu-id="b7424-352">**常见原因**</span><span class="sxs-lookup"><span data-stu-id="b7424-352">**Common causes**</span></span> | <span data-ttu-id="b7424-353">包不支持项目框架。</span><span class="sxs-lookup"><span data-stu-id="b7424-353">The package doesn't support the project framework.</span></span> |
| <span data-ttu-id="b7424-354">**示例消息**</span><span class="sxs-lookup"><span data-stu-id="b7424-354">**Example message**</span></span> | <span data-ttu-id="b7424-355">*包 NuGet.Versioning 已还原可移植 net45 + win8 改为使用项目目标框架 netstandard1.5。此程序包并不一定与你的项目完全兼容。*</span><span class="sxs-lookup"><span data-stu-id="b7424-355">*Package 'NuGet.Versioning' was restored using 'portable-net45+win8' instead the project target framework 'netstandard1.5'. This package may not be fully compatible with your project.*</span></span> |

## <a name="feed-warnings"></a><span data-ttu-id="b7424-356">源警告</span><span class="sxs-lookup"><span data-stu-id="b7424-356">Feed warnings</span></span>

[<span data-ttu-id="b7424-357">NU1801</span><span class="sxs-lookup"><span data-stu-id="b7424-357">NU1801</span></span>](#nu1801)

### <a name="nu1801"></a><span data-ttu-id="b7424-358">NU1801</span><span class="sxs-lookup"><span data-stu-id="b7424-358">NU1801</span></span>

| | |
| --- | --- |
| <span data-ttu-id="b7424-359">**问题**</span><span class="sxs-lookup"><span data-stu-id="b7424-359">**Issue**</span></span> | <span data-ttu-id="b7424-360">读取源时出错时`IgnoreFailedSources`设置为 true，将其转换为非致命性警告。</span><span class="sxs-lookup"><span data-stu-id="b7424-360">An error occurred when reading the feed when `IgnoreFailedSources` is set to true, converting it to a non-fatal warning.</span></span> <span data-ttu-id="b7424-361">这可能包含的任何消息，并为泛型。</span><span class="sxs-lookup"><span data-stu-id="b7424-361">This could contain any message and is generic.</span></span> |
| <span data-ttu-id="b7424-362">**常见原因**</span><span class="sxs-lookup"><span data-stu-id="b7424-362">**Common causes**</span></span> | <span data-ttu-id="b7424-363">源无效。</span><span class="sxs-lookup"><span data-stu-id="b7424-363">The source is invalid.</span></span> |
| <span data-ttu-id="b7424-364">**示例消息**</span><span class="sxs-lookup"><span data-stu-id="b7424-364">**Example message**</span></span> | <span data-ttu-id="b7424-365">无</span><span class="sxs-lookup"><span data-stu-id="b7424-365">n/a</span></span> |

## <a name="nuget-internal-errors-and-warnings"></a><span data-ttu-id="b7424-366">NuGet 内部错误和警告</span><span class="sxs-lookup"><span data-stu-id="b7424-366">NuGet internal errors and warnings</span></span>

<span data-ttu-id="b7424-367">[NU1000](#nu1000) | [NU1500](#nu1500)</span><span class="sxs-lookup"><span data-stu-id="b7424-367">[NU1000](#nu1000) | [NU1500](#nu1500)</span></span>

### <a name="nu1000"></a><span data-ttu-id="b7424-368">NU1000</span><span class="sxs-lookup"><span data-stu-id="b7424-368">NU1000</span></span>

| | |
| --- | --- |
| <span data-ttu-id="b7424-369">**问题**</span><span class="sxs-lookup"><span data-stu-id="b7424-369">**Issue**</span></span> | <span data-ttu-id="b7424-370">从 NuGet 非特定的内部错误。</span><span class="sxs-lookup"><span data-stu-id="b7424-370">A non specific internal error from NuGet.</span></span> |
| <span data-ttu-id="b7424-371">**常见原因**</span><span class="sxs-lookup"><span data-stu-id="b7424-371">**Common causes**</span></span> | <span data-ttu-id="b7424-372">检查日志以了解更多信息</span><span class="sxs-lookup"><span data-stu-id="b7424-372">Check the logs for more information</span></span> |

### <a name="nu1500"></a><span data-ttu-id="b7424-373">NU1500</span><span class="sxs-lookup"><span data-stu-id="b7424-373">NU1500</span></span>

| | |
| --- | --- |
| <span data-ttu-id="b7424-374">**问题**</span><span class="sxs-lookup"><span data-stu-id="b7424-374">**Issue**</span></span> | <span data-ttu-id="b7424-375">从 NuGet 内部非特定警告。</span><span class="sxs-lookup"><span data-stu-id="b7424-375">A non specific internal warning from NuGet.</span></span> |
| <span data-ttu-id="b7424-376">**常见原因**</span><span class="sxs-lookup"><span data-stu-id="b7424-376">**Common causes**</span></span> | <span data-ttu-id="b7424-377">检查日志以了解更多信息</span><span class="sxs-lookup"><span data-stu-id="b7424-377">Check the logs for more information</span></span> |
