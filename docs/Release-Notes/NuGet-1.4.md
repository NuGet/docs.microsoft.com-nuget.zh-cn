---
title: "NuGet 1.4 的发行说明 |Microsoft 文档"
author: karann-msft
ms.author: karann-msft
manager: ghogen
ms.date: 11/11/2016
ms.topic: article
ms.prod: nuget
ms.technology: 
description: "包括已知的问题、 bug 修复、 增加的功能，以及 DCRs NuGet 1.4 的发行说明。"
keywords: "NuGet 1.4 发行说明，bug 修复的已知问题，添加了一些功能，DCRs"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: bc0800361551b996d958e03b9cfa3d745b78e43d
ms.sourcegitcommit: b0af28d1c809c7e951b0817d306643fcc162a030
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/14/2018
---
# <a name="nuget-14-release-notes"></a>NuGet 1.4 的发行说明

[NuGet 1.3 发行说明](../release-notes/nuget-1.3.md) | [NuGet 1.5 发行说明](../release-notes/nuget-1.5.md)

NuGet 1.4 已于 2011 年 6 月 17 日发布。

## <a name="features"></a>功能

### <a name="update-package-improvements"></a>更新包改进
NuGet 1.4 引入了大量的更新包命令使其更方便地保持在相同版本的包，跨解决方案中的多个项目的改进。 例如，当升级包的最新版本时，情况非常常见，需要的所有项目与安装更新到同一 verision 该软件包。

`Update-Package`命令现在可以更轻松地：

#### <a name="update-all-packages-in-a-single-project"></a>更新单个项目中的所有包

    Update-Package -Project MvcApplication1

#### <a name="update-a-package-in-all-projects"></a>更新所有项目中的包

    Update-Package PackageId

#### <a name="update-all-packages-in-all-projects"></a>更新所有项目中的所有包

    Update-Package

#### <a name="perform-a-safe-update-on-all-packages"></a>对所有包执行的"安全"的更新
`-Safe`将使用相同的主要和次要版本组件的唯一版本升级约束为标志。 例如，如果安装程序包的版本 1.0.0，并且源中, 提供了版本 1.0.1、 1.0.2 和 1.1`-Safe`标志程序包更新到 1.0.2。 升级而不必`-Safe`标志将包升级到最新版本 1.1。

    Update-Package -Safe

### <a name="managing-packages-at-the-solution-level"></a>解决方法级别的管理包
在 NuGet 1.4 之前将包安装到多个项目已繁琐使用对话框。 它需要启动一次每个项目对话框。

NuGet 1.4 同时添加多个项目中的安装/卸载/更新包的支持。 只需启动通过右键单击解决方案并选择**管理 NuGet 包**菜单选项。

![解决方案级别管理 NuGet 包对话框](./media/manage-nuget-packages-solution-dialog.png)

请注意，在对话框的标题栏，显示的解决方案名称，不是项目的名称。
包操作现在提供操作应该应用到的项目列表的复选框的列表。

![管理 NuGet 包项目选择](./media/manage-nuget-packages-project-selection.png)

