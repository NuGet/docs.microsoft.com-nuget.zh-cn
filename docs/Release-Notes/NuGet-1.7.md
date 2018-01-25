---
title: "NuGet 1.7 发行说明 |Microsoft 文档"
author: karann-msft
ms.author: karann-msft
manager: ghogen
ms.date: 11/11/2016
ms.topic: article
ms.prod: nuget
ms.technology: 
description: "包括已知的问题、 bug 修复、 增加的功能，以及 DCRs NuGet 1.7 的发行说明。"
keywords: "NuGet 1.7 发行说明，bug 修复的已知问题，添加了一些功能，DCRs"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 7b16bea8c6bcc77f814dd32a43b895b5e656c95d
ms.sourcegitcommit: 262d026beeffd4f3b6fc47d780a2f701451663a8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/25/2018
---
# <a name="nuget-17-release-notes"></a><span data-ttu-id="33dfd-104">NuGet 1.7 版的发行说明</span><span class="sxs-lookup"><span data-stu-id="33dfd-104">NuGet 1.7 Release Notes</span></span>

<span data-ttu-id="33dfd-105">[NuGet 1.6 发行说明](../release-notes/nuget-1.6.md) | [NuGet 1.8 发行说明](../release-notes/nuget-1.8.md)</span><span class="sxs-lookup"><span data-stu-id="33dfd-105">[NuGet 1.6 Release Notes](../release-notes/nuget-1.6.md) | [NuGet 1.8 Release Notes](../release-notes/nuget-1.8.md)</span></span>

<span data-ttu-id="33dfd-106">NuGet 1.7 已于 2012 年 4 月 4 日发布。</span><span class="sxs-lookup"><span data-stu-id="33dfd-106">NuGet 1.7 was released on April 4, 2012.</span></span>

## <a name="known-installation-issue"></a><span data-ttu-id="33dfd-107">已知的安装问题</span><span class="sxs-lookup"><span data-stu-id="33dfd-107">Known Installation Issue</span></span>
<span data-ttu-id="33dfd-108">如果你运行的 VS 2010 SP1，你可能尝试升级 NuGet，如果安装了较旧版本时遇到安装错误。</span><span class="sxs-lookup"><span data-stu-id="33dfd-108">If you are running VS 2010 SP1, you might run into an installation error when attempting to upgrade NuGet if you have an older version installed.</span></span>

