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
ms.openlocfilehash: 29eb72cbb6c095cd3aeb524fd8b28416ec5dc798
ms.sourcegitcommit: 6ccb963e065680ab2e7df1d8dd5492897fd56b04
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/23/2018
---
# <a name="errors-and-warnings"></a><span data-ttu-id="a7054-104">错误和警告</span><span class="sxs-lookup"><span data-stu-id="a7054-104">Errors and warnings</span></span>

<span data-ttu-id="a7054-105">在 NuGet 4.3.0，错误和警告本主题中所述进行编号，并提供详细的信息来帮助您解决所涉及的问题。</span><span class="sxs-lookup"><span data-stu-id="a7054-105">In NuGet 4.3.0, errors and warnings are numbered as described in this topic and provide detailed information to help you address the issues involved.</span></span> 

<span data-ttu-id="a7054-106">错误和警告在此处列出是仅适用于[PackageReference 基于](../Consume-Packages/Package-References-in-Project-Files.md)项目和 NuGet 4.3.0。</span><span class="sxs-lookup"><span data-stu-id="a7054-106">The errors and warnings listed here are available only with [PackageReference-based](../Consume-Packages/Package-References-in-Project-Files.md) projects and NuGet 4.3.0.</span></span> <span data-ttu-id="a7054-107">NuGet 也服从 MSBuild 属性，以禁止显示警告或将它们提升到错误。</span><span class="sxs-lookup"><span data-stu-id="a7054-107">NuGet also honors MSBuild properties to suppress warnings or elevate them to errors.</span></span> <span data-ttu-id="a7054-108">有关详细信息，请参阅[如何： 禁止显示编译器警告](/visualstudio/ide/how-to-suppress-compiler-warnings)Visual Studio 文档中。</span><span class="sxs-lookup"><span data-stu-id="a7054-108">For more information, see [How to: Suppress Compiler Warnings](/visualstudio/ide/how-to-suppress-compiler-warnings) in the Visual Studio documentation.</span></span>

<span data-ttu-id="a7054-109">**错误**</span><span class="sxs-lookup"><span data-stu-id="a7054-109">**Errors**</span></span>

