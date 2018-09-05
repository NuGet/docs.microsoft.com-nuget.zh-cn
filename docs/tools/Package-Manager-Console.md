---
title: NuGet 包管理器控制台指南
description: 使用 Visual Studio 中的 NuGet 包管理器控制台，用于处理包的说明。
author: karann-msft
ms.author: karann
ms.date: 01/23/2018
ms.topic: conceptual
f1_keywords:
- vs.nuget.packagemanager.console
ms.openlocfilehash: 88979c67ea7f073f2ea5a02c445186642f77f210
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/04/2018
ms.locfileid: "43546873"
---
# <a name="package-manager-console"></a>程序包管理器控制台

Windows 2012 和更高版本上的 Visual Studio 内置 NuGet 包管理器控制台。 （它不包含在 Visual Studio for Mac 或 Visual Studio Code。）

在控制台，可以使用[NuGet PowerShell 命令](../tools/powershell-reference.md)查找、 安装、 卸载和更新 NuGet 包。 使用控制台是在包管理器 UI 不提供一种方法来执行操作的情况下必需的。 若要使用`nuget.exe`命令在控制台中，请参阅[使用 nuget.exe CLI 在控制台中](#using-the-nugetexe-cli-in-the-console)。

例如，查找和安装包是通过三个简单步骤：

1. 在 Visual Studio 中，打开项目/解决方案并打开控制台使用**工具 > NuGet 包管理器 > 程序包管理器控制台**命令。

1. 找到想要安装的程序包。 如果您已经知道此，请跳到步骤 3。

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
> 在控制台中可用的所有操作也都可以使用[NuGet CLI](../tools/nuget-exe-cli-reference.md)。 但是，控制台命令在 Visual Studio 和已保存的项目/解决方案的上下文中运行，并且通常完成多个其等效的 CLI 命令。 例如，通过控制台将包安装添加到项目的引用而 CLI 命令不运行。 出于此原因，通常使用 Visual Studio 的开发人员更愿意使用控制台到 CLI。

> [!Tip]
> 许多控制台操作依赖于 Visual Studio 中使用已知的路径名打开某个解决方案。 如果你有未保存的解决方案或没有解决方案，您可以看到此错误，"未打开解决方案或不会保存。 请确保已打开并保存解决方案。" 这表示控制台不能确定的解决方案文件夹。 正在保存未保存的解决方案，或创建并保存解决方案，如果你还没有打开，应更正此错误。

## <a name="opening-the-console-and-console-controls"></a>打开控制台和控制台控件

1. 打开 Visual Studio 中使用控制台**工具 > NuGet 包管理器 > 程序包管理器控制台**命令。 在控制台是可以排列和放置您喜欢的 Visual Studio 窗口 (请参阅[自定义 Visual Studio 中的窗口布局](/visualstudio/ide/customizing-window-layouts-in-visual-studio))。

1. 默认情况下，控制台命令针对特定包源和项目在窗口顶部的控件中设置运行：

    ![包管理器控制台可以控制对包源和项目](media/PackageManagerConsoleControls1.png)

1. 选择不同的包源和/或项目更改这些默认值的后续命令。 到覆盖这些设置而无需更改默认设置，大多数命令支持`-Source`和`-ProjectName`选项。

1. 若要管理的包源，选择齿轮图标。 这是快捷方式**工具 > 选项 > NuGet 包管理器 > 程序包源**对话框中，如所述[包管理器 UI](package-manager-ui.md#package-sources)页。 此外，右侧的项目选择器控件中清除控制台的内容：

    ![包管理器控制台设置和清除控件](media/PackageManagerConsoleControls2.png)

1. 最右边的按钮会中断长时间运行命令。 例如，运行`Get-Package -ListAvailable -PageSize 500`列出的前 500 包上的默认源 （例如 nuget.org)，这可能需要几分钟时间才能运行。

    ![包管理器控制台停止控件](media/PackageManagerConsoleControls3.png)

## <a name="installing-a-package"></a>安装包

```ps
# Add the Elmah package to the default project as specified in the console's project selector
Install-Package Elmah

# Add the Elmah package to a project named UtilitiesLib that is not the default
Install-Package Elmah -ProjectName UtilitiesLib
```

请参阅[安装包](../tools/ps-ref-install-package.md)。

在控制台中安装的包执行相同的步骤，所描述的方法[安装包，则会发生什么情况](../consume-packages/ways-to-install-a-package.md#what-happens-when-a-package-is-installed)，增加了以下信息：

- 控制台会显示在其窗口具有隐式协议中适用的许可条款。 如果您不同意这些条款，则应立即卸载包。
- 此外对包的引用添加到项目文件并将出现在**解决方案资源管理器**下**引用**节点，你需要保存该项目来直接查看项目文件中的更改。

## <a name="uninstalling-a-package"></a>卸载包

```ps
# Uninstalls the Elmah package from the default project
Uninstall-Package Elmah

# Uninstalls the Elmah package and all its unused dependencies
Uninstall-Package Elmah -RemoveDependencies 

# Uninstalls the Elmah package even if another package depends on it
Uninstall-Package Elmah -Force
```

请参阅[卸载包](../tools/ps-ref-uninstall-package.md)。 使用[Get-package](../tools/ps-ref-get-package.md)以查看当前安装在默认项目中，如果需要查找标识符的所有包。

卸载包将执行以下操作：

- 删除对包的项目 （和正在使用中的任何管理格式）。 引用不再显示在**解决方案资源管理器**。 (您可能需要重新生成项目后，若要查看其从中**Bin**文件夹。)
- 反转对所做的任何更改`app.config`或`web.config`时已安装了包。
- 如果没有剩余的包使用这些依赖项的依赖以前安装中删除项。

## <a name="updating-a-package"></a>更新包

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

请参阅[Get-package](../tools/ps-ref-get-package.md)和[更新包](../tools/ps-ref-update-package.md)

## <a name="finding-a-package"></a>查找包

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

请参阅[查找包](../tools/ps-ref-find-package.md)。 在 Visual Studio 2013 及更早版本，使用[Get-package](../tools/ps-ref-get-package.md)相反。

## <a name="availability-of-the-console"></a>控制台的可用性

在 Visual Studio 2017，NuGet 和 NuGet 包管理器会自动安装时选择任何。NET 相关的工作负荷;您还可以安装它单独通过检查**各个组件 > 代码工具 > NuGet 包管理器**Visual Studio 2017 安装程序中的选项。

此外，如果您遗漏了 NuGet 包管理器在 Visual Studio 2015 及更早版本，请检查**工具 > 扩展和更新...** 和搜索 NuGet 包管理器扩展。 如果您无法在 Visual Studio 中使用扩展安装程序，也可以下载的扩展直接从[ https://dist.nuget.org/index.html ](https://dist.nuget.org/index.html)。

包管理器控制台不是目前适用于 Visual Studio for mac。 等效的命令，但是，都可通过[NuGet CLI](nuget-exe-CLI-reference.md)。 Visual Studio for Mac 也有一个用户界面，用于管理 NuGet 包。 请参阅[在项目中的包括 NuGet 包](/visualstudio/mac/nuget-walkthrough)。

包管理器控制台不包含使用 Visual Studio Code。

## <a name="extending-the-package-manager-console"></a>扩展包管理器控制台

某些包安装控制台的新命令。 例如，`MvcScaffolding`之类的命令将创建`Scaffold`如下所示，它在生成 ASP.NET MVC 控制器和视图：

![安装和使用 MvcScaffold](media/PackageManagerConsoleInstall.png)

## <a name="setting-up-a-nuget-powershell-profile"></a>NuGet PowerShell 配置文件的设置

PowerShell 配置文件，可以使常用命令可用，无论你使用 PowerShell。 NuGet 支持特定于 NuGet 的配置文件通常位于以下位置找到：

    %UserProfile%\Documents\WindowsPowerShell\NuGet_profile.ps1

若要查找该配置文件，请键入`$profile`在控制台中：

```ps
$profile
C:\Users\<user>\Documents\WindowsPowerShell\NuGet_profile.ps1
```

有关更多详细信息，请参阅[Windows PowerShell 配置文件](https://technet.microsoft.com/library/bb613488.aspx)。

## <a name="using-the-nugetexe-cli-in-the-console"></a>使用 nuget.exe CLI 在控制台中

若要使[ `nuget.exe` CLI](nuget-exe-cli-reference.md)程序包管理器控制台中提供安装[NuGet.CommandLine](http://www.nuget.org/packages/NuGet.CommandLine/)从控制台的包：

```ps
# Other versions are available, see http://www.nuget.org/packages/NuGet.CommandLine/
Install-Package NuGet.CommandLine -Version 4.4.1
```
