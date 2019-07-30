---
title: 在 Visual Studio 中安装和管理 NuGet 包
description: 有关在 Visual Studio 中使用 NuGet 包管理器 UI 以处理 NuGet 包的说明。
author: karann-msft
ms.author: karann
ms.date: 07/08/2019
ms.topic: conceptual
f1_keywords:
- vs.toolsoptionspages.nuget_package_manager
- vs.toolsoptionspages.nuget_package_manager.general
- vs.toolsoptionspages.nuget_package_manager.package_sources
- vs.nuget.packagemanager.ui
ms.openlocfilehash: 7e4ea59b9954e787e7ab060adc964f3097a8240b
ms.sourcegitcommit: e65180e622f6233b51bb0b41d0e919688083eb26
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/23/2019
ms.locfileid: "68419970"
---
# <a name="install-and-manage-packages-in-visual-studio-using-the-nuget-package-manager"></a>使用 NuGet 包管理器在 Visual Studio 中安装和管理包

通过 Windows 版 Visual Studio 中的 NuGet 包管理器 UI，可轻松安装、卸载和更新项目和解决方案中的 NuGet 包。 若要了解 Visual Studio for Mac 的使用体验，请参阅[在项目中包括 NuGet 包](/visualstudio/mac/nuget-walkthrough?toc=/nuget/toc.json)。 Visual Studio Code 中不包含包管理器 UI。

