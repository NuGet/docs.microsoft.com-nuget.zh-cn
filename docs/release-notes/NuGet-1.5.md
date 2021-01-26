---
title: NuGet 1.5 发行说明
description: NuGet 1.5 的发行说明，包括已知问题、bug 修复、新增功能和 Dcr。
author: JonDouglas
ms.author: jodou
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: c9946f3d8cf545ec14f842c40105743c231b4b72
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/26/2021
ms.locfileid: "98777087"
---
# <a name="nuget-15-release-notes"></a><span data-ttu-id="4642a-103">NuGet 1.5 发行说明</span><span class="sxs-lookup"><span data-stu-id="4642a-103">NuGet 1.5 Release Notes</span></span>

<span data-ttu-id="4642a-104">[NuGet 1.4 发行说明](../release-notes/nuget-1.4.md)  | [NuGet 1.6 发行说明](../release-notes/nuget-1.6.md)</span><span class="sxs-lookup"><span data-stu-id="4642a-104">[NuGet 1.4 Release Notes](../release-notes/nuget-1.4.md) | [NuGet 1.6 Release Notes](../release-notes/nuget-1.6.md)</span></span>

<span data-ttu-id="4642a-105">NuGet 1.5 于2011年8月30日发布。</span><span class="sxs-lookup"><span data-stu-id="4642a-105">NuGet 1.5 was released on August 30, 2011.</span></span>

## <a name="features"></a><span data-ttu-id="4642a-106">功能</span><span class="sxs-lookup"><span data-stu-id="4642a-106">Features</span></span>

### <a name="project-templates-with-preinstalled-nuget-packages"></a><span data-ttu-id="4642a-107">预安装了 NuGet 包的项目模板</span><span class="sxs-lookup"><span data-stu-id="4642a-107">Project Templates with Preinstalled NuGet Packages</span></span>
<span data-ttu-id="4642a-108">创建新的 ASP.NET MVC 3 项目模板时，项目中包含的 jQuery 脚本库实际上是通过安装 NuGet 包放置在那里。</span><span class="sxs-lookup"><span data-stu-id="4642a-108">When creating a new ASP.NET MVC 3 project template, the jQuery script libraries included in the project are actually placed there by installing NuGet packages.</span></span>

<span data-ttu-id="4642a-109">ASP.NET MVC 3 项目模板包含一组在调用项目模板时安装的 NuGet 包。</span><span class="sxs-lookup"><span data-stu-id="4642a-109">The ASP.NET MVC 3 project template includes a set of NuGet packages that get installed when the project template is invoked.</span></span> <span data-ttu-id="4642a-110">此功能能够将 NuGet 包包含到项目模板中，它现在是 NuGet 的一项功能，现在 _任何_ 项目模板都可以利用。</span><span class="sxs-lookup"><span data-stu-id="4642a-110">This ability to include NuGet packages with a project template is now a feature of NuGet that _any_ project template can now take advantage of.</span></span>

