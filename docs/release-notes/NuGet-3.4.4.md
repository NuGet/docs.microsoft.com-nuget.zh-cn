---
title: NuGet 3.4.4 发行说明
description: 发行说明，了解 NuGet 3.4.4 包括已知问题、 bug 修复、 增加的功能，以及 DCRs。
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 891d5c7ee884d31f405118739b57a169b9cd93b3
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/26/2018
ms.locfileid: "31820855"
---
# <a name="nuget-344-release-notes"></a><span data-ttu-id="ad950-103">NuGet 3.4.4 发行说明</span><span class="sxs-lookup"><span data-stu-id="ad950-103">NuGet 3.4.4 Release Notes</span></span>

<span data-ttu-id="ad950-104">[NuGet 3.4.3 发行说明](../release-notes/nuget-3.4.3.md) | [NuGet 3.5 Beta 发行说明](../release-notes/nuget-3.5-Beta.md)</span><span class="sxs-lookup"><span data-stu-id="ad950-104">[NuGet 3.4.3 Release Notes](../release-notes/nuget-3.4.3.md) | [NuGet 3.5-Beta Release Notes](../release-notes/nuget-3.5-Beta.md)</span></span>

<span data-ttu-id="ad950-105">此版本的主要侧重点在于已对 3.4.3 质量的改进的 nuget.exe 的 Visual Studio 扩展到几个修补程序的版本。</span><span class="sxs-lookup"><span data-stu-id="ad950-105">The primary focus of this release was improvements to the quality of 3.4.3 version of nuget.exe with a few fixes to the Visual Studio extension as well.</span></span>

<span data-ttu-id="ad950-106">你可以下载 VSIX 和 nuget.exe[此处](https://dist.nuget.org/index.html)。</span><span class="sxs-lookup"><span data-stu-id="ad950-106">You can download both the VSIX and nuget.exe [here](https://dist.nuget.org/index.html).</span></span>

## <a name="344-rtmhttpsgithubcomnugetnugetclienttree344-rtm-2016-05-19"></a><span data-ttu-id="ad950-107">[3.4.4-rtm](https://github.com/NuGet/NuGet.Client/tree/3.4.4-rtm) (2016年-05-19)</span><span class="sxs-lookup"><span data-stu-id="ad950-107">[3.4.4-rtm](https://github.com/NuGet/NuGet.Client/tree/3.4.4-rtm) (2016-05-19)</span></span>

[<span data-ttu-id="ad950-108">完整的版本记录</span><span class="sxs-lookup"><span data-stu-id="ad950-108">Full Changelog</span></span>](https://github.com/NuGet/NuGet.Client/compare/3.5.0-beta-final...3.4.4-rtm)

[<span data-ttu-id="ad950-109">问题的列表</span><span class="sxs-lookup"><span data-stu-id="ad950-109">List of Issues</span></span>](https://github.com/NuGet/Home/issues?q=is%3Aissue+milestone%3A3.4.4+is%3Aclosed)

### <a name="changes"></a><span data-ttu-id="ad950-110">更改</span><span class="sxs-lookup"><span data-stu-id="ad950-110">Changes</span></span>

- <span data-ttu-id="ad950-111">包改进： 封装与对封装符号，改进`project.json`更多[ \#606](https://github.com/NuGet/NuGet.Client/pull/606)</span><span class="sxs-lookup"><span data-stu-id="ad950-111">Pack Improvements: Improvements to packing symbols, packing with `project.json` and more [\#606](https://github.com/NuGet/NuGet.Client/pull/606)</span></span>
- <span data-ttu-id="ad950-112">在更新命令中查找项目失败时显示异常 [\#605] (https://github.com/NuGet/NuGet.Client/pull/605</span><span class="sxs-lookup"><span data-stu-id="ad950-112">Display exception when there is a failure finding projects in update command [\#605](https://github.com/NuGet/NuGet.Client/pull/605</span></span>
- <span data-ttu-id="ad950-113">从输入读取包类型`.nuspec`和`project.json`时装箱[ \#603](https://github.com/NuGet/NuGet.Client/pull/603)</span><span class="sxs-lookup"><span data-stu-id="ad950-113">Read package type from input `.nuspec` and `project.json` when packing [\#603](https://github.com/NuGet/NuGet.Client/pull/603)</span></span>
- <span data-ttu-id="ad950-114">请 NuGet.Shared 不是项目。</span><span class="sxs-lookup"><span data-stu-id="ad950-114">Make NuGet.Shared not a project.</span></span> [<span data-ttu-id="ad950-115">\#602</span><span class="sxs-lookup"><span data-stu-id="ad950-115">\#602</span></span>](https://github.com/NuGet/NuGet.Client/pull/602)
- <span data-ttu-id="ad950-116">使用推送超时作为 HTTP 响应超时[ \#599](https://github.com/NuGet/NuGet.Client/pull/599)</span><span class="sxs-lookup"><span data-stu-id="ad950-116">Use the push timeout as the HTTP response timeout [\#599](https://github.com/NuGet/NuGet.Client/pull/599)</span></span>
- <span data-ttu-id="ad950-117">将来的时间的包文件不会使用其时间[ \#597](https://github.com/NuGet/NuGet.Client/pull/597)</span><span class="sxs-lookup"><span data-stu-id="ad950-117">Package files with future times will not have their times used [\#597](https://github.com/NuGet/NuGet.Client/pull/597)</span></span>
- <span data-ttu-id="ad950-118">更新`NuGet.Core.dll`版本到 2.12.0 若要解决 XML 问题[ \#594](https://github.com/NuGet/NuGet.Client/pull/594)</span><span class="sxs-lookup"><span data-stu-id="ad950-118">Updating `NuGet.Core.dll` version to 2.12.0 to fix XML issue [\#594](https://github.com/NuGet/NuGet.Client/pull/594)</span></span>
- <span data-ttu-id="ad950-119">支持./NuGet.CommandLine.XPlat v\<详细级别\>\<模式\> [ \#593](https://github.com/NuGet/NuGet.Client/pull/593)</span><span class="sxs-lookup"><span data-stu-id="ad950-119">Support ./NuGet.CommandLine.XPlat -v \<verbosity\> \<mode\> [\#593](https://github.com/NuGet/NuGet.Client/pull/593)</span></span>
- <span data-ttu-id="ad950-120">显示错误还原，而不`project.json`或`packages.config` [ \#590](https://github.com/NuGet/NuGet.Client/pull/590)</span><span class="sxs-lookup"><span data-stu-id="ad950-120">Display error restoring without `project.json` or `packages.config` [\#590](https://github.com/NuGet/NuGet.Client/pull/590)</span></span>
- <span data-ttu-id="ad950-121">如果所需的版本不相同修复依赖项版本[ \#559](https://github.com/NuGet/NuGet.Client/pull/559)</span><span class="sxs-lookup"><span data-stu-id="ad950-121">Fixing dependency versions when required versions differ [\#559](https://github.com/NuGet/NuGet.Client/pull/559)</span></span>