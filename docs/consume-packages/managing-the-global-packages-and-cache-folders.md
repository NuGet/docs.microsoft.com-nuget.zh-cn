---
title: 如何管理 NuGet 中的全局包、缓存、临时文件夹
description: 如何管理计算机上存在的全局包安装文件夹、包缓存和临时文件夹，这些在安装、还原和更新包时将用到。
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 03/19/2018
ms.topic: conceptual
ms.openlocfilehash: 545e658d26b557f27d6534bf677f467e65a315b4
ms.sourcegitcommit: 8d5121af528e68789485405e24e2100fda2868d6
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/23/2018
ms.locfileid: "42793613"
---
# <a name="managing-the-global-packages-cache-and-temp-folders"></a>管理全局包、缓存和临时文件夹

每当安装、更新或还原包时，NuGet 将管理项目结构多个文件夹之外的包和包信息：

| name | 说明和位置（每个用户）|
| --- | --- |
| global&#8209;packages | global-packages 文件夹是 NuGet 安装任何下载包的位置。 每个包完全展开到匹配包标识符和版本号的子文件夹。 使用 PackageReference 格式的项目总是直接从该文件夹中使用包。 使用 `packages.config` 时，包将安装到 global-packages 文件夹，然后复制到项目的 `packages` 文件夹。<br/><ul><li>Windows：`%userprofile%\.nuget\packages`</li><li>Mac/Linux：`~/.nuget/packages`</li><li>使用 NUGET_PACKAGES 重写环境变量 `globalPackagesFolder` 或 `repositoryPath` [配置设置](../reference/nuget-config-file.md#config-section)（分别在使用 PackageReference 和 `packages.config` 时）或 `RestorePackagesPath` MSBuild 属性（仅限 MSBuild）。 环境变量优先于配置设置。</li></ul> |
| http&#8209;cache | Visual Studio 包管理器 (NuGet 3.x+) 和 `dotnet` 工具存储此缓存中下载包的副本（另存为 `.dat` 文件），这些副本被组织到每个包源的子文件夹中。 未展开包，且缓存中有 30 分钟的到期时间。<br/><ul><li>Windows：`%localappdata%\NuGet\v3-cache`</li><li>Mac/Linux：`~/.local/share/NuGet/v3-cache`</li><li>使用 NUGET_HTTP_CACHE_PATH 环境变量替代。</li></ul> |
| temp | NuGet 在各操作期间在其中存储临时文件的文件夹。<br/><li>Windows：`%temp%\NuGetScratch`</li><li>Mac/Linux：`/tmp/NuGetScratch`</li></ul> |
| plugins-cache **4.8 +** | NuGet 存储来自操作声明请求的结果的文件夹。<br/><ul><li>Windows：`%localappdata%\NuGet\plugins-cache`</li><li>Mac/Linux：`~/.local/share/NuGet/plugins-cache`</li><li>使用 NUGET_PLUGINS_CACHE_PATH 环境变量替代。</li></ul> |

> [!Note]
> NuGet 3.5 和早期版本使用 `%localappdata%\NuGet\Cache` 中的 packages-cache 而不是 http-cache。

通过使用缓存和 global-packages 文件夹，NuGet 通常会避免下载计算机上已存在的包，以提高安装、更新和还原操作的性能。 在使用 PackageReference 时，global-packages 文件夹还会避免在项目文件夹中保存下载的包，其中它们可能会在无意间被添加到源代码管理，并减少 NuGet 对计算机存储的总体影响。

当要求检索包时，NuGet 会首先查看 global-packages 文件夹。 如果不存在包的确切版本，NuGet 将检查所有非 HTTP 包源。 如果仍未找到包，NuGet 将查找 http-cache 中的包，除非使用 `dotnet.exe` 命令指定 `--no-cache`，或使用 `nuget.exe` 命令指定 `-NoCache`。 如果包不在缓存中，或未使用缓存，那么 NuGet 将通过 HTTP 检索包。

