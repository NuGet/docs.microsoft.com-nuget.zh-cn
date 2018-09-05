---
title: NuGet 1.7 版发行说明
description: 包括已知的问题、 bug 修复、 新增的功能和 Dcr NuGet 1.7 的发行说明。
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 07cd541ef215d2a1bacc45995a22dadb6dfeac6d
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/04/2018
ms.locfileid: "43551462"
---
# <a name="nuget-17-release-notes"></a><span data-ttu-id="11613-103">NuGet 1.7 版发行说明</span><span class="sxs-lookup"><span data-stu-id="11613-103">NuGet 1.7 Release Notes</span></span>

<span data-ttu-id="11613-104">[NuGet 1.6 发行说明](../release-notes/nuget-1.6.md) | [NuGet 1.8 发行说明](../release-notes/nuget-1.8.md)</span><span class="sxs-lookup"><span data-stu-id="11613-104">[NuGet 1.6 Release Notes](../release-notes/nuget-1.6.md) | [NuGet 1.8 Release Notes](../release-notes/nuget-1.8.md)</span></span>

<span data-ttu-id="11613-105">NuGet 1.7 已于 2012 年 4 月 4 日发布。</span><span class="sxs-lookup"><span data-stu-id="11613-105">NuGet 1.7 was released on April 4, 2012.</span></span>

## <a name="known-installation-issue"></a><span data-ttu-id="11613-106">已知的安装问题</span><span class="sxs-lookup"><span data-stu-id="11613-106">Known Installation Issue</span></span>
<span data-ttu-id="11613-107">如果运行 VS 2010 SP1，你可能会遇到安装错误，尝试升级 NuGet，如果您有安装了旧版本时。</span><span class="sxs-lookup"><span data-stu-id="11613-107">If you are running VS 2010 SP1, you might run into an installation error when attempting to upgrade NuGet if you have an older version installed.</span></span>

