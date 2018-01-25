---
title: "NuGet 1.5 发行说明 |Microsoft 文档"
author: karann-msft
ms.author: karann-msft
manager: ghogen
ms.date: 11/11/2016
ms.topic: article
ms.prod: nuget
ms.technology: 
description: "包括已知的问题、 bug 修复、 增加的功能，以及 DCRs NuGet 1.5 的发行说明。"
keywords: "NuGet 1.5 发行说明，bug 修复的已知问题，添加了一些功能，DCRs"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 261cfbbd262bad28f142b0c3dff8a541641d9fda
ms.sourcegitcommit: 262d026beeffd4f3b6fc47d780a2f701451663a8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/25/2018
---
# <a name="nuget-15-release-notes"></a><span data-ttu-id="e2b7b-104">NuGet 1.5 的发行说明</span><span class="sxs-lookup"><span data-stu-id="e2b7b-104">NuGet 1.5 Release Notes</span></span>

<span data-ttu-id="e2b7b-105">[NuGet 1.4 的发行说明](../release-notes/nuget-1.4.md) | [NuGet 1.6 发行说明](../release-notes/nuget-1.6.md)</span><span class="sxs-lookup"><span data-stu-id="e2b7b-105">[NuGet 1.4 Release Notes](../release-notes/nuget-1.4.md) | [NuGet 1.6 Release Notes](../release-notes/nuget-1.6.md)</span></span>

<span data-ttu-id="e2b7b-106">NuGet 1.5 已于 2011 年 8 月 30 日发布。</span><span class="sxs-lookup"><span data-stu-id="e2b7b-106">NuGet 1.5 was released on August 30, 2011.</span></span>

## <a name="features"></a><span data-ttu-id="e2b7b-107">功能</span><span class="sxs-lookup"><span data-stu-id="e2b7b-107">Features</span></span>

### <a name="project-templates-with-preinstalled-nuget-packages"></a><span data-ttu-id="e2b7b-108">使用预安装的 NuGet 包的项目模板</span><span class="sxs-lookup"><span data-stu-id="e2b7b-108">Project Templates with Preinstalled NuGet Packages</span></span>
<span data-ttu-id="e2b7b-109">创建新的 ASP.NET MVC 3 项目模板时，jQuery 脚本库项目中包含实际放在此处通过安装 NuGet 包。</span><span class="sxs-lookup"><span data-stu-id="e2b7b-109">When creating a new ASP.NET MVC 3 project template, the jQuery script libraries included in the project are actually placed there by installing NuGet packages.</span></span>

<span data-ttu-id="e2b7b-110">ASP.NET MVC 3 项目模板包含一组调用项目模板时，获取安装的 NuGet 包。</span><span class="sxs-lookup"><span data-stu-id="e2b7b-110">The ASP.NET MVC 3 project template includes a set of NuGet packages that get installed when the project template is invoked.</span></span> <span data-ttu-id="e2b7b-111">将 NuGet 程序包的项目模板包括此功能现在是一项功能的 NuGet 的_任何_项目模板现在可以充分利用。</span><span class="sxs-lookup"><span data-stu-id="e2b7b-111">This ability to include NuGet packages with a project template is now a feature of NuGet that _any_ project template can now take advantage of.</span></span>

