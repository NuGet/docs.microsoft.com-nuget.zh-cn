---
title: NuGet 2.6 发行说明
description: NuGet 2.6 的发行说明，包括已知问题、bug 修复、新增功能和 Dcr。
author: JonDouglas
ms.author: jodou
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 6b25b9df062afc88466ad107e718f632878debfc
ms.sourcegitcommit: 40c039ace0330dd9e68922882017f9878f4283d1
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/22/2021
ms.locfileid: "107901416"
---
# <a name="nuget-26-release-notes"></a><span data-ttu-id="7648d-103">NuGet 2.6 发行说明</span><span class="sxs-lookup"><span data-stu-id="7648d-103">NuGet 2.6 Release Notes</span></span>

<span data-ttu-id="7648d-104">[NuGet 2.5 发行说明](../release-notes/nuget-2.5.md)  | [NuGet 2.6.1 For WebMatrix 发行说明](../release-notes/nuget-2.6.1-for-webmatrix.md)</span><span class="sxs-lookup"><span data-stu-id="7648d-104">[NuGet 2.5 Release Notes](../release-notes/nuget-2.5.md) | [NuGet 2.6.1 for WebMatrix Release Notes](../release-notes/nuget-2.6.1-for-webmatrix.md)</span></span>

<span data-ttu-id="7648d-105">NuGet 2.6 于2013年6月26日发布。</span><span class="sxs-lookup"><span data-stu-id="7648d-105">NuGet 2.6 was released on June 26, 2013.</span></span>

## <a name="notable-features-in-the-release"></a><span data-ttu-id="7648d-106">版本中值得注意的功能</span><span class="sxs-lookup"><span data-stu-id="7648d-106">Notable features in the release</span></span>

### <a name="support-for-visual-studio-2013"></a><span data-ttu-id="7648d-107">支持 Visual Studio 2013</span><span class="sxs-lookup"><span data-stu-id="7648d-107">Support for Visual Studio 2013</span></span>

<span data-ttu-id="7648d-108">NuGet 2.6 是为 Visual Studio 2013 提供支持的第一个版本。</span><span class="sxs-lookup"><span data-stu-id="7648d-108">NuGet 2.6 is the first release that provides support for Visual Studio 2013.</span></span> <span data-ttu-id="7648d-109">和 Visual Studio 2012 一样，每个版本的 Visual Studio 中都包含 NuGet 包管理器扩展。</span><span class="sxs-lookup"><span data-stu-id="7648d-109">And like Visual Studio 2012, the NuGet Package Manager extension is included in every edition of Visual Studio.</span></span>

<span data-ttu-id="7648d-110">为了尽可能提供对 Visual Studio 2013 的最佳支持，同时同时支持 Visual Studio 2010 和 Visual Studio 2012，并尽可能缩小扩展大小，我们将为 Visual Studio 2013 生成一个单独的扩展，同时原始扩展将继续面向 Visual Studio 2010 和2012。</span><span class="sxs-lookup"><span data-stu-id="7648d-110">In order to provide the best possible support for Visual Studio 2013 while still supporting both Visual Studio 2010 and Visual Studio 2012, and keeping the extension sizes as small as possible, we are producing a separate extension for Visual Studio 2013 while the original extension continues to target both Visual Studio 2010 and 2012.</span></span>

<span data-ttu-id="7648d-111">从 NuGet 2.6 开始，我们将发布两个扩展，如下所示：</span><span class="sxs-lookup"><span data-stu-id="7648d-111">Starting with NuGet 2.6, we will publish two extensions as below:</span></span>

