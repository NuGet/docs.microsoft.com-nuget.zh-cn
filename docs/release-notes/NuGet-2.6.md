---
title: NuGet 2.6 发行说明
description: NuGet 2.6.1 for WebMatrix 的发行说明，包括已知问题、bug 修复、新增功能和 Dcr。
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 5e80965aad4caa69130be31a37b7f5f5ffb12ea6
ms.sourcegitcommit: 26a8eae00af2d4be581171e7a73009f94534c336
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/25/2019
ms.locfileid: "75384119"
---
# <a name="nuget-26-release-notes"></a>NuGet 2.6 发行说明

[Nuget 2.5 发行说明](../release-notes/nuget-2.5.md) | [Nuget 2.6.1 For WebMatrix 发行说明](../release-notes/nuget-2.6.1-for-webmatrix.md)

NuGet 2.6 于2013年6月26日发布。

## <a name="notable-features-in-the-release"></a>版本中值得注意的功能

### <a name="support-for-visual-studio-2013"></a>支持 Visual Studio 2013

NuGet 2.6 是为 Visual Studio 2013 提供支持的第一个版本。 和 Visual Studio 2012 一样，每个版本的 Visual Studio 中都包含 NuGet 包管理器扩展。

若要为 Visual Studio 2013 提供尽可能好的支持，同时仍然支持 Visual Studio 2010 和 Visual Studio 2012，并尽可能缩小扩展大小，我们将为 Visual Studio 2013 生成一个单独的扩展，同时原始扩展将继续面向 Visual Studio 2010 和2012。

从 NuGet 2.6 开始，我们将发布两个扩展，如下所示：

