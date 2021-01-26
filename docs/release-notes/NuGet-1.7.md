---
title: NuGet 1.7 发行说明
description: NuGet 1.7 的发行说明，包括已知问题、bug 修复、新增功能和 Dcr。
author: JonDouglas
ms.author: jodou
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 50eb326c5ada4f74685b07c0d1b0f84b14e547ac
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/26/2021
ms.locfileid: "98777068"
---
# <a name="nuget-17-release-notes"></a><span data-ttu-id="ae638-103">NuGet 1.7 发行说明</span><span class="sxs-lookup"><span data-stu-id="ae638-103">NuGet 1.7 Release Notes</span></span>

<span data-ttu-id="ae638-104">[NuGet 1.6 发行说明](../release-notes/nuget-1.6.md)  | [NuGet 1.8 发行说明](../release-notes/nuget-1.8.md)</span><span class="sxs-lookup"><span data-stu-id="ae638-104">[NuGet 1.6 Release Notes](../release-notes/nuget-1.6.md) | [NuGet 1.8 Release Notes](../release-notes/nuget-1.8.md)</span></span>

<span data-ttu-id="ae638-105">NuGet 1.7 于年4月 4 2012 日发布。</span><span class="sxs-lookup"><span data-stu-id="ae638-105">NuGet 1.7 was released on April 4, 2012.</span></span>

## <a name="known-installation-issue"></a><span data-ttu-id="ae638-106">已知安装问题</span><span class="sxs-lookup"><span data-stu-id="ae638-106">Known Installation Issue</span></span>
<span data-ttu-id="ae638-107">如果你运行的是 VS 2010 SP1，但如果你安装了较旧的版本，你可能会遇到安装错误。</span><span class="sxs-lookup"><span data-stu-id="ae638-107">If you are running VS 2010 SP1, you might run into an installation error when attempting to upgrade NuGet if you have an older version installed.</span></span>

<span data-ttu-id="ae638-108">解决方法是仅卸载 NuGet，然后从 VS 扩展库安装它。</span><span class="sxs-lookup"><span data-stu-id="ae638-108">The workaround is to simply uninstall NuGet and then install it from the VS Extension Gallery.</span></span>  <span data-ttu-id="ae638-109">有关更多信息，请参见<https://support.microsoft.com/kb/2581019>。</span><span class="sxs-lookup"><span data-stu-id="ae638-109">See <https://support.microsoft.com/kb/2581019> for more information.</span></span>

<span data-ttu-id="ae638-110">注意：如果 Visual Studio 不允许卸载扩展 (禁用了 "卸载" 按钮) ，则可能需要使用 "以管理员身份运行" 重启 Visual Studio。</span><span class="sxs-lookup"><span data-stu-id="ae638-110">Note: If Visual Studio won't allow you to uninstall the extension (the Uninstall button is disabled), then you likely need to restart Visual Studio using "Run as Administrator."</span></span>

## <a name="features"></a><span data-ttu-id="ae638-111">功能</span><span class="sxs-lookup"><span data-stu-id="ae638-111">Features</span></span>

### <a name="support-opening-readmetxt-file-after-installation"></a><span data-ttu-id="ae638-112">支持在安装后打开 readme.txt 文件</span><span class="sxs-lookup"><span data-stu-id="ae638-112">Support opening readme.txt file after installation</span></span>
<span data-ttu-id="ae638-113">1.7 中的新增内容，如果你 `readme.txt` 的包在包的根目录中包含一个文件，则在安装完包之后，NuGet 将自动打开此文件。</span><span class="sxs-lookup"><span data-stu-id="ae638-113">New in 1.7, if your package includes a `readme.txt` file at the root of the package, NuGet will automatically open this file after it's finished installing your package.</span></span>

### <a name="show-prerelease-packages-in-the-manage-nuget-packages-dialog"></a><span data-ttu-id="ae638-114">在 "管理 NuGet 包" 对话框中显示预发行包</span><span class="sxs-lookup"><span data-stu-id="ae638-114">Show prerelease packages in the Manage NuGet packages dialog</span></span>
<span data-ttu-id="ae638-115">"管理 NuGet 包" 对话框现在包含一个下拉列表，其中提供了显示预发行包的选项。</span><span class="sxs-lookup"><span data-stu-id="ae638-115">The Manage NuGet Packages dialog now includes a dropdown which provides option to show prerelease packages.</span></span>

![显示预发行包](./media/prerelease-dropdown.png)

