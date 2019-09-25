---
title: NuGet 5.3 发行说明
description: NuGet 5.3 的发行说明，包括新功能、bug 修复和 Dcr。
author: karann-msft
ms.author: karann
ms.date: 09/06/2019
ms.topic: conceptual
ms.openlocfilehash: 96d176beaa6b2f0c4f53488390e585b70c9ba846
ms.sourcegitcommit: 188ade66b7ac807ba1667c77cfb9325bf89a8a4a
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/24/2019
ms.locfileid: "71248164"
---
# <a name="nuget-53-release-notes"></a><span data-ttu-id="406d9-103">NuGet 5.3 发行说明</span><span class="sxs-lookup"><span data-stu-id="406d9-103">NuGet 5.3 Release Notes</span></span>

<span data-ttu-id="406d9-104">NuGet 分发车辆：</span><span class="sxs-lookup"><span data-stu-id="406d9-104">NuGet distribution vehicles:</span></span>

| <span data-ttu-id="406d9-105">NuGet 版本</span><span class="sxs-lookup"><span data-stu-id="406d9-105">NuGet version</span></span> | <span data-ttu-id="406d9-106">适用于 Visual Studio 版本</span><span class="sxs-lookup"><span data-stu-id="406d9-106">Available in Visual Studio version</span></span>| <span data-ttu-id="406d9-107">适用于 .NET SDK</span><span class="sxs-lookup"><span data-stu-id="406d9-107">Available in .NET SDK(s)</span></span>|
|:---|:---|:---|
| [<span data-ttu-id="406d9-108">**5.3.0**</span><span class="sxs-lookup"><span data-stu-id="406d9-108">**5.3.0**</span></span>](https://nuget.org/downloads) | [<span data-ttu-id="406d9-109">Visual Studio 2019 版本16。3</span><span class="sxs-lookup"><span data-stu-id="406d9-109">Visual Studio 2019 version 16.3</span></span>](https://visualstudio.microsoft.com/downloads/) | <span data-ttu-id="406d9-110">[3.0.100](https://dotnet.microsoft.com/download/dotnet-core/3.0)<sup>1</sup></span><span class="sxs-lookup"><span data-stu-id="406d9-110">[3.0.100](https://dotnet.microsoft.com/download/dotnet-core/3.0)<sup>1</sup></span></span> |

<span data-ttu-id="406d9-111"><sup>1</sup>随 Visual Studio 2019 with .NET Core 工作负载一起安装</span><span class="sxs-lookup"><span data-stu-id="406d9-111"><sup>1</sup>Installed with Visual Studio 2019 with .NET Core workload</span></span>

## <a name="summary-whats-new-in-53"></a><span data-ttu-id="406d9-112">摘要:5.3 中的新增功能</span><span class="sxs-lookup"><span data-stu-id="406d9-112">Summary: What's New in 5.3</span></span>

* <span data-ttu-id="406d9-113">[包图标可以嵌入到包中](../reference/msbuild-targets.md#packing-an-icon-image-file)，而无需使用外部 URL。</span><span class="sxs-lookup"><span data-stu-id="406d9-113">[Package Icon can be embedded in the package](../reference/msbuild-targets.md#packing-an-icon-image-file), instead of needing an external URL.</span></span><span data-ttu-id="406d9-114"> - [#352](https://github.com/NuGet/Home/issues/352)</span><span class="sxs-lookup"><span data-stu-id="406d9-114"> - [#352](https://github.com/NuGet/Home/issues/352)</span></span>

* <span data-ttu-id="406d9-115">提高了对包的 SHA 跟踪和强制执行的安全性- [#7281](https://github.com/NuGet/Home/issues/7281)</span><span class="sxs-lookup"><span data-stu-id="406d9-115">Improved security with SHA tracking and enforcement for Packages.Config - [#7281](https://github.com/NuGet/Home/issues/7281)</span></span>

### <a name="issues-fixed-in-this-release"></a><span data-ttu-id="406d9-116">此版本中已修复的问题</span><span class="sxs-lookup"><span data-stu-id="406d9-116">Issues fixed in this release</span></span>

<span data-ttu-id="406d9-117">**Bug**</span><span class="sxs-lookup"><span data-stu-id="406d9-117">**Bugs**</span></span>

* <span data-ttu-id="406d9-118">使用 3.0.100-preview9 SDK 生成的 NuGet 包不能由 2.2 SDK 用户使用 .。。具体取决于时区[#8603](https://github.com/NuGet/Home/issues/8603)</span><span class="sxs-lookup"><span data-stu-id="406d9-118">NuGet packages produced with 3.0.100-preview9 SDK cannot be used by 2.2 SDK users...depending on your timezone [#8603](https://github.com/NuGet/Home/issues/8603)</span></span>

* <span data-ttu-id="406d9-119">引号 "路径中的字符导致" 路径中的非法字符 " `nuget restore` [#8168](https://github.com/NuGet/Home/issues/8168)中的失败</span><span class="sxs-lookup"><span data-stu-id="406d9-119">Quote " characters in PATH cause "Illegal characters in path" failure in `nuget restore` [#8168](https://github.com/NuGet/Home/issues/8168)</span></span>

* <span data-ttu-id="406d9-120">VS：程序集是完全 ngen-ed，而不是部分 ngen- [#8513](https://github.com/NuGet/Home/issues/8513)</span><span class="sxs-lookup"><span data-stu-id="406d9-120">VS: assemblies are fully ngen-ed not partially ngen-ed - [#8513](https://github.com/NuGet/Home/issues/8513)</span></span>

* <span data-ttu-id="406d9-121">减少内存使用量（取消订阅事件）- [#8471](https://github.com/NuGet/Home/issues/8471)</span><span class="sxs-lookup"><span data-stu-id="406d9-121">Reduce memory usage (unsubscribe from events) - [#8471](https://github.com/NuGet/Home/issues/8471)</span></span>

* <span data-ttu-id="406d9-122">"Error_UnableToFindProjectInfo" 消息的语法不正确- [#8441](https://github.com/NuGet/Home/issues/8441)</span><span class="sxs-lookup"><span data-stu-id="406d9-122">"Error_UnableToFindProjectInfo" message is not grammatically correct - [#8441](https://github.com/NuGet/Home/issues/8441)</span></span>

* <span data-ttu-id="406d9-123">NU1403 改进-验证所有包，包括预期/实际 sha 值- [#8424](https://github.com/NuGet/Home/issues/8424)</span><span class="sxs-lookup"><span data-stu-id="406d9-123">NU1403 improvements - validate all packages, include the expected/actual sha values - [#8424](https://github.com/NuGet/Home/issues/8424)</span></span>

* <span data-ttu-id="406d9-124">[#8401](https://github.com/NuGet/Home/issues/8401)中的`NuGetPackageManager.PreviewUpdatePackagesAsync`  - 多个枚举</span><span class="sxs-lookup"><span data-stu-id="406d9-124">Multiple enumeration in `NuGetPackageManager.PreviewUpdatePackagesAsync` - [#8401](https://github.com/NuGet/Home/issues/8401)</span></span>

* <span data-ttu-id="406d9-125">恢复 Pluginprocess.exe 中的 "公共 > 内部" 更改- [#8390](https://github.com/NuGet/Home/issues/8390)</span><span class="sxs-lookup"><span data-stu-id="406d9-125">Revert "public -> internal" change in PluginProcess - [#8390](https://github.com/NuGet/Home/issues/8390)</span></span>

* <span data-ttu-id="406d9-126">IVsPackageSourceProvider. GetSources （...）的异常行为定义错误- [#8383](https://github.com/NuGet/Home/issues/8383)</span><span class="sxs-lookup"><span data-stu-id="406d9-126">IVsPackageSourceProvider.GetSources(…) has ill-defined exception behavior - [#8383](https://github.com/NuGet/Home/issues/8383)</span></span>

* <span data-ttu-id="406d9-127">使 PluginManager 构造函数再次公开- [#8379](https://github.com/NuGet/Home/issues/8379)</span><span class="sxs-lookup"><span data-stu-id="406d9-127">Make PluginManager constructor public again - [#8379](https://github.com/NuGet/Home/issues/8379)</span></span>

* <span data-ttu-id="406d9-128">用于跟踪 PM UI 的刷新速率的指标- [#8369](https://github.com/NuGet/Home/issues/8369)</span><span class="sxs-lookup"><span data-stu-id="406d9-128">Metrics to track the refresh rate of the PM UI - [#8369](https://github.com/NuGet/Home/issues/8369)</span></span>

* <span data-ttu-id="406d9-129">通过包管理器 UI 安装时减少 UI 刷新的次数- [#8358](https://github.com/NuGet/Home/issues/8358)</span><span class="sxs-lookup"><span data-stu-id="406d9-129">Decrease the number of UI refreshes when installing through the Package Manager UI - [#8358](https://github.com/NuGet/Home/issues/8358)</span></span>

* <span data-ttu-id="406d9-130">遥测： datetime 值使用特定于区域性的格式- [#8351](https://github.com/NuGet/Home/issues/8351)</span><span class="sxs-lookup"><span data-stu-id="406d9-130">Telemetry:  datetime values use culture-specific formats - [#8351](https://github.com/NuGet/Home/issues/8351)</span></span>

* <span data-ttu-id="406d9-131">减少包管理器 UI 的浏览选项卡中的 UI 刷新 #6570- [#8339](https://github.com/NuGet/Home/issues/8339)</span><span class="sxs-lookup"><span data-stu-id="406d9-131">Reduce UI refreshes in browse tab of Package Manager UI #6570 - [#8339](https://github.com/NuGet/Home/issues/8339)</span></span>

* <span data-ttu-id="406d9-132">[测试失败]"无法解析配置文件" 将提示两次[#8320](https://github.com/NuGet/Home/issues/8320)</span><span class="sxs-lookup"><span data-stu-id="406d9-132">[Test Failure] “Unable to parse config file” will prompt twice - [#8320](https://github.com/NuGet/Home/issues/8320)</span></span>

* <span data-ttu-id="406d9-133">向说明客户修补程序的良好文档页引发 NU5037 错误（包缺少所需的 nuspec 文件）- [#8291](https://github.com/NuGet/Home/issues/8291)</span><span class="sxs-lookup"><span data-stu-id="406d9-133">Raise NU5037 error with good doc page that explains customer fixes (The package is missing the required nuspec file) - [#8291](https://github.com/NuGet/Home/issues/8291)</span></span>

* <span data-ttu-id="406d9-134">更改项目的 Runtimeidentifiers 时，锁定模式还原失败- [#8260](https://github.com/NuGet/Home/issues/8260)</span><span class="sxs-lookup"><span data-stu-id="406d9-134">Locked-mode restore fails when a project's RuntimeIdentifier is changed - [#8260](https://github.com/NuGet/Home/issues/8260)</span></span>

* <span data-ttu-id="406d9-135">在 VS 懒惰[#8156](https://github.com/NuGet/Home/issues/8156)中进行设置读取</span><span class="sxs-lookup"><span data-stu-id="406d9-135">Make the Settings reading in VS lazy - [#8156](https://github.com/NuGet/Home/issues/8156)</span></span>

* <span data-ttu-id="406d9-136">中`Nuget sources add`的回归导致 "：" 字符（十六进制值0x3A）不能包含在名称 "errors- [#7948](https://github.com/NuGet/Home/issues/7948)</span><span class="sxs-lookup"><span data-stu-id="406d9-136">Regression in `Nuget sources add` causes "The ':' character, hexadecimal value 0x3A, cannot be included in a name" errors - [#7948](https://github.com/NuGet/Home/issues/7948)</span></span>

* <span data-ttu-id="406d9-137">NuGet 插件凭据提供程序-隐藏进程窗口- [#7511](https://github.com/NuGet/Home/issues/7511)</span><span class="sxs-lookup"><span data-stu-id="406d9-137">NuGet plugin credential providers - hide the process window - [#7511](https://github.com/NuGet/Home/issues/7511)</span></span>

* <span data-ttu-id="406d9-138">强制 PackagePathResolver 是绝对路径[#7349](https://github.com/NuGet/Home/issues/7349)</span><span class="sxs-lookup"><span data-stu-id="406d9-138">Enforce PackagePathResolver is an absolute path - [#7349](https://github.com/NuGet/Home/issues/7349)</span></span>

* <span data-ttu-id="406d9-139">减少安装和更新包管理器 UI 的选项卡中的 UI 刷新- [#6570](https://github.com/NuGet/Home/issues/6570)</span><span class="sxs-lookup"><span data-stu-id="406d9-139">Reduce UI refreshes in install and update tabs of Package Manager UI - [#6570](https://github.com/NuGet/Home/issues/6570)</span></span>

<span data-ttu-id="406d9-140">**DCR：**</span><span class="sxs-lookup"><span data-stu-id="406d9-140">**DCR:**</span></span>

* <span data-ttu-id="406d9-141">更新 Xamarin framework 以映射到 NetStandard 2.1- [#8368](https://github.com/NuGet/Home/issues/8368)</span><span class="sxs-lookup"><span data-stu-id="406d9-141">Update Xamarin frameworks to map to NetStandard 2.1 - [#8368](https://github.com/NuGet/Home/issues/8368)</span></span>

* <span data-ttu-id="406d9-142">为安装/更新[#8324](https://github.com/NuGet/Home/issues/8324)启用包管理器 "预览窗口" 的内容复制</span><span class="sxs-lookup"><span data-stu-id="406d9-142">Enable copying the contents of package manager "preview window" for install/update - [#8324](https://github.com/NuGet/Home/issues/8324)</span></span>

* <span data-ttu-id="406d9-143">对 proj 文件启用还原- [#8212](https://github.com/NuGet/Home/issues/8212)</span><span class="sxs-lookup"><span data-stu-id="406d9-143">Enable restore on .proj files - [#8212](https://github.com/NuGet/Home/issues/8212)</span></span>

* <span data-ttu-id="406d9-144">同时`NUGET_NETFX_PLUGIN_PATHS`引入`NUGET_NETCORE_PLUGIN_PATHS`和，同时支持[#8151](https://github.com/NuGet/Home/issues/8151)的配置</span><span class="sxs-lookup"><span data-stu-id="406d9-144">Introduce `NUGET_NETFX_PLUGIN_PATHS` and `NUGET_NETCORE_PLUGIN_PATHS` to support configuration of both at same time - [#8151](https://github.com/NuGet/Home/issues/8151)</span></span>

* <span data-ttu-id="406d9-145">通过版本属性为 PackageDownload 启用多个版本- [#8074](https://github.com/NuGet/Home/issues/8074)</span><span class="sxs-lookup"><span data-stu-id="406d9-145">Enable multiple versions for a PackageDownload via Version attribute - [#8074](https://github.com/NuGet/Home/issues/8074)</span></span>

* <span data-ttu-id="406d9-146">将-SolutionDirectory 和-PackageDirectory 选项添加到 nuget.exe 包- [#7163](https://github.com/NuGet/Home/issues/7163)</span><span class="sxs-lookup"><span data-stu-id="406d9-146">Add -SolutionDirectory and -PackageDirectory options to nuget.exe pack - [#7163](https://github.com/NuGet/Home/issues/7163)</span></span>

<span data-ttu-id="406d9-147">**[此版本中已修复的所有问题的列表-5。3](https://github.com/nuget/home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%225.3")**</span><span class="sxs-lookup"><span data-stu-id="406d9-147">**[List of all issues fixed in this release - 5.3](https://github.com/nuget/home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%225.3")**</span></span>
