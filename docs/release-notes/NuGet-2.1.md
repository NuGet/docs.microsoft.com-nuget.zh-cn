---
title: NuGet 2.1 发行说明
description: NuGet 2.1 的发行说明，包括已知问题、bug 修复、新增功能和 Dcr。
author: JonDouglas
ms.author: jodou
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: c44ad32c8c4018ccb517b41bffda674eef1f11f3
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/26/2021
ms.locfileid: "98777029"
---
# <a name="nuget-21-release-notes"></a>NuGet 2.1 发行说明

[NuGet 2.0 发行说明](../release-notes/nuget-2.0.md)  | [NuGet 2.2 发行说明](../release-notes/nuget-2.2.md)

NuGet 2.1 于2012年10月4日发布。

## <a name="hierarchical-nugetconfig"></a>分层 Nuget.Config

NuGet 2.1 通过以递归方式遍历用于查找文件的文件夹结构 `NuGet.Config` ，然后从所有找到的文件集生成配置，为你提供更大的灵活性。  作为示例，请考虑这样一种情况：团队具有内部包存储库，用于 CI 的其他内部依赖项的生成。 单个项目的文件夹结构可能如下所示：

```
C:\
C:\myteam\
C:\myteam\solution1
C:\myteam\solution1\project1
```

此外，如果为解决方案启用了包还原，则还会存在以下文件夹：

```
C:\myteam\solution1\.nuget
```

为了使团队的内部包存储库可用于团队处理的所有项目，而不是使其可用于计算机上的每个项目，我们可以创建一个新的 Nuget.Config 文件并将其放在 c:\myteam 文件夹中。 无法为每个项目指定包文件夹。

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

现在，我们可以通过在 c:\myteam 下的任何文件夹中运行 "nuget.exe 源" 命令来添加源，如下所示：

![从父 nuget 配置包源](./media/releasenotes-21-cfg-hierarchy.png)

`NuGet.Config` 将按以下顺序搜索文件：

1. `.nuget\Nuget.Config`
2. 从项目文件夹到根的递归遍历
3. 全局 `Nuget.Config` (`%appdata%\NuGet\Nuget.Config`) 

配置不是按 *顺序* 应用的，这意味着，根据上述排序，全局 Nuget.Config 首先应用，然后是从根到项目文件夹中发现的 Nuget.Config 文件，后跟 `.nuget\Nuget.Config` 。  如果你正在使用 `<clear/>` 元素从配置中删除一组项，则这一点特别重要。

## <a name="specify-packages-folder-location"></a>指定 "包" 文件夹位置

在过去，NuGet 从解决方案根文件夹下的已知 "包" 文件夹中管理了解决方案的包。  对于具有多个安装了 NuGet 包的不同解决方案的开发团队，这可能会导致在文件系统上的多个不同位置安装相同的包。

NuGet 2.1 通过文件中的元素，更精细地控制包文件夹的位置 `repositoryPath` `NuGet.Config` 。  根据上一个分层 Nuget.Config 支持示例，假设我们想让 C:\myteam\ 下的所有项目共享相同的包文件夹。  若要实现此目的，只需将以下项添加到 `c:\myteam\Nuget.Config` 。

```xml
<configuration>
    <config>
    <add key="repositoryPath" value="C:\myteam\teampackages" />
    </config>
    ...
</configuration>
```

在此示例中，共享 `Nuget.Config` 文件为在 C:\myteam 下创建的每个项目指定共享包文件夹，而不考虑深度。 请注意，如果你在解决方案根目录下有 "现有包" 文件夹，则需要将其删除，NuGet 才能将包置于新位置。

## <a name="support-for-portable-libraries"></a>支持可移植库