<span data-ttu-id="4642a-111">有关此功能的更多详细信息，请阅读此博客文章，了解该 [功能的开发人员](https://blogs.msdn.com/b/marcinon/archive/2011/07/08/project-templates-and-preinstalled-nuget-packages.aspx)。</span><span class="sxs-lookup"><span data-stu-id="4642a-111">For more details about this feature, read this [blog post by the developer of the feature](https://blogs.msdn.com/b/marcinon/archive/2011/07/08/project-templates-and-preinstalled-nuget-packages.aspx).</span></span>

### <a name="explicit-assembly-references"></a><span data-ttu-id="4642a-112">显式程序集引用</span><span class="sxs-lookup"><span data-stu-id="4642a-112">Explicit Assembly References</span></span>

<span data-ttu-id="4642a-113">添加了一个新 `<references />` 元素，用于显式指定应引用包中的程序集。</span><span class="sxs-lookup"><span data-stu-id="4642a-113">Added a new `<references />` element used to explicitly specify which assemblies within the the package should be referenced.</span></span>

<span data-ttu-id="4642a-114">例如，如果添加以下内容：</span><span class="sxs-lookup"><span data-stu-id="4642a-114">For example, if you add the following:</span></span>

```xml
<references>
    <reference file="xunit.dll" />
    <reference file="xunit.extensions.dll" />
</references>
```

<span data-ttu-id="4642a-115">然后 `xunit.dll` ，将仅 `xunit.extensions.dll` 从文件夹的相应 [框架/配置文件子](../reference/nuspec.md#explicit-assembly-references) 文件夹中引用和， `lib` 即使该文件夹中存在其他程序集。</span><span class="sxs-lookup"><span data-stu-id="4642a-115">Then only the `xunit.dll` and `xunit.extensions.dll` will be referenced from the appropriate [framework/profile subfolder](../reference/nuspec.md#explicit-assembly-references) of the `lib` folder even if there are other assemblies in the folder.</span></span>

<span data-ttu-id="4642a-116">如果省略此元素，则会应用常用行为，即引用文件夹中的每个程序集 `lib` 。</span><span class="sxs-lookup"><span data-stu-id="4642a-116">If this element is omitted, then the usual behavior applies, which is to reference every assembly in the `lib` folder.</span></span>

<span data-ttu-id="4642a-117">__此功能的用途是什么？__</span><span class="sxs-lookup"><span data-stu-id="4642a-117">__What is this feature used for?__</span></span>

<span data-ttu-id="4642a-118">此功能支持仅设计时程序集。</span><span class="sxs-lookup"><span data-stu-id="4642a-118">This feature supports design-time only assemblies.</span></span> <span data-ttu-id="4642a-119">例如，使用代码协定时，协定程序集需要位于它们增加的运行时程序集旁边，以便 Visual Studio 可以找到它们，但是协定程序集实际上不应被项目引用，因此不应复制到 `bin` 文件夹中。</span><span class="sxs-lookup"><span data-stu-id="4642a-119">For example, when using Code Contracts, the contract assemblies need to be next to the runtime assemblies that they augment so that Visual Studio can find them, but the contract assemblies should not actually be referenced by the project and should not be copied into the `bin` folder.</span></span>

<span data-ttu-id="4642a-120">同样，此功能可用于单元测试框架（如 XUnit），这需要将其工具程序集放在运行时程序集旁边，但从项目引用中排除。</span><span class="sxs-lookup"><span data-stu-id="4642a-120">Likewise, the feature can be used to for unit test frameworks such as XUnit which need its tools assemblies to be located next to the runtime assemblies, but excluded from project references.</span></span>

### <a name="added-ability-to-exclude-files-in-the-nuspec"></a><span data-ttu-id="4642a-121">添加了排除 nuspec 中的文件的功能</span><span class="sxs-lookup"><span data-stu-id="4642a-121">Added ability to exclude files in the .nuspec</span></span>
<span data-ttu-id="4642a-122">`<file>`文件中的元素 `.nuspec` 可用于包含特定文件或使用通配符的一组文件。</span><span class="sxs-lookup"><span data-stu-id="4642a-122">The `<file>` element within a `.nuspec` file can be used to include a specific file or a set of files using a wildcard.</span></span> <span data-ttu-id="4642a-123">使用通配符时，无法排除包含的文件的特定子集。</span><span class="sxs-lookup"><span data-stu-id="4642a-123">When using a wildcard, there's no way to exclude a specific subset of the included files.</span></span> <span data-ttu-id="4642a-124">例如，假设您希望文件夹中的所有文本文件除外。</span><span class="sxs-lookup"><span data-stu-id="4642a-124">For example, suppose you want all text files within a folder except a specific one.</span></span>

```xml
<files>
    <file src="*.txt" target="content\docs" exclude="admin.txt" />
</files>
```

<span data-ttu-id="4642a-125">使用分号指定多个文件。</span><span class="sxs-lookup"><span data-stu-id="4642a-125">Use semicolons to specify multiple files.</span></span>

```xml
<files>
    <file src="*.txt" target="content\docs" exclude="admin.txt;log.txt" />
</files>
```

<span data-ttu-id="4642a-126">或使用通配符排除一组文件，如所有备份文件</span><span class="sxs-lookup"><span data-stu-id="4642a-126">Or use a wild card to exclude a set of files such as all backup files</span></span>

```xml
<files>
    <file src="tools\*.*" target="tools" exclude="*.bak" />
</files>
```

### <a name="removing-packages-using-the-dialog-prompts-to-remove-dependencies"></a><span data-ttu-id="4642a-127">使用对话框删除包会提示删除依赖项</span><span class="sxs-lookup"><span data-stu-id="4642a-127">Removing packages using the dialog prompts to remove dependencies</span></span>
<span data-ttu-id="4642a-128">卸载具有依赖项的包时，NuGet 会提示，允许删除包的依赖项和包。</span><span class="sxs-lookup"><span data-stu-id="4642a-128">When uninstalling a package with dependencies, NuGet prompts, allowing the removal of a package's dependencies along with the package.</span></span>

![删除依赖包](./media/remove-dependent-packages.png)


### <a name="get-package-command-improvement"></a><span data-ttu-id="4642a-130">`Get-Package` 命令改进</span><span class="sxs-lookup"><span data-stu-id="4642a-130">`Get-Package` command improvement</span></span>
<span data-ttu-id="4642a-131">`Get-Package`命令现在支持 `-ProjectName` 参数。</span><span class="sxs-lookup"><span data-stu-id="4642a-131">The `Get-Package` command now supports a `-ProjectName` parameter.</span></span> <span data-ttu-id="4642a-132">因此命令</span><span class="sxs-lookup"><span data-stu-id="4642a-132">So the command</span></span>

```
Get-Package –ProjectName A
```

<span data-ttu-id="4642a-133">将列出在项目 A 中安装的所有包。</span><span class="sxs-lookup"><span data-stu-id="4642a-133">will list all packages installed in project A.</span></span>

### <a name="support-for-proxies-that-require-authentication"></a><span data-ttu-id="4642a-134">支持需要身份验证的代理</span><span class="sxs-lookup"><span data-stu-id="4642a-134">Support for Proxies that require authentication</span></span>
<span data-ttu-id="4642a-135">使用需要身份验证的代理后面的 NuGet 时，NuGet 现在会提示输入代理凭据。</span><span class="sxs-lookup"><span data-stu-id="4642a-135">When using NuGet behind a proxy that requires authentication, NuGet will now prompt for proxy credentials.</span></span> <span data-ttu-id="4642a-136">输入凭据后，NuGet 即可连接到远程存储库。</span><span class="sxs-lookup"><span data-stu-id="4642a-136">Entering credentials allows NuGet to connect to the remote repository.</span></span>

### <a name="support-for-repositories-that-require-authentication"></a><span data-ttu-id="4642a-137">支持需要身份验证的存储库</span><span class="sxs-lookup"><span data-stu-id="4642a-137">Support for Repositories that require authentication</span></span>
<span data-ttu-id="4642a-138">NuGet 现在支持连接到需要基本或 NTLM 身份验证的 [专用存储库](../hosting-packages/local-feeds.md) 。</span><span class="sxs-lookup"><span data-stu-id="4642a-138">NuGet now supports connecting to [private repositories](../hosting-packages/local-feeds.md) that require basic or NTLM authentication.</span></span>

<span data-ttu-id="4642a-139">未来版本中将添加对摘要式身份验证的支持。</span><span class="sxs-lookup"><span data-stu-id="4642a-139">Support for Digest authentication will be added in a future release.</span></span>

### <a name="performance-improvements-to-the-nugetorg-repository"></a><span data-ttu-id="4642a-140">Nuget.org 存储库的性能改进</span><span class="sxs-lookup"><span data-stu-id="4642a-140">Performance improvements to the nuget.org repository</span></span>
<span data-ttu-id="4642a-141">我们对 nuget.org 库进行了几项性能改进，使包列表和搜索速度更快。</span><span class="sxs-lookup"><span data-stu-id="4642a-141">We've made several performance improvements to the nuget.org gallery to make package listing and searching faster.</span></span>

### <a name="solution-dialog-project-filtering"></a><span data-ttu-id="4642a-142">解决方案对话框项目筛选</span><span class="sxs-lookup"><span data-stu-id="4642a-142">Solution dialog project filtering</span></span>
<span data-ttu-id="4642a-143">在解决方案级对话框中，当提示您要安装的项目时，我们只显示与所选包兼容的项目。</span><span class="sxs-lookup"><span data-stu-id="4642a-143">In the Solution-level dialog, when prompting for what projects to install, we only show projects that are compatible with the selected package.</span></span>

### <a name="package-release-notes"></a><span data-ttu-id="4642a-144">包发行说明</span><span class="sxs-lookup"><span data-stu-id="4642a-144">Package Release Notes</span></span>
<span data-ttu-id="4642a-145">NuGet 包现在包括对发行说明的支持。</span><span class="sxs-lookup"><span data-stu-id="4642a-145">NuGet packages now include support for release notes.</span></span> <span data-ttu-id="4642a-146">仅当查看包的 _更新_ 时才会显示发行说明，因此，将其添加到第一个版本中并没有什么意义。</span><span class="sxs-lookup"><span data-stu-id="4642a-146">The release notes only show up when viewing _Updates_ for a package, so it doesn't make sense to add them to your first release.</span></span>

!["更新" 选项卡中的发行说明](./media/manage-nuget-packages-release-notes.png)

<span data-ttu-id="4642a-148">若要向包添加发行说明，请 `<releaseNotes />` 在 NuSpec 文件中使用新的元数据元素。</span><span class="sxs-lookup"><span data-stu-id="4642a-148">To add release notes to a package, use the new `<releaseNotes />` metadata element in your NuSpec file.</span></span>

### <a name="nuspec-ltfiles-gt-improvement"></a><span data-ttu-id="4642a-149">. nuspec &ltfiles/ &gt; 改进</span><span class="sxs-lookup"><span data-stu-id="4642a-149">.nuspec &ltfiles /&gt; improvement</span></span>
<span data-ttu-id="4642a-150">`.nuspec`文件现在允许空 `<files />` 元素，这会告诉 nuget.exe 不包含包中的任何文件。</span><span class="sxs-lookup"><span data-stu-id="4642a-150">The `.nuspec` file now allows empty `<files />` element, which tells nuget.exe not to include any file in the package.</span></span>

## <a name="bug-fixes"></a><span data-ttu-id="4642a-151">Bug 修复</span><span class="sxs-lookup"><span data-stu-id="4642a-151">Bug Fixes</span></span>
<span data-ttu-id="4642a-152">NuGet 1.5 总共修复了107个工作项。</span><span class="sxs-lookup"><span data-stu-id="4642a-152">NuGet 1.5 had a total of 107 work items fixed.</span></span> <span data-ttu-id="4642a-153">103标记为 bug。</span><span class="sxs-lookup"><span data-stu-id="4642a-153">103 of those were marked as bugs.</span></span>

<span data-ttu-id="4642a-154">有关 NuGet 1.5 中已修复的工作项的完整列表，请查看 [此版本的 NuGet 问题跟踪程序](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=All&type=All&priority=All&release=NuGet%201.5&assignedTo=All&component=All&sortField=Summary&sortDirection=Descending&page=0)。</span><span class="sxs-lookup"><span data-stu-id="4642a-154">For a full list of work items fixed in NuGet 1.5, please view the [NuGet Issue Tracker for this release](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=All&type=All&priority=All&release=NuGet%201.5&assignedTo=All&component=All&sortField=Summary&sortDirection=Descending&page=0).</span></span>

## <a name="bug-fixes-worth-noting"></a><span data-ttu-id="4642a-155">需要注意的 Bug 修复：</span><span class="sxs-lookup"><span data-stu-id="4642a-155">Bug fixes worth noting:</span></span>

* <span data-ttu-id="4642a-156">[问题 1273](http://nuget.codeplex.com/workitem/1273)： `packages.config` 通过按字母顺序对包排序并删除额外的空白，使版本控制更友好。</span><span class="sxs-lookup"><span data-stu-id="4642a-156">[Issue 1273](http://nuget.codeplex.com/workitem/1273): Made `packages.config` more version control friendly by sorting packages alphabetically and removing extra whitespace.</span></span>
* <span data-ttu-id="4642a-157">[问题 844](http://nuget.codeplex.com/workitem/844)：版本号现已规范化，因此适用于版本为的 `Install-Package 1.0` 包 `1.0.0` 。</span><span class="sxs-lookup"><span data-stu-id="4642a-157">[Issue 844](http://nuget.codeplex.com/workitem/844): Version numbers are now normalized so that `Install-Package 1.0` works on a package with the version `1.0.0`.</span></span>
* <span data-ttu-id="4642a-158">[问题 1060](http://nuget.codeplex.com/workitem/1060)：使用 nuget.exe 创建包时，标志将 `-Version` 重写 `<version />` 元素。</span><span class="sxs-lookup"><span data-stu-id="4642a-158">[Issue 1060](http://nuget.codeplex.com/workitem/1060): When creating a package using nuget.exe, the `-Version` flag overrides the `<version />` element.</span></span>
