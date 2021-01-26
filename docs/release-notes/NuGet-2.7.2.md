---
title: NuGet 2.7.2 发行说明
description: NuGet 2.7.2 的发行说明，包括已知问题、bug 修复、新增功能和 Dcr。
author: JonDouglas
ms.author: jodou
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 7643bf930bca39684eb626fe737001bc3e3ea769
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/26/2021
ms.locfileid: "98776787"
---
# <a name="nuget-272-release-notes"></a><span data-ttu-id="72a58-103">NuGet 2.7.2 发行说明</span><span class="sxs-lookup"><span data-stu-id="72a58-103">NuGet 2.7.2 Release Notes</span></span>

<span data-ttu-id="72a58-104">[NuGet 2.7.1 发行说明](../release-notes/nuget-2.7.1.md)  | [NuGet 2.8 发行说明](../release-notes/nuget-2.8.md)</span><span class="sxs-lookup"><span data-stu-id="72a58-104">[NuGet 2.7.1 Release Notes](../release-notes/nuget-2.7.1.md) | [NuGet 2.8 Release Notes](../release-notes/nuget-2.8.md)</span></span>

<span data-ttu-id="72a58-105">NuGet 2.7.2 于2013年11月11日发布。</span><span class="sxs-lookup"><span data-stu-id="72a58-105">NuGet 2.7.2 was released on November 11, 2013.</span></span>

## <a name="noteworthy-bug-fixes-and-features"></a><span data-ttu-id="72a58-106">值得注意的 Bug 修复和功能</span><span class="sxs-lookup"><span data-stu-id="72a58-106">Noteworthy Bug Fixes and Features</span></span>

### <a name="license-text"></a><span data-ttu-id="72a58-107">许可文本</span><span class="sxs-lookup"><span data-stu-id="72a58-107">License Text</span></span>
<span data-ttu-id="72a58-108">在很长一段时间内，Microsoft 在 Visual Studio 中为 Web 应用程序项目的默认模板包含了多个常用开源库的 NuGet 包。</span><span class="sxs-lookup"><span data-stu-id="72a58-108">For quite some time, Microsoft has included the NuGet packages for several popular open-source libraries as a part of the default templates for Web application projects in Visual Studio.</span></span> <span data-ttu-id="72a58-109">jQuery 可能是此类型库的最常见的示例。</span><span class="sxs-lookup"><span data-stu-id="72a58-109">jQuery is probably the most well-known example of this type of library.</span></span> <span data-ttu-id="72a58-110">由于与产品一起传送的组件相关联的支持协议，包的脚本文件包含不同的许可文本，而不是公共 nuget.org 库上同一个包中的脚本文件。</span><span class="sxs-lookup"><span data-stu-id="72a58-110">Because of the support agreement associated with components that are delivered along with a product, the package's script file contains different license text than the script file found in the same package on the public nuget.org gallery.</span></span> <span data-ttu-id="72a58-111">这种文本差异可能会导致包更新因不同的许可证文本块而无法继续进行，导致脚本文件 (的内容哈希值，因此在项目) 中被视为已修改。</span><span class="sxs-lookup"><span data-stu-id="72a58-111">This difference in text can prevent package updates from proceeding as a result of the different license text blocks causing the script files to have different content hash values (and therefore to be treated as modified within the project).</span></span>

<span data-ttu-id="72a58-112">为了缓解此问题，NuGet 2.7.2 允许脚本作者将许可证文本块包含在一个特别标记的部分中，如下所示。</span><span class="sxs-lookup"><span data-stu-id="72a58-112">To mitigate this issue, NuGet 2.7.2 allows the script author to include the license text block within a specially marked section which looks as follows.</span></span>

```
/************** NUGET: BEGIN LICENSE TEXT **************
    * The following code is licensed under the MIT license
    * Additional license information below is informational
    * only.
    ************** NUGET: END LICENSE TEXT ***************/
```

<span data-ttu-id="72a58-113">当更新包含包含此块的内容文件的包时，NuGet 不会将块的内容与 NuGet 库中的版本进行比较，因此，可以删除并更新内容文件，就像它与原始副本匹配一样。</span><span class="sxs-lookup"><span data-stu-id="72a58-113">When updating packages with content files containing this block, NuGet does not factor the contents of the block into the comparison with the version on the NuGet gallery, and can therefore delete and update the content file as though it matches the original copy.</span></span>

<span data-ttu-id="72a58-114">此块由文本 "NUGET： BEGIN LICENSE TEXT" 和 "NUGET： END LICENSE TEXT" 标识，出现在开始和结束行的任何位置。</span><span class="sxs-lookup"><span data-stu-id="72a58-114">This block is identified by the text "NUGET: BEGIN LICENSE TEXT" and "NUGET: END LICENSE TEXT" occurring anywhere on the beginning and ending lines.</span></span>  <span data-ttu-id="72a58-115">不存在其他格式设置要求，因此，无论使用何种语言，都可以在任何类型的文本文件中使用此功能。</span><span class="sxs-lookup"><span data-stu-id="72a58-115">No other formatting requirements exist, allowing this feature to be used in any type of text file regardless of language.</span></span>

