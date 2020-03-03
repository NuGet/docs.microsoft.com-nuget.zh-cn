---
title: NuGet 1.4 发行说明
description: NuGet 1.4 的发行说明，包括已知问题、bug 修复、新增功能和 Dcr。
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 4b31c02b9251d6d45d952fdf8b111493495d57ba
ms.sourcegitcommit: c81561e93a7be467c1983d639158d4e3dc25b93a
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/02/2020
ms.locfileid: "78230702"
---
# <a name="nuget-14-release-notes"></a>NuGet 1.4 发行说明

[Nuget 1.3 发行说明](../release-notes/nuget-1.3.md) | [Nuget 1.5 发行说明](../release-notes/nuget-1.5.md)

NuGet 1.4 于2011年6月17日发布。

## <a name="features"></a>功能

### <a name="update-package-improvements"></a>更新-包改进
NuGet 1.4 为更新包命令引入了很多改进，使解决方案中多个项目的包保持同一版本。 例如，将包升级到最新版本时，需要将安装该程序包的所有项目更新为相同的 verision，这种情况很常见。

`Update-Package` 命令现在可以更轻松地执行以下操作：

#### <a name="update-all-packages-in-a-single-project"></a>更新单个项目中的所有包

    Update-Package -Project MvcApplication1

#### <a name="update-a-package-in-all-projects"></a>更新所有项目中的包

    Update-Package PackageId

#### <a name="update-all-packages-in-all-projects"></a>更新所有项目中的所有包

    Update-Package

#### <a name="perform-a-safe-update-on-all-packages"></a>在所有包上执行 "安全" 更新
`-Safe` 标志仅将升级限制为具有相同的主要版本和次要版本组件的版本。 例如，如果安装了包的1.0.0 版，并且源中提供了版本1.0.1、1.0.2 和1.1，则 `-Safe` 标志会将包更新到1.0.2。 如果升级时没有 `-Safe` 标志，会将包升级到最新版本1.1。

    Update-Package -Safe

### <a name="managing-packages-at-the-solution-level"></a>在解决方案级别管理包
在 NuGet 1.4 之前，使用对话框将包安装到多个项目中会很繁琐。 每个项目都需要启动一次此对话。

NuGet 1.4 添加了对在多个项目中同时安装/卸载/更新包的支持。 只需通过右键单击解决方案并选择 "**管理 NuGet 包**" 菜单选项即可启动。

![解决方案级别 "管理 NuGet 包" 对话框](./media/manage-nuget-packages-solution-dialog.png)

请注意，在对话框的标题栏中显示解决方案的名称，而不是项目的名称。
包操作现在提供了一个复选框列表，其中包含操作应应用到的项目的列表。

![管理 NuGet 包项目选择](./media/manage-nuget-packages-project-selection.png)

