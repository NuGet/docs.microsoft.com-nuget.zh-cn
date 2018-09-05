---
title: NuGet 3.4.3 发行说明
description: NuGet 3.4.3 包括的发行说明的已知问题、 bug 修复、 新增的功能和 Dcr。
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 6ee4ecc06eb5119e24108d1cd6d2050254c45817
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/04/2018
ms.locfileid: "43549160"
---
# <a name="nuget-343-release-notes"></a><span data-ttu-id="61f46-103">NuGet 3.4.3 发行说明</span><span class="sxs-lookup"><span data-stu-id="61f46-103">NuGet 3.4.3 Release Notes</span></span>

<span data-ttu-id="61f46-104">[NuGet 3.4.2 发行说明](../release-notes/nuget-3.4.2.md) | [NuGet 3.4.4 发行说明](../release-notes/nuget-3.4.4.md)</span><span class="sxs-lookup"><span data-stu-id="61f46-104">[NuGet 3.4.2 Release Notes](../release-notes/nuget-3.4.2.md) | [NuGet 3.4.4 Release Notes](../release-notes/nuget-3.4.4.md)</span></span>

<span data-ttu-id="61f46-105">NuGet 3.4.3 发布于 2016 年 4 月 22，若要解决在 3.4 及后续版本中已发现的几个问题。</span><span class="sxs-lookup"><span data-stu-id="61f46-105">NuGet 3.4.3 was released on April 22, 2016 to address several issues that were identified in the 3.4 and subsequent releases.</span></span>

<span data-ttu-id="61f46-106">您可以下载的 VSIX 和 nuget.exe[此处](https://dist.nuget.org/index.html)。</span><span class="sxs-lookup"><span data-stu-id="61f46-106">You can download both the VSIX and nuget.exe [here](https://dist.nuget.org/index.html).</span></span>

## <a name="updates-and-improvements"></a><span data-ttu-id="61f46-107">更新和改进</span><span class="sxs-lookup"><span data-stu-id="61f46-107">Updates and Improvements</span></span>

* <span data-ttu-id="61f46-108">改进了 Visual Studio 可靠性。</span><span class="sxs-lookup"><span data-stu-id="61f46-108">Improved Visual Studio reliability.</span></span> <span data-ttu-id="61f46-109">我们已在 Visual Studio 中导致崩溃的 NuGet 中解决一些问题。</span><span class="sxs-lookup"><span data-stu-id="61f46-109">We have fixed some issues in NuGet that caused crashes in Visual Studio.</span></span>

## <a name="fixes"></a><span data-ttu-id="61f46-110">修补程序</span><span class="sxs-lookup"><span data-stu-id="61f46-110">Fixes</span></span>

* <span data-ttu-id="61f46-111">修复一些授权问题与受密码保护私有 nuget 源。</span><span class="sxs-lookup"><span data-stu-id="61f46-111">Fixed some authorization issues with password protected private nuget feeds.</span></span>
* <span data-ttu-id="61f46-112">修复了围绕无法还原 PCL 从`project.json`与指定的运行时。</span><span class="sxs-lookup"><span data-stu-id="61f46-112">Fixed an issue around being unable to restore PCL's from `project.json` with runtimes specified.</span></span>
* <span data-ttu-id="61f46-113">安装包时，某些客户已遇到间歇性故障。</span><span class="sxs-lookup"><span data-stu-id="61f46-113">Some customers were running into intermittent failures when installing packages.</span></span> <span data-ttu-id="61f46-114">此问题现在已在此版本中修复。</span><span class="sxs-lookup"><span data-stu-id="61f46-114">This has now been fixed in this release.</span></span>
* <span data-ttu-id="61f46-115">修复了导致还原失败，在 C + + /cli 项目与`project.json`。</span><span class="sxs-lookup"><span data-stu-id="61f46-115">Fixed an issue that caused restore failures in C++/CLI projects with `project.json`.</span></span>
* <span data-ttu-id="61f46-116">在其中不解压缩正确在 mono 中使用 nuget 时某些包 (例如 ModernHttpClient)。</span><span class="sxs-lookup"><span data-stu-id="61f46-116">Some packages (E.g ModernHttpClient) where not being unzipped correctly when you use nuget in mono.</span></span> <span data-ttu-id="61f46-117">此问题现在已在此版本中修复。</span><span class="sxs-lookup"><span data-stu-id="61f46-117">This has now been fixed in this release.</span></span>

<span data-ttu-id="61f46-118">有关此版本中的修补程序和改进的完整列表，请参阅问题列表[此处](https://github.com/NuGet/Home/issues?q=is%3Aissue+milestone%3A3.4.3+is%3Aclosed)。</span><span class="sxs-lookup"><span data-stu-id="61f46-118">For the complete list of fixes and improvements in this release, check out the list of issues [here](https://github.com/NuGet/Home/issues?q=is%3Aissue+milestone%3A3.4.3+is%3Aclosed).</span></span>