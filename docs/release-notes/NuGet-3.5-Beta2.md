---
title: 3.5 Beta2 发行说明
description: 包括已知的问题、 bug 修复、 新增的功能和 Dcr NuGet 3.5 Beta 2 的发行说明。
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 4b47939e2fafc11823c41a849b3c58bbf0800ada
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/04/2018
ms.locfileid: "43551986"
---
# <a name="nuget-35-beta2-release-notes"></a><span data-ttu-id="d215b-103">NuGet 3.5 Beta2 发行说明</span><span class="sxs-lookup"><span data-stu-id="d215b-103">NuGet 3.5 Beta2 Release Notes</span></span>

<span data-ttu-id="d215b-104">[NuGet 3.5 测试版发行说明](../release-notes/nuget-3.5-Beta.md) | [NuGet 3.5 RC 发行说明](../release-notes/nuget-3.5-RC.md)</span><span class="sxs-lookup"><span data-stu-id="d215b-104">[NuGet 3.5-Beta Release Notes](../release-notes/nuget-3.5-Beta.md) | [NuGet 3.5-RC Release Notes](../release-notes/nuget-3.5-RC.md)</span></span>

<span data-ttu-id="d215b-105">NuGet 3.5 Beta 2 RTM 发布了 2016 年 6 月 27 日，Visual Studio 2013 和 nuget.exe</span><span class="sxs-lookup"><span data-stu-id="d215b-105">NuGet 3.5 Beta 2 RTM was released June 27, 2016 for Visual Studio 2013 and nuget.exe</span></span>

