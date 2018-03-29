---
title: NuGet 错误和警告参考 |Microsoft 文档
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 03/06/2018
ms.topic: reference
ms.prod: nuget
ms.technology: ''
description: 针对警告和错误各种 NuGet 操作过程中从 NuGet 发出的完整参考。
keywords: NuGet 错误、 NuGet 警告诊断
ms.reviewer:
- anangaur
- karann-msft
- unniravindranathan
ms.workload:
- dotnet
- aspnet
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
ms.openlocfilehash: 020e31dc8646c43b86bcee555f1772e8b1db7761
ms.sourcegitcommit: beb229893559824e8abd6ab16707fd5fe1c6ac26
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/28/2018
---
# <a name="errors-and-warnings"></a><span data-ttu-id="8b877-104">错误和警告</span><span class="sxs-lookup"><span data-stu-id="8b877-104">Errors and warnings</span></span>

<span data-ttu-id="8b877-105">在 NuGet 4.3.0+ 错误和警告本主题中所述进行编号，并提供帮助您解决所涉及的问题详细的信息。</span><span class="sxs-lookup"><span data-stu-id="8b877-105">In NuGet 4.3.0+, errors and warnings are numbered as described in this topic and provide detailed information to help you address the issues involved.</span></span>

<span data-ttu-id="8b877-106">错误和警告在此处列出是仅适用于[PackageReference 基于](../consume-packages/package-references-in-project-files.md)项目和 NuGet 4.3.0+。</span><span class="sxs-lookup"><span data-stu-id="8b877-106">The errors and warnings listed here are available only with [PackageReference-based](../consume-packages/package-references-in-project-files.md) projects and NuGet 4.3.0+.</span></span> <span data-ttu-id="8b877-107">NuGet 也服从 MSBuild 属性，以禁止显示警告或将它们提升到错误。</span><span class="sxs-lookup"><span data-stu-id="8b877-107">NuGet also honors MSBuild properties to suppress warnings or elevate them to errors.</span></span> <span data-ttu-id="8b877-108">有关详细信息，请参阅[如何： 禁止显示编译器警告](/visualstudio/ide/how-to-suppress-compiler-warnings)Visual Studio 文档中。</span><span class="sxs-lookup"><span data-stu-id="8b877-108">For more information, see [How to: Suppress Compiler Warnings](/visualstudio/ide/how-to-suppress-compiler-warnings) in the Visual Studio documentation.</span></span>

<span data-ttu-id="8b877-109">**错误**</span><span class="sxs-lookup"><span data-stu-id="8b877-109">**Errors**</span></span>