> [!NOTE]
> 如果 Visual Studio 2015 中缺少 NuGet 包管理器，请选中“工具”>“扩展和更新...”  并搜索“NuGet 包管理器”  扩展。 如果无法在 Visual Studio 中使用扩展安装程序，请直接从 [https://dist.nuget.org/index.html](https://dist.nuget.org/index.html) 下载扩展。
>
> 从 Visual Studio 2017 开始，NuGet 和 NuGet 包管理器会与任何 .NET 相关的工作负载一起自动安装。 通过在 Visual Studio 安装程序中选择“单个组件”>“代码工具”>“NuGet 包管理器”  选项，可以单独安装它。

## <a name="find-and-install-a-package"></a>查找和安装包

1. 在“解决方案资源管理器”中，右键单击“引用”或某个项目，然后选择“管理 NuGet 包...”    。

    ![“管理 NuGet 包”菜单选项](media/ManagePackagesUICommand.png)

1. “浏览”  选项卡按当前所选来源的受欢迎程度显示包（请参阅[包源](#package-sources)）。 使用左上角的搜索框搜索特定包。 从列表中选择一个包以显示其信息，此操作还会启用“安装”  按钮以及版本选择下拉列表。

    ![“管理 NuGet 包”对话框“浏览”选项卡](media/Search.png)

1. 从下拉列表中选择所需的版本，然后选择“安装”  。 Visual Studio 随即将包及其依赖项安装到项目中。 系统可能会要求你接受许可条款。 安装完成后，添加的包将显示在“已安装”  选项卡上。包同时还列在解决方案资源管理器的“引用”  节点中，表明可以使用 `using` 语句在项目中引用它们。

    ![解决方案资源管理器中的“引用”](media/References.png)

> [!Tip]
> 若要在搜索中包含预发布版本，并在版本下拉列表中提供预发布版本，请选中“包含预发布版本”  选项。

## <a name="uninstall-a-package"></a>卸载包

1. 在“解决方案资源管理器”  中，右键单击“引用”  或所需项目，然后选择“管理 NuGet 包...”  。
1. 选择“已安装”  选项卡。
1. 选择要卸载的包（如有必要，使用搜索来筛选列表）并选择“卸载”  。

    ![卸载包](media/UninstallPackage.png)

1. 请注意，在卸载包时，“包含预发布版本”  和“包源”  控件无效。

## <a name="update-a-package"></a>更新包

1. 在“解决方案资源管理器”  中，右键单击“引用”  或所需项目，然后选择“管理 NuGet 包...”  。（在网站项目中，右键单击“Bin”  文件夹。）
1. 选择“更新”  选项卡，查看所选包源中包含可用更新的包。 选中“包含预发布版本”  ，以便在更新列表中包含预发布版本的包。
1. 选择要更新的包，从右侧的下拉列表中选择所需的版本，然后选择“更新”  。

    ![更新包](media/UpdatePackages.png)

1. <a name="implicit_reference"></a>对于某些包，“更新”  按钮处于禁用状态，并显示一条消息，指示它是“由 SDK 隐式引用”（或“AutoReferenced”）。 此消息表明该包是较大框架或 SDK 的一部分，不能单独更新。 （此类包在内部标有 `<IsImplicitlyDefined>True</IsImplicitlyDefined>`。）例如，`Microsoft.NETCore.App` 是 .NET Core SDK 的一部分，并且包版本与应用程序使用的运行时框架的版本不同。 需要[更新 .NET Core 安装](https://aka.ms/dotnet-download)以获取新版本的 ASP.NET Core 和 .NET Core 运行时。 [请参阅本文档，详细了解 .NET Core 元包和版本控制](/dotnet/core/packages)。 这适用于以下常用包：
    * Microsoft.AspNetCore.All
    * Microsoft.AspNetCore.App
    * Microsoft.NETCore.App
    * NETStandard.Library

    ![标记为“隐式引用”或“AutoReferenced”的示例包](media/PackageManagerUIAutoReferenced.png)

1. 若要将多个包更新到其最新版本，请在列表中选中它们，然后选择列表上方的“更新”  按钮。
1. 还可以从“已安装”  选项卡更新单个包。在这种情况下，包的详细信息包括版本选择器（受“包含预发布版本”  选项的约束）和“更新”  按钮。

## <a name="manage-packages-for-the-solution"></a>管理解决方案的包

管理解决方案的包是同时处理多个项目的便捷方式。

1. 选择“工具”>“NuGet 包管理器”>“管理解决方案的 NuGet 包...”菜单命令，或右键单击解决方案，然后选择“管理 NuGet 包...”   ：

    ![管理解决方案的 NuGet 包](media/ManagePackagesSolutionUICommand.png)

1. 管理解决方案的包时，UI 让你可以选择受操作影响的项目：

    ![管理解决方案的包时的项目选择器](media/SolutionPackagesUI.png)

### <a name="consolidate-tab"></a>“合并”选项卡

开发人员通常认为，在同一解决方案的不同项目中使用相同 NuGet 包的不同版本的做法不好。 当你选择管理解决方案的包时，包管理器 UI 提供了一个“合并”  选项卡，让你可以轻松查看解决方案中不同项目使用的具有不同版本号的包：

![包管理器 UI“合并”选项卡](media/ConsolidateTab.png)

在本例中，ClassLibrary1 项目使用的是 EntityFramework 6.2.0，而 ConsoleApp1 使用的是 EntityFramework 6.1.0。 若要合并包版本，请执行以下操作：

- 在项目列表中选择要更新的项目。
- 选择要在“版本”  控件中的所有项目中使用的版本，例如 EntityFramework 6.2.0。
- 选择“安装”按钮  。

包管理器将选定的包版本安装到所有选定的项目中，之后包不再显示在“合并”选项卡上  。

## <a name="package-sources"></a>包源

若要更改 Visual Studio 从中获取包的源，请从源选择器中选择一个源：

![包管理器 UI 中的包源选择器](media/PackageSourceDropDown.png)

管理包源：

1. 在下面的包管理器 UI 中选择“设置”  图标，或使用“工具”>“选项”  命令并滚动到“NuGet 包管理器”  ：

    ![包管理器 UI“设置”图标](media/PackageSourceSettings.png)

1. 选择“包源”节点  ：

    ![“包源”选项](media/options.png)

1. 要添加源，请选择“+”  ，编辑名称，在“源”  控件中输入 URL 或路径，然后选择“更新”  。 选择器下拉列表中现在显示源。
1. 若要更改包源，请选中它，在“名称”  和“源”  框中进行编辑，然后选择“更新”  。
1. 若要禁用包源，请清除列表中名称左侧的框。
1. 若要删除包源，请选中它，然后选择“X”  按钮。
1. 使用向上和向下箭头按钮不会更改包源的优先级顺序。 Visual Studio 会忽略包源的顺序，使用来自任何首先响应请求的源的包。 有关详细信息，请参阅[包源](../consume-packages/package-restore.md)。

> [!Tip]
> 如果在删除某个包源后，该包源重新出现，则它可能会列在计算机级或用户级 `NuGet.Config` 文件中。 有关这些文件的位置，请参阅[常见 NuGet 配置](../consume-packages/configuring-nuget-behavior.md)，然后通过手动编辑文件或使用 [nuget 源命令](../reference/nuget-exe-CLI-reference.md)删除源。

## <a name="package-manager-options-control"></a>包管理器“选项”控件

选择包后，包管理器 UI 会在版本选择器下方显示一个可扩展的“选项”小控件（此处显示为折叠和展开）  。 请注意，对于某些项目类型，仅提供“显示预览窗口”选项  。

![包管理器选项](media/PackageManagerUIOptions.png)

以下各节介绍了这些选项。

### <a name="show-preview-window"></a>显示预览窗口

选中此选项后，模式窗口将显示安装包之前所选包的依赖项：

![示例“预览”对话框](media/InstallPreviewDialog.png)

<!-- This is here because the link in the UI needs this anchor. See https://github.com/NuGet/NuGet.Client/blob/dev/src/NuGet.Clients/PackageManagement.UI/Xamls/OptionsControl.xaml -->
<a name="install-options"></a>

### <a name="install-and-update-options"></a>安装与更新选项

（并非适用于所有项目类型。）

“依赖项行为”  用于配置 NuGet 如何决定要安装哪些版本的依赖包：

- “忽略依赖项”  会跳过安装任何依赖项，这通常会破坏正在安装的软件包。
- 如果选择“最低”  [默认选项]，则安装具有可满足主要选定包要求的最小版本号的依赖项。
- 如果选择“最高版本的修补程序”  ，则安装的版本的主要版本号和次要版本号相同，但修补程序版本号最高。 例如，如果指定版本 1.2.2，则会安装以 1.2 开头的最高版本
- 如果选择“最高次要版本”  ，则安装的版本的主要版本号相同，但次要版本号和修补程序版本号最高。 如果指定版本 1.2.2，则会安装以 1 开头的最高版本
- 选择“最高”  可安装包的最高可用版本。

“文件冲突操作”  指定 NuGet 应如何处理项目或本地计算机中已存在的包：

- “提示”  指示 NuGet 询问是保留还是覆盖现有包。
- “全部忽略”  指示 NuGet 跳过覆盖任何现有包。
- “全部覆盖”  指示 NuGet 覆盖任何现有包。

<!-- This is here because the link in the UI needs this anchor. See https://github.com/NuGet/NuGet.Client/blob/dev/src/NuGet.Clients/PackageManagement.UI/Xamls/OptionsControl.xaml -->
<a name="uninstall-options"></a>

### <a name="uninstall-options"></a>卸载选项

（并非适用于所有项目类型。）

“删除依赖项”  ：如果选中，则删除任何依赖包（如果它们未在项目中的其他位置引用）。

“在存在依赖项时仍强制卸载”  ：选中后，即使在项目中仍然引用了该包，也会卸载它。 此选项通常与“删除依赖项”  一起选中，用于删除包及其安装的任何依赖项。 不过，使用此选项可能会导致项目中的引用中断。 在这种情况下，可能需要[重新安装其他包](../consume-packages/reinstalling-and-updating-packages.md)。
