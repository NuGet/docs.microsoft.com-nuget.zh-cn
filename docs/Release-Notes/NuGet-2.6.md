---
title: "NuGet 2.6 发行说明 |Microsoft 文档"
author: karann-msft
ms.author: karann-msft
manager: ghogen
ms.date: 11/11/2016
ms.topic: article
ms.prod: nuget
ms.technology: 
ms.assetid: d99bbf29-2b9a-4dc5-a823-5eb4f9e30f7f
description: "包括已知的问题、 bug 修复、 增加的功能，以及 DCRs NuGet 2.6 的发行说明。"
keywords: "NuGet 2.6 发行说明，bug 修复的已知问题，添加了一些功能，DCRs"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: f93e34326aa9ab3d6bd5d1756126e6bfa24fd82e
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/14/2017
---
# <a name="nuget-26-release-notes"></a><span data-ttu-id="521e7-104">NuGet 2.6 发行说明</span><span class="sxs-lookup"><span data-stu-id="521e7-104">NuGet 2.6 Release Notes</span></span>

<span data-ttu-id="521e7-105">[NuGet 2.5 发行说明](../release-notes/nuget-2.5.md) | [NuGet 2.6.1 for WebMatrix 发行说明](../release-notes/nuget-2.6.1-for-webmatrix.md)</span><span class="sxs-lookup"><span data-stu-id="521e7-105">[NuGet 2.5 Release Notes](../release-notes/nuget-2.5.md) | [NuGet 2.6.1 for WebMatrix Release Notes](../release-notes/nuget-2.6.1-for-webmatrix.md)</span></span>

<span data-ttu-id="521e7-106">NuGet 2.6 已于 2013 年 6 月 26 日发布。</span><span class="sxs-lookup"><span data-stu-id="521e7-106">NuGet 2.6 was released on June 26, 2013.</span></span>

## <a name="notable-features-in-the-release"></a><span data-ttu-id="521e7-107">发行版中的值得注意的功能</span><span class="sxs-lookup"><span data-stu-id="521e7-107">Notable features in the release</span></span>

### <a name="support-for-visual-studio-2013"></a><span data-ttu-id="521e7-108">对 Visual Studio 2013 的支持</span><span class="sxs-lookup"><span data-stu-id="521e7-108">Support for Visual Studio 2013</span></span>

<span data-ttu-id="521e7-109">NuGet 2.6 是提供对 Visual Studio 2013 的支持的第一个版本。</span><span class="sxs-lookup"><span data-stu-id="521e7-109">NuGet 2.6 is the first release that provides support for Visual Studio 2013.</span></span> <span data-ttu-id="521e7-110">如 Visual Studio 2012，NuGet 包管理器扩展包含在 Visual Studio 的每个版本。</span><span class="sxs-lookup"><span data-stu-id="521e7-110">And like Visual Studio 2012, the NuGet Package Manager extension is included in every edition of Visual Studio.</span></span>

<span data-ttu-id="521e7-111">为了提供对 Visual Studio 2013，同时仍支持 Visual Studio 2010 和 Visual Studio 2012 和保持尽可能小的扩展大小的最佳可能支持，我们将生成一个单独的 Visual Studio 2013 时扩展继续针对 Visual Studio 2010 和 2012年原来的扩展名。</span><span class="sxs-lookup"><span data-stu-id="521e7-111">In order to provide the best possible support for Visual Studio 2013 while still supporting both Visual Studio 2010 and Visual Studio 2012, and keeping the extension sizes as small as possible, we are producing a separate extension for Visual Studio 2013 while the original extension continues to target both Visual Studio 2010 and 2012.</span></span>

<span data-ttu-id="521e7-112">从 NuGet 2.6 开始，我们将发布两个扩展，如下所示：</span><span class="sxs-lookup"><span data-stu-id="521e7-112">Starting with NuGet 2.6, we will publish two extensions as below:</span></span>