<span data-ttu-id="e2b7b-112">有关此功能的详细信息，请参阅此[功能的开发人员的博客文章](http://blogs.msdn.com/b/marcinon/archive/2011/07/08/project-templates-and-preinstalled-nuget-packages.aspx)。</span><span class="sxs-lookup"><span data-stu-id="e2b7b-112">For more details about this feature, read this [blog post by the developer of the feature](http://blogs.msdn.com/b/marcinon/archive/2011/07/08/project-templates-and-preinstalled-nuget-packages.aspx).</span></span>

### <a name="explicit-assembly-references"></a><span data-ttu-id="e2b7b-113">显式程序集引用</span><span class="sxs-lookup"><span data-stu-id="e2b7b-113">Explicit Assembly References</span></span>

<span data-ttu-id="e2b7b-114">添加一个新`<references />`用于显式指定的程序集内的元素应引用包。</span><span class="sxs-lookup"><span data-stu-id="e2b7b-114">Added a new `<references />` element used to explicitly specify which assemblies within the the package should be referenced.</span></span>

<span data-ttu-id="e2b7b-115">例如，如果你将以下代码添加：</span><span class="sxs-lookup"><span data-stu-id="e2b7b-115">For example, if you add the following:</span></span>

```xml
<references>
    <reference file="xunit.dll" />
    <reference file="xunit.extensions.dll" />
</references>
```

<span data-ttu-id="e2b7b-116">然后仅`xunit.dll`和`xunit.extensions.dll`将引用从相应[framework/配置文件子文件夹](../schema/nuspec.md#explicit-assembly-references)的`lib`即使文件夹中没有其他程序集的文件夹。</span><span class="sxs-lookup"><span data-stu-id="e2b7b-116">Then only the `xunit.dll` and `xunit.extensions.dll` will be referenced from the appropriate [framework/profile subfolder](../schema/nuspec.md#explicit-assembly-references) of the `lib` folder even if there are other assemblies in the folder.</span></span>

<span data-ttu-id="e2b7b-117">如果省略此元素，则适用常用的行为，即引用中的每个程序集`lib`文件夹。</span><span class="sxs-lookup"><span data-stu-id="e2b7b-117">If this element is omitted, then the usual behavior applies, which is to reference every assembly in the `lib` folder.</span></span>

<span data-ttu-id="e2b7b-118">__此功能的用途是什么？__</span><span class="sxs-lookup"><span data-stu-id="e2b7b-118">__What is this feature used for?__</span></span>

<span data-ttu-id="e2b7b-119">此功能支持设计时只有程序集。</span><span class="sxs-lookup"><span data-stu-id="e2b7b-119">This feature supports design-time only assemblies.</span></span> <span data-ttu-id="e2b7b-120">例如，当使用代码协定，则需要进行补充，以便 Visual Studio 可以找到它们，但协定程序集不应实际引用由项目并不会复制到运行时程序集旁是协定程序集`bin`文件夹。</span><span class="sxs-lookup"><span data-stu-id="e2b7b-120">For example, when using Code Contracts, the contract assemblies need to be next to the runtime assemblies that they augment so that Visual Studio can find them, but the contract assemblies should not actually be referenced by the project and should not be copied into the `bin` folder.</span></span>

<span data-ttu-id="e2b7b-121">同样，该功能可用来为单元测试框架，例如 XUnit 需要旁边运行时程序集，但从项目引用中排除其工具程序集。</span><span class="sxs-lookup"><span data-stu-id="e2b7b-121">Likewise, the feature can be used to for unit test frameworks such as XUnit which need its tools assemblies to be located next to the runtime assemblies, but excluded from project references.</span></span>

### <a name="added-ability-to-exclude-files-in-the-nuspec"></a><span data-ttu-id="e2b7b-122">添加以排除.nuspec 中的文件的能力</span><span class="sxs-lookup"><span data-stu-id="e2b7b-122">Added ability to exclude files in the .nuspec</span></span>
<span data-ttu-id="e2b7b-123">`<file>`中的元素`.nuspec`文件可以用于包括特定文件或一组使用通配符的文件。</span><span class="sxs-lookup"><span data-stu-id="e2b7b-123">The `<file>` element within a `.nuspec` file can be used to include a specific file or a set of files using a wildcard.</span></span> <span data-ttu-id="e2b7b-124">在使用通配符时，没有方法来排除包含的文件的特定子集。</span><span class="sxs-lookup"><span data-stu-id="e2b7b-124">When using a wildcard, there's no way to exclude a specific subset of the included files.</span></span> <span data-ttu-id="e2b7b-125">例如，假设你想在除特定文件夹内的所有文本文件。</span><span class="sxs-lookup"><span data-stu-id="e2b7b-125">For example, suppose you want all text files within a folder except a specific one.</span></span>

```xml
<files>
    <file src="*.txt" target="content\docs" exclude="admin.txt" />
</files>
```

<span data-ttu-id="e2b7b-126">使用分号指定多个文件。</span><span class="sxs-lookup"><span data-stu-id="e2b7b-126">Use semicolons to specify multiple files.</span></span>

```xml
<files>
    <file src="*.txt" target="content\docs" exclude="admin.txt;log.txt" />
</files>
```

<span data-ttu-id="e2b7b-127">或使用通配符来排除一套例如所有备份文件的文件</span><span class="sxs-lookup"><span data-stu-id="e2b7b-127">Or use a wild card to exclude a set of files such as all backup files</span></span>

```xml
<files>
    <file src="tools\*.*" target="tools" exclude="*.bak" />
</files>
```

### <a name="removing-packages-using-the-dialog-prompts-to-remove-dependencies"></a><span data-ttu-id="e2b7b-128">删除包使用对话框提示以删除依赖关系</span><span class="sxs-lookup"><span data-stu-id="e2b7b-128">Removing packages using the dialog prompts to remove dependencies</span></span>
<span data-ttu-id="e2b7b-129">卸载程序包依赖项而 NuGet 提示时，允许包的依赖关系和程序包一起删除。</span><span class="sxs-lookup"><span data-stu-id="e2b7b-129">When uninstalling a package with dependencies, NuGet prompts, allowing the removal of a package's dependencies along with the package.</span></span>

![删除依赖的包](./media/remove-dependent-packages.png)


### <a name="get-package-command-improvement"></a><span data-ttu-id="e2b7b-131">`Get-Package`命令改善</span><span class="sxs-lookup"><span data-stu-id="e2b7b-131">`Get-Package` command improvement</span></span>
<span data-ttu-id="e2b7b-132">`Get-Package`命令现在支持`-ProjectName`参数。</span><span class="sxs-lookup"><span data-stu-id="e2b7b-132">The `Get-Package` command now supports a `-ProjectName` parameter.</span></span> <span data-ttu-id="e2b7b-133">因此该命令</span><span class="sxs-lookup"><span data-stu-id="e2b7b-133">So the command</span></span>

    Get-Package –ProjectName A

<span data-ttu-id="e2b7b-134">将列出项目 A.中安装的所有包</span><span class="sxs-lookup"><span data-stu-id="e2b7b-134">will list all packages installed in project A.</span></span>

### <a name="support-for-proxies-that-require-authentication"></a><span data-ttu-id="e2b7b-135">代理需要身份验证的支持</span><span class="sxs-lookup"><span data-stu-id="e2b7b-135">Support for Proxies that require authentication</span></span>
<span data-ttu-id="e2b7b-136">在要求身份验证的代理后面使用 NuGet，NuGet 将现在将提示输入代理服务器凭据。</span><span class="sxs-lookup"><span data-stu-id="e2b7b-136">When using NuGet behind a proxy that requires authentication, NuGet will now prompt for proxy credentials.</span></span> <span data-ttu-id="e2b7b-137">输入凭据允许连接到远程存储库的 NuGet。</span><span class="sxs-lookup"><span data-stu-id="e2b7b-137">Entering credentials allows NuGet to connect to the remote repository.</span></span>

### <a name="support-for-repositories-that-require-authentication"></a><span data-ttu-id="e2b7b-138">对要求进行身份验证的存储库的支持</span><span class="sxs-lookup"><span data-stu-id="e2b7b-138">Support for Repositories that require authentication</span></span>
<span data-ttu-id="e2b7b-139">NuGet 现在支持连接到[专用的存储库](../hosting-packages/local-feeds.md)需要基本或 NTLM 身份验证。</span><span class="sxs-lookup"><span data-stu-id="e2b7b-139">NuGet now supports connecting to [private repositories](../hosting-packages/local-feeds.md) that require basic or NTLM authentication.</span></span>

<span data-ttu-id="e2b7b-140">未来版本中，将添加为摘要式身份验证的支持。</span><span class="sxs-lookup"><span data-stu-id="e2b7b-140">Support for Digest authentication will be added in a future release.</span></span>

### <a name="performance-improvements-to-the-nugetorg-repository"></a><span data-ttu-id="e2b7b-141">到 nuget.org 存储库的性能改进</span><span class="sxs-lookup"><span data-stu-id="e2b7b-141">Performance improvements to the nuget.org repository</span></span>
<span data-ttu-id="e2b7b-142">我们已进行了 nuget.org 库，以使包列出和更快地搜索到的一些性能改进。</span><span class="sxs-lookup"><span data-stu-id="e2b7b-142">We've made several performance improvements to the nuget.org gallery to make package listing and searching faster.</span></span>

### <a name="solution-dialog-project-filtering"></a><span data-ttu-id="e2b7b-143">解决方案对话框项目筛选</span><span class="sxs-lookup"><span data-stu-id="e2b7b-143">Solution dialog project filtering</span></span>
<span data-ttu-id="e2b7b-144">在解决方案级别对话框中，当提示输入要安装哪些项目时，我们只会显示所选包与兼容的项目。</span><span class="sxs-lookup"><span data-stu-id="e2b7b-144">In the Solution-level dialog, when prompting for what projects to install, we only show projects that are compatible with the selected package.</span></span>

### <a name="package-release-notes"></a><span data-ttu-id="e2b7b-145">包发行说明</span><span class="sxs-lookup"><span data-stu-id="e2b7b-145">Package Release Notes</span></span>
<span data-ttu-id="e2b7b-146">NuGet 包现在包括对发行说明支持。</span><span class="sxs-lookup"><span data-stu-id="e2b7b-146">NuGet packages now include support for release notes.</span></span> <span data-ttu-id="e2b7b-147">发行说明邮件查看时仅显示_更新_对于包，因此它没有意义将它们添加到你的第一个发布。</span><span class="sxs-lookup"><span data-stu-id="e2b7b-147">The release notes only show up when viewing _Updates_ for a package, so it doesn't make sense to add them to your first release.</span></span>

![在更新选项卡内的发行说明](./media/manage-nuget-packages-release-notes.png)

<span data-ttu-id="e2b7b-149">若要添加到包的发行说明，使用新`<releaseNotes />`NuSpec 文件中的元数据元素。</span><span class="sxs-lookup"><span data-stu-id="e2b7b-149">To add release notes to a package, use the new `<releaseNotes />` metadata element in your NuSpec file.</span></span>

### <a name="nuspec-ltfiles-gt-improvement"></a><span data-ttu-id="e2b7b-150">.nuspec 和 ltfiles /&gt;改善</span><span class="sxs-lookup"><span data-stu-id="e2b7b-150">.nuspec &ltfiles /&gt; improvement</span></span>
<span data-ttu-id="e2b7b-151">`.nuspec`文件现在允许空`<files />`元素，它告知 nuget.exe 不要包含在包中的任何文件。</span><span class="sxs-lookup"><span data-stu-id="e2b7b-151">The `.nuspec` file now allows empty `<files />` element, which tells nuget.exe not to include any file in the package.</span></span>

## <a name="bug-fixes"></a><span data-ttu-id="e2b7b-152">Bug 修复</span><span class="sxs-lookup"><span data-stu-id="e2b7b-152">Bug Fixes</span></span>
<span data-ttu-id="e2b7b-153">NuGet 1.5 具有总共 107 工作固定的项。</span><span class="sxs-lookup"><span data-stu-id="e2b7b-153">NuGet 1.5 had a total of 107 work items fixed.</span></span> <span data-ttu-id="e2b7b-154">103 的那些已标记为 bug。</span><span class="sxs-lookup"><span data-stu-id="e2b7b-154">103 of those were marked as bugs.</span></span>

<span data-ttu-id="e2b7b-155">有关工作的完整列表项固定 NuGet 1.5 中请视图[对于此版本的 NuGet 问题跟踪程序](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=All&type=All&priority=All&release=NuGet%201.5&assignedTo=All&component=All&sortField=Summary&sortDirection=Descending&page=0)。</span><span class="sxs-lookup"><span data-stu-id="e2b7b-155">For a full list of work items fixed in NuGet 1.5, please view the [NuGet Issue Tracker for this release](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=All&type=All&priority=All&release=NuGet%201.5&assignedTo=All&component=All&sortField=Summary&sortDirection=Descending&page=0).</span></span>

## <a name="bug-fixes-worth-noting"></a><span data-ttu-id="e2b7b-156">值得注意的 bug 修复：</span><span class="sxs-lookup"><span data-stu-id="e2b7b-156">Bug fixes worth noting:</span></span>

* <span data-ttu-id="e2b7b-157">[问题 1273年](http://nuget.codeplex.com/workitem/1273)： 进行`packages.config`友好按字母顺序排序包并删除多余的空格的多个版本控制。</span><span class="sxs-lookup"><span data-stu-id="e2b7b-157">[Issue 1273](http://nuget.codeplex.com/workitem/1273): Made `packages.config` more version control friendly by sorting packages alphabetically and removing extra whitespace.</span></span>
* <span data-ttu-id="e2b7b-158">[问题 844](http://nuget.codeplex.com/workitem/844)： 现在规范化版本号，以便`Install-Package 1.0`适用于版本的包`1.0.0`。</span><span class="sxs-lookup"><span data-stu-id="e2b7b-158">[Issue 844](http://nuget.codeplex.com/workitem/844): Version numbers are now normalized so that `Install-Package 1.0` works on a package with the version `1.0.0`.</span></span>
* <span data-ttu-id="e2b7b-159">[问题 1060年](http://nuget.codeplex.com/workitem/1060)： 创建使用 nuget.exe，包时`-Version`标志替代`<version />`元素。</span><span class="sxs-lookup"><span data-stu-id="e2b7b-159">[Issue 1060](http://nuget.codeplex.com/workitem/1060): When creating a package using nuget.exe, the `-Version` flag overrides the `<version />` element.</span></span>
