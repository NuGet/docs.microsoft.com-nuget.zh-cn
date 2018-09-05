---
title: NuGet 2.2 发行说明
description: 包括已知的问题、 bug 修复、 新增的功能和 Dcr NuGet 2.2 的发行说明。
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: a968ced3c58b7187a8bd9a8b14baa92f61f0140f
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/04/2018
ms.locfileid: "43545987"
---
# <a name="nuget-22-release-notes"></a><span data-ttu-id="5cd6c-103">NuGet 2.2 发行说明</span><span class="sxs-lookup"><span data-stu-id="5cd6c-103">NuGet 2.2 Release Notes</span></span>

<span data-ttu-id="5cd6c-104">[NuGet 2.1 发行说明](../release-notes/nuget-2.1.md) | [NuGet 2.2.1 发行说明](../release-notes/nuget-2.2.1.md)</span><span class="sxs-lookup"><span data-stu-id="5cd6c-104">[NuGet 2.1 Release Notes](../release-notes/nuget-2.1.md) | [NuGet 2.2.1 Release Notes](../release-notes/nuget-2.2.1.md)</span></span>

<span data-ttu-id="5cd6c-105">NuGet 2.2 已于 2012 年 12 月 12 日发布。</span><span class="sxs-lookup"><span data-stu-id="5cd6c-105">NuGet 2.2 was released on December 12, 2012.</span></span>

## <a name="visual-studio-quick-launch"></a><span data-ttu-id="5cd6c-106">Visual Studio 快速启动</span><span class="sxs-lookup"><span data-stu-id="5cd6c-106">Visual Studio Quick Launch</span></span>
<span data-ttu-id="5cd6c-107">在 Visual Studio 2012 中已添加的新功能之一是[快速启动对话框](/visualstudio/ide/reference/quick-launch-environment-options-dialog-box)。</span><span class="sxs-lookup"><span data-stu-id="5cd6c-107">One of the new features that was added in Visual Studio 2012 was the [quick launch dialog](/visualstudio/ide/reference/quick-launch-environment-options-dialog-box).</span></span> <span data-ttu-id="5cd6c-108">NuGet 2.2 扩展了此对话框中，使其能够与在快速启动栏中输入的搜索条件初始化包管理器对话框。</span><span class="sxs-lookup"><span data-stu-id="5cd6c-108">NuGet 2.2 extends this dialog, allowing it to initialize the package manager dialog with the search terms entered in the quick launch.</span></span> <span data-ttu-id="5cd6c-109">例如，现在在快速启动中输入 jquery 将包括在结果中搜索匹配 jquery NuGet 包的选项。</span><span class="sxs-lookup"><span data-stu-id="5cd6c-109">For example, entering 'jquery' in quick launch now includes an option in the results to search NuGet packages matching 'jquery'.</span></span>

![Visual Studio 快速启动中的 NuGet](./media/quick-launch.png)

<span data-ttu-id="5cd6c-111">选择此选项将启动术语 jquery 的标准 NuGet 包管理器搜索的体验。</span><span class="sxs-lookup"><span data-stu-id="5cd6c-111">Selecting this option will launch the standard NuGet package manager search experience for the term 'jquery'.</span></span>

![预填充的 NuGet 包管理器对话框](./media/pkg-mgr-search-from-quick-launch.png)

## <a name="specify-entire-folder-for-package-contents"></a><span data-ttu-id="5cd6c-113">指定包内容的整个文件夹</span><span class="sxs-lookup"><span data-stu-id="5cd6c-113">Specify Entire Folder for Package Contents</span></span>
<span data-ttu-id="5cd6c-114">NuGet 2.2 现在允许你指定的整个文件夹中`<file>`元素的`.nuspec`文件来包含所有该文件夹的内容。</span><span class="sxs-lookup"><span data-stu-id="5cd6c-114">NuGet 2.2 now allows you to specify an entire folder in the `<file>` element of the `.nuspec` file to include all of the contents of that folder.</span></span> <span data-ttu-id="5cd6c-115">例如，以下将导致所有脚本要添加到 contents\scripts 文件夹中，当包安装到项目的包的脚本文件夹中。</span><span class="sxs-lookup"><span data-stu-id="5cd6c-115">For example, the following will cause all scripts in the package's scripts folder to be added to the contents\scripts folder when the package is installed into a project.</span></span>

```xml
<file src="scripts\" target="content\scripts"/>
```

<span data-ttu-id="5cd6c-116">**更新 6/24/16： 安装包时，"内容"文件夹中的空文件夹将被忽略。**</span><span class="sxs-lookup"><span data-stu-id="5cd6c-116">**Update 6/24/16: Empty folders in the "content" folder are ignored when installing the package.**</span></span>

## <a name="known-issues"></a><span data-ttu-id="5cd6c-117">已知问题</span><span class="sxs-lookup"><span data-stu-id="5cd6c-117">Known Issues</span></span>

### <a name="package-installation-fails-for-f-projects-when-using-the-package-manager-console"></a><span data-ttu-id="5cd6c-118">使用包管理器控制台时，软件包安装失败的 F # 项目</span><span class="sxs-lookup"><span data-stu-id="5cd6c-118">Package installation fails for F# projects when using the package manager console</span></span>
<span data-ttu-id="5cd6c-119">当尝试将 NuGet 程序包安装到 F # 项目使用包管理器控制台时，将引发 InvalidOperationException。</span><span class="sxs-lookup"><span data-stu-id="5cd6c-119">When attempting to install a NuGet package into an F# project using the package manager console, an InvalidOperationException is thrown.</span></span> <span data-ttu-id="5cd6c-120">我们正在积极与 F # 团队来解决此问题，但在此期间，解决方法是将 NuGet 包安装到 F # 项目的 NuGet 包管理器对话框而不是在控制台通过。</span><span class="sxs-lookup"><span data-stu-id="5cd6c-120">We are actively working with the F# team to resolve the issue, but in the meantime, the workaround is to install NuGet packages into F# projects via NuGet's package manager dialog rather than the console.</span></span> <span data-ttu-id="5cd6c-121">[CodePlex 上提供了详细信息](http://nuget.codeplex.com/workitem/2873)。</span><span class="sxs-lookup"><span data-stu-id="5cd6c-121">[More information is available on CodePlex](http://nuget.codeplex.com/workitem/2873).</span></span>


## <a name="bug-fixes"></a><span data-ttu-id="5cd6c-122">Bug 修复</span><span class="sxs-lookup"><span data-stu-id="5cd6c-122">Bug Fixes</span></span>
<span data-ttu-id="5cd6c-123">NuGet 2.2 包括许多 bug 修复。</span><span class="sxs-lookup"><span data-stu-id="5cd6c-123">NuGet 2.2 includes many bug fixes.</span></span> <span data-ttu-id="5cd6c-124">有关工作的完整列表项中已修复 NuGet 2.2，请查看[对于此版本的 NuGet 问题跟踪程序](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Closed&type=All&priority=All&release=NuGet%202.2&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0)。</span><span class="sxs-lookup"><span data-stu-id="5cd6c-124">For a full list of work items fixed in NuGet 2.2, please view the [NuGet Issue Tracker for this release](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Closed&type=All&priority=All&release=NuGet%202.2&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0).</span></span>
