---
title: NuGet 5.4 发行说明
description: NuGet 5.4 的发行说明，包括新功能、bug 修复和 Dcr。
author: karann-msft
ms.author: karann
ms.date: 09/06/2019
ms.topic: conceptual
ms.openlocfilehash: 69f78ba5483fcc92887624584663e8c496cfc497
ms.sourcegitcommit: fe34b1fc79d6a9b2943a951f70b820037d2dd72d
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/04/2019
ms.locfileid: "74828392"
---
# <a name="nuget-54-release-notes"></a><span data-ttu-id="9f069-103">NuGet 5.4 发行说明</span><span class="sxs-lookup"><span data-stu-id="9f069-103">NuGet 5.4 Release Notes</span></span>

<span data-ttu-id="9f069-104">NuGet 分发车辆：</span><span class="sxs-lookup"><span data-stu-id="9f069-104">NuGet distribution vehicles:</span></span>

| <span data-ttu-id="9f069-105">NuGet 版本</span><span class="sxs-lookup"><span data-stu-id="9f069-105">NuGet version</span></span> | <span data-ttu-id="9f069-106">适用于 Visual Studio 版本</span><span class="sxs-lookup"><span data-stu-id="9f069-106">Available in Visual Studio version</span></span>| <span data-ttu-id="9f069-107">适用于 .NET SDK</span><span class="sxs-lookup"><span data-stu-id="9f069-107">Available in .NET SDK(s)</span></span>|
|:---|:---|:---|
| [<span data-ttu-id="9f069-108">**5.4.0**</span><span class="sxs-lookup"><span data-stu-id="9f069-108">**5.4.0**</span></span>](https://nuget.org/downloads) | [<span data-ttu-id="9f069-109">Visual Studio 2019 版本16。4</span><span class="sxs-lookup"><span data-stu-id="9f069-109">Visual Studio 2019 version 16.4</span></span>](https://visualstudio.microsoft.com/downloads/) | <span data-ttu-id="9f069-110">[3.1.100](https://dotnet.microsoft.com/download/dotnet-core/3.1)<sup>1</sup></span><span class="sxs-lookup"><span data-stu-id="9f069-110">[3.1.100](https://dotnet.microsoft.com/download/dotnet-core/3.1)<sup>1</sup></span></span> |

<span data-ttu-id="9f069-111"><sup>1</sup>随 Visual Studio 2019 with .NET Core 工作负载一起安装</span><span class="sxs-lookup"><span data-stu-id="9f069-111"><sup>1</sup>Installed with Visual Studio 2019 with .NET Core workload</span></span>

## <a name="summary-whats-new-in-54"></a><span data-ttu-id="9f069-112">摘要：5.4 中的新增功能</span><span class="sxs-lookup"><span data-stu-id="9f069-112">Summary: What's New in 5.4</span></span>

* <span data-ttu-id="9f069-113">更快的解决方案加载时间-在第一个解决方案加载过程中，运行 NuGet 代码的开销已通过部分 ngen 降低，以减少 JIT 成本[#6007](https://github.com/NuGet/Home/issues/6007)</span><span class="sxs-lookup"><span data-stu-id="9f069-113">Faster solution load time - Overhead running NuGet code during first solution load has been reduced via partial-ngen to reduce JIT cost - [#6007](https://github.com/NuGet/Home/issues/6007)</span></span>

* <span data-ttu-id="9f069-114">新建帮助程序函数-给定包 id 和版本的列表，获取可能的顶级包。</span><span class="sxs-lookup"><span data-stu-id="9f069-114">New helper function - given a list of package ids and versions, get the likely top level packages.</span></span><span data-ttu-id="9f069-115"> - [#8316](https://github.com/NuGet/Home/issues/8316)</span><span class="sxs-lookup"><span data-stu-id="9f069-115"> - [#8316](https://github.com/NuGet/Home/issues/8316)</span></span>

### <a name="issues-fixed-in-this-release"></a><span data-ttu-id="9f069-116">此版本中已修复的问题</span><span class="sxs-lookup"><span data-stu-id="9f069-116">Issues fixed in this release</span></span>

<span data-ttu-id="9f069-117">**Bug**</span><span class="sxs-lookup"><span data-stu-id="9f069-117">**Bugs**</span></span>

* <span data-ttu-id="9f069-118">插件： linux/Mac 上的日志记录时间准确性已关闭- [#8747](https://github.com/NuGet/Home/issues/8747)</span><span class="sxs-lookup"><span data-stu-id="9f069-118">Plugin: Logging time accuracy is off on linux/Mac - [#8747](https://github.com/NuGet/Home/issues/8747)</span></span>

* <span data-ttu-id="9f069-119">释放插件有时会引发并使整个操作失败。</span><span class="sxs-lookup"><span data-stu-id="9f069-119">Disposing of a plugin can sometimes throw and fail the whole operation.</span></span><span data-ttu-id="9f069-120"> - [#8732](https://github.com/NuGet/Home/issues/8732)</span><span class="sxs-lookup"><span data-stu-id="9f069-120"> - [#8732](https://github.com/NuGet/Home/issues/8732)</span></span>

* <span data-ttu-id="9f069-121">停止在 PMUI 中的允许和阻止版本列表中显示版本重复项- [#8679](https://github.com/NuGet/Home/issues/8679)</span><span class="sxs-lookup"><span data-stu-id="9f069-121">Stop displaying version duplicates in allowed and blocked versions list in PMUI - [#8679](https://github.com/NuGet/Home/issues/8679)</span></span>

* <span data-ttu-id="9f069-122">锁定文件未正确生成-框架排序不应影响 restore with lockedmode- [#8645](https://github.com/NuGet/Home/issues/8645)</span><span class="sxs-lookup"><span data-stu-id="9f069-122">Lock File not properly generated - framework ordering should not impact the restore with lockedmode - [#8645](https://github.com/NuGet/Home/issues/8645)</span></span>

* <span data-ttu-id="9f069-123"><RuntimeIdentifiers> SDK 3.0.100 中设置的项目的 LockFile 验证失败- [#8639](https://github.com/NuGet/Home/issues/8639)</span><span class="sxs-lookup"><span data-stu-id="9f069-123">LockFile validation fails for projects with <RuntimeIdentifiers> set in SDK 3.0.100 - [#8639](https://github.com/NuGet/Home/issues/8639)</span></span>

* <span data-ttu-id="9f069-124">签名验证现在会正确拒绝带有时间戳的签名，该时间戳在同一 OID [#8629](https://github.com/NuGet/Home/issues/8629)下具有2个值</span><span class="sxs-lookup"><span data-stu-id="9f069-124">Signing Validation will now properly reject signatures with timestamps which have 2 values under the same OID - [#8629](https://github.com/NuGet/Home/issues/8629)</span></span>

* <span data-ttu-id="9f069-125">更新许可证列表- [#8544](https://github.com/NuGet/Home/issues/8544)</span><span class="sxs-lookup"><span data-stu-id="9f069-125">Update the license list - [#8544](https://github.com/NuGet/Home/issues/8544)</span></span>

<span data-ttu-id="9f069-126">**Dcr**</span><span class="sxs-lookup"><span data-stu-id="9f069-126">**DCRs**</span></span>

* <span data-ttu-id="9f069-127">将诊断文件载入 IFeedbackDiagnosticFileProvider- [#8535](https://github.com/NuGet/Home/issues/8535)</span><span class="sxs-lookup"><span data-stu-id="9f069-127">Onboarding diagnostic files to IFeedbackDiagnosticFileProvider - [#8535](https://github.com/NuGet/Home/issues/8535)</span></span>

<span data-ttu-id="9f069-128">**[此版本中已修复的所有问题的列表-5。4](https://github.com/nuget/home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%225.4")**</span><span class="sxs-lookup"><span data-stu-id="9f069-128">**[List of all issues fixed in this release - 5.4](https://github.com/nuget/home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%225.4")**</span></span>
