---
title: NuGet 1.4 的发行说明
description: 包括已知的问题、 bug 修复、 新增的功能和 Dcr NuGet 1.4 的发行说明。
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 3f4d712f83ea108a82a1bc4910c2a721a8c24d51
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/04/2018
ms.locfileid: "43550626"
---
# <a name="nuget-14-release-notes"></a>NuGet 1.4 的发行说明

[NuGet 1.3 发行说明](../release-notes/nuget-1.3.md) | [NuGet 1.5 发行说明](../release-notes/nuget-1.5.md)

NuGet 1.4 已于 2011 年 6 月 17 日发布。

## <a name="features"></a>功能

### <a name="update-package-improvements"></a>更新包改进
NuGet 1.4 引入了大量改进，使其更容易地跨多个项目在解决方案中相同的版本将包的更新 Package 命令。 例如，当升级到最新版本的包，是很常见，要想要安装更新到相同 verision 该程序包的所有项目。

`Update-Package`命令现在可以更容易：

#### <a name="update-all-packages-in-a-single-project"></a>更新单个项目中的所有包

    Update-Package -Project MvcApplication1

#### <a name="update-a-package-in-all-projects"></a>更新所有项目中的包

    Update-Package PackageId

#### <a name="update-all-packages-in-all-projects"></a>更新所有项目中的所有包

    Update-Package

#### <a name="perform-a-safe-update-on-all-packages"></a>对所有包执行的"安全"更新
`-Safe`标志限制升级到与相同的主要和次要版本组件的唯一版本。 例如，如果已安装的包的版本 1.0.0，并且在源中有版本 1.0.1、 1.0.2 和 1.1`-Safe`标志将程序包更新到 1.0.2。 升级而`-Safe`标志将包升级到最新版本 1.1。

    Update-Package -Safe

### <a name="managing-packages-at-the-solution-level"></a>在解决方案级别的管理包
在 NuGet 1.4 之前包安装到多个项目是件非常麻烦的使用对话框。 它需要启动一次每个项目对话框。

NuGet 1.4 同时添加多个项目中的安装/卸载/更新包的支持。 只需启动通过右键单击解决方案并选择**管理 NuGet 包**菜单选项。

![解决方案级别管理 NuGet 包对话框](./media/manage-nuget-packages-solution-dialog.png)

请注意，在对话框的标题栏中，显示解决方案的名称，不是项目的名称。
包操作现在提供的操作应该应用到的项目列表的复选框的列表。

![管理 NuGet 包项目选择](./media/manage-nuget-packages-project-selection.png)