<span data-ttu-id="33dfd-109">解决方法是只需卸载 NuGet，然后从 VS 扩展库安装它。</span><span class="sxs-lookup"><span data-stu-id="33dfd-109">The workaround is to simply uninstall NuGet and then install it from the VS Extension Gallery.</span></span>  <span data-ttu-id="33dfd-110">有关详细信息，请参阅 [http://support.microsoft.com/kb/2581019](http://support.microsoft.com/kb/2581019)。</span><span class="sxs-lookup"><span data-stu-id="33dfd-110">See [http://support.microsoft.com/kb/2581019](http://support.microsoft.com/kb/2581019) for more information.</span></span>

<span data-ttu-id="33dfd-111">注意： 如果 Visual Studio 不会使您可以卸载的扩展 （卸载按钮为禁用），然后你可能需要重新启动 Visual Studio 中使用"以管理员身份运行"。</span><span class="sxs-lookup"><span data-stu-id="33dfd-111">Note: If Visual Studio won't allow you to uninstall the extension (the Uninstall button is disabled), then you likely need to restart Visual Studio using "Run as Administrator."</span></span>

## <a name="features"></a><span data-ttu-id="33dfd-112">功能</span><span class="sxs-lookup"><span data-stu-id="33dfd-112">Features</span></span>

### <a name="support-opening-readmetxt-file-after-installation"></a><span data-ttu-id="33dfd-113">支持在安装后打开 readme.txt 文件</span><span class="sxs-lookup"><span data-stu-id="33dfd-113">Support opening readme.txt file after installation</span></span>
<span data-ttu-id="33dfd-114">如果你的包包括在 1.7，新`readme.txt`根目录下的包，NuGet 的文件将自动打开此文件后它已完成安装你的包。</span><span class="sxs-lookup"><span data-stu-id="33dfd-114">New in 1.7, if your package includes a `readme.txt` file at the root of the package, NuGet will automatically open this file after it's finished installing your package.</span></span>

### <a name="show-prerelease-packages-in-the-manage-nuget-packages-dialog"></a><span data-ttu-id="33dfd-115">在管理 NuGet 包对话框中显示预发行程序包</span><span class="sxs-lookup"><span data-stu-id="33dfd-115">Show prerelease packages in the Manage NuGet packages dialog</span></span>
<span data-ttu-id="33dfd-116">管理 NuGet 包对话框现在包括一个下拉列表，它提供选项，可以显示预发行程序包。</span><span class="sxs-lookup"><span data-stu-id="33dfd-116">The Manage NuGet Packages dialog now includes a dropdown which provides option to show prerelease packages.</span></span>

![显示预发行程序包](./media/prerelease-dropdown.png)

### <a name="show-package-restore-button-when-package-files-are-missing"></a><span data-ttu-id="33dfd-118">缺少包文件时显示程序包还原按钮</span><span class="sxs-lookup"><span data-stu-id="33dfd-118">Show Package Restore button when package files are missing</span></span>
<span data-ttu-id="33dfd-119">当你打开程序包管理器控制台或管理器 NuGet 包对话框，NuGet 将检查当前解决方案已启用的程序包还原模式并且任何包文件中缺少`packages`文件夹。</span><span class="sxs-lookup"><span data-stu-id="33dfd-119">When you open the Package Manager console or the Manager NuGet packages dialog, NuGet will check if the current solution has enabled the Package Restore mode and if any package files are missing from the `packages` folder.</span></span> <span data-ttu-id="33dfd-120">如果满足这两个条件，NuGet 将通知你，将显示一个方便的还原按钮。</span><span class="sxs-lookup"><span data-stu-id="33dfd-120">If these two conditions are met, NuGet will notify you and will show a convenient Restore button.</span></span> <span data-ttu-id="33dfd-121">单击此按钮将触发 NuGet 还原所有缺少的程序包。</span><span class="sxs-lookup"><span data-stu-id="33dfd-121">Clicking this button will trigger NuGet to restore all the missing packages.</span></span>

![在对话框的包还原按钮](./media/packagerestore-dialog.png)

![在控制台上的包还原按钮](./media/packagerestore-console.png)

### <a name="add-solution-level-packagesconfig-file"></a><span data-ttu-id="33dfd-124">添加解决方案级 packages.config 文件</span><span class="sxs-lookup"><span data-stu-id="33dfd-124">Add solution-level packages.config file</span></span>
<span data-ttu-id="33dfd-125">在以前版本的 NuGet 中，每个项目有`packages.config`文件来跟踪哪些 NuGet 包安装在该项目。</span><span class="sxs-lookup"><span data-stu-id="33dfd-125">In previous versions of NuGet, each project has a `packages.config` file which keeps track of what NuGet packages are installed in that project.</span></span> <span data-ttu-id="33dfd-126">但是，没有类似文件可以在解决方案级别来跟踪解决方案级包。</span><span class="sxs-lookup"><span data-stu-id="33dfd-126">However, there was no similar file at the solution level to keep track of solution-level packages.</span></span> <span data-ttu-id="33dfd-127">因此，没有方法来还原解决方案级程序包。</span><span class="sxs-lookup"><span data-stu-id="33dfd-127">As a result, there was no way to restore solution-level packages.</span></span>
<span data-ttu-id="33dfd-128">在 NuGet 1.7 中现在实现此功能。</span><span class="sxs-lookup"><span data-stu-id="33dfd-128">This feature is now implemented in NuGet 1.7.</span></span> <span data-ttu-id="33dfd-129">解决方案级`packages.config`文件放置在`.nuget`下解决方案文件夹的根，并将存储解决方案仅级包。</span><span class="sxs-lookup"><span data-stu-id="33dfd-129">The solution-level `packages.config` file is placed under the `.nuget` folder under solution root and will store only solution-level packages.</span></span>

### <a name="remove-new-package-command"></a><span data-ttu-id="33dfd-130">删除新建包命令</span><span class="sxs-lookup"><span data-stu-id="33dfd-130">Remove New-Package command</span></span>
<span data-ttu-id="33dfd-131">由于使用率低，新建包命令已被删除。</span><span class="sxs-lookup"><span data-stu-id="33dfd-131">Due to low usage, the New-Package command has been removed.</span></span> <span data-ttu-id="33dfd-132">建议开发人员使用 nuget.exe 或方便 NuGet 包资源管理器来创建包。</span><span class="sxs-lookup"><span data-stu-id="33dfd-132">Developers are recommended to use nuget.exe or the handy NuGet Package Explorer to create packages.</span></span>

## <a name="bug-fixes"></a><span data-ttu-id="33dfd-133">Bug 修复</span><span class="sxs-lookup"><span data-stu-id="33dfd-133">Bug Fixes</span></span>
<span data-ttu-id="33dfd-134">NuGet 1.7 已修复 bug 的程序包还原工作流和网络/源控制方案都很多。</span><span class="sxs-lookup"><span data-stu-id="33dfd-134">NuGet 1.7 has fixed many bugs around the Package Restore workflow and Network/Source Control scenarios.</span></span>

<span data-ttu-id="33dfd-135">有关工作的完整列表项固定在 NuGet 1.7，请查看[对于此版本的 NuGet 问题跟踪程序](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Closed&type=All&priority=All&release=NuGet%201.7&assignedTo=All&component=All&sortField=Votes&sortDirection=Descending&page=0)。</span><span class="sxs-lookup"><span data-stu-id="33dfd-135">For a full list of work items fixed in NuGet 1.7, please view the [NuGet Issue Tracker for this release](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Closed&type=All&priority=All&release=NuGet%201.7&assignedTo=All&component=All&sortField=Votes&sortDirection=Descending&page=0).</span></span>
