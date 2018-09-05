---
title: NuGet 包管理器用户界面参考
description: 使用 Visual Studio 中的 NuGet 包管理器用户界面，用于处理 NuGet 包的说明。
author: karann-msft
ms.author: karann
ms.date: 12/08/2017
ms.topic: conceptual
f1_keywords:
- vs.toolsoptionspages.nuget_package_manager
- vs.toolsoptionspages.nuget_package_manager.general
- vs.toolsoptionspages.nuget_package_manager.package_sources
- vs.nuget.packagemanager.ui
ms.openlocfilehash: 651bbe63ec95fcedb8e9504022d08d6ba7f9219e
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/04/2018
ms.locfileid: "43551752"
---
# <a name="nuget-package-manager-ui"></a>NuGet 包管理器 UI

Windows 上的 Visual Studio 中的 NuGet 包管理器用户界面，可轻松地安装、 卸载和更新中项目和解决方案的 NuGet 包。 在 Visual Studio for Mac 的体验，请参阅[在项目中的包括 NuGet 包](/visualstudio/mac/nuget-walkthrough)。 包管理器 UI 不包含使用 Visual Studio Code。

本主题内容：

- [查找和安装包 （浏览选项卡）](#finding-and-installing-a-package)
- [卸载包 （已安装选项卡）](#uninstalling-a-package)
- [更新包 （已安装和更新选项卡）](#updating-a-package) (包括["隐式引用的 SDK"或"AutoReferenced"消息](#implicit_reference))
- [管理解决方案包](#managing-packages-for-the-solution)（使用多个项目在同一时间）。
- [包源](#package-sources)
- [包管理器选项控件](#package-manager-options-control)

> [!Note]
> 如果您遗漏了 Visual Studio 2015 中的 NuGet 包管理器，请检查**工具 > 扩展和更新...** 并搜索*NuGet 包管理器*扩展。 如果您无法在 Visual Studio 中使用扩展安装程序，下载的扩展直接从[ https://dist.nuget.org/index.html ](https://dist.nuget.org/index.html)。
>
> 在 Visual Studio 2017，NuGet 和 NuGet 包管理器会自动安装任何。NET 相关的工作负荷。 通过选择单独安装它**各个组件 > 代码工具 > NuGet 包管理器**Visual Studio 2017 安装程序中的选项。

## <a name="finding-and-installing-a-package"></a>查找和安装包

1. 在中**解决方案资源管理器**，右键单击**引用**或某个项目并选择**管理 NuGet 包...**.

    ![管理 NuGet 包菜单选项](media/ManagePackagesUICommand.png)

1. **浏览**选项卡显示包的当前所选源中的受欢迎程度 (请参阅[包源](#package-sources))。 搜索特定的包使用左上角的搜索框中。 从列表以显示其信息，还可以选择包**安装**以及版本选择下拉列表的按钮。

    ![管理 NuGet 包对话框浏览选项卡](media/Search.png)

1. 从下拉列表中选择所需的版本，然后选择**安装**。 Visual Studio 将包及其依赖项安装到项目中。 您可能需要接受许可条款。 完成安装后，添加的包将出现在**已安装**选项卡。包也会列在**引用**解决方案资源管理器，指示你可以使用项目中引用这些节点`using`语句。

    ![在解决方案资源管理器的引用](media/References.png)

> [!Tip]
> 若要在搜索中，包括预发布版本并使预发布版本的版本中可用下拉列表，选择**包括预发行版**选项。

## <a name="uninstalling-a-package"></a>卸载包

1. 在中**解决方案资源管理器**，右键单击**引用**或所需的项目，然后选择**管理 NuGet 包...**.
1. 选择**已安装**选项卡。
1. 选择要卸载 （使用搜索来筛选列表，如有必要） 的包，然后选择**卸载**。

    ![卸载包](media/UninstallPackage.png)

1. 请注意，**包括预发行版**并**包源**卸载包时，控件不起任何作用。

## <a name="updating-a-package"></a>更新包

1. 在中**解决方案资源管理器**，右键单击**引用**或所需的项目，然后选择**管理 NuGet 包...**.(在网站项目中，右键单击**Bin**文件夹。)
1. 选择**更新**选项卡以查看从所选的包的源有可用更新的包。 选择**包括预发行版**要包括在更新列表中的预发行包。
1. 选择要更新，请从在右侧的下拉列表中选择所需的版本并选择包**更新**。

    ![更新包](media/UpdatePackages.png)

1. <a name="implicit_reference"></a>某些包的**更新**按钮处于禁用状态并显示一条消息说它"隐式引用的 sdk"（或"AutoReferenced"）。 该消息指示程序包，例如 Microsoft.NETCore.App 或 Microsoft.NETStandard.Library，是更大的框架或 SDK 的一部分，并且不应独立更新。 (此类包在内部标记有`<IsImplicitlyDefined>True</IsImplicitlyDefined>`。)若要更新的包，更新其所属，推断从包名称包含 SDK 的 SDK。 例如，程序包一样 Microsoft.NETCore.App 是.NET Core SDK 的一部分，因此需要将.NET Core SDK 安装更新。

    ![示例包标记为隐式引用或 AutoReferenced](media/PackageManagerUIAutoReferenced.png)

1. 若要为其最新版本更新多个包，选择其在列表中，选择**更新**列表上方的按钮。
1. 此外可以更新个别包从**已安装**选项卡。在这种情况下，包的详细信息包括版本选择器 (受**包括预发行版**选项) 和一个**更新**按钮。

## <a name="managing-packages-for-the-solution"></a>管理解决方案包

管理解决方案的包是一种便利方法，以同时使用多个项目。

1. 选择**工具 > NuGet 包管理器 > 管理解决方案的 NuGet 包...** 菜单命令，或右键单击解决方案并选择**管理 NuGet 包...**:

    ![管理解决方案的 NuGet 包](media/ManagePackagesSolutionUICommand.png)

1. 在管理解决方案的包时，您可以通过 UI 选择的操作影响的项目：

    ![管理解决方案的包时，项目选择器](media/SolutionPackagesUI.png)

### <a name="consolidate-tab"></a>合并选项卡

开发人员通常考虑它在同一解决方案中的不同项目中使用相同的 NuGet 包的不同版本不正确的做法。 当您选择管理包的解决方案时，提供了包管理器 UI**整合**在其可以轻松查看其中有不同的版本号的包由解决方案中的不同项目的选项卡：

![包管理器 UI 合并选项卡](media/ConsolidateTab.png)

在此示例中，ClassLibrary1 项目使用 EntityFramework 6.2.0，而 ConsoleApp1 使用 EntityFramework 6.1.0。 要合并的包版本，请执行以下操作：

- 选择要更新项目列表中的项目。
- 选择要在所有这些项目中使用的版本**版本**控件，例如 EntityFramework 6.2.0。
- 选择**安装**按钮。

包管理器将所选的包版本安装到所有选定的项目，在其后包不会再出现在**整合**选项卡。

## <a name="package-sources"></a>包源

若要更改 Visual Studio 将从其获取包的源，选择一个源选择器：

![包管理器 UI 中的包源选择器](media/PackageSourceDropDown.png)

若要管理的包源：

1. 选择**设置**程序包管理器 UI 中的图标如下所述，或使用**工具 > 选项**命令，并滚动到**NuGet 包管理器**:

    ![包管理器 UI 设置图标](media/PackageSourceSettings.png)

1. 选择**包源**节点：

    ![包源选项](media/options.png)

1. 若要添加的源，选择 **+** ，编辑的名称，输入的 URL 或路径中的 **源** 控件，并选择 **更新** 。 现在将显示源选择器下拉列表。
1. 若要更改包源，选择它，请在编辑**名称**并**源**框中，然后选择**更新**。
1. 若要禁用的包源，请清除列表中的名称左边的框。
1. 若要删除的包源，选择它，然后选择**X**按钮。
1. 使用向上和向下箭头按钮可以更改包源的优先级顺序。 还原项目的包时，visual Studio 中的优先顺序搜索这些源。 有关详细信息，请参阅[包还原](../consume-packages/package-restore.md)。

> [!Tip]
> 如果包源中删除它后再次出现，它可能会列出在计算机级别或用户级别`NuGet.Config`文件。 请参阅[配置 NuGet 行为](../consume-packages/configuring-nuget-behavior.md)对于这些文件的位置，然后删除源通过手动编辑文件或使用[nuget 源命令](../tools/nuget-exe-CLI-reference.md)。

## <a name="package-manager-options-control"></a>包管理器选项控件

选择包后，程序包管理器 UI 会显示一个较小，可展开**选项**下面 （此处显示同时折叠和展开） 的版本选择器控件。 请注意，对于某些项目类型，仅**显示预览窗口**提供选项。

![包管理器选项](media/PackageManagerUIOptions.png)

以下部分介绍这些选项。

### <a name="show-preview-window"></a>显示预览窗口

选定后，一个模式窗口显示其中所选包的依赖项之前安装此包：

![示例预览对话框](media/InstallPreviewDialog.png)

<!-- This is here because the link in the UI needs this anchor. See https://github.com/NuGet/NuGet.Client/blob/dev/src/NuGet.Clients/PackageManagement.UI/Xamls/OptionsControl.xaml -->
<a name="install-options"></a>

### <a name="install-and-update-options"></a>安装和更新选项

（不可用的所有项目类型。）

**依赖关系行为**配置 NuGet 如何决定取决于要安装的包版本：

- *忽略依赖关系*将跳过安装任何依赖项，这通常会中断正在安装的软件包。
- *最低*[默认] 使用满足要求的主要的所选包的最小版本号安装依赖项。
- *最高的修补程序*安装的版本具有相同主版本号和次版本号，但在最高的修补程序编号。 例如，如果指定版本 1.2.2 则开头 1.2 的最高版本将安装
- *最高次要*使用相同的主版本号，但最高次版本号和修补程序号安装的版本。 如果指定版本 1.2.2，从 1 开始的最高版本将会安装
- *最高*安装包的最高的可用版本。

**文件冲突操作**指定 NuGet 应如何处理项目或本地计算机中已存在的包：

- *提示*指示 NuGet 询问是要保留还是覆盖现有包。
- *全部忽略*指示 NuGet 跳过覆盖任何现有包。
- *覆盖所有*指示 NuGet 覆盖任何现有包。

<!-- This is here because the link in the UI needs this anchor. See https://github.com/NuGet/NuGet.Client/blob/dev/src/NuGet.Clients/PackageManagement.UI/Xamls/OptionsControl.xaml -->
<a name="uninstall-options"></a>

### <a name="uninstall-options"></a>卸载选项

（不可用的所有项目类型。）

**删除依赖项**： 选定后，删除任何依赖的包，如果它们不在项目中的其他位置引用。

**强制卸载不管它是否存在依赖关系**： 选定后，卸载程序包，即使它仍引用项目中。 这通常使用结合**删除依赖项**删除包以及任何依赖项安装它。 使用此选项可能，但是，会导致项目中损坏的引用。 在这种情况下，可能需要[重新安装这些其他包](../consume-packages/reinstalling-and-updating-packages.md)。
