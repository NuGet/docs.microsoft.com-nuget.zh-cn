---
title: NuGet 2.6 发行说明
description: 发行说明适用于 NuGet 2.6.1 的 WebMatrix 包括已知的问题、 bug 修复、 新增的功能和 Dcr。
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: f011a8db7ac2067a2ed7db67849d63f7dd40d1ce
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/04/2018
ms.locfileid: "43551938"
---
# <a name="nuget-26-release-notes"></a>NuGet 2.6 发行说明

[NuGet 2.5 发行说明](../release-notes/nuget-2.5.md) | [NuGet 2.6.1 for WebMatrix 发行说明](../release-notes/nuget-2.6.1-for-webmatrix.md)

NuGet 2.6 已于 2013 年 6 月 26 日发布。

## <a name="notable-features-in-the-release"></a>在版本中值得注意的功能

### <a name="support-for-visual-studio-2013"></a>对 Visual Studio 2013 的支持

NuGet 2.6 是提供对 Visual Studio 2013 的支持的第一个版本。 例如 Visual Studio 2012，NuGet 包管理器扩展包含在 Visual Studio 的每个版本。

为了提供尽可能最好的支持 Visual Studio 2013，同时仍支持 Visual Studio 2010 和 Visual Studio 2012 中，和保持扩展大小越小越好，我们会生成适用于 Visual Studio 2013 时的单独扩展原来的扩展名继续针对 Visual Studio 2010 和 2012年。

从 NuGet 2.6 开始，我们将发布两个扩展，按如下所示：