### <a name="show-package-restore-button-when-package-files-are-missing"></a><span data-ttu-id="ae638-117">缺少包文件时显示 "包还原" 按钮</span><span class="sxs-lookup"><span data-stu-id="ae638-117">Show Package Restore button when package files are missing</span></span>
<span data-ttu-id="ae638-118">打开 "程序包管理器控制台" 或 "管理器 NuGet 包" 对话框时，NuGet 将检查当前解决方案是否已启用包还原模式，以及文件夹中是否缺少任何包文件 `packages` 。</span><span class="sxs-lookup"><span data-stu-id="ae638-118">When you open the Package Manager console or the Manager NuGet packages dialog, NuGet will check if the current solution has enabled the Package Restore mode and if any package files are missing from the `packages` folder.</span></span> <span data-ttu-id="ae638-119">如果满足这两个条件，NuGet 会通知你，并显示一个便利的 "还原" 按钮。</span><span class="sxs-lookup"><span data-stu-id="ae638-119">If these two conditions are met, NuGet will notify you and will show a convenient Restore button.</span></span> <span data-ttu-id="ae638-120">单击此按钮将触发 NuGet 以还原所有缺少的包。</span><span class="sxs-lookup"><span data-stu-id="ae638-120">Clicking this button will trigger NuGet to restore all the missing packages.</span></span>

![对话框上的 "包还原" 按钮](./media/packagerestore-dialog.png)

![控制台上的 "包还原" 按钮](./media/packagerestore-console.png)

### <a name="add-solution-level-packagesconfig-file"></a><span data-ttu-id="ae638-123">添加解决方案级 packages.config 文件</span><span class="sxs-lookup"><span data-stu-id="ae638-123">Add solution-level packages.config file</span></span>
<span data-ttu-id="ae638-124">在 NuGet 的早期版本中，每个项目都有一个 `packages.config` 文件，该文件跟踪在该项目中安装的 NuGet 包。</span><span class="sxs-lookup"><span data-stu-id="ae638-124">In previous versions of NuGet, each project has a `packages.config` file which keeps track of what NuGet packages are installed in that project.</span></span> <span data-ttu-id="ae638-125">不过，解决方案级别没有类似的文件来跟踪解决方案级包。</span><span class="sxs-lookup"><span data-stu-id="ae638-125">However, there was no similar file at the solution level to keep track of solution-level packages.</span></span> <span data-ttu-id="ae638-126">因此，无法还原解决方案级包。</span><span class="sxs-lookup"><span data-stu-id="ae638-126">As a result, there was no way to restore solution-level packages.</span></span>
<span data-ttu-id="ae638-127">此功能现已在 NuGet 1.7 中实现。</span><span class="sxs-lookup"><span data-stu-id="ae638-127">This feature is now implemented in NuGet 1.7.</span></span> <span data-ttu-id="ae638-128">解决方案级文件位于 `packages.config` `.nuget` 解决方案根下的文件夹下，并且将仅存储解决方案级包。</span><span class="sxs-lookup"><span data-stu-id="ae638-128">The solution-level `packages.config` file is placed under the `.nuget` folder under solution root and will store only solution-level packages.</span></span>

### <a name="remove-new-package-command"></a><span data-ttu-id="ae638-129">删除 New-Package 命令</span><span class="sxs-lookup"><span data-stu-id="ae638-129">Remove New-Package command</span></span>
<span data-ttu-id="ae638-130">由于使用率低，已删除 New-Package 命令。</span><span class="sxs-lookup"><span data-stu-id="ae638-130">Due to low usage, the New-Package command has been removed.</span></span> <span data-ttu-id="ae638-131">建议开发人员使用 nuget.exe 或便捷的 NuGet 包资源管理器来创建包。</span><span class="sxs-lookup"><span data-stu-id="ae638-131">Developers are recommended to use nuget.exe or the handy NuGet Package Explorer to create packages.</span></span>

## <a name="bug-fixes"></a><span data-ttu-id="ae638-132">Bug 修复</span><span class="sxs-lookup"><span data-stu-id="ae638-132">Bug Fixes</span></span>
<span data-ttu-id="ae638-133">NuGet 1.7 在包还原工作流和网络/源代码管理方案周围修复了很多 bug。</span><span class="sxs-lookup"><span data-stu-id="ae638-133">NuGet 1.7 has fixed many bugs around the Package Restore workflow and Network/Source Control scenarios.</span></span>

<span data-ttu-id="ae638-134">有关 NuGet 1.7 中已修复的工作项的完整列表，请查看 [此版本的 NuGet 问题跟踪程序](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Closed&type=All&priority=All&release=NuGet%201.7&assignedTo=All&component=All&sortField=Votes&sortDirection=Descending&page=0)。</span><span class="sxs-lookup"><span data-stu-id="ae638-134">For a full list of work items fixed in NuGet 1.7, please view the [NuGet Issue Tracker for this release](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Closed&type=All&priority=All&release=NuGet%201.7&assignedTo=All&component=All&sortField=Votes&sortDirection=Descending&page=0).</span></span>
