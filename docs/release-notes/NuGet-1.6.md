---
title: NuGet 1.6 发行说明
description: NuGet 1.6 的发行说明，包括已知问题、bug 修复、新增功能和 Dcr。
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 2878d3809b2be4fb71f4e7b1a1e08e405ead44b9
ms.sourcegitcommit: 26a8eae00af2d4be581171e7a73009f94534c336
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/25/2019
ms.locfileid: "75384132"
---
 # <a name="nuget-16-release-notes"></a><span data-ttu-id="b1a6d-103">NuGet 1.6 发行说明</span><span class="sxs-lookup"><span data-stu-id="b1a6d-103">NuGet 1.6 Release Notes</span></span>

<span data-ttu-id="b1a6d-104">[Nuget 1.5 发行说明](../release-notes/nuget-1.5.md) | [Nuget 1.7 发行说明](../release-notes/nuget-1.7.md)</span><span class="sxs-lookup"><span data-stu-id="b1a6d-104">[NuGet 1.5 Release Notes](../release-notes/nuget-1.5.md) | [NuGet 1.7 Release Notes](../release-notes/nuget-1.7.md)</span></span>

<span data-ttu-id="b1a6d-105">NuGet 1.6 于2011年12月13日发布。</span><span class="sxs-lookup"><span data-stu-id="b1a6d-105">NuGet 1.6 was released on December 13, 2011.</span></span>

## <a name="known-installation-issue"></a><span data-ttu-id="b1a6d-106">已知安装问题</span><span class="sxs-lookup"><span data-stu-id="b1a6d-106">Known Installation Issue</span></span>
<span data-ttu-id="b1a6d-107">如果你运行的是 VS 2010 SP1，但如果你安装了较旧的版本，你可能会遇到安装错误。</span><span class="sxs-lookup"><span data-stu-id="b1a6d-107">If you are running VS 2010 SP1, you might run into an installation error when attempting to upgrade NuGet if you have an older version installed.</span></span>

<span data-ttu-id="b1a6d-108">解决方法是仅卸载 NuGet，然后从 VS 扩展库安装它。</span><span class="sxs-lookup"><span data-stu-id="b1a6d-108">The workaround is to simply uninstall NuGet and then install it from the VS Extension Gallery.</span></span>  <span data-ttu-id="b1a6d-109">有关更多信息，请参见<https://support.microsoft.com/kb/2581019>。</span><span class="sxs-lookup"><span data-stu-id="b1a6d-109">See <https://support.microsoft.com/kb/2581019> for more information.</span></span>

<span data-ttu-id="b1a6d-110">注意：如果 Visual Studio 不允许你卸载扩展（"卸载" 按钮已禁用），则可能需要使用 "以管理员身份运行" 重启 Visual Studio。</span><span class="sxs-lookup"><span data-stu-id="b1a6d-110">Note: If Visual Studio won't allow you to uninstall the extension (the Uninstall button is disabled), then you likely need to restart Visual Studio using "Run as Administrator."</span></span>

## <a name="features"></a><span data-ttu-id="b1a6d-111">特征</span><span class="sxs-lookup"><span data-stu-id="b1a6d-111">Features</span></span>

### <a name="support-for-semantic-versioning-and-prerelease-packages"></a><span data-ttu-id="b1a6d-112">支持语义版本控制和预发行包</span><span class="sxs-lookup"><span data-stu-id="b1a6d-112">Support for Semantic Versioning and Prerelease Packages</span></span>
<span data-ttu-id="b1a6d-113">NuGet 1.6 引入了对语义版本控制（SemVer）的支持。</span><span class="sxs-lookup"><span data-stu-id="b1a6d-113">NuGet 1.6 introduces support for Semantic Versioning (SemVer).</span></span> <span data-ttu-id="b1a6d-114">有关如何使用 SemVer 的更多详细信息，请参阅[版本控制文档](../create-packages/prerelease-packages.md)。</span><span class="sxs-lookup"><span data-stu-id="b1a6d-114">For more details on how it uses SemVer, read the [Versioning documentation](../create-packages/prerelease-packages.md).</span></span>

### <a name="using-nuget-without-checking-in-packages-package-restore"></a><span data-ttu-id="b1a6d-115">使用 NuGet 而不签入包（包还原）</span><span class="sxs-lookup"><span data-stu-id="b1a6d-115">Using NuGet Without Checking In Packages (Package Restore)</span></span>
<span data-ttu-id="b1a6d-116">NuGet 1.6 现在提供对工作流的第一类支持，其中 NuGet 包未添加到源代码管理中，但在生成时将在缺少时还原。</span><span class="sxs-lookup"><span data-stu-id="b1a6d-116">NuGet 1.6 now has first class support for the workflow in which NuGet packages are not added to source control, but instead are restored at build time if missing.</span></span> <span data-ttu-id="b1a6d-117">有关更多详细信息，请阅读[使用 NuGet 但不将包提交到源代码管理](../consume-packages/packages-and-source-control.md)主题。</span><span class="sxs-lookup"><span data-stu-id="b1a6d-117">For more details, read the [Using NuGet without committing packages to source control](../consume-packages/packages-and-source-control.md) topic.</span></span>