[<span data-ttu-id="d215b-106">完整更改日志</span><span class="sxs-lookup"><span data-stu-id="d215b-106">Full Changelog</span></span>](https://github.com/NuGet/NuGet.Client/compare/release-3.5.0-beta...release-3.5.0-beta2)

[<span data-ttu-id="d215b-107">问题列表</span><span class="sxs-lookup"><span data-stu-id="d215b-107">Issues List</span></span>](https://github.com/Nuget/Home/issues?q=is%3Aissue+milestone%3A%223.5+Beta2%22+is%3Aclosed)

## <a name="bug-fixes"></a><span data-ttu-id="d215b-108">Bug 修复</span><span class="sxs-lookup"><span data-stu-id="d215b-108">Bug Fixes</span></span>

* <span data-ttu-id="d215b-109">更新的错误消息到不支持的已验证的源-.NET Core 中的密码 decrpytion [# 2942年](https://github.com/NuGet/Home/issues/2942)</span><span class="sxs-lookup"><span data-stu-id="d215b-109">Updated error message to lack of support for password decrpytion in .NET Core for authenticated feeds  - [#2942](https://github.com/NuGet/Home/issues/2942)</span></span>

* <span data-ttu-id="d215b-110">如果.NET Core 项目处于打开状态的程序包管理器控制台获取的包失败[# 2932年](https://github.com/NuGet/Home/issues/2932)</span><span class="sxs-lookup"><span data-stu-id="d215b-110">Package Manager Console Get-Package fails if .NET Core project is open - [#2932](https://github.com/NuGet/Home/issues/2932)</span></span>

* <span data-ttu-id="d215b-111">在 NuGet push 命令中修复的 403 错误处理[# 2910年](https://github.com/NuGet/Home/issues/2910)</span><span class="sxs-lookup"><span data-stu-id="d215b-111">Fix incorrect handling of 403 in NuGet push command [#2910](https://github.com/NuGet/Home/issues/2910)</span></span>

* <span data-ttu-id="d215b-112">修复在卸载时 disableSourceControlIntegration 设置绑定到 TFS 源代码管理解决方案中的包的问题为 true 的[# 2739年](https://github.com/NuGet/Home/issues/2739)</span><span class="sxs-lookup"><span data-stu-id="d215b-112">Fix issues in uninstalling packages in a solution bound to TFS source control when disableSourceControlIntegration is set to true - [#2739](https://github.com/NuGet/Home/issues/2739)</span></span>

* <span data-ttu-id="d215b-113">修复包更新要考虑到帐户非目标包- [# 2724年](https://github.com/NuGet/Home/issues/2724)</span><span class="sxs-lookup"><span data-stu-id="d215b-113">Fix package update to take into account non-target packages - [#2724](https://github.com/NuGet/Home/issues/2724)</span></span>

* <span data-ttu-id="d215b-114">使用 MSBuild 详细级别设置为 Nuget 程序包管理器的记录器级别 UI 操作- [# 2705年](https://github.com/NuGet/Home/issues/2705)</span><span class="sxs-lookup"><span data-stu-id="d215b-114">Use MSBuild verbosity level to set logger level for Nuget package manager UI actions - [#2705](https://github.com/NuGet/Home/issues/2705)</span></span>

* <span data-ttu-id="d215b-115">修复 NuGet 配置是在网站项目的 VS 2015 VSIX (v3.4.3)-无效的错误[# 2667年](https://github.com/NuGet/Home/issues/2667)</span><span class="sxs-lookup"><span data-stu-id="d215b-115">Fix NuGet configuration is invalid error in WebSite projects - VS 2015 VSIX (v3.4.3) - [#2667](https://github.com/NuGet/Home/issues/2667)</span></span>

* <span data-ttu-id="d215b-116">修复包期刊`.csproj`时将包含的内容文件[# 2658年](https://github.com/NuGet/Home/issues/2658)</span><span class="sxs-lookup"><span data-stu-id="d215b-116">Fix pack issues from `.csproj` when content files are included - [#2658](https://github.com/NuGet/Home/issues/2658)</span></span>

* <span data-ttu-id="d215b-117">在 DefaultPushSource `NuGetDefaults.Config` (`ProgramData\NuGet`) 不起作用- [# 2653年](https://github.com/NuGet/Home/issues/2653)</span><span class="sxs-lookup"><span data-stu-id="d215b-117">DefaultPushSource in `NuGetDefaults.Config` (`ProgramData\NuGet`) doesn't work - [#2653](https://github.com/NuGet/Home/issues/2653)</span></span>

* <span data-ttu-id="d215b-118">在 Nuget 3.4.3 版本中的值不能为 null 在包创建-修复问题[# 2648年](https://github.com/NuGet/Home/issues/2648)</span><span class="sxs-lookup"><span data-stu-id="d215b-118">Fix issue in Nuget 3.4.3 release - Value cannot be null on package creation - [#2648](https://github.com/NuGet/Home/issues/2648)</span></span>

* <span data-ttu-id="d215b-119">还原为 VSTS 源-使用存储的凭据从 Nuget.Config [# 2647年](https://github.com/NuGet/Home/issues/2647)</span><span class="sxs-lookup"><span data-stu-id="d215b-119">Restore uses stored credentials from Nuget.Config for VSTS feeds - [#2647](https://github.com/NuGet/Home/issues/2647)</span></span>

* <span data-ttu-id="d215b-120">性能-版本比较代码中修复过多分配- [# 2632年](https://github.com/NuGet/Home/issues/2632)</span><span class="sxs-lookup"><span data-stu-id="d215b-120">Performance - Fix excessive allocations in version comparsion code - [#2632](https://github.com/NuGet/Home/issues/2632)</span></span>

* <span data-ttu-id="d215b-121">Nuget.exe 的多个实例会尝试并行的安装相同包时，解决问题[# 2628年](https://github.com/NuGet/Home/issues/2628)</span><span class="sxs-lookup"><span data-stu-id="d215b-121">Fix issues when multiple instances of nuget.exe tries to install the same package in parallel - [#2628](https://github.com/NuGet/Home/issues/2628)</span></span>

* <span data-ttu-id="d215b-122">性能-缓存依赖项信息的多项目操作- [# 2619年](https://github.com/NuGet/Home/issues/2619)</span><span class="sxs-lookup"><span data-stu-id="d215b-122">Performance - Cache dependency information for multi-project operations - [#2619](https://github.com/NuGet/Home/issues/2619)</span></span>

* <span data-ttu-id="d215b-123">解决问题的包源无法从设置时要从源列表为空-添加[# 2617年](https://github.com/NuGet/Home/issues/2617)</span><span class="sxs-lookup"><span data-stu-id="d215b-123">Fix issue where package sources cannnot be added from settings when source list is empty - [#2617](https://github.com/NuGet/Home/issues/2617)</span></span>

* <span data-ttu-id="d215b-124">尝试安装包依赖于设计时外观-时修复令人误解错误[# 2594年](https://github.com/NuGet/Home/issues/2594)</span><span class="sxs-lookup"><span data-stu-id="d215b-124">Fix Misleading error when attempting to install package that depends on design-time facades - [#2594](https://github.com/NuGet/Home/issues/2594)</span></span>

* <span data-ttu-id="d215b-125">将包安装从 PackageManager 控制台中设置"All"会尝试仅第一个源- [# 2557年](https://github.com/NuGet/Home/issues/2557)</span><span class="sxs-lookup"><span data-stu-id="d215b-125">Installing a package from PackageManager console with setting "All" tries only first source - [#2557](https://github.com/NuGet/Home/issues/2557)</span></span>

* <span data-ttu-id="d215b-126">修复文件写入时间在将来有 (Mono) 的包的问题[# 2518年](https://github.com/NuGet/Home/issues/2518)</span><span class="sxs-lookup"><span data-stu-id="d215b-126">Fix issues with packages that have files with write times in the future (Mono) - [#2518](https://github.com/NuGet/Home/issues/2518)</span></span>

* <span data-ttu-id="d215b-127">失败时查找项目中更新命令-显示异常[# 2418年](https://github.com/NuGet/Home/issues/2418)</span><span class="sxs-lookup"><span data-stu-id="d215b-127">Display exception when there is a failure finding projects in update command - [#2418](https://github.com/NuGet/Home/issues/2418)</span></span>

* <span data-ttu-id="d215b-128">从 nuget v3.3 + 安装的包源具有参数时，不正确还原包的内容时包中包含的-NoCache`.nupkg`文件- [# 2354年](https://github.com/NuGet/Home/issues/2354)</span><span class="sxs-lookup"><span data-stu-id="d215b-128">Package content is not restored correctly when installing a package from a nuget v3.3+ feed with the argument -NoCache when the package contains `.nupkg` files - [#2354](https://github.com/NuGet/Home/issues/2354)</span></span>

* <span data-ttu-id="d215b-129">修复问题，与包安装 （所有源） 时从 1 源的包缺少[# 2322年](https://github.com/NuGet/Home/issues/2322)</span><span class="sxs-lookup"><span data-stu-id="d215b-129">Fix issue with package install (All Sources) when package is missing from 1 source - [#2322](https://github.com/NuGet/Home/issues/2322)</span></span>

* <span data-ttu-id="d215b-130">如果单个源失败授权-安装块[# 2034年](https://github.com/NuGet/Home/issues/2034)</span><span class="sxs-lookup"><span data-stu-id="d215b-130">Install blocks if a single source fails authorization - [#2034](https://github.com/NuGet/Home/issues/2034)</span></span>

* <span data-ttu-id="d215b-131">`.nuspec` 版本范围应重写-IncludeReferencedProjects 版本- [# 1983年](https://github.com/NuGet/Home/issues/1983)</span><span class="sxs-lookup"><span data-stu-id="d215b-131">`.nuspec` version range should override -IncludeReferencedProjects version - [#1983](https://github.com/NuGet/Home/issues/1983)</span></span>

* <span data-ttu-id="d215b-132">NuGet 3.3.0 更新失败，出现...更多约束中定义 packages.config 阻止此操作。</span><span class="sxs-lookup"><span data-stu-id="d215b-132">NuGet 3.3.0 update fails with 'An additional constraint ... defined in packages.config prevents this operation.'</span></span><span data-ttu-id="d215b-133"> - [#1816](https://github.com/NuGet/Home/issues/1816)</span><span class="sxs-lookup"><span data-stu-id="d215b-133"> - [#1816](https://github.com/NuGet/Home/issues/1816)</span></span>

* <span data-ttu-id="d215b-134">nuget.exe 更新中删除程序集强名称和专用属性。</span><span class="sxs-lookup"><span data-stu-id="d215b-134">nuget.exe update drops the assembly strong name and Private attribute.</span></span><span data-ttu-id="d215b-135"> - [#1778](https://github.com/NuGet/Home/issues/1778)</span><span class="sxs-lookup"><span data-stu-id="d215b-135"> - [#1778](https://github.com/NuGet/Home/issues/1778)</span></span>

* <span data-ttu-id="d215b-136">使用相对文件路径为"DefaultPushSource"-修复问题[# 1746年](https://github.com/NuGet/Home/issues/1746)</span><span class="sxs-lookup"><span data-stu-id="d215b-136">Fix issues with relative file path for "DefaultPushSource" - [#1746](https://github.com/NuGet/Home/issues/1746)</span></span>

* <span data-ttu-id="d215b-137">提高更新冲突解决程序失败消息- [# 1373年](https://github.com/NuGet/Home/issues/1373)</span><span class="sxs-lookup"><span data-stu-id="d215b-137">Improve Update resolver failure messages - [#1373](https://github.com/NuGet/Home/issues/1373)</span></span>

## <a name="features-and-behavior-changes"></a><span data-ttu-id="d215b-138">功能及行为变化</span><span class="sxs-lookup"><span data-stu-id="d215b-138">Features and Behavior Changes</span></span>

* <span data-ttu-id="d215b-139">nuget.exe 推送-超时参数不起作用- [# 2785年](https://github.com/NuGet/Home/issues/2785)</span><span class="sxs-lookup"><span data-stu-id="d215b-139">nuget.exe push - timeout parameter doesn't work  - [#2785](https://github.com/NuGet/Home/issues/2785)</span></span>

* <span data-ttu-id="d215b-140">nuget.exe 还原不会产生`.props`并`.targets`文件，以`.nuproj`项目 （v3.4.3.855 中回归）- [# 2711年](https://github.com/NuGet/Home/issues/2711)</span><span class="sxs-lookup"><span data-stu-id="d215b-140">nuget.exe restore doesn't produce `.props` and `.targets` files for `.nuproj` projects (regression in v3.4.3.855) - [#2711](https://github.com/NuGet/Home/issues/2711)</span></span>

* <span data-ttu-id="d215b-141">需要扩展性 API 以比较框架与导入- [# 2633年](https://github.com/NuGet/Home/issues/2633)</span><span class="sxs-lookup"><span data-stu-id="d215b-141">Need extensibility API to compare frameworks with imports - [#2633](https://github.com/NuGet/Home/issues/2633)</span></span>

* <span data-ttu-id="d215b-142">使用时隐藏依赖关系选项`project.json`  -  [# 2486年](https://github.com/NuGet/Home/issues/2486)</span><span class="sxs-lookup"><span data-stu-id="d215b-142">Hide dependency options when using `project.json` - [#2486](https://github.com/NuGet/Home/issues/2486)</span></span>

* <span data-ttu-id="d215b-143">打印出 nuget.exe 版本标头中详细输出- [# 1887年](https://github.com/NuGet/Home/issues/1887)</span><span class="sxs-lookup"><span data-stu-id="d215b-143">Print out nuget.exe version header in detailed output - [#1887](https://github.com/NuGet/Home/issues/1887)</span></span>

* <span data-ttu-id="d215b-144">NuGet 应添加对 /runtimes/ {rid} /nativeassets/ {txm} 的支持 /- [# 2782年](https://github.com/NuGet/Home/issues/2782)</span><span class="sxs-lookup"><span data-stu-id="d215b-144">NuGet should add support for /runtimes/{rid}/nativeassets/{txm}/ - [#2782](https://github.com/NuGet/Home/issues/2782)</span></span>