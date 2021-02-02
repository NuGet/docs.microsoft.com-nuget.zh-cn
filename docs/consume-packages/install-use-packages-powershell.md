---
title: 在 Visual Studio 中使用控制台安装和管理 NuGet 包
description: 有关在 Visual Studio 中使用 NuGet 包管理器控制台以处理包的说明。
author: JonDouglas
ms.author: jodou
ms.date: 07/08/2019
ms.topic: conceptual
f1_keywords:
- vs.nuget.packagemanager.console
ms.openlocfilehash: 119bf32426e5cbc179c3713e60688c691e133c5d
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/26/2021
ms.locfileid: "98774903"
---
# <a name="install-and-manage-packages-with-the-package-manager-console-in-visual-studio-powershell"></a>在 Visual Studio 中使用包管理器控制台安装和管理包 (PowerShell)

借助 NuGet 包管理器控制台，可以使用 [NuGet PowerShell 命令](../reference/powershell-reference.md)查找、安装、卸载和更新 NuGet 包。 如果包管理器 UI 未提供执行操作的方法，则必须使用控制台。 若要在控制台中使用 `nuget.exe` CLI 命令，请参阅[在控制台中使用 nuget.exe CLI](#use-the-nugetexe-cli-in-the-console)。

Windows 版 Visual Studio 中内置了该控制台。 Visual Studio for Mac 或 Visual Studio Code 中未提供该控制台。

> [!Important]
> 此处列出的命令特定于 Visual Studio 中的包管理器控制台，它不同于常规 PowerShell 环境中提供的[包管理模块命令](/powershell/module/packagemanagement/)。 具体而言，每个环境都有一些命令，这些命令在其他环境中不可用，而具有相同名称的命令在其特定参数中也可能不同。 使用 Visual Studio 中的包管理控制台时，本主题中所述的命令和参数适用。

## <a name="find-and-install-a-package"></a>查找和安装包

例如，通过三个简单的步骤查找和安装包：

1. 在 Visual Studio 中打开项目/解决方案，然后使用“工具”>“NuGet 包管理器”>“包管理器控制台”命令打开控制台。

1. 找到要安装的包。 如果你已经知道此操作步骤，请跳至步骤 3。

    ```ps
    # Find packages containing the keyword "elmah"
    Find-Package elmah
    ```

1. 运行安装命令：

    ```ps
    # Install the Elmah package to the project named MyProject.
    Install-Package Elmah -ProjectName MyProject
    ```

> [!Important]
> 控制台中可用的全部操作也可以通过 [NuGet CLI](../reference/nuget-exe-cli-reference.md) 完成。 但是，控制台命令在 Visual Studio 和已保存的项目/解决方案的上下文中运行，并且通常比其等效的 CLI 命令完成更多操作。 例如，通过控制台安装包会添加对项目的引用，而 CLI 命令则不会执行此操作。 因此，在 Visual Studio 中工作的开发人员通常更愿意使用控制台而不是 CLI。

> [!Tip]
> 许多控制台操作依赖于在 Visual Studio 中通过已知路径名打开解决方案。 如果你有未保存的解决方案或没有解决方案，可以看到错误：“解决方案未打开或未保存。 请确保你有一个已打开且已保存的解决方案。” 这表示控制台无法确定解决方案文件夹。 保存未保存的解决方案，或者如果没有打开解决方案，则创建并保存解决方案，这些操作应该可以纠正错误。

## <a name="opening-the-console-and-console-controls"></a>打开控制台和控制台控件

1. 在 Visual Studio 中使用“工具”>“NuGet 包管理器”>“包管理器控制台”命令打开控制台。 控制台是一个 Visual Studio 窗口，可以根据需要进行排列和放置（请参阅[在 Visual Studio 中自定义窗口布局](/visualstudio/ide/customizing-window-layouts-in-visual-studio)）。

1. 默认情况下，控制台命令针对窗口顶部控件中设置的特定包源和项目执行操作：

    ![包源和项目的“包管理器控制台”控件](media/PackageManagerConsoleControls1.png)

1. 选择不同的包源和/或项目会更改后续命令的默认值。 要在不更改默认值的情况下覆盖这些设置，大多数命令都支持 `-Source` 和 `-ProjectName` 选项。

1. 若要管理包源，请选择齿轮图标。 这是“工具”>“选项”>“NuGet 包管理器”>“包源”对话框的快捷方式，如[包管理器 UI](install-use-packages-visual-studio.md#package-sources) 页中所述。 此外，项目选择器右侧的控件可清除控制台的内容：

    ![包管理器控制台设置和清除控件](media/PackageManagerConsoleControls2.png)

1. 最右边的按钮会中断长时间运行的命令。 例如，运行 `Get-Package -ListAvailable -PageSize 500` 会列出默认源（例如 nuget.org）上的前 500 个包，这可能需要几分钟才能运行完毕。

    ![包管理器控制台停止控件](media/PackageManagerConsoleControls3.png)

## <a name="install-a-package"></a>安装包

```ps
# Add the Elmah package to the default project as specified in the console's project selector
Install-Package Elmah

# Add the Elmah package to a project named UtilitiesLib that is not the default
Install-Package Elmah -ProjectName UtilitiesLib
```

请参阅 [Install-Package](../reference/ps-reference/ps-ref-install-package.md)。

在控制台中安装包执行的步骤与[安装包时会发生什么情况](../concepts/package-installation-process.md)相同，只不过它添加了以下内容：

- 控制台在其窗口中显示适用的许可条款，并附带隐含协议。 如果你不同意这些条款，应立即卸载包。
- 此外，对包的引用也会添加到项目文件中，并显示在“引用”节点下的“解决方案资源管理器”中，需要保存项目才能直接查看项目文件中的更改。

## <a name="uninstall-a-package"></a>卸载包

```ps
# Uninstalls the Elmah package from the default project
Uninstall-Package Elmah

# Uninstalls the Elmah package and all its unused dependencies
Uninstall-Package Elmah -RemoveDependencies 

# Uninstalls the Elmah package even if another package depends on it
Uninstall-Package Elmah -Force
```

请参阅 [Uninstall-Package](../reference/ps-reference/ps-ref-uninstall-package.md)。 如果需要查找标识符，请使用 [Get-Package](../reference/ps-reference/ps-ref-get-package.md) 查看当前安装在默认项目中的所有包。

卸载包将执行以下操作：

- 从项目中删除对包的引用（以及正在使用的任何管理格式）。 引用不再出现在“解决方案资源管理器”中。 （可能需要重建项目才能看到它已从 Bin 文件夹中删除。）
- 安装包后，撤销对 `app.config` 或 `web.config` 的任何更改。
- 如果没有其余包使用这些依赖项，则删除以前安装的依赖项。

## <a name="update-a-package"></a>更新包

```ps
# Checks if there are newer versions available for any installed packages
Get-Package -updates

# Updates a specific package using its identifier, in this case jQuery
Update-Package jQuery

# Update all packages in the project named MyProject (as it appears in Solution Explorer)
Update-Package -ProjectName MyProject

# Update all packages in the solution
Update-Package
```

请参阅 [Get-Package](../reference/ps-reference/ps-ref-get-package.md) 和 [Update-Package](../reference/ps-reference/ps-ref-update-package.md)

## <a name="find-a-package"></a>查找包

```ps
# Find packages containing keywords
Find-Package elmah
Find-Package logging

# List packages whose ID begins with Elmah
Find-Package Elmah -StartWith

# By default, Get-Package returns a list of 20 packages; use -First to show more
Find-Package logging -First 100

# List all versions of the package with the ID of "jquery"
Find-Package jquery -AllVersions -ExactMatch
```

请参阅 [Find-Package](../reference/ps-reference/ps-ref-find-package.md)。 在 Visual Studio 2013 及更早版本中，请改用 [Get-Package](../reference/ps-reference/ps-ref-get-package.md)。

## <a name="availability-of-the-console"></a>控制台的可用性

从 Visual Studio 2017 开始，当你选择任何与 .NET 相关的工作负载时，会自动安装 NuGet 和 NuGet 包管理器；不过，也可以通过在 Visual Studio 安装程序中选中“单个组件”>“代码工具”>“NuGet 包管理器”选项来单独安装它。

另外，如果你在 Visual Studio 2015 及更早版本中缺少 NuGet 包管理器，请选中“工具”>“扩展和更新...”并搜索“NuGet 包管理器”扩展。 如果无法在 Visual Studio 中使用扩展安装程序，可以直接从 [https://dist.nuget.org/index.html](https://dist.nuget.org/index.html) 下载扩展。

Visual Studio for Mac 目前不提供包管理器控制台。 但是，可以通过 [NuGet CLI](../reference/nuget-exe-CLI-reference.md) 获取等效命令。 Visual Studio for Mac 确实有一个用于管理 NuGet 包的 UI。 请参阅[在项目中包括 NuGet 包](/visualstudio/mac/nuget-walkthrough)。

Visual Studio Code 中不包含包管理器控制台。

## <a name="extend-the-package-manager-console"></a>扩展包管理器控制台

某些包为控制台安装新命令。 例如，`MvcScaffolding` 创建如下所示的 `Scaffold` 命令，用于生成 ASP.NET MVC 控制器和视图：

![安装和使用 MvcScaffold](media/PackageManagerConsoleInstall.png)

## <a name="set-up-a-nuget-powershell-profile"></a>设置 NuGet PowerShell 配置文件

通过 PowerShell 配置文件，可以在每次使用 PowerShell 时使用常用命令。 NuGet 支持通常位于以下位置的 NuGet 特定配置文件：

%UserProfile%\Documents\WindowsPowerShell\NuGet_profile.ps1

要查找配置文件，请在控制台中键入 `$profile`：

```ps
$profile
C:\Users\<user>\Documents\WindowsPowerShell\NuGet_profile.ps1
```

有关更多详细信息，请参阅 [Windows PowerShell 配置文件](/previous-versions//bb613488(v=vs.85))。

## <a name="use-the-nugetexe-cli-in-the-console"></a>在控制台中使用 nuget.exe CLI

若要在包管理器控制台中使用 [`nuget.exe` CLI](../reference/nuget-exe-cli-reference.md)，请从控制台安装 [NuGet.CommandLine](https://www.nuget.org/packages/NuGet.CommandLine/) 包：

```ps
# Other versions are available, see https://www.nuget.org/packages/NuGet.CommandLine/
Install-Package NuGet.CommandLine -Version 4.4.1
```
