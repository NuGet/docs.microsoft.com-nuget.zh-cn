---
title: NuGet 3.4.3 发行说明
description: NuGet 3.4.3 的发行说明，包括已知问题、bug 修复、新增功能和 Dcr。
author: JonDouglas
ms.author: jodou
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: f0d9740aaf0a82b9e4023b5e4990c8f4adbea63c
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/26/2021
ms.locfileid: "98776464"
---
# <a name="nuget-343-release-notes"></a><span data-ttu-id="e8461-103">NuGet 3.4.3 发行说明</span><span class="sxs-lookup"><span data-stu-id="e8461-103">NuGet 3.4.3 Release Notes</span></span>

<span data-ttu-id="e8461-104">[NuGet 3.4.2 发行说明](../release-notes/nuget-3.4.2.md)  | [NuGet 3.4.4 发行说明](../release-notes/nuget-3.4.4.md)</span><span class="sxs-lookup"><span data-stu-id="e8461-104">[NuGet 3.4.2 Release Notes](../release-notes/nuget-3.4.2.md) | [NuGet 3.4.4 Release Notes](../release-notes/nuget-3.4.4.md)</span></span>

<span data-ttu-id="e8461-105">NuGet 3.4.3 于2016年4月22日发布，以解决3.4 和后续版本中标识的几个问题。</span><span class="sxs-lookup"><span data-stu-id="e8461-105">NuGet 3.4.3 was released on April 22, 2016 to address several issues that were identified in the 3.4 and subsequent releases.</span></span>

<span data-ttu-id="e8461-106">可在 [此处](https://dist.nuget.org/index.html)下载 VSIX 和 nuget.exe。</span><span class="sxs-lookup"><span data-stu-id="e8461-106">You can download both the VSIX and nuget.exe [here](https://dist.nuget.org/index.html).</span></span>

## <a name="updates-and-improvements"></a><span data-ttu-id="e8461-107">更新和改进</span><span class="sxs-lookup"><span data-stu-id="e8461-107">Updates and Improvements</span></span>

* <span data-ttu-id="e8461-108">改进了 Visual Studio 的可靠性。</span><span class="sxs-lookup"><span data-stu-id="e8461-108">Improved Visual Studio reliability.</span></span> <span data-ttu-id="e8461-109">我们已修复了 NuGet 中导致 Visual Studio 崩溃的一些问题。</span><span class="sxs-lookup"><span data-stu-id="e8461-109">We have fixed some issues in NuGet that caused crashes in Visual Studio.</span></span>

## <a name="fixes"></a><span data-ttu-id="e8461-110">修复项</span><span class="sxs-lookup"><span data-stu-id="e8461-110">Fixes</span></span>

* <span data-ttu-id="e8461-111">解决了密码保护的专用 nuget 源的一些授权问题。</span><span class="sxs-lookup"><span data-stu-id="e8461-111">Fixed some authorization issues with password protected private nuget feeds.</span></span>
* <span data-ttu-id="e8461-112">解决了无法从 `project.json` 指定的运行时中还原 PCL 的问题。</span><span class="sxs-lookup"><span data-stu-id="e8461-112">Fixed an issue around being unable to restore PCL's from `project.json` with runtimes specified.</span></span>
* <span data-ttu-id="e8461-113">有些客户在安装包时遇到间歇性故障。</span><span class="sxs-lookup"><span data-stu-id="e8461-113">Some customers were running into intermittent failures when installing packages.</span></span> <span data-ttu-id="e8461-114">此版本中现已修复此项。</span><span class="sxs-lookup"><span data-stu-id="e8461-114">This has now been fixed in this release.</span></span>
* <span data-ttu-id="e8461-115">修复了在 c + +/CLI 项目中导致还原失败的问题 `project.json` 。</span><span class="sxs-lookup"><span data-stu-id="e8461-115">Fixed an issue that caused restore failures in C++/CLI projects with `project.json`.</span></span>
* <span data-ttu-id="e8461-116">某些包 (例如，当你在 mono 中使用 nuget 时，ModernHttpClient) 未正确进行解压缩。</span><span class="sxs-lookup"><span data-stu-id="e8461-116">Some packages (E.g ModernHttpClient) where not being unzipped correctly when you use nuget in mono.</span></span> <span data-ttu-id="e8461-117">此版本中现已修复此项。</span><span class="sxs-lookup"><span data-stu-id="e8461-117">This has now been fixed in this release.</span></span>

<span data-ttu-id="e8461-118">有关此版本中的修复和改进的完整列表，请查看 [此处](https://github.com/NuGet/Home/issues?q=is%3Aissue+milestone%3A3.4.3+is%3Aclosed)的问题列表。</span><span class="sxs-lookup"><span data-stu-id="e8461-118">For the complete list of fixes and improvements in this release, check out the list of issues [here](https://github.com/NuGet/Home/issues?q=is%3Aissue+milestone%3A3.4.3+is%3Aclosed).</span></span>