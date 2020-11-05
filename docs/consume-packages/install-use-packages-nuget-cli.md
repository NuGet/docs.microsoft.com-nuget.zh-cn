---
title: 使用 nuget.exe CLI 管理 NuGet 包
description: 有关使用 nuget.exe CLI 处理 NuGet 包的说明。
author: mikejo5000
ms.author: mikejo
ms.date: 06/03/2019
ms.topic: conceptual
ms.openlocfilehash: 7039dd27f2dddebc3c84e5ad35d5efec59547792
ms.sourcegitcommit: b138bc1d49fbf13b63d975c581a53be4283b7ebf
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/03/2020
ms.locfileid: "93237382"
---
# <a name="manage-packages-using-the-nugetexe-cli"></a>使用 nuget.exe CLI 管理包

通过 CLI 工具可轻松更新和还原项目和解决方案中的 NuGet 包。 该工具提供 Windows 上的所有 NuGet 功能以及 Mac 和 Linux 上在 Mono 下运行时的大多数功能。

`nuget.exe` CLI 适用于 .NET Framework 项目和非 SDK 样式项目（例如，面向 .NET Standard 库的非 SDK 样式项目）。 如果你使用的是已迁移到 `PackageReference` 的非 SDK 样式项目，请改用 `dotnet` CLI。 `nuget.exe` CLI 需要 [packages.config](../reference/packages-config.md) 文件来进行包引用。

> [!NOTE]
> 在大多数情况下，建议[将使用 `packages.config` 的非 SDK 样式项目迁移至 PackageReference](../consume-packages/migrate-packages-config-to-package-reference.md)，然后可以使用 `dotnet` CLI 而不是 `nuget.exe` CLI。 目前，C++ 和 ASP.NET 项目无法进行迁移。

本文介绍了一些最常见的 `nuget.exe` CLI 命令的基本用法。 对于大多数这些命令，CLI 工具在当前目录中查找项目文件，除非在命令中指定了项目文件。 有关命令和可能使用的参数的完整列表，请参阅 [nuget.exe CLI 参考](../reference/nuget-exe-cli-reference.md)。

## <a name="prerequisites"></a>必备条件

- 要安装 `nuget.exe` CLI，从 [nuget.org](https://dist.nuget.org/win-x86-commandline/latest/nuget.exe) 下载它，将 `.exe` 文件保存到合适的文件夹，然后将该文件夹添加到 PATH 环境变量中。

## <a name="install-a-package"></a>安装包

[install](../reference/cli-reference/cli-ref-install.md) 命令使用指定的包源将包下载并安装到项目中，默认为当前文件夹。 将新包安装到项目根目录的“包”文件夹中  。

> [!IMPORTANT]
> `install` 命令不会修改项目文件或 packages.config  ；在这种方式下，它类似于 `restore`，因为它只向磁盘添加包，而不更改项目的依赖项。 要添加依赖项，请通过 Visual Studio 中的包管理器 UI 或控制台添加包，或修改 packages.config  ，然后运行 `install` 或 `restore`。

1. 打开命令行并切换到包含项目文件的目录。

2. 使用以下命令将 NuGet 包安装到“包”文件夹  。

    ```cli
    nuget install <packageID> -OutputDirectory packages
    ```

    要将 `Newtonsoft.json` 包安装到“包”文件夹，请使用以下命令  ：

    ```cli
    nuget install Newtonsoft.Json -OutputDirectory packages
    ```

或者可以使用以下命令将现有 `packages.config` 文件的 NuGet 包安装到“包”  文件夹。 该操作不会将包添加到项目依赖项中，而是在本地安装它。

```cli
nuget install packages.config -OutputDirectory packages
```

## <a name="install-a-specific-version-of-a-package"></a>安装特定版本的包

如果在使用 [install](../reference/cli-reference/cli-ref-install.md) 命令时未指定版本，NuGet 将安装最新版本的包。 还可以安装特定版本的 Nuget 包：

```cli
nuget install <packageID | configFilePath> -Version <version>
```

例如，要添加 `Newtonsoft.json` 包的 12.0.1 版，请使用以下命令：

```cli
nuget install Newtonsoft.Json -Version 12.0.1
```

有关 `install` 的限制和行为的详细信息，请参阅[安装包](#install-a-package)。

## <a name="remove-a-package"></a>删除包

要删除一个或多个包，请从“包”文件夹中删除要删除的包  。

如果要重新安装包，请使用 `restore` 或 `install` 命令。

## <a name="list-packages"></a>列出包

可以使用 [list](../reference/cli-reference/cli-ref-list.md) 命令显示给定源的包列表。 使用 `-Source` 选项限制搜索。

```cli
nuget list -Source <source>
```

例如，列出“包”文件夹中的包  。

```cli
nuget list -Source C:\Users\username\source\repos\MyProject\packages
```

如果使用搜索词，则搜索包括包名称、标记和包描述。

```cli
nuget list <search term>
```

## <a name="update-an-individual-package"></a>更新单个包

除非指定包版本，否则 NuGet 会在使用 `install` 命令时安装最新版本的包。

## <a name="update-all-packages"></a>更新所有包

使用 [update](../reference/cli-reference/cli-ref-update.md) 命令更新所有包。 将项目中的所有包（使用 `packages.config`）更新为其最新可用版本。 建议在运行 `update` 之前运行 `restore`。

```cli
nuget update
```

## <a name="restore-packages"></a>还原包

[!INCLUDE [restore-nuget-exe-cli](includes/restore-nuget-exe-cli.md)]

## <a name="get-the-cli-version"></a>获取 CLI 版本

使用此命令：

```cli
nuget help
```

帮助输出中的第一行显示版本。 若要避免向上滚动，请改用 `nuget help | more`。