---
title: "NuGet 3.4.3 发行说明 |Microsoft 文档"
author: karann-msft
ms.author: karann-msft
manager: ghogen
ms.date: 11/11/2016
ms.topic: article
ms.prod: nuget
ms.technology: 
description: "发行说明，了解 NuGet 3.4.3 包括已知问题、 bug 修复、 增加的功能，以及 DCRs。"
keywords: "NuGet 3.4.3 发行说明，bug 修复的已知问题，添加了一些功能，DCRs"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 68aab607659d15f96aefeab7bb90afc787710824
ms.sourcegitcommit: 4651b16a3a08f6711669fc4577f5d63b600f8f58
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/02/2018
---
# <a name="nuget-343-release-notes"></a><span data-ttu-id="ea3c7-104">NuGet 3.4.3 发行说明</span><span class="sxs-lookup"><span data-stu-id="ea3c7-104">NuGet 3.4.3 Release Notes</span></span>

<span data-ttu-id="ea3c7-105">[NuGet 上面 3.4.2 发行说明](../release-notes/nuget-3.4.2.md) | [NuGet 3.4.4 发行说明](../release-notes/nuget-3.4.4.md)</span><span class="sxs-lookup"><span data-stu-id="ea3c7-105">[NuGet 3.4.2 Release Notes](../release-notes/nuget-3.4.2.md) | [NuGet 3.4.4 Release Notes](../release-notes/nuget-3.4.4.md)</span></span>

<span data-ttu-id="ea3c7-106">NuGet 3.4.3 发布于 2016 年 4 月 22，为了解决发现 3.4 及后续版本中的几个问题。</span><span class="sxs-lookup"><span data-stu-id="ea3c7-106">NuGet 3.4.3 was released on April 22, 2016 to address several issues that were identified in the 3.4 and subsequent releases.</span></span>

<span data-ttu-id="ea3c7-107">你可以下载 VSIX 和 nuget.exe[此处](https://dist.nuget.org/index.html)。</span><span class="sxs-lookup"><span data-stu-id="ea3c7-107">You can download both the VSIX and nuget.exe [here](https://dist.nuget.org/index.html).</span></span>

## <a name="updates-and-improvements"></a><span data-ttu-id="ea3c7-108">更新和改进</span><span class="sxs-lookup"><span data-stu-id="ea3c7-108">Updates and Improvements</span></span>

* <span data-ttu-id="ea3c7-109">改进了 Visual Studio 可靠性。</span><span class="sxs-lookup"><span data-stu-id="ea3c7-109">Improved Visual Studio reliability.</span></span> <span data-ttu-id="ea3c7-110">在 Visual Studio 中导致崩溃的 NuGet 中，我们已解决的一些问题。</span><span class="sxs-lookup"><span data-stu-id="ea3c7-110">We have fixed some issues in NuGet that caused crashes in Visual Studio.</span></span>

## <a name="fixes"></a><span data-ttu-id="ea3c7-111">修补程序</span><span class="sxs-lookup"><span data-stu-id="ea3c7-111">Fixes</span></span>

* <span data-ttu-id="ea3c7-112">使用密码保护私有 nuget 源固定一些授权问题。</span><span class="sxs-lookup"><span data-stu-id="ea3c7-112">Fixed some authorization issues with password protected private nuget feeds.</span></span>
* <span data-ttu-id="ea3c7-113">修复了问题解决时无法进行还原 PCL 从`project.json`与指定的运行时。</span><span class="sxs-lookup"><span data-stu-id="ea3c7-113">Fixed an issue around being unable to restore PCL's from `project.json` with runtimes specified.</span></span>
* <span data-ttu-id="ea3c7-114">某些客户安装程序包时遇到了出现间歇性故障。</span><span class="sxs-lookup"><span data-stu-id="ea3c7-114">Some customers were running into intermittent failures when installing packages.</span></span> <span data-ttu-id="ea3c7-115">此问题现在已在此版本中修复。</span><span class="sxs-lookup"><span data-stu-id="ea3c7-115">This has now been fixed in this release.</span></span>
* <span data-ttu-id="ea3c7-116">修复了问题导致还原故障，在 C + + /cli 项目与`project.json`。</span><span class="sxs-lookup"><span data-stu-id="ea3c7-116">Fixed an issue that caused restore failures in C++/CLI projects with `project.json`.</span></span>
* <span data-ttu-id="ea3c7-117">其中不解压缩正确 mono 中使用 nuget 时某些包 (例如 ModernHttpClient)。</span><span class="sxs-lookup"><span data-stu-id="ea3c7-117">Some packages (E.g ModernHttpClient) where not being unzipped correctly when you use nuget in mono.</span></span> <span data-ttu-id="ea3c7-118">此问题现在已在此版本中修复。</span><span class="sxs-lookup"><span data-stu-id="ea3c7-118">This has now been fixed in this release.</span></span>

<span data-ttu-id="ea3c7-119">有关此版本中的修补程序和改进的完整列表，请参阅的问题列表[此处](https://github.com/NuGet/Home/issues?q=is%3Aissue+milestone%3A3.4.3+is%3Aclosed)。</span><span class="sxs-lookup"><span data-stu-id="ea3c7-119">For the complete list of fixes and improvements in this release, check out the list of issues [here](https://github.com/NuGet/Home/issues?q=is%3Aissue+milestone%3A3.4.3+is%3Aclosed).</span></span>