更多详细信息，请参阅主题上[解决方案的管理包](../tools/package-manager-ui.md#managing-packages-for-the-solution)。

### <a name="constraining-upgrades-to-allowed-versions"></a>约束升级到允许的版本
默认情况下，运行时`Update-Package`命令包 （或更新包使用对话框），它将更新为在源中的最新版本。 用于更新所有包的新支持，可能想要锁定到特定的版本范围的包的情况。 例如，您可能事先知道您的应用程序将仅用于版本 2.* 的包，但不是 3.0 及更高版本。 为了防止意外更新为 3 的包，NuGet 1.4 添加了用于约束的包可以通过手动编辑升级到的版本范围的支持`packages.config`文件中使用新`allowedVersions`属性。

例如，下面的示例演示如何锁定`SomePackage`包版本 2.0-3.0 （独占） 的范围。
`allowedVersions`属性接受的值使用[版本范围格式](../reference/package-versioning.md#version-ranges-and-wildcards)。

```xml
<?xml version="1.0" encoding="utf-8"?>
<packages>
    <package id="SomePackage" version="2.1.0" allowedVersions="[2.0, 3.0)" />
</packages>
```

请注意，在 1.4，锁定到特定的版本范围的包必须手动编辑。 我们打算在 NuGet 1.5 中添加对将通过此范围的支持`Install-Package`命令。

### <a name="package-visualizer"></a>包可视化工具
新的包可视化工具，通过启动**工具** -> **库程序包管理器** -> **包可视化工具**菜单选项可轻松地直观显示所有项目和解决方案及其包依赖关系。

_**重要说明：** 此功能在 Visual Studio 中充分利用 DGML 支持。仅支持 Visual Studio Ultimate 中创建可视化效果。查看 DGML 关系图仅支持在 Visual Studio 高级专业版或更高。_

![包可视化工具](./media/package-visualizer.png)

### <a name="automatic-update-check-for-the-nuget-dialog"></a>NuGet 对话框的自动更新检查
某些版本的 NuGet 中引入新功能通过表示`.nuspec`不理解的较旧版本的 NuGet 对话框的文件。
例如，对于 NuGet 1.4 中的引入[指定 framework 程序集](../release-notes/nuget-1.2.md#framework-assembly-refs)。
因此，务必使用 NuGet 的最新版本以确保你可以使用利用最新功能的包。
要使到 NuGet 更新更可见，NuGet 对话框包含逻辑，以便突出显示的较新版本时可用。

_**请注意**： 如果在仅进行检查**Online**当前会话中所选选项卡。_

![管理 NuGet 包对话框，使用新版本可用](./media/manage-nuget-packages-update-notification.png)

若要关闭自动检查更新，请转到 NuGet 设置对话框，并取消选中**自动检查更新**。

![NuGet 设置](./media/nuget-settings.png)

此功能实际上已添加在 NuGet 1.3 中，但会显示，当然，直到对 1.3，例如 NuGet 1.4 的更新，提供。

### <a name="package-manager-dialog-improvements"></a>包管理器对话框改进
* **改进的菜单名称**： 为了清楚起见已重命名的菜单选项来启动的对话框。 菜单选项现**管理 NuGet 包**。
* **详细信息窗格中显示了最新的更新日期**: NuGet 对话框在包的详细信息窗格中显示的最新的更新日期时**Online**或**更新**选择选项卡。
* **显示标记列表**: Nuget 对话框显示标记。

### <a name="powershell-improvements"></a>Powershell 改进
* **签名的 PowerShell 脚本**: NuGet 包含签名的 Powershell 脚本启用限制性更强的环境中的使用情况。
* **提示支持**： 的程序包管理器控制台中现在支持通过提示`$host.ui.Prompt`和`$host.ui.PromptForChoice`命令。
* **包源名称**： 指定包源使用时提供的包源名称支持`-Source`标志。

### <a name="nugetexe-command-line-improvements"></a>nuget.exe 命令行的改进
* **NuGet 自定义命令**: nuget.exe 是可扩展的通过使用 MEF 的自定义命令。
* **更简单的工作流创建符号包**:`-Symbols`标志可以应用于正常约定基于文件夹结构创建符号包仅包括源和`.pdb`文件夹中的文件。
* **指定多个源**:`NuGet install`命令支持指定多个源使用分号作为分隔符或通过指定`-Source`多次。
* **代理身份验证支持**: NuGet 1.4 增加了对要求身份验证的代理后面使用 NuGet 时，会提示输入用户凭据支持。
* **nuget.exe 更新重大更改**:`-Self`标志是现在所需的 nuget.exe 自行更新。 `nuget.exe Update` 现在只需在路径中`packages.config`文件，并将尝试更新包。 请注意此更新的局限性在于它不会: * * 更新，请添加、 删除项目文件中的内容。
* * 运行的包中的 Powershell 脚本。

### <a name="nuget-server-support-for-pushing-packages-using-nugetexe"></a>使用 nuget.exe 推送包的 NuGet 服务器支持
NuGet 包括主机的简单方法[轻型 web 基于 NuGet 存储库](../hosting-packages/nuget-server.md)通过`NuGet.Server`NuGet 包。 与 NuGet 1.4 轻型服务器支持将推送和删除包使用 nuget.exe。
最新版`NuGet.Server`添加一个新`appSetting`名为`apiKey`。 当省略密钥或将其留空时，将包推送到源被禁用。 设置 apiKey 的值 （理想情况下为强密码），使用 nuget.exe 推送包。

```xml
<appSettings>
    <!-- Set the value here to allow people to push/delete packages from the server.
            NOTE: This is a shared key (password) for all users. -->
    <add key="apiKey" value="" />
</appSettings>
```

### <a name="support-for-windows-phone-tools-mango-edition"></a>对 Windows Phone 工具 Mango Edition 的支持
NuGet 现在支持在 Windows Phone Mango 的工具的候选发布版本。
目前，Windows Phone 工具不具有对 Visual Studio 扩展管理器，因此，若要安装 Windows Phone 工具的 NuGet 支持，可能需要下载并手动运行 VSIX。

若要卸载 Windows Phone 工具的 NuGet，请运行以下命令。

     vsixinstaller.exe /uninstall:NuPackToolsVsix.Microsoft.67e54e40-0ae3-42c5-a949-fddf5739e7a5

## <a name="bug-fixes"></a>Bug 修复
NuGet 1.4 有工作项固定为 88 总计。 71 的那些已标记为 bug。

有关工作的完整列表项中已修复 NuGet 1.4，请查看[对于此版本的 NuGet 问题跟踪程序](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=All&type=All&priority=All&release=NuGet%201.4&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0)。

## <a name="bug-fixes-worth-noting"></a>值得注意的 bug 修复：

* [问题 603](http://nuget.codeplex.com/workitem/603)： 跨不同的存储库的包依赖项是否正确解析时指定特定的包源。
* [问题 1036年](http://nuget.codeplex.com/workitem/1036)： 添加`NuGet Pack SomeProject.csproj`后不再生成事件将导致无限循环。
* [问题 961](http://nuget.codeplex.com/workitem/961):`-Source`标志支持相对路径。

## <a name="nuget-14-update"></a>NuGet 1.4 更新
NuGet 1.4 发布，我们发现了几个重要修复的问题。
1.4 的此次更新的特定版本号是 1.4.20615.9020。

### <a name="bug-fixes"></a>Bug 修复
* [问题 1220年](http://nuget.codeplex.com/workitem/1220)： 更新包不会执行`install.ps1` / `uninstall.ps1`在多个项目时的所有项目中
* [问题 1156年](http://nuget.codeplex.com/workitem/1156)： 程序包管理器控制台停滞 W2K3/XP 上 （如果未安装 Powershell 2）
