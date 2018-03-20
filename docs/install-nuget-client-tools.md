---
title: "安装 NuGet 客户端工具 | Microsoft Docs"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 01/24/2018
ms.topic: get-started-article
ms.prod: nuget
ms.technology: 
description: "有关安装客户端工具、dotnet 和 nuget 命令行接口 (CLI) 以及 Visual Studio 软件包管理器的指导。"
keywords: "dotnet.exe CLI, nuget.exe CLI, NuGet 客户端工具, NuGet 包管理器, NuGet 包管理器控制台, NuGet for Visual Studio, NuGet beta 通道"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 462557e939e769f26fe05d6f9e2994eaf43c6e11
ms.sourcegitcommit: 8f26d10bdf256f72962010348083ff261dae81b9
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/08/2018
---
# <a name="installing-nuget-client-tools"></a>安装 NuGet 客户端工具

> **打算安装包？请参阅[安装 NuGet 包的方式](consume-packages/ways-to-install-a-package.md)**

要使用 NuGet，作为软件包使用者或创建者，可以使用[跨平台命令行接口 (CLI) 工具](#cli-tools)以及 [Visual Studio 中的 NuGet 功能](#visual-studio)。 本文简要介绍了不同工具的功能，如何安装它们，以及它们[功能可用性](#feature-availability)的相对优势。

| 工具&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; | 描述 | 下载&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; |
|:------------- |:-------------|:-----|
| [dotnet.exe](#dotnetexe-cli) | 包含在 .NET Core SDK 中，并在所有平台上提供核心 NuGet 功能。 | [.NET Core SDK](https://www.microsoft.com/net/download/) |
| [nuget.exe](#nugetexe-cli) | 提供 Windows 上的所有 NuGet 功能以及 Mac 和 Linux 上在 [Mono](http://www.mono-project.com/docs/getting-started/install/) 下运行的大多数功能。 | [nuget.exe](https://dist.nuget.org/win-x86-commandline/latest/nuget.exe) |
| [Visual Studio](#visual-studio) | 通过包管理器 UI 和包管理器控制台提供 NuGet 功能；包含在与 .NET 相关的工作负荷中。 | [Visual Studio 2017](https://www.visualstudio.com/downloads/) |

[MSBuild CLI](reference/msbuild-targets.md) 还提供了还原和创建包的功能，该功能主要在生成服务器上使用。 否则，MSBuild 不是与 NuGet 一起使用的通用工具。

## <a name="cli-tools"></a>CLI 工具

两个 NuGet CLI 工具是 `dotnet.exe` 和 `nuget.exe`。 请参阅[功能可用性](#feature-availability)以进行比较。

### <a name="dotnetexe-cli"></a>dotnet.exe CLI

.NET Core 2.0 CLI `dotnet.exe` 适用于所有平台（Windows、Mac 和 Linux），并提供核心的 NuGet 功能，例如安装、还原和发布程序包。 'dotnet' 提供了与 .NET Core 项目文件（如 `.csproj`）的直接集成，这在大多数情况下都很有用。 此外，`dotnet` 是直接为每个平台构建的，不需要你安装 Mono。

安装：

- 在开发人员计算机上，请安装 [.NET Core SDK](https://aka.ms/dotnetcoregs)。
- 对于生成服务器，请按照[在持续集成 (CI) 中使用 .NET Core SDK 和工具](/dotnet/core/tools/using-ci-with-cli)中的说明进行操作。

有关详细信息，请参阅 [.NET Core 命令行接口工具](/dotnet/core/tools/index?tabs=netcore2x#tabpanel_fXL5YCOYDa_netcore2x)。

### <a name="nugetexe-cli"></a>nuget.exe CLI

NuGet CLI `nuget.exe` 是适用于 Windows 的命令行实用工具，可提供所有 NuGet 功能；它也可以使用存在一些限制的 Mono 在 Mac OSX 和 Linux 上运行。 与 `dotnet` 不同，`nuget.exe` CLI 不会影响项目文件。

安装：

[!INCLUDE[install-cli](includes/install-cli.md)]

> [!Tip]
> 可以使用 `nuget update -self` 将现有 nuget.exe 更新到最新版本。

> [!Note]
> `https://dist.nuget.org/win-x86-commandline/latest/nuget.exe` 中始终提供推荐的最新 NuGet CLI。 为了实现与旧版持续集成系统的兼容性，以前的 URL `https://nuget.org/nuget.exe` 当前提供 2.8.6 CLI 工具。 [此内容已弃用](https://github.com/NuGet/NuGetGallery/issues/5381)。

## <a name="visual-studio"></a>Visual Studio

- Visual Studio Code：NuGet 功能可通过市场扩展提供，或者使用 `dotnet.exe` 或 `nuget.exe` CLI 工具。
- Visual Studio for Mac：特定 NuGet 功能是直接内置的。 请参阅[在项目中添加 NuGet 包](/visualstudio/mac/nuget-walkthrough)，获取有关演练。 对于其他功能，请使用 `dotnet.exe` 或 `nuget.exe` CLI 工具。

- Windows 上的 Visual Studio：Visual Studio 2012 及更高版本中都包括“NuGet 包管理器”。 该程序包管理器提供[程序包管理器 UI](tools/package-manager-ui.md) 和[程序包管理器控制台](tools/package-manager-console.md)，通过它可以运行大部分的 NuGet 操作。
  - Visual Studio 2017 安装程序包括具有任何采用 .NET 的工作负荷的 NuGet 包管理器。 若要单独安装，或验证是否已安装包管理器，运行 Visual Studio 2017 安装程序，并检查“各个组件”>“代码工具”>“NuGet 包管理器”下的选项。
  - 程序包管理器 UI 和控制台对于 Windows 上的 Visual Studio 是唯一的。 目前，它们在 Visual Studio for Mac 上不可用。
  - Visual Studio 不会自动包含 `nuget.exe` CLI，必须按照前面所述单独安装。
  - 程序包管理器控制台命令只能在 Windows 的 Visual Studio 中工作，不能在其他 PowerShell 环境中使用。
  - 对于 Visual Studio 2010 及更早版本，请安装“适用于 Visual Studio 的 NuGet 包管理器”扩展。
  - 适用于 Visual Studio 2013 和 2015 的 NuGet 扩展也可以从 [https://dist.nuget.org/index.html](https://dist.nuget.org/index.html) 下载。
  - 如果希望预览即将推出的 NuGet 功能，请安装 [Visual Studio 2017 预览版](https://www.visualstudio.com/vs/preview/)，该版本与 Visual Studio 稳定版本并行工作。 若要报告问题或分享对预览版的看法，请在 [NuGet GitHub 存储库](https://github.com/Nuget/Home/issues)上打开问题。

## <a name="feature-availability"></a>功能可用性

| 功能 | dotnet CLI | nuget CLI (Windows) | nuget CLI (Mono) | Visual Studio (Windows) | Visual Studio for Mac |
| --- | --- | --- | --- | --- | --- |
| 搜索包 |  | &#10004; | &#10004; | &#10004; | &#10004; |
| 安装/卸载包 | &#10004;(1) | &#10004;(2) | &#10004; | &#10004; | &#10004; |
| 更新包 | &#10004; | &#10004; | | &#10004; | &#10004; |
| 还原包 | &#10004; | &#10004; | &#10004;(3) | &#10004; | &#10004; |
| 管理包源（来源） | | &#10004; | &#10004; | &#10004; | &#10004; |
| 在源上管理包 | &#10004;(1) | &#10004; | &#10004; | | |
| 设置源的 API 密钥 | | &#10004; | &#10004; | | |
| 创建包(4) | &#10004; | &#10004; | &#10004;(5) | &#10004; | |
| 发布包 | &#10004;(1) | &#10004; | &#10004; | &#10004; |  |
| 复制包 |  | &#10004; | &#10004; | | |
| 管理 NuGet 缓存 | &#10004; | &#10004; | &#10004; | | |
| 管理 NuGet 配置 | | &#10004; | &#10004; | | |

(1) 仅限 nuget.org 上的包

(2) 不会影响项目文件；改用 `dotnet.exe`。

(3) 仅适用于 `packages.config` 文件，不适用于解决方案 (`.sln`) 文件。

(4) 各种高级包功能只能通过 CLI 提供，因为它们不在 Visual Studio UI 工具中表示。

(5) 适用于 `.nuspec` 文件，但不适用于项目文件。

### <a name="related-topics"></a>相关主题

- [dotnet 命令](tools/dotnet-commands.md)
- [NuGet CLI 引用](tools/nuget-exe-cli-reference.md)
- [包管理器 UI 引用](tools/package-manager-ui.md)
- [包管理器控制台引用](tools/package-manager-console.md)
- [包管理器控制台 PowerShell 引用](tools/powershell-reference.md)
- [创建包](create-packages/creating-a-package.md)
- [发布包](create-packages/publish-a-package.md)

在 Windows 上工作的开发人员还可以浏览 [NuGet 包资源管理器](https://github.com/NuGetPackageExplorer/NuGetPackageExplorer)，它是可直观浏览、创建和编辑 NuGet 包的独立开源工具。 它非常有用，例如，无需重新生成包即可对包结构进行实验性更改。
