---
title: NuGet 2.7.2 发行说明
description: NuGet 2.7.2，它包括的发行说明的已知问题、 bug 修复、 新增的功能和 Dcr。
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 3e63944a05f66d5dadf17c5d4b91d3bc4478bb33
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/04/2018
ms.locfileid: "43550065"
---
# <a name="nuget-272-release-notes"></a><span data-ttu-id="102c1-103">NuGet 2.7.2 发行说明</span><span class="sxs-lookup"><span data-stu-id="102c1-103">NuGet 2.7.2 Release Notes</span></span>

<span data-ttu-id="102c1-104">[NuGet 2.7.1 发行说明](../release-notes/nuget-2.7.1.md) | [NuGet 2.8 发行说明](../release-notes/nuget-2.8.md)</span><span class="sxs-lookup"><span data-stu-id="102c1-104">[NuGet 2.7.1 Release Notes](../release-notes/nuget-2.7.1.md) | [NuGet 2.8 Release Notes](../release-notes/nuget-2.8.md)</span></span>

<span data-ttu-id="102c1-105">NuGet 2.7.2，它已于 2013 年 11 月 11 日发布。</span><span class="sxs-lookup"><span data-stu-id="102c1-105">NuGet 2.7.2 was released on November 11, 2013.</span></span>

## <a name="noteworthy-bug-fixes-and-features"></a><span data-ttu-id="102c1-106">值得注意的 Bug 修复和功能</span><span class="sxs-lookup"><span data-stu-id="102c1-106">Noteworthy Bug Fixes and Features</span></span>

### <a name="license-text"></a><span data-ttu-id="102c1-107">许可证文本</span><span class="sxs-lookup"><span data-stu-id="102c1-107">License Text</span></span>
<span data-ttu-id="102c1-108">一段时间，Microsoft 已包含在 Visual Studio 为 Web 应用程序项目的默认模板的一部分的几个常用的开源库的 NuGet 包。</span><span class="sxs-lookup"><span data-stu-id="102c1-108">For quite some time, Microsoft has included the NuGet packages for several popular open-source libraries as a part of the default templates for Web application projects in Visual Studio.</span></span> <span data-ttu-id="102c1-109">jQuery 可能是库的这种类型的最常见示例。</span><span class="sxs-lookup"><span data-stu-id="102c1-109">jQuery is probably the most well-known example of this type of library.</span></span> <span data-ttu-id="102c1-110">由于与产品一起提供的组件关联的支持协议，包的脚本文件包含不同的许可证文本中比在同一个包中找到公共 nuget.org 库上的脚本文件。</span><span class="sxs-lookup"><span data-stu-id="102c1-110">Because of the support agreement associated with components that are delivered along with a product, the package's script file contains different license text than the script file found in the same package on the public nuget.org gallery.</span></span> <span data-ttu-id="102c1-111">这种文本的差异可以防止由于导致要具有不同的内容哈希值的脚本文件的其他许可证文本块继续包更新 （并因此被视为在项目中修改）。</span><span class="sxs-lookup"><span data-stu-id="102c1-111">This difference in text can prevent package updates from proceeding as a result of the different license text blocks causing the script files to have different content hash values (and therefore to be treated as modified within the project).</span></span>

<span data-ttu-id="102c1-112">若要缓解此问题，NuGet 2.7.2，它允许脚本作者以包括如下所示的特殊标记部分中的许可证文本块。</span><span class="sxs-lookup"><span data-stu-id="102c1-112">To mitigate this issue, NuGet 2.7.2 allows the script author to include the license text block within a specially marked section which looks as follows.</span></span>

    /************** NUGET: BEGIN LICENSE TEXT **************
     * The following code is licensed under the MIT license
     * Additional license information below is informational
     * only.
     ************** NUGET: END LICENSE TEXT ***************/

<span data-ttu-id="102c1-113">当更新包的内容文件，其中包含此块中，NuGet 不会不块的内容，应考虑使用 NuGet 库上的版本比较和可以因此删除和更新内容文件，就好像它匹配的原始副本。</span><span class="sxs-lookup"><span data-stu-id="102c1-113">When updating packages with content files containing this block, NuGet does not factor the contents of the block into the comparison with the version on the NuGet gallery, and can therefore delete and update the content file as though it matches the original copy.</span></span>

<span data-ttu-id="102c1-114">由文本"NUGET:: BEGIN 许可证 TEXT"和"NUGET:: 结束许可证 TEXT"发生任意位置上开始和结束行标识此块。</span><span class="sxs-lookup"><span data-stu-id="102c1-114">This block is identified by the text "NUGET: BEGIN LICENSE TEXT" and "NUGET: END LICENSE TEXT" occurring anywhere on the beginning and ending lines.</span></span>  <span data-ttu-id="102c1-115">没有其他格式设置要求存在，可让在任何类型的文本与语言无关的文件中使用此功能。</span><span class="sxs-lookup"><span data-stu-id="102c1-115">No other formatting requirements exist, allowing this feature to be used in any type of text file regardless of language.</span></span>

