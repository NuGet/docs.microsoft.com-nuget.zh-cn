---
title: NuGet 1.6 版说明
description: 发行说明适用于 NuGet 1.6 包括已知的问题、 bug 修复、 新增的功能和 Dcr。
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 351303ca3ae27a37c19e59d84dfc9b4629fe0ca5
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/04/2018
ms.locfileid: "43549007"
---
 # <a name="nuget-16-release-notes"></a><span data-ttu-id="193d0-103">NuGet 1.6 版说明</span><span class="sxs-lookup"><span data-stu-id="193d0-103">NuGet 1.6 Release Notes</span></span>

<span data-ttu-id="193d0-104">[NuGet 1.5 发行说明](../release-notes/nuget-1.5.md) | [NuGet 1.7 发行说明](../release-notes/nuget-1.7.md)</span><span class="sxs-lookup"><span data-stu-id="193d0-104">[NuGet 1.5 Release Notes](../release-notes/nuget-1.5.md) | [NuGet 1.7 Release Notes](../release-notes/nuget-1.7.md)</span></span>

<span data-ttu-id="193d0-105">NuGet 1.6 已于 2011 年 12 月 13 日发布。</span><span class="sxs-lookup"><span data-stu-id="193d0-105">NuGet 1.6 was released on December 13, 2011.</span></span>

## <a name="known-installation-issue"></a><span data-ttu-id="193d0-106">已知的安装问题</span><span class="sxs-lookup"><span data-stu-id="193d0-106">Known Installation Issue</span></span>
<span data-ttu-id="193d0-107">如果运行 VS 2010 SP1，你可能会遇到安装错误，尝试升级 NuGet，如果您有安装了旧版本时。</span><span class="sxs-lookup"><span data-stu-id="193d0-107">If you are running VS 2010 SP1, you might run into an installation error when attempting to upgrade NuGet if you have an older version installed.</span></span>

