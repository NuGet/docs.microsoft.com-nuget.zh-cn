---
title: NuGet 3.4.4 发行说明
description: NuGet 3.4.4 包括的发行说明的已知问题、 bug 修复、 新增的功能和 Dcr。
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 44a9f21c61f0552fdc21aab24f48eee993654b01
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/04/2018
ms.locfileid: "43547468"
---
# <a name="nuget-344-release-notes"></a><span data-ttu-id="a54cf-103">NuGet 3.4.4 发行说明</span><span class="sxs-lookup"><span data-stu-id="a54cf-103">NuGet 3.4.4 Release Notes</span></span>

<span data-ttu-id="a54cf-104">[NuGet 3.4.3 发行说明](../release-notes/nuget-3.4.3.md) | [NuGet 3.5 测试版发行说明](../release-notes/nuget-3.5-Beta.md)</span><span class="sxs-lookup"><span data-stu-id="a54cf-104">[NuGet 3.4.3 Release Notes](../release-notes/nuget-3.4.3.md) | [NuGet 3.5-Beta Release Notes](../release-notes/nuget-3.5-Beta.md)</span></span>

<span data-ttu-id="a54cf-105">此版本的主要重点是 3.4.3 质量的改进与几个修补程序，用于 Visual Studio 扩展插件的 nuget.exe 版本。</span><span class="sxs-lookup"><span data-stu-id="a54cf-105">The primary focus of this release was improvements to the quality of 3.4.3 version of nuget.exe with a few fixes to the Visual Studio extension as well.</span></span>

<span data-ttu-id="a54cf-106">您可以下载的 VSIX 和 nuget.exe[此处](https://dist.nuget.org/index.html)。</span><span class="sxs-lookup"><span data-stu-id="a54cf-106">You can download both the VSIX and nuget.exe [here](https://dist.nuget.org/index.html).</span></span>

## <a name="344-rtmhttpsgithubcomnugetnugetclienttree344-rtm-2016-05-19"></a><span data-ttu-id="a54cf-107">[3.4.4-rtm](https://github.com/NuGet/NuGet.Client/tree/3.4.4-rtm) (2016年-05-19)</span><span class="sxs-lookup"><span data-stu-id="a54cf-107">[3.4.4-rtm](https://github.com/NuGet/NuGet.Client/tree/3.4.4-rtm) (2016-05-19)</span></span>

[<span data-ttu-id="a54cf-108">完整更改日志</span><span class="sxs-lookup"><span data-stu-id="a54cf-108">Full Changelog</span></span>](https://github.com/NuGet/NuGet.Client/compare/3.5.0-beta-final...3.4.4-rtm)

[<span data-ttu-id="a54cf-109">问题列表</span><span class="sxs-lookup"><span data-stu-id="a54cf-109">List of Issues</span></span>](https://github.com/NuGet/Home/issues?q=is%3Aissue+milestone%3A3.4.4+is%3Aclosed)

### <a name="changes"></a><span data-ttu-id="a54cf-110">更改</span><span class="sxs-lookup"><span data-stu-id="a54cf-110">Changes</span></span>

- <span data-ttu-id="a54cf-111">包改进： 改进的打包符号，与封装`project.json`和更多[ \#606](https://github.com/NuGet/NuGet.Client/pull/606)</span><span class="sxs-lookup"><span data-stu-id="a54cf-111">Pack Improvements: Improvements to packing symbols, packing with `project.json` and more [\#606](https://github.com/NuGet/NuGet.Client/pull/606)</span></span>
- <span data-ttu-id="a54cf-112">未找到项目更新命令中时显示异常 [\#605] (https://github.com/NuGet/NuGet.Client/pull/605</span><span class="sxs-lookup"><span data-stu-id="a54cf-112">Display exception when there is a failure finding projects in update command [\#605](https://github.com/NuGet/NuGet.Client/pull/605</span></span>
- <span data-ttu-id="a54cf-113">从输入读取包类型`.nuspec`并`project.json`打包时[ \#603](https://github.com/NuGet/NuGet.Client/pull/603)</span><span class="sxs-lookup"><span data-stu-id="a54cf-113">Read package type from input `.nuspec` and `project.json` when packing [\#603](https://github.com/NuGet/NuGet.Client/pull/603)</span></span>
- <span data-ttu-id="a54cf-114">请 NuGet.Shared 不是项目。</span><span class="sxs-lookup"><span data-stu-id="a54cf-114">Make NuGet.Shared not a project.</span></span> [<span data-ttu-id="a54cf-115">\#602</span><span class="sxs-lookup"><span data-stu-id="a54cf-115">\#602</span></span>](https://github.com/NuGet/NuGet.Client/pull/602)
- <span data-ttu-id="a54cf-116">使用推送超时作为 HTTP 响应超时[ \#599](https://github.com/NuGet/NuGet.Client/pull/599)</span><span class="sxs-lookup"><span data-stu-id="a54cf-116">Use the push timeout as the HTTP response timeout [\#599](https://github.com/NuGet/NuGet.Client/pull/599)</span></span>
- <span data-ttu-id="a54cf-117">将来时间与包文件不会使用其时间[ \#597](https://github.com/NuGet/NuGet.Client/pull/597)</span><span class="sxs-lookup"><span data-stu-id="a54cf-117">Package files with future times will not have their times used [\#597](https://github.com/NuGet/NuGet.Client/pull/597)</span></span>
- <span data-ttu-id="a54cf-118">正在更新`NuGet.Core.dll`2.12.0 若要解决 XML 问题的版本[ \#594](https://github.com/NuGet/NuGet.Client/pull/594)</span><span class="sxs-lookup"><span data-stu-id="a54cf-118">Updating `NuGet.Core.dll` version to 2.12.0 to fix XML issue [\#594](https://github.com/NuGet/NuGet.Client/pull/594)</span></span>
- <span data-ttu-id="a54cf-119">支持./NuGet.CommandLine.XPlat-v\<详细程度\>\<模式\> [ \#593](https://github.com/NuGet/NuGet.Client/pull/593)</span><span class="sxs-lookup"><span data-stu-id="a54cf-119">Support ./NuGet.CommandLine.XPlat -v \<verbosity\> \<mode\> [\#593](https://github.com/NuGet/NuGet.Client/pull/593)</span></span>
- <span data-ttu-id="a54cf-120">显示错误还原，而无需`project.json`或`packages.config` [ \#590](https://github.com/NuGet/NuGet.Client/pull/590)</span><span class="sxs-lookup"><span data-stu-id="a54cf-120">Display error restoring without `project.json` or `packages.config` [\#590](https://github.com/NuGet/NuGet.Client/pull/590)</span></span>
- <span data-ttu-id="a54cf-121">修复依赖项版本，如果所需的版本不同[ \#559](https://github.com/NuGet/NuGet.Client/pull/559)</span><span class="sxs-lookup"><span data-stu-id="a54cf-121">Fixing dependency versions when required versions differ [\#559](https://github.com/NuGet/NuGet.Client/pull/559)</span></span>