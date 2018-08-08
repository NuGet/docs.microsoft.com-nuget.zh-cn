---
title: NuGet 3.1 发行说明
description: 包括已知的问题、 bug 修复、 增加的功能，以及 DCRs NuGet 3.1 的发行说明。
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: d14455da6f8af4db92f7105ea1b0e88eb9e71600
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/26/2018
ms.locfileid: "31820856"
---
# <a name="nuget-31-release-notes"></a><span data-ttu-id="810ac-103">NuGet 3.1 发行说明</span><span class="sxs-lookup"><span data-stu-id="810ac-103">NuGet 3.1 Release Notes</span></span>

<span data-ttu-id="810ac-104">[NuGet 3.0 发行说明](../release-notes/nuget-3.0.0.md) | [NuGet 3.1.1 发行说明](../release-notes/nuget-3.1.1.md)</span><span class="sxs-lookup"><span data-stu-id="810ac-104">[NuGet 3.0 Release Notes](../release-notes/nuget-3.0.0.md) | [NuGet 3.1.1 Release Notes](../release-notes/nuget-3.1.1.md)</span></span>

<span data-ttu-id="810ac-105">NuGet 3.1 发布于 2015 年 7 月 27 日为通用 Windows 平台 SDK 的捆绑扩展 for Visual Studio 2015。</span><span class="sxs-lookup"><span data-stu-id="810ac-105">NuGet 3.1 was released on July 27, 2015 as a bundled extension to the Universal Windows Platform SDK for Visual Studio 2015.</span></span> <span data-ttu-id="810ac-106">我们提供与 Windows 平台 SDK 的此版本，以便 Windows 开发体验可能会利用以前已经开始的 NuGet 跨平台工作。</span><span class="sxs-lookup"><span data-stu-id="810ac-106">We delivered this release with the Windows Platform SDK so that the Windows development experience could take advantage of the NuGet cross-platform work that had been previously started.</span></span> <span data-ttu-id="810ac-107">此 NuGet 扩展版本仅可用于 Visual Studio 2015。</span><span class="sxs-lookup"><span data-stu-id="810ac-107">This NuGet extension version is only available for Visual Studio 2015.</span></span>

<span data-ttu-id="810ac-108">我们建议这些开发人员有权访问不可用，因为我们始终要发布 bug 修补程序和新功能的更新的最新版本的 Visual Studio 库更新。</span><span class="sxs-lookup"><span data-stu-id="810ac-108">We recommend those developers that have access to the Visual Studio gallery update to the latest version that is available, as we are always publishing updates with bug fixes and new features.</span></span>

## <a name="nuget-visual-studio-extension"></a><span data-ttu-id="810ac-109">NuGet Visual Studio 扩展</span><span class="sxs-lookup"><span data-stu-id="810ac-109">NuGet Visual Studio Extension</span></span>

