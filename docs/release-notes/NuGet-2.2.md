---
title: NuGet 2.2 发行说明
description: NuGet 2.2 的发行说明，包括已知问题、bug 修复、新增功能和 Dcr。
author: JonDouglas
ms.author: jodou
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: cc81d0ff53a5e8ac8b632a08c3cfe0b8b59c9bd7
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/26/2021
ms.locfileid: "98780430"
---
# <a name="nuget-22-release-notes"></a><span data-ttu-id="92b24-103">NuGet 2.2 发行说明</span><span class="sxs-lookup"><span data-stu-id="92b24-103">NuGet 2.2 Release Notes</span></span>

<span data-ttu-id="92b24-104">[NuGet 2.1 发行说明](../release-notes/nuget-2.1.md)  | [NuGet 2.2.1 发行说明](../release-notes/nuget-2.2.1.md)</span><span class="sxs-lookup"><span data-stu-id="92b24-104">[NuGet 2.1 Release Notes](../release-notes/nuget-2.1.md) | [NuGet 2.2.1 Release Notes](../release-notes/nuget-2.2.1.md)</span></span>

<span data-ttu-id="92b24-105">NuGet 2.2 于2012年12月12日发布。</span><span class="sxs-lookup"><span data-stu-id="92b24-105">NuGet 2.2 was released on December 12, 2012.</span></span>

## <a name="visual-studio-quick-launch"></a><span data-ttu-id="92b24-106">Visual Studio 快速启动</span><span class="sxs-lookup"><span data-stu-id="92b24-106">Visual Studio Quick Launch</span></span>
<span data-ttu-id="92b24-107">Visual Studio 2012 中新增的一项功能是 " [快速启动" 对话框](/visualstudio/ide/reference/quick-launch-environment-options-dialog-box)。</span><span class="sxs-lookup"><span data-stu-id="92b24-107">One of the new features that was added in Visual Studio 2012 was the [quick launch dialog](/visualstudio/ide/reference/quick-launch-environment-options-dialog-box).</span></span> <span data-ttu-id="92b24-108">NuGet 2.2 扩展了此对话框，使其能够通过 "快速启动" 中输入的搜索词初始化 "包管理器" 对话框。</span><span class="sxs-lookup"><span data-stu-id="92b24-108">NuGet 2.2 extends this dialog, allowing it to initialize the package manager dialog with the search terms entered in the quick launch.</span></span> <span data-ttu-id="92b24-109">例如，在 "快速启动" 中输入 "jquery" 现在会在结果中包含一个选项，用于搜索匹配 "jquery" 的 NuGet 包。</span><span class="sxs-lookup"><span data-stu-id="92b24-109">For example, entering 'jquery' in quick launch now includes an option in the results to search NuGet packages matching 'jquery'.</span></span>

![Visual Studio 快速启动中的 NuGet](./media/quick-launch.png)

<span data-ttu-id="92b24-111">选择此选项将启动术语 "jquery" 的标准 NuGet 包管理器搜索体验。</span><span class="sxs-lookup"><span data-stu-id="92b24-111">Selecting this option will launch the standard NuGet package manager search experience for the term 'jquery'.</span></span>

![预填充的 "NuGet 包管理器" 对话框](./media/pkg-mgr-search-from-quick-launch.png)

## <a name="specify-entire-folder-for-package-contents"></a><span data-ttu-id="92b24-113">为包内容指定整个文件夹</span><span class="sxs-lookup"><span data-stu-id="92b24-113">Specify Entire Folder for Package Contents</span></span>
<span data-ttu-id="92b24-114">NuGet 2.2 现在允许在文件的元素中指定整个文件夹， `<file>` `.nuspec` 以包含该文件夹的所有内容。</span><span class="sxs-lookup"><span data-stu-id="92b24-114">NuGet 2.2 now allows you to specify an entire folder in the `<file>` element of the `.nuspec` file to include all of the contents of that folder.</span></span> <span data-ttu-id="92b24-115">例如，当包安装到项目中时，以下将导致程序包的 scripts 文件夹中的所有脚本都添加到 contents\scripts 文件夹中。</span><span class="sxs-lookup"><span data-stu-id="92b24-115">For example, the following will cause all scripts in the package's scripts folder to be added to the contents\scripts folder when the package is installed into a project.</span></span>

```xml
<file src="scripts\" target="content\scripts"/>
```

<span data-ttu-id="92b24-116">**更新6/24/16：安装包时忽略 "content" 文件夹中的空文件夹。**</span><span class="sxs-lookup"><span data-stu-id="92b24-116">**Update 6/24/16: Empty folders in the "content" folder are ignored when installing the package.**</span></span>

## <a name="known-issues"></a><span data-ttu-id="92b24-117">已知问题</span><span class="sxs-lookup"><span data-stu-id="92b24-117">Known Issues</span></span>

### <a name="package-installation-fails-for-f-projects-when-using-the-package-manager-console"></a><span data-ttu-id="92b24-118">使用包管理器控制台时，F # 项目的包安装失败</span><span class="sxs-lookup"><span data-stu-id="92b24-118">Package installation fails for F# projects when using the package manager console</span></span>
<span data-ttu-id="92b24-119">尝试使用 package manager console 将 NuGet 包安装到 F # 项目时，将引发 InvalidOperationException。</span><span class="sxs-lookup"><span data-stu-id="92b24-119">When attempting to install a NuGet package into an F# project using the package manager console, an InvalidOperationException is thrown.</span></span> <span data-ttu-id="92b24-120">我们正在积极地与 F # 团队合作解决此问题，但在这种情况下，解决方法是通过 NuGet 的包管理器对话框而不是控制台将 NuGet 包安装到 F # 项目。</span><span class="sxs-lookup"><span data-stu-id="92b24-120">We are actively working with the F# team to resolve the issue, but in the meantime, the workaround is to install NuGet packages into F# projects via NuGet's package manager dialog rather than the console.</span></span> <span data-ttu-id="92b24-121">有关[详细信息，请访问 CodePlex](http://nuget.codeplex.com/workitem/2873)。</span><span class="sxs-lookup"><span data-stu-id="92b24-121">[More information is available on CodePlex](http://nuget.codeplex.com/workitem/2873).</span></span>


## <a name="bug-fixes"></a><span data-ttu-id="92b24-122">Bug 修复</span><span class="sxs-lookup"><span data-stu-id="92b24-122">Bug Fixes</span></span>
<span data-ttu-id="92b24-123">NuGet 2.2 包含多个 bug 修复。</span><span class="sxs-lookup"><span data-stu-id="92b24-123">NuGet 2.2 includes many bug fixes.</span></span> <span data-ttu-id="92b24-124">有关 NuGet 2.2 中已修复的工作项的完整列表，请查看 [此版本的 NuGet 问题跟踪程序](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Closed&type=All&priority=All&release=NuGet%202.2&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0)。</span><span class="sxs-lookup"><span data-stu-id="92b24-124">For a full list of work items fixed in NuGet 2.2, please view the [NuGet Issue Tracker for this release](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Closed&type=All&priority=All&release=NuGet%202.2&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0).</span></span>
