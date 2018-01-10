---
title: "NuGet 程序包管理器用户界面参考 |Microsoft 文档"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 12/08/2017
ms.topic: article
ms.prod: nuget
ms.technology: 
ms.assetid: 62f6962b-7b84-4452-ae0d-a9e1ef1fc6f0
f1_keywords:
- vs.toolsoptionspages.nuget_package_manager
- vs.toolsoptionspages.nuget_package_manager.general
- vs.toolsoptionspages.nuget_package_manager.package_sources
description: "使用 Visual Studio 中的 NuGet 包管理器用户界面，用于使用 NuGet 包的说明。"
keywords: "NuGet UI 中，NuGet 包管理器 UI 中，NuGet 在 Visual Studio 中，管理 NuGet 包、 NuGet 用户界面、 Visual Studio 中的包管理器"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: fb2166b727dd01de0f7096535fdbc71c5ab0e2a3
ms.sourcegitcommit: cde52deee5691d3e8bcb96f46f9645c7ba579af8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/10/2018
---
# <a name="nuget-package-manager-ui"></a>NuGet 包管理器 UI

在 Windows 上的 Visual Studio 中的 NuGet 包管理器 UI，可轻松地安装、 卸载和更新为项目和解决方案的 NuGet 程序包。 Visual Studio 中适用于 Mac 的体验，请参阅[中你的项目包括 NuGet 包](/visualstudio/mac/nuget-walkthrough)。 程序包管理器 UI 不包括 Visual Studio 代码。

本主题内容：

