---
title: NuGet 5.4 发行说明
description: NuGet 5.4 的发行说明，包括新功能、bug 修复和 Dcr。
author: JonDouglas
ms.author: jodou
ms.date: 09/06/2019
ms.topic: conceptual
ms.openlocfilehash: dd4c10672db3a65b68f18636105ee55ab09da7ef
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/26/2021
ms.locfileid: "98776188"
---
# <a name="nuget-54-release-notes"></a><span data-ttu-id="d7596-103">NuGet 5.4 发行说明</span><span class="sxs-lookup"><span data-stu-id="d7596-103">NuGet 5.4 Release Notes</span></span>

<span data-ttu-id="d7596-104">NuGet 分发车辆：</span><span class="sxs-lookup"><span data-stu-id="d7596-104">NuGet distribution vehicles:</span></span>

| <span data-ttu-id="d7596-105">NuGet 版本</span><span class="sxs-lookup"><span data-stu-id="d7596-105">NuGet version</span></span> | <span data-ttu-id="d7596-106">适用于 Visual Studio 版本</span><span class="sxs-lookup"><span data-stu-id="d7596-106">Available in Visual Studio version</span></span>| <span data-ttu-id="d7596-107">适用于 .NET SDK</span><span class="sxs-lookup"><span data-stu-id="d7596-107">Available in .NET SDK(s)</span></span>|
|:---|:---|:---|
| [<span data-ttu-id="d7596-108">**5.4.0**</span><span class="sxs-lookup"><span data-stu-id="d7596-108">**5.4.0**</span></span>](https://nuget.org/downloads) | [<span data-ttu-id="d7596-109">Visual Studio 2019 版本 16.4</span><span class="sxs-lookup"><span data-stu-id="d7596-109">Visual Studio 2019 version 16.4</span></span>](https://visualstudio.microsoft.com/downloads/) | <span data-ttu-id="d7596-110">[3.1.100](https://dotnet.microsoft.com/download/dotnet-core/3.1)<sup>1</sup></span><span class="sxs-lookup"><span data-stu-id="d7596-110">[3.1.100](https://dotnet.microsoft.com/download/dotnet-core/3.1)<sup>1</sup></span></span> |

<span data-ttu-id="d7596-111"><sup>1</sup>随 Visual Studio 2019 with .NET Core 工作负载一起安装</span><span class="sxs-lookup"><span data-stu-id="d7596-111"><sup>1</sup>Installed with Visual Studio 2019 with .NET Core workload</span></span>

## <a name="summary-whats-new-in-54"></a><span data-ttu-id="d7596-112">摘要：5.4 中的新增功能</span><span class="sxs-lookup"><span data-stu-id="d7596-112">Summary: What's New in 5.4</span></span>

* <span data-ttu-id="d7596-113">更快的解决方案加载时间-在第一个解决方案加载过程中，运行 NuGet 代码的开销已通过部分 ngen 降低，以减少 JIT 成本 [#6007](https://github.com/NuGet/Home/issues/6007)</span><span class="sxs-lookup"><span data-stu-id="d7596-113">Faster solution load time - Overhead running NuGet code during first solution load has been reduced via partial-ngen to reduce JIT cost - [#6007](https://github.com/NuGet/Home/issues/6007)</span></span>

* <span data-ttu-id="d7596-114">新建帮助程序函数-给定包 id 和版本的列表，获取可能的顶级包。</span><span class="sxs-lookup"><span data-stu-id="d7596-114">New helper function - given a list of package ids and versions, get the likely top level packages.</span></span><span data-ttu-id="d7596-115"> - [#8316](https://github.com/NuGet/Home/issues/8316)</span><span class="sxs-lookup"><span data-stu-id="d7596-115"> - [#8316](https://github.com/NuGet/Home/issues/8316)</span></span>

* <span data-ttu-id="d7596-116">[`nuget/setup-nuget`](https://github.com/marketplace/actions/setup-nuget-exe-for-use-with-actions)用于在[GitHub 操作](https://github.com/features/actions)上安装和配置 NuGet.exe 的新操作。</span><span class="sxs-lookup"><span data-stu-id="d7596-116">New [`nuget/setup-nuget`](https://github.com/marketplace/actions/setup-nuget-exe-for-use-with-actions) action for installing and configuring NuGet.exe on [GitHub Actions](https://github.com/features/actions).</span></span><span data-ttu-id="d7596-117"> - [#8818](https://github.com/NuGet/Home/issues/8818)</span><span class="sxs-lookup"><span data-stu-id="d7596-117"> - [#8818](https://github.com/NuGet/Home/issues/8818)</span></span>

### <a name="issues-fixed-in-this-release"></a><span data-ttu-id="d7596-118">此版本中已修复的问题</span><span class="sxs-lookup"><span data-stu-id="d7596-118">Issues fixed in this release</span></span>

<span data-ttu-id="d7596-119">**Bug**</span><span class="sxs-lookup"><span data-stu-id="d7596-119">**Bugs**</span></span>

* <span data-ttu-id="d7596-120">插件： linux/Mac 上的日志记录时间准确性已关闭- [#8747](https://github.com/NuGet/Home/issues/8747)</span><span class="sxs-lookup"><span data-stu-id="d7596-120">Plugin: Logging time accuracy is off on linux/Mac - [#8747](https://github.com/NuGet/Home/issues/8747)</span></span>

* <span data-ttu-id="d7596-121">释放插件有时会引发并使整个操作失败。</span><span class="sxs-lookup"><span data-stu-id="d7596-121">Disposing of a plugin can sometimes throw and fail the whole operation.</span></span><span data-ttu-id="d7596-122"> - [#8732](https://github.com/NuGet/Home/issues/8732)</span><span class="sxs-lookup"><span data-stu-id="d7596-122"> - [#8732](https://github.com/NuGet/Home/issues/8732)</span></span>

* <span data-ttu-id="d7596-123">停止在 PMUI 中的允许和阻止版本列表中显示版本重复项- [#8679](https://github.com/NuGet/Home/issues/8679)</span><span class="sxs-lookup"><span data-stu-id="d7596-123">Stop displaying version duplicates in allowed and blocked versions list in PMUI - [#8679](https://github.com/NuGet/Home/issues/8679)</span></span>

* <span data-ttu-id="d7596-124">锁定文件未正确生成-框架排序不应影响 restore with lockedmode- [#8645](https://github.com/NuGet/Home/issues/8645)</span><span class="sxs-lookup"><span data-stu-id="d7596-124">Lock File not properly generated - framework ordering should not impact the restore with lockedmode - [#8645](https://github.com/NuGet/Home/issues/8645)</span></span>

* <span data-ttu-id="d7596-125"><RuntimeIdentifiers>SDK 3.0.100 [#8639](https://github.com/NuGet/Home/issues/8639)中设置的项目的 LockFile 验证失败</span><span class="sxs-lookup"><span data-stu-id="d7596-125">LockFile validation fails for projects with <RuntimeIdentifiers> set in SDK 3.0.100 - [#8639](https://github.com/NuGet/Home/issues/8639)</span></span>

* <span data-ttu-id="d7596-126">签名验证现在会正确拒绝带有时间戳的签名，该时间戳在同一 OID [#8629](https://github.com/NuGet/Home/issues/8629)下具有2个值</span><span class="sxs-lookup"><span data-stu-id="d7596-126">Signing Validation will now properly reject signatures with timestamps which have 2 values under the same OID - [#8629](https://github.com/NuGet/Home/issues/8629)</span></span>

* <span data-ttu-id="d7596-127">更新许可证列表- [#8544](https://github.com/NuGet/Home/issues/8544)</span><span class="sxs-lookup"><span data-stu-id="d7596-127">Update the license list - [#8544](https://github.com/NuGet/Home/issues/8544)</span></span>

<span data-ttu-id="d7596-128">**DCR**</span><span class="sxs-lookup"><span data-stu-id="d7596-128">**DCRs**</span></span>

* <span data-ttu-id="d7596-129">将诊断文件载入 IFeedbackDiagnosticFileProvider- [#8535](https://github.com/NuGet/Home/issues/8535)</span><span class="sxs-lookup"><span data-stu-id="d7596-129">Onboarding diagnostic files to IFeedbackDiagnosticFileProvider - [#8535](https://github.com/NuGet/Home/issues/8535)</span></span>

<span data-ttu-id="d7596-130">**[此版本中已修复的所有问题的列表-5。4](https://github.com/nuget/home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%225.4")**</span><span class="sxs-lookup"><span data-stu-id="d7596-130">**[List of all issues fixed in this release - 5.4](https://github.com/nuget/home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%225.4")**</span></span>
