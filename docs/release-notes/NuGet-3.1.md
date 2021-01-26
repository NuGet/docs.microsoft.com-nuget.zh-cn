---
title: NuGet 3.1 发行说明
description: NuGet 3.1 的发行说明，包括已知问题、bug 修复、新增功能和 Dcr。
author: JonDouglas
ms.author: jodou
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: e1dc31e2543610b1da395f77fd2424bd85d985ef
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/26/2021
ms.locfileid: "98776537"
---
# <a name="nuget-31-release-notes"></a><span data-ttu-id="a83a6-103">NuGet 3.1 发行说明</span><span class="sxs-lookup"><span data-stu-id="a83a6-103">NuGet 3.1 Release Notes</span></span>

<span data-ttu-id="a83a6-104">[NuGet 3.0 发行说明](../release-notes/nuget-3.0.0.md)  | [NuGet 3.1.1 发行说明](../release-notes/nuget-3.1.1.md)</span><span class="sxs-lookup"><span data-stu-id="a83a6-104">[NuGet 3.0 Release Notes](../release-notes/nuget-3.0.0.md) | [NuGet 3.1.1 Release Notes](../release-notes/nuget-3.1.1.md)</span></span>

<span data-ttu-id="a83a6-105">NuGet 3.1 已于年7月27日发布2015，作为 Visual Studio 2015 通用 Windows 平台 SDK 的捆绑扩展。</span><span class="sxs-lookup"><span data-stu-id="a83a6-105">NuGet 3.1 was released on July 27, 2015 as a bundled extension to the Universal Windows Platform SDK for Visual Studio 2015.</span></span> <span data-ttu-id="a83a6-106">我们使用 Windows 平台 SDK 交付了此版本，以便 Windows 开发体验能够利用之前已启动的 NuGet 跨平台工作。</span><span class="sxs-lookup"><span data-stu-id="a83a6-106">We delivered this release with the Windows Platform SDK so that the Windows development experience could take advantage of the NuGet cross-platform work that had been previously started.</span></span> <span data-ttu-id="a83a6-107">此 NuGet 扩展版本仅适用于 Visual Studio 2015。</span><span class="sxs-lookup"><span data-stu-id="a83a6-107">This NuGet extension version is only available for Visual Studio 2015.</span></span>

<span data-ttu-id="a83a6-108">我们建议那些有权访问 Visual Studio 库的开发人员更新到可用的最新版本，因为我们始终发布包含 bug 修复和新功能的更新。</span><span class="sxs-lookup"><span data-stu-id="a83a6-108">We recommend those developers that have access to the Visual Studio gallery update to the latest version that is available, as we are always publishing updates with bug fixes and new features.</span></span>

## <a name="nuget-visual-studio-extension"></a><span data-ttu-id="a83a6-109">NuGet Visual Studio 扩展</span><span class="sxs-lookup"><span data-stu-id="a83a6-109">NuGet Visual Studio Extension</span></span>

