---
title: NuGet 1.2 发行说明
description: NuGet 1.2 的发行说明，包括已知问题、bug 修复、新增功能和 Dcr。
author: JonDouglas
ms.author: jodou
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: af2248a41800f7641be9b77d7bb72e2a94d4ce47
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/26/2021
ms.locfileid: "98777202"
---
# <a name="nuget-12-release-notes"></a><span data-ttu-id="00526-103">NuGet 1.2 发行说明</span><span class="sxs-lookup"><span data-stu-id="00526-103">NuGet 1.2 Release Notes</span></span>

<span data-ttu-id="00526-104">[NuGet 1.0 和1.1 发行说明](../release-notes/nuget-1.1.md)  | [NuGet 1.3 发行说明](../release-notes/nuget-1.3.md)</span><span class="sxs-lookup"><span data-stu-id="00526-104">[NuGet 1.0 and 1.1 Release Notes](../release-notes/nuget-1.1.md) | [NuGet 1.3 Release Notes](../release-notes/nuget-1.3.md)</span></span>

<span data-ttu-id="00526-105">NuGet 1.2 于年3月 30 2011 日发布。</span><span class="sxs-lookup"><span data-stu-id="00526-105">NuGet 1.2 was released on March 30, 2011.</span></span>

## <a name="new-features"></a><span data-ttu-id="00526-106">新功能</span><span class="sxs-lookup"><span data-stu-id="00526-106">New Features</span></span>

### <a name="framework-profile-support"></a><span data-ttu-id="00526-107">框架配置文件支持</span><span class="sxs-lookup"><span data-stu-id="00526-107">Framework Profile Support</span></span>

<span data-ttu-id="00526-108">从开始，NuGet 支持的库以不同的框架为目标。</span><span class="sxs-lookup"><span data-stu-id="00526-108">From the start, NuGet supported having libraries target different frameworks.</span></span> <span data-ttu-id="00526-109">但现在，包可能包含面向特定配置文件（如 Windows Phone 配置文件）的程序集。</span><span class="sxs-lookup"><span data-stu-id="00526-109">But now packages may contain assemblies that target specific profiles such as the Windows Phone profile.</span></span> <span data-ttu-id="00526-110">若要以框架的特定配置文件为目标，请追加一条短划线，后跟配置文件缩写。</span><span class="sxs-lookup"><span data-stu-id="00526-110">To target a specific profile of a framework, append a dash followed by the profile abbreviation.</span></span> <span data-ttu-id="00526-111">例如，若要将 (Windows Phone 上运行的 SilverLight 定位 Windows Phone 7) ，可以将程序集放入 sl3 wp 文件夹中，如以下屏幕截图所示。</span><span class="sxs-lookup"><span data-stu-id="00526-111">For example, to target SilverLight running on a Windows Phone (aka Windows Phone 7), you can put an assembly in the sl3-wp folder as demonstrated in the following screenshot.</span></span>

![框架配置文件文件夹布局](./media/framework-profile-support.png)

<span data-ttu-id="00526-113">您可能会问为什么我们不只选择使用 "wp7" 作为名字对象。</span><span class="sxs-lookup"><span data-stu-id="00526-113">You might ask why we didn’t just choose to use “wp7” as the moniker.</span></span> <span data-ttu-id="00526-114">在部分中，我们将预测到 Windows Phone 7 以后可能会运行较新版本的 Silverlight，在这种情况下，你可能需要更具体地了解要针对哪个框架配置文件。</span><span class="sxs-lookup"><span data-stu-id="00526-114">In part, we’re anticipating that Windows Phone 7 might run a newer version of Silverlight in the future, in which case you may need to be more specific about which framework profile you’re targetting.</span></span>

### <a name="automatically-add-binding-redirects"></a><span data-ttu-id="00526-115">自动添加绑定重定向</span><span class="sxs-lookup"><span data-stu-id="00526-115">Automatically Add Binding Redirects</span></span>

