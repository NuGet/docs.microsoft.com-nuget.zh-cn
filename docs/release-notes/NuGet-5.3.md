---
title: NuGet 5.3 发行说明
description: NuGet 5.3 的发行说明，包括新功能、bug 修复和 Dcr。
author: karann-msft
ms.author: karann
ms.date: 09/06/2019
ms.topic: conceptual
ms.openlocfilehash: f16bfe5481009f7924a61f03233d288d25ac618f
ms.sourcegitcommit: f4bfdbf62302c95f1f39e81ccf998f8bbc6d56b0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/06/2019
ms.locfileid: "70774085"
---
# <a name="nuget-53-release-notes"></a><span data-ttu-id="c2edf-103">NuGet 5.3 发行说明</span><span class="sxs-lookup"><span data-stu-id="c2edf-103">NuGet 5.3 Release Notes</span></span>

<span data-ttu-id="c2edf-104">NuGet 分发车辆：</span><span class="sxs-lookup"><span data-stu-id="c2edf-104">NuGet distribution vehicles:</span></span>

| <span data-ttu-id="c2edf-105">NuGet 版本</span><span class="sxs-lookup"><span data-stu-id="c2edf-105">NuGet version</span></span> | <span data-ttu-id="c2edf-106">适用于 Visual Studio 版本</span><span class="sxs-lookup"><span data-stu-id="c2edf-106">Available in Visual Studio version</span></span>| <span data-ttu-id="c2edf-107">适用于 .NET SDK</span><span class="sxs-lookup"><span data-stu-id="c2edf-107">Available in .NET SDK(s)</span></span>|
|:---|:---|:---|
| [<span data-ttu-id="c2edf-108">**5.3.0-preview3**</span><span class="sxs-lookup"><span data-stu-id="c2edf-108">**5.3.0-preview3**</span></span>](https://nuget.org/downloads) | [<span data-ttu-id="c2edf-109">Visual Studio 2019 版本16.3 预览版3</span><span class="sxs-lookup"><span data-stu-id="c2edf-109">Visual Studio 2019 version 16.3 Preview 3</span></span>](https://visualstudio.microsoft.com/vs/preview/) | <span data-ttu-id="c2edf-110">[3.0.100-preview9](https://dotnet.microsoft.com/download/dotnet-core/3.0)<sup>1</sup></span><span class="sxs-lookup"><span data-stu-id="c2edf-110">[3.0.100-preview9](https://dotnet.microsoft.com/download/dotnet-core/3.0)<sup>1</sup></span></span> |

<span data-ttu-id="c2edf-111"><sup>1</sup>随 Visual Studio 2019 with .NET Core 工作负载一起安装</span><span class="sxs-lookup"><span data-stu-id="c2edf-111"><sup>1</sup>Installed with Visual Studio 2019 with .NET Core workload</span></span>

## <a name="summary-whats-new-in-53-preview-3"></a><span data-ttu-id="c2edf-112">摘要:5.3 preview 3 中的新增功能</span><span class="sxs-lookup"><span data-stu-id="c2edf-112">Summary: What's New in 5.3 preview 3</span></span>

* <span data-ttu-id="c2edf-113">[包图标可以嵌入到包中](../reference/msbuild-targets.md#packing-an-icon-image-file)，而无需使用外部 URL。</span><span class="sxs-lookup"><span data-stu-id="c2edf-113">[Package Icon can be embedded in the package](../reference/msbuild-targets.md#packing-an-icon-image-file), instead of needing an external URL.</span></span><span data-ttu-id="c2edf-114"> - [#352](https://github.com/NuGet/Home/issues/352)</span><span class="sxs-lookup"><span data-stu-id="c2edf-114"> - [#352](https://github.com/NuGet/Home/issues/352)</span></span>

* <span data-ttu-id="c2edf-115">提高了对包的 SHA 跟踪和强制执行的安全性- [#7281](https://github.com/NuGet/Home/issues/7281)</span><span class="sxs-lookup"><span data-stu-id="c2edf-115">Improved security with SHA tracking and enforcement for Packages.Config - [#7281](https://github.com/NuGet/Home/issues/7281)</span></span>

### <a name="issues-fixed-in-this-release"></a><span data-ttu-id="c2edf-116">此版本中已修复的问题</span><span class="sxs-lookup"><span data-stu-id="c2edf-116">Issues fixed in this release</span></span>

<span data-ttu-id="c2edf-117">**Bug**</span><span class="sxs-lookup"><span data-stu-id="c2edf-117">**Bugs**</span></span>

* <span data-ttu-id="c2edf-118">VS：程序集是完全 ngen-ed，而不是部分 ngen- [#8513](https://github.com/NuGet/Home/issues/8513)</span><span class="sxs-lookup"><span data-stu-id="c2edf-118">VS: assemblies are fully ngen-ed not partially ngen-ed - [#8513](https://github.com/NuGet/Home/issues/8513)</span></span>

* <span data-ttu-id="c2edf-119">减少内存使用量（取消订阅事件）- [#8471](https://github.com/NuGet/Home/issues/8471)</span><span class="sxs-lookup"><span data-stu-id="c2edf-119">Reduce memory usage (unsubscribe from events) - [#8471](https://github.com/NuGet/Home/issues/8471)</span></span>

* <span data-ttu-id="c2edf-120">"Error_UnableToFindProjectInfo" 消息的语法不正确- [#8441](https://github.com/NuGet/Home/issues/8441)</span><span class="sxs-lookup"><span data-stu-id="c2edf-120">"Error_UnableToFindProjectInfo" message is not grammatically correct - [#8441](https://github.com/NuGet/Home/issues/8441)</span></span>

* <span data-ttu-id="c2edf-121">NU1403 改进-验证所有包，包括预期/实际 sha 值- [#8424](https://github.com/NuGet/Home/issues/8424)</span><span class="sxs-lookup"><span data-stu-id="c2edf-121">NU1403 improvements - validate all packages, include the expected/actual sha values - [#8424](https://github.com/NuGet/Home/issues/8424)</span></span>

* <span data-ttu-id="c2edf-122">NuGetPackageManager. PreviewUpdatePackagesAsync 中的多个枚举- [#8401](https://github.com/NuGet/Home/issues/8401)</span><span class="sxs-lookup"><span data-stu-id="c2edf-122">Multiple enumeration in NuGetPackageManager.PreviewUpdatePackagesAsync - [#8401](https://github.com/NuGet/Home/issues/8401)</span></span>

* <span data-ttu-id="c2edf-123">恢复 Pluginprocess.exe 中的 "公共 > 内部" 更改- [#8390](https://github.com/NuGet/Home/issues/8390)</span><span class="sxs-lookup"><span data-stu-id="c2edf-123">Revert "public -> internal" change in PluginProcess - [#8390](https://github.com/NuGet/Home/issues/8390)</span></span>

* <span data-ttu-id="c2edf-124">IVsPackageSourceProvider. GetSources （...）的异常行为定义错误- [#8383](https://github.com/NuGet/Home/issues/8383)</span><span class="sxs-lookup"><span data-stu-id="c2edf-124">IVsPackageSourceProvider.GetSources(…) has ill-defined exception behavior - [#8383](https://github.com/NuGet/Home/issues/8383)</span></span>

* <span data-ttu-id="c2edf-125">使 PluginManager 构造函数再次公开- [#8379](https://github.com/NuGet/Home/issues/8379)</span><span class="sxs-lookup"><span data-stu-id="c2edf-125">Make PluginManager constructor public again - [#8379](https://github.com/NuGet/Home/issues/8379)</span></span>

* <span data-ttu-id="c2edf-126">用于跟踪 PM UI 的刷新速率的指标- [#8369](https://github.com/NuGet/Home/issues/8369)</span><span class="sxs-lookup"><span data-stu-id="c2edf-126">Metrics to track the refresh rate of the PM UI - [#8369](https://github.com/NuGet/Home/issues/8369)</span></span>

* <span data-ttu-id="c2edf-127">通过包管理器 UI 安装时减少 UI 刷新的次数- [#8358](https://github.com/NuGet/Home/issues/8358)</span><span class="sxs-lookup"><span data-stu-id="c2edf-127">Decrease the number of UI refreshes when installing through the Package Manager UI - [#8358](https://github.com/NuGet/Home/issues/8358)</span></span>

* <span data-ttu-id="c2edf-128">遥测： datetime 值使用特定于区域性的格式- [#8351](https://github.com/NuGet/Home/issues/8351)</span><span class="sxs-lookup"><span data-stu-id="c2edf-128">Telemetry:  datetime values use culture-specific formats - [#8351](https://github.com/NuGet/Home/issues/8351)</span></span>

* <span data-ttu-id="c2edf-129">减少包管理器 UI 的浏览选项卡中的 UI 刷新 #6570- [#8339](https://github.com/NuGet/Home/issues/8339)</span><span class="sxs-lookup"><span data-stu-id="c2edf-129">Reduce UI refreshes in browse tab of Package Manager UI #6570 - [#8339](https://github.com/NuGet/Home/issues/8339)</span></span>

* <span data-ttu-id="c2edf-130">[测试失败]"无法解析配置文件" 将提示两次[#8320](https://github.com/NuGet/Home/issues/8320)</span><span class="sxs-lookup"><span data-stu-id="c2edf-130">[Test Failure] “Unable to parse config file” will prompt twice - [#8320](https://github.com/NuGet/Home/issues/8320)</span></span>

* <span data-ttu-id="c2edf-131">向说明客户修补程序的良好文档页引发 NU5037 错误（包缺少所需的 nuspec 文件）- [#8291](https://github.com/NuGet/Home/issues/8291)</span><span class="sxs-lookup"><span data-stu-id="c2edf-131">Raise NU5037 error with good doc page that explains customer fixes (The package is missing the required nuspec file) - [#8291](https://github.com/NuGet/Home/issues/8291)</span></span>

* <span data-ttu-id="c2edf-132">更改项目的 Runtimeidentifiers 时，锁定模式还原失败- [#8260](https://github.com/NuGet/Home/issues/8260)</span><span class="sxs-lookup"><span data-stu-id="c2edf-132">Locked-mode restore fails when a project's RuntimeIdentifier is changed - [#8260](https://github.com/NuGet/Home/issues/8260)</span></span>

* <span data-ttu-id="c2edf-133">在 VS 懒惰[#8156](https://github.com/NuGet/Home/issues/8156)中进行设置读取</span><span class="sxs-lookup"><span data-stu-id="c2edf-133">Make the Settings reading in VS lazy - [#8156](https://github.com/NuGet/Home/issues/8156)</span></span>

* <span data-ttu-id="c2edf-134">"Nuget 源添加" 中的回归导致 "：" 字符（十六进制值0x3A）不能包含在名称 "errors- [#7948](https://github.com/NuGet/Home/issues/7948)</span><span class="sxs-lookup"><span data-stu-id="c2edf-134">Regression in 'Nuget sources add' causes "The ':' character, hexadecimal value 0x3A, cannot be included in a name" errors - [#7948](https://github.com/NuGet/Home/issues/7948)</span></span>

* <span data-ttu-id="c2edf-135">NuGet 插件凭据提供程序-隐藏进程窗口- [#7511](https://github.com/NuGet/Home/issues/7511)</span><span class="sxs-lookup"><span data-stu-id="c2edf-135">NuGet plugin credential providers - hide the process window - [#7511](https://github.com/NuGet/Home/issues/7511)</span></span>

* <span data-ttu-id="c2edf-136">强制 PackagePathResolver 是绝对路径[#7349](https://github.com/NuGet/Home/issues/7349)</span><span class="sxs-lookup"><span data-stu-id="c2edf-136">Enforce PackagePathResolver is an absolute path - [#7349](https://github.com/NuGet/Home/issues/7349)</span></span>

* <span data-ttu-id="c2edf-137">减少安装和更新包管理器 UI 的选项卡中的 UI 刷新- [#6570](https://github.com/NuGet/Home/issues/6570)</span><span class="sxs-lookup"><span data-stu-id="c2edf-137">Reduce UI refreshes in install and update tabs of Package Manager UI - [#6570](https://github.com/NuGet/Home/issues/6570)</span></span>

<span data-ttu-id="c2edf-138">**DCR：**</span><span class="sxs-lookup"><span data-stu-id="c2edf-138">**DCR:**</span></span>

* <span data-ttu-id="c2edf-139">更新 Xamarin framework 以映射到 NetStandard 2.1- [#8368](https://github.com/NuGet/Home/issues/8368)</span><span class="sxs-lookup"><span data-stu-id="c2edf-139">Update Xamarin frameworks to map to NetStandard 2.1 - [#8368](https://github.com/NuGet/Home/issues/8368)</span></span>

* <span data-ttu-id="c2edf-140">为安装/更新[#8324](https://github.com/NuGet/Home/issues/8324)启用包管理器 "预览窗口" 的内容复制</span><span class="sxs-lookup"><span data-stu-id="c2edf-140">Enable copying the contents of package manager "preview window" for install/update - [#8324](https://github.com/NuGet/Home/issues/8324)</span></span>

* <span data-ttu-id="c2edf-141">对 proj 文件启用还原- [#8212](https://github.com/NuGet/Home/issues/8212)</span><span class="sxs-lookup"><span data-stu-id="c2edf-141">Enable restore on .proj files - [#8212](https://github.com/NuGet/Home/issues/8212)</span></span>

* <span data-ttu-id="c2edf-142">同时`NUGET_NETFX_PLUGIN_PATHS`引入`NUGET_NETCORE_PLUGIN_PATHS`和，同时支持[#8151](https://github.com/NuGet/Home/issues/8151)的配置</span><span class="sxs-lookup"><span data-stu-id="c2edf-142">Introduce `NUGET_NETFX_PLUGIN_PATHS` and `NUGET_NETCORE_PLUGIN_PATHS` to support configuration of both at same time - [#8151](https://github.com/NuGet/Home/issues/8151)</span></span>

* <span data-ttu-id="c2edf-143">通过版本属性为 PackageDownload 启用多个版本- [#8074](https://github.com/NuGet/Home/issues/8074)</span><span class="sxs-lookup"><span data-stu-id="c2edf-143">Enable multiple versions for a PackageDownload via Version attribute - [#8074](https://github.com/NuGet/Home/issues/8074)</span></span>

* <span data-ttu-id="c2edf-144">将-SolutionDirectory 和-PackageDirectory 选项添加到 nuget.exe 包- [#7163](https://github.com/NuGet/Home/issues/7163)</span><span class="sxs-lookup"><span data-stu-id="c2edf-144">Add -SolutionDirectory and -PackageDirectory options to nuget.exe pack - [#7163](https://github.com/NuGet/Home/issues/7163)</span></span>

* <span data-ttu-id="c2edf-145">使 NuGet 包具有确定性[#6229](https://github.com/NuGet/Home/issues/6229)</span><span class="sxs-lookup"><span data-stu-id="c2edf-145">Enable NuGet Pack to be deterministic - [#6229](https://github.com/NuGet/Home/issues/6229)</span></span>

<span data-ttu-id="c2edf-146">**[此版本中已解决的所有问题的列表-5.3 预览版3](https://github.com/nuget/home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%225.3")**</span><span class="sxs-lookup"><span data-stu-id="c2edf-146">**[List of all issues fixed in this release - 5.3 preview 3](https://github.com/nuget/home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%225.3")**</span></span>
