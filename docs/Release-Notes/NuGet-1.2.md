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
# <a name="nuget-12-release-notes"></a>NuGet 1.2 发行说明

[NuGet 1.0 和 1.1 发行说明](../release-notes/nuget-1.1.md) | [NuGet 1.3 发行说明](../release-notes/nuget-1.3.md)

NuGet 1.2 已于 2011 年 3 月 30 日发布。

## <a name="new-features"></a>新增功能

### <a name="framework-profile-support"></a>框架配置文件支持

开始时，请从 NuGet 支持具有不同的框架作为目标的库。 但现在包可能包含程序集面向特定的配置文件，如 Windows Phone 配置文件。 若要针对特定框架的配置文件，追加划线后跟的配置文件缩写。 例如，若要针对 Windows Phone (又称 Windows Phone 7) 上运行的 SilverLight，你可以将程序集在 sl3 wp 文件夹如以下屏幕截图中所示。

![Framework 配置文件文件夹布局](./media/framework-profile-support.png)

您可能会问为何我们未只需选择要用作标记"wp7"。 在情况下，我们要预测，Windows Phone 7 可能在将来运行 Silverlight 的较新版本，在这种情况下你可能需要将更细致地指出哪些框架的配置文件是针对。

### <a name="automatically-add-binding-redirects"></a>自动添加绑定重定向

当使用强名称程序集安装包，NuGet 可以现在会检测项目需要绑定重定向添加到项目后，若要编译并自动将其添加顺序中的配置文件的情况。 第 3 部分 David Ebbo 的博客文章系列中的 NuGet 版本控制标题为"[通过绑定将重定向的统一](http://blog.davidebbo.com/2011/01/nuget-versioning-part-3-unification-via.html)"介绍此功能的更多详细信息的用途。

<a name="framework-assembly-refs"></a>

### <a name="specifying-framework-assembly-references-gac"></a>指定 Framework 程序集引用 (GAC)

在某些情况下，包可能依赖于.NET Framework 中的程序集中。 严格地说，它并不总是需要你的包的使用者引用 framework 程序集。 但在某些情况下，很重要，例如开发人员需要对该程序集中的类型的代码才能使用你的包。 新`frameworkAssemblies`元素，元数据元素的子元素允许你指定的一组`frameworkAssembly`指向 Framework 程序集在 gac 中的元素。 请注意主要侧重于 Framework 程序集。
这些程序集不包含在你的包中，因为它们被假定为每台计算机上作为.NET Framework 的一部分。 下表列出的属性`frameworkAssembly`元素。


|特性 |描述|
|----------------|-----------|
|**assemblyName**|*所需*。 如程序集名称`System.Net`。|
|**targetFramework**|*可选*。 允许指定的框架和配置文件的名称 （或别名），此框架程序集适用于如"net40"或"sl4"。 使用相同的格式中所述[支持多个目标框架](../create-packages/supporting-multiple-target-frameworks.md)。|

```xml
  <frameworkAssemblies>
    <frameworkAssembly assemblyName="System.ComponentModel.DataAnnotations" targetFramework="net40" />
    <frameworkAssembly assemblyName="System.ServiceModel" targetFramework="net40" />
  </frameworkAssemblies>
```

### <a name="nugetexe-now-is-able-to-store-api-key-credentials"></a>nuget.exe 现在是能够存储 API 密钥凭据

使用 nuget.exe 命令行工具时，你现在可以使用 SetApiKey 命令来存储你的 API 密钥。 这样一来，你不需要每次推送包时指定它。 有关详细信息使用 nuget.exe，保存你的 API 密钥[读取该文档描述有关发布包](../create-packages/publish-a-package.md)。

### <a name="package-explorer"></a>包资源管理器
包资源管理器已更新为支持 NuGet 1.2。 有关详细信息，请参阅[包资源管理器发行说明](http://nuget.codeplex.com/wikipage?title=New%20features%20in%20NuGet%20Package%20Explorer%201.0)。

## <a name="other-featuresfixes"></a>其他功能/修补程序

前面的列表是最为明显的许多我们实现的功能和我们解决的 bug。 总之，我们实现/修复[59 工作项](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=All&type=All&priority=All&release=NuGet%201.2&assignedTo=All&component=All&sortField=Votes&sortDirection=Descending&page=0)在此版本中。

## <a name="known-issues"></a>已知问题

* **1.2 包不兼容性**： 用命令行工具的最新版本的包生成的 nuget.exe (> 1.2) 不会使用较旧版本的 NuGet VS 外接程序 （如 1.1)。 如果遇到错误消息，表明一些有关不兼容的架构时，你是否遇到了此错误。 请更新到最新版本的 NuGet。
* **NuGet.Server 不兼容性**： 如果你要托管源使用 NuGet.Server 项目内部 NuGet，你将需要 NuGet.Server 为最新版本更新该项目。
* **签名不匹配错误**： 如果有关签名不匹配的消息升级期间遇到错误，则需要首先卸载 NuGet，然后安装它。 这被列入我们[已知问题页](../release-notes/known-issues.md)它提供更多详细信息。 此问题仅影响那些运行 Visual Studio 2010 SP1，并具有 NuGet 1.0 安装不正确签名的版本。 此版本已仅可从 CodePlex 网站在短时间内使此问题不应影响太多的人。