- [查找和安装包 （浏览选项卡）](#finding-and-installing-a-package)
- [卸载程序包 （已安装选项卡）](#uninstalling-a-package)
- [更新包 （已安装和更新选项卡）](#updating-a-package) (包括["隐式引用的 SDK"或"AutoReferenced"消息](#implicit_reference))
- [管理解决方案的包](#managing-packages-for-the-solution)（使用多个项目在同一时间）。
- [包源](#package-sources)
- [包管理器选项控件](#package-manager-options-control)

> [!Note]
> 如果您缺少 Visual Studio 2015 中的 NuGet 包管理器，请检查**工具 > 扩展和更新...**并搜索*NuGet 包管理器*扩展。 如果你无法使用 Visual Studio 中的扩展安装程序，下载直接从扩展[https://dist.nuget.org/index.html](https://dist.nuget.org/index.html)。
>
> 在 Visual Studio 2017，NuGet 和 NuGet 包管理器将自动安装与任意。提供与.NET 相关的工作负荷。 通过选择单独安装它**各个组件 > 代码工具 > NuGet 包管理器**在 Visual Studio 2017 安装程序中的选项。

## <a name="finding-and-installing-a-package"></a>查找和安装的包

1. 在**解决方案资源管理器**，右键单击**引用**或某个项目并选择**管理 NuGet 包...**.

    ![管理 NuGet 包菜单选项](media/ManagePackagesUICommand.png)

1. **浏览**选项卡显示由从当前所选的源的受欢迎程度包 (请参阅[包源](#package-sources))。 搜索特定包在左上方使用搜索框。 从列表以显示其信息，还可以选择包**安装**以及版本选择的下拉列表的按钮。

    ![管理 NuGet 包对话框浏览选项卡](media/Search.png)

1. 从下拉列表中选择所需的版本，然后选择**安装**。 Visual Studio 在项目中安装包和其依赖项。 你可能会要求以接受许可条款。 安装完成后，添加的包会出现在**已安装**选项卡。包也会列在**引用**的解决方案资源管理器，指示，你可以参考它们具有项目中的节点`using`语句。

    ![在解决方案资源管理器的引用](media/References.png)

> [!Tip]
    > 若要在搜索中，包括预发布版本并使预发布版本在版本中可用下拉列表，选中**包括预发行版**选项。

## <a name="uninstalling-a-package"></a>卸载包

1. 在**解决方案资源管理器**，右键单击**引用**或所需的项目，并选择**管理 NuGet 包...**.
1. 选择**已安装**选项卡。
1. 选择要卸载 （使用搜索以筛选列表，如有必要） 的包，并选择**卸载**。

    ![卸载包](media/UninstallPackage.png)

1. 请注意，**包括 preprelease**和**包源**卸载包时，控件将产生任何影响。

## <a name="updating-a-package"></a>更新程序包

1. 在**解决方案资源管理器**，右键单击**引用**或所需的项目，并选择**管理 NuGet 包...**.(在网站项目中，右键单击**Bin**文件夹。)
1. 选择**更新**选项卡可查看从选定的程序包源中具有可用的更新的包。 选择**包括预发行版**将预发行程序包包括在更新列表。
1. 选择要更新，从在右侧的下拉列表中选择所需的版本并选择的包**更新**。

    ![更新程序包](media/UpdatePackages.png)

1. <a name="implicit_reference"></a>某些包的**更新**按钮处于禁用状态，并显示一条消息，指出，它"隐式引用由 SDK"（或"AutoReferenced"）。 消息指示包，如 Microsoft.NETCore.App 或 Microsoft.NETStandard.Library，是更大的框架或 SDK 的一部分，并且不应单独更新。 (此类 packagee 内部标记有`<IsImplicitlyDefined>True</IsImplicitlyDefined>`。)若要更新的包，更新其所属的 SDK。

    ![示例包标记为作为隐式引用或 AutoReferenced](media/PackageManagerUIAutoReferenced.png)

1. 若要为其最新版本更新多个包，它们在中选择该列表并选择**更新**列表上方的按钮。
1. 你还可以更新从单个包**已安装**选项卡。在这种情况下，包的详细信息包括版本选择器 (受制于**包括预发行版**选项) 和**更新**按钮。

## <a name="managing-packages-for-the-solution"></a>管理解决方案包

管理包的解决方案是同时使用多个项目的便捷方式。

1. 选择**工具 > NuGet 包管理器 > 管理解决方案的 NuGet 包...**菜单命令，或右键单击该解决方案并选择**管理 NuGet 包...**:

    ![管理解决方案的 NuGet 包](media/ManagePackagesSolutionUICommand.png)

1. 在管理解决方案的包时，UI 将允许你选择的操作会影响的项目：

    ![管理解决方案的包时，项目选择器](media/SolutionPackagesUI.png)

### <a name="consolidate-tab"></a>合并选项卡

开发人员通常考虑它在同一解决方案中的不同项目使用不同版本的相同的 NuGet 包的做法不妥。 当你选择管理包的解决方案时，提供包管理器 UI**合并**依据你可轻松看到其中由解决方案中的不同项目使用具有不同版本号的包的选项卡：

![包管理器 UI 合并选项卡](media/ConsolidateTab.png)

在此示例中，ClassLibrary1 项目使用 EntityFramework 6.2.0，而 ConsoleApp1 正在使用 EntityFramework 6.2.0。 要合并包版本，请执行以下操作：

- 选择项目列表中要更新的项目。
- 选择要在中的所有这些项目中使用的版本**版本**的控制权，例如 EntityFramework 6.2.0。
- 选择**安装**按钮。

程序包管理器安装到所有选定的项目，此后包不会再出现在所选的包版本**合并**选项卡。

## <a name="package-sources"></a>包源

若要更改 Visual Studio 将从其获取包的源，选择一个从源选择器：

![包管理器 UI 中的包源选择器](media/PackageSourceDropDown.png)

若要管理的包源：

1. 选择**设置**程序包管理器用户界面中的图标如下所述，或使用**工具 > 选项**命令并滚动到**NuGet 包管理器**:

    ![包管理器 UI 设置图标](media/PackageSourceSettings.png)

1. 选择**包源**节点：

    ![包源选项](media/options.png)

1. 若要添加的源，选择 **+** ，编辑的名称，输入的 URL 或路径中的**源**控件，并选择**更新**。 源现在将显示在选择器下拉列表中。
1. 若要更改包源，选择它，请在编辑**名称**和**源**框中，然后选择**更新**。
1. 若要禁用的包源，请清除列表中的名称左边的框。
1. 若要删除的包源，选择它，然后选择**X**按钮。
1. 使用向上和向下箭头按钮更改包源的优先顺序。 还原项目包时，visual Studio 中的优先级顺序搜索这些源。 有关详细信息，请参阅[程序包还原](../Consume-Packages/Package-Restore.md)。

> [!Tip]
> 如果包源中删除它后再次出现，它可能会列出在计算机级别或用户级别`NuGet.Config`文件。 请参阅[配置 NuGet 行为](../Consume-Packages/Configuring-NuGet-Behavior.md)对于这些文件的位置，然后删除源通过手动编辑文件，或使用[nuget 源命令](../tools/nuget-exe-CLI-reference.md)。

## <a name="package-manager-options-control"></a>包管理器选项控件

选择包后，包管理器 UI 显示一个较小，可展开**选项**下面 （此处显示了折叠和扩展） 的版本选择器控件。 请注意，对于某些项目类型，如.NET 核心和那些使用`project.json`引用格式，仅**显示预览窗口**提供选项。

![包管理器选项](media/PackageManagerUIOptions.png)

以下各节说明这些选项。

### <a name="show-preview-window"></a>显示预览窗口

选定后，一个模式窗口显示其选包的依赖关系之前安装此包：

![示例预览对话框](media/InstallPreviewDialog.png)

<!-- This is here because the link in the UI needs this anchor. See https://github.com/NuGet/NuGet.Client/blob/dev/src/NuGet.Clients/PackageManagement.UI/Xamls/OptionsControl.xaml -->
<a name="install-options"></a>

### <a name="install-and-update-options"></a>安装和更新选项

（不可用的所有项目类型。）

**依赖项行为**配置 NuGet 如何判断哪些版本的依赖的包要进行安装：

- *忽略依赖项*会跳过安装任何依赖关系，这通常违反要安装的程序包。
- *最低*[默认] 使用的最小的版本号，可满足要求的主选定包安装依赖项。
- *最高的修补程序*安装的版本具有相同主版本号和次版本号，但最高的修补程序数。 例如，如果指定版本 1.2.2 则开头 1.2 最高的版本将安装
- *最高的次要*与相同的主版本号，但最高次版本号和修补程序号一起安装的版本。 如果指定版本 1.2.2，然后从 1 开始的最高版本安装
- *最高*安装包的最高可用版本。

**文件冲突操作**指定 NuGet 应如何处理项目或本地计算机中已存在的包：

- *提示*指示 NuGet 询问是要保留还是覆盖现有包。
- *忽略所有*指示 NuGet 要跳过覆盖任何现有包。
- *覆盖所有*指示 NuGet 覆盖任何现有包。

<!-- This is here because the link in the UI needs this anchor. See https://github.com/NuGet/NuGet.Client/blob/dev/src/NuGet.Clients/PackageManagement.UI/Xamls/OptionsControl.xaml -->
<a name="uninstall-options"></a>

### <a name="uninstall-options"></a>卸载选项

（不可用的所有项目类型。）

**删除依赖关系**： 当选中时，删除任何依赖的包，如果它们不在项目中的其他位置引用。

**强制卸载，即使在其上有依赖关系**： 当选中时，卸载程序包，即使它仍然引用项目中。 这通常与结合使用**删除依赖关系**若要删除包和任何依赖项安装它。 使用此选项可能，但是，会导致损坏的引用，项目中。 在这种情况下你可能需要[重新安装这些其他包](../consume-packages/reinstalling-and-updating-packages.md)。