| <span data-ttu-id="a7054-110">Group</span><span class="sxs-lookup"><span data-stu-id="a7054-110">Group</span></span> | <span data-ttu-id="a7054-111">错误号</span><span class="sxs-lookup"><span data-stu-id="a7054-111">Error Numbers</span></span> |
| --- | --- |
| [<span data-ttu-id="a7054-112">无效的输入的错误</span><span class="sxs-lookup"><span data-stu-id="a7054-112">Invalid input errors</span></span>](#invalid-input-errors) | <span data-ttu-id="a7054-113">[NU1001](#nu1001), [NU1002](#nu1002), [NU1003](#nu1003)</span><span class="sxs-lookup"><span data-stu-id="a7054-113">[NU1001](#nu1001), [NU1002](#nu1002), [NU1003](#nu1003)</span></span> |
| [<span data-ttu-id="a7054-114">缺少的包和项目错误</span><span class="sxs-lookup"><span data-stu-id="a7054-114">Missing package and project errors</span></span>](#missing-package-and-project-errors) | <span data-ttu-id="a7054-115">[NU1100](#nu1100)， [NU1101](#nu1101)， [NU1102](#nu1102)， [NU1103](#nu1103)， [NU1104](#nu1104)， [NU1105](#nu1105)， [NU1106](#nu1106)， [NU1107](#nu1107) (以前 NU1607) [NU1108](#nu1108) (以前 NU1606)</span><span class="sxs-lookup"><span data-stu-id="a7054-115">[NU1100](#nu1100), [NU1101](#nu1101), [NU1102](#nu1102), [NU1103](#nu1103), [NU1104](#nu1104), [NU1105](#nu1105), [NU1106](#nu1106), [NU1107](#nu1107) (previously NU1607), [NU1108](#nu1108) (previously NU1606)</span></span> |
| [<span data-ttu-id="a7054-116">兼容性错误</span><span class="sxs-lookup"><span data-stu-id="a7054-116">Compatibility errors</span></span>](#compatibility-errors) | <span data-ttu-id="a7054-117">[NU1201](#nu1201), [NU1202](#nu1202), [NU1203](#nu1203), [NU1401](#nu1401)</span><span class="sxs-lookup"><span data-stu-id="a7054-117">[NU1201](#nu1201), [NU1202](#nu1202), [NU1203](#nu1203), [NU1401](#nu1401)</span></span> |

<span data-ttu-id="a7054-118">**警告**</span><span class="sxs-lookup"><span data-stu-id="a7054-118">**Warnings**</span></span>

| <span data-ttu-id="a7054-119">Group</span><span class="sxs-lookup"><span data-stu-id="a7054-119">Group</span></span> | <span data-ttu-id="a7054-120">警告编号</span><span class="sxs-lookup"><span data-stu-id="a7054-120">Warning numbers</span></span> |
| --- | --- |
| [<span data-ttu-id="a7054-121">无效的输入的警告</span><span class="sxs-lookup"><span data-stu-id="a7054-121">Invalid input warnings</span></span>](#invalid-input-warnings) | <span data-ttu-id="a7054-122">[NU1501](#nu1501)， [NU1502](#nu1502)， [NU1503](#nu1503)</span><span class="sxs-lookup"><span data-stu-id="a7054-122">[NU1501](#nu1501), [NU1502](#nu1502), [NU1503](#nu1503)</span></span> |
| [<span data-ttu-id="a7054-123">意外的包版本警告</span><span class="sxs-lookup"><span data-stu-id="a7054-123">Unexpected package version warnings</span></span>](#unexpected-package-version-warnings) | <span data-ttu-id="a7054-124">[NU1601](#nu1601)， [NU1602](#nu1602)， [NU1603](#nu1603)， [NU1604](#nu1604)， [NU1605](#nu1605)</span><span class="sxs-lookup"><span data-stu-id="a7054-124">[NU1601](#nu1601), [NU1602](#nu1602), [NU1603](#nu1603), [NU1604](#nu1604), [NU1605](#nu1605)</span></span> |
| [<span data-ttu-id="a7054-125">冲突解决程序冲突警告</span><span class="sxs-lookup"><span data-stu-id="a7054-125">Resolver conflict warnings</span></span>](#resolver-conflict-warnings) | [<span data-ttu-id="a7054-126">NU1608</span><span class="sxs-lookup"><span data-stu-id="a7054-126">NU1608</span></span>](#nu1608) |
| [<span data-ttu-id="a7054-127">包回退警告</span><span class="sxs-lookup"><span data-stu-id="a7054-127">Package fallback warnings</span></span>](#package-fallback-warnings) | [<span data-ttu-id="a7054-128">NU1701</span><span class="sxs-lookup"><span data-stu-id="a7054-128">NU1701</span></span>](#nu1701) |
| [<span data-ttu-id="a7054-129">源警告</span><span class="sxs-lookup"><span data-stu-id="a7054-129">Feed warnings</span></span>](#feed-warnings) | [<span data-ttu-id="a7054-130">NU1801</span><span class="sxs-lookup"><span data-stu-id="a7054-130">NU1801</span></span>](#nu1801) |
| [<span data-ttu-id="a7054-131">NuGet 内部错误和警告</span><span class="sxs-lookup"><span data-stu-id="a7054-131">NuGet internal errors and warnings</span></span>](#nuget-internal-errors-and-warnings) | <span data-ttu-id="a7054-132">[NU1000](#nu1000), [NU1500](#nu1500)</span><span class="sxs-lookup"><span data-stu-id="a7054-132">[NU1000](#nu1000), [NU1500](#nu1500)</span></span> |

## <a name="invalid-input-errors"></a><span data-ttu-id="a7054-133">无效的输入的错误</span><span class="sxs-lookup"><span data-stu-id="a7054-133">Invalid input errors</span></span>

<span data-ttu-id="a7054-134">[NU1001](#nu1001) | [NU1002](#nu1002) | [NU1003](#nu1003)</span><span class="sxs-lookup"><span data-stu-id="a7054-134">[NU1001](#nu1001) | [NU1002](#nu1002) | [NU1003](#nu1003)</span></span>

### <a name="nu1001"></a><span data-ttu-id="a7054-135">NU1001</span><span class="sxs-lookup"><span data-stu-id="a7054-135">NU1001</span></span>

| | |
| --- | --- |
| <span data-ttu-id="a7054-136">**问题**</span><span class="sxs-lookup"><span data-stu-id="a7054-136">**Issue**</span></span> | <span data-ttu-id="a7054-137">项目不包含一个或多个框架。</span><span class="sxs-lookup"><span data-stu-id="a7054-137">The project doesn't contain one or more frameworks.</span></span> |
| <span data-ttu-id="a7054-138">**常见原因**</span><span class="sxs-lookup"><span data-stu-id="a7054-138">**Common causes**</span></span> | <span data-ttu-id="a7054-139">项目不包含`TargetFramework`或`TargetFrameworks`属性。</span><span class="sxs-lookup"><span data-stu-id="a7054-139">The project doesn't contain a `TargetFramework` or `TargetFrameworks` property.</span></span> |
| <span data-ttu-id="a7054-140">**示例消息**</span><span class="sxs-lookup"><span data-stu-id="a7054-140">**Example message**</span></span> | <span data-ttu-id="a7054-141">*项目 projA c:\tmp\projA.csproj 中未指定任何目标框架*</span><span class="sxs-lookup"><span data-stu-id="a7054-141">*The project projA does not specify any target frameworks in c:\tmp\projA.csproj*</span></span> |

### <a name="nu1002"></a><span data-ttu-id="a7054-142">NU1002</span><span class="sxs-lookup"><span data-stu-id="a7054-142">NU1002</span></span>

| | |
| --- | --- |
| <span data-ttu-id="a7054-143">**问题**</span><span class="sxs-lookup"><span data-stu-id="a7054-143">**Issue**</span></span> | <span data-ttu-id="a7054-144">无效的输入以及清除关键字的组合。</span><span class="sxs-lookup"><span data-stu-id="a7054-144">Invalid combination of inputs along with a CLEAR keyword.</span></span> |
| <span data-ttu-id="a7054-145">**常见原因**</span><span class="sxs-lookup"><span data-stu-id="a7054-145">**Common causes**</span></span> | <span data-ttu-id="a7054-146">清除不能使用其他输入组合。</span><span class="sxs-lookup"><span data-stu-id="a7054-146">CLEAR may not be combined with other inputs.</span></span> |
| <span data-ttu-id="a7054-147">**示例消息**</span><span class="sxs-lookup"><span data-stu-id="a7054-147">**Example message**</span></span> | <span data-ttu-id="a7054-148">*清除不能在与其他值一起使用*</span><span class="sxs-lookup"><span data-stu-id="a7054-148">*'CLEAR' cannot be used in conjunction with other values*</span></span> |

### <a name="nu1003"></a><span data-ttu-id="a7054-149">NU1003</span><span class="sxs-lookup"><span data-stu-id="a7054-149">NU1003</span></span>

| | |
| --- | --- |
| <span data-ttu-id="a7054-150">**问题**</span><span class="sxs-lookup"><span data-stu-id="a7054-150">**Issue**</span></span> | <span data-ttu-id="a7054-151">`PackageTargetFallback`和`AssetTargetFallback`用于选择资产提供不同的行为和不能一起使用。</span><span class="sxs-lookup"><span data-stu-id="a7054-151">`PackageTargetFallback` and `AssetTargetFallback` provide different behavior for selecting assets and cannot be used together.</span></span> |
| <span data-ttu-id="a7054-152">**常见原因**</span><span class="sxs-lookup"><span data-stu-id="a7054-152">**Common causes**</span></span> | <span data-ttu-id="a7054-153">同时`PackageTargetFallback`和`AssetTargetFallback`项目中存在。</span><span class="sxs-lookup"><span data-stu-id="a7054-153">Both `PackageTargetFallback` and `AssetTargetFallback` exist in the project.</span></span> |
| <span data-ttu-id="a7054-154">**示例消息**</span><span class="sxs-lookup"><span data-stu-id="a7054-154">**Example message**</span></span> | <span data-ttu-id="a7054-155">*PackageTargetFallback 和 AssetTargetFallback 不能一起使用。从项目环境删除 PackageTargetFallback(deprecated) 的引用。*</span><span class="sxs-lookup"><span data-stu-id="a7054-155">*PackageTargetFallback and AssetTargetFallback cannot be used together. Remove PackageTargetFallback(deprecated) references from the project environment.*</span></span> |

## <a name="missing-package-and-project-errors"></a><span data-ttu-id="a7054-156">缺少的包和项目错误</span><span class="sxs-lookup"><span data-stu-id="a7054-156">Missing package and project errors</span></span>

<span data-ttu-id="a7054-157">[NU1100](#nu1100) | [NU1101](#nu1101) | [NU1102](#nu1102) | [NU1103](#nu1103) | [NU1104](#nu1104) | [NU1105](#nu1105) | [NU1106](#nu1106)</span><span class="sxs-lookup"><span data-stu-id="a7054-157">[NU1100](#nu1100) | [NU1101](#nu1101) | [NU1102](#nu1102) | [NU1103](#nu1103) | [NU1104](#nu1104) | [NU1105](#nu1105) | [NU1106](#nu1106)</span></span>

### <a name="nu1100"></a><span data-ttu-id="a7054-158">NU1100</span><span class="sxs-lookup"><span data-stu-id="a7054-158">NU1100</span></span>

| | |
| --- | --- |
| <span data-ttu-id="a7054-159">**问题**</span><span class="sxs-lookup"><span data-stu-id="a7054-159">**Issue**</span></span> | <span data-ttu-id="a7054-160">依赖关系组不被解析。</span><span class="sxs-lookup"><span data-stu-id="a7054-160">A dependency group not be resolved.</span></span> <span data-ttu-id="a7054-161">这是一个泛型类型不是包或项目的问题。</span><span class="sxs-lookup"><span data-stu-id="a7054-161">This is a generic issue for types that are not packages or projects.</span></span> |
| <span data-ttu-id="a7054-162">**常见原因**</span><span class="sxs-lookup"><span data-stu-id="a7054-162">**Common causes**</span></span> | <span data-ttu-id="a7054-163">项目包含依赖于不存在的项。</span><span class="sxs-lookup"><span data-stu-id="a7054-163">The project contains a dependency on an item that doesn't exist.</span></span> |
| <span data-ttu-id="a7054-164">**示例消息**</span><span class="sxs-lookup"><span data-stu-id="a7054-164">**Example message**</span></span> | <span data-ttu-id="a7054-165">*无法解析 net45 System.Missing*</span><span class="sxs-lookup"><span data-stu-id="a7054-165">*Unable to resolve System.Missing for net45*</span></span> |

### <a name="nu1101"></a><span data-ttu-id="a7054-166">NU1101</span><span class="sxs-lookup"><span data-stu-id="a7054-166">NU1101</span></span>

| | |
| --- | --- |
| <span data-ttu-id="a7054-167">**问题**</span><span class="sxs-lookup"><span data-stu-id="a7054-167">**Issue**</span></span> | <span data-ttu-id="a7054-168">在任何源上找不到包。</span><span class="sxs-lookup"><span data-stu-id="a7054-168">The package cannot be found on any sources.</span></span> |
| <span data-ttu-id="a7054-169">**常见原因**</span><span class="sxs-lookup"><span data-stu-id="a7054-169">**Common causes**</span></span> | <span data-ttu-id="a7054-170">正确的包源缺失或不正确的包标识符。</span><span class="sxs-lookup"><span data-stu-id="a7054-170">The correct package source is missing or the package identifier is incorrect.</span></span> |
| <span data-ttu-id="a7054-171">**示例消息**</span><span class="sxs-lookup"><span data-stu-id="a7054-171">**Example message**</span></span> | <span data-ttu-id="a7054-172">*找不到程序包 System.Missing。具有此 id 在源中存在的任何包： dotnet 核心、 dotnet roslyn、 nuget.org*</span><span class="sxs-lookup"><span data-stu-id="a7054-172">*Unable to find package System.Missing. No packages exist with this id in source(s): dotnet-core, dotnet-roslyn, nuget.org*</span></span> |

### <a name="nu1102"></a><span data-ttu-id="a7054-173">NU1102</span><span class="sxs-lookup"><span data-stu-id="a7054-173">NU1102</span></span>

| | |
| --- | --- |
| <span data-ttu-id="a7054-174">**问题**</span><span class="sxs-lookup"><span data-stu-id="a7054-174">**Issue**</span></span> | <span data-ttu-id="a7054-175">找到的包标识符，但在任何源上找不到指定的依赖范围内的版本。</span><span class="sxs-lookup"><span data-stu-id="a7054-175">The package identifier is found but a version within the specified dependency range cannot be found on any of the sources.</span></span> |
| <span data-ttu-id="a7054-176">**常见原因**</span><span class="sxs-lookup"><span data-stu-id="a7054-176">**Common causes**</span></span> | <span data-ttu-id="a7054-177">正确的包源缺失或依赖项范围不正确。</span><span class="sxs-lookup"><span data-stu-id="a7054-177">The correct package source is missing or the dependency range is incorrect.</span></span> <span data-ttu-id="a7054-178">可能由包和不是用户指定的范围。</span><span class="sxs-lookup"><span data-stu-id="a7054-178">The range might be specified by a package and not the user.</span></span> <span data-ttu-id="a7054-179">用户可能需要切换到可用的版本，如果此包被直接引用该项目。</span><span class="sxs-lookup"><span data-stu-id="a7054-179">The user may need to switch to an available version if this package is referenced by the project directly.</span></span> |
| <span data-ttu-id="a7054-180">**示例消息**</span><span class="sxs-lookup"><span data-stu-id="a7054-180">**Example message**</span></span> | <span data-ttu-id="a7054-181">*找不到版本包 NuGet.Versioning (> = 9.0.1)<br/> -于 nuget.org 中的找到 30 版本 [最接近的版本： 4.0.0]<br/> -dotnet buildtools 中找到的 10 版本 [最接近的版本： 4.0.0-rc-2129]<br/> -找到 9在 NuGetVolatile 版本 [最接近的版本： 3.0.0-beta-00032]<br/> -0 版本位于 dotnet 核心<br/>-0 版本位于 dotnet roslyn*</span><span class="sxs-lookup"><span data-stu-id="a7054-181">*Unable to find package NuGet.Versioning with version (>= 9.0.1)<br/>  - Found 30 version(s) in nuget.org [ Nearest version: 4.0.0 ]<br/>  - Found 10 version(s) in dotnet-buildtools [ Nearest version: 4.0.0-rc-2129 ]<br/>  - Found 9 version(s) in NuGetVolatile [ Nearest version: 3.0.0-beta-00032 ]<br/>  - Found 0 version(s) in dotnet-core<br/>  - Found 0 version(s) in dotnet-roslyn*</span></span> |

### <a name="nu1103"></a><span data-ttu-id="a7054-182">NU1103</span><span class="sxs-lookup"><span data-stu-id="a7054-182">NU1103</span></span>

| | |
| --- | --- |
| <span data-ttu-id="a7054-183">**问题**</span><span class="sxs-lookup"><span data-stu-id="a7054-183">**Issue**</span></span> | <span data-ttu-id="a7054-184">依赖项范围中发现了不稳定的版本。</span><span class="sxs-lookup"><span data-stu-id="a7054-184">No stable versions were found in the dependency range.</span></span> <span data-ttu-id="a7054-185">预发行版本未找到，但不是允许。</span><span class="sxs-lookup"><span data-stu-id="a7054-185">Pre-release versions were found but are not allowed.</span></span> |
| <span data-ttu-id="a7054-186">**常见原因**</span><span class="sxs-lookup"><span data-stu-id="a7054-186">**Common causes**</span></span> | <span data-ttu-id="a7054-187">项目指定的依赖项范围是稳定的版本。</span><span class="sxs-lookup"><span data-stu-id="a7054-187">The project specified a stable version for the dependency range.</span></span> <span data-ttu-id="a7054-188">用户需要更改该版本范围以包括预发行版本。</span><span class="sxs-lookup"><span data-stu-id="a7054-188">Users need to change the version range to include pre-release versions.</span></span> |
| <span data-ttu-id="a7054-189">**示例消息**</span><span class="sxs-lookup"><span data-stu-id="a7054-189">**Example message**</span></span> | <span data-ttu-id="a7054-190">*找不到稳定的包 NuGet.Versioning 随版本 (> = 3.0.0)<br/> -dotnet buildtools 中找到的 10 版本 [最接近的版本： 4.0.0-rc-2129]<br/> -NuGetVolatile 中的找到 9 版本 [最接近的版本： 3.0.0-beta-00032]<br/> -0 版本位于 dotnet 核心<br/>-0 版本位于 dotnet roslyn*</span><span class="sxs-lookup"><span data-stu-id="a7054-190">*Unable to find a stable package NuGet.Versioning with version (>= 3.0.0)<br/>  - Found 10 version(s) in dotnet-buildtools [ Nearest version: 4.0.0-rc-2129 ]<br/>  - Found 9 version(s) in NuGetVolatile [ Nearest version: 3.0.0-beta-00032 ]<br/>  - Found 0 version(s) in dotnet-core<br/>  - Found 0 version(s) in dotnet-roslyn*</span></span> |

### <a name="nu1104"></a><span data-ttu-id="a7054-191">NU1104</span><span class="sxs-lookup"><span data-stu-id="a7054-191">NU1104</span></span>

| | |
| --- | --- |
| <span data-ttu-id="a7054-192">**问题**</span><span class="sxs-lookup"><span data-stu-id="a7054-192">**Issue**</span></span> | <span data-ttu-id="a7054-193">ProjectReference 指向不存在的文件。</span><span class="sxs-lookup"><span data-stu-id="a7054-193">A ProjectReference points to a file that doesn't exist.</span></span> |
| <span data-ttu-id="a7054-194">**常见原因**</span><span class="sxs-lookup"><span data-stu-id="a7054-194">**Common causes**</span></span> | <span data-ttu-id="a7054-195">项目文件缺少从磁盘或引用不正确。</span><span class="sxs-lookup"><span data-stu-id="a7054-195">The project file is missing from disk or the reference is incorrect.</span></span> |
| <span data-ttu-id="a7054-196">**示例消息**</span><span class="sxs-lookup"><span data-stu-id="a7054-196">**Example message**</span></span> | <span data-ttu-id="a7054-197">*项目引用不存在 c:\a.csproj。检查项目引用有效以及项目文件是否存在。*</span><span class="sxs-lookup"><span data-stu-id="a7054-197">*Project reference does not exist 'c:\a.csproj'. Check that the project reference is valid and that the project file exists.*</span></span> |

### <a name="nu1105"></a><span data-ttu-id="a7054-198">NU1105</span><span class="sxs-lookup"><span data-stu-id="a7054-198">NU1105</span></span>

| | |
| --- | --- |
| <span data-ttu-id="a7054-199">**问题**</span><span class="sxs-lookup"><span data-stu-id="a7054-199">**Issue**</span></span> | <span data-ttu-id="a7054-200">项目文件存在，但不还原信息已为其提供。</span><span class="sxs-lookup"><span data-stu-id="a7054-200">The project file exists but no restore information was provided for it.</span></span> |
| <span data-ttu-id="a7054-201">**常见原因**</span><span class="sxs-lookup"><span data-stu-id="a7054-201">**Common causes**</span></span> | <span data-ttu-id="a7054-202">在 Visual Studio 中，这可能意味着该项目已卸载。</span><span class="sxs-lookup"><span data-stu-id="a7054-202">In Visual Studio this could mean that the project is unloaded.</span></span> <span data-ttu-id="a7054-203">从命令行中，这可能表示该文件已损坏或后进行恢复从中读取项目所需的导入目标不包含自定义。</span><span class="sxs-lookup"><span data-stu-id="a7054-203">From the command line this could mean that the file is corrupt or that it doesn't contain the custom after imports target needed for restore to read the project.</span></span> |
| <span data-ttu-id="a7054-204">**示例消息**</span><span class="sxs-lookup"><span data-stu-id="a7054-204">**Example message**</span></span> | <span data-ttu-id="a7054-205">*无法读取 c:\a.csproj 的项目信息。项目文件可能无效或缺少所需的还原的目标。*</span><span class="sxs-lookup"><span data-stu-id="a7054-205">*Unable to read project information for 'c:\a.csproj'. The project file may be invalid or missing targets required for restore.*</span></span> |

### <a name="nu1106"></a><span data-ttu-id="a7054-206">NU1106</span><span class="sxs-lookup"><span data-stu-id="a7054-206">NU1106</span></span>

| | |
| --- | --- |
| <span data-ttu-id="a7054-207">**问题**</span><span class="sxs-lookup"><span data-stu-id="a7054-207">**Issue**</span></span> | <span data-ttu-id="a7054-208">无法解析依赖项约束。</span><span class="sxs-lookup"><span data-stu-id="a7054-208">Dependency constraints cannot be resolved.</span></span> |
| <span data-ttu-id="a7054-209">**常见原因**</span><span class="sxs-lookup"><span data-stu-id="a7054-209">**Common causes**</span></span> | <span data-ttu-id="a7054-210">包包含的包而不是开放式的范围的确切版本上的依赖项。</span><span class="sxs-lookup"><span data-stu-id="a7054-210">Packages contain dependency on exact versions of a package instead of open-ended ranges.</span></span> |
| <span data-ttu-id="a7054-211">**示例消息**</span><span class="sxs-lookup"><span data-stu-id="a7054-211">**Example message**</span></span> | <span data-ttu-id="a7054-212">*无法满足 {id} 互相冲突的请求: {冲突路径} Framework: {目标关系图}*</span><span class="sxs-lookup"><span data-stu-id="a7054-212">*Unable to satisfy conflicting requests for {id}: {conflict path} Framework: {target graph}*</span></span> |

<a name="nu1107"></a> 

### <a name="nu1107-previously-nu1607"></a><span data-ttu-id="a7054-213">NU1107 (以前 NU1607)</span><span class="sxs-lookup"><span data-stu-id="a7054-213">NU1107 (Previously NU1607)</span></span>

| | |
| --- | --- |
| <span data-ttu-id="a7054-214">**问题**</span><span class="sxs-lookup"><span data-stu-id="a7054-214">**Issue**</span></span> | <span data-ttu-id="a7054-215">无法解析包之间的依赖关系约束。</span><span class="sxs-lookup"><span data-stu-id="a7054-215">Unable to resolve dependency constraints between packages.</span></span> |
| <span data-ttu-id="a7054-216">**常见原因**</span><span class="sxs-lookup"><span data-stu-id="a7054-216">**Common causes**</span></span> | <span data-ttu-id="a7054-217">依赖项与上的约束的确切版本的包不允许其他包以根据需要增大版本号。</span><span class="sxs-lookup"><span data-stu-id="a7054-217">Packages with dependency constraints on exact versions do not allow other packages to increase the version if needed.</span></span> |
| <span data-ttu-id="a7054-218">**示例消息**</span><span class="sxs-lookup"><span data-stu-id="a7054-218">**Example message**</span></span> | <span data-ttu-id="a7054-219">*NuGet.Versioning 检测到的版本冲突。若要解决此问题的项目中直接引用包。<br/>NuGet.Packaging 3.5.0-> （= 3.5.0） NuGet.Versioning<br/> NuGet.Configuration 4.0.0-> 的 NuGet.Versioning （= 4.0.0）*</span><span class="sxs-lookup"><span data-stu-id="a7054-219">*Version conflict detected for NuGet.Versioning. Reference the package directly from the project to resolve this issue.<br/>  NuGet.Packaging 3.5.0 -> NuGet.Versioning (= 3.5.0)<br/>  NuGet.Configuration 4.0.0 -> NuGet.Versioning (= 4.0.0)*</span></span> |

<a name="nu1108"></a>

### <a name="nu1108-previously-nu1606"></a><span data-ttu-id="a7054-220">NU1108 (以前 NU1606)</span><span class="sxs-lookup"><span data-stu-id="a7054-220">NU1108 (Previously NU1606)</span></span>

| | |
| --- | --- |
| <span data-ttu-id="a7054-221">**问题**</span><span class="sxs-lookup"><span data-stu-id="a7054-221">**Issue**</span></span> | <span data-ttu-id="a7054-222">检测到循环依赖关系。</span><span class="sxs-lookup"><span data-stu-id="a7054-222">A circular dependency was detected.</span></span> |
| <span data-ttu-id="a7054-223">**常见原因**</span><span class="sxs-lookup"><span data-stu-id="a7054-223">**Common causes**</span></span> | <span data-ttu-id="a7054-224">未正确编写了包。</span><span class="sxs-lookup"><span data-stu-id="a7054-224">A package is authored incorrectly.</span></span> |
| <span data-ttu-id="a7054-225">**示例消息**</span><span class="sxs-lookup"><span data-stu-id="a7054-225">**Example message**</span></span> | <span data-ttu-id="a7054-226">*检测到循环： A-> B-> A*</span><span class="sxs-lookup"><span data-stu-id="a7054-226">*Cycle detected: A -> B -> A*</span></span> |

## <a name="compatibility-errors"></a><span data-ttu-id="a7054-227">兼容性错误</span><span class="sxs-lookup"><span data-stu-id="a7054-227">Compatibility errors</span></span>

<span data-ttu-id="a7054-228">[NU1201](#nu1201) | [NU1202](#nu1202) | [NU1203](#nu1203) | [NU1401](#nu1401)</span><span class="sxs-lookup"><span data-stu-id="a7054-228">[NU1201](#nu1201) | [NU1202](#nu1202) | [NU1203](#nu1203) | [NU1401](#nu1401)</span></span>

### <a name="nu1201"></a><span data-ttu-id="a7054-229">NU1201</span><span class="sxs-lookup"><span data-stu-id="a7054-229">NU1201</span></span>

| | |
| --- | --- |
| <span data-ttu-id="a7054-230">**问题**</span><span class="sxs-lookup"><span data-stu-id="a7054-230">**Issue**</span></span> | <span data-ttu-id="a7054-231">依赖项项目不包含与当前项目兼容的框架。</span><span class="sxs-lookup"><span data-stu-id="a7054-231">A dependency project doesn't contain a framework compatible with the current project.</span></span> |
| <span data-ttu-id="a7054-232">**常见原因**</span><span class="sxs-lookup"><span data-stu-id="a7054-232">**Common causes**</span></span> | <span data-ttu-id="a7054-233">项目的目标框架是比使用项目的更高版本。</span><span class="sxs-lookup"><span data-stu-id="a7054-233">The project's target framework is a higher version than the consuming project.</span></span> |
| <span data-ttu-id="a7054-234">**示例消息**</span><span class="sxs-lookup"><span data-stu-id="a7054-234">**Example message**</span></span> | <span data-ttu-id="a7054-235">*项目 ServerWeb 与不兼容 netstandard1.3 (。NETStandard，Version = v1.3)。项目 ServerWeb 支持：<br/> -netstandard1.6 (。NETStandard，Version = v1.6)<br/> -netcoreapp1.0 (。NETCoreApp，Version = v1.0)*</span><span class="sxs-lookup"><span data-stu-id="a7054-235">*Project ServerWeb is not compatible with netstandard1.3 (.NETStandard,Version=v1.3). Project ServerWeb supports:<br/>  - netstandard1.6 (.NETStandard,Version=v1.6)<br/>  - netcoreapp1.0 (.NETCoreApp,Version=v1.0)*</span></span> |

### <a name="nu1202"></a><span data-ttu-id="a7054-236">NU1202</span><span class="sxs-lookup"><span data-stu-id="a7054-236">NU1202</span></span>

| | |
| --- | --- |
| <span data-ttu-id="a7054-237">**问题**</span><span class="sxs-lookup"><span data-stu-id="a7054-237">**Issue**</span></span> | <span data-ttu-id="a7054-238">依赖项包不包含任何与项目兼容的资产。</span><span class="sxs-lookup"><span data-stu-id="a7054-238">A dependency package doesn't contain any assets compatible with the project.</span></span> |
| <span data-ttu-id="a7054-239">**常见原因**</span><span class="sxs-lookup"><span data-stu-id="a7054-239">**Common causes**</span></span> | <span data-ttu-id="a7054-240">包不支持项目的目标框架。</span><span class="sxs-lookup"><span data-stu-id="a7054-240">The package doesn't support the project's target framework.</span></span> |
| <span data-ttu-id="a7054-241">**示例消息**</span><span class="sxs-lookup"><span data-stu-id="a7054-241">**Example message**</span></span> | <span data-ttu-id="a7054-242">*包 System.ComponentModel.EventBasedAsync 4.0.11 与不兼容 netstandard1.3 (。NETStandard，Version = v1.3)。打包 System.ComponentModel.EventBasedAsync 4.0.11 支持：<br/> -monoandroid10 (MonoAndroid，Version = v1.0)<br/> -monotouch10 (MonoTouch，Version = v1.0)<br/> -net45 (。NETFramework，Version = v4.5)<br/> -netcore50 (。NETCore，Version = 5.0 版)<br/> -netstandard1.0 (。NETStandard，Version = v1.0)<br/> -可移植 net45 + win8 + wp8 + wpa81 (。NETPortable，Version = v0.0，配置文件 = Profile259)<br/> -win8 (Windows、 版本 = v8.0)<br/> -wp8 (WindowsPhone，Version = v8.0)<br/> -wpa81 (WindowsPhoneApp，Version = v8.1)<br/> -xamarinios10 (Xamarin.iOS,Version=v1.0)<br/> -xamarinmac20 (Xamarin.Mac,Version=v2.0)<br/> -xamarintvos10 (Xamarin.TVOS,Version=v1.0)<br/> -xamarinwatchos10 (Xamarin.WatchOS,Version=v1.0)*</span><span class="sxs-lookup"><span data-stu-id="a7054-242">*Package System.ComponentModel.EventBasedAsync 4.0.11 is not compatible with netstandard1.3 (.NETStandard,Version=v1.3). Package System.ComponentModel.EventBasedAsync 4.0.11 supports:<br/>  - monoandroid10 (MonoAndroid,Version=v1.0)<br/>  - monotouch10 (MonoTouch,Version=v1.0)<br/>  - net45 (.NETFramework,Version=v4.5)<br/>  - netcore50 (.NETCore,Version=v5.0)<br/>  - netstandard1.0 (.NETStandard,Version=v1.0)<br/>  - portable-net45+win8+wp8+wpa81 (.NETPortable,Version=v0.0,Profile=Profile259)<br/>  - win8 (Windows,Version=v8.0)<br/>  - wp8 (WindowsPhone,Version=v8.0)<br/>  - wpa81 (WindowsPhoneApp,Version=v8.1)<br/>  - xamarinios10 (Xamarin.iOS,Version=v1.0)<br/>  - xamarinmac20 (Xamarin.Mac,Version=v2.0)<br/>  - xamarintvos10 (Xamarin.TVOS,Version=v1.0)<br/>  - xamarinwatchos10 (Xamarin.WatchOS,Version=v1.0)*</span></span>|

### <a name="nu1203"></a><span data-ttu-id="a7054-243">NU1203</span><span class="sxs-lookup"><span data-stu-id="a7054-243">NU1203</span></span>

| | |
| --- | --- |
| <span data-ttu-id="a7054-244">**问题**</span><span class="sxs-lookup"><span data-stu-id="a7054-244">**Issue**</span></span> | <span data-ttu-id="a7054-245">包不支持项目的`RuntimeIdentifier`。</span><span class="sxs-lookup"><span data-stu-id="a7054-245">The package doesn't support the project's `RuntimeIdentifier`.</span></span> |
| <span data-ttu-id="a7054-246">**常见原因**</span><span class="sxs-lookup"><span data-stu-id="a7054-246">**Common causes**</span></span> | <span data-ttu-id="a7054-247">包不支持当前`RuntimeIdentifier`。</span><span class="sxs-lookup"><span data-stu-id="a7054-247">The package doesn't support the current `RuntimeIdentifier`.</span></span> <span data-ttu-id="a7054-248">更改`RuntimeIdentifier`如果需要在项目中使用的值。</span><span class="sxs-lookup"><span data-stu-id="a7054-248">Change the `RuntimeIdentifier` values used in the project if needed.</span></span> |
| <span data-ttu-id="a7054-249">**示例消息**</span><span class="sxs-lookup"><span data-stu-id="a7054-249">**Example message**</span></span> | <span data-ttu-id="a7054-250">*System.Example 1.0.0 提供 a.dll 的编译时引用程序集上 net461，但没有兼容的运行时程序集。*</span><span class="sxs-lookup"><span data-stu-id="a7054-250">*System.Example 1.0.0 provides a compile-time reference assembly for a.dll on net461, but there is no compatible run-time assembly.*</span></span> |

### <a name="nu1401"></a><span data-ttu-id="a7054-251">NU1401</span><span class="sxs-lookup"><span data-stu-id="a7054-251">NU1401</span></span>

| | |
| --- | --- |
| <span data-ttu-id="a7054-252">**问题**</span><span class="sxs-lookup"><span data-stu-id="a7054-252">**Issue**</span></span> | <span data-ttu-id="a7054-253">包需要功能或框架当前不支持安装的 NuGet 版本。</span><span class="sxs-lookup"><span data-stu-id="a7054-253">The package requires features or frameworks not currently supported by the installed version of NuGet.</span></span> |
| <span data-ttu-id="a7054-254">**常见原因**</span><span class="sxs-lookup"><span data-stu-id="a7054-254">**Common causes**</span></span> | <span data-ttu-id="a7054-255">升级 NuGet，以解决此问题。</span><span class="sxs-lookup"><span data-stu-id="a7054-255">Upgrade NuGet to fix the issue.</span></span> |
| <span data-ttu-id="a7054-256">**示例消息**</span><span class="sxs-lookup"><span data-stu-id="a7054-256">**Example message**</span></span> | <span data-ttu-id="a7054-257">*NuGet.Versioning 程序包需要 NuGet 客户端版本"5.0.0"或更高版本，但是当前 NuGet 版本为"4.3.0"。若要升级 NuGet，请转到 http://docs.nuget.org/consume/installing-nuget。*</span><span class="sxs-lookup"><span data-stu-id="a7054-257">*The 'NuGet.Versioning' package requires NuGet client version '5.0.0' or above, but the current NuGet version is '4.3.0'. To upgrade NuGet, please go to http://docs.nuget.org/consume/installing-nuget.*</span></span> |

## <a name="invalid-input-warnings"></a><span data-ttu-id="a7054-258">无效的输入的警告</span><span class="sxs-lookup"><span data-stu-id="a7054-258">Invalid input warnings</span></span>

<span data-ttu-id="a7054-259">[NU1501](#nu1501) | [NU1502](#nu1502) | [NU1503](#nu1503)</span><span class="sxs-lookup"><span data-stu-id="a7054-259">[NU1501](#nu1501) | [NU1502](#nu1502) | [NU1503](#nu1503)</span></span>

### <a name="nu1501"></a><span data-ttu-id="a7054-260">NU1501</span><span class="sxs-lookup"><span data-stu-id="a7054-260">NU1501</span></span>

| | |
| --- | --- |
| <span data-ttu-id="a7054-261">**问题**</span><span class="sxs-lookup"><span data-stu-id="a7054-261">**Issue**</span></span> | <span data-ttu-id="a7054-262">项目还原尝试运行在未找到。</span><span class="sxs-lookup"><span data-stu-id="a7054-262">The project restore is attempting to operate on was not found.</span></span> |
| <span data-ttu-id="a7054-263">**常见原因**</span><span class="sxs-lookup"><span data-stu-id="a7054-263">**Common causes**</span></span> | <span data-ttu-id="a7054-264">找不到该项目。</span><span class="sxs-lookup"><span data-stu-id="a7054-264">The project is missing.</span></span> |
| <span data-ttu-id="a7054-265">**示例消息**</span><span class="sxs-lookup"><span data-stu-id="a7054-265">**Example message**</span></span> | <span data-ttu-id="a7054-266">*文件夹 c:\projects\a 不包含要还原的项目。*</span><span class="sxs-lookup"><span data-stu-id="a7054-266">*The folder 'c:\projects\a' does not contain a project to restore.*</span></span> |

### <a name="nu1502"></a><span data-ttu-id="a7054-267">NU1502</span><span class="sxs-lookup"><span data-stu-id="a7054-267">NU1502</span></span>

| | |
| --- | --- |
| <span data-ttu-id="a7054-268">**问题**</span><span class="sxs-lookup"><span data-stu-id="a7054-268">**Issue**</span></span> | <span data-ttu-id="a7054-269">`RuntimeSupports`包含无效的配置文件。</span><span class="sxs-lookup"><span data-stu-id="a7054-269">`RuntimeSupports` contains an invalid profile.</span></span> |
| <span data-ttu-id="a7054-270">**常见原因**</span><span class="sxs-lookup"><span data-stu-id="a7054-270">**Common causes**</span></span> | <span data-ttu-id="a7054-271">中找不到支持的配置文件`runtime.json`从当前的依赖项包文件。</span><span class="sxs-lookup"><span data-stu-id="a7054-271">The supports profile was not found in a `runtime.json` file from the current dependency packages.</span></span> |
| <span data-ttu-id="a7054-272">**示例消息**</span><span class="sxs-lookup"><span data-stu-id="a7054-272">**Example message**</span></span> | <span data-ttu-id="a7054-273">*未知的兼容性配置文件： aaa*</span><span class="sxs-lookup"><span data-stu-id="a7054-273">*Unknown Compatibility Profile: aaa*</span></span> |

### <a name="nu1503"></a><span data-ttu-id="a7054-274">NU1503</span><span class="sxs-lookup"><span data-stu-id="a7054-274">NU1503</span></span>

| | |
| --- | --- |
| <span data-ttu-id="a7054-275">**问题**</span><span class="sxs-lookup"><span data-stu-id="a7054-275">**Issue**</span></span> | <span data-ttu-id="a7054-276">依赖项项目不能导入 NuGet 的恢复目标。</span><span class="sxs-lookup"><span data-stu-id="a7054-276">A dependency project doesn't import NuGet's restore targets.</span></span> <span data-ttu-id="a7054-277">这是类似于 NU1105 但此处项目，将跳过并忽略而不是导致所有还原失败。</span><span class="sxs-lookup"><span data-stu-id="a7054-277">This is similar to NU1105 but here the project is skipped and ignored instead of causing all of restore to fail.</span></span> <span data-ttu-id="a7054-278">在复杂的解决方案通常有其他类型的可能不支持还原的项目中。</span><span class="sxs-lookup"><span data-stu-id="a7054-278">In complex solutions there are often other types of projects that may not support restore.</span></span> |
| <span data-ttu-id="a7054-279">**常见原因**</span><span class="sxs-lookup"><span data-stu-id="a7054-279">**Common causes**</span></span> | <span data-ttu-id="a7054-280">这可能会导致不导入公共属性/目标的自动导入还原的项目。</span><span class="sxs-lookup"><span data-stu-id="a7054-280">This can happen for projects that do not import common props/targets which automatically import restore.</span></span> <span data-ttu-id="a7054-281">如果项目不需要还原这可予以忽视。</span><span class="sxs-lookup"><span data-stu-id="a7054-281">If the project doesn't need to be restored this can be ignored.</span></span> |
| <span data-ttu-id="a7054-282">**示例消息**</span><span class="sxs-lookup"><span data-stu-id="a7054-282">**Example message**</span></span> | <span data-ttu-id="a7054-283">*正在跳过还原项目 c:\a.csproj。项目文件可能无效或缺少所需的还原的目标。*</span><span class="sxs-lookup"><span data-stu-id="a7054-283">*Skipping restore for project 'c:\a.csproj'. The project file may be invalid or missing targets required for restore.*</span></span> |

## <a name="unexpected-package-version-warnings"></a><span data-ttu-id="a7054-284">意外的包版本警告</span><span class="sxs-lookup"><span data-stu-id="a7054-284">Unexpected package version warnings</span></span>

<span data-ttu-id="a7054-285">[NU1601](#nu1601) | [NU1602](#nu1602) | [NU1603](#nu1603) | [NU1604](#nu1604) | [NU1605](#nu1605)</span><span class="sxs-lookup"><span data-stu-id="a7054-285">[NU1601](#nu1601) | [NU1602](#nu1602) | [NU1603](#nu1603) | [NU1604](#nu1604) | [NU1605](#nu1605)</span></span>

### <a name="nu1601"></a><span data-ttu-id="a7054-286">NU1601</span><span class="sxs-lookup"><span data-stu-id="a7054-286">NU1601</span></span>

| | |
| --- | --- |
| <span data-ttu-id="a7054-287">**问题**</span><span class="sxs-lookup"><span data-stu-id="a7054-287">**Issue**</span></span> | <span data-ttu-id="a7054-288">直接项目依赖项已解除了一个为更高版本比指定的项目。</span><span class="sxs-lookup"><span data-stu-id="a7054-288">A direct project dependency was bumped to a higher version than the project specified.</span></span> |
| <span data-ttu-id="a7054-289">**常见原因**</span><span class="sxs-lookup"><span data-stu-id="a7054-289">**Common causes**</span></span> | <span data-ttu-id="a7054-290">另一个依赖项包需要更高版本，并增加包。</span><span class="sxs-lookup"><span data-stu-id="a7054-290">Another dependency package required a higher version and bumped the package up.</span></span> |
| <span data-ttu-id="a7054-291">**示例消息**</span><span class="sxs-lookup"><span data-stu-id="a7054-291">**Example message**</span></span> | <span data-ttu-id="a7054-292">*指定的依赖项已 NuGet.Versioning (> = 3.5.0) 但最终的 NuGet.Versioning 4.0.0。*</span><span class="sxs-lookup"><span data-stu-id="a7054-292">*Dependency specified was NuGet.Versioning (>= 3.5.0) but ended up with NuGet.Versioning 4.0.0.*</span></span> |

### <a name="nu1602"></a><span data-ttu-id="a7054-293">NU1602</span><span class="sxs-lookup"><span data-stu-id="a7054-293">NU1602</span></span>

| | |
| --- | --- |
| <span data-ttu-id="a7054-294">**问题**</span><span class="sxs-lookup"><span data-stu-id="a7054-294">**Issue**</span></span> | <span data-ttu-id="a7054-295">包依赖项缺少零下限。</span><span class="sxs-lookup"><span data-stu-id="a7054-295">A package dependency is missing a lower bound.</span></span> <span data-ttu-id="a7054-296">这不允许还原，以便查找*最佳匹配*。</span><span class="sxs-lookup"><span data-stu-id="a7054-296">This doesn't allow restore to find the *best match*.</span></span> <span data-ttu-id="a7054-297">每个还原将浮动向下尝试查找可以使用较低版本。</span><span class="sxs-lookup"><span data-stu-id="a7054-297">Each restore will float downwards trying to find a lower version that can be used.</span></span> <span data-ttu-id="a7054-298">这意味着此恢复将进入联机状态，以检查每个时间而不是在用户程序包文件夹中使用已存在的包的所有源。</span><span class="sxs-lookup"><span data-stu-id="a7054-298">This means that restore goes online to check all sources each time instead of using the packages that already exist in the user package folder.</span></span> |
| <span data-ttu-id="a7054-299">**常见原因**</span><span class="sxs-lookup"><span data-stu-id="a7054-299">**Common causes**</span></span> | <span data-ttu-id="a7054-300">这通常是创作错误的包。</span><span class="sxs-lookup"><span data-stu-id="a7054-300">This is usually a package authoring error.</span></span> |
| <span data-ttu-id="a7054-301">**示例消息**</span><span class="sxs-lookup"><span data-stu-id="a7054-301">**Example message**</span></span> | <span data-ttu-id="a7054-302">*NuGet.Packaging 4.0.0 不依赖项 NuGet.Versioning (> 3.5.0) 提供包含下限。3.6.0 的近似最佳匹配已解决。*</span><span class="sxs-lookup"><span data-stu-id="a7054-302">*NuGet.Packaging 4.0.0 does not provide an inclusive lower bound for dependency NuGet.Versioning (> 3.5.0). An approximate best match of 3.6.0 was resolved.*</span></span> |

### <a name="nu1603"></a><span data-ttu-id="a7054-303">NU1603</span><span class="sxs-lookup"><span data-stu-id="a7054-303">NU1603</span></span>

| | |
| --- | --- |
| <span data-ttu-id="a7054-304">**问题**</span><span class="sxs-lookup"><span data-stu-id="a7054-304">**Issue**</span></span> | <span data-ttu-id="a7054-305">包依赖项指定未找到的版本。</span><span class="sxs-lookup"><span data-stu-id="a7054-305">A package dependency specified a version that could not be found.</span></span> <span data-ttu-id="a7054-306">与它不同的包编写针对相反，使用更高版本。</span><span class="sxs-lookup"><span data-stu-id="a7054-306">A higher version was used instead, which differs from what the package was authored against.</span></span><br/><br/><span data-ttu-id="a7054-307">这意味着找不到该还原*最佳匹配*。</span><span class="sxs-lookup"><span data-stu-id="a7054-307">This means that restore did not find the *best match*.</span></span> <span data-ttu-id="a7054-308">每个还原将浮动向下尝试查找可以使用较低版本。</span><span class="sxs-lookup"><span data-stu-id="a7054-308">Each restore will float downwards trying to find a lower version that can be used.</span></span> <span data-ttu-id="a7054-309">这意味着此恢复将进入联机状态，以检查每个时间而不是在用户程序包文件夹中使用已存在的包的所有源。</span><span class="sxs-lookup"><span data-stu-id="a7054-309">This means that restore goes online to check all sources each time instead of using the packages that already exist in the user package folder.</span></span> |
| <span data-ttu-id="a7054-310">**常见原因**</span><span class="sxs-lookup"><span data-stu-id="a7054-310">**Common causes**</span></span> | <span data-ttu-id="a7054-311">包源不包含预期的下限版本。</span><span class="sxs-lookup"><span data-stu-id="a7054-311">The package sources do not contain the expected lower bound version.</span></span> <span data-ttu-id="a7054-312">如果尚未释放预期包，这可能是包创作错误。</span><span class="sxs-lookup"><span data-stu-id="a7054-312">If the package expected has not been released then this may be a package authoring error.</span></span> |
| <span data-ttu-id="a7054-313">**示例消息**</span><span class="sxs-lookup"><span data-stu-id="a7054-313">**Example message**</span></span> | <span data-ttu-id="a7054-314">NuGet.Packaging 4.0.0 取决于 NuGet.Versioning (> = 4.0.0) 但找不到 4.0.0。</span><span class="sxs-lookup"><span data-stu-id="a7054-314">NuGet.Packaging 4.0.0 depends on NuGet.Versioning (>= 4.0.0) but 4.0.0 was not found.</span></span> <span data-ttu-id="a7054-315">5.0.0 的近似最佳匹配已解决。</span><span class="sxs-lookup"><span data-stu-id="a7054-315">An approximate best match of 5.0.0 was resolved.</span></span> |

### <a name="nu1604"></a><span data-ttu-id="a7054-316">NU1604</span><span class="sxs-lookup"><span data-stu-id="a7054-316">NU1604</span></span>

| | |
| --- | --- |
| <span data-ttu-id="a7054-317">**问题**</span><span class="sxs-lookup"><span data-stu-id="a7054-317">**Issue**</span></span> | <span data-ttu-id="a7054-318">项目依赖项未定义零下限。</span><span class="sxs-lookup"><span data-stu-id="a7054-318">A project dependency doesn't define a lower bound.</span></span><br/><br/><span data-ttu-id="a7054-319">这意味着找不到该还原*最佳匹配*。</span><span class="sxs-lookup"><span data-stu-id="a7054-319">This means that restore did not find the *best match*.</span></span> <span data-ttu-id="a7054-320">每个还原将浮动向下尝试查找可以使用较低版本。</span><span class="sxs-lookup"><span data-stu-id="a7054-320">Each restore will float downwards trying to find a lower version that can be used.</span></span> <span data-ttu-id="a7054-321">这意味着此恢复将进入联机状态，以检查每个时间而不是在用户程序包文件夹中使用已存在的包的所有源。</span><span class="sxs-lookup"><span data-stu-id="a7054-321">This means that restore goes online to check all sources each time instead of using the packages that already exist in the user package folder.</span></span> |
| <span data-ttu-id="a7054-322">**常见原因**</span><span class="sxs-lookup"><span data-stu-id="a7054-322">**Common causes**</span></span> | <span data-ttu-id="a7054-323">项目的*PackageReference* *版本*应更新属性以包括零下限。</span><span class="sxs-lookup"><span data-stu-id="a7054-323">The project's *PackageReference* *Version* attribute should be updated to include a lower bound.</span></span> |
| <span data-ttu-id="a7054-324">**示例消息**</span><span class="sxs-lookup"><span data-stu-id="a7054-324">**Example message**</span></span> | <span data-ttu-id="a7054-325">*项目依赖项 NuGet.Versioning (< = 9.0.0) doe 不包含包含下限。依赖项版本以确保一致还原结果中包括零下限。*</span><span class="sxs-lookup"><span data-stu-id="a7054-325">*Project dependency NuGet.Versioning (<= 9.0.0) doe not contain an inclusive lower bound. Include a lower bound in the dependency version to ensure consistent restore results.*</span></span> |

### <a name="nu1605"></a><span data-ttu-id="a7054-326">NU1605</span><span class="sxs-lookup"><span data-stu-id="a7054-326">NU1605</span></span>

| | |
| --- | --- |
| <span data-ttu-id="a7054-327">**问题**</span><span class="sxs-lookup"><span data-stu-id="a7054-327">**Issue**</span></span> | <span data-ttu-id="a7054-328">依赖项包指定比还原最终解决更高版本的包的版本约束。</span><span class="sxs-lookup"><span data-stu-id="a7054-328">A dependency package specified a version constraint on a higher version of a package than restore ultimately resolved.</span></span> |
| <span data-ttu-id="a7054-329">**常见原因**</span><span class="sxs-lookup"><span data-stu-id="a7054-329">**Common causes**</span></span> | <span data-ttu-id="a7054-330">接近 wins 解析包时。</span><span class="sxs-lookup"><span data-stu-id="a7054-330">Nearest wins when resolving packages.</span></span> <span data-ttu-id="a7054-331">在图中的最近包可能已重写相距包。</span><span class="sxs-lookup"><span data-stu-id="a7054-331">A nearer package in the graph may have overridden a distant package.</span></span> |
| <span data-ttu-id="a7054-332">**示例消息**</span><span class="sxs-lookup"><span data-stu-id="a7054-332">**Example message**</span></span> | <span data-ttu-id="a7054-333">*检测到包降级： NuGet.Versioning 从 4.0.0 到 3.5.0。要选择的不同版本的项目中直接引用包。<br/>NuGet.Packaging 3.5.0-> NuGet.Versioning 3.5.0<br/> NuGet.Commands 4.0.0-> NuGet.Configuration 4.0.0-> NuGet.Versioning 4.0.0*</span><span class="sxs-lookup"><span data-stu-id="a7054-333">*Detected package downgrade: NuGet.Versioning from 4.0.0 to 3.5.0. Reference the package directly from the project to select a different version.<br/>  NuGet.Packaging 3.5.0 -> NuGet.Versioning 3.5.0<br/>  NuGet.Commands 4.0.0 -> NuGet.Configuration 4.0.0 -> NuGet.Versioning 4.0.0*</span></span> |

## <a name="resolver-conflict-warnings"></a><span data-ttu-id="a7054-334">冲突解决程序冲突警告</span><span class="sxs-lookup"><span data-stu-id="a7054-334">Resolver conflict warnings</span></span>

### <a name="nu1608"></a><span data-ttu-id="a7054-335">NU1608</span><span class="sxs-lookup"><span data-stu-id="a7054-335">NU1608</span></span>

| | |
| --- | --- |
| <span data-ttu-id="a7054-336">**问题**</span><span class="sxs-lookup"><span data-stu-id="a7054-336">**Issue**</span></span> | <span data-ttu-id="a7054-337">解决包是不是依赖项约束允许，更高版本。</span><span class="sxs-lookup"><span data-stu-id="a7054-337">A resolve package is higher than a dependency constraint allows.</span></span> <span data-ttu-id="a7054-338">在某些情况下，这是有意，可以禁止显示警告。</span><span class="sxs-lookup"><span data-stu-id="a7054-338">In some cases this is intentional and the warning can be suppressed.</span></span> |
| <span data-ttu-id="a7054-339">**常见原因**</span><span class="sxs-lookup"><span data-stu-id="a7054-339">**Common causes**</span></span> | <span data-ttu-id="a7054-340">一个项目直接引用的包将覆盖其他包中的依赖关系约束。</span><span class="sxs-lookup"><span data-stu-id="a7054-340">A package referenced directly by a project will override dependency constraints from other packages.</span></span>   |
| <span data-ttu-id="a7054-341">**示例消息**</span><span class="sxs-lookup"><span data-stu-id="a7054-341">**Example message**</span></span> | <span data-ttu-id="a7054-342">*外部依赖关系约束的检测到的包版本： x 1.0.0 要求的 y （= 1.0.0），但版本 y 2.0.0 为已解决。*</span><span class="sxs-lookup"><span data-stu-id="a7054-342">*Detected package version outside of dependency constraint: x 1.0.0 requires y (= 1.0.0) but version y 2.0.0 was resolved.*</span></span> |

## <a name="package-fallback-warnings"></a><span data-ttu-id="a7054-343">包回退警告</span><span class="sxs-lookup"><span data-stu-id="a7054-343">Package fallback warnings</span></span>

### <a name="nu1701"></a><span data-ttu-id="a7054-344">NU1701</span><span class="sxs-lookup"><span data-stu-id="a7054-344">NU1701</span></span>

| | |
| --- | --- |
| <span data-ttu-id="a7054-345">**问题**</span><span class="sxs-lookup"><span data-stu-id="a7054-345">**Issue**</span></span> | <span data-ttu-id="a7054-346">*PackageTargetFallback/AssetTargetFallback*用于从包选择资产。</span><span class="sxs-lookup"><span data-stu-id="a7054-346">*PackageTargetFallback/AssetTargetFallback* was used to select assets from a package.</span></span> <span data-ttu-id="a7054-347">这是警告，以让用户知道资产可能不兼容的 100%。</span><span class="sxs-lookup"><span data-stu-id="a7054-347">This is a warning to let the user know that the assets may not be 100% compatible.</span></span> |
| <span data-ttu-id="a7054-348">**常见原因**</span><span class="sxs-lookup"><span data-stu-id="a7054-348">**Common causes**</span></span> | <span data-ttu-id="a7054-349">包不支持项目框架。</span><span class="sxs-lookup"><span data-stu-id="a7054-349">The package doesn't support the project framework.</span></span> |
| <span data-ttu-id="a7054-350">**示例消息**</span><span class="sxs-lookup"><span data-stu-id="a7054-350">**Example message**</span></span> | <span data-ttu-id="a7054-351">*包 NuGet.Versioning 已还原可移植 net45 + win8 改为使用项目目标框架 netstandard1.5。此程序包并不一定与你的项目完全兼容。*</span><span class="sxs-lookup"><span data-stu-id="a7054-351">*Package 'NuGet.Versioning' was restored using 'portable-net45+win8' instead the project target framework 'netstandard1.5'. This package may not be fully compatible with your project.*</span></span> |

## <a name="feed-warnings"></a><span data-ttu-id="a7054-352">源警告</span><span class="sxs-lookup"><span data-stu-id="a7054-352">Feed warnings</span></span>

### <a name="nu1801"></a><span data-ttu-id="a7054-353">NU1801</span><span class="sxs-lookup"><span data-stu-id="a7054-353">NU1801</span></span>

| | |
| --- | --- |
| <span data-ttu-id="a7054-354">**问题**</span><span class="sxs-lookup"><span data-stu-id="a7054-354">**Issue**</span></span> | <span data-ttu-id="a7054-355">读取源时出错时`IgnoreFailedSources`设置为 true，将其转换为非致命性警告。</span><span class="sxs-lookup"><span data-stu-id="a7054-355">An error occurred when reading the feed when `IgnoreFailedSources` is set to true, converting it to a non-fatal warning.</span></span> <span data-ttu-id="a7054-356">这可能包含的任何消息，并为泛型。</span><span class="sxs-lookup"><span data-stu-id="a7054-356">This could contain any message and is generic.</span></span> |
| <span data-ttu-id="a7054-357">**常见原因**</span><span class="sxs-lookup"><span data-stu-id="a7054-357">**Common causes**</span></span> | <span data-ttu-id="a7054-358">源无效。</span><span class="sxs-lookup"><span data-stu-id="a7054-358">The source is invalid.</span></span> |
| <span data-ttu-id="a7054-359">**示例消息**</span><span class="sxs-lookup"><span data-stu-id="a7054-359">**Example message**</span></span> | <span data-ttu-id="a7054-360">不可用</span><span class="sxs-lookup"><span data-stu-id="a7054-360">n/a</span></span> |

## <a name="nuget-internal-errors-and-warnings"></a><span data-ttu-id="a7054-361">NuGet 内部错误和警告</span><span class="sxs-lookup"><span data-stu-id="a7054-361">NuGet internal errors and warnings</span></span>

<span data-ttu-id="a7054-362">[NU1000](#nu1000) | [NU1500](#nu1500)</span><span class="sxs-lookup"><span data-stu-id="a7054-362">[NU1000](#nu1000) | [NU1500](#nu1500)</span></span>

### <a name="nu1000"></a><span data-ttu-id="a7054-363">NU1000</span><span class="sxs-lookup"><span data-stu-id="a7054-363">NU1000</span></span>

| | |
| --- | --- |
| <span data-ttu-id="a7054-364">**问题**</span><span class="sxs-lookup"><span data-stu-id="a7054-364">**Issue**</span></span> | <span data-ttu-id="a7054-365">从 NuGet 非特定的内部错误。</span><span class="sxs-lookup"><span data-stu-id="a7054-365">A non specific internal error from NuGet.</span></span> |
| <span data-ttu-id="a7054-366">**常见原因**</span><span class="sxs-lookup"><span data-stu-id="a7054-366">**Common causes**</span></span> | <span data-ttu-id="a7054-367">检查日志以了解更多信息</span><span class="sxs-lookup"><span data-stu-id="a7054-367">Check the logs for more information</span></span> |

### <a name="nu1500"></a><span data-ttu-id="a7054-368">NU1500</span><span class="sxs-lookup"><span data-stu-id="a7054-368">NU1500</span></span>

| | |
| --- | --- |
| <span data-ttu-id="a7054-369">**问题**</span><span class="sxs-lookup"><span data-stu-id="a7054-369">**Issue**</span></span> | <span data-ttu-id="a7054-370">从 NuGet 内部非特定警告。</span><span class="sxs-lookup"><span data-stu-id="a7054-370">A non specific internal warning from NuGet.</span></span> |
| <span data-ttu-id="a7054-371">**常见原因**</span><span class="sxs-lookup"><span data-stu-id="a7054-371">**Common causes**</span></span> | <span data-ttu-id="a7054-372">检查日志以了解更多信息</span><span class="sxs-lookup"><span data-stu-id="a7054-372">Check the logs for more information</span></span> |