更多详细信息，请参阅主题上[解决方案管理包](../tools/package-manager-ui.md#managing-packages-for-the-solution)。

### <a name="constraining-upgrades-to-allowed-versions"></a>约束升级到允许的版本
默认情况下，运行时`Update-Package`命令对包 （或更新包使用对话框），它将更新到数据源中的最新版本。 使用用于更新所有包的新支持，可能是想要锁定到特定版本范围的包的情况。 例如，你可能事先知道你的应用程序将只适用于版本 2.* 的包，但不是 3.0 和更高版本。 为了防止意外更新为 3 的包，NuGet 1.4 增加了对约束的包可以通过手动编辑升级到的版本范围支持`packages.config`文件使用新`allowedVersions`属性。

例如，下面的示例演示如何锁定`SomePackage`包版本范围 2.0 3.0 （独占）。
`allowedVersions`属性接受使用值[版本范围格式](../reference/package-versioning.md#version-ranges-and-wildcards)。

```xml
<?xml version="1.0" encoding="utf-8"?>
<packages>
    <package id="SomePackage" version="2.1.0" allowedVersions="[2.0, 3.0)" />
</packages>
```

请注意，在 1.4 中, 锁定到特定版本范围包必须手动编辑。 我们打算 NuGet 1.5 中添加对将通过此范围的支持`Install-Package`命令。

### <a name="package-visualizer"></a>包可视化工具
新的包可视化工具，通过启动**工具** -> **库程序包管理器** -> **包可视化工具**菜单选项，使您可以轻松可视化的所有项目和解决方案内其包的依赖项。

_**重要说明：**此功能利用 DGML 支持 Visual Studio 中。在 Visual Studio Ultimate 中仅支持创建可视化效果。在 Visual Studio 高级专业版或更高，仅支持 DGML 关系图中查看。_

![包可视化工具](./media/package-visualizer.png)

### <a name="automatic-update-check-for-the-nuget-dialog"></a>NuGet 对话框的自动更新检查
某些版本的 NuGet 引入新功能通过表示`.nuspec`不理解的较旧版本的 NuGet 对话框的文件。
一个示例是在为 NuGet 1.4 中的简介[指定 framework 程序集](../release-notes/nuget-1.2.md#framework-assembly-refs)。
因此，务必使用 NuGet 的最新版本以确保可以使用利用最新功能的包。
要使到 NuGet 更新更可见，NuGet 对话框包含逻辑，以便在有可用的较新版本时突出显示。

_**请注意**： 如果只进行检查**联机**已在当前会话中选择选项卡。_

![管理 NuGet 包对话框，使用新版本可用](./media/manage-nuget-packages-update-notification.png)

若要关闭自动检查更新，请转到 NuGet 设置对话框，并取消选中**自动检查更新**。

![NuGet 设置](./media/nuget-settings.png)

此功能已实际添加在 NuGet 1.3 中，但将不可见，当然，直到对 1.3，例如 NuGet 1.4 的更新，都已变为可用。

### <a name="package-manager-dialog-improvements"></a>程序包管理器对话框改进
* **改进的菜单名**： 为清楚起见已重命名菜单选项，以便启动对话框。 菜单选项现已**管理 NuGet 包**。
* **详细信息窗格中显示最新的更新日期**: NuGet 对话框在包的详细信息窗格中显示最新的更新的日期时**联机**或**更新**选择选项卡。
* **显示的标记列表**: Nuget 对话框显示标记。

### <a name="powershell-improvements"></a>Powershell 改进
* **签名的 PowerShell 脚本**: NuGet 包括签名启用限制性更强的环境中的使用情况的 Powershell 脚本。
* **提示支持**： 的程序包管理器控制台现在支持通过提示`$host.ui.Prompt`和`$host.ui.PromptForChoice`命令。
* **包源名称**： 指定包源中使用时提供的程序包源名称支持`-Source`标志。

### <a name="nugetexe-command-line-improvements"></a>nuget.exe 命令行改进
* **自定义的 NuGet 命令**: nuget.exe 是可扩展的通过使用 MEF 的自定义命令。
* **更简单的工作流创建符号包**:`-Symbols`标志可应用到通过仅包括源中创建符号包的基于正常约定文件夹结构和`.pdb`文件夹内的文件。
* **指定多个源**:`NuGet install`命令支持指定使用分号作为分隔符或通过指定的多个源`-Source`多次。
* **代理身份验证支持**: NuGet 1.4 增加了对要求身份验证的代理后面使用 NuGet 时，会提示输入用户凭据支持。
* **nuget.exe 更新重大更改**:`-Self`标志现在是所需的 nuget.exe 自行更新。 `nuget.exe Update` 现在采用的路径`packages.config`文件并将尝试更新包。 请注意，此更新，因为它不会受到限制: * * 更新，添加、 删除项目文件中的内容。
* * 运行包内的 Powershell 脚本。

### <a name="nuget-server-support-for-pushing-packages-using-nugetexe"></a>使用 nuget.exe 的推送的包的 NuGet 服务器支持
NuGet 包括主机的简单方法[基于 NuGet 存储库的轻型 web](../hosting-packages/nuget-server.md)通过`NuGet.Server`NuGet 包。 使用 NuGet 1.4 轻型服务器支持将推送和删除使用 nuget.exe 包。
最新版本`NuGet.Server`添加一个新`appSetting`命名`apiKey`。 当省略密钥或将其留空时，将包推送到源会被禁用。 将 apiKey 设置一个值 （理想情况下为强密码） 为启用推送使用 nuget.exe 的包。

```xml
<appSettings>
    <!-- Set the value here to allow people to push/delete packages from the server.
            NOTE: This is a shared key (password) for all users. -->
    <add key="apiKey" value="" />
</appSettings>
```

### <a name="support-for-windows-phone-tools-mango-edition"></a>支持 Windows Phone 工具 Mango 版
NuGet 现在支持在 Windows Phone Tools for Mango 的候选发布版本。
目前，Windows Phone 工具不具有对 Visual Studio 扩展管理器，因此，若要安装 Windows Phone 工具的 NuGet 的支持，你可能需要下载并手动运行 VSIX。

若要卸载的 Windows Phone 工具 NuGet，请运行以下命令。

     vsixinstaller.exe /uninstall:NuPackToolsVsix.Microsoft.67e54e40-0ae3-42c5-a949-fddf5739e7a5

## <a name="bug-fixes"></a>Bug 修复
NuGet 1.4 有 88 总共工作固定的项。 71 的那些已标记为 bug。

有关工作的完整列表项固定在 NuGet 1.4，请查看[对于此版本的 NuGet 问题跟踪程序](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=All&type=All&priority=All&release=NuGet%201.4&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0)。

## <a name="bug-fixes-worth-noting"></a>值得注意的 bug 修复：

* [问题 603](http://nuget.codeplex.com/workitem/603)： 指定特定的包源时，包在不同的存储库间的依赖项是否正确解析。
* [问题 1036年](http://nuget.codeplex.com/workitem/1036)： 添加`NuGet Pack SomeProject.csproj`后无法再生成事件将导致无限循环。
* [问题 961](http://nuget.codeplex.com/workitem/961):`-Source`标志支持相对路径。

## <a name="nuget-14-update"></a>NuGet 1.4 更新
不久前 NuGet 1.4 的发行，我们发现了几个重要修复的问题。
为 1.4 此更新的特定版本号是 1.4.20615.9020。

### <a name="bug-fixes"></a>Bug 修复
* [问题 1220年](http://nuget.codeplex.com/workitem/1220)： 更新包并不执行`install.ps1` / `uninstall.ps1`多个项目时的所有项目中
* [问题 1156年](http://nuget.codeplex.com/workitem/1156)： 包管理器控制台停滞在 W2K3/XP （如果未安装 Powershell 2）