### <a name="add-binding-redirects-for-non-framework-assemblies"></a><span data-ttu-id="102c1-116">添加绑定重定向为非 Framework 程序集</span><span class="sxs-lookup"><span data-stu-id="102c1-116">Add Binding Redirects for non-Framework Assemblies</span></span>
<span data-ttu-id="102c1-117">对于属于.NET Framework 的程序集，NuGet 将跳过添加绑定重定向到应用程序的配置文件更新包时。</span><span class="sxs-lookup"><span data-stu-id="102c1-117">For assemblies that are part of the .NET Framework, NuGet skips adding binding redirects into the application's configuration file when updating the package.</span></span> <span data-ttu-id="102c1-118">此修补程序地址，由此绑定重定向不添加对于某些程序集，即使这些程序集不是 NuGet 2.7 中的回归视为.NET Framework 的一部分。</span><span class="sxs-lookup"><span data-stu-id="102c1-118">This fix addresses a regression in NuGet 2.7 whereby binding redirects were not being added for some assemblies, even though those assemblies are not considered a part of the .NET Framework.</span></span> <span data-ttu-id="102c1-119">NuGet 2.7.2，它将还原以前的 NuGet 2.5 和 2.6 行为，并将添加绑定重定向。</span><span class="sxs-lookup"><span data-stu-id="102c1-119">NuGet 2.7.2 restores the previous NuGet 2.5 and 2.6 behavior and adds the binding redirects.</span></span>

### <a name="installing-portable-libraries-with-xamarin-tools-installed"></a><span data-ttu-id="102c1-120">使用安装了 Xamarin 工具安装可移植库</span><span class="sxs-lookup"><span data-stu-id="102c1-120">Installing portable libraries with Xamarin Tools installed</span></span>
<span data-ttu-id="102c1-121">当在计算机上安装 Xamarin 的开发工具时，它们修改要指定现有的目标框架组合和 Xamarin 框架之间的兼容性的支持的框架配置数据。</span><span class="sxs-lookup"><span data-stu-id="102c1-121">When Xamarin's development tools are installed on a machine, they modify the supported frameworks configuration data to specify compatibility between existing target framework combinations and Xamarin frameworks.</span></span> <span data-ttu-id="102c1-122">2.7.2，它在版本，NuGet 会了解这样的隐式的兼容性规则，并因此可以轻松面向 Xamarin 平台的开发人员能够在包中这种情况下安装 Xamarin 兼容，但未显式标记的可移植库元数据本身。</span><span class="sxs-lookup"><span data-stu-id="102c1-122">With version 2.7.2, NuGet is now aware of these implicit compatibility rules, and therefore makes it easy for developers targeting Xamarin platforms to install portable libraries that are Xamarin-compatible but not explicitly marked as such in the package metadata itself.</span></span>

### <a name="machine-wide-configuration-settings-honored"></a><span data-ttu-id="102c1-123">接受的计算机范围的配置设置</span><span class="sxs-lookup"><span data-stu-id="102c1-123">Machine-wide configuration settings honored</span></span>
<span data-ttu-id="102c1-124">使用分层 Nuget.Config 文件时，repositoryPath 密钥不被接受 Nuget.Config 文件接近解决方案根目录。</span><span class="sxs-lookup"><span data-stu-id="102c1-124">When using hierarchical Nuget.Config files, the repositoryPath key was not being honored for Nuget.Config files closest to the solution root.</span></span> <span data-ttu-id="102c1-125">在 Visual Studio 2013 中，NuGet 安装自定义在 %ProgramData%\NuGet\Config\VisualStudio\12.0\Microsoft.VisualStudio.config Nuget.Config 文件以添加"Microsoft 和.NET"包源。</span><span class="sxs-lookup"><span data-stu-id="102c1-125">In Visual Studio 2013, NuGet installs a custom Nuget.Config file at %ProgramData%\NuGet\Config\VisualStudio\12.0\Microsoft.VisualStudio.config in order to add the "Microsoft and .NET" package source.</span></span> <span data-ttu-id="102c1-126">因此，解决在解决方案中使用自定义 repositoryPath 是删除计算机级别 Nuget.Config-这也意味着删除"Microsoft 和.NET"包源。</span><span class="sxs-lookup"><span data-stu-id="102c1-126">As a result, the work-around for using a custom repositoryPath in a solution was to delete the machine-level Nuget.Config - which also meant removing the "Microsoft and .NET" package source.</span></span> <span data-ttu-id="102c1-127">使用分层 Nuget.Config 文件时，NuGet 2.7.2，它现在遵循 repositoryPath 的优先顺序规则。</span><span class="sxs-lookup"><span data-stu-id="102c1-127">NuGet 2.7.2 now honors the precedence rules for repositoryPath when using hierarchical Nuget.Config files.</span></span>

## <a name="all-changes"></a><span data-ttu-id="102c1-128">所有更改</span><span class="sxs-lookup"><span data-stu-id="102c1-128">All Changes</span></span>
<span data-ttu-id="102c1-129">有关完整列表的工作项中已修复 NuGet 2.7.2，它，请查看[对于此版本的 NuGet 问题跟踪程序](https://nuget.codeplex.com/workitem/list/advanced?keyword=&status=All&type=All&priority=All&release=NuGet%202.7.2&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0&reasonClosed=Fixed)。</span><span class="sxs-lookup"><span data-stu-id="102c1-129">For a full list of work items fixed in NuGet 2.7.2, please view the [NuGet Issue Tracker for this release](https://nuget.codeplex.com/workitem/list/advanced?keyword=&status=All&type=All&priority=All&release=NuGet%202.7.2&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0&reasonClosed=Fixed).</span></span>