<span data-ttu-id="810ac-110">问题和此版本中的功能标记与 GitHub 上["3.1 RTM UWP 可传递支持"里程碑](https://github.com/NuGet/Home/issues?utf8=%E2%9C%93&q=is%3Aclosed+milestone%3A%223.1+RTM+UWP+transitive+support%22+)，总共我们关闭 3.1 版本中的 67 问题。</span><span class="sxs-lookup"><span data-stu-id="810ac-110">Issues and features in this release are tagged on GitHub with the ["3.1 RTM UWP transitive support" milestone](https://github.com/NuGet/Home/issues?utf8=%E2%9C%93&q=is%3Aclosed+milestone%3A%223.1+RTM+UWP+transitive+support%22+)  In total, we closed 67 issues in the 3.1 release.</span></span>

### <a name="new-features"></a><span data-ttu-id="810ac-111">新增功能</span><span class="sxs-lookup"><span data-stu-id="810ac-111">New Features</span></span>

* <span data-ttu-id="810ac-112">`project.json` 支持针对 Windows UWP 和 ASP.NET 5 支持</span><span class="sxs-lookup"><span data-stu-id="810ac-112">`project.json` support for Windows UWP and ASP.NET 5 support</span></span>
* <span data-ttu-id="810ac-113">可传递的包安装</span><span class="sxs-lookup"><span data-stu-id="810ac-113">Transitive package installation</span></span>

<span data-ttu-id="810ac-114">说明和定义这些功能可以找到其他地方文档中。</span><span class="sxs-lookup"><span data-stu-id="810ac-114">Description and definition of these features can be found elsewhere in the documentation.</span></span>

### <a name="deprecated"></a><span data-ttu-id="810ac-115">不推荐使用</span><span class="sxs-lookup"><span data-stu-id="810ac-115">Deprecated</span></span>

<span data-ttu-id="810ac-116">以下功能将不再可用于 Visual Studio 2015:</span><span class="sxs-lookup"><span data-stu-id="810ac-116">The following features are no longer available for Visual Studio 2015:</span></span>

* <span data-ttu-id="810ac-117">解决方案级别程序包可以不再进行安装</span><span class="sxs-lookup"><span data-stu-id="810ac-117">Solution level packages can no longer be installed</span></span>

<span data-ttu-id="810ac-118">以下功能将不再可用于 Visual Studio 2015 和使用的项目`project.json`规范</span><span class="sxs-lookup"><span data-stu-id="810ac-118">The following features are no longer available for Visual Studio 2015 and projects that use the `project.json` specification</span></span>

* <span data-ttu-id="810ac-119">`install.ps1` 和`uninstall.ps1`-这些脚本将包安装过程中忽略、 还原、 更新和卸载</span><span class="sxs-lookup"><span data-stu-id="810ac-119">`install.ps1` and `uninstall.ps1` - These scripts will be ignored during package install, restore, update, and uninstall</span></span>
* <span data-ttu-id="810ac-120">将忽略配置转换</span><span class="sxs-lookup"><span data-stu-id="810ac-120">Configuration transforms will be ignored</span></span>
* <span data-ttu-id="810ac-121">内容将执行，但不是复制到项目。</span><span class="sxs-lookup"><span data-stu-id="810ac-121">Content will be carried, but not copied into a project.</span></span>
    * <span data-ttu-id="810ac-122">团队正致力于重新实现此功能，请按照讨论和在进度： [https://github.com/NuGet/Home/issues/627](https://github.com/NuGet/Home/issues/627)</span><span class="sxs-lookup"><span data-stu-id="810ac-122">The team is working to re-implement this feature, follow the discussion and progress at: [https://github.com/NuGet/Home/issues/627](https://github.com/NuGet/Home/issues/627)</span></span>


### <a name="known-issues"></a><span data-ttu-id="810ac-123">已知问题</span><span class="sxs-lookup"><span data-stu-id="810ac-123">Known Issues</span></span>

<span data-ttu-id="810ac-124">没有大量的时候附带此版本的已知问题。</span><span class="sxs-lookup"><span data-stu-id="810ac-124">There were a number of known issues delivered with this release.</span></span>

* <span data-ttu-id="810ac-125">使用 Windows 10 SDK 的 3.1 版本的安装将将以前已安装的 NuGet 任何的扩展版本降级</span><span class="sxs-lookup"><span data-stu-id="810ac-125">Installation of the 3.1 release with the Windows 10 SDK will downgrade any version of NuGet extension that was previously installed</span></span>

## <a name="nuget-command-line"></a><span data-ttu-id="810ac-126">NuGet 命令行</span><span class="sxs-lookup"><span data-stu-id="810ac-126">NuGet Command-line</span></span>

<span data-ttu-id="810ac-127">NuGet 命令行可执行文件已更新，并移动到新的可分发位置，以便 nuget.exe 的历史版本可以继续将变得可。</span><span class="sxs-lookup"><span data-stu-id="810ac-127">The NuGet command-line executable was updated and moved to a new distributable location so that historical versions of nuget.exe can continue to be made available.</span></span>  <span data-ttu-id="810ac-128">你可以为在 Windows 上下载 nuget.exe 的 3.1 beta 版本： [http://dist.nuget.org/win-x86-commandline/v3.1.0-beta/nuget.exe](http://dist.nuget.org/win-x86-commandline/v3.1.0-beta/nuget.exe)</span><span class="sxs-lookup"><span data-stu-id="810ac-128">You can download the 3.1 beta version of nuget.exe for Windows at: [http://dist.nuget.org/win-x86-commandline/v3.1.0-beta/nuget.exe](http://dist.nuget.org/win-x86-commandline/v3.1.0-beta/nuget.exe)</span></span>

<span data-ttu-id="810ac-129">新的可分发位置位于在 dist.nuget.org 主机上，遵循此模板的文件夹结构：</span><span class="sxs-lookup"><span data-stu-id="810ac-129">The new distributable location resides on the dist.nuget.org host, with a folder structure that follows this template:</span></span>

     {platform supported}/{version}/nuget.exe

### <a name="new-features"></a><span data-ttu-id="810ac-130">新增功能</span><span class="sxs-lookup"><span data-stu-id="810ac-130">New Features</span></span>

* <span data-ttu-id="810ac-131">nuget.exe 可以恢复，并将包安装到使用的项目`project.json`文件。</span><span class="sxs-lookup"><span data-stu-id="810ac-131">nuget.exe can restore and install packages into projects that use a `project.json` file.</span></span>
* <span data-ttu-id="810ac-132">nuget.exe 可以连接到和使用 NuGet v3 协议： [https://api.nuget.org/v3/index.json](https://api.nuget.org/v3/index.json)</span><span class="sxs-lookup"><span data-stu-id="810ac-132">nuget.exe can connect to and consume the NuGet v3 protocol at: [https://api.nuget.org/v3/index.json](https://api.nuget.org/v3/index.json)</span></span>

## <a name="known-issues"></a><span data-ttu-id="810ac-133">已知问题</span><span class="sxs-lookup"><span data-stu-id="810ac-133">Known Issues</span></span> ##

1.    <span data-ttu-id="810ac-134">无法执行包针对`project.json`文件- [928](https://github.com/NuGet/Home/issues/928)</span><span class="sxs-lookup"><span data-stu-id="810ac-134">Cannot execute pack against a `project.json` file - [928](https://github.com/NuGet/Home/issues/928)</span></span>
2.    <span data-ttu-id="810ac-135">不支持 Mono- [1059年](https://github.com/NuGet/Home/issues/1059)</span><span class="sxs-lookup"><span data-stu-id="810ac-135">Is not supported on Mono - [1059](https://github.com/NuGet/Home/issues/1059)</span></span>
3.    <span data-ttu-id="810ac-136">未本地化的[1058年](https://github.com/NuGet/Home/issues/1058)， [1057年](https://github.com/NuGet/Home/issues/1057)</span><span class="sxs-lookup"><span data-stu-id="810ac-136">Is not localized - [1058](https://github.com/NuGet/Home/issues/1058),   [1057](https://github.com/NuGet/Home/issues/1057)</span></span>
4.    <span data-ttu-id="810ac-137">未签名，就像现有 http://nuget.org/nuget.exe - [1073年](https://github.com/NuGet/Home/issues/1073)</span><span class="sxs-lookup"><span data-stu-id="810ac-137">Is not signed, just like the existing http://nuget.org/nuget.exe - [1073](https://github.com/NuGet/Home/issues/1073)</span></span>
