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
# <a name="nuget-12-release-notes"></a>NuGet 1.2 发行说明

[NuGet 1.0 和1.1 发行说明](../release-notes/nuget-1.1.md)  | [NuGet 1.3 发行说明](../release-notes/nuget-1.3.md)

NuGet 1.2 于年3月 30 2011 日发布。

## <a name="new-features"></a>新功能

### <a name="framework-profile-support"></a>框架配置文件支持

从开始，NuGet 支持的库以不同的框架为目标。 但现在，包可能包含面向特定配置文件（如 Windows Phone 配置文件）的程序集。 若要以框架的特定配置文件为目标，请追加一条短划线，后跟配置文件缩写。 例如，若要将 (Windows Phone 上运行的 SilverLight 定位 Windows Phone 7) ，可以将程序集放入 sl3 wp 文件夹中，如以下屏幕截图所示。

![框架配置文件文件夹布局](./media/framework-profile-support.png)

您可能会问为什么我们不只选择使用 "wp7" 作为名字对象。 在部分中，我们将预测到 Windows Phone 7 以后可能会运行较新版本的 Silverlight，在这种情况下，你可能需要更具体地了解要针对哪个框架配置文件。

### <a name="automatically-add-binding-redirects"></a>自动添加绑定重定向

当安装具有强名称程序集的包时，NuGet 现在可以检测项目需要将绑定重定向添加到配置文件中的情况，以便项目自动编译和添加它们。 "David Ebbo 的博客文章系列" 中的第3部分 "NuGet 版本管理" "[通过绑定重定向](http://blog.davidebbo.com/2011/01/nuget-versioning-part-3-unification-via.html)" 包含此功能的更多详细信息。

<a name="framework-assembly-refs"></a>

### <a name="specifying-framework-assembly-references-gac"></a>指定 Framework 程序集引用 (GAC) 

在某些情况下，包可能依赖于 .NET Framework 中的程序集。 严格地说，包的使用者并非始终需要引用框架程序集。 但在某些情况下，这一点很重要，例如当开发人员需要针对该程序集中的类型编写代码时，才使用您的包。 新 `frameworkAssemblies` 元素（metadata 元素的子元素）允许您指定一组 `frameworkAssembly` 指向 GAC 中的框架程序集的元素。 请注意框架程序集的重点。
这些程序集不包含在包中，因为它们被假定为在每台计算机上作为 .NET Framework 的一部分。 下表列出了元素的属性 `frameworkAssembly` 。


|属性 |描述|
|----------------|-----------|
|**assemblyName**|“必需”。 程序集的名称，例如 `System.Net` 。|
|**targetFramework**|可选。 允许指定此框架程序集应用到的框架和配置文件名称 (或别名) ，如 "net40" 或 "sl4"。 使用的格式与 [支持多个目标框架](../create-packages/supporting-multiple-target-frameworks.md)中所述的格式相同。|

```xml
  <frameworkAssemblies>
    <frameworkAssembly assemblyName="System.ComponentModel.DataAnnotations" targetFramework="net40" />
    <frameworkAssembly assemblyName="System.ServiceModel" targetFramework="net40" />
  </frameworkAssemblies>
```

### <a name="nugetexe-now-is-able-to-store-api-key-credentials"></a>nuget.exe 现在可以存储 API 密钥凭据

使用 nuget.exe 命令行工具时，现在可以使用 SetApiKey 命令来存储 API 密钥。 这样，每次推送包时都无需指定它。 有关使用 nuget.exe 保存 API 密钥的详细信息，请 [阅读有关发布包的文档](../nuget-org/publish-a-package.md)。

### <a name="package-explorer"></a>包资源管理器
包资源管理器已更新为支持 NuGet 1.2。 有关详细信息，请参阅 [包资源管理器发行说明](http://nuget.codeplex.com/wikipage?title=New%20features%20in%20NuGet%20Package%20Explorer%201.0)。

## <a name="other-featuresfixes"></a>其他功能/修补程序

之前的列表是我们实现的许多功能和修复的 bug 中最明显的一项。 毕竟，我们在此版本中实现/修复了 [59 工作项](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=All&type=All&priority=All&release=NuGet%201.2&assignedTo=All&component=All&sortField=Votes&sortDirection=Descending&page=0) 。

## <a name="known-issues"></a>已知问题

* **1.2 包不兼容**：使用最新版本的命令行工具生成的包，nuget.exe ( # A0 1.2) 将不适用于其他版本的 NuGet VS 外接程序 (例如 1.1) 。 如果遇到一条错误消息，指出不兼容的架构，则会遇到此错误。 请将 NuGet 更新到最新版本。
* **NuGet。服务器不兼容性**：如果你要使用 nuget.exe 服务器项目托管内部 nuget 源，则需要使用最新版本的 nuget 更新该项目。
* **签名不匹配错误**：如果在升级过程中遇到与签名不匹配有关的消息，则需要先卸载 NuGet，然后再进行安装。 这会在我们的 " [已知问题" 页](../release-notes/known-issues.md) 中列出，其中提供了更多详细信息。 此问题只会影响那些运行 Visual Studio 2010 SP1 的版本，并且安装的 NuGet 1.0 版本未正确签名。 此版本仅在 CodePlex 网站中提供一小段时间，因此，此问题不会影响太多人。