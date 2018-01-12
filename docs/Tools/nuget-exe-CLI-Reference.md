---
title: "NuGet 命令行界面 (CLI) 参考 |Microsoft 文档"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 10/24/2017
ms.topic: reference
ms.prod: nuget
ms.technology: 
ms.assetid: d777c424-0cf3-4bc0-8abd-7ca16c22192b
description: "Nuget.exe CLI 命令行参考索引"
keywords: "nuget.exe 引用索引、 nuget.exe 命令行界面、 nuget.exe CLI、 nuget 命令"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 5dba358b1dda46f551721461e0460219f8210f9a
ms.sourcegitcommit: bdcd2046b1b187d8b59716b9571142c02181c8fb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/10/2018
---
# <a name="nuget-cli-reference"></a>NuGet CLI 参考

NuGet 命令行界面 (CLI)， `nuget.exe`，提供了 NuGet 功能安装、 创建、 发布和管理包而无需进行任何更改的项目文件的完全程度。

若要使用任何命令，请打开命令窗口或 bash shell，然后运行`nuget`跟的命令和相应的选项，如`nuget help pack`（若要查看包命令上的帮助）。

本文档将反映最新版本的 NuGet CLI。 对于你使用的任何给定版本的准确详细信息，运行`nuget help`所需的命令。

## <a name="installing-nugetexe"></a>安装 nuget.exe

[!INCLUDE[install-cli](../includes/install-cli.md)]

## <a name="availability"></a>可用性

- 在 Windows 上的所有命令都都可用。
- 所有命令都使用[Mono 上运行的 nuget.exe](../guides/install-nuget.md#mac-osx-and-linux)为指明除外`pack`， `restore`，和`update`。
- `pack`， `restore`， `delete`， `locals`，和`push`命令也是适用于 Mac 和 Linux 通过[dotnet CLI](dotnet-Commands.md)。

## <a name="commands-and-applicability"></a>命令和适用性

可用的命令和适用于创建包、 包消耗和/或发布到主机的包：

| 常见的命令 | 适当的角色 | NuGet 版本 | 描述 |
| --- | --- | --- | --- |
| [pack](cli-ref-pack.md) | 创建 | 2.7+ | 创建从 NuGet 包`.nuspec`或项目文件。 Mono 上运行时，不支持从项目文件创建包。 |
| [push](cli-ref-push.md) | 发布 | 全部 | 将包发布到包源。 |
| [config](cli-ref-config.md) | 全部 | 全部 | 获取或设置 NuGet 配置值。 |
| [help or ?](cli-ref-help.md) | 全部 | 全部 | 显示帮助信息或命令的帮助。 |
| [locals](cli-ref-locals.md) | 使用 | 3.3+ | 清除或列出各种缓存或全局包文件夹中中的包或标识这些文件夹。 |
| [restore](cli-ref-restore.md) | 使用 | 2.7+ | 还原引用使用的包引用格式的所有包。 Mono 上运行时，不支持还原使用 PackageReference 格式的包。 |
| [setapikey](cli-ref-setapikey.md) | 发布消耗 | 全部 | 该包源需要访问密钥时，将保存给定的包源的 API 密钥。 |
| [spec](cli-ref-spec.md) | 创建 | 全部 | 生成`.nuspec`文件，请使用令牌，如果从 Visual Studio 项目中生成文件。 |


| 辅助命令 | 适当的角色 | NuGet 版本 | 描述 |
| --- | --- | --- | --- |
| [add](cli-ref-add.md) | 发布 | 3.3+ | 将程序包添加到使用层次结构布局非 HTTP 包源。 对于 HTTP 源使用*推送*。 |
| [delete](cli-ref-delete.md) | 发布 | 全部 | 删除或 unlists 从包源的包。 |
| [init](cli-ref-init.md) | 创建 | 3.3+ | 将包从文件夹添加到包源使用层次结构布局。 |
| [install](cli-ref-install.md) | 使用 | 全部 | 某个到当前的包的安装项目，但不修改的项目或引用文件。 |
| [list](cli-ref-list.md) | 消耗，可能发布 | 全部 | 显示从给定的源的包。 |
| [mirror](cli-ref-mirror.md) | 发布 | 3.2 + 中不推荐使用 | 镜像包和从源到目标存储库及其依赖项。 |
| [sources](cli-ref-sources.md) | 消耗发布 | 全部 | 管理配置文件中的包源。 |
| [update](cli-ref-update.md) | 使用 | 全部 | 更新为最新的可用版本的项目的包。 不支持在 Mono 上运行时。 |

不同的命令，请使用的各种[环境变量](cli-ref-environment-variables.md)。

通过适当的角色的 NuGet CLI 命令：

| 角色 | 命令 |
| --- | --- |
| 使用 | `config`, `help`, `install`, `list`, `locals`, `restore`, `setapikey`, `sources`, `update` |
| 创建 | `config`, `help`, `init`, `pack`, `spec` |
| 发布 | `add`, `config`, `delete`, `help`, `list`, `push`, `setapikey`, `sources` |

例如，开发人员来说仅与使用包，只需理解该子集的 NuGet 命令。

> [!Note]
> 命令选项名称不区分大小写。 不推荐使用的选项中未包括此引用，如`NoPrompt`(替换为`NonInteractive`) 和`Verbose`(替换为`Verbosity`)。