1. <span data-ttu-id="521e7-113">[NuGet 包管理器](http://visualstudiogallery.msdn.microsoft.com/27077b70-9dad-4c64-adcf-c7cf6bc9970c/file/37502/30/NuGet.Tools.vsix)（适用于 Visual Studio 2010 和 2012年）</span><span class="sxs-lookup"><span data-stu-id="521e7-113">[NuGet Package Manager](http://visualstudiogallery.msdn.microsoft.com/27077b70-9dad-4c64-adcf-c7cf6bc9970c/file/37502/30/NuGet.Tools.vsix) (applies to Visual Studio 2010 and 2012)</span></span>
2. [<span data-ttu-id="521e7-114">用于 Visual Studio 2013 的 NuGet 程序包管理器</span><span class="sxs-lookup"><span data-stu-id="521e7-114">NuGet Package Manager for Visual Studio 2013</span></span>](http://visualstudiogallery.msdn.microsoft.com/4ec1526c-4a8c-4a84-b702-b21a8f5293ca)

<span data-ttu-id="521e7-115">此拆分， [nuget.org](https://nuget.org)主页的"安装 NuGet"按钮现在你将转到[安装 NuGet](../guides/install-nuget.md)页上，你可以在其中找到有关安装不同的 NuGet 客户端的详细信息。</span><span class="sxs-lookup"><span data-stu-id="521e7-115">With this split, the [nuget.org](https://nuget.org) home page's "Install NuGet" button will now take you to the [installing NuGet](../guides/install-nuget.md) page, where you can find more information about installing the different NuGet clients.</span></span>

<a name="xdt"></a>

### <a name="xdt-webconfig-transformation-support"></a><span data-ttu-id="521e7-116">XDT Web.config 转换支持</span><span class="sxs-lookup"><span data-stu-id="521e7-116">XDT Web.config transformation support</span></span>

<span data-ttu-id="521e7-117">NuGet 客户端的高请求功能之一是支持使用 XDT 转换引擎在 Visual Studio 中使用的功能更强大 XML 转换[生成配置转换](http://msdn.microsoft.com/library/dd465318(v=vs.100).aspx)。</span><span class="sxs-lookup"><span data-stu-id="521e7-117">One of the most highly-requested features for the NuGet client has been to support more powerful XML transformations using the XDT transformation engine which is used in Visual Studio [build configuration transformations](http://msdn.microsoft.com/library/dd465318(v=vs.100).aspx).</span></span>
<span data-ttu-id="521e7-118">2013 年 4 月，我们做 XDT 的 NuGet 支持的两个大公告。</span><span class="sxs-lookup"><span data-stu-id="521e7-118">In April 2013, we made two big announcements regarding NuGet support for XDT.</span></span> <span data-ttu-id="521e7-119">第一种是在 XDT 库自身正在本身[发布为 NuGet 包](https://nuget.org/packages/Microsoft.Web.Xdt)和[打开来源 CodePlex 上](http://xdt.codeplex.com/)。</span><span class="sxs-lookup"><span data-stu-id="521e7-119">The first was that the XDT library itself was being itself [released as a NuGet package](https://nuget.org/packages/Microsoft.Web.Xdt) and [open sourced on CodePlex](http://xdt.codeplex.com/).</span></span> <span data-ttu-id="521e7-120">此步骤启用 XDT 引擎以自由地供其他开放源代码软件，包括 NuGet 客户端。</span><span class="sxs-lookup"><span data-stu-id="521e7-120">This step enabled the XDT engine to be used freely by other open-source software, including the NuGet client.</span></span> <span data-ttu-id="521e7-121">第二个公告时要使用 XDT 引擎支持在 NuGet 客户端中进行转换的计划。</span><span class="sxs-lookup"><span data-stu-id="521e7-121">The second announcement was the plan to support use of the XDT engine for transformations in the NuGet client.</span></span> <span data-ttu-id="521e7-122">NuGet 2.6 包括此集成。</span><span class="sxs-lookup"><span data-stu-id="521e7-122">NuGet 2.6 includes this integration.</span></span>

#### <a name="how-it-works"></a><span data-ttu-id="521e7-123">它是如何工作</span><span class="sxs-lookup"><span data-stu-id="521e7-123">How it works</span></span>

<span data-ttu-id="521e7-124">若要利用的 NuGet 的 XDT 支持，机制查找类似于[当前配置转换功能](../create-packages/source-and-config-file-transformations.md)。</span><span class="sxs-lookup"><span data-stu-id="521e7-124">To take advantage of NuGet’s XDT support, the mechanics look similar to those of the [current config transformation feature](../create-packages/source-and-config-file-transformations.md).</span></span>
<span data-ttu-id="521e7-125">转换文件添加到程序包的内容文件夹。</span><span class="sxs-lookup"><span data-stu-id="521e7-125">Transformation files are added to the package’s content folder.</span></span> <span data-ttu-id="521e7-126">但是，配置转换进行时使用单个文件安装和卸载，XDT 转换将启用对这两个使用以下文件这些进程细化的控制：</span><span class="sxs-lookup"><span data-stu-id="521e7-126">However, while config transformations use a single file for both installation and uninstallation, XDT transformations enable fine-grained control over both of these processes using the following files:</span></span>

- <span data-ttu-id="521e7-127">Web.config.install.xdt</span><span class="sxs-lookup"><span data-stu-id="521e7-127">Web.config.install.xdt</span></span>
- <span data-ttu-id="521e7-128">Web.config.uninstall.xdt</span><span class="sxs-lookup"><span data-stu-id="521e7-128">Web.config.uninstall.xdt</span></span>

<span data-ttu-id="521e7-129">此外，NuGet 使用文件后缀来确定哪些引擎运行进行转换，以便使用现有 web.config.transforms 包将继续工作。</span><span class="sxs-lookup"><span data-stu-id="521e7-129">Additionally, NuGet uses the file suffix to determine which engine to run for transformations, so packages using the existing web.config.transforms will continue to work.</span></span> <span data-ttu-id="521e7-130">XDT 转换还可应用于任何 XML 文件 (而不仅仅是 web.config)，因此你可以利用这对于其他应用程序项目中。</span><span class="sxs-lookup"><span data-stu-id="521e7-130">XDT transformations can also be applied to any XML file (not just web.config), so you can leverage this for other applications in your project.</span></span>

#### <a name="what-you-can-do-with-xdt"></a><span data-ttu-id="521e7-131">你可以使用 XDT 做什么</span><span class="sxs-lookup"><span data-stu-id="521e7-131">What you can do with XDT</span></span>

<span data-ttu-id="521e7-132">XDT 的最大优势之一是其[简单但功能强大的语法](http://msdn.microsoft.com/library/dd465326.aspx)用于操作的结构的 XML dom。</span><span class="sxs-lookup"><span data-stu-id="521e7-132">One of XDT’s greatest strengths is its [simple but powerful syntax](http://msdn.microsoft.com/library/dd465326.aspx) for manipulating the structure of an XML DOM.</span></span> <span data-ttu-id="521e7-133">而不是只需覆盖到另一个结构的一个固定的文档结构，XDT 提供用于匹配中有许多种情况下，从简单的属性名称匹配到完整的 XPath 支持的元素的控件。</span><span class="sxs-lookup"><span data-stu-id="521e7-133">Rather than simply overlaying one fixed document structure onto another structure, XDT provides controls for matching elements in a variety of ways, from simple attribute name matching to full XPath support.</span></span> <span data-ttu-id="521e7-134">这意味着添加、 更新或删除的属性，将新元素放置在特定位置，或替换或删除整个，XDT 一旦找到一个匹配元素或一组的元素，提供用于操作元素，一组丰富的函数元素及其子级。</span><span class="sxs-lookup"><span data-stu-id="521e7-134">Once a matching element or set of elements is found, XDT provides a rich set of functions for manipulating the elements, whether that means adding, updating, or removing attributes, placing a new element at a specific location, or replacing or removing the entire element and its children.</span></span>

### <a name="machine-wide-configuration"></a><span data-ttu-id="521e7-135">计算机范围的配置</span><span class="sxs-lookup"><span data-stu-id="521e7-135">Machine-Wide Configuration</span></span>

<span data-ttu-id="521e7-136">NuGet 的极佳优势之一是它将分解否则为大可执行文件或到一组模块化组件可以独立是集成，并最重要的是保持和已进行版本管理的库。</span><span class="sxs-lookup"><span data-stu-id="521e7-136">One of the great strengths of NuGet is that it breaks down an otherwise large executable or library into a set of modular components which can be integrated, and most importantly maintained and versioned independently.</span></span> <span data-ttu-id="521e7-137">但是，，的一个副作用是，某个产品或产品系列的常规理论基础可能碎片的增多。</span><span class="sxs-lookup"><span data-stu-id="521e7-137">One side effect of this, however, is that the conventional idea of a product or product family becomes potentially more fragmented.</span></span>
<span data-ttu-id="521e7-138">NuGet 的自定义包源功能提供了一种组织包;但是，自定义的包源都不在其自己可发现。</span><span class="sxs-lookup"><span data-stu-id="521e7-138">NuGet’s custom package source feature provides one way of organizing packages; however, custom package sources are not discoverable on their own.</span></span>

<span data-ttu-id="521e7-139">NuGet 2.6 扩展通过搜索 %programdata%/nuget/config 路径下的文件夹层次结构配置 NuGet 的逻辑。产品安装程序可以添加自定义 NuGet 配置文件来注册他们的产品的自定义包源此文件夹下。</span><span class="sxs-lookup"><span data-stu-id="521e7-139">NuGet 2.6 extends the logic for configuring NuGet by searching the folder hierarchy under the path %ProgramData%/NuGet/Config. Product installers can add custom NuGet configuration files under this folder to register a custom package source for their products.</span></span> <span data-ttu-id="521e7-140">此外，文件夹结构的产品、 版本和甚至 SKU 的 IDE 支持语义。</span><span class="sxs-lookup"><span data-stu-id="521e7-140">Additionally, the folder structure supports semantics for product, version, and even SKU of the IDE.</span></span> <span data-ttu-id="521e7-141">从以下目录的设置的应用"上次在 wins"优先策略下的顺序。</span><span class="sxs-lookup"><span data-stu-id="521e7-141">Settings from these directories are applied in the following order with a "last in wins" precedence strategy.</span></span>

1. <span data-ttu-id="521e7-142">%ProgramData%\NuGet\Config\*.config</span><span class="sxs-lookup"><span data-stu-id="521e7-142">%ProgramData%\NuGet\Config\*.config</span></span>
2. <span data-ttu-id="521e7-143">%ProgramData%\NuGet\Config\{IDE}\*.config</span><span class="sxs-lookup"><span data-stu-id="521e7-143">%ProgramData%\NuGet\Config\{IDE}\*.config</span></span>
3. <span data-ttu-id="521e7-144">%ProgramData%\NuGet\Config\{IDE}\{版本}\*.config</span><span class="sxs-lookup"><span data-stu-id="521e7-144">%ProgramData%\NuGet\Config\{IDE}\{Version}\*.config</span></span>
4. <span data-ttu-id="521e7-145">%ProgramData%\NuGet\Config\{IDE}\{版本}\{SKU}\*.config</span><span class="sxs-lookup"><span data-stu-id="521e7-145">%ProgramData%\NuGet\Config\{IDE}\{Version}\{SKU}\*.config</span></span>

<span data-ttu-id="521e7-146">在此列表中，{IDE} 占位符是特定于在其中运行 NuGet，IDE，因此，对于 Visual Studio 中，它将是"visual Studio"。</span><span class="sxs-lookup"><span data-stu-id="521e7-146">In this list, the {IDE} placeholder is specific to the IDE in which NuGet is running, so in the case of Visual Studio, it will be "VisualStudio".</span></span> <span data-ttu-id="521e7-147">{版本} 和 {SKU} 占位符 （例如由 IDE"11.0"和"WDExpress"、"VWDExpress"和"Pro"，分别)。</span><span class="sxs-lookup"><span data-stu-id="521e7-147">The {Version} and {SKU} placeholders are provided by the IDE (e.g. "11.0" and "WDExpress", "VWDExpress" and "Pro", respectively).</span></span> <span data-ttu-id="521e7-148">然后，该文件夹可以包含许多不同 *.config 文件。</span><span class="sxs-lookup"><span data-stu-id="521e7-148">The folder can then contain many different *.config files.</span></span>
<span data-ttu-id="521e7-149">因此，acme 开发组件公司，作为其产品安装程序的一部分，可通过创建以下文件路径中将仅在 Visual Studio 2012 Professional 和 Ultimate 版本中可见的自定义包源：</span><span class="sxs-lookup"><span data-stu-id="521e7-149">Therefore, the ACME component company can, as a part of their product installer, add a custom package source which will be visible only in the Professional and Ultimate versions of Visual Studio 2012 by creating the following file path:</span></span>

<span data-ttu-id="521e7-150">%ProgramData%\NuGet\Config\VisualStudio\11.0\Pro\acme.config</span><span class="sxs-lookup"><span data-stu-id="521e7-150">%ProgramData%\NuGet\Config\VisualStudio\11.0\Pro\acme.config</span></span>

<span data-ttu-id="521e7-151">尽管文件夹结构使得变得简单程序如软件安装程序将计算机范围包源添加到 NuGet 的配置，NuGet 配置对话框也已更新以便为包源的注册任一特定于用户的 （例如注册 %appdata%/nuget/nuget.config 中） 或计算机范围。</span><span class="sxs-lookup"><span data-stu-id="521e7-151">While the folder structure makes it straightforward for programs like software installers to add machine-wide package sources to NuGet's configuration, the NuGet configuration dialog has also been updated to allow for the registration of package sources as either user-specific (e.g. registered in %AppData%/NuGet/NuGet.Config) or machine-wide.</span></span>

<span data-ttu-id="521e7-152">Visual Studio 2013 中，其中一个文件安装在使用此功能：</span><span class="sxs-lookup"><span data-stu-id="521e7-152">This feature is utilized by Visual Studio 2013, where a file is installed at:</span></span>

<span data-ttu-id="521e7-153">%ProgramData%\NuGet\Config\VisualStudio\12.0\Microsoft.VisualStudio.config</span><span class="sxs-lookup"><span data-stu-id="521e7-153">%ProgramData%\NuGet\Config\VisualStudio\12.0\Microsoft.VisualStudio.config</span></span>

<span data-ttu-id="521e7-154">在此文件中，配置名为".NET Framework 包"的新包源。</span><span class="sxs-lookup"><span data-stu-id="521e7-154">Within this file, a new package source called ".NET Framework Packages" is configured.</span></span>

![NuGet 配置文件的计算机范围的设置](./media/NuGet-Config-File-Machine-Wide.png)

### <a name="contextualizing-search"></a><span data-ttu-id="521e7-156">不一而足搜索</span><span class="sxs-lookup"><span data-stu-id="521e7-156">Contextualizing Search</span></span>

<span data-ttu-id="521e7-157">如的包由 NuGet 库提供服务的数量不断增长指数节奏，NuGet 优先级列表顶部改善搜索曾经保持。</span><span class="sxs-lookup"><span data-stu-id="521e7-157">As the number of packages served by the NuGet gallery continues to grow at an exponential pace, improving search remains ever at the top of the NuGet priority list.</span></span> <span data-ttu-id="521e7-158">Nuget 的计划功能之一是搜索的项目的上下文搜索，这意味着，NuGet 将使用版本以及 SKU 的 Visual Studio 的使用和要生成的类型信息作为条件确定潜在的相关性结果。</span><span class="sxs-lookup"><span data-stu-id="521e7-158">One of the planned features for NuGet is contextual search, meaning that NuGet will use information about the version and SKU of Visual Studio that you are using and the type of project that you are building as criteria for determining the relevance of potential search results.</span></span>

<span data-ttu-id="521e7-159">从 NuGet 2.6 开始，每次安装包时，安装的上下文记录为安装操作数据的一部分。</span><span class="sxs-lookup"><span data-stu-id="521e7-159">Starting with NuGet 2.6, each time a package is installed, the context for the installation is recorded as part of the installation operation data.</span></span>  <span data-ttu-id="521e7-160">搜索还发送相同的上下文信息，这将允许 NuGet 库，以通过上下文安装趋势提升搜索结果。</span><span class="sxs-lookup"><span data-stu-id="521e7-160">Searches also send the same context information, which will allow the NuGet Gallery to boost search results by contextual installation trends.</span></span>  <span data-ttu-id="521e7-161">NuGet 库到未来的更新将启用此上下文相关的相关性提升。</span><span class="sxs-lookup"><span data-stu-id="521e7-161">A future update to the NuGet Gallery will enable this context-sensitive relevance boosting.</span></span>

### <a name="tracking-direct-installs-vs-dependency-installs"></a><span data-ttu-id="521e7-162">跟踪直接安装 vs。依赖项安装</span><span class="sxs-lookup"><span data-stu-id="521e7-162">Tracking Direct Installs vs. Dependency Installs</span></span>

<span data-ttu-id="521e7-163">程序包作者多地依赖于[包统计信息](http://blog.nuget.org/20130226/Introducing-Package-Statistics.html)NuGet 库上提供。</span><span class="sxs-lookup"><span data-stu-id="521e7-163">Package authors are relying more and more on the [Package Statistics](http://blog.nuget.org/20130226/Introducing-Package-Statistics.html) provided on the NuGet Gallery.</span></span>  <span data-ttu-id="521e7-164">一个重要缺少数据点作者已要求是直接包安装，依赖项安装之间的区别。</span><span class="sxs-lookup"><span data-stu-id="521e7-164">One significant missing data point that authors have asked for is a differentiation between direct package installs and dependency installs.</span></span>  <span data-ttu-id="521e7-165">到目前为止，NuGet 客户端未发送任何上下文解决开发人员直接安装包，或如果已安装要满足依赖关系的安装操作。</span><span class="sxs-lookup"><span data-stu-id="521e7-165">Until now, the NuGet client did not send any context around the installation operation for whether the developer directly installed the package or if it was installed to satisfy a dependency.</span></span>
<span data-ttu-id="521e7-166">从 NuGet 2.6 针对安装操作将立即发送数据。</span><span class="sxs-lookup"><span data-stu-id="521e7-166">Starting with NuGet 2.6, that data will now be sent for the installation operation.</span></span>  <span data-ttu-id="521e7-167">NuGet 库上的包统计信息将公开该数据作为单独的安装操作，与"-依赖项"后缀。</span><span class="sxs-lookup"><span data-stu-id="521e7-167">Package Statistics on the NuGet Gallery will expose that data as separate install operations, with a "-Dependency" suffix.</span></span>

* <span data-ttu-id="521e7-168">安装</span><span class="sxs-lookup"><span data-stu-id="521e7-168">Install</span></span>
* <span data-ttu-id="521e7-169">安装依赖项</span><span class="sxs-lookup"><span data-stu-id="521e7-169">Install-Dependency</span></span>
* <span data-ttu-id="521e7-170">更新</span><span class="sxs-lookup"><span data-stu-id="521e7-170">Update</span></span>
* <span data-ttu-id="521e7-171">更新依赖项</span><span class="sxs-lookup"><span data-stu-id="521e7-171">Update-Dependency</span></span>
* <span data-ttu-id="521e7-172">重新安装</span><span class="sxs-lookup"><span data-stu-id="521e7-172">Reinstall</span></span>
* <span data-ttu-id="521e7-173">重新安装依赖项</span><span class="sxs-lookup"><span data-stu-id="521e7-173">Reinstall-Dependency</span></span>

<span data-ttu-id="521e7-174">除了不同的操作名称，还会安装记录依赖的包 id。</span><span class="sxs-lookup"><span data-stu-id="521e7-174">In addition to the different operation name, the dependent package id is also recorded for the installation.</span></span>  <span data-ttu-id="521e7-175">NuGet 库到未来的更新将公开报表，允许包作者，若要全面了解如何开发人员要安装其包中的数据。</span><span class="sxs-lookup"><span data-stu-id="521e7-175">A future update to the NuGet Gallery will expose that data within reports, allowing package authors to fully understand how developers are installing their packages.</span></span>

## <a name="bug-fixes"></a><span data-ttu-id="521e7-176">Bug 修复</span><span class="sxs-lookup"><span data-stu-id="521e7-176">Bug Fixes</span></span>

<span data-ttu-id="521e7-177">NuGet 2.6 还包括多项 bug 修复。</span><span class="sxs-lookup"><span data-stu-id="521e7-177">NuGet 2.6 also includes several bug fixes.</span></span> <span data-ttu-id="521e7-178">有关工作的完整列表项固定在 NuGet 2.6 中，请查看[对于此版本的 NuGet 问题跟踪程序](https://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Closed&type=All&priority=All&release=NuGet%202.6&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0&reasonClosed=All)。</span><span class="sxs-lookup"><span data-stu-id="521e7-178">For a full list of work items fixed in NuGet 2.6, please view the [NuGet Issue Tracker for this release](https://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Closed&type=All&priority=All&release=NuGet%202.6&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0&reasonClosed=All).</span></span>