### <a name="add-binding-redirects-for-non-framework-assemblies"></a><span data-ttu-id="72a58-116">添加非框架程序集的绑定重定向</span><span class="sxs-lookup"><span data-stu-id="72a58-116">Add Binding Redirects for non-Framework Assemblies</span></span>
<span data-ttu-id="72a58-117">对于作为 .NET Framework 一部分的程序集，NuGet 将在更新包时跳过将绑定重定向添加到应用程序的配置文件中。</span><span class="sxs-lookup"><span data-stu-id="72a58-117">For assemblies that are part of the .NET Framework, NuGet skips adding binding redirects into the application's configuration file when updating the package.</span></span> <span data-ttu-id="72a58-118">此修补程序解决了 NuGet 2.7 中的回归，因为没有为某些程序集添加绑定重定向，即使不将这些程序集视为 .NET Framework 的一部分。</span><span class="sxs-lookup"><span data-stu-id="72a58-118">This fix addresses a regression in NuGet 2.7 whereby binding redirects were not being added for some assemblies, even though those assemblies are not considered a part of the .NET Framework.</span></span> <span data-ttu-id="72a58-119">NuGet 2.7.2 将还原以前的 NuGet 2.5 和2.6 行为，并添加绑定重定向。</span><span class="sxs-lookup"><span data-stu-id="72a58-119">NuGet 2.7.2 restores the previous NuGet 2.5 and 2.6 behavior and adds the binding redirects.</span></span>

### <a name="installing-portable-libraries-with-xamarin-tools-installed"></a><span data-ttu-id="72a58-120">安装安装了 Xamarin 工具的可移植库</span><span class="sxs-lookup"><span data-stu-id="72a58-120">Installing portable libraries with Xamarin Tools installed</span></span>
<span data-ttu-id="72a58-121">当 Xamarin 的开发工具安装在计算机上时，它们将修改支持的框架配置数据以指定现有目标框架组合和 Xamarin 框架之间的兼容性。</span><span class="sxs-lookup"><span data-stu-id="72a58-121">When Xamarin's development tools are installed on a machine, they modify the supported frameworks configuration data to specify compatibility between existing target framework combinations and Xamarin frameworks.</span></span> <span data-ttu-id="72a58-122">利用版本2.7.2，NuGet 现在可以识别这些隐式兼容性规则，并因此使面向 Xamarin 平台的开发人员可以轻松地安装与 Xamarin 兼容但未在包元数据本身中显式标记为这样的可移植库。</span><span class="sxs-lookup"><span data-stu-id="72a58-122">With version 2.7.2, NuGet is now aware of these implicit compatibility rules, and therefore makes it easy for developers targeting Xamarin platforms to install portable libraries that are Xamarin-compatible but not explicitly marked as such in the package metadata itself.</span></span>

### <a name="machine-wide-configuration-settings-honored"></a><span data-ttu-id="72a58-123">计算机范围的配置设置生效</span><span class="sxs-lookup"><span data-stu-id="72a58-123">Machine-wide configuration settings honored</span></span>
<span data-ttu-id="72a58-124">使用分层 Nuget.Config 文件时，对于最接近于解决方案根的 Nuget.Config 文件，repositoryPath 键将不起作用。</span><span class="sxs-lookup"><span data-stu-id="72a58-124">When using hierarchical Nuget.Config files, the repositoryPath key was not being honored for Nuget.Config files closest to the solution root.</span></span> <span data-ttu-id="72a58-125">在 Visual Studio 2013 中，NuGet 将在% ProgramData% \NuGet\Config\VisualStudio\12.0\Microsoft.VisualStudio.config 上安装一个自定义 Nuget.Config 文件，以便添加 "Microsoft 和 .NET" 包源。</span><span class="sxs-lookup"><span data-stu-id="72a58-125">In Visual Studio 2013, NuGet installs a custom Nuget.Config file at %ProgramData%\NuGet\Config\VisualStudio\12.0\Microsoft.VisualStudio.config in order to add the "Microsoft and .NET" package source.</span></span> <span data-ttu-id="72a58-126">因此，在解决方案中使用自定义 repositoryPath 的解决方法是删除计算机级别 Nuget.Config-这也意味着删除 "Microsoft 和 .NET" 包源。</span><span class="sxs-lookup"><span data-stu-id="72a58-126">As a result, the work-around for using a custom repositoryPath in a solution was to delete the machine-level Nuget.Config - which also meant removing the "Microsoft and .NET" package source.</span></span> <span data-ttu-id="72a58-127">在使用分层 Nuget.Config 文件时，NuGet 2.7.2 现在遵循 repositoryPath 的优先规则。</span><span class="sxs-lookup"><span data-stu-id="72a58-127">NuGet 2.7.2 now honors the precedence rules for repositoryPath when using hierarchical Nuget.Config files.</span></span>

## <a name="all-changes"></a><span data-ttu-id="72a58-128">所有更改</span><span class="sxs-lookup"><span data-stu-id="72a58-128">All Changes</span></span>
<span data-ttu-id="72a58-129">有关 NuGet 2.7.2 中修复的工作项的完整列表，请查看 [此版本的 NuGet 问题跟踪程序](https://nuget.codeplex.com/workitem/list/advanced?keyword=&status=All&type=All&priority=All&release=NuGet%202.7.2&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0&reasonClosed=Fixed)。</span><span class="sxs-lookup"><span data-stu-id="72a58-129">For a full list of work items fixed in NuGet 2.7.2, please view the [NuGet Issue Tracker for this release](https://nuget.codeplex.com/workitem/list/advanced?keyword=&status=All&type=All&priority=All&release=NuGet%202.7.2&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0&reasonClosed=Fixed).</span></span>
