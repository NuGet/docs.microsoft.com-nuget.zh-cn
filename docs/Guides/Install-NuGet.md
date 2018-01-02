---
title: "安装 NuGet 客户端工具 | Microsoft Docs"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 10/02/2017
ms.topic: get-started-article
ms.prod: nuget
ms.technology: 
ms.assetid: 683b8b34-a6f4-4d56-b9cd-2483bfbad1ad
description: "安装客户端工具、命令行界面 (CLI) 和适用于 Visual Studio 包管理器的指南。"
keywords: "nuget.exe CLI, NuGet 客户端工具, NuGet 包管理器, NuGet 包管理器控制台, 适用于 Visual Studio 的 NuGet, NuGet beta 通道"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: b1abb30458c9ebfb0ffb28be254efd9709a9627f
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/14/2017
---
# <a name="installing-nuget-client-tools"></a>安装 NuGet 客户端工具

> [!Tip]
> **打算安装包？请参阅[快速入门 - 使用包](../Quickstart/Use-a-Package.md)。**

有两个主要工具可用于帮助生成、发布和使用 NuGet 包：

1. [NuGet CLI](#nuget-cli) 是适用于 Windows 的命令行实用工具，可提供所有 NuGet 功能；它也可以使用 Mono 或通过 .NET Core CLI (`dotnet`) 在 Mac OSX 和 Linux 上运行。
1. [Visual Studio 中的 NuGet 包管理器](#nuget-package-manager-in-visual-studio)（仅限于 Windows）是用于管理包的 GUI 工具，它包括 PowerShell 控制台，通过该控制台可直接在 Visual Studio 中使用某些 NuGet 命令。 包管理器 UI 和控制台均包括在 Visual Studio（Windows 上）2012 及更高版本中，并且可为早期版本手动安装。

    对于 Visual Studio for Mac，NuGet 功能是直接内置的。 请参阅[在项目中添加 NuGet 包](https://docs.microsoft.com/visualstudio/mac/nuget-walkthrough)，获取有关演练。

    Visual Studio Code 目前没有任何内置 NuGet 支持。 请使用 NuGet CLI 或 [dotnet CLI](../Tools/dotnet-Commands.md)。

NuGet CLI 和包管理器均支持以下操作：

- 搜索包
- 安装包
- 更新包
- 卸载包
- 还原包（仅限于包管理器中的 UI）
- 管理 NuGet 源

以下功能仅受 NuGet CLI 支持：

- 管理包（nuget.org 或专用源）
- 创建包 
- 发布包
- 管理 Nuget.Config
- 管理 NuGet 缓存
- 复制包

> [!Note]
> 另一个很好的工具是 [NuGet 包资源管理器](https://github.com/NuGetPackageExplorer/NuGetPackageExplorer)，它是可直观浏览、创建和编辑 NuGet 包的独立开源工具。 它非常有用，例如，无需每次重新生成包即可对包结构进行实验性更改。
> 用于开发 .NET Core 应用程序的跨平台 [.NET Core CLI](https://docs.microsoft.com/dotnet/articles/core/tools/index#installation) 工具链支持多个 NuGet 命令，如删除、局部变量、推送、打包和还原。 

## <a name="nuget-cli"></a>NuGet CLI

NuGet 命令行接口提供对所有 NuGet 功能的访问权限，并且可在 Windows、Mac OSX 和 Linux 上运行，如以下各节所述。

### <a name="windows"></a>Windows

**直接下载：**

[!INCLUDE[install-cli](../includes/install-cli.md)]

> [!Note]
> 对于 NuGet 1.4+，可以使用 `nuget update -self` 将现有 nuget.exe 更新到最新版本。

**其他方法：**

- **Chocolatey**：使用 [Chocolatey](http://chocolatey.org) 客户端安装 [NuGet.CommandLine](http://chocolatey.org/packages/NuGet.CommandLine) Chocolatey 包。 

    ```ps
    choco install nuget.commandline
    ```

- **Visual Studio**：从 Visual Studio 中的包管理器控制台安装 [NuGet.CommandLine](http://www.nuget.org/packages/NuGet.CommandLine/) 包。

    > [!Note]
    > **针对 NuGet 2.x 用户**：由于 NuGet 3.2 中引入了重大更改，因此 [https://nuget.org/nuget.exe](https://nuget.org/nuget.exe) 指向最新稳定 NuGet 2.x 版本，防止持续集成系统可能出现的中断。

<a name="compatibility-with-mono"></a>

## <a name="mac-osx-and-linux"></a>Mac OSX 和 Linux

在 Mac OSX 和 Linux 上，有两种方法可运行 NuGet CLI：

- 安装包括核心 NuGet 功能的 [.NET Core SDK](https://www.microsoft.com/net/download/core)。 下载还会在 [github.com/dotnet/cli](https://github.com/dotnet/cli) 上列出。 如果需要更完整的功能，则通过下面第二个选项，将 `nuget.exe` 与 Mono 结合使用。

- 安装 [Mono](http://www.mono-project.com/docs/getting-started/install/)，然后从 [nuget.org/downloads](https://nuget.org/downloads) 使用适用于 Windows（版本 3.2 及更高版本）的 `nuget.exe` 命令行可执行文件。 在 Mono 上运行 NuGet 受到以下限制：

    - 经测试可运行的命令：
        - config
        - 删除
        - 帮助
        - install
        - list
        - push
        - setApiKey
        - sources
        - spec

    - 部分运行的命令：
        - pack：适用于 `.nuspec` 文件，但不适用于项目文件。
        - restore：适用于 `packages.config` 和 `project.json` 文件，但不适用于解决方案 (`.sln`) 文件。

    - 不起作用的命令：
        - 更新

### <a name="related-topics"></a>相关主题

- [NuGet CLI 引用](../tools/nuget-exe-cli-reference.md)
- [创建包](../create-packages/creating-a-package.md)
- [发布包](../create-packages/publish-a-package.md)

## <a name="nuget-package-manager-in-visual-studio"></a>Visual Studio 中的 NuGet 包管理器

Windows（2012 及更高版本）上每个版本的 Visual Studio 中都包括 NuGet 包管理器。 它包括包管理器 UI（[引用](../tools/package-manager-ui.md)，以及包管理器控制台，可通过其访问某些包附带的工具（[引用](../tools/package-manager-console.md)）。

Visual Studio 2017 安装程序包括具有任何采用 .NET 的工作负荷的 NuGet 包管理器。 若要单独安装，或验证是否已安装包管理器，运行 Visual Studio 2017 安装程序，并检查“各个组件”>“代码工具”>“NuGet 包管理器”下的选项。

> [!Note]
> 控制台需要 [PowerShell 2.0](http://support.microsoft.com/kb/968929)，Windows 7 或更高版本及 Windows Server 2008 R2 或更高版本中已安装 PowerShell 2.0。
>
> 包管理器控制台命令也仅可在 Windows 上的 Visual Studio 中运行。 在该环境外使用 NuGet CLI，包括使用 Visual Studio for Mac 和 Visual Studio Code 的情况。

### <a name="package-manager-installation-for-visual-studio-2010-and-earlier"></a>适用于 Visual Studio 2010 及更早版本的包管理器安装

Visual Studio 2012 及更高版本不需要这些步骤，它们已包括包管理器。

1. 在 Visual Studio 2010 及更早版本中，单击“工具”>“扩展和更新”。
1. 导航到“联机”，然后搜索“适用于 Visual Studio 的 NuGet 包管理器”，然后单击“下载”。
1. 在“安装程序”对话框中，单击“安装”。
1. 安装完成后，重新启动 Visual Studio。

> [!Tip]
> 如果无法使用 Visual Studio 中的“扩展和更新”对话框（例如，已被代理阻止），则可以直接在 [https://dist.nuget.org/index.html](https://dist.nuget.org/index.html) 下载适用于 Visual Studio 2013 和 2015 的扩展。

### <a name="updating-the-package-manager"></a>更新包管理器

对于 Visual Studio 2015 Update 2 及更高版本，包管理器自动更新为最新稳定版本。

对于 Visual Studio 2015 Update 1 及更早版本，请选择“工具 > 扩展和更新”命令，然后单击“更新”选项卡，查看是否有可用的包管理器新版本。  

### <a name="nuget-previews"></a>NuGet 预览版

如果希望预览即将推出的 NuGet 功能，请安装 [Visual Studio 2017 预览版](https://www.visualstudio.com/vs/preview/)，该版本与 Visual Studio 稳定版本并行工作。

请注意，不再使用以前的适用于 Visual Studio 2015 的 NuGet Beta 通道 (`https://dotnet.myget.org/F/nuget-beta/vsix/`)。

若要报告任何版本的 NuGet 的问题或分享观点，请在 [NuGet GitHub 存储库](https://github.com/Nuget/Home)上打开问题。

### <a name="related-topics"></a>相关主题

- [包管理器 UI 引用](../tools/package-manager-ui.md)
- [包管理器控制台引用](../tools/package-manager-console.md)
- [包管理器控制台 PowerShell 引用](../tools/powershell-reference.md)