### <a name="item-templates-that-install-nuget-packages"></a><span data-ttu-id="b1a6d-118">安装 NuGet 包的项模板</span><span class="sxs-lookup"><span data-stu-id="b1a6d-118">Item Templates That Install NuGet Packages</span></span>
<span data-ttu-id="b1a6d-119">基于支持预安装 NuGet 包的工作以支持 Visual Studio 项目模板，NuGet 1.6 还添加了对 Visual Studio 项模板的支持。</span><span class="sxs-lookup"><span data-stu-id="b1a6d-119">Building on the work to support preinstalled NuGet package to Visual Studio project templates, NuGet 1.6 also adds support for Visual Studio item templates.</span></span> <span data-ttu-id="b1a6d-120">项模板可以具有在调用模板时安装的关联 NuGet 包。</span><span class="sxs-lookup"><span data-stu-id="b1a6d-120">Item templates can have associated NuGet packages that are installed when the template in invoked.</span></span>

<span data-ttu-id="b1a6d-121">有关如何更改项目/项模板以安装 NuGet 包的详细信息，请阅读[Visual Studio 模板中的包](../visual-studio-extensibility/visual-studio-templates.md)主题。</span><span class="sxs-lookup"><span data-stu-id="b1a6d-121">For more details on how to change a project/item template to install NuGet packages, read the [Packages in Visual Studio Templates](../visual-studio-extensibility/visual-studio-templates.md) topic.</span></span>

### <a name="support-for-disabling-package-sources"></a><span data-ttu-id="b1a6d-122">支持禁用包源</span><span class="sxs-lookup"><span data-stu-id="b1a6d-122">Support for disabling package sources</span></span>
<span data-ttu-id="b1a6d-123">当配置了多个包源时，NuGet 将在包及其依赖项的安装过程中为包查找每个源。</span><span class="sxs-lookup"><span data-stu-id="b1a6d-123">When multiple package sources are configured, NuGet will look in each one for packages during installation of a package and its dependencies.</span></span> <span data-ttu-id="b1a6d-124">出于某种原因关闭的包源可能严重降低了 NuGet 速度。</span><span class="sxs-lookup"><span data-stu-id="b1a6d-124">A package source that is down for some reason can severely slow down NuGet.</span></span>

<span data-ttu-id="b1a6d-125">在 NuGet 1.6 之前，你可以删除包源，但当你想要将其重新添加时，必须记住的详细信息。</span><span class="sxs-lookup"><span data-stu-id="b1a6d-125">Prior to NuGet 1.6, you could remove the package source, but then you have to remember the details for when you want to add it back in.</span></span>

<span data-ttu-id="b1a6d-126">NuGet 1.6 允许不选中包源来禁用它，但要进行保留。</span><span class="sxs-lookup"><span data-stu-id="b1a6d-126">NuGet 1.6 allows unchecking a package source to disable it, but keep it around.</span></span>

![禁用包](./media/package-source-with-disabled-source.png)

## <a name="bug-fixes"></a><span data-ttu-id="b1a6d-128">Bug 修复</span><span class="sxs-lookup"><span data-stu-id="b1a6d-128">Bug Fixes</span></span>
<span data-ttu-id="b1a6d-129">NuGet 1.6 总共修复了106个工作项。</span><span class="sxs-lookup"><span data-stu-id="b1a6d-129">NuGet 1.6 had a total of 106 work items fixed.</span></span> <span data-ttu-id="b1a6d-130">其中的95归类为 bug，其中10个是功能。</span><span class="sxs-lookup"><span data-stu-id="b1a6d-130">95 of those were classified as bugs and 10 of those were features.</span></span>

<span data-ttu-id="b1a6d-131">有关 NuGet 1.6 中已修复的工作项的完整列表，请查看[此版本的 NuGet 问题跟踪程序](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Closed&type=All&priority=All&release=NuGet%201.6&assignedTo=All&component=All&sortField=Votes&sortDirection=Descending&page=0)。</span><span class="sxs-lookup"><span data-stu-id="b1a6d-131">For a full list of work items fixed in NuGet 1.6, please view the [NuGet Issue Tracker for this release](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Closed&type=All&priority=All&release=NuGet%201.6&assignedTo=All&component=All&sortField=Votes&sortDirection=Descending&page=0).</span></span>
