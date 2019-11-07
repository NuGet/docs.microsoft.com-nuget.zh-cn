---
title: 安装 NuGet 客户端工具
description: 有关安装客户端工具、dotnet 和 nuget 命令行接口 (CLI) 以及 Visual Studio 软件包管理器的指导。
author: karann-msft
ms.author: karann
ms.date: 06/20/2019
ms.topic: quickstart
ms.openlocfilehash: 09c859c0ab6767ea80b6a64c194aa2623ee5c505
ms.sourcegitcommit: 39f2ae79fbbc308e06acf67ee8e24cfcdb2c831b
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/05/2019
ms.locfileid: "73610528"
---
# <a name="install-nuget-client-tools"></a>安装 NuGet 客户端工具

> **打算安装包？请参阅[安装 NuGet 包的方式](consume-packages/overview-and-workflow.md#ways-to-install-a-nuget-package)**

要使用 NuGet，作为软件包使用者或创建者，可以使用命令行接口 (CLI) 工具以及 Visual Studio 中的 NuGet 功能。 本文简要介绍了不同工具的功能，如何安装它们，以及它们[功能可用性](#feature-availability)的相对优势。 若要开始借助 NuGet 来使用包，请参阅[安装和使用包 (dotnet CLI)](quickstart/install-and-use-a-package-using-the-dotnet-cli.md) 以及[安装和使用包 (Visual Studio)](quickstart/install-and-use-a-package-in-visual-studio.md)。 若要开始创建 NuGet 包，请参阅[创建和发布 NET Standard 包 (dotnet CLI)](quickstart/create-and-publish-a-package-using-the-dotnet-cli.md) 以及[创建和发布 NET Standard 包 (Visual Studio)](quickstart/create-and-publish-a-package-using-visual-studio.md)。

| 工具&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; | 说明 | 下载&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; |
|:------------- |:-------------|:-----|
| [dotnet.exe](#dotnetexe-cli) | 适用于 .NET Core 和 .NET Standard 库，以及适用于任何 [SDK 样式项目](resources/check-project-format.md)（例如面向 .NET Framework 的项目）的 CLI 工具。 包含在 .NET Core SDK 中，并在所有平台上提供核心 NuGet 功能。 （从 Visual Studio 2017 开始，dotnet CLI 将自动随任何与 .NET Core 相关的工作负载一起安装。）| [.NET Core SDK](https://www.microsoft.com/net/download/) |
| [nuget.exe](#nugetexe-cli) | 适用于 .NET Framework 库，以及适用于任何 [非 SDK 样式项目](resources/check-project-format.md)（例如面向 .NET Standard 库的项目）的 CLI 工具。 提供 Windows 上的所有 NuGet 功能以及 Mac 和 Linux 上在 Mono 下运行时的大多数功能。 | [nuget.exe](https://dist.nuget.org/win-x86-commandline/latest/nuget.exe) |
| [Visual Studio](#visual-studio) | 在 Windows 上，通过包管理器 UI 和包管理器控制台提供 NuGet 功能；包含在与 .NET 相关的工作负荷中。 在 Mac 上，通过 UI 提供某些功能。 在 Visual Studio Code 中，通过扩展提供 NuGet 功能。 | [Visual Studio](https://www.visualstudio.com/downloads/) |

[MSBuild CLI](reference/msbuild-targets.md) 还提供了还原和创建包的功能，该功能主要在生成服务器上使用。 MSBuild 不是与 NuGet 一起使用的通用工具。

## <a name="cli-tools"></a>CLI 工具

两个 NuGet CLI 工具是 `dotnet.exe` 和 `nuget.exe`。 请参阅[功能可用性](#feature-availability)以进行比较。

* 若要面向 .NET Core 或 .NET Standard，请使用 dotnet CLI。 `dotnet` CLI 是 SDK 样式项目格式所必需的，该格式使用 [SDK 属性](/dotnet/core/tools/csproj#additions)。
* 要面向 .NET Framework（仅限非 SDK 样式项目），请使用 `nuget.exe` CLI。 如果项目从 `packages.config` 迁移到 PackageReference，请使用 dotnet CLI。

### <a name="dotnetexe-cli"></a>dotnet.exe CLI

.NET Core 2.0 CLI `dotnet.exe` 适用于所有平台（Windows、Mac 和 Linux），并提供核心的 NuGet 功能，例如安装、还原和发布程序包。 `dotnet` 提供了与 .NET Core 项目文件（如 `.csproj`）的直接集成，这在大多数情况下都很有用。 此外，`dotnet` 是直接为每个平台构建的，不需要你安装 Mono。

安装：

- 在开发人员计算机上，请安装 [.NET Core SDK](https://aka.ms/dotnetcoregs)。 从 Visual Studio 2017 开始，dotnet CLI 将自动随任何与 .NET Core 相关的工作负载一起安装。
- 对于生成服务器，请按照[在持续集成 (CI) 中使用 .NET Core SDK 和工具](/dotnet/core/tools/using-ci-with-cli)中的说明进行操作。

要了解如何在 dotnet CLI 中使用基本命令，请参阅[使用 dotnet CLI 安装并使用包](consume-packages/install-use-packages-dotnet-cli.md)。

### <a name="nugetexe-cli"></a>nuget.exe CLI

`nuget.exe` CLI（即 `nuget.exe`）是适用于 Windows 的命令行实用工具，可提供所有 NuGet 功能；它也可以使用存在一些限制的 [Mono](https://www.mono-project.com/docs/getting-started/install/) 在 Mac OSX 和 Linux 上运行。

要了解如何在 `nuget.exe` CLI 中使用基本命令，请参阅[使用 nuget.exe CLI 安装并使用包](consume-packages/install-use-packages-nuget-cli.md)。

安装：

[!INCLUDE [install-cli](includes/install-cli.md)]

> [!Tip]
> 在 Windows 上运行 `nuget update -self` 可以将现有 nuget.exe 更新为最新版本。

> [!Note]
> `https://dist.nuget.org/win-x86-commandline/latest/nuget.exe` 中始终提供推荐的最新 NuGet CLI。 为了实现与旧版持续集成系统的兼容性，以前的 URL `https://nuget.org/nuget.exe` 当前提供[弃用的 2.8.6 CLI 工具](https://github.com/NuGet/NuGetGallery/issues/5381)。

## <a name="visual-studio"></a>Visual Studio

- Visual Studio Code：NuGet 功能可通过市场扩展提供，或者使用 `dotnet.exe` 或 `nuget.exe` CLI 工具。

- Visual Studio for Mac：特定 NuGet 功能是直接内置的。 请参阅[在项目中添加 NuGet 包](/visualstudio/mac/nuget-walkthrough)，获取有关演练。 对于其他功能，请使用 `dotnet.exe` 或 `nuget.exe` CLI 工具。

- Windows 上的 Visual Studio：Visual Studio 2012 及更高版本中都包括“NuGet 包管理器”  。 Visual Studio 提供[包管理器 UI](consume-packages/install-use-packages-visual-studio.md) 和[包管理器控制台](consume-packages/install-use-packages-powershell.md)，通过它可以运行大部分的 NuGet 操作。
  - 从 Visual Studio 2017 开始，安装程序包括具有任何采用 .NET 的工作负荷的 NuGet 包管理器。 若要单独安装，或验证是否已安装包管理器，运行 Visual Studio 安装程序，并检查“各个组件”>“代码工具”>“NuGet 包管理器”下的选项  。
  - 程序包管理器 UI 和控制台对于 Windows 上的 Visual Studio 是唯一的。 目前，它们在 Visual Studio for Mac 上不可用。
  - 支持 IDE 中的 NuGet 功能需要 CLI 工具。 可以使用 `dotnet` CLI 或 `nuget.exe` CLI。 `dotnet` CLI 随某些 Visual Studio 工作负载一起安装，例如 .NET Core。 如前面所述，必须单独安装 `nuget.exe` CLI。
  - 程序包管理器控制台命令只能在 Windows 的 Visual Studio 中工作，不能在其他 PowerShell 环境中工作。
  - 对于 Visual Studio 2010 及更早版本，请安装“适用于 Visual Studio 的 NuGet 包管理器”扩展。
  - 适用于 Visual Studio 2013 和 2015 的 NuGet 扩展也可以从 [https://dist.nuget.org/index.html](https://dist.nuget.org/index.html) 下载。
  - 如果希望预览即将推出的 NuGet 功能，请安装 [Visual Studio 预览版](https://www.visualstudio.com/vs/preview/)，该版本与 Visual Studio 稳定版本并行工作。 若要报告问题或分享对预览版的看法，请在 [NuGet GitHub 存储库](https://github.com/Nuget/Home/issues)上打开问题。

## <a name="feature-availability"></a>功能可用性

| 功能 | dotnet CLI | nuget CLI (Windows) | nuget CLI (Mono) | Visual Studio (Windows) | Visual Studio for Mac |
| --- | --- | --- | --- | --- | --- |
| 搜索包 |  | &#10004; | &#10004; | &#10004; | &#10004; |
| 安装/卸载包 | &#10004; | &#10004;(1) | &#10004; | &#10004; | &#10004; |
| 更新包 | &#10004; | &#10004; | | &#10004; | &#10004; |
| 还原包 | &#10004; | &#10004; | &#10004;(2) | &#10004; | &#10004; |
| 管理包源（来源） | | &#10004; | &#10004; | &#10004; | &#10004; |
| 在源上管理包 | &#10004; | &#10004; | &#10004; | | |
| 设置源的 API 密钥 | | &#10004; | &#10004; | | |
| 创建包(3) | &#10004; | &#10004; | &#10004;(4) | &#10004; | |
| 发布包 | &#10004; | &#10004; | &#10004; | &#10004; |  |
| 复制包 |  | &#10004; | &#10004; | | |
| 管理 global-packages  文件夹和缓存文件夹。 | &#10004; | &#10004; | &#10004; | | |
| 管理 NuGet 配置 | | &#10004; | &#10004; | | |

(1) 不影响项目文件；改用 `dotnet.exe`。

(2) 仅适用于 `packages.config` 文件，不适用于解决方案 (`.sln`) 文件。

(3) 只能通过 CLI 使用各种高级包功能，因为 Visual Studio UI 工具中没有它们。

(4) 适用于 `.nuspec` 文件，但不适用于项目文件。

### <a name="related-topics"></a>相关主题

- [使用 Visual Studio 安装和管理包](consume-packages/install-use-packages-visual-studio.md)
- [使用 PowerShell 安装和管理包](consume-packages/install-use-packages-powershell.md)
- [使用 dotnet CLI 安装和管理包](consume-packages/install-use-packages-dotnet-cli.md)
- [使用 nuget.exe CLI 安装和管理包](consume-packages/install-use-packages-nuget-cli.md)
- [包管理器控制台 PowerShell 引用](reference/powershell-reference.md)
- [创建包](create-packages/creating-a-package.md)
- [发布包](nuget-org/publish-a-package.md)

在 Windows 上工作的开发人员还可以浏览 [NuGet 包资源管理器](https://github.com/NuGetPackageExplorer/NuGetPackageExplorer)，它是可直观浏览、创建和编辑 NuGet 包的独立开源工具。 它非常有用，例如，无需重新生成包即可对包结构进行实验性更改。
