---
title: NuGet 2.7.2 发行说明
description: 发行说明，了解 NuGet 2.7.2 包括已知问题、 bug 修复、 增加的功能，以及 DCRs。
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 0cb99e4e1ae9238286dc4fab7b8d34e5b117ed64
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/26/2018
---
# <a name="nuget-272-release-notes"></a><span data-ttu-id="ee973-103">NuGet 2.7.2 发行说明</span><span class="sxs-lookup"><span data-stu-id="ee973-103">NuGet 2.7.2 Release Notes</span></span>

<span data-ttu-id="ee973-104">[NuGet 2.7.1 发行说明](../release-notes/nuget-2.7.1.md) | [NuGet 2.8 发行说明](../release-notes/nuget-2.8.md)</span><span class="sxs-lookup"><span data-stu-id="ee973-104">[NuGet 2.7.1 Release Notes](../release-notes/nuget-2.7.1.md) | [NuGet 2.8 Release Notes](../release-notes/nuget-2.8.md)</span></span>

<span data-ttu-id="ee973-105">NuGet 2.7.2 已于 2013 年 11 月 11 日发布。</span><span class="sxs-lookup"><span data-stu-id="ee973-105">NuGet 2.7.2 was released on November 11, 2013.</span></span>

## <a name="noteworthy-bug-fixes-and-features"></a><span data-ttu-id="ee973-106">值得注意的 Bug 修补程序和功能</span><span class="sxs-lookup"><span data-stu-id="ee973-106">Noteworthy Bug Fixes and Features</span></span>

### <a name="license-text"></a><span data-ttu-id="ee973-107">许可证文本</span><span class="sxs-lookup"><span data-stu-id="ee973-107">License Text</span></span>
<span data-ttu-id="ee973-108">很长一段时间，Microsoft 具有 Visual Studio 中包含的 Web 应用程序项目的默认模板一部分的几个常用的开源库的 NuGet 包。</span><span class="sxs-lookup"><span data-stu-id="ee973-108">For quite some time, Microsoft has included the NuGet packages for several popular open-source libraries as a part of the default templates for Web application projects in Visual Studio.</span></span> <span data-ttu-id="ee973-109">jQuery 可能是库的这种类型的已知示例。</span><span class="sxs-lookup"><span data-stu-id="ee973-109">jQuery is probably the most well-known example of this type of library.</span></span> <span data-ttu-id="ee973-110">由于与随产品一起传递的组件相关的支持协议，包的脚本文件包含其他许可证文本中比在公共 nuget.org 库上位于同一个包的脚本文件。</span><span class="sxs-lookup"><span data-stu-id="ee973-110">Because of the support agreement associated with components that are delivered along with a product, the package's script file contains different license text than the script file found in the same package on the public nuget.org gallery.</span></span> <span data-ttu-id="ee973-111">文本这种差异可以防止由于导致要具有不同的内容哈希值的脚本文件的其他许可证文本块继续包更新 （并因此被视为修改项目中）。</span><span class="sxs-lookup"><span data-stu-id="ee973-111">This difference in text can prevent package updates from proceeding as a result of the different license text blocks causing the script files to have different content hash values (and therefore to be treated as modified within the project).</span></span>

<span data-ttu-id="ee973-112">若要缓解此问题，NuGet 2.7.2 允许脚本作者以包括如下所示的特殊标记部分中的许可证文本块。</span><span class="sxs-lookup"><span data-stu-id="ee973-112">To mitigate this issue, NuGet 2.7.2 allows the script author to include the license text block within a specially marked section which looks as follows.</span></span>

    /************** NUGET: BEGIN LICENSE TEXT **************
     * The following code is licensed under the MIT license
     * Additional license information below is informational
     * only.
     ************** NUGET: END LICENSE TEXT ***************/

<span data-ttu-id="ee973-113">更新包的内容时文件，其中包含此块中，NuGet 不等因素如何影响块中的内容与 NuGet 库上的版本的比较结果和可以因此删除和更新内容文件，就好像它与匹配的原始副本。</span><span class="sxs-lookup"><span data-stu-id="ee973-113">When updating packages with content files containing this block, NuGet does not factor the contents of the block into the comparison with the version on the NuGet gallery, and can therefore delete and update the content file as though it matches the original copy.</span></span>

<span data-ttu-id="ee973-114">通过文本"NUGET:: 开始许可证 TEXT"和"NUGET:: 许可证文本结束"发生任何位置上开始和结束行标识此块。</span><span class="sxs-lookup"><span data-stu-id="ee973-114">This block is identified by the text "NUGET: BEGIN LICENSE TEXT" and "NUGET: END LICENSE TEXT" occurring anywhere on the beginning and ending lines.</span></span>  <span data-ttu-id="ee973-115">没有其他格式设置要求存在，允许要在任何一种文本文件，而不考虑语言中使用此功能。</span><span class="sxs-lookup"><span data-stu-id="ee973-115">No other formatting requirements exist, allowing this feature to be used in any type of text file regardless of language.</span></span>

