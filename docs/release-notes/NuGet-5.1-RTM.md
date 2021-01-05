---
title: NuGet 5.1 RTM 发行说明
description: NuGet 5.1 的发行说明，包括新功能、bug 修复和 Dcr。
author: karann-msft
ms.author: karann
ms.date: 05/21/2019
ms.topic: conceptual
ms.openlocfilehash: 2a94360dc375ba90b90c1045f4acbcfca81fea5b
ms.sourcegitcommit: 53b06e27bcfef03500a69548ba2db069b55837f1
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/19/2020
ms.locfileid: "97699861"
---
# <a name="nuget-51-release-notes"></a><span data-ttu-id="3e111-103">NuGet 5.1 发行说明</span><span class="sxs-lookup"><span data-stu-id="3e111-103">NuGet 5.1 Release Notes</span></span>

<span data-ttu-id="3e111-104">NuGet 分发车辆：</span><span class="sxs-lookup"><span data-stu-id="3e111-104">NuGet distribution vehicles:</span></span>

| <span data-ttu-id="3e111-105">NuGet 版本</span><span class="sxs-lookup"><span data-stu-id="3e111-105">NuGet version</span></span> | <span data-ttu-id="3e111-106">适用于 Visual Studio 版本</span><span class="sxs-lookup"><span data-stu-id="3e111-106">Available in Visual Studio version</span></span>| <span data-ttu-id="3e111-107">适用于 .NET SDK</span><span class="sxs-lookup"><span data-stu-id="3e111-107">Available in .NET SDK(s)</span></span>|
|:---|:---|:---|
| [<span data-ttu-id="3e111-108">**5.1.0**</span><span class="sxs-lookup"><span data-stu-id="3e111-108">**5.1.0**</span></span>](https://nuget.org/downloads) | [<span data-ttu-id="3e111-109">Visual Studio 2019 版本 16.1</span><span class="sxs-lookup"><span data-stu-id="3e111-109">Visual Studio 2019 version 16.1</span></span>](https://visualstudio.microsoft.com/downloads/) | <span data-ttu-id="3e111-110">[2.1.70 x](https://dotnet.microsoft.com/download/dotnet-core/2.1)<sup>1</sup>， [2.2.30 x](https://dotnet.microsoft.com/download/dotnet-core/2.2)<sup>2</sup></span><span class="sxs-lookup"><span data-stu-id="3e111-110">[2.1.70X](https://dotnet.microsoft.com/download/dotnet-core/2.1)<sup>1</sup>, [2.2.30X](https://dotnet.microsoft.com/download/dotnet-core/2.2)<sup>2</sup></span></span> |

<span data-ttu-id="3e111-111"><sup>1</sup>随 Visual Studio 2019 with .NET Core 工作负载一起安装</span><span class="sxs-lookup"><span data-stu-id="3e111-111"><sup>1</sup>Installed with Visual Studio 2019 with .NET Core workload</span></span> 

<span data-ttu-id="3e111-112"><sup>2</sup>可用作 Visual Studio 2019 with .NET Core 工作负载的可选安装</span><span class="sxs-lookup"><span data-stu-id="3e111-112"><sup>2</sup>Available as an optional install with Visual Studio 2019 with .NET Core workload</span></span>

## <a name="summary-whats-new-in-51"></a><span data-ttu-id="3e111-113">摘要：5.1 中的新增功能</span><span class="sxs-lookup"><span data-stu-id="3e111-113">Summary: What's New in 5.1</span></span>

* <span data-ttu-id="3e111-114">支持跳过包推送（如果它已存在，以便更好地与 CI/CD 工作流集成）， [#1630](https://github.com/NuGet/Home/issues/1630#issuecomment-483461100)</span><span class="sxs-lookup"><span data-stu-id="3e111-114">Support to skip a package push if it already exists to allow for better integration with CI/CD workflows - [#1630](https://github.com/NuGet/Home/issues/1630#issuecomment-483461100)</span></span>

* <span data-ttu-id="3e111-115">Visual Studio 现在提供了一个方便的链接，指向包的 nuget.org 库页 [#5299](https://github.com/NuGet/Home/issues/5299#issuecomment-494458510)</span><span class="sxs-lookup"><span data-stu-id="3e111-115">Visual Studio now provides a convenient link to the the package's nuget.org gallery page - [#5299](https://github.com/NuGet/Home/issues/5299#issuecomment-494458510)</span></span>

* <span data-ttu-id="3e111-116">支持新的 .NET Core 3.0 资产，例如 [目标包](https://github.com/dotnet/cli/issues/10006) 和 [运行时包](https://github.com/dotnet/cli/issues/10007)</span><span class="sxs-lookup"><span data-stu-id="3e111-116">Support for new .NET Core 3.0 assets such as [Targeting Packs](https://github.com/dotnet/cli/issues/10006) and [Runtime Packs](https://github.com/dotnet/cli/issues/10007)</span></span>
  * <span data-ttu-id="3e111-117">针对 FrameworkReferences 的 NuGet 包和还原支持启用目标和运行时包引用- [#7342](https://github.com/NuGet/Home/issues/7342)</span><span class="sxs-lookup"><span data-stu-id="3e111-117">NuGet pack and restore support for FrameworkReferences to enable targeting and runtime package references - [#7342](https://github.com/NuGet/Home/issues/7342)</span></span>
  * <span data-ttu-id="3e111-118">支持 "仅下载" 包方案和 PackageDownload- [#7339](https://github.com/NuGet/Home/issues/7339)</span><span class="sxs-lookup"><span data-stu-id="3e111-118">Support "download only" package scenario with PackageDownload - [#7339](https://github.com/NuGet/Home/issues/7339)</span></span>
  * <span data-ttu-id="3e111-119">使用 PackageType 从搜索结果中排除运行时和目标包 & 还原图形- [#7337](https://github.com/NuGet/Home/issues/7337)</span><span class="sxs-lookup"><span data-stu-id="3e111-119">Exclude runtime and targeting packs from search results & restore graph using PackageType - [#7337](https://github.com/NuGet/Home/issues/7337)</span></span>

### <a name="issues-fixed-in-this-release"></a><span data-ttu-id="3e111-120">此版本修复的问题</span><span class="sxs-lookup"><span data-stu-id="3e111-120">Issues fixed in this release</span></span>

<span data-ttu-id="3e111-121">**Bug**</span><span class="sxs-lookup"><span data-stu-id="3e111-121">**Bugs**</span></span>

* <span data-ttu-id="3e111-122">插件：在创建插件期间丢失异常详细信息- [#8057](https://github.com/NuGet/Home/issues/8057)</span><span class="sxs-lookup"><span data-stu-id="3e111-122">Plugins:  exception details lost during plugin creation - [#8057](https://github.com/NuGet/Home/issues/8057)</span></span>

* <span data-ttu-id="3e111-123">如果某个源上存在下限，则具有互斥下限的 PackageReference 范围将不起作用。</span><span class="sxs-lookup"><span data-stu-id="3e111-123">PackageReference range with exclusive lower bound does not work if the lower bound is present on one of the sources.</span></span><span data-ttu-id="3e111-124"> - [#8054](https://github.com/NuGet/Home/issues/8054)</span><span class="sxs-lookup"><span data-stu-id="3e111-124"> - [#8054](https://github.com/NuGet/Home/issues/8054)</span></span>

* <span data-ttu-id="3e111-125">提高 IsPackableFalseError 消息 [#8021](https://github.com/NuGet/Home/issues/8021)</span><span class="sxs-lookup"><span data-stu-id="3e111-125">Improve IsPackableFalseError message - [#8021](https://github.com/NuGet/Home/issues/8021)</span></span>

* <span data-ttu-id="3e111-126">包锁定文件-在项目关系图发生更改时重新生成锁定文件- [#8019](https://github.com/NuGet/Home/issues/8019)</span><span class="sxs-lookup"><span data-stu-id="3e111-126">Packages Lock File - regenerate lock file when project graph changes - [#8019](https://github.com/NuGet/Home/issues/8019)</span></span>

* <span data-ttu-id="3e111-127">ProjectSystem bug：已自动删除 Nuget 包- [#8017](https://github.com/NuGet/Home/issues/8017)</span><span class="sxs-lookup"><span data-stu-id="3e111-127">ProjectSystem bug: Nuget Packages getting auto removed - [#8017](https://github.com/NuGet/Home/issues/8017)</span></span>

* <span data-ttu-id="3e111-128">添加用于返回 FrameworkReference 的目标，类似于 CollectPackageDownloads 和 CollectPackageReferences [#8005](https://github.com/NuGet/Home/issues/8005)</span><span class="sxs-lookup"><span data-stu-id="3e111-128">Add a target for returning the FrameworkReference similar to CollectPackageDownloads and CollectPackageReferences - [#8005](https://github.com/NuGet/Home/issues/8005)</span></span>

* <span data-ttu-id="3e111-129">HTTP 缓存： RepositoryResources 资源未按版本控制方式缓存- [#7997](https://github.com/NuGet/Home/issues/7997)</span><span class="sxs-lookup"><span data-stu-id="3e111-129">HTTP cache:  RepositoryResources resource is not cached in a versioned way - [#7997](https://github.com/NuGet/Home/issues/7997)</span></span>

* <span data-ttu-id="3e111-130">日志记录：不会报告异常调用堆栈详细详细信息- [#7955](https://github.com/NuGet/Home/issues/7955)</span><span class="sxs-lookup"><span data-stu-id="3e111-130">Logging:  exception callstacks are not reported with detailed verbosity - [#7955](https://github.com/NuGet/Home/issues/7955)</span></span>

* <span data-ttu-id="3e111-131">更改所有 NuGet 文档 Url 以使用 HTTPS- [#7950](https://github.com/NuGet/Home/issues/7950)</span><span class="sxs-lookup"><span data-stu-id="3e111-131">Change all NuGet Docs URLs to use HTTPS - [#7950](https://github.com/NuGet/Home/issues/7950)</span></span>

* <span data-ttu-id="3e111-132">提高 NU3024 警告消息 [#7933](https://github.com/NuGet/Home/issues/7933)</span><span class="sxs-lookup"><span data-stu-id="3e111-132">Improve NU3024 warning message - [#7933](https://github.com/NuGet/Home/issues/7933)</span></span>

* <span data-ttu-id="3e111-133">删除 packagereference 时锁定文件未更新- [#7930](https://github.com/NuGet/Home/issues/7930)</span><span class="sxs-lookup"><span data-stu-id="3e111-133">lock file not updating when packagereference removed - [#7930](https://github.com/NuGet/Home/issues/7930)</span></span>

* <span data-ttu-id="3e111-134">改善在 nuspec 中验证 licenseurl 和 license 元素时处理的错误情况处理 [#7915](https://github.com/NuGet/Home/issues/7915)</span><span class="sxs-lookup"><span data-stu-id="3e111-134">Improve the error case handling when validating licenseurl and license element in nuspec - [#7915](https://github.com/NuGet/Home/issues/7915)</span></span>

* <span data-ttu-id="3e111-135">PM UI-右键单击选项卡标题，并单击 "打开文件位置" 会导致错误- [#7913](https://github.com/NuGet/Home/issues/7913)</span><span class="sxs-lookup"><span data-stu-id="3e111-135">PM UI - right click on tab header and clicking "Open file location" results in error - [#7913](https://github.com/NuGet/Home/issues/7913)</span></span>

* <span data-ttu-id="3e111-136">插件：插件进程退出时的日志- [#7907](https://github.com/NuGet/Home/issues/7907)</span><span class="sxs-lookup"><span data-stu-id="3e111-136">Plugins:  log when plugin process exits - [#7907](https://github.com/NuGet/Home/issues/7907)</span></span>

* <span data-ttu-id="3e111-137">插件：记录日期时间值的高冲突率- [#7899](https://github.com/NuGet/Home/issues/7899)</span><span class="sxs-lookup"><span data-stu-id="3e111-137">Plugins:  high collision rate in logging datetime values - [#7899](https://github.com/NuGet/Home/issues/7899)</span></span>

* <span data-ttu-id="3e111-138">System.xml.linq.xnode.readfrom 在具有 LicenseExpression [#7894](https://github.com/NuGet/Home/issues/7894)的任何 nuspec 上失败</span><span class="sxs-lookup"><span data-stu-id="3e111-138">Manifest.ReadFrom fails on any nuspec with LicenseExpression - [#7894](https://github.com/NuGet/Home/issues/7894)</span></span>

* <span data-ttu-id="3e111-139">RestoreLockedMode：当 ProjectReference 引用具有自定义 AssemblyName [#7889](https://github.com/NuGet/Home/issues/7889)的项目时，意外 NU1004</span><span class="sxs-lookup"><span data-stu-id="3e111-139">RestoreLockedMode: Unexpected NU1004 when ProjectReference refers to a project with custom AssemblyName - [#7889](https://github.com/NuGet/Home/issues/7889)</span></span>

* <span data-ttu-id="3e111-140">如果插件启动失败并出现异常，则提供更好的错误消息- [#7857](https://github.com/NuGet/Home/issues/7857)</span><span class="sxs-lookup"><span data-stu-id="3e111-140">Better error message when the plugin startup fails with an exception - [#7857](https://github.com/NuGet/Home/issues/7857)</span></span>

* <span data-ttu-id="3e111-141">执行 NoOp 还原时，请避免 \* .dgspec.js在 obj 目录中写入 [#7854](https://github.com/NuGet/Home/issues/7854)</span><span class="sxs-lookup"><span data-stu-id="3e111-141">When doing a NoOp restore, avoid \*.dgspec.json write in obj directory - [#7854](https://github.com/NuGet/Home/issues/7854)</span></span>

* <span data-ttu-id="3e111-142">GeneratePathProperty = true 生成属性时失败，大小写不匹配- [#7843](https://github.com/NuGet/Home/issues/7843)</span><span class="sxs-lookup"><span data-stu-id="3e111-142">GeneratePathProperty=true fails to generate property on case mismatch - [#7843](https://github.com/NuGet/Home/issues/7843)</span></span>

* <span data-ttu-id="3e111-143">设置：包源路径中的非法字符会导致与[#7820](https://github.com/NuGet/Home/issues/7820)崩溃</span><span class="sxs-lookup"><span data-stu-id="3e111-143">Settings:  illegal character in package source path can crash VS - [#7820](https://github.com/NuGet/Home/issues/7820)</span></span>

* <span data-ttu-id="3e111-144">如果删除了 "锁定文件"，则还原不会在 NoOp 上生成锁定文件- [#7807](https://github.com/NuGet/Home/issues/7807)</span><span class="sxs-lookup"><span data-stu-id="3e111-144">If lock file is deleted, restore does not generate lock file on NoOp  - [#7807](https://github.com/NuGet/Home/issues/7807)</span></span>

* <span data-ttu-id="3e111-145">许可证 URL 和许可证会导致元数据的读取错误- [#7547](https://github.com/NuGet/Home/issues/7547)</span><span class="sxs-lookup"><span data-stu-id="3e111-145">License URL and license causes read error with Metadata - [#7547](https://github.com/NuGet/Home/issues/7547)</span></span>

* <span data-ttu-id="3e111-146">V2FeedParser 中的未处理异常- [#7523](https://github.com/NuGet/Home/issues/7523)</span><span class="sxs-lookup"><span data-stu-id="3e111-146">Unhandled exceptions in V2FeedParser - [#7523](https://github.com/NuGet/Home/issues/7523)</span></span>

* <span data-ttu-id="3e111-147">nuget.exe 返回无效参数的退出代码零- [#7178](https://github.com/NuGet/Home/issues/7178)</span><span class="sxs-lookup"><span data-stu-id="3e111-147">nuget.exe returns exit code zero for invalid arguments - [#7178](https://github.com/NuGet/Home/issues/7178)</span></span>

* <span data-ttu-id="3e111-148">更新错误和警告文档，以反映与签名相关的方案- [#6498](https://github.com/NuGet/Home/issues/6498)</span><span class="sxs-lookup"><span data-stu-id="3e111-148">Update Errors and warning docs to reflect signing related scenarios - [#6498](https://github.com/NuGet/Home/issues/6498)</span></span>

* <span data-ttu-id="3e111-149">资产文件应使用相对路径来更轻松地移动项目- [#4582](https://github.com/NuGet/Home/issues/4582)</span><span class="sxs-lookup"><span data-stu-id="3e111-149">Assets file should use relative paths to enable moving projects more easily - [#4582](https://github.com/NuGet/Home/issues/4582)</span></span>

<span data-ttu-id="3e111-150">**DCR**</span><span class="sxs-lookup"><span data-stu-id="3e111-150">**DCRs**</span></span>

* <span data-ttu-id="3e111-151">插件：启用诊断日志记录- [#7859](https://github.com/NuGet/Home/issues/7859)</span><span class="sxs-lookup"><span data-stu-id="3e111-151">Plugins:  enable diagnostic logging - [#7859](https://github.com/NuGet/Home/issues/7859)</span></span>

* <span data-ttu-id="3e111-152">使 Tizen 6 映射到 NetStandard 2.1- [#7773](https://github.com/NuGet/Home/issues/7773)</span><span class="sxs-lookup"><span data-stu-id="3e111-152">Make Tizen 6 map to NetStandard 2.1 - [#7773](https://github.com/NuGet/Home/issues/7773)</span></span>

<span data-ttu-id="3e111-153">**[此版本中已修复的所有问题的列表-5.1 RTM](https://github.com/nuget/home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%225.1")**</span><span class="sxs-lookup"><span data-stu-id="3e111-153">**[List of all issues fixed in this release - 5.1 RTM](https://github.com/nuget/home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%225.1")**</span></span>
