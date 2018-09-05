---
title: NuGet 1.2 发行说明
description: 包括已知的问题、 bug 修复、 新增的功能和 Dcr NuGet 1.2 的发行说明。
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: b47f73c1c225540226d3780e17053427b8ea4a8a
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/04/2018
ms.locfileid: "43545682"
---
# <a name="nuget-12-release-notes"></a>NuGet 1.2 发行说明

[NuGet 1.0 和 1.1 发行说明](../release-notes/nuget-1.1.md) | [NuGet 1.3 发行说明](../release-notes/nuget-1.3.md)

NuGet 1.2 已于 2011 年 3 月 30 日发布。

## <a name="new-features"></a>新增功能

### <a name="framework-profile-support"></a>框架配置文件的支持

从一开始，NuGet 支持具有库定目标到不同的框架。 但现在包可能包含目标特定的配置文件，如 Windows Phone 配置文件的程序集。 若要针对特定的配置文件的一个框架，追加划线后跟的配置文件的缩写形式。 例如，若要针对 Windows Phone (又称 Windows Phone 7) 上运行的 SilverLight，可以将程序集放在 sl3 wp 文件夹中，如以下屏幕截图所示。

![框架配置文件文件夹布局](./media/framework-profile-support.png)

您可能会问为什么我们不只是选择使用"wp7"作为名字对象。 部分，我们要预测，Windows Phone 7 可能在将来运行 Silverlight 的较新版本，在这种情况下可能需要进行更细致地指出哪个框架配置文件，因此继续针对。

### <a name="automatically-add-binding-redirects"></a>自动添加绑定重定向

当使用强名称程序集安装包，NuGet 现在可以检测项目需要绑定重定向添加到项目编译并自动将其添加顺序中的配置文件的情况。 第 3 部分的 David Ebbo 的博客文章系列上标题为的 NuGet 版本控制"[通过绑定重定向统一](http://blog.davidebbo.com/2011/01/nuget-versioning-part-3-unification-via.html)"介绍了此功能的更多详细信息的用途。

<a name="framework-assembly-refs"></a>

### <a name="specifying-framework-assembly-references-gac"></a>指定 Framework 程序集引用 (GAC)

在某些情况下，包可能依赖于.NET Framework 中的程序集。 严格地说，它并不总是必要的包使用者引用 framework 程序集。 但在某些情况下，很重要的是，例如开发人员需要针对该程序集中的类型进行编码以便使用您的包。 新`frameworkAssemblies`元素，元数据元素的子元素允许您指定的一组`frameworkAssembly`指向 Framework 程序集位于 GAC 中的元素。 请注意对 Framework 程序集的强调。
这些程序集不包含在包中，因为它们被假定为每台计算机上作为.NET Framework 的一部分。 下表列出了属性的`frameworkAssembly`元素。


|特性 |描述|
|----------------|-----------|
|**assemblyName**|*所需*。 如程序集的名称`System.Net`。|
|**targetFramework**|*可选*。 允许指定框架和配置文件名称 （或别名），此框架程序集适用于"net40"或"sl4"等。 使用相同的格式中所述[支持多个目标框架](../create-packages/supporting-multiple-target-frameworks.md)。|

```xml
  <frameworkAssemblies>
    <frameworkAssembly assemblyName="System.ComponentModel.DataAnnotations" targetFramework="net40" />
    <frameworkAssembly assemblyName="System.ServiceModel" targetFramework="net40" />
  </frameworkAssemblies>
```

### <a name="nugetexe-now-is-able-to-store-api-key-credentials"></a>nuget.exe 现在是能够存储 API 密钥凭据

使用 nuget.exe 命令行工具时，你现在可以使用 SetApiKey 命令来存储你的 API 密钥。 这样一来，就不必每次推送包时指定它。 有关详细信息使用 nuget.exe，保存你的 API 密钥[阅读有关发布包文档](../create-packages/publish-a-package.md)。

### <a name="package-explorer"></a>包资源管理器
包资源管理器已更新为支持 NuGet 1.2。 有关详细信息，请查看[包资源管理器发行说明](http://nuget.codeplex.com/wikipage?title=New%20features%20in%20NuGet%20Package%20Explorer%201.0)。

## <a name="other-featuresfixes"></a>其他功能/修补程序

前面的列表是最明显的许多我们实现的功能和 bug 修复。 总而言之，我们实现/修复[59 工作项](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=All&type=All&priority=All&release=NuGet%201.2&assignedTo=All&component=All&sortField=Votes&sortDirection=Descending&page=0)在此版本中。

## <a name="known-issues"></a>已知问题

* **1.2 包不兼容性**： 使用命令行工具的最新版本的包生成，nuget.exe (> 1.2) 不会使用较旧版本的 NuGet VS 外接程序 （如 1.1)。 如果遇到错误消息，表明不兼容的架构有关的内容时，您是否遇到了此错误。 请更新到最新版本的 NuGet。
* **NuGet.Server 不兼容性**： 如果您正在托管内部 NuGet 源使用 NuGet.Server 项目，你将需要使用 NuGet.Server 的最新版本更新该项目。
* **签名不匹配错误**： 如果在有关签名不匹配的消息的升级过程中遇到错误，则需要先卸载 NuGet，然后安装它。 这被列入我们[已知问题页](../release-notes/known-issues.md)提供更多详细信息。 此问题仅影响那些运行 Visual Studio 2010 SP1 和拥有的 NuGet 1.0 安装不正确签名的版本。 此版本是仅可从 CodePlex 网站在短时间内使此问题不应影响太多的人。