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
ms.openlocfilehash: b34c0049a5ba42f6bcd5b36fa5b0ba261e27ecd5
ms.sourcegitcommit: a40c1c1cc05a46410f317a72f695ad1d80f39fa2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/05/2018
---
# <a name="nuget-26-release-notes"></a>NuGet 2.6 发行说明

[NuGet 2.5 发行说明](../release-notes/nuget-2.5.md) | [NuGet 2.6.1 for WebMatrix 发行说明](../release-notes/nuget-2.6.1-for-webmatrix.md)

NuGet 2.6 已于 2013 年 6 月 26 日发布。

## <a name="notable-features-in-the-release"></a>发行版中的值得注意的功能

### <a name="support-for-visual-studio-2013"></a>对 Visual Studio 2013 的支持

NuGet 2.6 是提供对 Visual Studio 2013 的支持的第一个版本。 如 Visual Studio 2012，NuGet 包管理器扩展包含在 Visual Studio 的每个版本。

为了提供对 Visual Studio 2013，同时仍支持 Visual Studio 2010 和 Visual Studio 2012 和保持尽可能小的扩展大小的最佳可能支持，我们将生成一个单独的 Visual Studio 2013 时扩展继续针对 Visual Studio 2010 和 2012年原来的扩展名。

从 NuGet 2.6 开始，我们将发布两个扩展，如下所示：

