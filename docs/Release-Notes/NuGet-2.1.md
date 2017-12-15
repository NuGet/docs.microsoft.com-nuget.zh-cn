---
title: "NuGet 2.1 发行说明 |Microsoft 文档"
author: karann-msft
ms.author: karann-msft
manager: ghogen
ms.date: 11/11/2016
ms.topic: article
ms.prod: nuget
ms.technology: 
ms.assetid: 6f972803-9e17-43f5-b77b-973c3accf695
description: "包括已知的问题、 bug 修复、 增加的功能，以及 DCRs NuGet 2.1 的发行说明。"
keywords: "NuGet 2.1 发行说明，bug 修复的已知问题，添加了一些功能，DCRs"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: c45cfb9f6a46a1efd9fe4531602191973da66290
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/14/2017
---
# <a name="nuget-21-release-notes"></a>NuGet 2.1 发行说明

[NuGet 2.0 发行说明](../release-notes/nuget-2.0.md) | [NuGet 2.2 发行说明](../release-notes/nuget-2.2.md)

NuGet 2.1 已于 2012 年 10 月 4 日发布。

## <a name="hierarchical-nugetconfig"></a>分层 Nuget.Config
NuGet 2.1 提供更灵活地控制通过以递归方式查找的文件夹结构向上遍历 NuGet 设置`NuGet.Config`文件，然后构建中找到的所有文件组的配置。  作为示例，请考虑其中团队具有的其他内部的依赖关系的 CI 生成的内部包存储库的方案。 为单个项目的文件夹结构可能如下所示：

    C:\
    C:\myteam\
    C:\myteam\solution1
    C:\myteam\solution1\project1

此外，如果启用程序包还原了解决方案，还会存在以下文件夹：

    C:\myteam\solution1\.nuget

为了具有可用的所有项目的团队处理，同时不使它可用于每个项目的计算机上的团队的内部的程序包存储库中，我们可以创建新的 Nuget.Config 文件，并将它置于 c:\myteam 文件夹。 无法为指定每个项目的 packages 文件夹。

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

现在，我们可以看到的源通过从下 c:\myteam 如下所示的所有文件夹运行 'nuget.exe 资源' 命令添加：

![从父 nuget 配置的包源](./media/releasenotes-21-cfg-hierarchy.png)

`NuGet.Config`按以下顺序搜索了文件：

1. `.nuget\Nuget.Config`
2. 递归从项目文件夹审核到根
3. 全局`Nuget.Config`(`%appdata%\NuGet\Nuget.Config`)

配置是不是在应用*逆序*，这意味着，取决于上述排序，全局 Nuget.Config 将是首先应用、 发现 Nuget.Config 文件从根到项目文件夹依次跟通过`.nuget\Nuget.Config`。  这一点特别重要，如果你使用`<clear/>`要从配置中删除一组项的元素。

## <a name="specify-packages-folder-location"></a>指定 packages 文件夹位置
在过去，NuGet 具有托管的解决方案的根文件夹下找到的已知 packages 文件夹从解决方案的包。  对于具有很多不同的解决方案的 NuGet 包安装的开发团队而言，这可能导致同一个包安装在文件系统上的许多不同的位置。

NuGet 2.1 提供更精细地控制通过包文件夹的位置`repositoryPath`中的元素`NuGet.Config`文件。  生成的分层 Nuget.Config 支持前面的示例，假设我们想要有 C:\myteam\ 共享相同的包文件夹下的所有项目。  若要完成此操作，只需将添加以下条目到`c:\myteam\Nuget.Config`。

```xml
<configuration>
    <config>
    <add key="repositoryPath" value="C:\myteam\teampackages" />
    </config>
    ...
</configuration>
```

在此示例中，共享`Nuget.Config`文件指定无论深度创建下方 C:\myteam，每个项目的共享的包文件夹。 请注意，是否你的解决方案根目录下有现有的包文件夹，你将需要将其删除之前 NuGet 会将包放置在新位置。

