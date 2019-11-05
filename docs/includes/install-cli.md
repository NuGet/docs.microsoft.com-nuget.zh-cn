---
ms.openlocfilehash: 5197447531288a8b071354dbeb3a3ae02f7cce09
ms.sourcegitcommit: 39f2ae79fbbc308e06acf67ee8e24cfcdb2c831b
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/05/2019
ms.locfileid: "73610530"
---
#### <a name="windows"></a>Windows

> [!Note]
> NuGet.exe 5.0 及更高版本需要 .NET Framework 4.7.2 或更高版本才能执行。

1. 请访问 [nuget.org/downloads](https://nuget.org/downloads)，并选择 NuGet 3.3 或更高版本（2.8.6 与 Mono 不兼容）。 始终建议使用最新版。若要将包发布到 nuget.org，版本至少必须是 4.1.0。
1. 每次下载都直接下载 `nuget.exe` 文件。 让浏览器将文件保存到选定文件夹。 此文件不  是安装程序；如果直接在浏览器中运行，就不会看到任何内容。
1. 将文件夹添加到 `nuget.exe` 中放置 PATH 环境变量的位置，这样就可以从任意位置使用 CLI 工具。

#### <a name="macoslinux"></a>macOS/Linux

行为可能因 OS 分发版本略有不同。

1. 安装 [Mono 4.4.2 或更高版本](https://www.mono-project.com/docs/getting-started/install/)。

1. 在 shell 提示符处，执行下列命令：

    ```bash
    # Download the latest stable `nuget.exe` to `/usr/local/bin`
    sudo curl -o /usr/local/bin/nuget.exe https://dist.nuget.org/win-x86-commandline/latest/nuget.exe
    ```

1. 通过将以下脚本添加到 OS 的相应文件来创建别名（通常为 `~/.bash_aliases` 或 `~/.bash_profile`）：

    ```bash
    # Create as alias for nuget
    alias nuget="mono /usr/local/bin/nuget.exe"
    ```

1. 重载 shell。  通过输入 `nuget`（而不使用任何参数）来测试安装。 应该会看到 NuGet CLI 帮助。