有关详细信息，请参阅[安装包时会发生什么情况](ways-to-install-a-package.md#what-happens-when-a-package-is-installed)。

## <a name="viewing-folder-locations"></a>查看文件夹位置

可以使用 [nuget locals 命令](../tools/cli-ref-locals.md)查看位置：

```cli
# Display locals for all folders: global-packages, http cache, temp and plugins cache
nuget locals all -list
```

典型输出（Windows；“user1”为当前用户名）：

```output
http-cache: C:\Users\user1\AppData\Local\NuGet\v3-cache
global-packages: C:\Users\user1\.nuget\packages\
temp: C:\Users\user1\AppData\Local\Temp\NuGetScratch
plugins-cache: C:\Users\user1\AppData\Local\NuGet\plugins-cache
```

（`package-cache` 在 NuGet 2.x 中使用，并在 NuGet 3.5 及更早版本中显示。）

还可以使用 [dotnet nuget locals 命令](/dotnet/core/tools/dotnet-nuget-locals)查看文件夹位置：

```cli
dotnet nuget locals all --list
```

典型输出（Mac/Linux；“user1”为当前用户名）：

```output
info : http-cache: /home/user1/.local/share/NuGet/v3-cache
info : global-packages: /home/user1/.nuget/packages/
info : temp: /tmp/NuGetScratch
info : plugins-cache: /home/user1/.local/share/NuGet/plugins-cache
```

若要显示单个文件夹的位置，请使用 `http-cache`、`global-packages`、`temp` 或 `plugins-cache`，而不是 `all`。

## <a name="clearing-local-folders"></a>清除本地文件夹

如果安装包时遇到问题或想要确保从远程库安装包，请使用 `locals --clear` 选项 (dotnet.exe) 或 `locals -clear` (nuget.exe)，指定要清除的文件夹，或使用 `all` 清除所有文件夹：

```cli
# Clear the 3.x+ cache (use either command)
dotnet nuget locals http-cache --clear
nuget locals http-cache -clear

# Clear the 2.x cache (NuGet CLI 3.5 and earlier only)
nuget locals packages-cache -clear

# Clear the global packages folder (use either command)
dotnet nuget locals global-packages --clear
nuget locals global-packages -clear

# Clear the temporary cache (use either command)
dotnet nuget locals temp --clear
nuget locals temp -clear

# Clear the plugins cache (use either command)
dotnet nuget locals plugins-cache --clear
nuget locals plugins-cache -clear

# Clear all caches (use either command)
dotnet nuget locals all --clear
nuget locals all -clear
```

目前在 Visual Studio 中打开的项目所使用的任何包都不会从 global-packages 文件夹中清除。

在 Visual Studio 2017 中，使用“工具”>“NuGet 包管理器”>“包管理器设置”菜单命令，然后选择“清除所有 NuGet 缓存”。 管理缓存目前不支持通过包管理器控制台提供。 在 Visual Studio 2015 中，则改用 CLI 命令。

![用于清除缓存的 NuGet 选项命令](media/options-clear-caches.png)

## <a name="troubleshooting-errors"></a>错误疑难解答

使用 `nuget locals` 或 `dotnet nuget locals` 时可能出现以下错误：

- 错误：进程无法访问文件 <package>，因为另一个进程正在使用该文件或清除本地资源失败：无法删除一个或多个文件

    另一个进程正在使用文件夹中的一个或多个文件；例如，Visual Studio 项目处于打开状态，它指的是 global-packages 文件夹中的包。 关闭这些进程，然后重试。

- 错误：访问路径 <path> 被拒绝或目录不为空

    你没有删除缓存文件的权限。 如果可能，请更改文件夹权限，然后重试。 否则，请与系统管理员联系。

- 错误：指定的路径、文件名或两者太长。*完全限定文件名必须少于 260 个字符，而目录名必须少于 248 个字符。*

    缩短文件夹名称，然后重试。
