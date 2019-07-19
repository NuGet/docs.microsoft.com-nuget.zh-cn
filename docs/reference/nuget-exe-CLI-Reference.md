---
title: NuGet 命令行接口 (CLI) 参考
description: Nuget.exe CLI 的命令行参考索引
author: karann-msft
ms.author: karann
ms.date: 01/23/2018
ms.topic: reference
ms.openlocfilehash: 52aa2c533a8b67ae10455888a34a7ac9767fd0e3
ms.sourcegitcommit: efc18d484fdf0c7a8979b564dcb191c030601bb4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/18/2019
ms.locfileid: "68327464"
---
# <a name="nuget-cli-reference"></a>NuGet CLI 参考

Nuget 命令行接口 (CLI) `nuget.exe`提供了完整的 nuget 功能, 可用于安装、创建、发布和管理包, 而无需对项目文件进行任何更改。

若要使用任何命令, 请打开命令窗口或 bash shell, 然后`nuget`运行命令和相应的选项, `nuget help pack`如 (以查看 pack 命令的帮助)。

本文档反映了最新版本的 NuGet CLI。 有关所使用的任何给定版本的确切详细信息, 请`nuget help`运行以获取所需的命令。

要了解如何在 `nuget.exe` CLI 中使用基本命令，请参阅[使用 nuget.exe CLI 安装并使用包](../consume-packages/install-use-packages-nuget-cli.md)。

## <a name="installing-nugetexe"></a>安装 nuget.exe

[!INCLUDE [install-cli](../includes/install-cli.md)]

> [!Tip]
> 若要使 NuGet CLI 在 Visual Studio 的包管理器控制台内可用, 请参阅[控制台中的使用 NUGET.EXE cli](../consume-packages/install-use-packages-powershell.md#use-the-nugetexe-cli-in-the-console)。

## <a name="availability"></a>可用性

有关详细信息, 请参阅[功能可用性](../install-nuget-client-tools.md#feature-availability)。

- 所有命令都在 Windows 上可用。
- 除为、和`pack` `update`指示的情况外, `restore`所有命令都使用在 Mono 上运行的 nuget.exe。
- `locals` `restore` `delete`在 Mac 和 Linux 上`push` , 通过 dotnet CLI 还可以使用、、、和命令。 `pack`

## <a name="commands-and-applicability"></a>命令和适用性

可用命令和对包创建、包使用和/或将包发布到主机的适用性:

| 常见命令 | 适用的角色 | NuGet 版本 | 描述 |
| --- | --- | --- | --- |
| [pack](cli-reference/cli-ref-pack.md) | 建立 | 2.7+ | 从`.nuspec`或项目文件创建 NuGet 包。 在 Mono 上运行时, 不支持从项目文件创建包。 |
| [push](cli-reference/cli-ref-push.md) | 发布 | 全部 | 将包发布到包源。 |
| [config](cli-reference/cli-ref-config.md) | 全部 | 全部 | 获取或设置 NuGet 配置值。 |
| [help or ?](cli-reference/cli-ref-help.md) | 全部 | 全部 | 显示命令的帮助信息或帮助。 |
| [locals](cli-reference/cli-ref-locals.md) | 使用 | 3.3+ | 列出*全局包*、 *http 缓存*和*临时*文件夹的位置, 并清除这些文件夹的内容。 |
| [restore](cli-reference/cli-ref-restore.md) | 使用 | 2.7+ | 还原使用中的包管理格式所引用的所有包。 在 Mono 上运行时, 不支持使用 PackageReference 格式还原包。 |
| [setapikey](cli-reference/cli-ref-setapikey.md) | 发布, 消耗 | 全部 | 当包源需要访问密钥时, 保存给定包源的 API 密钥。 |
| [spec](cli-reference/cli-ref-spec.md) | 建立 | 全部 | 如果从`.nuspec` Visual Studio 项目生成文件, 则使用标记生成一个文件。 |

| 辅助命令 | 适用的角色 | NuGet 版本 | 描述 |
| --- | --- | --- | --- |
| [add](cli-reference/cli-ref-add.md) | 发布 | 3.3+ | 使用分层布局将包添加到非 HTTP 包源。 对于 HTTP 源, 请使用*push*。 |
| [delete](cli-reference/cli-ref-delete.md) | 发布 | 全部 | 从包源中删除或取消列出包。 |
| [init](cli-reference/cli-ref-init.md) | 建立 | 3.3+ | 使用分层布局, 将文件夹中的包添加到包源。 |
| [install](cli-reference/cli-ref-install.md) | 使用 | 全部 | 将包安装到当前项目中, 但不修改项目或引用文件。 |
| [list](cli-reference/cli-ref-list.md) | 消耗, 可能正在发布 | 全部 | 显示来自给定源的包。 |
| [mirror](cli-reference/cli-ref-mirror.md) | 发布 | 3\.2 + 中弃用 | 将包及其依赖项从源存储库镜像到目标存储库。 |
| [sources](cli-reference/cli-ref-sources.md) | 消耗, 发布 | 全部 | 管理配置文件中的包源。 |
| [update](cli-reference/cli-ref-update.md) | 使用 | 全部 | 将项目的包更新为最新的可用版本。 在 Mono 上运行时不受支持。 |

不同的命令使用各种[环境变量](cli-reference/cli-ref-environment-variables.md)。

按适用角色的 NuGet CLI 命令:

| 角色 | 命令 |
| --- | --- |
| 使用 | `config`、`help`、`install`、`list`、`locals`、`restore`、`setapikey`、`sources`、`update` |
| 建立 | `config`, `help`, `init`, `pack`, `spec` |
| 发布 | `add`, `config`, `delete`, `help`, `list`, `push`, `setapikey`, `sources` |

例如, 仅关注使用包的开发人员只需了解 NuGet 命令的子集。

> [!Note]
> 命令选项名称不区分大小写。 不推荐使用的选项不包括在此引用中, 如`NoPrompt` ( `NonInteractive`替换为`Verbosity`) 和`Verbose` (替换为)。