## <a name="support-for-portable-libraries"></a>对可移植库的支持
[可移植库](http://msdn.microsoft.com/library/gg597391.aspx)是一项功能首次引入，可生成程序集的可在不修改不同 Microsoft 在平台上，从版本的.net Framework 对 Windows Phone 和 Xbox 甚至 Silverlight 的.NET 4360 （但在此期间，NuGet 不支持 Xbox 可移植运行库目标）。  通过扩展[打包约定](../create-packages/supporting-multiple-target-frameworks.md)framework 版本和配置文件，NuGet 2.1 现在支持可移植库，使您用于创建包来让复合 framework 和配置文件目标`lib`文件夹。

作为示例，请考虑以下可移植类库的可用目标平台。

![可移植运行库创建对话框](./media/releasenotes-21-plib.png)

构建库之后和命令`nuget.exe pack MyPortableProject.csproj`运行时，新的可移植库包文件夹结构可以看到，检查生成的 NuGet 包的内容。

![可移植运行库包布局](./media/releasenotes-21-plib-layout.png)

如你所见，可移植运行库文件夹命名约定遵循模式 '可移植 {框架 1} + {framework n}' framework 标识符遵循现有[framework 名称和版本约定](../schema/target-frameworks.md)。 名称和版本约定的一个例外是用于 Windows Phone framework 标识符中找到。  此名字对象应使用的框架名称 wp （wp7、 wp71 或 wp8）。 使用 silverlight-wp7，例如，将导致错误。

在安装时创建此文件夹结构中的包，NuGet 现在可以将其框架和配置文件规则应用到多个目标，作为文件夹名称中指定。  在 NuGet 的匹配规则后面是，"详细"目标将优先于"不太具体"的原则。  这意味着，面向特定平台的名字对象将始终为首选通过可移植的两个类型都与一个项目兼容。  此外，如果多个可移植目标符合项目，NuGet 将首选的一套支持的平台是"最靠近的"到项目引用包的一个。

## <a name="targeting-windows-8-and-windows-phone-8-projects"></a>面向 Windows 8 和 Windows Phone 8 项目
除了添加针对可移植类库项目的支持，NuGet 2.1 所提供的 Windows 8 应用商店和 Windows Phone 8 项目中，以及为 Windows 应用商店和 Windows Phone 项目将某些新常规名字对象的新框架名字对象易于管理各个将来版本的相应的平台。

对于 Windows 8 应用商店应用程序中，标识符如下所示：

|NuGet 2.0 及更早版本|NuGet 2.1|
|----------------|-----------|
|winRT45。NETCore45|Windows、 windows 8，win win8|

<br/>
对于 Windows Phone 项目，标识符如下所示：

|Phone OS|NuGet 2.0 及更早版本|NuGet 2.1
|----------------|-----------|-----------|
|Windows Phone 7|silverlight3 wp|wp，wp7，WindowsPhone WindowsPhone7|
|Windows Phone 7.5 (Mango)|silverilght4 wp71|wp71 WindowsPhone71|
|Windows Phone 8|（不支持）|wp8 WindowsPhone8|
<br/>
在所有上述更改，旧的框架名称将继续由 NuGet 2.1 完全支持。  接着，新名称应使用因为将更稳定，各个将来版本的相应的平台。 新名称将*不*是 2.1 之前的 NuGet 版本中受支持，但是，因此制定相应的计划来确定何时进行切换。

## <a name="improved-search-in-package-manager-dialog"></a>改进的搜索，在程序包管理器对话框
通过过去的若干次迭代，更改已引入到极大地改进的速度和相关性的包搜索 NuGet 库。  但是，这些改进会受限于 nuget.org Web 站点。  NuGet 2.1 使改进的搜索体验可通过 NuGet 包管理器对话框。  例如，假设你想要查找 Windows Azure Caching 预览包。  此包的合理的搜索查询可能是"Azure 缓存"。  在以前版本的包管理器对话框中，所需的包将不甚至上列出的结果的第一页。  但是，在 NuGet 2.1 中，所需的包现在显示在搜索结果顶部。

![包管理器对话框搜索](./media/releasenotes-21-vsdlg-search.png)

## <a name="force-package-update"></a>强制包更新
在 NuGet 2.1 之前 NuGet 将跳过更新包时不高的版本号。  这就产生了某些方案-尤其是对于其中团队又不想针对每个生成的数字将包版本递增的生成或 CI 方案的问题。  所需的行为是强制执行更新而不考虑。  NuGet 2.1 可解决这的重新安装标志。  例如，当尝试更新包中没有的较新的包版本以前版本的 NuGet 将导致以下：

    PM> Update-Package Moq
    No updates available for 'Moq' in project 'MySolution.MyConsole'.

进行重新安装标志，包将会更新而不管是否没有较新版本。

    PM> Update-Package Moq -Reinstall
    Successfully removed 'Moq 4.0.10827' from MySolution.MyConsole.
    Successfully uninstalled 'Moq 4.0.10827'.
    Successfully installed 'Moq 4.0.10827'.
    Successfully added 'Moq 4.0.10827' to MySolution.MyConsole.

重新安装标志证明有益的另一种情况是 framework 重定目标。 更改一个项目 （例如，为.NET 4.5 的.NET 4) 的目标框架时更新包的重新安装可更新对项目中安装的所有 NuGet 包的正确程序集的引用。

## <a name="edit-package-sources-within-visual-studio"></a>编辑 Visual Studio 中的包源
在以前版本的 NuGet 中，更新在 Visual Studio 选项对话框中所需删除然后重新添加包源从包源。  NuGet 2.1 通过支持为配置用户界面的第一类函数的更新，提高了此工作流。

![包管理器配置对话框](./media/releasenotes-21-edit-pkg-source.png)

## <a name="bug-fixes"></a>Bug 修复
NuGet 2.1 包括许多的 bug 修补程序。 有关工作的完整列表项固定在 NuGet 2.0 中，请查看[对于此版本的 NuGet 问题跟踪程序](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Fixed&type=All&priority=All&release=NuGet%202.1&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0)。