1. <span data-ttu-id="7648d-112">[NuGet 包管理器](https://marketplace.visualstudio.com/items?itemName=NuGetTeam.NuGetPackageManager) (适用于 Visual Studio 2010 和 2012) </span><span class="sxs-lookup"><span data-stu-id="7648d-112">[NuGet Package Manager](https://marketplace.visualstudio.com/items?itemName=NuGetTeam.NuGetPackageManager) (applies to Visual Studio 2010 and 2012)</span></span>
1. [<span data-ttu-id="7648d-113">Visual Studio 2013 的 NuGet 包管理器</span><span class="sxs-lookup"><span data-stu-id="7648d-113">NuGet Package Manager for Visual Studio 2013</span></span>](https://marketplace.visualstudio.com/items?itemName=NuGetTeam.NuGetPackageManagerforVisualStudio2013)

<span data-ttu-id="7648d-114">使用此拆分时， [nuget.org](https://nuget.org) 主页的 "安装 nuget" 按钮将转到 "安装 [nuget](../install-nuget-client-tools.md) " 页，您可以在其中找到有关安装不同 nuget 客户端的详细信息。</span><span class="sxs-lookup"><span data-stu-id="7648d-114">With this split, the [nuget.org](https://nuget.org) home page's "Install NuGet" button takes you to the [installing NuGet](../install-nuget-client-tools.md) page, where you can find more information about installing the different NuGet clients.</span></span>

<a name="xdt"></a>

### <a name="xdt-webconfig-transformation-support"></a><span data-ttu-id="7648d-115">XDT Web.config 转换支持</span><span class="sxs-lookup"><span data-stu-id="7648d-115">XDT Web.config transformation support</span></span>

<span data-ttu-id="7648d-116">NuGet 客户端最常请求的功能之一就是使用在 Visual Studio 生成配置转换中使用的 XDT 转换引擎，支持更强大的 XML 转换。</span><span class="sxs-lookup"><span data-stu-id="7648d-116">One of the most highly-requested features for the NuGet client has been to support more powerful XML transformations using the XDT transformation engine which is used in Visual Studio build configuration transformations.</span></span>

<span data-ttu-id="7648d-117">2013年4月，我们为 XDT 提供了两个有关 NuGet 支持的重要公告。</span><span class="sxs-lookup"><span data-stu-id="7648d-117">In April 2013, we made two big announcements regarding NuGet support for XDT.</span></span> <span data-ttu-id="7648d-118">第一种是，XDT 库本身 [作为 NuGet 包发布](https://nuget.org/packages/Microsoft.Web.Xdt) ，并 [在 CodePlex 上开放](http://xdt.codeplex.com/)。</span><span class="sxs-lookup"><span data-stu-id="7648d-118">The first was that the XDT library itself was being itself [released as a NuGet package](https://nuget.org/packages/Microsoft.Web.Xdt) and [open sourced on CodePlex](http://xdt.codeplex.com/).</span></span> <span data-ttu-id="7648d-119">此步骤启用了其他开源软件（包括 NuGet 客户端）可自由使用的 XDT 引擎。</span><span class="sxs-lookup"><span data-stu-id="7648d-119">This step enabled the XDT engine to be used freely by other open-source software, including the NuGet client.</span></span> <span data-ttu-id="7648d-120">第二个公告是在 NuGet 客户端中支持使用 XDT 引擎进行转换的计划。</span><span class="sxs-lookup"><span data-stu-id="7648d-120">The second announcement was the plan to support use of the XDT engine for transformations in the NuGet client.</span></span> <span data-ttu-id="7648d-121">NuGet 2.6 包括此集成。</span><span class="sxs-lookup"><span data-stu-id="7648d-121">NuGet 2.6 includes this integration.</span></span>

#### <a name="how-it-works"></a><span data-ttu-id="7648d-122">工作原理</span><span class="sxs-lookup"><span data-stu-id="7648d-122">How it works</span></span>

<span data-ttu-id="7648d-123">若要利用 NuGet 的 XDT 支持，该结构与 [当前配置转换功能](../create-packages/source-and-config-file-transformations.md)的外观类似。</span><span class="sxs-lookup"><span data-stu-id="7648d-123">To take advantage of NuGet’s XDT support, the mechanics look similar to those of the [current config transformation feature](../create-packages/source-and-config-file-transformations.md).</span></span>
<span data-ttu-id="7648d-124">转换文件被添加到包的内容文件夹中。</span><span class="sxs-lookup"><span data-stu-id="7648d-124">Transformation files are added to the package’s content folder.</span></span> <span data-ttu-id="7648d-125">但是，虽然配置转换使用单个文件进行安装和卸载，但 XDT 转换使用以下文件实现对这两个过程的精细控制：</span><span class="sxs-lookup"><span data-stu-id="7648d-125">However, while config transformations use a single file for both installation and uninstallation, XDT transformations enable fine-grained control over both of these processes using the following files:</span></span>

- <span data-ttu-id="7648d-126">Web.config xdt</span><span class="sxs-lookup"><span data-stu-id="7648d-126">Web.config.install.xdt</span></span>
- <span data-ttu-id="7648d-127">Web.config xdt</span><span class="sxs-lookup"><span data-stu-id="7648d-127">Web.config.uninstall.xdt</span></span>

<span data-ttu-id="7648d-128">此外，NuGet 使用文件后缀来确定要为转换运行的引擎，以便使用现有 web.config 进行打包。转换将继续工作。</span><span class="sxs-lookup"><span data-stu-id="7648d-128">Additionally, NuGet uses the file suffix to determine which engine to run for transformations, so packages using the existing web.config.transforms will continue to work.</span></span> <span data-ttu-id="7648d-129">还可将 XDT 转换应用到任何 XML 文件 (不 web.config) ，因此，你可以将此应用于项目中的其他应用程序。</span><span class="sxs-lookup"><span data-stu-id="7648d-129">XDT transformations can also be applied to any XML file (not just web.config), so you can leverage this for other applications in your project.</span></span>

#### <a name="what-you-can-do-with-xdt"></a><span data-ttu-id="7648d-130">可以通过 XDT 执行的操作</span><span class="sxs-lookup"><span data-stu-id="7648d-130">What you can do with XDT</span></span>

<span data-ttu-id="7648d-131">XDT 的最大优势之一是它的 [简单但功能强大的语法](/previous-versions/aspnet/dd465326(v=vs.110)) ，用于处理 XML DOM 的结构。</span><span class="sxs-lookup"><span data-stu-id="7648d-131">One of XDT’s greatest strengths is its [simple but powerful syntax](/previous-versions/aspnet/dd465326(v=vs.110)) for manipulating the structure of an XML DOM.</span></span> <span data-ttu-id="7648d-132">XDT 可以通过多种方式（从简单的属性名称匹配到完整的 XPath 支持）为匹配元素提供控件，而不是只是将一个固定文档结构覆盖到另一结构。</span><span class="sxs-lookup"><span data-stu-id="7648d-132">Rather than simply overlaying one fixed document structure onto another structure, XDT provides controls for matching elements in a variety of ways, from simple attribute name matching to full XPath support.</span></span> <span data-ttu-id="7648d-133">一旦找到匹配的元素或一组元素，XDT 就提供了一组丰富的用于操作元素的函数，无论是指添加、更新或删除属性、将新元素放在特定位置还是替换或删除整个元素及其子级。</span><span class="sxs-lookup"><span data-stu-id="7648d-133">Once a matching element or set of elements is found, XDT provides a rich set of functions for manipulating the elements, whether that means adding, updating, or removing attributes, placing a new element at a specific location, or replacing or removing the entire element and its children.</span></span>

### <a name="machine-wide-configuration"></a><span data-ttu-id="7648d-134">Machine-Wide 配置</span><span class="sxs-lookup"><span data-stu-id="7648d-134">Machine-Wide Configuration</span></span>

<span data-ttu-id="7648d-135">NuGet 的优点之一是，它将其他大的可执行文件或库分解为一组模块化组件，这些组件可进行集成，并且最重要的维护和版本控制。</span><span class="sxs-lookup"><span data-stu-id="7648d-135">One of the great strengths of NuGet is that it breaks down an otherwise large executable or library into a set of modular components which can be integrated, and most importantly maintained and versioned independently.</span></span> <span data-ttu-id="7648d-136">不过，这种情况的一个副作用是，产品或产品系列的传统思路可能会产生更多的碎片。</span><span class="sxs-lookup"><span data-stu-id="7648d-136">One side effect of this, however, is that the conventional idea of a product or product family becomes potentially more fragmented.</span></span>
<span data-ttu-id="7648d-137">NuGet 的自定义包源功能提供了一种组织包的方式;但是，自定义包源本身无法发现。</span><span class="sxs-lookup"><span data-stu-id="7648d-137">NuGet’s custom package source feature provides one way of organizing packages; however, custom package sources are not discoverable on their own.</span></span>

<span data-ttu-id="7648d-138">NuGet 2.6 通过在路径% ProgramData%/NuGet/Config. 下搜索文件夹层次结构来扩展用于配置 NuGet 的逻辑。产品安装程序可在此文件夹下添加自定义 NuGet 配置文件，以便为其产品注册自定义包源。</span><span class="sxs-lookup"><span data-stu-id="7648d-138">NuGet 2.6 extends the logic for configuring NuGet by searching the folder hierarchy under the path %ProgramData%/NuGet/Config. Product installers can add custom NuGet configuration files under this folder to register a custom package source for their products.</span></span> <span data-ttu-id="7648d-139">此外，文件夹结构还支持 IDE 的产品、版本甚至 SKU 的语义。</span><span class="sxs-lookup"><span data-stu-id="7648d-139">Additionally, the folder structure supports semantics for product, version, and even SKU of the IDE.</span></span> <span data-ttu-id="7648d-140">这些目录中的设置将按以下顺序应用，并具有 "last in wins" 优先级策略。</span><span class="sxs-lookup"><span data-stu-id="7648d-140">Settings from these directories are applied in the following order with a "last in wins" precedence strategy.</span></span>

1. <span data-ttu-id="7648d-141">%ProgramData%\NuGet\Config \*</span><span class="sxs-lookup"><span data-stu-id="7648d-141">%ProgramData%\NuGet\Config\*.config</span></span>
2. <span data-ttu-id="7648d-142">%ProgramData%\NuGet\Config \{ IDE} \* .config</span><span class="sxs-lookup"><span data-stu-id="7648d-142">%ProgramData%\NuGet\Config\{IDE}\*.config</span></span>
3. <span data-ttu-id="7648d-143">%ProgramData%\NuGet\Config \{ IDE} \{ 版本} \* .config</span><span class="sxs-lookup"><span data-stu-id="7648d-143">%ProgramData%\NuGet\Config\{IDE}\{Version}\*.config</span></span>
4. <span data-ttu-id="7648d-144">%ProgramData%\NuGet\Config \{ IDE} \{ 版本} \{ SKU} \* .config</span><span class="sxs-lookup"><span data-stu-id="7648d-144">%ProgramData%\NuGet\Config\{IDE}\{Version}\{SKU}\*.config</span></span>

<span data-ttu-id="7648d-145">在此列表中，{IDE} 占位符特定于运行 NuGet 的 IDE，因此，在 Visual Studio 中，它将为 "VisualStudio"。</span><span class="sxs-lookup"><span data-stu-id="7648d-145">In this list, the {IDE} placeholder is specific to the IDE in which NuGet is running, so in the case of Visual Studio, it will be "VisualStudio".</span></span> <span data-ttu-id="7648d-146">IDE (（例如 "11.0" 和 "WDExpress"、"VWDExpress" 和 "Pro"）) 分别提供 {Version} 和 {SKU} 占位符。</span><span class="sxs-lookup"><span data-stu-id="7648d-146">The {Version} and {SKU} placeholders are provided by the IDE (e.g. "11.0" and "WDExpress", "VWDExpress" and "Pro", respectively).</span></span> <span data-ttu-id="7648d-147">然后，文件夹可以包含许多不同的 \* .config 文件。</span><span class="sxs-lookup"><span data-stu-id="7648d-147">The folder can then contain many different \*.config files.</span></span>
<span data-ttu-id="7648d-148">因此，ACME 组件公司可以作为其产品安装程序的一部分，添加自定义包源，仅在 Visual Studio 2012 的专业版和旗舰版（通过创建以下文件路径）中可见：</span><span class="sxs-lookup"><span data-stu-id="7648d-148">Therefore, the ACME component company can, as a part of their product installer, add a custom package source which will be visible only in the Professional and Ultimate versions of Visual Studio 2012 by creating the following file path:</span></span>

<span data-ttu-id="7648d-149">% ProgramData% \NuGet\Config\VisualStudio\11.0\Pro\acme.config</span><span class="sxs-lookup"><span data-stu-id="7648d-149">%ProgramData%\NuGet\Config\VisualStudio\11.0\Pro\acme.config</span></span>

<span data-ttu-id="7648d-150">虽然该文件夹结构使软件安装程序等程序可以简单地将计算机范围的包源添加到 NuGet 的配置，但还更新了 NuGet 配置对话框，以允许将包源注册为用户特定的 (例如，在% AppData%/NuGet/NuGet.Config) 或计算机范围内注册。</span><span class="sxs-lookup"><span data-stu-id="7648d-150">While the folder structure makes it straightforward for programs like software installers to add machine-wide package sources to NuGet's configuration, the NuGet configuration dialog has also been updated to allow for the registration of package sources as either user-specific (e.g. registered in %AppData%/NuGet/NuGet.Config) or machine-wide.</span></span>

<span data-ttu-id="7648d-151">此功能的使用 Visual Studio 2013，其中的文件安装位置如下：</span><span class="sxs-lookup"><span data-stu-id="7648d-151">This feature is utilized by Visual Studio 2013, where a file is installed at:</span></span>

<span data-ttu-id="7648d-152">% ProgramData% \NuGet\Config\VisualStudio\12.0\Microsoft.VisualStudio.config</span><span class="sxs-lookup"><span data-stu-id="7648d-152">%ProgramData%\NuGet\Config\VisualStudio\12.0\Microsoft.VisualStudio.config</span></span>

<span data-ttu-id="7648d-153">在此文件中，将配置名为 ".NET Framework 包" 的新包源。</span><span class="sxs-lookup"><span data-stu-id="7648d-153">Within this file, a new package source called ".NET Framework Packages" is configured.</span></span>

![NuGet 配置文件计算机范围设置](./media/NuGet-Config-File-Machine-Wide.png)

### <a name="contextualizing-search"></a><span data-ttu-id="7648d-155">Contextualizing 搜索</span><span class="sxs-lookup"><span data-stu-id="7648d-155">Contextualizing Search</span></span>

<span data-ttu-id="7648d-156">随着 NuGet 库所提供的包数量不断增长，在 NuGet 优先级列表的顶部，提高搜索范围。</span><span class="sxs-lookup"><span data-stu-id="7648d-156">As the number of packages served by the NuGet gallery continues to grow at an exponential pace, improving search remains ever at the top of the NuGet priority list.</span></span> <span data-ttu-id="7648d-157">NuGet 的计划功能之一是上下文搜索，也就是说，NuGet 将使用有关所使用的 Visual Studio 版本和 SKU 的信息，以及要生成的项目类型，以确定潜在搜索结果的相关性。</span><span class="sxs-lookup"><span data-stu-id="7648d-157">One of the planned features for NuGet is contextual search, meaning that NuGet will use information about the version and SKU of Visual Studio that you are using and the type of project that you are building as criteria for determining the relevance of potential search results.</span></span>

<span data-ttu-id="7648d-158">从 NuGet 2.6 开始，每次安装包时，安装的上下文都将记录为安装操作数据的一部分。</span><span class="sxs-lookup"><span data-stu-id="7648d-158">Starting with NuGet 2.6, each time a package is installed, the context for the installation is recorded as part of the installation operation data.</span></span>  <span data-ttu-id="7648d-159">搜索还会发送相同的上下文信息，使 NuGet 库能够按上下文安装趋势增加搜索结果。</span><span class="sxs-lookup"><span data-stu-id="7648d-159">Searches also send the same context information, which will allow the NuGet Gallery to boost search results by contextual installation trends.</span></span>  <span data-ttu-id="7648d-160">对 NuGet 库的未来更新将实现此上下文相关的相关性提升。</span><span class="sxs-lookup"><span data-stu-id="7648d-160">A future update to the NuGet Gallery will enable this context-sensitive relevance boosting.</span></span>

### <a name="tracking-direct-installs-vs-dependency-installs"></a><span data-ttu-id="7648d-161">跟踪直接安装与依赖项安装</span><span class="sxs-lookup"><span data-stu-id="7648d-161">Tracking Direct Installs vs. Dependency Installs</span></span>

<span data-ttu-id="7648d-162">包作者依赖于 NuGet 库上提供的 [包统计信息](http://blog.nuget.org/20130226/Introducing-Package-Statistics.html) 。</span><span class="sxs-lookup"><span data-stu-id="7648d-162">Package authors are relying more and more on the [Package Statistics](http://blog.nuget.org/20130226/Introducing-Package-Statistics.html) provided on the NuGet Gallery.</span></span>  <span data-ttu-id="7648d-163">作者要求的一个重要的数据点是直接包安装和依赖项安装之间的差异。</span><span class="sxs-lookup"><span data-stu-id="7648d-163">One significant missing data point that authors have asked for is a differentiation between direct package installs and dependency installs.</span></span>  <span data-ttu-id="7648d-164">到现在为止，NuGet 客户端不会在安装操作周围发送任何上下文，无论开发人员是否直接安装了包，或者是否已安装以满足依赖项的需要。</span><span class="sxs-lookup"><span data-stu-id="7648d-164">Until now, the NuGet client did not send any context around the installation operation for whether the developer directly installed the package or if it was installed to satisfy a dependency.</span></span>
<span data-ttu-id="7648d-165">从 NuGet 2.6 开始，现在将为安装操作发送数据。</span><span class="sxs-lookup"><span data-stu-id="7648d-165">Starting with NuGet 2.6, that data will now be sent for the installation operation.</span></span>  <span data-ttu-id="7648d-166">NuGet 库中的包统计信息会将这些数据作为单独的安装操作公开，并带有 "-依赖项" 后缀。</span><span class="sxs-lookup"><span data-stu-id="7648d-166">Package Statistics on the NuGet Gallery will expose that data as separate install operations, with a "-Dependency" suffix.</span></span>

* <span data-ttu-id="7648d-167">安装</span><span class="sxs-lookup"><span data-stu-id="7648d-167">Install</span></span>
* <span data-ttu-id="7648d-168">Install-Dependency</span><span class="sxs-lookup"><span data-stu-id="7648d-168">Install-Dependency</span></span>
* <span data-ttu-id="7648d-169">更新</span><span class="sxs-lookup"><span data-stu-id="7648d-169">Update</span></span>
* <span data-ttu-id="7648d-170">Update-Dependency</span><span class="sxs-lookup"><span data-stu-id="7648d-170">Update-Dependency</span></span>
* <span data-ttu-id="7648d-171">重新安装</span><span class="sxs-lookup"><span data-stu-id="7648d-171">Reinstall</span></span>
* <span data-ttu-id="7648d-172">Reinstall-Dependency</span><span class="sxs-lookup"><span data-stu-id="7648d-172">Reinstall-Dependency</span></span>

<span data-ttu-id="7648d-173">除了不同的操作名称外，还会为安装记录依赖程序包 id。</span><span class="sxs-lookup"><span data-stu-id="7648d-173">In addition to the different operation name, the dependent package id is also recorded for the installation.</span></span>  <span data-ttu-id="7648d-174">对 NuGet 库的将来更新将在报表中公开这些数据，以使包创作者能够充分了解开发人员安装包的方式。</span><span class="sxs-lookup"><span data-stu-id="7648d-174">A future update to the NuGet Gallery will expose that data within reports, allowing package authors to fully understand how developers are installing their packages.</span></span>

## <a name="bug-fixes"></a><span data-ttu-id="7648d-175">Bug 修复</span><span class="sxs-lookup"><span data-stu-id="7648d-175">Bug Fixes</span></span>

<span data-ttu-id="7648d-176">NuGet 2.6 还包括多个 bug 修复。</span><span class="sxs-lookup"><span data-stu-id="7648d-176">NuGet 2.6 also includes several bug fixes.</span></span> <span data-ttu-id="7648d-177">有关 NuGet 2.6 中已修复的工作项的完整列表，请查看 [此版本的 NuGet 问题跟踪程序](https://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Closed&type=All&priority=All&release=NuGet%202.6&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0&reasonClosed=All)。</span><span class="sxs-lookup"><span data-stu-id="7648d-177">For a full list of work items fixed in NuGet 2.6, please view the [NuGet Issue Tracker for this release](https://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Closed&type=All&priority=All&release=NuGet%202.6&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0&reasonClosed=All).</span></span>