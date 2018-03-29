---
title: NuGet 1.2 发行说明 |Microsoft 文档
author: karann-msft
ms.author: karann-msft
manager: ghogen
ms.date: 11/11/2016
ms.topic: article
ms.prod: nuget
ms.technology: ''
description: 包括已知的问题、 bug 修复、 增加的功能，以及 DCRs NuGet 1.2 的发行说明。
keywords: NuGet 1.2 发行说明，bug 修复的已知问题，添加了一些功能，DCRs
ms.reviewer:
- karann-msft
- unniravindranathan
ms.workload:
- dotnet
- aspnet
ms.openlocfilehash: 0d95f41c5bc5d490764c9f128ee621e1037cef66
ms.sourcegitcommit: beb229893559824e8abd6ab16707fd5fe1c6ac26
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/28/2018
---
# <a name="nuget-12-release-notes"></a><span data-ttu-id="4c68c-104">NuGet 1.2 发行说明</span><span class="sxs-lookup"><span data-stu-id="4c68c-104">NuGet 1.2 Release Notes</span></span>

<span data-ttu-id="4c68c-105">[NuGet 1.0 和 1.1 发行说明](../release-notes/nuget-1.1.md) | [NuGet 1.3 发行说明](../release-notes/nuget-1.3.md)</span><span class="sxs-lookup"><span data-stu-id="4c68c-105">[NuGet 1.0 and 1.1 Release Notes](../release-notes/nuget-1.1.md) | [NuGet 1.3 Release Notes](../release-notes/nuget-1.3.md)</span></span>

<span data-ttu-id="4c68c-106">NuGet 1.2 已于 2011 年 3 月 30 日发布。</span><span class="sxs-lookup"><span data-stu-id="4c68c-106">NuGet 1.2 was released on March 30, 2011.</span></span>

## <a name="new-features"></a><span data-ttu-id="4c68c-107">新增功能</span><span class="sxs-lookup"><span data-stu-id="4c68c-107">New Features</span></span>

### <a name="framework-profile-support"></a><span data-ttu-id="4c68c-108">框架配置文件支持</span><span class="sxs-lookup"><span data-stu-id="4c68c-108">Framework Profile Support</span></span>

<span data-ttu-id="4c68c-109">开始时，请从 NuGet 支持具有不同的框架作为目标的库。</span><span class="sxs-lookup"><span data-stu-id="4c68c-109">From the start, NuGet supported having libraries target different frameworks.</span></span> <span data-ttu-id="4c68c-110">但现在包可能包含程序集面向特定的配置文件，如 Windows Phone 配置文件。</span><span class="sxs-lookup"><span data-stu-id="4c68c-110">But now packages may contain assemblies that target specific profiles such as the Windows Phone profile.</span></span> <span data-ttu-id="4c68c-111">若要针对特定框架的配置文件，追加划线后跟的配置文件缩写。</span><span class="sxs-lookup"><span data-stu-id="4c68c-111">To target a specific profile of a framework, append a dash followed by the profile abbreviation.</span></span> <span data-ttu-id="4c68c-112">例如，若要针对 Windows Phone (又称 Windows Phone 7) 上运行的 SilverLight，你可以将程序集在 sl3 wp 文件夹如以下屏幕截图中所示。</span><span class="sxs-lookup"><span data-stu-id="4c68c-112">For example, to target SilverLight running on a Windows Phone (aka Windows Phone 7), you can put an assembly in the sl3-wp folder as demonstrated in the following screenshot.</span></span>

![Framework 配置文件文件夹布局](./media/framework-profile-support.png)

<span data-ttu-id="4c68c-114">您可能会问为何我们未只需选择要用作标记"wp7"。</span><span class="sxs-lookup"><span data-stu-id="4c68c-114">You might ask why we didn’t just choose to use “wp7” as the moniker.</span></span> <span data-ttu-id="4c68c-115">在情况下，我们要预测，Windows Phone 7 可能在将来运行 Silverlight 的较新版本，在这种情况下你可能需要将更细致地指出哪些框架的配置文件是针对。</span><span class="sxs-lookup"><span data-stu-id="4c68c-115">In part, we’re anticipating that Windows Phone 7 might run a newer version of Silverlight in the future, in which case you may need to be more specific about which framework profile you’re targetting.</span></span>