| <span data-ttu-id="8b877-110">Group</span><span class="sxs-lookup"><span data-stu-id="8b877-110">Group</span></span> | <span data-ttu-id="8b877-111">错误号</span><span class="sxs-lookup"><span data-stu-id="8b877-111">Error Numbers</span></span> |
| --- | --- |
| [<span data-ttu-id="8b877-112">无效的输入的错误</span><span class="sxs-lookup"><span data-stu-id="8b877-112">Invalid input errors</span></span>](#invalid-input-errors) | <span data-ttu-id="8b877-113">[NU1001](#nu1001), [NU1002](#nu1002), [NU1003](#nu1003)</span><span class="sxs-lookup"><span data-stu-id="8b877-113">[NU1001](#nu1001), [NU1002](#nu1002), [NU1003](#nu1003)</span></span> |
| [<span data-ttu-id="8b877-114">缺少的包和项目错误</span><span class="sxs-lookup"><span data-stu-id="8b877-114">Missing package and project errors</span></span>](#missing-package-and-project-errors) | <span data-ttu-id="8b877-115">[NU1100](#nu1100)， [NU1101](#nu1101)， [NU1102](#nu1102)， [NU1103](#nu1103)， [NU1104](#nu1104)， [NU1105](#nu1105)， [NU1106](#nu1106)， [NU1107](#nu1107) (以前 NU1607) [NU1108](#nu1108) (以前 NU1606)</span><span class="sxs-lookup"><span data-stu-id="8b877-115">[NU1100](#nu1100), [NU1101](#nu1101), [NU1102](#nu1102), [NU1103](#nu1103), [NU1104](#nu1104), [NU1105](#nu1105), [NU1106](#nu1106), [NU1107](#nu1107) (previously NU1607), [NU1108](#nu1108) (previously NU1606)</span></span> |
| [<span data-ttu-id="8b877-116">兼容性错误</span><span class="sxs-lookup"><span data-stu-id="8b877-116">Compatibility errors</span></span>](#compatibility-errors) | <span data-ttu-id="8b877-117">[NU1201](#nu1201), [NU1202](#nu1202), [NU1203](#nu1203), [NU1401](#nu1401)</span><span class="sxs-lookup"><span data-stu-id="8b877-117">[NU1201](#nu1201), [NU1202](#nu1202), [NU1203](#nu1203), [NU1401](#nu1401)</span></span> |

<span data-ttu-id="8b877-118">**警告**</span><span class="sxs-lookup"><span data-stu-id="8b877-118">**Warnings**</span></span>

| <span data-ttu-id="8b877-119">Group</span><span class="sxs-lookup"><span data-stu-id="8b877-119">Group</span></span> | <span data-ttu-id="8b877-120">警告编号</span><span class="sxs-lookup"><span data-stu-id="8b877-120">Warning numbers</span></span> |
| --- | --- |
| [<span data-ttu-id="8b877-121">无效的输入的警告</span><span class="sxs-lookup"><span data-stu-id="8b877-121">Invalid input warnings</span></span>](#invalid-input-warnings) | <span data-ttu-id="8b877-122">[NU1501](#nu1501)， [NU1502](#nu1502)， [NU1503](#nu1503)</span><span class="sxs-lookup"><span data-stu-id="8b877-122">[NU1501](#nu1501), [NU1502](#nu1502), [NU1503](#nu1503)</span></span> |
| [<span data-ttu-id="8b877-123">意外的包版本警告</span><span class="sxs-lookup"><span data-stu-id="8b877-123">Unexpected package version warnings</span></span>](#unexpected-package-version-warnings) | <span data-ttu-id="8b877-124">[NU1601](#nu1601)， [NU1602](#nu1602)， [NU1603](#nu1603)， [NU1604](#nu1604)， [NU1605](#nu1605)</span><span class="sxs-lookup"><span data-stu-id="8b877-124">[NU1601](#nu1601), [NU1602](#nu1602), [NU1603](#nu1603), [NU1604](#nu1604), [NU1605](#nu1605)</span></span> |
| [<span data-ttu-id="8b877-125">冲突解决程序冲突警告</span><span class="sxs-lookup"><span data-stu-id="8b877-125">Resolver conflict warnings</span></span>](#resolver-conflict-warnings) | [<span data-ttu-id="8b877-126">NU1608</span><span class="sxs-lookup"><span data-stu-id="8b877-126">NU1608</span></span>](#nu1608) |
| [<span data-ttu-id="8b877-127">包回退警告</span><span class="sxs-lookup"><span data-stu-id="8b877-127">Package fallback warnings</span></span>](#package-fallback-warnings) | [<span data-ttu-id="8b877-128">NU1701</span><span class="sxs-lookup"><span data-stu-id="8b877-128">NU1701</span></span>](#nu1701) |
| [<span data-ttu-id="8b877-129">源警告</span><span class="sxs-lookup"><span data-stu-id="8b877-129">Feed warnings</span></span>](#feed-warnings) | [<span data-ttu-id="8b877-130">NU1801</span><span class="sxs-lookup"><span data-stu-id="8b877-130">NU1801</span></span>](#nu1801) |
| [<span data-ttu-id="8b877-131">NuGet 内部错误和警告</span><span class="sxs-lookup"><span data-stu-id="8b877-131">NuGet internal errors and warnings</span></span>](#nuget-internal-errors-and-warnings) | <span data-ttu-id="8b877-132">[NU1000](#nu1000), [NU1500](#nu1500)</span><span class="sxs-lookup"><span data-stu-id="8b877-132">[NU1000](#nu1000), [NU1500](#nu1500)</span></span> |
| [<span data-ttu-id="8b877-133">已签名的软件包 （创建和验证）</span><span class="sxs-lookup"><span data-stu-id="8b877-133">Signed packages (creation and verification)</span></span>](#signed-packages-creation-and-verification)| <span data-ttu-id="8b877-134">[NU3000](#nu3000), [NU3001](#nu3001), [NU3002](#nu3002), [NU3004](#nu3004), [NU3008](#nu3008), [NU3018](#nu3018), [NU3028](#nu3028)</span><span class="sxs-lookup"><span data-stu-id="8b877-134">[NU3000](#nu3000), [NU3001](#nu3001), [NU3002](#nu3002), [NU3004](#nu3004), [NU3008](#nu3008), [NU3018](#nu3018), [NU3028](#nu3028)</span></span> |

## <a name="invalid-input-errors"></a><span data-ttu-id="8b877-135">无效的输入的错误</span><span class="sxs-lookup"><span data-stu-id="8b877-135">Invalid input errors</span></span>

<span data-ttu-id="8b877-136">[NU1001](#nu1001) | [NU1002](#nu1002) | [NU1003](#nu1003)</span><span class="sxs-lookup"><span data-stu-id="8b877-136">[NU1001](#nu1001) | [NU1002](#nu1002) | [NU1003](#nu1003)</span></span>

### <a name="nu1001"></a><span data-ttu-id="8b877-137">NU1001</span><span class="sxs-lookup"><span data-stu-id="8b877-137">NU1001</span></span>

| | |
| --- | --- |
| <span data-ttu-id="8b877-138">**问题**</span><span class="sxs-lookup"><span data-stu-id="8b877-138">**Issue**</span></span> | <span data-ttu-id="8b877-139">项目不包含一个或多个框架。</span><span class="sxs-lookup"><span data-stu-id="8b877-139">The project doesn't contain one or more frameworks.</span></span> |
| <span data-ttu-id="8b877-140">**示例消息**</span><span class="sxs-lookup"><span data-stu-id="8b877-140">**Example message**</span></span> | <span data-ttu-id="8b877-141">*项目 projA c:\tmp\projA.csproj 中未指定任何目标框架*</span><span class="sxs-lookup"><span data-stu-id="8b877-141">*The project projA does not specify any target frameworks in c:\tmp\projA.csproj*</span></span> |
| <span data-ttu-id="8b877-142">**解决方案**</span><span class="sxs-lookup"><span data-stu-id="8b877-142">**Solution**</span></span> | <span data-ttu-id="8b877-143">添加`TargetFramework`或`TargetFrameworks`属性设置为指定的项目文件。</span><span class="sxs-lookup"><span data-stu-id="8b877-143">Add a `TargetFramework` or `TargetFrameworks` property to the specified project file.</span></span> |

### <a name="nu1002"></a><span data-ttu-id="8b877-144">NU1002</span><span class="sxs-lookup"><span data-stu-id="8b877-144">NU1002</span></span>

| | |
| --- | --- |
| <span data-ttu-id="8b877-145">**问题**</span><span class="sxs-lookup"><span data-stu-id="8b877-145">**Issue**</span></span> | <span data-ttu-id="8b877-146">无效的输入以及清除关键字的组合。</span><span class="sxs-lookup"><span data-stu-id="8b877-146">Invalid combination of inputs along with a CLEAR keyword.</span></span> |
| <span data-ttu-id="8b877-147">**示例消息**</span><span class="sxs-lookup"><span data-stu-id="8b877-147">**Example message**</span></span> | <span data-ttu-id="8b877-148">*清除不能在与其他值一起使用*</span><span class="sxs-lookup"><span data-stu-id="8b877-148">*'CLEAR' cannot be used in conjunction with other values*</span></span> |
| <span data-ttu-id="8b877-149">**解决方案**</span><span class="sxs-lookup"><span data-stu-id="8b877-149">**Solution**</span></span> | <span data-ttu-id="8b877-150">清除自行使用，而忽略所有其他输入。</span><span class="sxs-lookup"><span data-stu-id="8b877-150">Use CLEAR by itself and omit all other inputs.</span></span> |

### <a name="nu1003"></a><span data-ttu-id="8b877-151">NU1003</span><span class="sxs-lookup"><span data-stu-id="8b877-151">NU1003</span></span>

| | |
| --- | --- |
| <span data-ttu-id="8b877-152">**问题**</span><span class="sxs-lookup"><span data-stu-id="8b877-152">**Issue**</span></span> | <span data-ttu-id="8b877-153">`PackageTargetFallback` 和`AssetTargetFallback`用于选择资产提供不同的行为和不能一起使用。</span><span class="sxs-lookup"><span data-stu-id="8b877-153">`PackageTargetFallback` and `AssetTargetFallback` provide different behavior for selecting assets and cannot be used together.</span></span> |
| <span data-ttu-id="8b877-154">**示例消息**</span><span class="sxs-lookup"><span data-stu-id="8b877-154">**Example message**</span></span> | <span data-ttu-id="8b877-155">*PackageTargetFallback 和 AssetTargetFallback 不能一起使用。从项目环境删除 PackageTargetFallback(deprecated) 的引用。*</span><span class="sxs-lookup"><span data-stu-id="8b877-155">*PackageTargetFallback and AssetTargetFallback cannot be used together. Remove PackageTargetFallback(deprecated) references from the project environment.*</span></span> |
| <span data-ttu-id="8b877-156">**解决方案**</span><span class="sxs-lookup"><span data-stu-id="8b877-156">**Solution**</span></span> | <span data-ttu-id="8b877-157">删除不推荐使用`PackageTargetFallback`从项目的元素。</span><span class="sxs-lookup"><span data-stu-id="8b877-157">Remove the deprecated `PackageTargetFallback` element from the project.</span></span> |

## <a name="missing-package-and-project-errors"></a><span data-ttu-id="8b877-158">缺少的包和项目错误</span><span class="sxs-lookup"><span data-stu-id="8b877-158">Missing package and project errors</span></span>

<span data-ttu-id="8b877-159">[NU1100](#nu1100) | [NU1101](#nu1101) | [NU1102](#nu1102) | [NU1103](#nu1103) | [NU1104](#nu1104) | [NU1105](#nu1105) | [NU1106](#nu1106)</span><span class="sxs-lookup"><span data-stu-id="8b877-159">[NU1100](#nu1100) | [NU1101](#nu1101) | [NU1102](#nu1102) | [NU1103](#nu1103) | [NU1104](#nu1104) | [NU1105](#nu1105) | [NU1106](#nu1106)</span></span>

### <a name="nu1100"></a><span data-ttu-id="8b877-160">NU1100</span><span class="sxs-lookup"><span data-stu-id="8b877-160">NU1100</span></span>

| | |
| --- | --- |
| <span data-ttu-id="8b877-161">**问题**</span><span class="sxs-lookup"><span data-stu-id="8b877-161">**Issue**</span></span> | <span data-ttu-id="8b877-162">依赖关系组不被解析。</span><span class="sxs-lookup"><span data-stu-id="8b877-162">A dependency group not be resolved.</span></span> <span data-ttu-id="8b877-163">这是一个泛型类型不是包或项目的问题。</span><span class="sxs-lookup"><span data-stu-id="8b877-163">This is a generic issue for types that are not packages or projects.</span></span> |
| <span data-ttu-id="8b877-164">**示例消息**</span><span class="sxs-lookup"><span data-stu-id="8b877-164">**Example message**</span></span> | <span data-ttu-id="8b877-165">*无法解析 net45 System.Missing*</span><span class="sxs-lookup"><span data-stu-id="8b877-165">*Unable to resolve System.Missing for net45*</span></span> |
| <span data-ttu-id="8b877-166">**解决方案**</span><span class="sxs-lookup"><span data-stu-id="8b877-166">**Solution**</span></span> | <span data-ttu-id="8b877-167">打开项目文件并检查其依赖项列表。</span><span class="sxs-lookup"><span data-stu-id="8b877-167">Open the project file and examine the list of its dependencies.</span></span> <span data-ttu-id="8b877-168">检查在你使用的包源上存在每个依赖关系和包支持项目的目标框架。</span><span class="sxs-lookup"><span data-stu-id="8b877-168">Check that each dependency exists on the package sources you're using, and that the package supports the project's target framework.</span></span> |

### <a name="nu1101"></a><span data-ttu-id="8b877-169">NU1101</span><span class="sxs-lookup"><span data-stu-id="8b877-169">NU1101</span></span>

| | |
| --- | --- |
| <span data-ttu-id="8b877-170">**问题**</span><span class="sxs-lookup"><span data-stu-id="8b877-170">**Issue**</span></span> | <span data-ttu-id="8b877-171">在任何源上找不到包。</span><span class="sxs-lookup"><span data-stu-id="8b877-171">The package cannot be found on any sources.</span></span> |
| <span data-ttu-id="8b877-172">**示例消息**</span><span class="sxs-lookup"><span data-stu-id="8b877-172">**Example message**</span></span> | <span data-ttu-id="8b877-173">*找不到程序包 System.Missing。具有此 id 在源中存在的任何包： dotnet 核心、 dotnet roslyn、 nuget.org*</span><span class="sxs-lookup"><span data-stu-id="8b877-173">*Unable to find package System.Missing. No packages exist with this id in source(s): dotnet-core, dotnet-roslyn, nuget.org*</span></span> |
| <span data-ttu-id="8b877-174">**解决方案**</span><span class="sxs-lookup"><span data-stu-id="8b877-174">**Solution**</span></span> | <span data-ttu-id="8b877-175">检查以确保使用正确的包标识符和版本号数目的 Visual Studio 中的项目的依赖关系。</span><span class="sxs-lookup"><span data-stu-id="8b877-175">Examine the project's dependencies in Visual Studio to be sure you're using the correct package identifier and version number.</span></span> <span data-ttu-id="8b877-176">此外检查[NuGet 配置](../consume-packages/Configuring-NuGet-Behavior.md)标识的包源你希望使用。</span><span class="sxs-lookup"><span data-stu-id="8b877-176">Also check that the [NuGet configuration](../consume-packages/Configuring-NuGet-Behavior.md) identifies the package sources your expect to be using.</span></span> <span data-ttu-id="8b877-177">如果你使用具有的包[语义版本控制 2.0.0](https://docs.microsoft.com/en-us/nuget/reference/package-versioning#semantic-versioning-200)，请确保你正在使用[V3 源](https://api.nuget.org/v3/index.json)中[NuGet 配置](../consume-packages/Configuring-NuGet-Behavior.md)。</span><span class="sxs-lookup"><span data-stu-id="8b877-177">If you use packages that have [Semantic Versioning 2.0.0](https://docs.microsoft.com/en-us/nuget/reference/package-versioning#semantic-versioning-200), please make sure that you are using the [V3 feed](https://api.nuget.org/v3/index.json) in the [NuGet configuration](../consume-packages/Configuring-NuGet-Behavior.md).</span></span> |

### <a name="nu1102"></a><span data-ttu-id="8b877-178">NU1102</span><span class="sxs-lookup"><span data-stu-id="8b877-178">NU1102</span></span>

| | |
| --- | --- |
| <span data-ttu-id="8b877-179">**问题**</span><span class="sxs-lookup"><span data-stu-id="8b877-179">**Issue**</span></span> | <span data-ttu-id="8b877-180">找到的包标识符，但在任何源上找不到指定的依赖范围内的版本。</span><span class="sxs-lookup"><span data-stu-id="8b877-180">The package identifier is found but a version within the specified dependency range cannot be found on any of the sources.</span></span> <span data-ttu-id="8b877-181">可能由包和不是用户指定的范围。</span><span class="sxs-lookup"><span data-stu-id="8b877-181">The range might be specified by a package and not the user.</span></span> |
| <span data-ttu-id="8b877-182">**示例消息**</span><span class="sxs-lookup"><span data-stu-id="8b877-182">**Example message**</span></span> | <span data-ttu-id="8b877-183">*找不到版本包 NuGet.Versioning (> = 9.0.1)<br/> -于 nuget.org 中的找到 30 版本 [最接近的版本： 4.0.0]<br/> -dotnet buildtools 中找到的 10 版本 [最接近的版本： 4.0.0-rc-2129]<br/> -找到 9在 NuGetVolatile 版本 [最接近的版本： 3.0.0-beta-00032]<br/> -0 版本位于 dotnet 核心<br/>-0 版本位于 dotnet roslyn*</span><span class="sxs-lookup"><span data-stu-id="8b877-183">*Unable to find package NuGet.Versioning with version (>= 9.0.1)<br/>  - Found 30 version(s) in nuget.org [ Nearest version: 4.0.0 ]<br/>  - Found 10 version(s) in dotnet-buildtools [ Nearest version: 4.0.0-rc-2129 ]<br/>  - Found 9 version(s) in NuGetVolatile [ Nearest version: 3.0.0-beta-00032 ]<br/>  - Found 0 version(s) in dotnet-core<br/>  - Found 0 version(s) in dotnet-roslyn*</span></span> |
| <span data-ttu-id="8b877-184">**解决方案**</span><span class="sxs-lookup"><span data-stu-id="8b877-184">**Solution**</span></span> | <span data-ttu-id="8b877-185">编辑项目文件以更正包版本。</span><span class="sxs-lookup"><span data-stu-id="8b877-185">Edit the project file to correct the package version.</span></span> <span data-ttu-id="8b877-186">此外检查[NuGet 配置](../consume-packages/Configuring-NuGet-Behavior.md)标识的包源你希望使用。</span><span class="sxs-lookup"><span data-stu-id="8b877-186">Also check that the [NuGet configuration](../consume-packages/Configuring-NuGet-Behavior.md) identifies the package sources your expect to be using.</span></span> <span data-ttu-id="8b877-187">你可能需要更改 requeted 版本，如果此包被直接引用该项目。</span><span class="sxs-lookup"><span data-stu-id="8b877-187">You may need to change the requeted version if this package is referenced by the project directly.</span></span> |

### <a name="nu1103"></a><span data-ttu-id="8b877-188">NU1103</span><span class="sxs-lookup"><span data-stu-id="8b877-188">NU1103</span></span>

| | |
| --- | --- |
| <span data-ttu-id="8b877-189">**问题**</span><span class="sxs-lookup"><span data-stu-id="8b877-189">**Issue**</span></span> | <span data-ttu-id="8b877-190">项目指定了依赖项的范围，稳定版本，但不稳定版本找该范围内。</span><span class="sxs-lookup"><span data-stu-id="8b877-190">The project specified a stable version for the dependency range, but no stable versions were found in that range.</span></span> <span data-ttu-id="8b877-191">预发行版本未找到，但不是允许。</span><span class="sxs-lookup"><span data-stu-id="8b877-191">Pre-release versions were found but are not allowed.</span></span> |
| <span data-ttu-id="8b877-192">**示例消息**</span><span class="sxs-lookup"><span data-stu-id="8b877-192">**Example message**</span></span> | <span data-ttu-id="8b877-193">*找不到稳定的包 NuGet.Versioning 随版本 (> = 3.0.0)<br/> -dotnet buildtools 中找到的 10 版本 [最接近的版本： 4.0.0-rc-2129]<br/> -NuGetVolatile 中的找到 9 版本 [最接近的版本： 3.0.0-beta-00032]<br/> -0 版本位于 dotnet 核心<br/>-0 版本位于 dotnet roslyn*</span><span class="sxs-lookup"><span data-stu-id="8b877-193">*Unable to find a stable package NuGet.Versioning with version (>= 3.0.0)<br/>  - Found 10 version(s) in dotnet-buildtools [ Nearest version: 4.0.0-rc-2129 ]<br/>  - Found 9 version(s) in NuGetVolatile [ Nearest version: 3.0.0-beta-00032 ]<br/>  - Found 0 version(s) in dotnet-core<br/>  - Found 0 version(s) in dotnet-roslyn*</span></span> |
| <span data-ttu-id="8b877-194">**解决方案**</span><span class="sxs-lookup"><span data-stu-id="8b877-194">**Solution**</span></span> |  <span data-ttu-id="8b877-195">编辑项目文件以包括预发行版本中的版本范围。</span><span class="sxs-lookup"><span data-stu-id="8b877-195">Edit the version range in the project file to include pre-release versions.</span></span> <span data-ttu-id="8b877-196">请参阅[包版本控制](../reference/Package-Versioning.md)。</span><span class="sxs-lookup"><span data-stu-id="8b877-196">See [Package versioning](../reference/Package-Versioning.md).</span></span> |

### <a name="nu1104"></a><span data-ttu-id="8b877-197">NU1104</span><span class="sxs-lookup"><span data-stu-id="8b877-197">NU1104</span></span>

| | |
| --- | --- |
| <span data-ttu-id="8b877-198">**问题**</span><span class="sxs-lookup"><span data-stu-id="8b877-198">**Issue**</span></span> | <span data-ttu-id="8b877-199">ProjectReference 指向不存在的文件。</span><span class="sxs-lookup"><span data-stu-id="8b877-199">A ProjectReference points to a file that doesn't exist.</span></span> |
| <span data-ttu-id="8b877-200">**示例消息**</span><span class="sxs-lookup"><span data-stu-id="8b877-200">**Example message**</span></span> | <span data-ttu-id="8b877-201">*项目引用不存在 c:\a.csproj。检查项目引用有效以及项目文件是否存在。*</span><span class="sxs-lookup"><span data-stu-id="8b877-201">*Project reference does not exist 'c:\a.csproj'. Check that the project reference is valid and that the project file exists.*</span></span> |
| <span data-ttu-id="8b877-202">**解决方案**</span><span class="sxs-lookup"><span data-stu-id="8b877-202">**Solution**</span></span> | <span data-ttu-id="8b877-203">编辑项目文件以更正引用的项目的路径，或若要删除的引用一起删除，如果不再需要。</span><span class="sxs-lookup"><span data-stu-id="8b877-203">Edit the project file to either correct the path to the referenced project or to remove the reference altogether if it's no longer needed.</span></span> |

### <a name="nu1105"></a><span data-ttu-id="8b877-204">NU1105</span><span class="sxs-lookup"><span data-stu-id="8b877-204">NU1105</span></span>

| | |
| --- | --- |
| <span data-ttu-id="8b877-205">**问题**</span><span class="sxs-lookup"><span data-stu-id="8b877-205">**Issue**</span></span> | <span data-ttu-id="8b877-206">项目文件存在，但不还原信息已为其提供。</span><span class="sxs-lookup"><span data-stu-id="8b877-206">The project file exists but no restore information was provided for it.</span></span> |
| <span data-ttu-id="8b877-207">**示例消息**</span><span class="sxs-lookup"><span data-stu-id="8b877-207">**Example message**</span></span> | <span data-ttu-id="8b877-208">*无法读取 c:\a.csproj 的项目信息。项目文件可能无效或缺少所需的还原的目标。*</span><span class="sxs-lookup"><span data-stu-id="8b877-208">*Unable to read project information for 'c:\a.csproj'. The project file may be invalid or missing targets required for restore.*</span></span> |
| <span data-ttu-id="8b877-209">**解决方案**</span><span class="sxs-lookup"><span data-stu-id="8b877-209">**Solution**</span></span> | <span data-ttu-id="8b877-210">在 Visual Studio 中，该错误可能意味着该项目已卸载，在这种情况下重新加载项目。</span><span class="sxs-lookup"><span data-stu-id="8b877-210">In Visual Studio, the error could mean that the project is unloaded, in which case reload the project.</span></span> <span data-ttu-id="8b877-211">从命令行这可能表示该文件已损坏或，它不包含"之后导入"自定义所需的还原，以便读取项目的目标。</span><span class="sxs-lookup"><span data-stu-id="8b877-211">From the command line this could mean that the file is corrupt or that it doesn't contain the custom "after imports" target needed for restore to read the project.</span></span> <span data-ttu-id="8b877-212">检查项目文件有效以及包含"之后导入"目标。</span><span class="sxs-lookup"><span data-stu-id="8b877-212">Check that the project file is valid and contains an "after imports" target.</span></span> |

### <a name="nu1106"></a><span data-ttu-id="8b877-213">NU1106</span><span class="sxs-lookup"><span data-stu-id="8b877-213">NU1106</span></span>

| | |
| --- | --- |
| <span data-ttu-id="8b877-214">**问题**</span><span class="sxs-lookup"><span data-stu-id="8b877-214">**Issue**</span></span> | <span data-ttu-id="8b877-215">无法解析依赖项约束。</span><span class="sxs-lookup"><span data-stu-id="8b877-215">Dependency constraints cannot be resolved.</span></span> |
| <span data-ttu-id="8b877-216">**示例消息**</span><span class="sxs-lookup"><span data-stu-id="8b877-216">**Example message**</span></span> | <span data-ttu-id="8b877-217">*无法满足 {id} 互相冲突的请求: {冲突路径} Framework: {目标关系图}*</span><span class="sxs-lookup"><span data-stu-id="8b877-217">*Unable to satisfy conflicting requests for {id}: {conflict path} Framework: {target graph}*</span></span> |
| <span data-ttu-id="8b877-218">**解决方案**</span><span class="sxs-lookup"><span data-stu-id="8b877-218">**Solution**</span></span> | <span data-ttu-id="8b877-219">编辑项目文件以指定的依赖项而不是准确的版本更自由范围。</span><span class="sxs-lookup"><span data-stu-id="8b877-219">Edit the project file to specify more open-ended ranges for the dependency rather than an exact version.</span></span> |
|

<a name="nu1107"></a>

### <a name="nu1107-previously-nu1607"></a><span data-ttu-id="8b877-220">NU1107 (以前 NU1607)</span><span class="sxs-lookup"><span data-stu-id="8b877-220">NU1107 (Previously NU1607)</span></span>

| | |
| --- | --- |
| <span data-ttu-id="8b877-221">**问题**</span><span class="sxs-lookup"><span data-stu-id="8b877-221">**Issue**</span></span> | <span data-ttu-id="8b877-222">无法解析包之间的依赖关系约束。</span><span class="sxs-lookup"><span data-stu-id="8b877-222">Unable to resolve dependency constraints between packages.</span></span> |
| <span data-ttu-id="8b877-223">**示例消息**</span><span class="sxs-lookup"><span data-stu-id="8b877-223">**Example message**</span></span> | <span data-ttu-id="8b877-224">*NuGet.Versioning 检测到的版本冲突。若要解决此问题的项目中直接引用包。<br/>NuGet.Packaging 3.5.0-> （= 3.5.0） NuGet.Versioning<br/> NuGet.Configuration 4.0.0-> 的 NuGet.Versioning （= 4.0.0）*</span><span class="sxs-lookup"><span data-stu-id="8b877-224">*Version conflict detected for NuGet.Versioning. Reference the package directly from the project to resolve this issue.<br/>  NuGet.Packaging 3.5.0 -> NuGet.Versioning (= 3.5.0)<br/>  NuGet.Configuration 4.0.0 -> NuGet.Versioning (= 4.0.0)*</span></span> |
| <span data-ttu-id="8b877-225">**解决方案**</span><span class="sxs-lookup"><span data-stu-id="8b877-225">**Solution**</span></span> | <span data-ttu-id="8b877-226">依赖项与上的约束的确切版本的包不允许其他包以根据需要增大版本号。</span><span class="sxs-lookup"><span data-stu-id="8b877-226">Packages with dependency constraints on exact versions do not allow other packages to increase the version if needed.</span></span> <span data-ttu-id="8b877-227">添加具有所需的确切版本对直接 （在项目文件中） 项目的引用。</span><span class="sxs-lookup"><span data-stu-id="8b877-227">Add a reference to the project directly (in the project file) with the exact version required.</span></span> |

<a name="nu1108"></a>

### <a name="nu1108-previously-nu1606"></a><span data-ttu-id="8b877-228">NU1108 (以前 NU1606)</span><span class="sxs-lookup"><span data-stu-id="8b877-228">NU1108 (Previously NU1606)</span></span>

| | |
| --- | --- |
| <span data-ttu-id="8b877-229">**问题**</span><span class="sxs-lookup"><span data-stu-id="8b877-229">**Issue**</span></span> | <span data-ttu-id="8b877-230">检测到循环依赖关系。</span><span class="sxs-lookup"><span data-stu-id="8b877-230">A circular dependency was detected.</span></span> |
| <span data-ttu-id="8b877-231">**示例消息**</span><span class="sxs-lookup"><span data-stu-id="8b877-231">**Example message**</span></span> | <span data-ttu-id="8b877-232">*检测到循环： A-> B-> A*</span><span class="sxs-lookup"><span data-stu-id="8b877-232">*Cycle detected: A -> B -> A*</span></span> |
| <span data-ttu-id="8b877-233">**解决方案**</span><span class="sxs-lookup"><span data-stu-id="8b877-233">**Solution**</span></span> | <span data-ttu-id="8b877-234">不正确; 创作包请与联系软件包所有者以更正 bug。</span><span class="sxs-lookup"><span data-stu-id="8b877-234">The package is authored incorrectly; contact the package owner to correct the bug.</span></span> |

## <a name="compatibility-errors"></a><span data-ttu-id="8b877-235">兼容性错误</span><span class="sxs-lookup"><span data-stu-id="8b877-235">Compatibility errors</span></span>

<span data-ttu-id="8b877-236">[NU1201](#nu1201) | [NU1202](#nu1202) | [NU1203](#nu1203) | [NU1401](#nu1401)</span><span class="sxs-lookup"><span data-stu-id="8b877-236">[NU1201](#nu1201) | [NU1202](#nu1202) | [NU1203](#nu1203) | [NU1401](#nu1401)</span></span>

### <a name="nu1201"></a><span data-ttu-id="8b877-237">NU1201</span><span class="sxs-lookup"><span data-stu-id="8b877-237">NU1201</span></span>

| | |
| --- | --- |
| <span data-ttu-id="8b877-238">**问题**</span><span class="sxs-lookup"><span data-stu-id="8b877-238">**Issue**</span></span> | <span data-ttu-id="8b877-239">依赖项项目不包含与当前项目兼容的框架。</span><span class="sxs-lookup"><span data-stu-id="8b877-239">A dependency project doesn't contain a framework compatible with the current project.</span></span> <span data-ttu-id="8b877-240">通常情况下，项目的目标框架是比使用项目的更高版本。</span><span class="sxs-lookup"><span data-stu-id="8b877-240">Typically, the project's target framework is a higher version than the consuming project.</span></span> |
| <span data-ttu-id="8b877-241">**示例消息**</span><span class="sxs-lookup"><span data-stu-id="8b877-241">**Example message**</span></span> | <span data-ttu-id="8b877-242">*项目 ServerWeb 与不兼容 netstandard1.3 (。NETStandard，Version = v1.3)。项目 ServerWeb 支持：<br/> -netstandard1.6 (。NETStandard，Version = v1.6)<br/> -netcoreapp1.0 (。NETCoreApp，Version = v1.0)*</span><span class="sxs-lookup"><span data-stu-id="8b877-242">*Project ServerWeb is not compatible with netstandard1.3 (.NETStandard,Version=v1.3). Project ServerWeb supports:<br/>  - netstandard1.6 (.NETStandard,Version=v1.6)<br/>  - netcoreapp1.0 (.NETCoreApp,Version=v1.0)*</span></span> |
| <span data-ttu-id="8b877-243">**解决方案**</span><span class="sxs-lookup"><span data-stu-id="8b877-243">**Solution**</span></span> | <span data-ttu-id="8b877-244">将项目的目标框架更改为使用项目的相等或更低版本。</span><span class="sxs-lookup"><span data-stu-id="8b877-244">Change the project's target framework to an equal or lower version than the consuming project.</span></span> |

### <a name="nu1202"></a><span data-ttu-id="8b877-245">NU1202</span><span class="sxs-lookup"><span data-stu-id="8b877-245">NU1202</span></span>

| | |
| --- | --- |
| <span data-ttu-id="8b877-246">**问题**</span><span class="sxs-lookup"><span data-stu-id="8b877-246">**Issue**</span></span> | <span data-ttu-id="8b877-247">依赖项包不包含任何与项目兼容的资产。</span><span class="sxs-lookup"><span data-stu-id="8b877-247">A dependency package doesn't contain any assets compatible with the project.</span></span> |
| <span data-ttu-id="8b877-248">**示例消息**</span><span class="sxs-lookup"><span data-stu-id="8b877-248">**Example message**</span></span> | <span data-ttu-id="8b877-249">*包 System.ComponentModel.EventBasedAsync 4.0.11 与不兼容 netstandard1.3 (。NETStandard，Version = v1.3)。打包 System.ComponentModel.EventBasedAsync 4.0.11 支持：<br/> -monoandroid10 (MonoAndroid，Version = v1.0)<br/> -monotouch10 (MonoTouch，Version = v1.0)<br/> -net45 (。NETFramework，Version = v4.5)<br/> -netcore50 (。NETCore，Version = 5.0 版)<br/> -netstandard1.0 (。NETStandard，Version = v1.0)<br/> -可移植 net45 + win8 + wp8 + wpa81 (。NETPortable，Version = v0.0，配置文件 = Profile259)<br/> -win8 (Windows、 版本 = v8.0)<br/> -wp8 (WindowsPhone，Version = v8.0)<br/> -wpa81 (WindowsPhoneApp，Version = v8.1)<br/> -xamarinios10 (Xamarin.iOS,Version=v1.0)<br/> -xamarinmac20 (Xamarin.Mac,Version=v2.0)<br/> -xamarintvos10 (Xamarin.TVOS,Version=v1.0)<br/> -xamarinwatchos10 (Xamarin.WatchOS,Version=v1.0)*</span><span class="sxs-lookup"><span data-stu-id="8b877-249">*Package System.ComponentModel.EventBasedAsync 4.0.11 is not compatible with netstandard1.3 (.NETStandard,Version=v1.3). Package System.ComponentModel.EventBasedAsync 4.0.11 supports:<br/>  - monoandroid10 (MonoAndroid,Version=v1.0)<br/>  - monotouch10 (MonoTouch,Version=v1.0)<br/>  - net45 (.NETFramework,Version=v4.5)<br/>  - netcore50 (.NETCore,Version=v5.0)<br/>  - netstandard1.0 (.NETStandard,Version=v1.0)<br/>  - portable-net45+win8+wp8+wpa81 (.NETPortable,Version=v0.0,Profile=Profile259)<br/>  - win8 (Windows,Version=v8.0)<br/>  - wp8 (WindowsPhone,Version=v8.0)<br/>  - wpa81 (WindowsPhoneApp,Version=v8.1)<br/>  - xamarinios10 (Xamarin.iOS,Version=v1.0)<br/>  - xamarinmac20 (Xamarin.Mac,Version=v2.0)<br/>  - xamarintvos10 (Xamarin.TVOS,Version=v1.0)<br/>  - xamarinwatchos10 (Xamarin.WatchOS,Version=v1.0)*</span></span>|
| <span data-ttu-id="8b877-250">**解决方案**</span><span class="sxs-lookup"><span data-stu-id="8b877-250">**Solution**</span></span> | <span data-ttu-id="8b877-251">将项目的目标框架更改为另一个包支持。</span><span class="sxs-lookup"><span data-stu-id="8b877-251">Change the project's target framework to one that the package supports.</span></span> |

### <a name="nu1203"></a><span data-ttu-id="8b877-252">NU1203</span><span class="sxs-lookup"><span data-stu-id="8b877-252">NU1203</span></span>

| | |
| --- | --- |
| <span data-ttu-id="8b877-253">**问题**</span><span class="sxs-lookup"><span data-stu-id="8b877-253">**Issue**</span></span> | <span data-ttu-id="8b877-254">包不支持项目的`RuntimeIdentifier`。</span><span class="sxs-lookup"><span data-stu-id="8b877-254">The package doesn't support the project's `RuntimeIdentifier`.</span></span> |
| <span data-ttu-id="8b877-255">**示例消息**</span><span class="sxs-lookup"><span data-stu-id="8b877-255">**Example message**</span></span> | <span data-ttu-id="8b877-256">*System.Example 1.0.0 提供 a.dll 的编译时引用程序集上 net461，但没有兼容的运行时程序集。*</span><span class="sxs-lookup"><span data-stu-id="8b877-256">*System.Example 1.0.0 provides a compile-time reference assembly for a.dll on net461, but there is no compatible run-time assembly.*</span></span> |
| <span data-ttu-id="8b877-257">**解决方案**</span><span class="sxs-lookup"><span data-stu-id="8b877-257">**Solution**</span></span> | <span data-ttu-id="8b877-258">更改`RuntimeIdentifier`根据需要在项目中使用的值。</span><span class="sxs-lookup"><span data-stu-id="8b877-258">Change the `RuntimeIdentifier` values used in the project as needed.</span></span> |

### <a name="nu1401"></a><span data-ttu-id="8b877-259">NU1401</span><span class="sxs-lookup"><span data-stu-id="8b877-259">NU1401</span></span>

| | |
| --- | --- |
| <span data-ttu-id="8b877-260">**问题**</span><span class="sxs-lookup"><span data-stu-id="8b877-260">**Issue**</span></span> | <span data-ttu-id="8b877-261">包需要功能或框架当前不支持安装的 NuGet 版本。</span><span class="sxs-lookup"><span data-stu-id="8b877-261">The package requires features or frameworks not currently supported by the installed version of NuGet.</span></span> |
| <span data-ttu-id="8b877-262">**示例消息**</span><span class="sxs-lookup"><span data-stu-id="8b877-262">**Example message**</span></span> | <span data-ttu-id="8b877-263">*NuGet.Versioning 程序包需要 NuGet 客户端版本"5.0.0"或更高版本，但是当前 NuGet 版本为"4.3.0"。*</span><span class="sxs-lookup"><span data-stu-id="8b877-263">*The 'NuGet.Versioning' package requires NuGet client version '5.0.0' or above, but the current NuGet version is '4.3.0'.*</span></span> |
| <span data-ttu-id="8b877-264">**解决方案**</span><span class="sxs-lookup"><span data-stu-id="8b877-264">**Solution**</span></span> | <span data-ttu-id="8b877-265">安装较新版本的 NuGet。</span><span class="sxs-lookup"><span data-stu-id="8b877-265">Install a newer version of NuGet.</span></span> <span data-ttu-id="8b877-266">请参阅[安装 NuGet 客户端工具](../install-nuget-client-tools.md)。</span><span class="sxs-lookup"><span data-stu-id="8b877-266">See [Installing NuGet client tools](../install-nuget-client-tools.md).</span></span> |

## <a name="invalid-input-warnings"></a><span data-ttu-id="8b877-267">无效的输入的警告</span><span class="sxs-lookup"><span data-stu-id="8b877-267">Invalid input warnings</span></span>

<span data-ttu-id="8b877-268">[NU1501](#nu1501) | [NU1502](#nu1502) | [NU1503](#nu1503)</span><span class="sxs-lookup"><span data-stu-id="8b877-268">[NU1501](#nu1501) | [NU1502](#nu1502) | [NU1503](#nu1503)</span></span>

### <a name="nu1501"></a><span data-ttu-id="8b877-269">NU1501</span><span class="sxs-lookup"><span data-stu-id="8b877-269">NU1501</span></span>

| | |
| --- | --- |
| <span data-ttu-id="8b877-270">**问题**</span><span class="sxs-lookup"><span data-stu-id="8b877-270">**Issue**</span></span> | <span data-ttu-id="8b877-271">项目还原尝试运行在未找到。</span><span class="sxs-lookup"><span data-stu-id="8b877-271">The project restore is attempting to operate on was not found.</span></span> |
| <span data-ttu-id="8b877-272">**示例消息**</span><span class="sxs-lookup"><span data-stu-id="8b877-272">**Example message**</span></span> | <span data-ttu-id="8b877-273">*文件夹 c:\projects\a 不包含要还原的项目。*</span><span class="sxs-lookup"><span data-stu-id="8b877-273">*The folder 'c:\projects\a' does not contain a project to restore.*</span></span> |
| <span data-ttu-id="8b877-274">**解决方案**</span><span class="sxs-lookup"><span data-stu-id="8b877-274">**Solution**</span></span> | <span data-ttu-id="8b877-275">在包含项目的文件夹中运行 nuget 还原。</span><span class="sxs-lookup"><span data-stu-id="8b877-275">Run nuget restore in a folder that contains a project.</span></span> |

### <a name="nu1502"></a><span data-ttu-id="8b877-276">NU1502</span><span class="sxs-lookup"><span data-stu-id="8b877-276">NU1502</span></span>

| | |
| --- | --- |
| <span data-ttu-id="8b877-277">**问题**</span><span class="sxs-lookup"><span data-stu-id="8b877-277">**Issue**</span></span> | <span data-ttu-id="8b877-278">`RuntimeSupports` 包含无效的配置文件。</span><span class="sxs-lookup"><span data-stu-id="8b877-278">`RuntimeSupports` contains an invalid profile.</span></span> <span data-ttu-id="8b877-279">通常情况下，支持配置文件中找不`runtime.json`从当前的依赖项包文件。</span><span class="sxs-lookup"><span data-stu-id="8b877-279">Typically, the supports profile was not found in a `runtime.json` file from the current dependency packages.</span></span>|
| <span data-ttu-id="8b877-280">**示例消息**</span><span class="sxs-lookup"><span data-stu-id="8b877-280">**Example message**</span></span> | <span data-ttu-id="8b877-281">*未知的兼容性配置文件： aaa*</span><span class="sxs-lookup"><span data-stu-id="8b877-281">*Unknown Compatibility Profile: aaa*</span></span> |
| <span data-ttu-id="8b877-282">**解决方案**</span><span class="sxs-lookup"><span data-stu-id="8b877-282">**Solution**</span></span> | <span data-ttu-id="8b877-283">检查`RuntimeSupports`项目中的值。</span><span class="sxs-lookup"><span data-stu-id="8b877-283">Check the `RuntimeSupports` value in your project.</span></span> |

### <a name="nu1503"></a><span data-ttu-id="8b877-284">NU1503</span><span class="sxs-lookup"><span data-stu-id="8b877-284">NU1503</span></span>

| | |
| --- | --- |
| <span data-ttu-id="8b877-285">**问题**</span><span class="sxs-lookup"><span data-stu-id="8b877-285">**Issue**</span></span> | <span data-ttu-id="8b877-286">依赖项项目不能导入 NuGet 的恢复目标。</span><span class="sxs-lookup"><span data-stu-id="8b877-286">A dependency project doesn't import NuGet's restore targets.</span></span> <span data-ttu-id="8b877-287">这是类似于 NU1105 但此处项目，将跳过并忽略而不是导致所有还原失败。</span><span class="sxs-lookup"><span data-stu-id="8b877-287">This is similar to NU1105 but here the project is skipped and ignored instead of causing all of restore to fail.</span></span> <span data-ttu-id="8b877-288">在复杂的解决方案通常有其他类型的可能不支持还原的项目中。</span><span class="sxs-lookup"><span data-stu-id="8b877-288">In complex solutions there are often other types of projects that may not support restore.</span></span> |
| <span data-ttu-id="8b877-289">**示例消息**</span><span class="sxs-lookup"><span data-stu-id="8b877-289">**Example message**</span></span> | <span data-ttu-id="8b877-290">*正在跳过还原项目 c:\a.csproj。项目文件可能无效或缺少所需的还原的目标。*</span><span class="sxs-lookup"><span data-stu-id="8b877-290">*Skipping restore for project 'c:\a.csproj'. The project file may be invalid or missing targets required for restore.*</span></span> |
| <span data-ttu-id="8b877-291">**解决方案**</span><span class="sxs-lookup"><span data-stu-id="8b877-291">**Solution**</span></span> | <span data-ttu-id="8b877-292">这可能会导致不导入公共属性/目标的自动导入还原的项目。</span><span class="sxs-lookup"><span data-stu-id="8b877-292">This can happen for projects that do not import common props/targets which automatically import restore.</span></span> <span data-ttu-id="8b877-293">如果项目不需要还原这可予以忽视。</span><span class="sxs-lookup"><span data-stu-id="8b877-293">If the project doesn't need to be restored this can be ignored.</span></span> <span data-ttu-id="8b877-294">否则，编辑受影响的项目添加为还原的目标。</span><span class="sxs-lookup"><span data-stu-id="8b877-294">Otherwise, edit the affected project to add targets for restore.</span></span> |

## <a name="unexpected-package-version-warnings"></a><span data-ttu-id="8b877-295">意外的包版本警告</span><span class="sxs-lookup"><span data-stu-id="8b877-295">Unexpected package version warnings</span></span>

<span data-ttu-id="8b877-296">[NU1601](#nu1601) | [NU1602](#nu1602) | [NU1603](#nu1603) | [NU1604](#nu1604) | [NU1605](#nu1605)</span><span class="sxs-lookup"><span data-stu-id="8b877-296">[NU1601](#nu1601) | [NU1602](#nu1602) | [NU1603](#nu1603) | [NU1604](#nu1604) | [NU1605](#nu1605)</span></span>

### <a name="nu1601"></a><span data-ttu-id="8b877-297">NU1601</span><span class="sxs-lookup"><span data-stu-id="8b877-297">NU1601</span></span>

| | |
| --- | --- |
| <span data-ttu-id="8b877-298">**问题**</span><span class="sxs-lookup"><span data-stu-id="8b877-298">**Issue**</span></span> | <span data-ttu-id="8b877-299">直接项目依赖项已解除了一个为更高版本比指定的项目。</span><span class="sxs-lookup"><span data-stu-id="8b877-299">A direct project dependency was bumped to a higher version than the project specified.</span></span> |
| <span data-ttu-id="8b877-300">**示例消息**</span><span class="sxs-lookup"><span data-stu-id="8b877-300">**Example message**</span></span> | <span data-ttu-id="8b877-301">*指定的依赖项已 NuGet.Versioning (> = 3.5.0) 但最终的 NuGet.Versioning 4.0.0。*</span><span class="sxs-lookup"><span data-stu-id="8b877-301">*Dependency specified was NuGet.Versioning (>= 3.5.0) but ended up with NuGet.Versioning 4.0.0.*</span></span> |
| <span data-ttu-id="8b877-302">**解决方案**</span><span class="sxs-lookup"><span data-stu-id="8b877-302">**Solution**</span></span> | <span data-ttu-id="8b877-303">更新到适当版本的项目中的依赖关系。</span><span class="sxs-lookup"><span data-stu-id="8b877-303">Update the dependency in the project to an appropriate version.</span></span> |

### <a name="nu1602"></a><span data-ttu-id="8b877-304">NU1602</span><span class="sxs-lookup"><span data-stu-id="8b877-304">NU1602</span></span>

| | |
| --- | --- |
| <span data-ttu-id="8b877-305">**问题**</span><span class="sxs-lookup"><span data-stu-id="8b877-305">**Issue**</span></span> | <span data-ttu-id="8b877-306">包依赖项缺少零下限。</span><span class="sxs-lookup"><span data-stu-id="8b877-306">A package dependency is missing a lower bound.</span></span> <span data-ttu-id="8b877-307">这不允许还原，以便查找*最佳匹配*。</span><span class="sxs-lookup"><span data-stu-id="8b877-307">This doesn't allow restore to find the *best match*.</span></span> <span data-ttu-id="8b877-308">每个还原将浮动向下尝试查找可以使用较低版本。</span><span class="sxs-lookup"><span data-stu-id="8b877-308">Each restore will float downwards trying to find a lower version that can be used.</span></span> <span data-ttu-id="8b877-309">这意味着此恢复将进入联机状态，以检查每个时间而不是在用户程序包文件夹中使用已存在的包的所有源。</span><span class="sxs-lookup"><span data-stu-id="8b877-309">This means that restore goes online to check all sources each time instead of using the packages that already exist in the user package folder.</span></span> |
| <span data-ttu-id="8b877-310">**示例消息**</span><span class="sxs-lookup"><span data-stu-id="8b877-310">**Example message**</span></span> | <span data-ttu-id="8b877-311">*NuGet.Packaging 4.0.0 不依赖项 NuGet.Versioning (> 3.5.0) 提供包含下限。3.6.0 的近似最佳匹配已解决。*</span><span class="sxs-lookup"><span data-stu-id="8b877-311">*NuGet.Packaging 4.0.0 does not provide an inclusive lower bound for dependency NuGet.Versioning (> 3.5.0). An approximate best match of 3.6.0 was resolved.*</span></span> |
| <span data-ttu-id="8b877-312">**解决方案**</span><span class="sxs-lookup"><span data-stu-id="8b877-312">**Solution**</span></span> | <span data-ttu-id="8b877-313">这通常是创作错误的包。</span><span class="sxs-lookup"><span data-stu-id="8b877-313">This is usually a package authoring error.</span></span> <span data-ttu-id="8b877-314">请联系程序包作者以解决此问题。</span><span class="sxs-lookup"><span data-stu-id="8b877-314">Contact the package author to resolve the issue.</span></span> |

### <a name="nu1603"></a><span data-ttu-id="8b877-315">NU1603</span><span class="sxs-lookup"><span data-stu-id="8b877-315">NU1603</span></span>

| | |
| --- | --- |
| <span data-ttu-id="8b877-316">**问题**</span><span class="sxs-lookup"><span data-stu-id="8b877-316">**Issue**</span></span> | <span data-ttu-id="8b877-317">包依赖项指定未找到的版本。</span><span class="sxs-lookup"><span data-stu-id="8b877-317">A package dependency specified a version that could not be found.</span></span> <span data-ttu-id="8b877-318">通常情况下，包源中不包含预期的下限版本。</span><span class="sxs-lookup"><span data-stu-id="8b877-318">Typically, the package sources do not contain the expected lower bound version.</span></span> <span data-ttu-id="8b877-319">与它不同的包编写针对相反，使用更高版本。</span><span class="sxs-lookup"><span data-stu-id="8b877-319">A higher version was used instead, which differs from what the package was authored against.</span></span><br/><br/><span data-ttu-id="8b877-320">这意味着找不到该还原*最佳匹配*。</span><span class="sxs-lookup"><span data-stu-id="8b877-320">This means that restore did not find the *best match*.</span></span> <span data-ttu-id="8b877-321">每个还原将浮动向下尝试查找可以使用较低版本。</span><span class="sxs-lookup"><span data-stu-id="8b877-321">Each restore will float downwards trying to find a lower version that can be used.</span></span> <span data-ttu-id="8b877-322">这意味着此恢复将进入联机状态，以检查每个时间而不是在用户程序包文件夹中使用已存在的包的所有源。</span><span class="sxs-lookup"><span data-stu-id="8b877-322">This means that restore goes online to check all sources each time instead of using the packages that already exist in the user package folder.</span></span> |
| <span data-ttu-id="8b877-323">**示例消息**</span><span class="sxs-lookup"><span data-stu-id="8b877-323">**Example message**</span></span> | <span data-ttu-id="8b877-324">NuGet.Packaging 4.0.0 取决于 NuGet.Versioning (> = 4.0.0) 但找不到 4.0.0。</span><span class="sxs-lookup"><span data-stu-id="8b877-324">NuGet.Packaging 4.0.0 depends on NuGet.Versioning (>= 4.0.0) but 4.0.0 was not found.</span></span> <span data-ttu-id="8b877-325">5.0.0 的近似最佳匹配已解决。</span><span class="sxs-lookup"><span data-stu-id="8b877-325">An approximate best match of 5.0.0 was resolved.</span></span> |
| <span data-ttu-id="8b877-326">**解决方案**</span><span class="sxs-lookup"><span data-stu-id="8b877-326">**Solution**</span></span> | <span data-ttu-id="8b877-327">如果尚未释放预期包，这可能是包创作错误。</span><span class="sxs-lookup"><span data-stu-id="8b877-327">If the package expected has not been released then this may be a package authoring error.</span></span> <span data-ttu-id="8b877-328">请联系程序包作者以解决此问题。</span><span class="sxs-lookup"><span data-stu-id="8b877-328">Contact the package author to resolve the issue.</span></span> <span data-ttu-id="8b877-329">如果已发布包，然后检查它是否可用上正在使用的包源。</span><span class="sxs-lookup"><span data-stu-id="8b877-329">If the package has been released, then check that it's available on the package sources you're using.</span></span> <span data-ttu-id="8b877-330">如果使用私有源时，你可能需要更新上的源的包。</span><span class="sxs-lookup"><span data-stu-id="8b877-330">If using a private source, you may need to update the package on that feed.</span></span> |

### <a name="nu1604"></a><span data-ttu-id="8b877-331">NU1604</span><span class="sxs-lookup"><span data-stu-id="8b877-331">NU1604</span></span>

| | |
| --- | --- |
| <span data-ttu-id="8b877-332">**问题**</span><span class="sxs-lookup"><span data-stu-id="8b877-332">**Issue**</span></span> | <span data-ttu-id="8b877-333">项目依赖项未定义零下限。</span><span class="sxs-lookup"><span data-stu-id="8b877-333">A project dependency doesn't define a lower bound.</span></span><br/><br/><span data-ttu-id="8b877-334">这意味着找不到该还原*最佳匹配*。</span><span class="sxs-lookup"><span data-stu-id="8b877-334">This means that restore did not find the *best match*.</span></span> <span data-ttu-id="8b877-335">每个还原将浮动向下尝试查找可以使用较低版本。</span><span class="sxs-lookup"><span data-stu-id="8b877-335">Each restore will float downwards trying to find a lower version that can be used.</span></span> <span data-ttu-id="8b877-336">这意味着此恢复将进入联机状态，以检查每个时间而不是在用户程序包文件夹中使用已存在的包的所有源。</span><span class="sxs-lookup"><span data-stu-id="8b877-336">This means that restore goes online to check all sources each time instead of using the packages that already exist in the user package folder.</span></span> |
| <span data-ttu-id="8b877-337">**示例消息**</span><span class="sxs-lookup"><span data-stu-id="8b877-337">**Example message**</span></span> | <span data-ttu-id="8b877-338">*项目依赖项 NuGet.Versioning (< = 9.0.0) doe 不包含包含下限。依赖项版本以确保一致还原结果中包括零下限。*</span><span class="sxs-lookup"><span data-stu-id="8b877-338">*Project dependency NuGet.Versioning (<= 9.0.0) doe not contain an inclusive lower bound. Include a lower bound in the dependency version to ensure consistent restore results.*</span></span> |
| <span data-ttu-id="8b877-339">**解决方案**</span><span class="sxs-lookup"><span data-stu-id="8b877-339">**Solution**</span></span> | <span data-ttu-id="8b877-340">更新项目的`PackageReference``Version`属性以包括零下限。</span><span class="sxs-lookup"><span data-stu-id="8b877-340">Update the project's `PackageReference` `Version` attribute to include a lower bound.</span></span> |

### <a name="nu1605"></a><span data-ttu-id="8b877-341">NU1605</span><span class="sxs-lookup"><span data-stu-id="8b877-341">NU1605</span></span>

| | |
| --- | --- |
| <span data-ttu-id="8b877-342">**问题**</span><span class="sxs-lookup"><span data-stu-id="8b877-342">**Issue**</span></span> | <span data-ttu-id="8b877-343">依赖项包指定比还原最终解决更高版本的包的版本约束。</span><span class="sxs-lookup"><span data-stu-id="8b877-343">A dependency package specified a version constraint on a higher version of a package than restore ultimately resolved.</span></span> <span data-ttu-id="8b877-344">也就是说，"最接近的 wins"规则在解析包时，由于在图中的最近包可能已重写相距包。</span><span class="sxs-lookup"><span data-stu-id="8b877-344">That is, because of the "nearest wins" rule when resolving packages, a nearer package in the graph may have overridden a distant package.</span></span> |
| <span data-ttu-id="8b877-345">**示例消息**</span><span class="sxs-lookup"><span data-stu-id="8b877-345">**Example message**</span></span> | <span data-ttu-id="8b877-346">*检测到包降级： NuGet.Versioning 从 4.0.0 到 3.5.0。要选择的不同版本的项目中直接引用包。<br/>NuGet.Packaging 3.5.0-> NuGet.Versioning 3.5.0<br/> NuGet.Commands 4.0.0-> NuGet.Configuration 4.0.0-> NuGet.Versioning 4.0.0*</span><span class="sxs-lookup"><span data-stu-id="8b877-346">*Detected package downgrade: NuGet.Versioning from 4.0.0 to 3.5.0. Reference the package directly from the project to select a different version.<br/>  NuGet.Packaging 3.5.0 -> NuGet.Versioning 3.5.0<br/>  NuGet.Commands 4.0.0 -> NuGet.Configuration 4.0.0 -> NuGet.Versioning 4.0.0*</span></span> |
| <span data-ttu-id="8b877-347">**解决方案**</span><span class="sxs-lookup"><span data-stu-id="8b877-347">**Solution**</span></span> | <span data-ttu-id="8b877-348">添加到你想要使用的包的更高版本的项目的直接引用。</span><span class="sxs-lookup"><span data-stu-id="8b877-348">Add a direct reference to the project for the higher version of the package that you want to use.</span></span> |

## <a name="resolver-conflict-warnings"></a><span data-ttu-id="8b877-349">冲突解决程序冲突警告</span><span class="sxs-lookup"><span data-stu-id="8b877-349">Resolver conflict warnings</span></span>

### <a name="nu1608"></a><span data-ttu-id="8b877-350">NU1608</span><span class="sxs-lookup"><span data-stu-id="8b877-350">NU1608</span></span>

| | |
| --- | --- |
| <span data-ttu-id="8b877-351">**问题**</span><span class="sxs-lookup"><span data-stu-id="8b877-351">**Issue**</span></span> | <span data-ttu-id="8b877-352">解决的包是不是依赖项约束允许，更高版本。</span><span class="sxs-lookup"><span data-stu-id="8b877-352">A resolved package is higher than a dependency constraint allows.</span></span> <span data-ttu-id="8b877-353">这意味着项目直接引用的包将从其他包的依赖项约束重写。</span><span class="sxs-lookup"><span data-stu-id="8b877-353">This means that a package referenced directly by a project overrides dependency constraints from other packages.</span></span>|
| <span data-ttu-id="8b877-354">**示例消息**</span><span class="sxs-lookup"><span data-stu-id="8b877-354">**Example message**</span></span> | <span data-ttu-id="8b877-355">*外部依赖关系约束的检测到的包版本： x 1.0.0 要求的 y （= 1.0.0），但版本 y 2.0.0 为已解决。*</span><span class="sxs-lookup"><span data-stu-id="8b877-355">*Detected package version outside of dependency constraint: x 1.0.0 requires y (= 1.0.0) but version y 2.0.0 was resolved.*</span></span> |
| <span data-ttu-id="8b877-356">**解决方案**</span><span class="sxs-lookup"><span data-stu-id="8b877-356">**Solution**</span></span> | <span data-ttu-id="8b877-357">在某些情况下，这是有意，可以禁止显示警告。</span><span class="sxs-lookup"><span data-stu-id="8b877-357">In some cases this is intentional and the warning can be suppressed.</span></span> <span data-ttu-id="8b877-358">否则，更改以扩大其版本约束的包项目的引用。</span><span class="sxs-lookup"><span data-stu-id="8b877-358">Otherwise, change the project's reference to the package to widen its version constraints.</span></span> |

## <a name="package-fallback-warnings"></a><span data-ttu-id="8b877-359">包回退警告</span><span class="sxs-lookup"><span data-stu-id="8b877-359">Package fallback warnings</span></span>

### <a name="nu1701"></a><span data-ttu-id="8b877-360">NU1701</span><span class="sxs-lookup"><span data-stu-id="8b877-360">NU1701</span></span>

| | |
| --- | --- |
| <span data-ttu-id="8b877-361">**问题**</span><span class="sxs-lookup"><span data-stu-id="8b877-361">**Issue**</span></span> | <span data-ttu-id="8b877-362">`PackageTargetFallback` / `AssetTargetFallback` 用来从包选择资产。</span><span class="sxs-lookup"><span data-stu-id="8b877-362">`PackageTargetFallback` / `AssetTargetFallback` was used to select assets from a package.</span></span> <span data-ttu-id="8b877-363">警告让用户知道资产可能不兼容的 100%。</span><span class="sxs-lookup"><span data-stu-id="8b877-363">The warning let users know that the assets may not be 100% compatible.</span></span> |
| <span data-ttu-id="8b877-364">**示例消息**</span><span class="sxs-lookup"><span data-stu-id="8b877-364">**Example message**</span></span> | <span data-ttu-id="8b877-365">*包 NuGet.Versioning 已还原可移植 net45 + win8 改为使用项目目标框架 netstandard1.5。此程序包并不一定与你的项目完全兼容。*</span><span class="sxs-lookup"><span data-stu-id="8b877-365">*Package 'NuGet.Versioning' was restored using 'portable-net45+win8' instead the project target framework 'netstandard1.5'. This package may not be fully compatible with your project.*</span></span> |
| <span data-ttu-id="8b877-366">**解决方案**</span><span class="sxs-lookup"><span data-stu-id="8b877-366">**Solution**</span></span> | <span data-ttu-id="8b877-367">将项目的目标框架更改为另一个包支持。</span><span class="sxs-lookup"><span data-stu-id="8b877-367">Change the project's target framework to one that the package supports.</span></span> |

## <a name="feed-warnings"></a><span data-ttu-id="8b877-368">源警告</span><span class="sxs-lookup"><span data-stu-id="8b877-368">Feed warnings</span></span>

### <a name="nu1801"></a><span data-ttu-id="8b877-369">NU1801</span><span class="sxs-lookup"><span data-stu-id="8b877-369">NU1801</span></span>

| | |
| --- | --- |
| <span data-ttu-id="8b877-370">**问题**</span><span class="sxs-lookup"><span data-stu-id="8b877-370">**Issue**</span></span> | <span data-ttu-id="8b877-371">读取源时出错时`IgnoreFailedSources`设置为 true，将其转换为非致命性警告。</span><span class="sxs-lookup"><span data-stu-id="8b877-371">An error occurred when reading the feed when `IgnoreFailedSources` is set to true, converting it to a non-fatal warning.</span></span> <span data-ttu-id="8b877-372">这可能包含的任何消息，并为泛型。</span><span class="sxs-lookup"><span data-stu-id="8b877-372">This could contain any message and is generic.</span></span> |
| <span data-ttu-id="8b877-373">**示例消息**</span><span class="sxs-lookup"><span data-stu-id="8b877-373">**Example message**</span></span> | <span data-ttu-id="8b877-374">n/a</span><span class="sxs-lookup"><span data-stu-id="8b877-374">n/a</span></span> |
| <span data-ttu-id="8b877-375">**解决方案**</span><span class="sxs-lookup"><span data-stu-id="8b877-375">**Solution**</span></span> | <span data-ttu-id="8b877-376">编辑你的配置来指定有效的源。</span><span class="sxs-lookup"><span data-stu-id="8b877-376">Edit your configuration to specify valid sources.</span></span> |

## <a name="nuget-internal-errors-and-warnings"></a><span data-ttu-id="8b877-377">NuGet 内部错误和警告</span><span class="sxs-lookup"><span data-stu-id="8b877-377">NuGet internal errors and warnings</span></span>

<span data-ttu-id="8b877-378">[NU1000](#nu1000) | [NU1500](#nu1500)</span><span class="sxs-lookup"><span data-stu-id="8b877-378">[NU1000](#nu1000) | [NU1500](#nu1500)</span></span>

### <a name="nu1000"></a><span data-ttu-id="8b877-379">NU1000</span><span class="sxs-lookup"><span data-stu-id="8b877-379">NU1000</span></span>

| | |
| --- | --- |
| <span data-ttu-id="8b877-380">**问题**</span><span class="sxs-lookup"><span data-stu-id="8b877-380">**Issue**</span></span> | <span data-ttu-id="8b877-381">从 NuGet 非特定的内部错误。</span><span class="sxs-lookup"><span data-stu-id="8b877-381">A non specific internal error from NuGet.</span></span> |
| <span data-ttu-id="8b877-382">**解决方案**</span><span class="sxs-lookup"><span data-stu-id="8b877-382">**Solution**</span></span> | <span data-ttu-id="8b877-383">检查日志以了解更多信息</span><span class="sxs-lookup"><span data-stu-id="8b877-383">Check the logs for more information</span></span> |

### <a name="nu1500"></a><span data-ttu-id="8b877-384">NU1500</span><span class="sxs-lookup"><span data-stu-id="8b877-384">NU1500</span></span>

| | |
| --- | --- |
| <span data-ttu-id="8b877-385">**问题**</span><span class="sxs-lookup"><span data-stu-id="8b877-385">**Issue**</span></span> | <span data-ttu-id="8b877-386">从 NuGet 内部非特定警告。</span><span class="sxs-lookup"><span data-stu-id="8b877-386">A non specific internal warning from NuGet.</span></span> |
| <span data-ttu-id="8b877-387">**解决方案**</span><span class="sxs-lookup"><span data-stu-id="8b877-387">**Solution**</span></span> | <span data-ttu-id="8b877-388">检查日志以了解更多信息</span><span class="sxs-lookup"><span data-stu-id="8b877-388">Check the logs for more information</span></span> |

## <a name="signed-packages-creation-and-verification"></a><span data-ttu-id="8b877-389">已签名的软件包 （创建和验证）</span><span class="sxs-lookup"><span data-stu-id="8b877-389">Signed packages (creation and verification)</span></span>

<span data-ttu-id="8b877-390">*NuGet 4.6.0+*</span><span class="sxs-lookup"><span data-stu-id="8b877-390">*NuGet 4.6.0+*</span></span>

<span data-ttu-id="8b877-391">[NU3000](#nu3000) | [NU3001](#nu3001) | [NU3002](#nu3002) | [NU3004](#nu3004) | [NU3008](#nu3008) | [NU3018](#nu3018) | [NU3028](#nu3028)</span><span class="sxs-lookup"><span data-stu-id="8b877-391">[NU3000](#nu3000) | [NU3001](#nu3001) | [NU3002](#nu3002) | [NU3004](#nu3004) | [NU3008](#nu3008) | [NU3018](#nu3018) | [NU3028](#nu3028)</span></span>

### <a name="nu3000"></a><span data-ttu-id="8b877-392">NU3000</span><span class="sxs-lookup"><span data-stu-id="8b877-392">NU3000</span></span>

| | |
| --- | --- |
| <span data-ttu-id="8b877-393">**问题**</span><span class="sxs-lookup"><span data-stu-id="8b877-393">**Issue**</span></span> | <span data-ttu-id="8b877-394">非特定错误相关的包签名和签名包验证。</span><span class="sxs-lookup"><span data-stu-id="8b877-394">A non-specific error related to package signing and signed package verification.</span></span> |
| <span data-ttu-id="8b877-395">**解决方案**</span><span class="sxs-lookup"><span data-stu-id="8b877-395">**Solution**</span></span> | <span data-ttu-id="8b877-396">请检查日志以了解更多信息。</span><span class="sxs-lookup"><span data-stu-id="8b877-396">Check the logs for more information.</span></span> |

### <a name="nu3001"></a><span data-ttu-id="8b877-397">NU3001</span><span class="sxs-lookup"><span data-stu-id="8b877-397">NU3001</span></span>

| | |
| --- | --- |
| <span data-ttu-id="8b877-398">**问题**</span><span class="sxs-lookup"><span data-stu-id="8b877-398">**Issue**</span></span> | <span data-ttu-id="8b877-399">无效的自变量为[登录命令](../tools/cli-ref-sign.md)或[验证命令](../tools/cli-ref-verify.md)。</span><span class="sxs-lookup"><span data-stu-id="8b877-399">Invalid arguments to either the [sign command](../tools/cli-ref-sign.md) or the [verify command](../tools/cli-ref-verify.md).</span></span> |
| <span data-ttu-id="8b877-400">**解决方案**</span><span class="sxs-lookup"><span data-stu-id="8b877-400">**Solution**</span></span> | <span data-ttu-id="8b877-401">检查并更正提供的自变量。</span><span class="sxs-lookup"><span data-stu-id="8b877-401">Check and correct the arguments provided.</span></span> |

### <a name="nu3002"></a><span data-ttu-id="8b877-402">NU3002</span><span class="sxs-lookup"><span data-stu-id="8b877-402">NU3002</span></span>

| | |
| --- | --- |
| <span data-ttu-id="8b877-403">**问题**</span><span class="sxs-lookup"><span data-stu-id="8b877-403">**Issue**</span></span> | <span data-ttu-id="8b877-404">`-Timestamper`选项未指定与[nuget 登录命令](../tools/cli-ref-sign.md)。</span><span class="sxs-lookup"><span data-stu-id="8b877-404">The `-Timestamper` option was not specified with the [nuget sign command](../tools/cli-ref-sign.md).</span></span> |
| <span data-ttu-id="8b877-405">**示例消息**</span><span class="sxs-lookup"><span data-stu-id="8b877-405">**Example message**</span></span> | <span data-ttu-id="8b877-406">*-Timestamper 未提供选项。签名的包不会加盖时间戳。*</span><span class="sxs-lookup"><span data-stu-id="8b877-406">*The '-Timestamper' option was not provided. The signed package will not be timestamped.*</span></span> |
| <span data-ttu-id="8b877-407">**解决方案**</span><span class="sxs-lookup"><span data-stu-id="8b877-407">**Solution**</span></span> | <span data-ttu-id="8b877-408">指定`-Timestamper`选项与`nuget sign`。</span><span class="sxs-lookup"><span data-stu-id="8b877-408">Specify the `-Timestamper` option with `nuget sign`.</span></span> |

### <a name="nu3004"></a><span data-ttu-id="8b877-409">NU3004</span><span class="sxs-lookup"><span data-stu-id="8b877-409">NU3004</span></span>

| | |
| --- | --- |
| <span data-ttu-id="8b877-410">**问题**</span><span class="sxs-lookup"><span data-stu-id="8b877-410">**Issue**</span></span> | <span data-ttu-id="8b877-411">未签名的软件包提供给[nuget 验证命令](../tools/cli-ref-verify.md)。</span><span class="sxs-lookup"><span data-stu-id="8b877-411">An unsigned package was provided to the [nuget verify command](../tools/cli-ref-verify.md).</span></span> |
| <span data-ttu-id="8b877-412">**解决方案**</span><span class="sxs-lookup"><span data-stu-id="8b877-412">**Solution**</span></span> | <span data-ttu-id="8b877-413">运行`nuget verify`与已签名的包。</span><span class="sxs-lookup"><span data-stu-id="8b877-413">Run `nuget verify` with a signed package.</span></span> <span data-ttu-id="8b877-414">请参阅[对包签名](../create-packages/Sign-a-Package.md)。</span><span class="sxs-lookup"><span data-stu-id="8b877-414">See [Sign a package](../create-packages/Sign-a-Package.md).</span></span> |

### <a name="nu3008"></a><span data-ttu-id="8b877-415">NU3008</span><span class="sxs-lookup"><span data-stu-id="8b877-415">NU3008</span></span>

| | |
| --- | --- |
| <span data-ttu-id="8b877-416">**问题**</span><span class="sxs-lookup"><span data-stu-id="8b877-416">**Issue**</span></span> | <span data-ttu-id="8b877-417">包完整性检查失败，这意味着已签名的包已被篡改因为正进行签名。</span><span class="sxs-lookup"><span data-stu-id="8b877-417">The package integrity check failed, meaning that a signed package was tampered with since being signed.</span></span> |
| <span data-ttu-id="8b877-418">**解决方案**</span><span class="sxs-lookup"><span data-stu-id="8b877-418">**Solution**</span></span> | <span data-ttu-id="8b877-419">扫描计算机中的与防病毒软件。</span><span class="sxs-lookup"><span data-stu-id="8b877-419">Scan your computer with anti-virus software.</span></span> <span data-ttu-id="8b877-420">然后从计算机中删除包、 重新安装它，和重试该操作。</span><span class="sxs-lookup"><span data-stu-id="8b877-420">Then remove the package from the computer, reinstall it, and try the operation again.</span></span> <span data-ttu-id="8b877-421">如果问题仍然存在，请联系的包源的所有者和包所有者。</span><span class="sxs-lookup"><span data-stu-id="8b877-421">If the problem persists, contact the owner of the package source and the package owner.</span></span> |

### <a name="nu3018"></a><span data-ttu-id="8b877-422">NU3018</span><span class="sxs-lookup"><span data-stu-id="8b877-422">NU3018</span></span>

| | |
| --- | --- |
| <span data-ttu-id="8b877-423">**问题**</span><span class="sxs-lookup"><span data-stu-id="8b877-423">**Issue**</span></span> | <span data-ttu-id="8b877-424">证书链生成失败主签名。</span><span class="sxs-lookup"><span data-stu-id="8b877-424">Certificate chain building failed for the primary signature.</span></span> <span data-ttu-id="8b877-425">主签名证书不受信任，被吊销，或者该证书的吊销信息不可用。</span><span class="sxs-lookup"><span data-stu-id="8b877-425">The primary signing certificate is untrusted, revoked, or revocation information for the certificate is unavailable.</span></span> |
| <span data-ttu-id="8b877-426">**示例消息**</span><span class="sxs-lookup"><span data-stu-id="8b877-426">**Example message**</span></span> | <span data-ttu-id="8b877-427">*警告： NU3018： 吊销功能无法检查吊销证书。*</span><span class="sxs-lookup"><span data-stu-id="8b877-427">*WARNING: NU3018: The revocation function was unable to check revocation for the certificate.*</span></span> |
| <span data-ttu-id="8b877-428">**解决方案**</span><span class="sxs-lookup"><span data-stu-id="8b877-428">**Solution**</span></span> | <span data-ttu-id="8b877-429">使用一个受信任且有效的证书。</span><span class="sxs-lookup"><span data-stu-id="8b877-429">Use a trusted and valid certificate.</span></span> <span data-ttu-id="8b877-430">检查 internet 连接。</span><span class="sxs-lookup"><span data-stu-id="8b877-430">Check internet connectivity.</span></span> |

### <a name="nu3028"></a><span data-ttu-id="8b877-431">NU3028</span><span class="sxs-lookup"><span data-stu-id="8b877-431">NU3028</span></span>

| | |
| --- | --- |
| <span data-ttu-id="8b877-432">**问题**</span><span class="sxs-lookup"><span data-stu-id="8b877-432">**Issue**</span></span> | <span data-ttu-id="8b877-433">证书链生成失败的时间戳签名。</span><span class="sxs-lookup"><span data-stu-id="8b877-433">Certificate chain building failed for the timestamp signature.</span></span> <span data-ttu-id="8b877-434">时间戳签名证书不受信任，被吊销，或者该证书的吊销信息不可用。</span><span class="sxs-lookup"><span data-stu-id="8b877-434">The timestamp signing certificate is untrusted, revoked, or revocation information for the certificate is unavailable.</span></span> |
| <span data-ttu-id="8b877-435">**示例消息**</span><span class="sxs-lookup"><span data-stu-id="8b877-435">**Example message**</span></span> | <span data-ttu-id="8b877-436">*警告： NU3028： 吊销功能无法检查吊销证书。*</span><span class="sxs-lookup"><span data-stu-id="8b877-436">*WARNING: NU3028: The revocation function was unable to check revocation for the certificate.*</span></span> |
| <span data-ttu-id="8b877-437">**解决方案**</span><span class="sxs-lookup"><span data-stu-id="8b877-437">**Solution**</span></span> | <span data-ttu-id="8b877-438">使用一个受信任且有效的证书。</span><span class="sxs-lookup"><span data-stu-id="8b877-438">Use a trusted and valid certificate.</span></span> <span data-ttu-id="8b877-439">检查 internet 连接。</span><span class="sxs-lookup"><span data-stu-id="8b877-439">Check internet connectivity.</span></span> |
