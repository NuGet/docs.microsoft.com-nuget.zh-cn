---
title: NuGet 4.7 RTM 发行说明
description: NuGet 4.7.0 的发行说明，包括已知问题、bug 修复、新增功能和 DCR。
author: JonDouglas
ms.author: jodou
ms.date: 5/14/2018
ms.topic: conceptual
ms.openlocfilehash: 143781cf0a95c6a156d4afcd83ad277f3e227711
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/26/2021
ms.locfileid: "98780161"
---
# <a name="nuget-47-release-notes"></a><span data-ttu-id="0959f-103">NuGet 4.7 发行说明</span><span class="sxs-lookup"><span data-stu-id="0959f-103">NuGet 4.7 Release Notes</span></span>

<span data-ttu-id="0959f-104">[Visual Studio 2017 15.7 RTW](https://www.visualstudio.com/news/releasenotes/vs2017-relnotes) 附带 [NuGet 4.7.0](https://dist.nuget.org/win-x86-commandline/v4.7.0/nuget.exe)。</span><span class="sxs-lookup"><span data-stu-id="0959f-104">[Visual Studio 2017 15.7 RTW](https://www.visualstudio.com/news/releasenotes/vs2017-relnotes) comes with [NuGet 4.7.0](https://dist.nuget.org/win-x86-commandline/v4.7.0/nuget.exe).</span></span>

## <a name="summary-whats-new-in-470"></a><span data-ttu-id="0959f-105">摘要:4.7.0 版中的新增功能</span><span class="sxs-lookup"><span data-stu-id="0959f-105">Summary: What's New in 4.7.0</span></span>

* <span data-ttu-id="0959f-106">我们已增强包签名，以便启用[存储库签名包](https://github.com/NuGet/Home/wiki/Repository-Signatures)</span><span class="sxs-lookup"><span data-stu-id="0959f-106">We have augmented package signing to enable [Repository Signed packages](https://github.com/NuGet/Home/wiki/Repository-Signatures)</span></span>

* <span data-ttu-id="0959f-107">在 Visual Studio 版本 15.7 中，我们已引入功能改为[迁移使用 packages.config 格式的现有项目以使用 PackageReference](../consume-packages/migrate-packages-config-to-package-reference.md)。</span><span class="sxs-lookup"><span data-stu-id="0959f-107">With Visual Studio Version 15.7, we have introduced the capability to [migrate existing projects that use the packages.config format to use PackageReference](../consume-packages/migrate-packages-config-to-package-reference.md) instead.</span></span>

## <a name="summary-whats-new-in-472"></a><span data-ttu-id="0959f-108">摘要:4.7.2 版中的新增功能</span><span class="sxs-lookup"><span data-stu-id="0959f-108">Summary: What's New in 4.7.2</span></span>

* <span data-ttu-id="0959f-109">安全修复：~/.nuget 中针对所创建文件的权限过于开放 [#7673](https://github.com/NuGet/Home/issues/7673) [CVE-2019-0757](https://portal.msrc.microsoft.com/en-us/security-guidance/advisory/CVE-2019-0757)</span><span class="sxs-lookup"><span data-stu-id="0959f-109">Security Fix: Permissions on files created inside ~/.nuget are too open [#7673](https://github.com/NuGet/Home/issues/7673) [CVE-2019-0757](https://portal.msrc.microsoft.com/en-us/security-guidance/advisory/CVE-2019-0757)</span></span>

## <a name="summary-whats-new-in-473"></a><span data-ttu-id="0959f-110">摘要:4.7.3 版中的新增功能</span><span class="sxs-lookup"><span data-stu-id="0959f-110">Summary: What's New in 4.7.3</span></span>

* <span data-ttu-id="0959f-111">安全修复：NUPKGs 中的文件可以具有高于 NUPKG 目录的相对路径 [#7906](https://github.com/NuGet/Home/issues/7906)</span><span class="sxs-lookup"><span data-stu-id="0959f-111">Security Fix: Files inside of NUPKGs can have a relative path above the NUPKG directory [#7906](https://github.com/NuGet/Home/issues/7906)</span></span>

## <a name="known-issues"></a><span data-ttu-id="0959f-112">已知问题</span><span class="sxs-lookup"><span data-stu-id="0959f-112">Known issues</span></span>

### <a name="the-migrate-packagesconfig-to-packagereference-option-is-not-available-in-the-right-click-context-menu"></a><span data-ttu-id="0959f-113">`Migrate packages.config to PackageReference...` 选项在右键单击上下文菜单中不可用</span><span class="sxs-lookup"><span data-stu-id="0959f-113">The `Migrate packages.config to PackageReference...` option is not available in the right-click context menu</span></span>

#### <a name="issue"></a><span data-ttu-id="0959f-114">问题</span><span class="sxs-lookup"><span data-stu-id="0959f-114">Issue</span></span>

<span data-ttu-id="0959f-115">首次打开项目时，在执行 NuGet 操作之前，NuGet 可能不会进行初始化。</span><span class="sxs-lookup"><span data-stu-id="0959f-115">When a project is first opened, NuGet may not have initialized until a NuGet operation is performed.</span></span> <span data-ttu-id="0959f-116">这将导致迁移选项不会显示在 `packages.config` 或 `References` 的右键单击上下文菜单中。</span><span class="sxs-lookup"><span data-stu-id="0959f-116">This causes the migration option to not show up in the right-click context menu on `packages.config` or `References`.</span></span>

#### <a name="workaround"></a><span data-ttu-id="0959f-117">解决方法</span><span class="sxs-lookup"><span data-stu-id="0959f-117">Workaround</span></span>

<span data-ttu-id="0959f-118">执行以下 NuGet 操作之一：</span><span class="sxs-lookup"><span data-stu-id="0959f-118">Perform any one of the following NuGet actions:</span></span>
* <span data-ttu-id="0959f-119">打开包管理器 UI - 右键单击 `References` 并选择 `Manage NuGet Packages...`</span><span class="sxs-lookup"><span data-stu-id="0959f-119">Open the Package Manager UI - Right-click on `References` and select `Manage NuGet Packages...`</span></span>
* <span data-ttu-id="0959f-120">打开“包管理器控制台” - 从 `Tools > NuGet Package Manager` 中选择 `Package Manager Console`</span><span class="sxs-lookup"><span data-stu-id="0959f-120">Open the Package Manager Console - From `Tools > NuGet Package Manager`, select `Package Manager Console`</span></span>
* <span data-ttu-id="0959f-121">运行 NuGet 还原 - 在“解决方案资源管理器”中，右键单击该解决方案节点，然后选择 `Restore NuGet Packages`</span><span class="sxs-lookup"><span data-stu-id="0959f-121">Run NuGet restore - Right-click on the solution node in the Solution Explorer and select `Restore NuGet Packages`</span></span>
* <span data-ttu-id="0959f-122">生成还会触发 NuGet 还原的项目</span><span class="sxs-lookup"><span data-stu-id="0959f-122">Build the project which also triggers NuGet restore</span></span>

<span data-ttu-id="0959f-123">现在应能够看到迁移选项。</span><span class="sxs-lookup"><span data-stu-id="0959f-123">You should now be able to see the migration option.</span></span> <span data-ttu-id="0959f-124">请注意，此选项不受支持且不会对 ASP.NET 和 C++ 项目类型显示。</span><span class="sxs-lookup"><span data-stu-id="0959f-124">Note that this option is not supported and will not show up for ASP.NET and C++ project types.</span></span>

### <a name="issues-with-net-standard-20-with-net-framework--nuget"></a><span data-ttu-id="0959f-125">使用 .NET Framework 和 NuGet 的 .NET Standard 2.0 的问题</span><span class="sxs-lookup"><span data-stu-id="0959f-125">Issues with .NET Standard 2.0 with .NET Framework & NuGet</span></span>

<span data-ttu-id="0959f-126">.NET Standard 及其工具旨在使面向 .NET Framework 4.6.1 的项目可使用面向 .NET Standard 2.0 或更早版本的 NuGet 包和项目。</span><span class="sxs-lookup"><span data-stu-id="0959f-126">.NET Standard & its tooling was designed such that projects targeting .NET Framework 4.6.1 can consume NuGet packages & projects targeting .NET Standard 2.0 or earlier.</span></span> <span data-ttu-id="0959f-127">[本文档](https://github.com/dotnet/standard/issues/481)总结了该方案相关问题、解决问题的计划以及可使用当前工具状态部署的变通方法。</span><span class="sxs-lookup"><span data-stu-id="0959f-127">[This document](https://github.com/dotnet/standard/issues/481) summarizes the issues around that scenario, the plan for addressing them, and workarounds you can deploy with today's state of the tooling.</span></span>

## <a name="top-issues-fixed-in-this-release"></a><span data-ttu-id="0959f-128">此版本中已修复的主要问题</span><span class="sxs-lookup"><span data-stu-id="0959f-128">Top issues fixed in this release</span></span>

### <a name="bugs"></a><span data-ttu-id="0959f-129">Bug</span><span class="sxs-lookup"><span data-stu-id="0959f-129">Bugs</span></span>

* <span data-ttu-id="0959f-130">NuGet 在 .Net Core 项目系统中遇到死锁（新回归）。</span><span class="sxs-lookup"><span data-stu-id="0959f-130">NuGet runs into a deadlock in .Net Core project system (new regression).</span></span><span data-ttu-id="0959f-131"> - [#6733](https://github.com/NuGet/Home/issues/6733)</span><span class="sxs-lookup"><span data-stu-id="0959f-131"> - [#6733](https://github.com/NuGet/Home/issues/6733)</span></span>
* <span data-ttu-id="0959f-132">包：如果 TfmSpecificPackageFile 与组合路径一起使用，则 PackagePath 构造不正确 - [#6726](https://github.com/NuGet/Home/issues/6726)</span><span class="sxs-lookup"><span data-stu-id="0959f-132">Pack: PackagePath is constructed incorrectly if TfmSpecificPackageFile is used with globbing paths - [#6726](https://github.com/NuGet/Home/issues/6726)</span></span>
* <span data-ttu-id="0959f-133">包：除非显式设置 ispackable，否则 Web API 项目无法创建包。</span><span class="sxs-lookup"><span data-stu-id="0959f-133">Pack: web api project cannot create package unless ispackable is explicitly set.</span></span><span data-ttu-id="0959f-134"> - [#6156](https://github.com/NuGet/Home/issues/6156)</span><span class="sxs-lookup"><span data-stu-id="0959f-134"> - [#6156](https://github.com/NuGet/Home/issues/6156)</span></span>
* <span data-ttu-id="0959f-135">VS UI 和 PMC 需要 30 分钟才能看到新包（nuget.exe 可以立即看到） - [#6657](https://github.com/NuGet/Home/issues/6657)</span><span class="sxs-lookup"><span data-stu-id="0959f-135">VS UI and PMC take 30min to see new package (nuget.exe sees it right away) - [#6657](https://github.com/NuGet/Home/issues/6657)</span></span>
* <span data-ttu-id="0959f-136">签名：SignatureUtility.GetCertificateChain(...) 不会检查所有链状态 - [#6565](https://github.com/NuGet/Home/issues/6565)</span><span class="sxs-lookup"><span data-stu-id="0959f-136">Signing:  SignatureUtility.GetCertificateChain(...) does not check all chain statuses - [#6565](https://github.com/NuGet/Home/issues/6565)</span></span>
* <span data-ttu-id="0959f-137">签名：改进 DER GeneralizedTime 处理 - [#6564](https://github.com/NuGet/Home/issues/6564)</span><span class="sxs-lookup"><span data-stu-id="0959f-137">Signing:  improve DER GeneralizedTime handling - [#6564](https://github.com/NuGet/Home/issues/6564)</span></span>
* <span data-ttu-id="0959f-138">签名：安装经篡改的包时，VS 不显示 NU3002 错误 - [#6337](https://github.com/NuGet/Home/issues/6337)</span><span class="sxs-lookup"><span data-stu-id="0959f-138">Signing: VS does not show a NU3002 error when installing a tampered package - [#6337](https://github.com/NuGet/Home/issues/6337)</span></span>
* <span data-ttu-id="0959f-139">lockFile.GetLibrary 区分大小写 - [#6500](https://github.com/NuGet/Home/issues/6500)</span><span class="sxs-lookup"><span data-stu-id="0959f-139">lockFile.GetLibrary is case sensitive - [#6500](https://github.com/NuGet/Home/issues/6500)</span></span>
* <span data-ttu-id="0959f-140">安装/更新还原代码和还原代码路径不一致 - [#3471](https://github.com/NuGet/Home/issues/3471)</span><span class="sxs-lookup"><span data-stu-id="0959f-140">Install/update restore code and Restore code paths are not consistent - [#3471](https://github.com/NuGet/Home/issues/3471)</span></span>
* <span data-ttu-id="0959f-141">解决方案 PackageManager 版本组合框可以通过键盘选择分隔符 - [#2606](https://github.com/NuGet/Home/issues/2606)</span><span class="sxs-lookup"><span data-stu-id="0959f-141">Solution PackageManager Version ComboBox can select separator via keyboard - [#2606](https://github.com/NuGet/Home/issues/2606)</span></span>
* <span data-ttu-id="0959f-142">无法加载源的服务索引 `https://www.myget.org/F/<id>`---> System.Net.Http.HttpRequestException：响应状态代码未指示成功：403（已禁止）- [#2530](https://github.com/NuGet/Home/issues/2530)</span><span class="sxs-lookup"><span data-stu-id="0959f-142">Unable to load the service index for source `https://www.myget.org/F/<id>` ---> System.Net.Http.HttpRequestException: Response status code does not indicate success: 403 (Forbidden) - [#2530](https://github.com/NuGet/Home/issues/2530)</span></span>

### <a name="dcrs"></a><span data-ttu-id="0959f-143">DCR</span><span class="sxs-lookup"><span data-stu-id="0959f-143">DCRs</span></span>

* <span data-ttu-id="0959f-144">发出 X-NuGet-Session-Id 标头以跨请求关联[功能建议] - [#5330](https://github.com/NuGet/Home/issues/5330)</span><span class="sxs-lookup"><span data-stu-id="0959f-144">Emit X-NuGet-Session-Id header to correlate across requests [feature proposal] - [#5330](https://github.com/NuGet/Home/issues/5330)</span></span>
* <span data-ttu-id="0959f-145">公开方法来等待运行通过 IV API 在 Visual Studio 中运行的还原操作。</span><span class="sxs-lookup"><span data-stu-id="0959f-145">Expose a way to wait on running restore operation running in Visual Studio via IVs apis.</span></span><span data-ttu-id="0959f-146"> - [#6029](https://github.com/NuGet/Home/issues/6029)</span><span class="sxs-lookup"><span data-stu-id="0959f-146"> - [#6029](https://github.com/NuGet/Home/issues/6029)</span></span>
* <span data-ttu-id="0959f-147">NuGet.exe -NoServiceEndpoint 将避免追加服务 URL 后缀 - [#6586](https://github.com/NuGet/Home/issues/6586)</span><span class="sxs-lookup"><span data-stu-id="0959f-147">NuGet.exe -NoServiceEndpoint will avoid appending service url suffix - [#6586](https://github.com/NuGet/Home/issues/6586)</span></span>
* <span data-ttu-id="0959f-148">将提交哈希添加到信息版本 - [#6492](https://github.com/NuGet/Home/issues/6492)</span><span class="sxs-lookup"><span data-stu-id="0959f-148">add commit hash to informational version - [#6492](https://github.com/NuGet/Home/issues/6492)</span></span>
* <span data-ttu-id="0959f-149">签名：启用存储库签名/副署删除 - [#6646](https://github.com/NuGet/Home/issues/6646)</span><span class="sxs-lookup"><span data-stu-id="0959f-149">Signing:  enable removal of repository signature/countersignature - [#6646](https://github.com/NuGet/Home/issues/6646)</span></span>
* <span data-ttu-id="0959f-150">签名：去除存储库签名/副署的 API - [#6589](https://github.com/NuGet/Home/issues/6589)</span><span class="sxs-lookup"><span data-stu-id="0959f-150">Signing:  API for stripping repository signature/countersignature - [#6589](https://github.com/NuGet/Home/issues/6589)</span></span>
* <span data-ttu-id="0959f-151">VS 中的登录源信息 - [#6527](https://github.com/NuGet/Home/issues/6527)</span><span class="sxs-lookup"><span data-stu-id="0959f-151">Log source information in VS - [#6527](https://github.com/NuGet/Home/issues/6527)</span></span>
* <span data-ttu-id="0959f-152">仅在 TFM 和 RID 上筛选 /tools，以便可将设置 XML 置于 /tools 文件夹中 - [#6197](https://github.com/NuGet/Home/issues/6197)</span><span class="sxs-lookup"><span data-stu-id="0959f-152">Filter /tools on only TFM and RID, so the settings XML can be put in /tools folder - [#6197](https://github.com/NuGet/Home/issues/6197)</span></span>
* <span data-ttu-id="0959f-153">当包命令排除开头的文件时发出警告。</span><span class="sxs-lookup"><span data-stu-id="0959f-153">Warn when Pack command excludes a file that starts with .</span></span><span data-ttu-id="0959f-154">  - [#3308](https://github.com/NuGet/Home/issues/3308)</span><span class="sxs-lookup"><span data-stu-id="0959f-154">  - [#3308](https://github.com/NuGet/Home/issues/3308)</span></span>

[<span data-ttu-id="0959f-155">此版本中所有已修复问题的列表</span><span class="sxs-lookup"><span data-stu-id="0959f-155">List of all issues fixed in this release</span></span>](https://github.com/NuGet/Home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%224.7")
