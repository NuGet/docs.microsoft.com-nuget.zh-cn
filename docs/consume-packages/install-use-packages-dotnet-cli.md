---
title: 使用 dotnet CLI 安装和管理 NuGet 包
description: 有关使用 dotnet CLI 处理 NuGet 包的说明。
author: mikejo5000
ms.author: mikejo
ms.date: 06/03/2019
ms.topic: conceptual
ms.openlocfilehash: 64f3a1978cd336064a77c9f3872357e65c37fc10
ms.sourcegitcommit: 0dea3b153ef823230a9d5f38351b7cef057cb299
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/12/2019
ms.locfileid: "67842362"
---
# <a name="install-and-manage-packages-using-the-dotnet-cli"></a>使用 dotnet CLI 安装和管理包

通过 CLI 工具可轻松安装、卸载和更新项目和解决方案中的 NuGet 包。 它可在 Windows、Mac OS X 和 Linux 上运行。

dotnet CLI 适用于 .NET Core 和 .NET Standard 项目（SDK 样式的项目类型），以及任何其他 SDK 样式项目（例如，面向 .NET Framework 的 SDK 样式项目）。 有关更多信息，请参阅 [SDK 属性](/dotnet/core/tools/csproj#additions)。

本文介绍了一些最常见的 dotnet CLI 命令的基本用法。 对于这些中的大多数命令，CLI 工具在当前目录中查找项目文件，除非在命令中指定了项目文件（项目文件是一个可选开关）。 如需获取命令的完整列表和可能使用的参数，请参阅 [.NET Core 命令行界面 (CLI) 工具](../tools/dotnet-commands.md)。

## <a name="prerequisites"></a>系统必备

- [.NET Core SDK](https://www.microsoft.com/net/download/)，提供 `dotnet` 命令行工具。 从 Visual Studio 2017 开始，dotnet CLI 将自动随任何与 .NET Core 相关的工作负载一起安装。

## <a name="install-a-package"></a>安装包

[dotnet add package](/dotnet/core/tools/dotnet-add-package?tabs=netcore2x) 添加对项目文件的包引用，然后运行 `dotnet restore` 以安装包。

1. 打开命令行并切换到包含项目文件的目录。

2. 运行以下命令安装 Nuget 包：

    ```cli
    dotnet add package <PACKAGE_NAME>
    ```

    例如，若要安装 `Newtonsoft.Json` 包，请使用以下命令

    ```cli
    dotnet add package Newtonsoft.Json
    ```

3. 命令完成后，查看项目文件以确保已安装该包。

   可以打开 `.csproj` 文件以查看添加的引用：

    ```xml
   <ItemGroup>
    <PackageReference Include="Newtonsoft.Json" Version="12.0.1" />
   </ItemGroup>
    ```

## <a name="install-a-specific-version-of-a-package"></a>安装特定版本的包

如果未指定版本，NuGet 将安装最新版本的包。 还可以使用 [dotnet add package](/dotnet/core/tools/dotnet-add-package?tabs=netcore2x) 命令安装特定版本的 Nuget 包：

```cli
dotnet add package <PACKAGE_NAME> -v <VERSION>
```

例如，要添加 12.0.1 版的 `Newtonsoft.Json` 包，请使用以下命令：

```cli
dotnet add package Newtonsoft.Json -v 12.0.1
```

## <a name="list-package-references"></a>NuGet 包引用

可以使用 [dotnet list package](/dotnet/core/tools/dotnet-list-package?tabs=netcore2x) 命令列出项目的包引用。

```cli
dotnet list package
```

## <a name="remove-a-package"></a>移除包

使用 [dotnet remove package](/dotnet/core/tools/dotnet-remove-package?tabs=netcore2x) 命令从项目文件中移除包引用。

```cli
dotnet remove package <PACKAGE_NAME>
```

例如，要移除 `Newtonsoft.Json` 包，请使用以下命令

```cli
dotnet remove package Newtonsoft.Json
```

## <a name="update-a-package"></a>更新包

除非指定包版本，否则 NuGet 会在使用 `dotnet add package` 命令时安装最新版本的包（`-v` 开关）。

## <a name="restore-packages"></a>还原包

使用 [dotnet restore](/dotnet/core/tools/dotnet-restore?tabs=netcore2x) 命令还原项目文件中列出的包（请参阅 [PackageReference](../consume-packages/package-references-in-project-files.md)）。 使用 .NET Core 2.0 和更高版本，通过 `dotnet build` 和 `dotnet run` 自动完成还原。 从 NuGet 4.0 开始，它运行与 `nuget restore` 相同的代码。

与其他 `dotnet` CLI 命令一样，先打开命令行并切换到包含项目文件的目录。

使用 `dotnet restore` 还原包：

```cli
dotnet restore 
```
