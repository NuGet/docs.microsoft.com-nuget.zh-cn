---
title: NuGet 5.1 RTM 发行说明
description: 包括新功能、 bug 修复和 Dcr NuGet 5.1 发行说明。
author: karann-msft
ms.author: karann
ms.date: 05/21/2019
ms.topic: conceptual
ms.openlocfilehash: 384145947b19af6577dc1255985df1a361c72bb5
ms.sourcegitcommit: 0dea3b153ef823230a9d5f38351b7cef057cb299
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/12/2019
ms.locfileid: "67842579"
---
# <a name="nuget-51-release-notes"></a><span data-ttu-id="d807f-103">NuGet 5.1 发行说明</span><span class="sxs-lookup"><span data-stu-id="d807f-103">NuGet 5.1 Release Notes</span></span>

<span data-ttu-id="d807f-104">NuGet 分发车辆：</span><span class="sxs-lookup"><span data-stu-id="d807f-104">NuGet distribution vehicles:</span></span>

| <span data-ttu-id="d807f-105">NuGet 版本</span><span class="sxs-lookup"><span data-stu-id="d807f-105">NuGet version</span></span> | <span data-ttu-id="d807f-106">适用于 Visual Studio 版本</span><span class="sxs-lookup"><span data-stu-id="d807f-106">Available in Visual Studio version</span></span>| <span data-ttu-id="d807f-107">适用于 .NET SDK</span><span class="sxs-lookup"><span data-stu-id="d807f-107">Available in .NET SDK(s)</span></span>|
|:---|:---|:---|
| [<span data-ttu-id="d807f-108">**5.1.0**</span><span class="sxs-lookup"><span data-stu-id="d807f-108">**5.1.0**</span></span>](https://nuget.org/downloads) | [<span data-ttu-id="d807f-109">Visual Studio 2019 版本 16.1</span><span class="sxs-lookup"><span data-stu-id="d807f-109">Visual Studio 2019 version 16.1</span></span>](https://visualstudio.microsoft.com/downloads/) | <span data-ttu-id="d807f-110">[2.1.70X](https://dotnet.microsoft.com/download/dotnet-core/2.1)<sup>1</sup>， [2.2.30X](https://dotnet.microsoft.com/download/dotnet-core/2.2)<sup>2</sup></span><span class="sxs-lookup"><span data-stu-id="d807f-110">[2.1.70X](https://dotnet.microsoft.com/download/dotnet-core/2.1)<sup>1</sup>, [2.2.30X](https://dotnet.microsoft.com/download/dotnet-core/2.2)<sup>2</sup></span></span> |

<span data-ttu-id="d807f-111"><sup>1</sup>随 Visual Studio 2019 一起安装.NET Core 工作负载</span><span class="sxs-lookup"><span data-stu-id="d807f-111"><sup>1</sup>Installed with Visual Studio 2019 with .NET Core workload</span></span> 

<span data-ttu-id="d807f-112"><sup>2</sup>作为可选安装随.NET Core 工作负载的 Visual Studio 2019</span><span class="sxs-lookup"><span data-stu-id="d807f-112"><sup>2</sup>Available as an optional install with Visual Studio 2019 with .NET Core workload</span></span>

## <a name="summary-whats-new-in-51"></a><span data-ttu-id="d807f-113">摘要:什么是 5.1 中的新增功能</span><span class="sxs-lookup"><span data-stu-id="d807f-113">Summary: What's New in 5.1</span></span>

* <span data-ttu-id="d807f-114">支持要跳过包推送，如果已存在，更好地集成 CI/CD 工作流- [# 1630年](https://github.com/NuGet/Home/issues/1630#issuecomment-483461100)</span><span class="sxs-lookup"><span data-stu-id="d807f-114">Support to skip a package push if it already exists to allow for better integration with CI/CD workflows - [#1630](https://github.com/NuGet/Home/issues/1630#issuecomment-483461100)</span></span>

* <span data-ttu-id="d807f-115">Visual Studio 现在提供了方便指向包的 nuget.org 库页- [#5299](https://github.com/NuGet/Home/issues/5299#issuecomment-494458510)</span><span class="sxs-lookup"><span data-stu-id="d807f-115">Visual Studio now provides a convenient link to the the package's nuget.org gallery page - [#5299](https://github.com/NuGet/Home/issues/5299#issuecomment-494458510)</span></span>

* <span data-ttu-id="d807f-116">新的.NET Core 3.0 是资产的支持，如[目标包](https://github.com/dotnet/cli/issues/10006)和[运行时包](https://github.com/dotnet/cli/issues/10007)</span><span class="sxs-lookup"><span data-stu-id="d807f-116">Support for new .NET Core 3.0 assets such as [Targeting Packs](https://github.com/dotnet/cli/issues/10006) and [Runtime Packs](https://github.com/dotnet/cli/issues/10007)</span></span>
  * <span data-ttu-id="d807f-117">NuGet 包和还原的支持 FrameworkReferences 启用目标和运行时包引用- [#7342](https://github.com/NuGet/Home/issues/7342)</span><span class="sxs-lookup"><span data-stu-id="d807f-117">NuGet pack and restore support for FrameworkReferences to enable targeting and runtime package references - [#7342](https://github.com/NuGet/Home/issues/7342)</span></span>
  * <span data-ttu-id="d807f-118">支持"仅下载"包方案具有 PackageDownload- [#7339](https://github.com/NuGet/Home/issues/7339)</span><span class="sxs-lookup"><span data-stu-id="d807f-118">Support "download only" package scenario with PackageDownload - [#7339](https://github.com/NuGet/Home/issues/7339)</span></span>
  * <span data-ttu-id="d807f-119">排除运行时和目标从搜索结果和还原的包关系图使用 PackageType- [#7337](https://github.com/NuGet/Home/issues/7337)</span><span class="sxs-lookup"><span data-stu-id="d807f-119">Exlcude runtime and targeting packs from search results & restore graph using PackageType - [#7337](https://github.com/NuGet/Home/issues/7337)</span></span>

### <a name="issues-fixed-in-this-release"></a><span data-ttu-id="d807f-120">此版本中已修复的问题</span><span class="sxs-lookup"><span data-stu-id="d807f-120">Issues fixed in this release</span></span>

<span data-ttu-id="d807f-121">**Bug**</span><span class="sxs-lookup"><span data-stu-id="d807f-121">**Bugs**</span></span>

* <span data-ttu-id="d807f-122">插件： 插件期间的异常详细信息丢失[#8057](https://github.com/NuGet/Home/issues/8057)</span><span class="sxs-lookup"><span data-stu-id="d807f-122">Plugins:  exception details lost during plugin creation - [#8057](https://github.com/NuGet/Home/issues/8057)</span></span>

* <span data-ttu-id="d807f-123">PackageReference 范围排他下限不适如果下限中存在，其中一个源。</span><span class="sxs-lookup"><span data-stu-id="d807f-123">PackageReference range with exclusive lower bound does not work if the lower bound is present on one of the sources.</span></span><span data-ttu-id="d807f-124"> - [#8054](https://github.com/NuGet/Home/issues/8054)</span><span class="sxs-lookup"><span data-stu-id="d807f-124"> - [#8054](https://github.com/NuGet/Home/issues/8054)</span></span>

* <span data-ttu-id="d807f-125">Improve IsPackableFalseError message - [#8021](https://github.com/NuGet/Home/issues/8021)</span><span class="sxs-lookup"><span data-stu-id="d807f-125">Improve IsPackableFalseError message - [#8021](https://github.com/NuGet/Home/issues/8021)</span></span>

* <span data-ttu-id="d807f-126">包锁定文件的项目图发生更改时，请重新生成锁文件- [#8019](https://github.com/NuGet/Home/issues/8019)</span><span class="sxs-lookup"><span data-stu-id="d807f-126">Packages Lock File - regenerate lock file when project graph changes - [#8019](https://github.com/NuGet/Home/issues/8019)</span></span>

* <span data-ttu-id="d807f-127">ProjectSystem bug:Nuget 包获取自动删除- [#8017](https://github.com/NuGet/Home/issues/8017)</span><span class="sxs-lookup"><span data-stu-id="d807f-127">ProjectSystem bug: Nuget Packages getting auto removed - [#8017](https://github.com/NuGet/Home/issues/8017)</span></span>

* <span data-ttu-id="d807f-128">添加用于返回 FrameworkReference 目标类似于 CollectPackageDownloads 和 CollectPackageReferences- [#8005](https://github.com/NuGet/Home/issues/8005)</span><span class="sxs-lookup"><span data-stu-id="d807f-128">Add a target for returning the FrameworkReference similar to CollectPackageDownloads and CollectPackageReferences - [#8005](https://github.com/NuGet/Home/issues/8005)</span></span>

* <span data-ttu-id="d807f-129">HTTP 缓存：RepositoryResources 资源未缓存的版本控制的方式- [#7997](https://github.com/NuGet/Home/issues/7997)</span><span class="sxs-lookup"><span data-stu-id="d807f-129">HTTP cache:  RepositoryResources resource is not cached in a versioned way - [#7997](https://github.com/NuGet/Home/issues/7997)</span></span>

* <span data-ttu-id="d807f-130">日志记录： 异常调用堆栈未报告详细- [#7955](https://github.com/NuGet/Home/issues/7955)</span><span class="sxs-lookup"><span data-stu-id="d807f-130">Logging:  exception callstacks are not reported with detailed verbosity - [#7955](https://github.com/NuGet/Home/issues/7955)</span></span>

* <span data-ttu-id="d807f-131">更改为使用 HTTPS-的所有 NuGet Docs Url [#7950](https://github.com/NuGet/Home/issues/7950)</span><span class="sxs-lookup"><span data-stu-id="d807f-131">Change all NuGet Docs URLs to use HTTPS - [#7950](https://github.com/NuGet/Home/issues/7950)</span></span>

* <span data-ttu-id="d807f-132">提高 NU3024 警告消息- [#7933](https://github.com/NuGet/Home/issues/7933)</span><span class="sxs-lookup"><span data-stu-id="d807f-132">Improve NU3024 warning message - [#7933](https://github.com/NuGet/Home/issues/7933)</span></span>

* <span data-ttu-id="d807f-133">锁定文件未更新时删除了-packagereference [#7930](https://github.com/NuGet/Home/issues/7930)</span><span class="sxs-lookup"><span data-stu-id="d807f-133">lock file not updating when packagereference removed - [#7930](https://github.com/NuGet/Home/issues/7930)</span></span>

* <span data-ttu-id="d807f-134">验证 licenseurl 和许可证 nuspec-中的元素时改进错误 case 处理[#7915](https://github.com/NuGet/Home/issues/7915)</span><span class="sxs-lookup"><span data-stu-id="d807f-134">Improve the error case handling when validating licenseurl and license element in nuspec - [#7915](https://github.com/NuGet/Home/issues/7915)</span></span>

* <span data-ttu-id="d807f-135">PM UI-右键单击选项卡标头，并单击"打开文件位置"错误-生成[#7913](https://github.com/NuGet/Home/issues/7913)</span><span class="sxs-lookup"><span data-stu-id="d807f-135">PM UI - right click on tab header and clicking "Open file location" results in error - [#7913](https://github.com/NuGet/Home/issues/7913)</span></span>

* <span data-ttu-id="d807f-136">插件： 日志时插件进程退出的[#7907](https://github.com/NuGet/Home/issues/7907)</span><span class="sxs-lookup"><span data-stu-id="d807f-136">Plugins:  log when plugin process exits - [#7907](https://github.com/NuGet/Home/issues/7907)</span></span>

* <span data-ttu-id="d807f-137">插件： 在日志记录的日期时间值的高冲突率[#7899](https://github.com/NuGet/Home/issues/7899)</span><span class="sxs-lookup"><span data-stu-id="d807f-137">Plugins:  high collision rate in logging datetime values - [#7899](https://github.com/NuGet/Home/issues/7899)</span></span>

* <span data-ttu-id="d807f-138">上与 LicenseExpression-任何 nuspec 失败 Manifest.ReadFrom [#7894](https://github.com/NuGet/Home/issues/7894)</span><span class="sxs-lookup"><span data-stu-id="d807f-138">Manifest.ReadFrom fails on any nuspec with LicenseExpression - [#7894](https://github.com/NuGet/Home/issues/7894)</span></span>

* <span data-ttu-id="d807f-139">RestoreLockedMode:意外的 NU1004 ProjectReference 引用具有自定义程序集名称的项目时[#7889](https://github.com/NuGet/Home/issues/7889)</span><span class="sxs-lookup"><span data-stu-id="d807f-139">RestoreLockedMode: Unexpected NU1004 when ProjectReference refers to a project with custom AssemblyName - [#7889](https://github.com/NuGet/Home/issues/7889)</span></span>

* <span data-ttu-id="d807f-140">更详细的错误消息时插件启动失败，异常- [#7857](https://github.com/NuGet/Home/issues/7857)</span><span class="sxs-lookup"><span data-stu-id="d807f-140">Better error message when the plugin startup fails with an exception - [#7857](https://github.com/NuGet/Home/issues/7857)</span></span>

* <span data-ttu-id="d807f-141">执行操作时 NoOp 还原，避免 \*。 在 obj 目录-dgspec.json 写[#7854](https://github.com/NuGet/Home/issues/7854)</span><span class="sxs-lookup"><span data-stu-id="d807f-141">When doing a NoOp restore, avoid \*.dgspec.json write in obj directory - [#7854](https://github.com/NuGet/Home/issues/7854)</span></span>

* <span data-ttu-id="d807f-142">GeneratePathProperty = true 无法生成在大小写不匹配的属性[#7843](https://github.com/NuGet/Home/issues/7843)</span><span class="sxs-lookup"><span data-stu-id="d807f-142">GeneratePathProperty=true fails to generate property on case mismatch - [#7843](https://github.com/NuGet/Home/issues/7843)</span></span>

* <span data-ttu-id="d807f-143">设置： 在包源路径中的非法字符可以导致 VS 崩溃- [#7820](https://github.com/NuGet/Home/issues/7820)</span><span class="sxs-lookup"><span data-stu-id="d807f-143">Settings:  illegal character in package source path can crash VS - [#7820](https://github.com/NuGet/Home/issues/7820)</span></span>

* <span data-ttu-id="d807f-144">如果删除锁定文件，还原不会生成 NoOp-上的锁定文件[#7807](https://github.com/NuGet/Home/issues/7807)</span><span class="sxs-lookup"><span data-stu-id="d807f-144">If lock file is deleted, restore does not generate lock file on NoOp  - [#7807](https://github.com/NuGet/Home/issues/7807)</span></span>

* <span data-ttu-id="d807f-145">许可证 URL 和许可证会导致读取错误与元数据- [#7547](https://github.com/NuGet/Home/issues/7547)</span><span class="sxs-lookup"><span data-stu-id="d807f-145">License URL and license causes read error with Metadata - [#7547](https://github.com/NuGet/Home/issues/7547)</span></span>

* <span data-ttu-id="d807f-146">未经处理的异常中 V2FeedParser- [#7523](https://github.com/NuGet/Home/issues/7523)</span><span class="sxs-lookup"><span data-stu-id="d807f-146">Unhandled exceptions in V2FeedParser - [#7523](https://github.com/NuGet/Home/issues/7523)</span></span>

* <span data-ttu-id="d807f-147">nuget.exe 返回退出代码为零的参数无效- [#7178](https://github.com/NuGet/Home/issues/7178)</span><span class="sxs-lookup"><span data-stu-id="d807f-147">nuget.exe returns exit code zero for invalid arguments - [#7178](https://github.com/NuGet/Home/issues/7178)</span></span>

* <span data-ttu-id="d807f-148">更新错误和警告文档以反映相关的签名方案- [#6498](https://github.com/NuGet/Home/issues/6498)</span><span class="sxs-lookup"><span data-stu-id="d807f-148">Update Errors and warning docs to reflect signing related scenarios - [#6498](https://github.com/NuGet/Home/issues/6498)</span></span>

* <span data-ttu-id="d807f-149">资产文件应该使用相对路径来更轻松地-启用移动项目[#4582](https://github.com/NuGet/Home/issues/4582)</span><span class="sxs-lookup"><span data-stu-id="d807f-149">Assets file should use relative paths to enable moving projects more easily - [#4582](https://github.com/NuGet/Home/issues/4582)</span></span>

<span data-ttu-id="d807f-150">**DCRs**</span><span class="sxs-lookup"><span data-stu-id="d807f-150">**DCRs**</span></span>

* <span data-ttu-id="d807f-151">插件： 启用诊断日志记录- [#7859](https://github.com/NuGet/Home/issues/7859)</span><span class="sxs-lookup"><span data-stu-id="d807f-151">Plugins:  enable diagnostic logging - [#7859](https://github.com/NuGet/Home/issues/7859)</span></span>

* <span data-ttu-id="d807f-152">请 Tizen 6 映射到 NetStandard 2.1- [#7773](https://github.com/NuGet/Home/issues/7773)</span><span class="sxs-lookup"><span data-stu-id="d807f-152">Make Tizen 6 map to NetStandard 2.1 - [#7773](https://github.com/NuGet/Home/issues/7773)</span></span>

<span data-ttu-id="d807f-153">**[在此版本的 5.1 RTM 中已解决所有问题的列表](https://github.com/nuget/home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%225.1")**</span><span class="sxs-lookup"><span data-stu-id="d807f-153">**[List of all issues fixed in this release - 5.1 RTM](https://github.com/nuget/home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%225.1")**</span></span>