<span data-ttu-id="a83a6-110">此版本中的问题和功能在 GitHub 上标记为 ["3.1 RTM UWP 可传递支持" 里程碑](https://github.com/NuGet/Home/issues?utf8=%E2%9C%93&q=is%3Aclosed+milestone%3A%223.1+RTM+UWP+transitive+support%22+)  ，在3.1 版本中关闭了67问题。</span><span class="sxs-lookup"><span data-stu-id="a83a6-110">Issues and features in this release are tagged on GitHub with the ["3.1 RTM UWP transitive support" milestone](https://github.com/NuGet/Home/issues?utf8=%E2%9C%93&q=is%3Aclosed+milestone%3A%223.1+RTM+UWP+transitive+support%22+)  In total, we closed 67 issues in the 3.1 release.</span></span>

### <a name="new-features"></a><span data-ttu-id="a83a6-111">新功能</span><span class="sxs-lookup"><span data-stu-id="a83a6-111">New Features</span></span>

* <span data-ttu-id="a83a6-112">`project.json` 支持 Windows UWP 和 ASP.NET 5 支持</span><span class="sxs-lookup"><span data-stu-id="a83a6-112">`project.json` support for Windows UWP and ASP.NET 5 support</span></span>
* <span data-ttu-id="a83a6-113">可传递包安装</span><span class="sxs-lookup"><span data-stu-id="a83a6-113">Transitive package installation</span></span>

<span data-ttu-id="a83a6-114">这些功能的说明和定义可在文档中的其他位置找到。</span><span class="sxs-lookup"><span data-stu-id="a83a6-114">Description and definition of these features can be found elsewhere in the documentation.</span></span>

### <a name="deprecated"></a><span data-ttu-id="a83a6-115">已放弃</span><span class="sxs-lookup"><span data-stu-id="a83a6-115">Deprecated</span></span>

<span data-ttu-id="a83a6-116">以下功能不再适用于 Visual Studio 2015：</span><span class="sxs-lookup"><span data-stu-id="a83a6-116">The following features are no longer available for Visual Studio 2015:</span></span>

* <span data-ttu-id="a83a6-117">解决方案级包无法再安装</span><span class="sxs-lookup"><span data-stu-id="a83a6-117">Solution level packages can no longer be installed</span></span>

<span data-ttu-id="a83a6-118">以下功能不再适用于 Visual Studio 2015 和使用该规范的项目 `project.json`</span><span class="sxs-lookup"><span data-stu-id="a83a6-118">The following features are no longer available for Visual Studio 2015 and projects that use the `project.json` specification</span></span>

* <span data-ttu-id="a83a6-119">`install.ps1` 和 `uninstall.ps1` -包安装、还原、更新和卸载过程中将忽略这些脚本</span><span class="sxs-lookup"><span data-stu-id="a83a6-119">`install.ps1` and `uninstall.ps1` - These scripts will be ignored during package install, restore, update, and uninstall</span></span>
* <span data-ttu-id="a83a6-120">将忽略配置转换</span><span class="sxs-lookup"><span data-stu-id="a83a6-120">Configuration transforms will be ignored</span></span>
* <span data-ttu-id="a83a6-121">内容将携带，但不会复制到项目中。</span><span class="sxs-lookup"><span data-stu-id="a83a6-121">Content will be carried, but not copied into a project.</span></span>
    * <span data-ttu-id="a83a6-122">团队正在努力重新实现此功能，请按照以下主题中的讨论和进度进行操作： [https://github.com/NuGet/Home/issues/627](https://github.com/NuGet/Home/issues/627)</span><span class="sxs-lookup"><span data-stu-id="a83a6-122">The team is working to re-implement this feature, follow the discussion and progress at: [https://github.com/NuGet/Home/issues/627](https://github.com/NuGet/Home/issues/627)</span></span>


### <a name="known-issues"></a><span data-ttu-id="a83a6-123">已知问题</span><span class="sxs-lookup"><span data-stu-id="a83a6-123">Known Issues</span></span>

<span data-ttu-id="a83a6-124">此版本提供了许多已知问题。</span><span class="sxs-lookup"><span data-stu-id="a83a6-124">There were a number of known issues delivered with this release.</span></span>

* <span data-ttu-id="a83a6-125">安装 Windows 10 SDK 的3.1 版本将会降级之前安装的任何版本的 NuGet 扩展</span><span class="sxs-lookup"><span data-stu-id="a83a6-125">Installation of the 3.1 release with the Windows 10 SDK will downgrade any version of NuGet extension that was previously installed</span></span>

## <a name="nuget-command-line"></a><span data-ttu-id="a83a6-126">NuGet 命令行</span><span class="sxs-lookup"><span data-stu-id="a83a6-126">NuGet Command-line</span></span>

<span data-ttu-id="a83a6-127">NuGet 命令行可执行文件已更新并移至新的可分发位置，因此可以继续使用 nuget.exe 的历史版本。</span><span class="sxs-lookup"><span data-stu-id="a83a6-127">The NuGet command-line executable was updated and moved to a new distributable location so that historical versions of nuget.exe can continue to be made available.</span></span>  <span data-ttu-id="a83a6-128">你可以在以下位置下载适用于 Windows 的 3.1 beta 版本的 nuget.exe： [http://dist.nuget.org/win-x86-commandline/v3.1.0-beta/nuget.exe](http://dist.nuget.org/win-x86-commandline/v3.1.0-beta/nuget.exe)</span><span class="sxs-lookup"><span data-stu-id="a83a6-128">You can download the 3.1 beta version of nuget.exe for Windows at: [http://dist.nuget.org/win-x86-commandline/v3.1.0-beta/nuget.exe](http://dist.nuget.org/win-x86-commandline/v3.1.0-beta/nuget.exe)</span></span>

<span data-ttu-id="a83a6-129">新的可分发位置位于 dist.nuget.org 主机上，其文件夹结构遵循以下模板：</span><span class="sxs-lookup"><span data-stu-id="a83a6-129">The new distributable location resides on the dist.nuget.org host, with a folder structure that follows this template:</span></span>

```
{platform supported}/{version}/nuget.exe
```

### <a name="new-features"></a><span data-ttu-id="a83a6-130">新功能</span><span class="sxs-lookup"><span data-stu-id="a83a6-130">New Features</span></span>

* <span data-ttu-id="a83a6-131">nuget.exe 可以还原包并将其安装到使用文件的项目中 `project.json` 。</span><span class="sxs-lookup"><span data-stu-id="a83a6-131">nuget.exe can restore and install packages into projects that use a `project.json` file.</span></span>
* <span data-ttu-id="a83a6-132">nuget.exe 可以连接到并使用 NuGet v3 协议，网址为： [https://api.nuget.org/v3/index.json](https://api.nuget.org/v3/index.json)</span><span class="sxs-lookup"><span data-stu-id="a83a6-132">nuget.exe can connect to and consume the NuGet v3 protocol at: [https://api.nuget.org/v3/index.json](https://api.nuget.org/v3/index.json)</span></span>

## <a name="known-issues"></a><span data-ttu-id="a83a6-133">已知问题</span><span class="sxs-lookup"><span data-stu-id="a83a6-133">Known Issues</span></span> ##

1.    <span data-ttu-id="a83a6-134">无法对文件执行 pack `project.json` - [928](https://github.com/NuGet/Home/issues/928)</span><span class="sxs-lookup"><span data-stu-id="a83a6-134">Cannot execute pack against a `project.json` file - [928](https://github.com/NuGet/Home/issues/928)</span></span>
2.    <span data-ttu-id="a83a6-135">Mono- [1059](https://github.com/NuGet/Home/issues/1059)不支持</span><span class="sxs-lookup"><span data-stu-id="a83a6-135">Is not supported on Mono - [1059](https://github.com/NuGet/Home/issues/1059)</span></span>
3.    <span data-ttu-id="a83a6-136">未本地化- [1058](https://github.com/NuGet/Home/issues/1058)、   [1057](https://github.com/NuGet/Home/issues/1057)</span><span class="sxs-lookup"><span data-stu-id="a83a6-136">Is not localized - [1058](https://github.com/NuGet/Home/issues/1058),   [1057](https://github.com/NuGet/Home/issues/1057)</span></span>
4.    <span data-ttu-id="a83a6-137">未签名，就像现有的 http://nuget.org/nuget.exe  -  [1073](https://github.com/NuGet/Home/issues/1073)</span><span class="sxs-lookup"><span data-stu-id="a83a6-137">Is not signed, just like the existing http://nuget.org/nuget.exe - [1073](https://github.com/NuGet/Home/issues/1073)</span></span>