1. [NuGet 包管理器](https://marketplace.visualstudio.com/items?itemName=NuGetTeam.NuGetPackageManager)（适用于 Visual Studio 2010 和2012）
1. [Visual Studio 2013 的 NuGet 包管理器](https://marketplace.visualstudio.com/items?itemName=NuGetTeam.NuGetPackageManagerforVisualStudio2013)

使用此拆分时， [nuget.org](https://nuget.org)主页的 "安装 nuget" 按钮将转到 "安装[nuget](../install-nuget-client-tools.md) " 页，您可以在其中找到有关安装不同 nuget 客户端的详细信息。

<a name="xdt"></a>

### <a name="xdt-webconfig-transformation-support"></a>XDT Web.config 转换支持

NuGet 客户端最常请求的功能之一就是使用在 Visual Studio 生成配置转换中使用的 XDT 转换引擎，支持更强大的 XML 转换。

2013年4月，我们为 XDT 提供了两个有关 NuGet 支持的重要公告。 第一种是，XDT 库本身[作为 NuGet 包发布](https://nuget.org/packages/Microsoft.Web.Xdt)，并[在 CodePlex 上开放](http://xdt.codeplex.com/)。 此步骤启用了其他开源软件（包括 NuGet 客户端）可自由使用的 XDT 引擎。 第二个公告是在 NuGet 客户端中支持使用 XDT 引擎进行转换的计划。 NuGet 2.6 包括此集成。

#### <a name="how-it-works"></a>工作原理

若要利用 NuGet 的 XDT 支持，该结构与[当前配置转换功能](../create-packages/source-and-config-file-transformations.md)的外观类似。
转换文件被添加到包的内容文件夹中。 但是，虽然配置转换使用单个文件进行安装和卸载，但 XDT 转换使用以下文件实现对这两个过程的精细控制：

- Web.config.install.xdt
- Web.config.uninstall.xdt

此外，NuGet 使用文件后缀来确定要为转换运行的引擎，以便使用现有 web.config 的包将继续工作。 XDT 转换还可以应用于任何 XML 文件（而不仅仅是 web.config），因此可以将此应用于项目中的其他应用程序。

#### <a name="what-you-can-do-with-xdt"></a>可以通过 XDT 执行的操作

XDT 的最大优势之一是它的[简单但功能强大的语法](https://docs.microsoft.com/previous-versions/aspnet/dd465326(v=vs.110))，用于处理 XML DOM 的结构。 XDT 可以通过多种方式（从简单的属性名称匹配到完整的 XPath 支持）为匹配元素提供控件，而不是只是将一个固定文档结构覆盖到另一结构。 一旦找到匹配的元素或一组元素，XDT 就提供了一组丰富的用于操作元素的函数，无论是指添加、更新或删除属性、将新元素放在特定位置还是替换或删除整个元素及其子元素。

### <a name="machine-wide-configuration"></a>计算机范围的配置

NuGet 的优点之一是，它将其他大的可执行文件或库分解为一组模块化组件，这些组件可进行集成，并且最重要的维护和版本控制。 不过，这种情况的一个副作用是，产品或产品系列的传统思路可能会产生更多的碎片。
NuGet 的自定义包源功能提供了一种组织包的方式;但是，自定义包源本身无法发现。

NuGet 2.6 通过在路径% ProgramData%/NuGet/Config. 下搜索文件夹层次结构来扩展用于配置 NuGet 的逻辑。产品安装程序可在此文件夹下添加自定义 NuGet 配置文件，以便为其产品注册自定义包源。 此外，文件夹结构还支持 IDE 的产品、版本甚至 SKU 的语义。 这些目录中的设置将按以下顺序应用，并具有 "last in wins" 优先级策略。

1. %ProgramData%\NuGet\Config\*.config
2. %ProgramData%\NuGet\Config\{IDE}\*.config
3. %ProgramData%\NuGet\Config\{IDE}\{Version}\*.config
4. %ProgramData%\NuGet\Config\{IDE}\{Version}\{SKU}\*.config

在此列表中，{IDE} 占位符特定于运行 NuGet 的 IDE，因此，在 Visual Studio 中，它将为 "VisualStudio"。 IDE （例如 "11.0" 和 "WDExpress"、"VWDExpress" 和 "Pro"）提供了 {Version} 和 {SKU} 占位符。 然后，文件夹可以包含许多不同的 * .config 文件。
因此，ACME 组件公司可以作为其产品安装程序的一部分，添加自定义包源，仅在 Visual Studio 2012 的专业版和旗舰版（通过创建以下文件路径）中可见：

%ProgramData%\NuGet\Config\VisualStudio\11.0\Pro\acme.config

虽然文件夹结构使软件安装程序等程序可以简单地将计算机范围的包源添加到 NuGet 的配置，但还更新了 NuGet 配置对话框，以允许将包源注册为用户特定的（例如，在% AppData%/NuGet/NuGet.Config 中注册）或计算机范围。

此功能的使用 Visual Studio 2013，其中的文件安装位置如下：

%ProgramData%\NuGet\Config\VisualStudio\12.0\Microsoft.VisualStudio.config

在此文件中，将配置名为 ".NET Framework 包" 的新包源。

![NuGet 配置文件计算机范围设置](./media/NuGet-Config-File-Machine-Wide.png)

### <a name="contextualizing-search"></a>Contextualizing 搜索

随着 NuGet 库所提供的包数量不断增长，在 NuGet 优先级列表的顶部，提高搜索范围。 NuGet 的计划功能之一是上下文搜索，也就是说，NuGet 将使用有关所使用的 Visual Studio 版本和 SKU 的信息，以及要构建为确定潜在搜索相关性的条件的项目类型后果.

从 NuGet 2.6 开始，每次安装包时，安装的上下文都将记录为安装操作数据的一部分。  搜索还会发送相同的上下文信息，使 NuGet 库能够按上下文安装趋势增加搜索结果。  对 NuGet 库的未来更新将实现此上下文相关的相关性提升。

### <a name="tracking-direct-installs-vs-dependency-installs"></a>跟踪直接安装与依赖项安装

包作者依赖于 NuGet 库上提供的[包统计信息](http://blog.nuget.org/20130226/Introducing-Package-Statistics.html)。  作者要求的一个重要的数据点是直接包安装和依赖项安装之间的差异。  到现在为止，NuGet 客户端不会在安装操作周围发送任何上下文，无论开发人员是否直接安装了包，或者是否已安装以满足依赖项的需要。
从 NuGet 2.6 开始，现在将为安装操作发送数据。  NuGet 库中的包统计信息会将这些数据作为单独的安装操作公开，并带有 "-依赖项" 后缀。

* 安装
* 安装-依赖项
* 更新
* 更新-依赖项
* 重新安装
* 重新安装-依赖项

除了不同的操作名称外，还会为安装记录依赖程序包 id。  对 NuGet 库的将来更新将在报表中公开这些数据，以使包创作者能够充分了解开发人员安装包的方式。

## <a name="bug-fixes"></a>Bug 修复

NuGet 2.6 还包括多个 bug 修复。 有关 NuGet 2.6 中已修复的工作项的完整列表，请查看[此版本的 NuGet 问题跟踪程序](https://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Closed&type=All&priority=All&release=NuGet%202.6&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0&reasonClosed=All)。