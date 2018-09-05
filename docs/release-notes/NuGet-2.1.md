---
title: NuGet 2.1 发行说明
description: 包括已知的问题、 bug 修复、 新增的功能和 Dcr NuGet 2.1 发行说明。
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: fd6dadc7968991c77c1b06a6a261415355b2fd73
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/04/2018
ms.locfileid: "43548592"
---
# <a name="nuget-21-release-notes"></a>NuGet 2.1 发行说明

[NuGet 2.0 发行说明](../release-notes/nuget-2.0.md) | [NuGet 2.2 发行说明](../release-notes/nuget-2.2.md)

NuGet 2.1 已于 2012 年 10 月 4 日发布。

## <a name="hierarchical-nugetconfig"></a>分层 Nuget.Config

NuGet 2.1 为您提供了更灵活地控制通过以递归方式查找的文件夹结构向上遍历的 NuGet 设置`NuGet.Config`文件，然后生成中找到的所有文件组的配置。  作为示例，请考虑其中一个团队具有的其他内部的依赖项的 CI 生成的内部包存储库的方案。 单个项目的文件夹结构可能类似以下形式：

    C:\
    C:\myteam\
    C:\myteam\solution1
    C:\myteam\solution1\project1

此外，如果解决方案启用了包还原，也将存在以下文件夹：

    C:\myteam\solution1\.nuget

为了使团队的内部包存储库可用的所有项目的团队处理，同时不使它可为每个项目的计算机上，我们可以创建一个新的 Nuget.Config 文件，并将其放在 c:\myteam 文件夹中。 无法为指定每个项目的 packages 文件夹。

```xml
<configuration>
    <packageSources>
    <add key="Official project team source" value="http://teamserver/api/v2/" />
    </packageSources>
    <disabledPackageSources />
    <activePackageSource>
    <add key="Official project team source" value="http://teamserver/api/v2/" />
    </activePackageSource>
</configuration>
```

现在，我们可以看到源被添加，如下所示的 c:\myteam 下任何文件夹中运行 nuget.exe 源命令：

![从父 nuget 配置包源](./media/releasenotes-21-cfg-hierarchy.png)

`NuGet.Config` 按以下顺序搜索了文件：

1. `.nuget\Nuget.Config`
2. 递归遍历到根项目文件夹中
3. 全局`Nuget.Config`(`%appdata%\NuGet\Nuget.Config`)

配置是不是应用于*反转顺序*，也就是说，取决于上述顺序，全局 Nuget.Config 将是首先应用后, 跟已发现的 Nuget.Config 文件从根项目文件夹，然后是通过`.nuget\Nuget.Config`。  这一点特别重要，如果您使用的`<clear/>`要从配置中删除一组项的元素。

## <a name="specify-packages-folder-location"></a>指定包文件夹位置

在过去，NuGet 具有托管解决方案的根文件夹下找到已知的包文件夹中的解决方案包。  对于具有许多不同的解决方案的已安装的 NuGet 包的开发团队，这可能导致在文件系统上的多个不同位置中安装在同一包中。

NuGet 2.1 提供了更精细地控制通过包文件夹的位置`repositoryPath`中的元素`NuGet.Config`文件。  生成的 Nuget.Config 的层次结构支持以上一个示例，假设我们想要拥有 C:\myteam\ 共享相同的包文件夹下的所有项目。  若要完成此操作，只需添加到以下一项`c:\myteam\Nuget.Config`。

```xml
<configuration>
    <config>
    <add key="repositoryPath" value="C:\myteam\teampackages" />
    </config>
    ...
</configuration>
```

在此示例中，共享`Nuget.Config`文件指定用于创建下方 C:\myteam，而不考虑深度的每个项目的共享的包文件夹。 请注意，是否解决方案根目录下有一个现有的包文件夹，您需要 NuGet 会将包放置在新位置之前将其删除。

## <a name="support-for-portable-libraries"></a>对可移植库的支持

[可移植库](/dotnet/standard/cross-platform/cross-platform-development-with-the-portable-class-library)是首次随.NET 4 中，可用于生成可以无需修改即可在不同的 Microsoft 平台，从.net Framework 对 Windows Phone 和甚至 Xbox silverlight 版本上的程序集的功能360 （尽管在此期间，NuGet 不支持 Xbox 可移植库目标）。  通过扩展[打包约定](../create-packages/supporting-multiple-target-frameworks.md)framework 版本和配置文件，NuGet 2.1 现在支持可移植库，使您创建具有复合框架和配置文件目标的包`lib`文件夹。

作为示例，请考虑以下可移植库的可用目标平台。

![可移植库创建对话框](./media/releasenotes-21-plib.png)

构建库后，该命令`nuget.exe pack MyPortableProject.csproj`运行时，新的可移植库包文件夹结构可以通过检查生成的 NuGet 包的内容发现。

![可移植库包布局](./media/releasenotes-21-plib-layout.png)