<span data-ttu-id="11613-108">解决方法是简单地卸载 NuGet，然后从 VS 扩展库安装它。</span><span class="sxs-lookup"><span data-stu-id="11613-108">The workaround is to simply uninstall NuGet and then install it from the VS Extension Gallery.</span></span>  <span data-ttu-id="11613-109">有关详细信息，请参阅 [http://support.microsoft.com/kb/2581019](http://support.microsoft.com/kb/2581019)。</span><span class="sxs-lookup"><span data-stu-id="11613-109">See [http://support.microsoft.com/kb/2581019](http://support.microsoft.com/kb/2581019) for more information.</span></span>

<span data-ttu-id="11613-110">注意： 如果 Visual Studio 不会使您可以卸载的扩展 （卸载按钮被禁用），然后您可能需要重启 Visual Studio 中使用"以管理员身份运行"。</span><span class="sxs-lookup"><span data-stu-id="11613-110">Note: If Visual Studio won't allow you to uninstall the extension (the Uninstall button is disabled), then you likely need to restart Visual Studio using "Run as Administrator."</span></span>

## <a name="features"></a><span data-ttu-id="11613-111">功能</span><span class="sxs-lookup"><span data-stu-id="11613-111">Features</span></span>

### <a name="support-opening-readmetxt-file-after-installation"></a><span data-ttu-id="11613-112">安装后打开 readme.txt 文件的支持</span><span class="sxs-lookup"><span data-stu-id="11613-112">Support opening readme.txt file after installation</span></span>
<span data-ttu-id="11613-113">中的新增功能 1.7，如果您的包包括`readme.txt`NuGet 包的根目录处文件将自动打开此文件之后它已完成安装您的包。</span><span class="sxs-lookup"><span data-stu-id="11613-113">New in 1.7, if your package includes a `readme.txt` file at the root of the package, NuGet will automatically open this file after it's finished installing your package.</span></span>

### <a name="show-prerelease-packages-in-the-manage-nuget-packages-dialog"></a><span data-ttu-id="11613-114">在管理 NuGet 包对话框中显示预发行包</span><span class="sxs-lookup"><span data-stu-id="11613-114">Show prerelease packages in the Manage NuGet packages dialog</span></span>
<span data-ttu-id="11613-115">管理 NuGet 包对话框中现在包含一个下拉列表，其中提供了选项，以显示预发行包。</span><span class="sxs-lookup"><span data-stu-id="11613-115">The Manage NuGet Packages dialog now includes a dropdown which provides option to show prerelease packages.</span></span>

![显示预发行包](./media/prerelease-dropdown.png)

### <a name="show-package-restore-button-when-package-files-are-missing"></a><span data-ttu-id="11613-117">缺少包文件时显示包还原按钮</span><span class="sxs-lookup"><span data-stu-id="11613-117">Show Package Restore button when package files are missing</span></span>
<span data-ttu-id="11613-118">当打开包管理器控制台或管理器 NuGet 包对话框时，NuGet 将检查当前解决方案已启用包还原模式下，如果任何包文件中缺少`packages`文件夹。</span><span class="sxs-lookup"><span data-stu-id="11613-118">When you open the Package Manager console or the Manager NuGet packages dialog, NuGet will check if the current solution has enabled the Package Restore mode and if any package files are missing from the `packages` folder.</span></span> <span data-ttu-id="11613-119">如果满足这两个条件，NuGet 会通知你，将显示一个方便访问的还原按钮。</span><span class="sxs-lookup"><span data-stu-id="11613-119">If these two conditions are met, NuGet will notify you and will show a convenient Restore button.</span></span> <span data-ttu-id="11613-120">单击此按钮会触发 NuGet 还原缺少的所有包。</span><span class="sxs-lookup"><span data-stu-id="11613-120">Clicking this button will trigger NuGet to restore all the missing packages.</span></span>

![在对话框中的包还原按钮](./media/packagerestore-dialog.png)

![在控制台上的包还原按钮](./media/packagerestore-console.png)

### <a name="add-solution-level-packagesconfig-file"></a><span data-ttu-id="11613-123">添加解决方案级 packages.config 文件</span><span class="sxs-lookup"><span data-stu-id="11613-123">Add solution-level packages.config file</span></span>
<span data-ttu-id="11613-124">在以前版本的 NuGet，每个项目具有`packages.config`文件，它将跟踪该项目中安装了哪些 NuGet 程序包。</span><span class="sxs-lookup"><span data-stu-id="11613-124">In previous versions of NuGet, each project has a `packages.config` file which keeps track of what NuGet packages are installed in that project.</span></span> <span data-ttu-id="11613-125">但是，没有类似文件在解决方案级别来跟踪解决方案级别包。</span><span class="sxs-lookup"><span data-stu-id="11613-125">However, there was no similar file at the solution level to keep track of solution-level packages.</span></span> <span data-ttu-id="11613-126">因此，没有方法来还原解决方案级别包。</span><span class="sxs-lookup"><span data-stu-id="11613-126">As a result, there was no way to restore solution-level packages.</span></span>
<span data-ttu-id="11613-127">在 NuGet 1.7 中现在实现此功能。</span><span class="sxs-lookup"><span data-stu-id="11613-127">This feature is now implemented in NuGet 1.7.</span></span> <span data-ttu-id="11613-128">解决方案级`packages.config`文件将位于下`.nuget`解决方案下的文件夹根，并将存储仅解决方案级别包。</span><span class="sxs-lookup"><span data-stu-id="11613-128">The solution-level `packages.config` file is placed under the `.nuget` folder under solution root and will store only solution-level packages.</span></span>

### <a name="remove-new-package-command"></a><span data-ttu-id="11613-129">删除新建包命令</span><span class="sxs-lookup"><span data-stu-id="11613-129">Remove New-Package command</span></span>
<span data-ttu-id="11613-130">由于低使用率，已删除新建程序包命令。</span><span class="sxs-lookup"><span data-stu-id="11613-130">Due to low usage, the New-Package command has been removed.</span></span> <span data-ttu-id="11613-131">开发人员建议使用 nuget.exe 或方便 NuGet 包资源管理器来创建包。</span><span class="sxs-lookup"><span data-stu-id="11613-131">Developers are recommended to use nuget.exe or the handy NuGet Package Explorer to create packages.</span></span>

## <a name="bug-fixes"></a><span data-ttu-id="11613-132">Bug 修复</span><span class="sxs-lookup"><span data-stu-id="11613-132">Bug Fixes</span></span>
<span data-ttu-id="11613-133">NuGet 1.7 已修复的包还原工作流和网络/源代码管理方案方面的许多缺陷。</span><span class="sxs-lookup"><span data-stu-id="11613-133">NuGet 1.7 has fixed many bugs around the Package Restore workflow and Network/Source Control scenarios.</span></span>

<span data-ttu-id="11613-134">有关完整列表的工作项中已修复 NuGet 1.7，请查看[对于此版本的 NuGet 问题跟踪程序](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Closed&type=All&priority=All&release=NuGet%201.7&assignedTo=All&component=All&sortField=Votes&sortDirection=Descending&page=0)。</span><span class="sxs-lookup"><span data-stu-id="11613-134">For a full list of work items fixed in NuGet 1.7, please view the [NuGet Issue Tracker for this release](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Closed&type=All&priority=All&release=NuGet%201.7&assignedTo=All&component=All&sortField=Votes&sortDirection=Descending&page=0).</span></span>