[可移植库](/dotnet/standard/cross-platform/cross-platform-development-with-the-portable-class-library) 是 .net 4 中首次引入的一项功能，使你能够构建可在不同 Microsoft 平台上无需修改的程序集（从 the.NET Framework 版本到 Silverlight 再到 Windows Phone 甚至 Xbox 360)  (）  通过扩展框架版本和配置文件的 [包约定](../create-packages/supporting-multiple-target-frameworks.md) ，NuGet 2.1 现在支持可移植库，使你能够创建具有复合框架和配置文件目标 `lib` 文件夹的包。

例如，请考虑以下可移植类库的可用目标平台。

![可移植库创建对话框](./media/releasenotes-21-plib.png)

生成库并运行该命令后 `nuget.exe pack MyPortableProject.csproj` ，可以通过检查生成的 NuGet 包的内容来查看新的可移植库包文件夹结构。

![可移植库包布局](./media/releasenotes-21-plib-layout.png)

如您所见，可移植库文件夹名称约定遵循模式 "可移植-{framework 1} + {framework n}"，其中框架标识符遵循现有的 [框架名称和版本约定](../reference/target-frameworks.md)。 用于 Windows Phone 的框架标识符中提供了名称和版本约定的一个例外。  此名字对象应使用框架名称 "wp" (wp7、wp71 或 wp8) 。 例如，使用 "wp7" 将导致错误。

安装从此文件夹结构创建的包时，NuGet 现在可以将其框架和配置文件规则应用到多个目标，如文件夹名称中所指定。  NuGet 的匹配规则的后面是 "更具体的" 目标优先于 "不太具体" 的原则。  这意味着，如果某个特定平台的名字对象均与项目兼容，则该名字对象将始终优先于可移植的名字对象。  此外，如果多个可移植目标与项目兼容，NuGet 将更喜欢其中一组受支持的平台 "最接近于引用包的项目"。

## <a name="targeting-windows-8-and-windows-phone-8-projects"></a>面向 Windows 8 和 Windows Phone 8 项目

除了添加对面向可移植库项目的支持外，NuGet 2.1 还为 Windows 8 应用商店和 Windows Phone 8 项目提供了新的框架名字对象，还为 Windows 应用商店和 Windows Phone 项目提供了一些新的常规名字对象。

对于 Windows 8 应用商店应用程序，标识符如下所示：

| NuGet 2.0 及更早版本 | NuGet 2.1 |
| ---------------- | ----------- |
| winRT45、。NETCore45 | Windows、Windows8、win、win8 |

<br/>
对于 Windows Phone 项目，标识符如下所示：

| 电话 OS | NuGet 2.0 及更早版本 | NuGet 2.1 |
| --- | --- | --- |
| Windows 7 Phone | silverlight3-wp | wp、wp7、WindowsPhone、WindowsPhone7 |
| Windows Phone 7.5 (Mango)  | silverlight4-wp71 | wp71, WindowsPhone71 |
| Windows Phone 8 | （不支持） | wp8、WindowsPhone8 |

<br/>
在上述所有更改中，NuGet 2.1 将继续完全支持旧框架名称。  前进时，应使用新的名称，因为这些名称在各个平台的未来版本中将更为稳定。 但是，在2.1 之前的版本中将 *不* 支持新的名称，因此请相应地计划何时进行切换。

## <a name="improved-search-in-package-manager-dialog"></a>改进了包管理器对话框中的搜索

在过去几个迭代中，已将更改引入到 NuGet 库，大大提高了包搜索速度和相关性。  不过，这些改进仅限于 nuget.org 网站。  NuGet 2.1 通过 "NuGet 包管理器" 对话框提供改进的搜索体验。  例如，假设你想要查找 Microsoft Azure 缓存预览版包。  此包的合理搜索查询可以是 "Azure Cache"。  在以前版本的 "包管理器" 对话框中，所需的包甚至不会在结果的第一页上列出。  但在 NuGet 2.1 中，所需的包现在会显示在搜索结果的顶部。

![程序包管理器对话框搜索](./media/releasenotes-21-vsdlg-search.png)

## <a name="force-package-update"></a>强制包更新

在 NuGet 2.1 之前，NuGet 将跳过更新包（如果版本编号不高）。  这在某些情况下引入了摩擦，特别是对于生成或 CI 方案，团队不希望在每次生成时递增包版本号。  所需行为是强制更新，而不考虑。  NuGet 2.1 通过 "重新安装" 标志来解决此情况。  例如，在尝试更新不具有更新包版本的包时，早期版本的 NuGet 会导致以下情况：

```
PM> Update-Package Moq
No updates available for 'Moq' in project 'MySolution.MyConsole'.
```

使用 "重新安装" 标志，无论是否有较新的版本，都将更新程序包。

```
PM> Update-Package Moq -Reinstall
Successfully removed 'Moq 4.0.10827' from MySolution.MyConsole.
Successfully uninstalled 'Moq 4.0.10827'.
Successfully installed 'Moq 4.0.10827'.
Successfully added 'Moq 4.0.10827' to MySolution.MyConsole.
```

重新安装标志证明好处的另一种情况是框架重新设定目标。 在更改项目的目标框架时 (例如，从 .NET 4 到 .NET 4.5) ，Update-Package 重新安装可以将对项目中安装的所有 NuGet 包的引用更新为正确的程序集。

## <a name="edit-package-sources-within-visual-studio"></a>在 Visual Studio 中编辑包源

在以前版本的 NuGet 中，从 Visual Studio 的 "选项" 对话框中更新包源需要删除并重新添加包源。  NuGet 2.1 通过支持更新作为配置用户界面的第一类函数来改进此工作流。

![程序包管理器配置对话框](./media/releasenotes-21-edit-pkg-source.png)

## <a name="bug-fixes"></a>Bug 修复

NuGet 2.1 包含多个 bug 修复。 有关 NuGet 2.0 中已修复的工作项的完整列表，请查看 [此版本的 NuGet 问题跟踪程序](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Fixed&type=All&priority=All&release=NuGet%202.1&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0)。