<span data-ttu-id="193d0-108">解决方法是简单地卸载 NuGet，然后从 VS 扩展库安装它。</span><span class="sxs-lookup"><span data-stu-id="193d0-108">The workaround is to simply uninstall NuGet and then install it from the VS Extension Gallery.</span></span>  <span data-ttu-id="193d0-109">有关详细信息，请参阅 [http://support.microsoft.com/kb/2581019](http://support.microsoft.com/kb/2581019)。</span><span class="sxs-lookup"><span data-stu-id="193d0-109">See [http://support.microsoft.com/kb/2581019](http://support.microsoft.com/kb/2581019) for more information.</span></span>

<span data-ttu-id="193d0-110">注意： 如果 Visual Studio 不会使您可以卸载的扩展 （卸载按钮被禁用），然后您可能需要重启 Visual Studio 中使用"以管理员身份运行"。</span><span class="sxs-lookup"><span data-stu-id="193d0-110">Note: If Visual Studio won't allow you to uninstall the extension (the Uninstall button is disabled), then you likely need to restart Visual Studio using "Run as Administrator."</span></span>

## <a name="features"></a><span data-ttu-id="193d0-111">功能</span><span class="sxs-lookup"><span data-stu-id="193d0-111">Features</span></span>

### <a name="support-for-semantic-versioning-and-prerelease-packages"></a><span data-ttu-id="193d0-112">对语义化版本控制和预发行包的支持</span><span class="sxs-lookup"><span data-stu-id="193d0-112">Support for Semantic Versioning and Prerelease Packages</span></span>
<span data-ttu-id="193d0-113">NuGet 1.6 引入了对语义化版本控制 (SemVer) 支持。</span><span class="sxs-lookup"><span data-stu-id="193d0-113">NuGet 1.6 introduces support for Semantic Versioning (SemVer).</span></span> <span data-ttu-id="193d0-114">有关如何使用 SemVer 的详细信息，请阅读[版本控制文档](../create-packages/prerelease-packages.md)。</span><span class="sxs-lookup"><span data-stu-id="193d0-114">For more details on how it uses SemVer, read the [Versioning documentation](../create-packages/prerelease-packages.md).</span></span>

### <a name="using-nuget-without-checking-in-packages-package-restore"></a><span data-ttu-id="193d0-115">不检查包 （包还原） 中使用 NuGet</span><span class="sxs-lookup"><span data-stu-id="193d0-115">Using NuGet Without Checking In Packages (Package Restore)</span></span>
<span data-ttu-id="193d0-116">NuGet 1.6 现在具有对工作流中的 NuGet 包不会添加到源代码管理，但改为会还原在生成时如果缺少第一类支持。</span><span class="sxs-lookup"><span data-stu-id="193d0-116">NuGet 1.6 now has first class support for the workflow in which NuGet packages are not added to source control, but instead are restored at build time if missing.</span></span> <span data-ttu-id="193d0-117">有关更多详细信息，请阅读[而包提交到源代码管理不使用 NuGet](../consume-packages/packages-and-source-control.md)主题。</span><span class="sxs-lookup"><span data-stu-id="193d0-117">For more details, read the [Using NuGet without committing packages to source control](../consume-packages/packages-and-source-control.md) topic.</span></span>

### <a name="item-templates-that-install-nuget-packages"></a><span data-ttu-id="193d0-118">安装 NuGet 包的项模板</span><span class="sxs-lookup"><span data-stu-id="193d0-118">Item Templates That Install NuGet Packages</span></span>
<span data-ttu-id="193d0-119">基础上运行以支持 Visual Studio 项目模板的预安装的 NuGet 包，NuGet 1.6 还将添加对 Visual Studio 项模板的支持。</span><span class="sxs-lookup"><span data-stu-id="193d0-119">Building on the work to support preinstalled NuGet package to Visual Studio project templates, NuGet 1.6 also adds support for Visual Studio item templates.</span></span> <span data-ttu-id="193d0-120">项模板可以具有关联的调用中的模板时安装的 NuGet 包。</span><span class="sxs-lookup"><span data-stu-id="193d0-120">Item templates can have associated NuGet packages that are installed when the template in invoked.</span></span>

<span data-ttu-id="193d0-121">有关如何更改要安装 NuGet 包的项目/项模板的更多详细信息，请阅读[Visual Studio 模板中的包](../visual-studio-extensibility/visual-studio-templates.md)主题。</span><span class="sxs-lookup"><span data-stu-id="193d0-121">For more details on how to change a project/item template to install NuGet packages, read the [Packages in Visual Studio Templates](../visual-studio-extensibility/visual-studio-templates.md) topic.</span></span>

### <a name="support-for-disabling-package-sources"></a><span data-ttu-id="193d0-122">禁用包源的支持</span><span class="sxs-lookup"><span data-stu-id="193d0-122">Support for disabling package sources</span></span>
<span data-ttu-id="193d0-123">当配置多个包源时，NuGet 将期间安装的包及其依赖项，查找每个包中。</span><span class="sxs-lookup"><span data-stu-id="193d0-123">When multiple package sources are configured, NuGet will look in each one for packages during installation of a package and its dependencies.</span></span> <span data-ttu-id="193d0-124">已关闭的一些原因会严重降低 NuGet 包源。</span><span class="sxs-lookup"><span data-stu-id="193d0-124">A package source that is down for some reason can severely slow down NuGet.</span></span>

<span data-ttu-id="193d0-125">在 NuGet 1.6 之前, 无法删除包的来源，但然后，必须记住的详细信息时，你想要将其添加回。</span><span class="sxs-lookup"><span data-stu-id="193d0-125">Prior to NuGet 1.6, you could remove the package source, but then you have to remember the details for when you want to add it back in.</span></span>

<span data-ttu-id="193d0-126">NuGet 1.6，取消选中要禁用它，但将其保留的包源。</span><span class="sxs-lookup"><span data-stu-id="193d0-126">NuGet 1.6 allows unchecking a package source to disable it, but keep it around.</span></span>

![禁用包](./media/package-source-with-disabled-source.png)

## <a name="bug-fixes"></a><span data-ttu-id="193d0-128">Bug 修复</span><span class="sxs-lookup"><span data-stu-id="193d0-128">Bug Fixes</span></span>
<span data-ttu-id="193d0-129">NuGet 1.6 必须总共 106 个工作项已修复。</span><span class="sxs-lookup"><span data-stu-id="193d0-129">NuGet 1.6 had a total of 106 work items fixed.</span></span> <span data-ttu-id="193d0-130">其中的 95 被分类为 bug 并且 10 的那些功能。</span><span class="sxs-lookup"><span data-stu-id="193d0-130">95 of those were classified as bugs and 10 of those were features.</span></span>

<span data-ttu-id="193d0-131">有关工作的完整列表项中已修复 NuGet 1.6，请查看[对于此版本的 NuGet 问题跟踪程序](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Closed&type=All&priority=All&release=NuGet%201.6&assignedTo=All&component=All&sortField=Votes&sortDirection=Descending&page=0)。</span><span class="sxs-lookup"><span data-stu-id="193d0-131">For a full list of work items fixed in NuGet 1.6, please view the [NuGet Issue Tracker for this release](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Closed&type=All&priority=All&release=NuGet%201.6&assignedTo=All&component=All&sortField=Votes&sortDirection=Descending&page=0).</span></span>
