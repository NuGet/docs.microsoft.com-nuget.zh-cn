---
title: "NuGet 2.2 发行说明 |Microsoft 文档"
author: karann-msft
ms.author: karann-msft
manager: ghogen
ms.date: 11/11/2016
ms.topic: article
ms.prod: nuget
ms.technology: 
ms.assetid: 25389d8c-e7db-4920-ab5e-cff20cebee7e
description: "包括已知的问题、 bug 修复、 增加的功能，以及 DCRs NuGet 2.2 的发行说明。"
keywords: "NuGet 2.2 发行说明，bug 修复的已知问题，添加了一些功能，DCRs"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 690e76a0686a5e7bb699410edef4a6e62ccd2a32
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/14/2017
---
# <a name="nuget-22-release-notes"></a><span data-ttu-id="7fe40-104">NuGet 2.2 发行说明</span><span class="sxs-lookup"><span data-stu-id="7fe40-104">NuGet 2.2 Release Notes</span></span>

<span data-ttu-id="7fe40-105">[NuGet 2.1 发行说明](../release-notes/nuget-2.1.md) | [NuGet 2.2.1 发行说明](../release-notes/nuget-2.2.1.md)</span><span class="sxs-lookup"><span data-stu-id="7fe40-105">[NuGet 2.1 Release Notes](../release-notes/nuget-2.1.md) | [NuGet 2.2.1 Release Notes](../release-notes/nuget-2.2.1.md)</span></span>

<span data-ttu-id="7fe40-106">NuGet 2.2 已于 2012 年 12 月 12 日发布。</span><span class="sxs-lookup"><span data-stu-id="7fe40-106">NuGet 2.2 was released on December 12, 2012.</span></span>

## <a name="visual-studio-quick-launch"></a><span data-ttu-id="7fe40-107">Visual Studio 快速启动</span><span class="sxs-lookup"><span data-stu-id="7fe40-107">Visual Studio Quick Launch</span></span>
<span data-ttu-id="7fe40-108">已添加到 Visual Studio 2012 中的新功能之一是[快速启动对话框](http://msdn.microsoft.com/library/hh417697.aspx)。</span><span class="sxs-lookup"><span data-stu-id="7fe40-108">One of the new features that was added in Visual Studio 2012 was the [quick launch dialog](http://msdn.microsoft.com/library/hh417697.aspx).</span></span> <span data-ttu-id="7fe40-109">NuGet 2.2 扩展此对话框中，使其能够与在快速启动中输入搜索词初始化包管理器对话框。</span><span class="sxs-lookup"><span data-stu-id="7fe40-109">NuGet 2.2 extends this dialog, allowing it to initialize the package manager dialog with the search terms entered in the quick launch.</span></span> <span data-ttu-id="7fe40-110">例如，现在在快速启动中输入 jquery 将包括在结果中要搜索匹配 jquery 的 NuGet 包的选项。</span><span class="sxs-lookup"><span data-stu-id="7fe40-110">For example, entering 'jquery' in quick launch now includes an option in the results to search NuGet packages matching 'jquery'.</span></span>

![NuGet 在 Visual Studio 快速启动](./media/quick-launch.png)

<span data-ttu-id="7fe40-112">选择此选项将启动长期 jquery 的标准 NuGet 包管理器搜索体验。</span><span class="sxs-lookup"><span data-stu-id="7fe40-112">Selecting this option will launch the standard NuGet package manager search experience for the term 'jquery'.</span></span>

![预填充的 NuGet 包管理器对话框](./media/pkg-mgr-search-from-quick-launch.png)

## <a name="specify-entire-folder-for-package-contents"></a><span data-ttu-id="7fe40-114">指定有关包内容的整个文件夹</span><span class="sxs-lookup"><span data-stu-id="7fe40-114">Specify Entire Folder for Package Contents</span></span>
<span data-ttu-id="7fe40-115">NuGet 2.2 现在允许你指定中的整个文件夹`<file>`元素`.nuspec`要包含该文件夹的内容的所有文件。</span><span class="sxs-lookup"><span data-stu-id="7fe40-115">NuGet 2.2 now allows you to specify an entire folder in the `<file>` element of the `.nuspec` file to include all of the contents of that folder.</span></span> <span data-ttu-id="7fe40-116">例如，以下将导致所有脚本在包的脚本文件夹中以包安装到项目时添加到 contents\scripts 文件夹。</span><span class="sxs-lookup"><span data-stu-id="7fe40-116">For example, the following will cause all scripts in the package's scripts folder to be added to the contents\scripts folder when the package is installed into a project.</span></span>

```xml
<file src="scripts\" target="content\scripts"/>
```

<span data-ttu-id="7fe40-117">**更新 6/24/16： 安装包时，将忽略空文件夹中的"内容"文件夹。**</span><span class="sxs-lookup"><span data-stu-id="7fe40-117">**Update 6/24/16: Empty folders in the "content" folder are ignored when installing the package.**</span></span>

## <a name="known-issues"></a><span data-ttu-id="7fe40-118">已知问题</span><span class="sxs-lookup"><span data-stu-id="7fe40-118">Known Issues</span></span>

### <a name="package-installation-fails-for-f-projects-when-using-the-package-manager-console"></a><span data-ttu-id="7fe40-119">使用包管理器控制台时，软件包安装失败，对于 F # 项目</span><span class="sxs-lookup"><span data-stu-id="7fe40-119">Package installation fails for F# projects when using the package manager console</span></span>
<span data-ttu-id="7fe40-120">当尝试将 NuGet 包安装到 F # 项目使用包管理器控制台，则会引发 InvalidOperationException。</span><span class="sxs-lookup"><span data-stu-id="7fe40-120">When attempting to install a NuGet package into an F# project using the package manager console, an InvalidOperationException is thrown.</span></span> <span data-ttu-id="7fe40-121">我们正在积极处理与 F # 团队以解决此问题，但在此期间，解决方法是将 NuGet 包安装到 F # 项目中的 NuGet 包管理器对话框而不是控制台通过。</span><span class="sxs-lookup"><span data-stu-id="7fe40-121">We are actively working with the F# team to resolve the issue, but in the meantime, the workaround is to install NuGet packages into F# projects via NuGet's package manager dialog rather than the console.</span></span> <span data-ttu-id="7fe40-122">[CodePlex 上提供了详细信息](http://nuget.codeplex.com/workitem/2873)。</span><span class="sxs-lookup"><span data-stu-id="7fe40-122">[More information is available on CodePlex](http://nuget.codeplex.com/workitem/2873).</span></span>


## <a name="bug-fixes"></a><span data-ttu-id="7fe40-123">Bug 修复</span><span class="sxs-lookup"><span data-stu-id="7fe40-123">Bug Fixes</span></span>
<span data-ttu-id="7fe40-124">NuGet 2.2 包括许多的 bug 修补程序。</span><span class="sxs-lookup"><span data-stu-id="7fe40-124">NuGet 2.2 includes many bug fixes.</span></span> <span data-ttu-id="7fe40-125">有关工作的完整列表项固定在 NuGet 2.2 中请视图[对于此版本的 NuGet 问题跟踪程序](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Closed&type=All&priority=All&release=NuGet%202.2&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0)。</span><span class="sxs-lookup"><span data-stu-id="7fe40-125">For a full list of work items fixed in NuGet 2.2, please view the [NuGet Issue Tracker for this release](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Closed&type=All&priority=All&release=NuGet%202.2&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0).</span></span>