有关更多详细信息，请参阅有关[管理解决方案的包](../consume-packages/install-use-packages-visual-studio.md#manage-packages-for-the-solution)的主题。

### <a name="constraining-upgrades-to-allowed-versions"></a>限制升级到允许的版本
默认情况下，在包上运行 `Update-Package` 命令（或使用对话框更新包）时，它将更新为源中的最新版本。 使用更新所有包的新支持，可能需要将包锁定到特定的版本范围。 例如，你可能事先知道，你的应用程序将仅适用于包的版本 2. *，而不是3.0 和更高版本。 为了防止意外将包更新到3，NuGet 1.4 添加了对约束可升级到的版本范围的支持，方法是使用新的 `allowedVersions` 属性手动编辑 `packages.config` 文件。

例如，下面的示例演示如何将 `SomePackage` 包锁定为 2.0-3.0 （独占）版本。
`allowedVersions` 属性接受使用[版本范围格式](../concepts/package-versioning.md#version-ranges)的值。

```xml
<?xml version="1.0" encoding="utf-8"?>
<packages>
    <package id="SomePackage" version="2.1.0" allowedVersions="[2.0, 3.0)" />
</packages>
```

请注意，在1.4 中，必须手动编辑将包锁定到特定的版本范围。 在 NuGet 1.5 中，我们计划添加对通过 `Install-Package` 命令放置此范围的支持。

### <a name="package-visualizer"></a>包可视化工具
通过 "**工具**" -> **库包管理器**" -> **包可视化**工具" 菜单选项启动的新包可视化工具，可以轻松地将所有项目及其包依赖关系可视化到解决方案中。

_**重要说明：** 此功能利用 Visual Studio 中的 DGML 支持。仅 Visual Studio Ultimate 支持创建可视化效果。仅 Visual Studio Premium 或更高版本中支持查看 DGML 关系图。_

![包可视化工具](./media/package-visualizer.png)

### <a name="automatic-update-check-for-the-nuget-dialog"></a>NuGet 对话框的自动更新检查
某些版本的 NuGet 引入通过 `.nuspec` 文件表示的新功能，这些新功能在 NuGet 对话框的较旧版本中不被理解。
其中一个示例是 NuGet 1.4 中用于[指定框架程序集](../release-notes/nuget-1.2.md#framework-assembly-refs)的简介。
因此，请务必使用最新版本的 NuGet，以确保可以使用包利用最新功能。
为了更直观地更新 NuGet，NuGet 对话框包含了在更新版本可用时要突出显示的逻辑。

_**注意**：仅当在当前会话中选择了 "**联机**" 选项卡时，才进行此检查。_

![新版本可用的 "管理 NuGet 包" 对话框](./media/manage-nuget-packages-update-notification.png)

若要禁用自动检查更新，请转到 NuGet 设置对话框，并取消选中 "**自动检查更新**"。

![NuGet 设置](./media/nuget-settings.png)

此功能实际上已添加到 NuGet 1.3 中，但在更新到1.3 （如 NuGet 1.4）之前，将不会显示此功能。

### <a name="package-manager-dialog-improvements"></a>程序包管理器对话框改进
* **菜单名称改进**：为了清楚起见，已重命名用于启动对话框的菜单选项。 菜单选项现在为 "**管理 NuGet 包**"。
* **详细信息窗格显示最新更新日期**：在选择 "**联机**" 或 "**更新**" 选项卡时，NuGet 对话框显示包的详细信息窗格中的最新更新的日期。
* **显示的标记列表**： Nuget 对话框显示标记。

### <a name="powershell-improvements"></a>Powershell 改进
* **已签名的 powershell 脚本**： NuGet 包括已签名的 powershell 脚本，以实现更严格的环境中的使用。
* **提示支持**：程序包管理器控制台现在支持通过 `$host.ui.Prompt` 和 `$host.ui.PromptForChoice` 命令发出提示。
* **包源名称**：在使用 `-Source` 标志指定包源时支持提供包源的名称。

### <a name="nugetexe-command-line-improvements"></a>nuget.exe 命令行改进
* **Nuget 自定义命令**：使用 MEF 通过自定义命令可扩展 nuget.exe。
* **更简单地创建符号包的工作流**： `-Symbols` 标志可应用于基于标准的基于约定的文件夹结构，该结构仅通过在文件夹中包含源和 `.pdb` 文件来创建符号包。
* **指定多个源**： `NuGet install` 命令支持使用分号作为分隔符或多次指定 `-Source` 来指定多个源。
* **代理身份验证支持**：在需要身份验证的代理后面使用 nuget 时，nuget 1.4 添加了对提示用户凭据的支持。
* **Nuget.exe 更新重大更改**：现在，nuget.exe 需要 `-Self` 标志才能更新自身。 `nuget.exe Update` 现在采用 `packages.config` 文件的路径，并将尝试更新包。 请注意，此更新有限，因为它不会： * * 更新、添加、删除项目文件中的内容。
* * 在包中运行 Powershell 脚本。

### <a name="nuget-server-support-for-pushing-packages-using-nugetexe"></a>NuGet 服务器支持使用 nuget.exe 推送包
NuGet 包含一种通过 `NuGet.Server` NuGet 包来托管[基于轻型 web 的 nuget 存储库](../hosting-packages/nuget-server.md)的简单方式。 使用 NuGet 1.4，轻型服务器支持使用 nuget.exe 推送和删除包。
最新版本的 `NuGet.Server` 添加名为 `apiKey`的新 `appSetting`。 如果省略该密钥或将其保留为空，则会禁用向该源推送包。 将 apiKey 设置为值（理想情况下为强密码）可启用使用 nuget.exe 推送包。

```xml
<appSettings>
    <!-- Set the value here to allow people to push/delete packages from the server.
            NOTE: This is a shared key (password) for all users. -->
    <add key="apiKey" value="" />
</appSettings>
```

### <a name="support-for-windows-phone-tools-mango-edition"></a>支持 Windows Phone Tools Mango Edition
Mango 的 Windows Phone 工具的候选发布版本中现在支持 NuGet。
目前，Windows Phone 工具不支持 Visual Studio 扩展管理器，因此若要为 Windows Phone 工具安装 NuGet，你可能需要手动下载并运行该 VSIX。

若要卸载 Windows Phone 工具的 NuGet，请运行以下命令。

     vsixinstaller.exe /uninstall:NuPackToolsVsix.Microsoft.67e54e40-0ae3-42c5-a949-fddf5739e7a5

## <a name="bug-fixes"></a>Bug 修复
NuGet 1.4 总共修复了88个工作项。 71标记为 bug。

有关 NuGet 1.4 中已修复的工作项的完整列表，请查看[此版本的 NuGet 问题跟踪程序](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=All&type=All&priority=All&release=NuGet%201.4&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0)。

## <a name="bug-fixes-worth-noting"></a>需要注意的 Bug 修复：

* [问题 603](http://nuget.codeplex.com/workitem/603)：指定特定包源时，跨不同存储库的包依赖项解析正确。
* [问题 1036](http://nuget.codeplex.com/workitem/1036)：将 `NuGet Pack SomeProject.csproj` 添加到生成后事件不再导致无限循环。
* [问题 961](http://nuget.codeplex.com/workitem/961)： `-Source` 标志支持相对路径。

## <a name="nuget-14-update"></a>NuGet 1.4 更新
在 NuGet 1.4 发布之后不久，我们发现了一些很重要的问题需要解决。
此更新到1.4 的特定版本号为1.4.20615.9020。

### <a name="bug-fixes"></a>Bug 修复
* [问题 1220](http://nuget.codeplex.com/workitem/1220)：如果有多个项目，则更新包不会在所有项目中执行 `install.ps1`/`uninstall.ps1`
* [问题 1156](http://nuget.codeplex.com/workitem/1156)：程序包管理器控制台在 W2K3/XP 上停滞（未安装 Powershell 2 时）