1. [NuGet 包管理器](https://marketplace.visualstudio.com/items?itemName=NuGetTeam.NuGetPackageManager)（适用于 Visual Studio 2010 和 2012年）
1. [Visual Studio 2013 的 NuGet 包管理器](https://marketplace.visualstudio.com/items?itemName=NuGetTeam.NuGetPackageManagerforVisualStudio2013)

此拆分[nuget.org](https://nuget.org)主页的"安装 NuGet"按钮可转到[安装 NuGet](../install-nuget-client-tools.md)页上，在哪里可以找到有关安装不同的 NuGet 客户端的详细信息。

<a name="xdt"></a>

### <a name="xdt-webconfig-transformation-support"></a>XDT Web.config 转换支持

NuGet 客户端的高请求功能之一是支持使用 XDT 转换引擎，在 Visual Studio 生成的配置转换中使用该功能更强大的 XML 转换。

在 2013 年 4 月，我们使 XDT 的 NuGet 支持的两个大公告。 第一种是 XDT 库本身已被本身[发布为 NuGet 包](https://nuget.org/packages/Microsoft.Web.Xdt)并[CodePlex 上的开源](http://xdt.codeplex.com/)。 此步骤启用通过包括 NuGet 客户端的其他开放源代码软件自由地使用 XDT 引擎。 第二个公告时计划使用 XDT 引擎支持在 NuGet 客户端中进行转换。 NuGet 2.6 包括此集成。

#### <a name="how-it-works"></a>其工作原理

若要利用 NuGet 的 XDT 支持，机制类似于那些[当前配置转换功能](../create-packages/source-and-config-file-transformations.md)。
转换文件添加到包的内容文件夹。 但是，虽然配置转换使用单个文件进行安装和卸载，XDT 转换允许精细地控制这两个过程使用以下文件：

- Web.config.install.xdt
- Web.config.uninstall.xdt

此外，NuGet 使用文件后缀来确定哪个引擎运行的转换，因此使用现有 web.config.transforms 包将继续工作。 XDT 转换还可以应用于任何 XML 文件 (而不仅仅是 web.config)，因此可以在项目中利用这对于其他应用程序。

#### <a name="what-you-can-do-with-xdt"></a>您可以使用 XDT 做什么

XDT 的最大优势之一是其[简单但功能强大的语法](http://msdn.microsoft.com/library/dd465326.aspx)用于操作 XML dom。 结构 而不是只需覆盖到另一个结构的一个固定的文档结构，XDT 提供对匹配的元素中有许多种情况下，从简单的属性名称匹配到完整的 XPath 支持的控制。 这意味着添加、 更新或删除属性，将新元素放置在特定位置，或替换或删除整个，XDT 一旦找到匹配的元素集，提供用于操作元素，一组丰富的函数元素与其子项。

### <a name="machine-wide-configuration"></a>计算机范围的配置

NuGet 的很好的优势之一是将拆否则为大型的可执行文件或库为一系列可进行集成，以及最重要的是维护和版本控制独立模块化组件。 此操作，一个副作用，但可能会变得更分段产品或产品系列的常规思路。
NuGet 的自定义包源功能提供了一种方法的组织包;但是，自定义包源不是靠自己可发现的。

NuGet 2.6 扩展配置的搜索路径 %programdata%/nuget/config 下的文件夹层次结构的 NuGet 逻辑。产品安装程序可以添加自定义 NuGet 配置文件来注册他们的产品的自定义包源此文件夹下。 此外，文件夹结构中支持产品、 版本和甚至 SKU IDE 的语义。 "上次中胜出"优先策略下的顺序应用这些目录中的设置。

1. %ProgramData%\NuGet\Config\*.config
2. %ProgramData%\NuGet\Config\{IDE}\*.config
3. %ProgramData%\NuGet\Config\{IDE}\{Version}\*.config
4. %ProgramData%\NuGet\Config\{IDE}\{Version}\{SKU}\*.config

在此列表中，{IDE} 占位符是特定于运行 NuGet IDE，因此对于 Visual Studio 中，它将是"visual Studio"。 {Version} 和 {SKU} 占位符 （例如由 IDE 提供"11.0"和"WDExpress"、"VWDExpress"和"Pro"分别)。 该文件夹然后可以包含许多不同 *.config 文件。
因此，ACME 组件公司可以其产品安装程序的一部分，添加将会看到仅在 Visual Studio 2012 Professional 和 Ultimate 版本中创建以下文件路径的自定义包源：

%ProgramData%\NuGet\Config\VisualStudio\11.0\Pro\acme.config

虽然文件夹结构非常简单的程序，如软件安装程序将计算机范围的包源添加到 NuGet 的配置，NuGet 配置对话框也进行了更新以便为包源的注册任一特定于用户的 （例如注册 %appdata%/nuget/nuget.config 中） 或计算机范围。

通过 Visual Studio 2013 中，在安装文件，其中使用此功能：

%ProgramData%\NuGet\Config\VisualStudio\12.0\Microsoft.VisualStudio.config

在此文件中，配置名为".NET Framework 包"的新包源。

![NuGet 配置文件的计算机范围的设置](./media/NuGet-Config-File-Machine-Wide.png)

### <a name="contextualizing-search"></a>不一而足搜索

由于提供的 NuGet 库包的数量将继续以指数速度增长，在 NuGet 优先级列表的顶部改善搜索曾经留下。 适用于 NuGet 计划推出的功能之一是搜索的项目的上下文搜索，这意味着，NuGet 将使用有关版本和 SKU 的 Visual Studio 的使用和生成的类型信息作为条件用于确定潜在相关性结果。

从 NuGet 2.6 开始，每次安装包时，安装的上下文记录为安装操作数据的一部分。  搜索还发送相同的上下文信息，这将允许 NuGet 库，以通过上下文安装趋势来提高搜索结果。  NuGet 库的将来更新将启用此上下文相关的相关性提升。

### <a name="tracking-direct-installs-vs-dependency-installs"></a>跟踪直接安装 vs。依赖项安装

包创建者将越来越多地依赖于[包的统计信息](http://blog.nuget.org/20130226/Introducing-Package-Statistics.html)NuGet 库中提供。  一个明显缺少数据点作者已要求进行是直接的包将安装与依赖项安装之间的差异。  到目前为止，NuGet 客户端未发送任何上下文周围是否开发人员直接安装包，或者如果它已安装要满足依赖项的安装操作。
有了 NuGet 2.6 开始针对安装操作将立即发送数据。  NuGet 库包的统计信息将该将数据公开为单独的安装操作，使用"-依赖关系"后缀。

* 安装
* 安装依赖项
* 更新
* 更新依赖关系
* 重新安装
* 重新安装依赖项

除了不同的操作名称，也会安装记录依赖的包 id。  NuGet 库的将来更新将公开该数据在报表内，允许包创建者完全了解开发人员如何安装它们的包。

## <a name="bug-fixes"></a>Bug 修复

NuGet 2.6 还包括多项 bug 修复。 有关工作的完整列表项固定在 NuGet 2.6 中，请查看[对于此版本的 NuGet 问题跟踪程序](https://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Closed&type=All&priority=All&release=NuGet%202.6&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0&reasonClosed=All)。