<span data-ttu-id="00526-116">当安装具有强名称程序集的包时，NuGet 现在可以检测项目需要将绑定重定向添加到配置文件中的情况，以便项目自动编译和添加它们。</span><span class="sxs-lookup"><span data-stu-id="00526-116">When installing a package with strong named assemblies, NuGet can now detect cases where the project requires binding redirects to be added to the configuration file in order for the project to compile and add them automatically.</span></span> <span data-ttu-id="00526-117">"David Ebbo 的博客文章系列" 中的第3部分 "NuGet 版本管理" "[通过绑定重定向](http://blog.davidebbo.com/2011/01/nuget-versioning-part-3-unification-via.html)" 包含此功能的更多详细信息。</span><span class="sxs-lookup"><span data-stu-id="00526-117">Part 3 of David Ebbo’s blog post series on NuGet Versioning entitled “[Unification via Binding Redirects](http://blog.davidebbo.com/2011/01/nuget-versioning-part-3-unification-via.html)” covers the purpose of this feature in more details.</span></span>

<a name="framework-assembly-refs"></a>

### <a name="specifying-framework-assembly-references-gac"></a><span data-ttu-id="00526-118">指定 Framework 程序集引用 (GAC) </span><span class="sxs-lookup"><span data-stu-id="00526-118">Specifying Framework Assembly References (GAC)</span></span>

<span data-ttu-id="00526-119">在某些情况下，包可能依赖于 .NET Framework 中的程序集。</span><span class="sxs-lookup"><span data-stu-id="00526-119">In some cases, a package may depend on an assembly that’s in the .NET Framework.</span></span> <span data-ttu-id="00526-120">严格地说，包的使用者并非始终需要引用框架程序集。</span><span class="sxs-lookup"><span data-stu-id="00526-120">Strictly speaking, it’s not always necessary that the consumer of your package reference the framework assembly.</span></span> <span data-ttu-id="00526-121">但在某些情况下，这一点很重要，例如当开发人员需要针对该程序集中的类型编写代码时，才使用您的包。</span><span class="sxs-lookup"><span data-stu-id="00526-121">But in some cases, it's important, such as when the developer needs to code against types in that assembly in order to use your package.</span></span> <span data-ttu-id="00526-122">新 `frameworkAssemblies` 元素（metadata 元素的子元素）允许您指定一组 `frameworkAssembly` 指向 GAC 中的框架程序集的元素。</span><span class="sxs-lookup"><span data-stu-id="00526-122">The new `frameworkAssemblies` element, a child element of the metadata element, allows you to specify a set of `frameworkAssembly` elements pointing to a Framework assembly in the GAC.</span></span> <span data-ttu-id="00526-123">请注意框架程序集的重点。</span><span class="sxs-lookup"><span data-stu-id="00526-123">Note the emphasis on Framework assembly.</span></span>
<span data-ttu-id="00526-124">这些程序集不包含在包中，因为它们被假定为在每台计算机上作为 .NET Framework 的一部分。</span><span class="sxs-lookup"><span data-stu-id="00526-124">These assemblies are not included in your package as they are assumed to be on every machine  as part of the .NET Framework.</span></span> <span data-ttu-id="00526-125">下表列出了元素的属性 `frameworkAssembly` 。</span><span class="sxs-lookup"><span data-stu-id="00526-125">The following table lists attributes of the `frameworkAssembly` element.</span></span>


|<span data-ttu-id="00526-126">属性</span><span class="sxs-lookup"><span data-stu-id="00526-126">Attribute</span></span> |<span data-ttu-id="00526-127">描述</span><span class="sxs-lookup"><span data-stu-id="00526-127">Description</span></span>|
|----------------|-----------|
|<span data-ttu-id="00526-128">**assemblyName**</span><span class="sxs-lookup"><span data-stu-id="00526-128">**assemblyName**</span></span>|<span data-ttu-id="00526-129">“必需”。</span><span class="sxs-lookup"><span data-stu-id="00526-129">*Required*.</span></span> <span data-ttu-id="00526-130">程序集的名称，例如 `System.Net` 。</span><span class="sxs-lookup"><span data-stu-id="00526-130">Name of the assembly such as `System.Net`.</span></span>|
|<span data-ttu-id="00526-131">**targetFramework**</span><span class="sxs-lookup"><span data-stu-id="00526-131">**targetFramework**</span></span>|<span data-ttu-id="00526-132">可选。</span><span class="sxs-lookup"><span data-stu-id="00526-132">*Optional*.</span></span> <span data-ttu-id="00526-133">允许指定此框架程序集应用到的框架和配置文件名称 (或别名) ，如 "net40" 或 "sl4"。</span><span class="sxs-lookup"><span data-stu-id="00526-133">Allows specifying a framework and profile name (or alias) that this framework assembly applies to such as "net40" or "sl4".</span></span> <span data-ttu-id="00526-134">使用的格式与 [支持多个目标框架](../create-packages/supporting-multiple-target-frameworks.md)中所述的格式相同。</span><span class="sxs-lookup"><span data-stu-id="00526-134">Uses the same format described in [Supporting Multiple Target Frameworks](../create-packages/supporting-multiple-target-frameworks.md).</span></span>|

```xml
  <frameworkAssemblies>
    <frameworkAssembly assemblyName="System.ComponentModel.DataAnnotations" targetFramework="net40" />
    <frameworkAssembly assemblyName="System.ServiceModel" targetFramework="net40" />
  </frameworkAssemblies>
```

### <a name="nugetexe-now-is-able-to-store-api-key-credentials"></a><span data-ttu-id="00526-135">nuget.exe 现在可以存储 API 密钥凭据</span><span class="sxs-lookup"><span data-stu-id="00526-135">nuget.exe now is able to store API Key credentials</span></span>

<span data-ttu-id="00526-136">使用 nuget.exe 命令行工具时，现在可以使用 SetApiKey 命令来存储 API 密钥。</span><span class="sxs-lookup"><span data-stu-id="00526-136">When using the nuget.exe command line tool, you can now use the SetApiKey command to store your API key.</span></span> <span data-ttu-id="00526-137">这样，每次推送包时都无需指定它。</span><span class="sxs-lookup"><span data-stu-id="00526-137">That way, you won’t need to specify it every time you push a package.</span></span> <span data-ttu-id="00526-138">有关使用 nuget.exe 保存 API 密钥的详细信息，请 [阅读有关发布包的文档](../nuget-org/publish-a-package.md)。</span><span class="sxs-lookup"><span data-stu-id="00526-138">For more details on saving your API key with nuget.exe, [read the documentation on publishing a package](../nuget-org/publish-a-package.md).</span></span>

### <a name="package-explorer"></a><span data-ttu-id="00526-139">包资源管理器</span><span class="sxs-lookup"><span data-stu-id="00526-139">Package Explorer</span></span>
<span data-ttu-id="00526-140">包资源管理器已更新为支持 NuGet 1.2。</span><span class="sxs-lookup"><span data-stu-id="00526-140">Package Explorer has been updated to support NuGet 1.2.</span></span> <span data-ttu-id="00526-141">有关详细信息，请参阅 [包资源管理器发行说明](http://nuget.codeplex.com/wikipage?title=New%20features%20in%20NuGet%20Package%20Explorer%201.0)。</span><span class="sxs-lookup"><span data-stu-id="00526-141">For more information, check out the [Package Explorer release notes](http://nuget.codeplex.com/wikipage?title=New%20features%20in%20NuGet%20Package%20Explorer%201.0).</span></span>

## <a name="other-featuresfixes"></a><span data-ttu-id="00526-142">其他功能/修补程序</span><span class="sxs-lookup"><span data-stu-id="00526-142">Other features/fixes</span></span>

<span data-ttu-id="00526-143">之前的列表是我们实现的许多功能和修复的 bug 中最明显的一项。</span><span class="sxs-lookup"><span data-stu-id="00526-143">The previous list were the most noticeable of the many features we implemented and bugs we fixed.</span></span> <span data-ttu-id="00526-144">毕竟，我们在此版本中实现/修复了 [59 工作项](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=All&type=All&priority=All&release=NuGet%201.2&assignedTo=All&component=All&sortField=Votes&sortDirection=Descending&page=0) 。</span><span class="sxs-lookup"><span data-stu-id="00526-144">All in all, we implemented/fixed [59 work items](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=All&type=All&priority=All&release=NuGet%201.2&assignedTo=All&component=All&sortField=Votes&sortDirection=Descending&page=0) in this release.</span></span>

## <a name="known-issues"></a><span data-ttu-id="00526-145">已知问题</span><span class="sxs-lookup"><span data-stu-id="00526-145">Known Issues</span></span>

* <span data-ttu-id="00526-146">**1.2 包不兼容**：使用最新版本的命令行工具生成的包，nuget.exe ( # A0 1.2) 将不适用于其他版本的 NuGet VS 外接程序 (例如 1.1) 。</span><span class="sxs-lookup"><span data-stu-id="00526-146">**1.2 Package incompatibility**: Packages built with the latest version of the command line tool, nuget.exe (> 1.2) will not work with older versions of the NuGet VS Add-in (such as 1.1).</span></span> <span data-ttu-id="00526-147">如果遇到一条错误消息，指出不兼容的架构，则会遇到此错误。</span><span class="sxs-lookup"><span data-stu-id="00526-147">If you run into an error message stating something about incompatible schema, you are running into this error.</span></span> <span data-ttu-id="00526-148">请将 NuGet 更新到最新版本。</span><span class="sxs-lookup"><span data-stu-id="00526-148">Please update NuGet to the latest version.</span></span>
* <span data-ttu-id="00526-149">**NuGet。服务器不兼容性**：如果你要使用 nuget.exe 服务器项目托管内部 nuget 源，则需要使用最新版本的 nuget 更新该项目。</span><span class="sxs-lookup"><span data-stu-id="00526-149">**NuGet.Server incompatibility**: If you’re hosting an internal NuGet feed using the NuGet.Server project, you’ll need to update that project with the latest version of NuGet.Server.</span></span>
* <span data-ttu-id="00526-150">**签名不匹配错误**：如果在升级过程中遇到与签名不匹配有关的消息，则需要先卸载 NuGet，然后再进行安装。</span><span class="sxs-lookup"><span data-stu-id="00526-150">**Signature Mismatch Error**: If you run into an error during an upgrade with a message about a Signature Mismatch, you need to uninstall NuGet first and then install it.</span></span> <span data-ttu-id="00526-151">这会在我们的 " [已知问题" 页](../release-notes/known-issues.md) 中列出，其中提供了更多详细信息。</span><span class="sxs-lookup"><span data-stu-id="00526-151">This is listed in our [Known Issues page](../release-notes/known-issues.md) which provides more details.</span></span> <span data-ttu-id="00526-152">此问题只会影响那些运行 Visual Studio 2010 SP1 的版本，并且安装的 NuGet 1.0 版本未正确签名。</span><span class="sxs-lookup"><span data-stu-id="00526-152">The issue only affects those running Visual Studio 2010 SP1 and have a version of NuGet 1.0 installed that was incorrectly signed.</span></span> <span data-ttu-id="00526-153">此版本仅在 CodePlex 网站中提供一小段时间，因此，此问题不会影响太多人。</span><span class="sxs-lookup"><span data-stu-id="00526-153">This version was only made available from the CodePlex website for a brief period so this issue shouldn't affect too many people.</span></span>