正如您所看到的可移植库文件夹名称约定遵循的模式可移植的 {framework 1} + {framework n} 的框架标识符遵循现有[framework 名称和版本约定](../reference/target-frameworks.md)。 用于 Windows Phone 的框架标识符中找到了一个异常的名称和版本的约定。  此名字对象应使用的框架名称 wp （wp7、 wp71 或 wp8）。 使用 silverlight-wp7，例如，将导致错误。

在安装时创建此文件夹结构中的包，NuGet 现在可以将其框架和配置文件规则应用于多个目标，文件夹名称中指定。  NuGet 的匹配规则是，"更多特定"目标将优先于"不太特定"的原则。  这意味着，面向特定平台的名字对象将始终是首选通过可移植的如果它们都与一个项目兼容。  此外，如果多个可移植目标兼容使用项目，NuGet 将首选支持的平台设置为"最靠近"项目引用包。

## <a name="targeting-windows-8-and-windows-phone-8-projects"></a>面向 Windows 8 和 Windows Phone 8 项目

除了添加支持面向可移植库项目，NuGet 2.1 所提供的 Windows 8 应用商店和 Windows Phone 8 项目，以及为 Windows 应用商店和 Windows Phone 项目将一些新常规名字对象的新框架名字对象更轻松地跨各自的平台的未来版本管理。

对于 Windows 8 应用商店应用程序中，标识符如下所示：

| NuGet 2.0 及更早版本 | NuGet 2.1 |
| ---------------- | ----------- |
| winRT45, .NETCore45 | Windows，Windows8，win win8 |

<br/>
对于 Windows Phone 项目，标识符如下所示：

| Phone 操作系统 | NuGet 2.0 及更早版本 | NuGet 2.1 |
| --- | --- | --- |
| Windows Phone 7 | silverlight3 wp | wp wp7，WindowsPhone WindowsPhone7 |
| Windows Phone 7.5 (Mango) | silverlight4 wp71 | wp71 WindowsPhone71 |
| Windows Phone 8 | （不支持） | wp8 WindowsPhone8 |

<br/>
在所有上述更改，将继续得到的 NuGet 2.1 完全支持旧的框架名称。  展望未来，新的名称应将更稳定，将来版本的各自的平台。 新名称将*不*是支持在 2.1 之前的 NuGet 版本，但是，因此相应地规划时切换。

## <a name="improved-search-in-package-manager-dialog"></a>在包管理器对话框改进的搜索

在过去的几个迭代，引入了更改到 NuGet 库，大大提高速度和包搜索相关性。  但是，这些改进的限制为 nuget.org Web 站点。  NuGet 2.1 可通过 NuGet 包管理器对话框提供改进的搜索体验。  例如，假设您想要找到 Windows Azure Caching 预览包。  此包的合理的搜索查询可能是"Azure 缓存"。  在以前版本的包管理器对话框中，所需的包将不甚至会列出结果的第一页。  但是，在 NuGet 2.1 所需的包现在显示在搜索结果顶部。

![包管理器对话框中搜索](./media/releasenotes-21-vsdlg-search.png)

## <a name="force-package-update"></a>强制执行包更新

在 NuGet 2.1 之前 NuGet 将跳过更新包时出现不高的版本号。  这就产生了某些情况下-尤其是对于生成或 CI 方案，团队没有不需要每次生成数字将包版本递增的冲突。  所需的行为是强制进行更新，而不考虑。  NuGet 2.1 可解决这的重新安装标志。  例如，尝试更新不具有最新包版本的包时 NuGet 的早期版本将导致以下：

    PM> Update-Package Moq
    No updates available for 'Moq' in project 'MySolution.MyConsole'.

通过重新安装标志，包将更新无论是否还有一个较新版本。

    PM> Update-Package Moq -Reinstall
    Successfully removed 'Moq 4.0.10827' from MySolution.MyConsole.
    Successfully uninstalled 'Moq 4.0.10827'.
    Successfully installed 'Moq 4.0.10827'.
    Successfully added 'Moq 4.0.10827' to MySolution.MyConsole.

重新安装标志证明有益的另一种方案是 framework 重定目标。 更改 （例如，从.NET 4 中为.NET 4.5)，一个项目的目标框架时更新包的重新安装可以更新到正确的程序集的所有项目中安装的 NuGet 包的引用。

## <a name="edit-package-sources-within-visual-studio"></a>编辑 Visual Studio 中的包源

在以前版本的 NuGet，正在更新从 Visual Studio 选项对话框所需删除并重新添加包源中的包源。  NuGet 2.1 通过支持更新作为配置用户界面的第一类函数来改进此工作流。

![包管理器配置对话框](./media/releasenotes-21-edit-pkg-source.png)

## <a name="bug-fixes"></a>Bug 修复

NuGet 2.1 包括许多 bug 修复。 有关工作的完整列表项中已修复 NuGet 2.0，请查看[对于此版本的 NuGet 问题跟踪程序](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Fixed&type=All&priority=All&release=NuGet%202.1&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0)。