### <a name="add-binding-redirects-for-non-framework-assemblies"></a><span data-ttu-id="ee973-116">添加绑定重定向的非 Framework 程序集</span><span class="sxs-lookup"><span data-stu-id="ee973-116">Add Binding Redirects for non-Framework Assemblies</span></span>
<span data-ttu-id="ee973-117">对于属于.NET Framework 的程序集，NuGet 时，跳过添加绑定重定向到应用程序的配置文件更新包。</span><span class="sxs-lookup"><span data-stu-id="ee973-117">For assemblies that are part of the .NET Framework, NuGet skips adding binding redirects into the application's configuration file when updating the package.</span></span> <span data-ttu-id="ee973-118">此修补程序地址，由此绑定重定向正在添加的某些程序集，即使这些程序集不是 NuGet 2.7 中的回归被认为.NET Framework 的一部分。</span><span class="sxs-lookup"><span data-stu-id="ee973-118">This fix addresses a regression in NuGet 2.7 whereby binding redirects were not being added for some assemblies, even though those assemblies are not considered a part of the .NET Framework.</span></span> <span data-ttu-id="ee973-119">NuGet 2.7.2 还原以前的 NuGet 2.5 和 2.6 行为，并将添加的绑定重定向。</span><span class="sxs-lookup"><span data-stu-id="ee973-119">NuGet 2.7.2 restores the previous NuGet 2.5 and 2.6 behavior and adds the binding redirects.</span></span>

### <a name="installing-portable-libraries-with-xamarin-tools-installed"></a><span data-ttu-id="ee973-120">使用安装的 Xamarin 工具安装的可移植库</span><span class="sxs-lookup"><span data-stu-id="ee973-120">Installing portable libraries with Xamarin Tools installed</span></span>
<span data-ttu-id="ee973-121">当在计算机上安装了 Xamarin 的开发工具时，他们将修改要指定现有的目标 framework 组合和 Xamarin 框架之间的兼容性的支持的框架配置数据。</span><span class="sxs-lookup"><span data-stu-id="ee973-121">When Xamarin's development tools are installed on a machine, they modify the supported frameworks configuration data to specify compatibility between existing target framework combinations and Xamarin frameworks.</span></span> <span data-ttu-id="ee973-122">使用版本 2.7.2，NuGet 目前感知这些隐式的兼容性的规则，并且因此轻松地针对 Xamarin 平台的开发人员包中的这种情况下安装 Xamarin 兼容，但未显式标记的可移植库元数据本身。</span><span class="sxs-lookup"><span data-stu-id="ee973-122">With version 2.7.2, NuGet is now aware of these implicit compatibility rules, and therefore makes it easy for developers targeting Xamarin platforms to install portable libraries that are Xamarin-compatible but not explicitly marked as such in the package metadata itself.</span></span>

### <a name="machine-wide-configuration-settings-honored"></a><span data-ttu-id="ee973-123">遵循的计算机范围的配置设置</span><span class="sxs-lookup"><span data-stu-id="ee973-123">Machine-wide configuration settings honored</span></span>
<span data-ttu-id="ee973-124">使用分层 Nuget.Config 文件时，repositoryPath 密钥不被接受 Nuget.Config 文件接近解决方案根。</span><span class="sxs-lookup"><span data-stu-id="ee973-124">When using hierarchical Nuget.Config files, the repositoryPath key was not being honored for Nuget.Config files closest to the solution root.</span></span> <span data-ttu-id="ee973-125">在 Visual Studio 2013 中，NuGet 安装自定义在 %ProgramData%\NuGet\Config\VisualStudio\12.0\Microsoft.VisualStudio.config Nuget.Config 文件以添加"Microsoft 和.NET"包源。</span><span class="sxs-lookup"><span data-stu-id="ee973-125">In Visual Studio 2013, NuGet installs a custom Nuget.Config file at %ProgramData%\NuGet\Config\VisualStudio\12.0\Microsoft.VisualStudio.config in order to add the "Microsoft and .NET" package source.</span></span> <span data-ttu-id="ee973-126">因此，解决办法在解决方案中使用自定义 repositoryPath 是删除计算机级别 Nuget.Config-这还意味着删除"Microsoft 和.NET"包源。</span><span class="sxs-lookup"><span data-stu-id="ee973-126">As a result, the work-around for using a custom repositoryPath in a solution was to delete the machine-level Nuget.Config - which also meant removing the "Microsoft and .NET" package source.</span></span> <span data-ttu-id="ee973-127">使用分层 Nuget.Config 文件时，NuGet 2.7.2 现在服从 repositoryPath 的优先顺序规则。</span><span class="sxs-lookup"><span data-stu-id="ee973-127">NuGet 2.7.2 now honors the precedence rules for repositoryPath when using hierarchical Nuget.Config files.</span></span>

## <a name="all-changes"></a><span data-ttu-id="ee973-128">所有更改</span><span class="sxs-lookup"><span data-stu-id="ee973-128">All Changes</span></span>
<span data-ttu-id="ee973-129">有关工作的完整列表项固定在 NuGet 2.7.2，请查看[对于此版本的 NuGet 问题跟踪程序](https://nuget.codeplex.com/workitem/list/advanced?keyword=&status=All&type=All&priority=All&release=NuGet%202.7.2&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0&reasonClosed=Fixed)。</span><span class="sxs-lookup"><span data-stu-id="ee973-129">For a full list of work items fixed in NuGet 2.7.2, please view the [NuGet Issue Tracker for this release](https://nuget.codeplex.com/workitem/list/advanced?keyword=&status=All&type=All&priority=All&release=NuGet%202.7.2&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0&reasonClosed=Fixed).</span></span>