1. [NuGet 包管理器](https://marketplace.visualstudio.com/items?itemName=NuGetTeam.NuGetPackageManager)（适用于 Visual Studio 2010 和 2012年）
1. [用于 Visual Studio 2013 的 NuGet 程序包管理器](https://marketplace.visualstudio.com/items?itemName=NuGetTeam.NuGetPackageManagerforVisualStudio2013)

此拆分， [nuget.org](https://nuget.org)主页的"安装 NuGet"按钮现在你将转到[安装 NuGet](../guides/install-nuget.md)页上，你可以在其中找到有关安装不同的 NuGet 客户端的详细信息。

<a name="xdt"></a>

### <a name="xdt-webconfig-transformation-support"></a>XDT Web.config 转换支持

NuGet 客户端的高请求功能之一是支持更强大的 XML 转换使用的 Visual Studio 生成配置转换中使用的 XDT 转换引擎。

2013 年 4 月，我们做 XDT 的 NuGet 支持的两个大公告。 第一种是在 XDT 库自身正在本身[发布为 NuGet 包](https://nuget.org/packages/Microsoft.Web.Xdt)和[打开来源 CodePlex 上](http://xdt.codeplex.com/)。 此步骤启用 XDT 引擎以自由地供其他开放源代码软件，包括 NuGet 客户端。 第二个公告时要使用 XDT 引擎支持在 NuGet 客户端中进行转换的计划。 NuGet 2.6 包括此集成。

#### <a name="how-it-works"></a>它是如何工作

若要利用的 NuGet 的 XDT 支持，机制查找类似于[当前配置转换功能](../create-packages/source-and-config-file-transformations.md)。
转换文件添加到程序包的内容文件夹。 但是，配置转换进行时使用单个文件安装和卸载，XDT 转换将启用对这两个使用以下文件这些进程细化的控制：

- Web.config.install.xdt
- Web.config.uninstall.xdt

此外，NuGet 使用文件后缀来确定哪些引擎运行进行转换，以便使用现有 web.config.transforms 包将继续工作。 XDT 转换还可应用于任何 XML 文件 (而不仅仅是 web.config)，因此你可以利用这对于其他应用程序项目中。

#### <a name="what-you-can-do-with-xdt"></a>你可以使用 XDT 做什么

XDT 的最大优势之一是其[简单但功能强大的语法](http://msdn.microsoft.com/library/dd465326.aspx)用于操作的结构的 XML dom。 而不是只需覆盖到另一个结构的一个固定的文档结构，XDT 提供用于匹配中有许多种情况下，从简单的属性名称匹配到完整的 XPath 支持的元素的控件。 这意味着添加、 更新或删除的属性，将新元素放置在特定位置，或替换或删除整个，XDT 一旦找到一个匹配元素或一组的元素，提供用于操作元素，一组丰富的函数元素及其子级。

### <a name="machine-wide-configuration"></a>计算机范围的配置

NuGet 的极佳优势之一是它将分解否则为大可执行文件或到一组模块化组件可以独立是集成，并最重要的是保持和已进行版本管理的库。 但是，，的一个副作用是，某个产品或产品系列的常规理论基础可能碎片的增多。
NuGet 的自定义包源功能提供了一种组织包;但是，自定义的包源都不在其自己可发现。

NuGet 2.6 扩展通过搜索 %programdata%/nuget/config 路径下的文件夹层次结构配置 NuGet 的逻辑。产品安装程序可以添加自定义 NuGet 配置文件来注册他们的产品的自定义包源此文件夹下。 此外，文件夹结构的产品、 版本和甚至 SKU 的 IDE 支持语义。 从以下目录的设置的应用"上次在 wins"优先策略下的顺序。

1. %ProgramData%\NuGet\Config\*.config
2. %ProgramData%\NuGet\Config\{IDE}\*.config
3. %ProgramData%\NuGet\Config\{IDE}\{版本}\*.config
4. %ProgramData%\NuGet\Config\{IDE}\{版本}\{SKU}\*.config

在此列表中，{IDE} 占位符是特定于在其中运行 NuGet，IDE，因此，对于 Visual Studio 中，它将是"visual Studio"。 {版本} 和 {SKU} 占位符 （例如由 IDE"11.0"和"WDExpress"、"VWDExpress"和"Pro"，分别)。 然后，该文件夹可以包含许多不同 *.config 文件。
因此，acme 开发组件公司，作为其产品安装程序的一部分，可通过创建以下文件路径中将仅在 Visual Studio 2012 Professional 和 Ultimate 版本中可见的自定义包源：

%ProgramData%\NuGet\Config\VisualStudio\11.0\Pro\acme.config

尽管文件夹结构使得变得简单程序如软件安装程序将计算机范围包源添加到 NuGet 的配置，NuGet 配置对话框也已更新以便为包源的注册任一特定于用户的 （例如注册 %appdata%/nuget/nuget.config 中） 或计算机范围。

Visual Studio 2013 中，其中一个文件安装在使用此功能：

%ProgramData%\NuGet\Config\VisualStudio\12.0\Microsoft.VisualStudio.config

在此文件中，配置名为".NET Framework 包"的新包源。

![NuGet 配置文件的计算机范围的设置](./media/NuGet-Config-File-Machine-Wide.png)

### <a name="contextualizing-search"></a>不一而足搜索

如的包由 NuGet 库提供服务的数量不断增长指数节奏，NuGet 优先级列表顶部改善搜索曾经保持。 Nuget 的计划功能之一是搜索的项目的上下文搜索，这意味着，NuGet 将使用版本以及 SKU 的 Visual Studio 的使用和要生成的类型信息作为条件确定潜在的相关性结果。

从 NuGet 2.6 开始，每次安装包时，安装的上下文记录为安装操作数据的一部分。  搜索还发送相同的上下文信息，这将允许 NuGet 库，以通过上下文安装趋势提升搜索结果。  NuGet 库到未来的更新将启用此上下文相关的相关性提升。

### <a name="tracking-direct-installs-vs-dependency-installs"></a>跟踪直接安装 vs。依赖项安装

程序包作者多地依赖于[包统计信息](http://blog.nuget.org/20130226/Introducing-Package-Statistics.html)NuGet 库上提供。  一个重要缺少数据点作者已要求是直接包安装，依赖项安装之间的区别。  到目前为止，NuGet 客户端未发送任何上下文解决开发人员直接安装包，或如果已安装要满足依赖关系的安装操作。
从 NuGet 2.6 针对安装操作将立即发送数据。  NuGet 库上的包统计信息将公开该数据作为单独的安装操作，与"-依赖项"后缀。

* 安装
* 安装依赖项
* 更新
* 更新依赖项
* 重新安装
* 重新安装依赖项

除了不同的操作名称，还会安装记录依赖的包 id。  NuGet 库到未来的更新将公开报表，允许包作者，若要全面了解如何开发人员要安装其包中的数据。

## <a name="bug-fixes"></a>Bug 修复

NuGet 2.6 还包括多项 bug 修复。 有关工作的完整列表项固定在 NuGet 2.6 中，请查看[对于此版本的 NuGet 问题跟踪程序](https://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Closed&type=All&priority=All&release=NuGet%202.6&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0&reasonClosed=All)。