### <a name="automatically-add-binding-redirects"></a><span data-ttu-id="4c68c-116">自动添加绑定重定向</span><span class="sxs-lookup"><span data-stu-id="4c68c-116">Automatically Add Binding Redirects</span></span>

<span data-ttu-id="4c68c-117">当使用强名称程序集安装包，NuGet 可以现在会检测项目需要绑定重定向添加到项目后，若要编译并自动将其添加顺序中的配置文件的情况。</span><span class="sxs-lookup"><span data-stu-id="4c68c-117">When installing a package with strong named assemblies, NuGet can now detect cases where the project requires binding redirects to be added to the configuration file in order for the project to compile and add them automatically.</span></span> <span data-ttu-id="4c68c-118">第 3 部分 David Ebbo 的博客文章系列中的 NuGet 版本控制标题为"[通过绑定将重定向的统一](http://blog.davidebbo.com/2011/01/nuget-versioning-part-3-unification-via.html)"介绍此功能的更多详细信息的用途。</span><span class="sxs-lookup"><span data-stu-id="4c68c-118">Part 3 of David Ebbo’s blog post series on NuGet Versioning entitled “[Unification via Binding Redirects](http://blog.davidebbo.com/2011/01/nuget-versioning-part-3-unification-via.html)” covers the purpose of this feature in more details.</span></span>

<a name="framework-assembly-refs"></a>

### <a name="specifying-framework-assembly-references-gac"></a><span data-ttu-id="4c68c-119">指定 Framework 程序集引用 (GAC)</span><span class="sxs-lookup"><span data-stu-id="4c68c-119">Specifying Framework Assembly References (GAC)</span></span>

<span data-ttu-id="4c68c-120">在某些情况下，包可能依赖于.NET Framework 中的程序集中。</span><span class="sxs-lookup"><span data-stu-id="4c68c-120">In some cases, a package may depend on an assembly that’s in the .NET Framework.</span></span> <span data-ttu-id="4c68c-121">严格地说，它并不总是需要你的包的使用者引用 framework 程序集。</span><span class="sxs-lookup"><span data-stu-id="4c68c-121">Strictly speaking, it’s not always necessary that the consumer of your package reference the framework assembly.</span></span> <span data-ttu-id="4c68c-122">但在某些情况下，很重要，例如开发人员需要对该程序集中的类型的代码才能使用你的包。</span><span class="sxs-lookup"><span data-stu-id="4c68c-122">But in some cases, it's important, such as when the developer needs to code against types in that assembly in order to use your package.</span></span> <span data-ttu-id="4c68c-123">新`frameworkAssemblies`元素，元数据元素的子元素允许你指定的一组`frameworkAssembly`指向 Framework 程序集在 gac 中的元素。</span><span class="sxs-lookup"><span data-stu-id="4c68c-123">The new `frameworkAssemblies` element, a child element of the metadata element, allows you to specify a set of `frameworkAssembly` elements pointing to a Framework assembly in the GAC.</span></span> <span data-ttu-id="4c68c-124">请注意主要侧重于 Framework 程序集。</span><span class="sxs-lookup"><span data-stu-id="4c68c-124">Note the emphasis on Framework assembly.</span></span>
<span data-ttu-id="4c68c-125">这些程序集不包含在你的包中，因为它们被假定为每台计算机上作为.NET Framework 的一部分。</span><span class="sxs-lookup"><span data-stu-id="4c68c-125">These assemblies are not included in your package as they are assumed to be on every machine  as part of the .NET Framework.</span></span> <span data-ttu-id="4c68c-126">下表列出的属性`frameworkAssembly`元素。</span><span class="sxs-lookup"><span data-stu-id="4c68c-126">The following table lists attributes of the `frameworkAssembly` element.</span></span>


|<span data-ttu-id="4c68c-127">特性</span><span class="sxs-lookup"><span data-stu-id="4c68c-127">Attribute</span></span> |<span data-ttu-id="4c68c-128">描述</span><span class="sxs-lookup"><span data-stu-id="4c68c-128">Description</span></span>|
|----------------|-----------|
|<span data-ttu-id="4c68c-129">**assemblyName**</span><span class="sxs-lookup"><span data-stu-id="4c68c-129">**assemblyName**</span></span>|<span data-ttu-id="4c68c-130">*所需*。</span><span class="sxs-lookup"><span data-stu-id="4c68c-130">*Required*.</span></span> <span data-ttu-id="4c68c-131">如程序集名称`System.Net`。</span><span class="sxs-lookup"><span data-stu-id="4c68c-131">Name of the assembly such as `System.Net`.</span></span>|
|<span data-ttu-id="4c68c-132">**targetFramework**</span><span class="sxs-lookup"><span data-stu-id="4c68c-132">**targetFramework**</span></span>|<span data-ttu-id="4c68c-133">*可选*。</span><span class="sxs-lookup"><span data-stu-id="4c68c-133">*Optional*.</span></span> <span data-ttu-id="4c68c-134">允许指定的框架和配置文件的名称 （或别名），此框架程序集适用于如"net40"或"sl4"。</span><span class="sxs-lookup"><span data-stu-id="4c68c-134">Allows specifying a framework and profile name (or alias) that this framework assembly applies to such as "net40" or "sl4".</span></span> <span data-ttu-id="4c68c-135">使用相同的格式中所述[支持多个目标框架](../create-packages/supporting-multiple-target-frameworks.md)。</span><span class="sxs-lookup"><span data-stu-id="4c68c-135">Uses the same format described in [Supporting Multiple Target Frameworks](../create-packages/supporting-multiple-target-frameworks.md).</span></span>|

```xml
  <frameworkAssemblies>
    <frameworkAssembly assemblyName="System.ComponentModel.DataAnnotations" targetFramework="net40" />
    <frameworkAssembly assemblyName="System.ServiceModel" targetFramework="net40" />
  </frameworkAssemblies>
```

### <a name="nugetexe-now-is-able-to-store-api-key-credentials"></a><span data-ttu-id="4c68c-136">nuget.exe 现在是能够存储 API 密钥凭据</span><span class="sxs-lookup"><span data-stu-id="4c68c-136">nuget.exe now is able to store API Key credentials</span></span>

<span data-ttu-id="4c68c-137">使用 nuget.exe 命令行工具时，你现在可以使用 SetApiKey 命令来存储你的 API 密钥。</span><span class="sxs-lookup"><span data-stu-id="4c68c-137">When using the nuget.exe command line tool, you can now use the SetApiKey command to store your API key.</span></span> <span data-ttu-id="4c68c-138">这样一来，你不需要每次推送包时指定它。</span><span class="sxs-lookup"><span data-stu-id="4c68c-138">That way, you won’t need to specify it every time you push a package.</span></span> <span data-ttu-id="4c68c-139">有关详细信息使用 nuget.exe，保存你的 API 密钥[读取该文档描述有关发布包](../create-packages/publish-a-package.md)。</span><span class="sxs-lookup"><span data-stu-id="4c68c-139">For more details on saving your API key with nuget.exe, [read the documentation on publishing a package](../create-packages/publish-a-package.md).</span></span>

### <a name="package-explorer"></a><span data-ttu-id="4c68c-140">包资源管理器</span><span class="sxs-lookup"><span data-stu-id="4c68c-140">Package Explorer</span></span>
<span data-ttu-id="4c68c-141">包资源管理器已更新为支持 NuGet 1.2。</span><span class="sxs-lookup"><span data-stu-id="4c68c-141">Package Explorer has been updated to support NuGet 1.2.</span></span> <span data-ttu-id="4c68c-142">有关详细信息，请参阅[包资源管理器发行说明](http://nuget.codeplex.com/wikipage?title=New%20features%20in%20NuGet%20Package%20Explorer%201.0)。</span><span class="sxs-lookup"><span data-stu-id="4c68c-142">For more information, check out the [Package Explorer release notes](http://nuget.codeplex.com/wikipage?title=New%20features%20in%20NuGet%20Package%20Explorer%201.0).</span></span>

## <a name="other-featuresfixes"></a><span data-ttu-id="4c68c-143">其他功能/修补程序</span><span class="sxs-lookup"><span data-stu-id="4c68c-143">Other features/fixes</span></span>

<span data-ttu-id="4c68c-144">前面的列表是最为明显的许多我们实现的功能和我们解决的 bug。</span><span class="sxs-lookup"><span data-stu-id="4c68c-144">The previous list were the most noticeable of the many features we implemented and bugs we fixed.</span></span> <span data-ttu-id="4c68c-145">总之，我们实现/修复[59 工作项](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=All&type=All&priority=All&release=NuGet%201.2&assignedTo=All&component=All&sortField=Votes&sortDirection=Descending&page=0)在此版本中。</span><span class="sxs-lookup"><span data-stu-id="4c68c-145">All in all, we implemented/fixed [59 work items](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=All&type=All&priority=All&release=NuGet%201.2&assignedTo=All&component=All&sortField=Votes&sortDirection=Descending&page=0) in this release.</span></span>

## <a name="known-issues"></a><span data-ttu-id="4c68c-146">已知问题</span><span class="sxs-lookup"><span data-stu-id="4c68c-146">Known Issues</span></span>

* <span data-ttu-id="4c68c-147">**1.2 包不兼容性**： 用命令行工具的最新版本的包生成的 nuget.exe (> 1.2) 不会使用较旧版本的 NuGet VS 外接程序 （如 1.1)。</span><span class="sxs-lookup"><span data-stu-id="4c68c-147">**1.2 Package incompatibility**: Packages built with the latest version of the command line tool, nuget.exe (> 1.2) will not work with older versions of the NuGet VS Add-in (such as 1.1).</span></span> <span data-ttu-id="4c68c-148">如果遇到错误消息，表明一些有关不兼容的架构时，你是否遇到了此错误。</span><span class="sxs-lookup"><span data-stu-id="4c68c-148">If you run into an error message stating something about incompatible schema, you are running into this error.</span></span> <span data-ttu-id="4c68c-149">请更新到最新版本的 NuGet。</span><span class="sxs-lookup"><span data-stu-id="4c68c-149">Please update NuGet to the latest version.</span></span>
* <span data-ttu-id="4c68c-150">**NuGet.Server 不兼容性**： 如果你要托管源使用 NuGet.Server 项目内部 NuGet，你将需要 NuGet.Server 为最新版本更新该项目。</span><span class="sxs-lookup"><span data-stu-id="4c68c-150">**NuGet.Server incompatibility**: If you’re hosting an internal NuGet feed using the NuGet.Server project, you’ll need to update that project with the latest version of NuGet.Server.</span></span>
* <span data-ttu-id="4c68c-151">**签名不匹配错误**： 如果有关签名不匹配的消息升级期间遇到错误，则需要首先卸载 NuGet，然后安装它。</span><span class="sxs-lookup"><span data-stu-id="4c68c-151">**Signature Mismatch Error**: If you run into an error during an upgrade with a message about a Signature Mismatch, you need to uninstall NuGet first and then install it.</span></span> <span data-ttu-id="4c68c-152">这被列入我们[已知问题页](../release-notes/known-issues.md)它提供更多详细信息。</span><span class="sxs-lookup"><span data-stu-id="4c68c-152">This is listed in our [Known Issues page](../release-notes/known-issues.md) which provides more details.</span></span> <span data-ttu-id="4c68c-153">此问题仅影响那些运行 Visual Studio 2010 SP1，并具有 NuGet 1.0 安装不正确签名的版本。</span><span class="sxs-lookup"><span data-stu-id="4c68c-153">The issue only affects those running Visual Studio 2010 SP1 and have a version of NuGet 1.0 installed that was incorrectly signed.</span></span> <span data-ttu-id="4c68c-154">此版本已仅可从 CodePlex 网站在短时间内使此问题不应影响太多的人。</span><span class="sxs-lookup"><span data-stu-id="4c68c-154">This version was only made available from the CodePlex website for a brief period so this issue shouldn't affect too many people.</span></span>