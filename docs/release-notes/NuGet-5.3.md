---
title: NuGet 5.3 发行说明
description: NuGet 5.3 的发行说明，包括新功能、bug 修复和 Dcr。
author: JonDouglas
ms.author: jodou
ms.date: 09/06/2019
ms.topic: conceptual
ms.openlocfilehash: 009a219139a767ee6453305be68ccce478b0ec75
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/26/2021
ms.locfileid: "98780128"
---
# <a name="nuget-53-release-notes"></a><span data-ttu-id="bbc03-103">NuGet 5.3 发行说明</span><span class="sxs-lookup"><span data-stu-id="bbc03-103">NuGet 5.3 Release Notes</span></span>

<span data-ttu-id="bbc03-104">NuGet 分发车辆：</span><span class="sxs-lookup"><span data-stu-id="bbc03-104">NuGet distribution vehicles:</span></span>

| <span data-ttu-id="bbc03-105">NuGet 版本</span><span class="sxs-lookup"><span data-stu-id="bbc03-105">NuGet version</span></span> | <span data-ttu-id="bbc03-106">适用于 Visual Studio 版本</span><span class="sxs-lookup"><span data-stu-id="bbc03-106">Available in Visual Studio version</span></span>| <span data-ttu-id="bbc03-107">适用于 .NET SDK</span><span class="sxs-lookup"><span data-stu-id="bbc03-107">Available in .NET SDK(s)</span></span>|
|:---|:---|:---|
| [<span data-ttu-id="bbc03-108">**5.3.0**</span><span class="sxs-lookup"><span data-stu-id="bbc03-108">**5.3.0**</span></span>](https://nuget.org/downloads) | [<span data-ttu-id="bbc03-109">Visual Studio 2019 版本 16.3</span><span class="sxs-lookup"><span data-stu-id="bbc03-109">Visual Studio 2019 version 16.3</span></span>](https://visualstudio.microsoft.com/downloads/) | <span data-ttu-id="bbc03-110">[3.0.100](https://dotnet.microsoft.com/download/dotnet-core/3.0)<sup>1</sup></span><span class="sxs-lookup"><span data-stu-id="bbc03-110">[3.0.100](https://dotnet.microsoft.com/download/dotnet-core/3.0)<sup>1</sup></span></span> |
| [<span data-ttu-id="bbc03-111">**5.3.1**</span><span class="sxs-lookup"><span data-stu-id="bbc03-111">**5.3.1**</span></span>](https://nuget.org/downloads) | [<span data-ttu-id="bbc03-112">Visual Studio 2019 版本16.3。6</span><span class="sxs-lookup"><span data-stu-id="bbc03-112">Visual Studio 2019 version 16.3.6</span></span>](https://visualstudio.microsoft.com/downloads/) | [<span data-ttu-id="bbc03-113">未来版本：3.0.101</span><span class="sxs-lookup"><span data-stu-id="bbc03-113">Future version: 3.0.101</span></span>](https://dotnet.microsoft.com/download/dotnet-core/3.0) |

<span data-ttu-id="bbc03-114"><sup>1</sup>随 Visual Studio 2019 with .NET Core 工作负载一起安装</span><span class="sxs-lookup"><span data-stu-id="bbc03-114"><sup>1</sup>Installed with Visual Studio 2019 with .NET Core workload</span></span>

## <a name="summary-whats-new-in-53"></a><span data-ttu-id="bbc03-115">摘要：5.3 中的新增功能</span><span class="sxs-lookup"><span data-stu-id="bbc03-115">Summary: What's New in 5.3</span></span>

* <span data-ttu-id="bbc03-116">[包图标可以嵌入到包中](../reference/msbuild-targets.md#packing-an-icon-image-file)，而无需使用外部 URL。</span><span class="sxs-lookup"><span data-stu-id="bbc03-116">[Package Icon can be embedded in the package](../reference/msbuild-targets.md#packing-an-icon-image-file), instead of needing an external URL.</span></span><span data-ttu-id="bbc03-117"> - [#352](https://github.com/NuGet/Home/issues/352)</span><span class="sxs-lookup"><span data-stu-id="bbc03-117"> - [#352](https://github.com/NuGet/Home/issues/352)</span></span>

* <span data-ttu-id="bbc03-118">提高了针对 Packages.Config [#7281](https://github.com/NuGet/Home/issues/7281)的 SHA 跟踪和强制的安全性</span><span class="sxs-lookup"><span data-stu-id="bbc03-118">Improved security with SHA tracking and enforcement for Packages.Config - [#7281](https://github.com/NuGet/Home/issues/7281)</span></span>

* <span data-ttu-id="bbc03-119">启用过时/旧 NuGet 包的弃用[#2867](https://github.com/NuGet/Home/issues/2867)  |  [博客文章](https://devblogs.microsoft.com/nuget/deprecating-packages-on-nuget-org/)  |  [文档](../nuget-org/deprecate-packages.md)</span><span class="sxs-lookup"><span data-stu-id="bbc03-119">Enable deprecation of obsolete/legacy NuGet Packages [#2867](https://github.com/NuGet/Home/issues/2867) | [Blog post](https://devblogs.microsoft.com/nuget/deprecating-packages-on-nuget-org/) | [Docs](../nuget-org/deprecate-packages.md)</span></span>

### <a name="issues-fixed-in-this-release"></a><span data-ttu-id="bbc03-120">此版本中已修复的问题</span><span class="sxs-lookup"><span data-stu-id="bbc03-120">Issues fixed in this release</span></span>

<span data-ttu-id="bbc03-121">**Bug**</span><span class="sxs-lookup"><span data-stu-id="bbc03-121">**Bugs**</span></span>

* <span data-ttu-id="bbc03-122">使用 3.0.100-preview9 SDK 生成的 NuGet 包不能由 2.2 SDK 用户使用 .。。具体取决于时区 [#8603](https://github.com/NuGet/Home/issues/8603)</span><span class="sxs-lookup"><span data-stu-id="bbc03-122">NuGet packages produced with 3.0.100-preview9 SDK cannot be used by 2.2 SDK users...depending on your timezone [#8603](https://github.com/NuGet/Home/issues/8603)</span></span>

* <span data-ttu-id="bbc03-123">引号 "路径中的字符导致" 路径中的非法字符 " `nuget restore` [#8168](https://github.com/NuGet/Home/issues/8168)中的失败</span><span class="sxs-lookup"><span data-stu-id="bbc03-123">Quote " characters in PATH cause "Illegal characters in path" failure in `nuget restore` [#8168](https://github.com/NuGet/Home/issues/8168)</span></span>

* <span data-ttu-id="bbc03-124">VS：程序集是完全 ngen-ed，而不是部分 ngen- [#8513](https://github.com/NuGet/Home/issues/8513)</span><span class="sxs-lookup"><span data-stu-id="bbc03-124">VS: assemblies are fully ngen-ed not partially ngen-ed - [#8513](https://github.com/NuGet/Home/issues/8513)</span></span>

* <span data-ttu-id="bbc03-125">减少内存使用 (取消订阅事件) - [#8471](https://github.com/NuGet/Home/issues/8471)</span><span class="sxs-lookup"><span data-stu-id="bbc03-125">Reduce memory usage (unsubscribe from events) - [#8471](https://github.com/NuGet/Home/issues/8471)</span></span>

* <span data-ttu-id="bbc03-126">"Error_UnableToFindProjectInfo" 消息的语法不正确- [#8441](https://github.com/NuGet/Home/issues/8441)</span><span class="sxs-lookup"><span data-stu-id="bbc03-126">"Error_UnableToFindProjectInfo" message is not grammatically correct - [#8441](https://github.com/NuGet/Home/issues/8441)</span></span>

* <span data-ttu-id="bbc03-127">NU1403 改进-验证所有包，包括预期/实际 sha 值- [#8424](https://github.com/NuGet/Home/issues/8424)</span><span class="sxs-lookup"><span data-stu-id="bbc03-127">NU1403 improvements - validate all packages, include the expected/actual sha values - [#8424](https://github.com/NuGet/Home/issues/8424)</span></span>

* <span data-ttu-id="bbc03-128">#8401 中的多个枚举 `NuGetPackageManager.PreviewUpdatePackagesAsync`  -  [](https://github.com/NuGet/Home/issues/8401)</span><span class="sxs-lookup"><span data-stu-id="bbc03-128">Multiple enumeration in `NuGetPackageManager.PreviewUpdatePackagesAsync` - [#8401](https://github.com/NuGet/Home/issues/8401)</span></span>

* <span data-ttu-id="bbc03-129">恢复 Pluginprocess.exe 中的 "公共 > 内部" 更改- [#8390](https://github.com/NuGet/Home/issues/8390)</span><span class="sxs-lookup"><span data-stu-id="bbc03-129">Revert "public -> internal" change in PluginProcess - [#8390](https://github.com/NuGet/Home/issues/8390)</span></span>

* <span data-ttu-id="bbc03-130">IVsPackageSourceProvider. GetSources ( ) 具有错误定义的异常行为- [#8383](https://github.com/NuGet/Home/issues/8383)</span><span class="sxs-lookup"><span data-stu-id="bbc03-130">IVsPackageSourceProvider.GetSources(…) has ill-defined exception behavior - [#8383](https://github.com/NuGet/Home/issues/8383)</span></span>

* <span data-ttu-id="bbc03-131">使 PluginManager 构造函数再次公开- [#8379](https://github.com/NuGet/Home/issues/8379)</span><span class="sxs-lookup"><span data-stu-id="bbc03-131">Make PluginManager constructor public again - [#8379](https://github.com/NuGet/Home/issues/8379)</span></span>

* <span data-ttu-id="bbc03-132">用于跟踪 PM UI 的刷新速率的指标- [#8369](https://github.com/NuGet/Home/issues/8369)</span><span class="sxs-lookup"><span data-stu-id="bbc03-132">Metrics to track the refresh rate of the PM UI - [#8369](https://github.com/NuGet/Home/issues/8369)</span></span>

* <span data-ttu-id="bbc03-133">通过包管理器 UI 安装时减少 UI 刷新的次数- [#8358](https://github.com/NuGet/Home/issues/8358)</span><span class="sxs-lookup"><span data-stu-id="bbc03-133">Decrease the number of UI refreshes when installing through the Package Manager UI - [#8358](https://github.com/NuGet/Home/issues/8358)</span></span>

* <span data-ttu-id="bbc03-134">遥测： datetime 值使用特定于区域性的格式- [#8351](https://github.com/NuGet/Home/issues/8351)</span><span class="sxs-lookup"><span data-stu-id="bbc03-134">Telemetry:  datetime values use culture-specific formats - [#8351](https://github.com/NuGet/Home/issues/8351)</span></span>

* <span data-ttu-id="bbc03-135">减少包管理器 UI 的浏览选项卡中的 UI 刷新 #6570- [#8339](https://github.com/NuGet/Home/issues/8339)</span><span class="sxs-lookup"><span data-stu-id="bbc03-135">Reduce UI refreshes in browse tab of Package Manager UI #6570 - [#8339](https://github.com/NuGet/Home/issues/8339)</span></span>

* <span data-ttu-id="bbc03-136">[测试失败]"无法解析配置文件" 将提示两次 [#8320](https://github.com/NuGet/Home/issues/8320)</span><span class="sxs-lookup"><span data-stu-id="bbc03-136">[Test Failure] “Unable to parse config file” will prompt twice - [#8320](https://github.com/NuGet/Home/issues/8320)</span></span>

* <span data-ttu-id="bbc03-137">在 (包缺少所需的 nuspec 文件) 的良好文档页中引发 NU5037 错误 [#8291](https://github.com/NuGet/Home/issues/8291)</span><span class="sxs-lookup"><span data-stu-id="bbc03-137">Raise NU5037 error with good doc page that explains customer fixes (The package is missing the required nuspec file) - [#8291](https://github.com/NuGet/Home/issues/8291)</span></span>

* <span data-ttu-id="bbc03-138">更改项目的 Runtimeidentifiers 时，锁定模式还原失败- [#8260](https://github.com/NuGet/Home/issues/8260)</span><span class="sxs-lookup"><span data-stu-id="bbc03-138">Locked-mode restore fails when a project's RuntimeIdentifier is changed - [#8260](https://github.com/NuGet/Home/issues/8260)</span></span>

* <span data-ttu-id="bbc03-139">在 VS 懒惰[#8156](https://github.com/NuGet/Home/issues/8156)中进行设置读取</span><span class="sxs-lookup"><span data-stu-id="bbc03-139">Make the Settings reading in VS lazy - [#8156](https://github.com/NuGet/Home/issues/8156)</span></span>

* <span data-ttu-id="bbc03-140">中的回归 `Nuget sources add` 导致 "：" 字符（十六进制值0x3A）不能包含在名称 "errors- [#7948](https://github.com/NuGet/Home/issues/7948)</span><span class="sxs-lookup"><span data-stu-id="bbc03-140">Regression in `Nuget sources add` causes "The ':' character, hexadecimal value 0x3A, cannot be included in a name" errors - [#7948](https://github.com/NuGet/Home/issues/7948)</span></span>

* <span data-ttu-id="bbc03-141">NuGet 插件凭据提供程序-隐藏进程窗口- [#7511](https://github.com/NuGet/Home/issues/7511)</span><span class="sxs-lookup"><span data-stu-id="bbc03-141">NuGet plugin credential providers - hide the process window - [#7511](https://github.com/NuGet/Home/issues/7511)</span></span>

* <span data-ttu-id="bbc03-142">强制 PackagePathResolver 是绝对路径 [#7349](https://github.com/NuGet/Home/issues/7349)</span><span class="sxs-lookup"><span data-stu-id="bbc03-142">Enforce PackagePathResolver is an absolute path - [#7349](https://github.com/NuGet/Home/issues/7349)</span></span>

* <span data-ttu-id="bbc03-143">减少安装和更新包管理器 UI 的选项卡中的 UI 刷新- [#6570](https://github.com/NuGet/Home/issues/6570)</span><span class="sxs-lookup"><span data-stu-id="bbc03-143">Reduce UI refreshes in install and update tabs of Package Manager UI - [#6570](https://github.com/NuGet/Home/issues/6570)</span></span>

<span data-ttu-id="bbc03-144">**DCR:**</span><span class="sxs-lookup"><span data-stu-id="bbc03-144">**DCR:**</span></span>

* <span data-ttu-id="bbc03-145">更新 Xamarin framework 以映射到 NetStandard 2.1- [#8368](https://github.com/NuGet/Home/issues/8368)</span><span class="sxs-lookup"><span data-stu-id="bbc03-145">Update Xamarin frameworks to map to NetStandard 2.1 - [#8368](https://github.com/NuGet/Home/issues/8368)</span></span>

* <span data-ttu-id="bbc03-146">为安装/更新[#8324](https://github.com/NuGet/Home/issues/8324)启用包管理器 "预览窗口" 的内容复制</span><span class="sxs-lookup"><span data-stu-id="bbc03-146">Enable copying the contents of package manager "preview window" for install/update - [#8324](https://github.com/NuGet/Home/issues/8324)</span></span>

* <span data-ttu-id="bbc03-147">对 proj 文件启用还原- [#8212](https://github.com/NuGet/Home/issues/8212)</span><span class="sxs-lookup"><span data-stu-id="bbc03-147">Enable restore on .proj files - [#8212](https://github.com/NuGet/Home/issues/8212)</span></span>

* <span data-ttu-id="bbc03-148">同时引入 `NUGET_NETFX_PLUGIN_PATHS` 和 `NUGET_NETCORE_PLUGIN_PATHS` ，同时支持[#8151](https://github.com/NuGet/Home/issues/8151)的配置</span><span class="sxs-lookup"><span data-stu-id="bbc03-148">Introduce `NUGET_NETFX_PLUGIN_PATHS` and `NUGET_NETCORE_PLUGIN_PATHS` to support configuration of both at same time - [#8151](https://github.com/NuGet/Home/issues/8151)</span></span>

* <span data-ttu-id="bbc03-149">通过版本属性为 PackageDownload 启用多个版本- [#8074](https://github.com/NuGet/Home/issues/8074)</span><span class="sxs-lookup"><span data-stu-id="bbc03-149">Enable multiple versions for a PackageDownload via Version attribute - [#8074](https://github.com/NuGet/Home/issues/8074)</span></span>

* <span data-ttu-id="bbc03-150">将-SolutionDirectory 和-PackageDirectory 选项添加到 nuget.exe 包- [#7163](https://github.com/NuGet/Home/issues/7163)</span><span class="sxs-lookup"><span data-stu-id="bbc03-150">Add -SolutionDirectory and -PackageDirectory options to nuget.exe pack - [#7163](https://github.com/NuGet/Home/issues/7163)</span></span>

<span data-ttu-id="bbc03-151">**[此版本中已修复的所有问题的列表-5。3](https://github.com/nuget/home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%225.3")**</span><span class="sxs-lookup"><span data-stu-id="bbc03-151">**[List of all issues fixed in this release - 5.3](https://github.com/nuget/home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%225.3")**</span></span>

## <a name="summary-whats-new-in-531"></a><span data-ttu-id="bbc03-152">摘要：5.3.1 中的新增功能</span><span class="sxs-lookup"><span data-stu-id="bbc03-152">Summary: What's New in 5.3.1</span></span>

* <span data-ttu-id="bbc03-153">插件：任务被取消-不允许取消影响插件实例化- [#8648](https://github.com/NuGet/Home/issues/8648)</span><span class="sxs-lookup"><span data-stu-id="bbc03-153">Plugin: A task was canceled - don't let cancellations affect plugin instantiation - [#8648](https://github.com/NuGet/Home/issues/8648)</span></span>

* <span data-ttu-id="bbc03-154"> (使用凭据提供程序时，不能在一个进程中安全地运行两次还原任务) - [#8688](https://github.com/NuGet/Home/issues/8688)</span><span class="sxs-lookup"><span data-stu-id="bbc03-154">Restore Task cannot be safely run twice in one process (when Credential providers are used) - [#8688](https://github.com/NuGet/Home/issues/8688)</span></span>
