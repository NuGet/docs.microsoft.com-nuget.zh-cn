---
title: NuGet 命令行接口 (CLI) 参考
description: Nuget.exe CLI 命令行参考索引
author: karann-msft
ms.author: karann
ms.date: 01/23/2018
ms.topic: reference
ms.openlocfilehash: a257dbbd9d56b5989e050ed4096d096cd1036184
ms.sourcegitcommit: b6810860b77b2d50aab031040b047c20a333aca3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/28/2019
ms.locfileid: "67426022"
---
# <a name="nuget-cli-reference"></a>NuGet CLI 参考

NuGet 命令行接口 (CLI)， `nuget.exe`，提供了 NuGet 安装、 创建、 发布和管理包而无需对项目文件进行任何更改的功能的完全程度。

若要使用的任何命令，打开命令窗口或 bash shell 中，然后运行`nuget`跟命令和相应的选项，例如`nuget help pack`（若要查看上的包命令的帮助）。

此文档反映了 NuGet CLI 的最新版本。 对于要将任何给定版本的准确详细信息，运行`nuget help`为所需的命令。

若要了解如何使用基本命令与`nuget.exe`CLI，请参阅[安装和使用包使用 nuget.exe CLI](../consume-packages/install-use-packages-nuget-cli.md)。

## <a name="installing-nugetexe"></a>安装 nuget.exe

[!INCLUDE [install-cli](../includes/install-cli.md)]

> [!Tip]
> 若要使 NuGet CLI 中 Visual Studio 包管理器控制台中可用，请参阅[使用 nuget.exe CLI 在控制台中](package-manager-console.md#using-the-nugetexe-cli-in-the-console)。

## <a name="availability"></a>可用性

请参阅[功能可用性](../install-nuget-client-tools.md#feature-availability)的准确详细信息。

- 在 Windows 上提供了所有命令。
- 所有命令都适用于在 Mono 上运行除特别指明为外的 nuget.exe `pack`， `restore`，和`update`。
- `pack`， `restore`， `delete`， `locals`，和`push`命令也是可在 Mac 和 Linux 上通过 dotnet CLI。

## <a name="commands-and-applicability"></a>命令和适用性

可用的命令和适用于创建包、 包使用，和/或发布到主机的包：

| 常用命令 | 适用角色 | NuGet 版本 | 描述 |
| --- | --- | --- | --- |
| [pack](cli-ref-pack.md) | 创建 | 2.7+ | 创建 NuGet 包从`.nuspec`或项目文件。 Mono 上运行时，不支持从项目文件创建包。 |
| [push](cli-ref-push.md) | 发布 | 全部 | 将包发布到包源。 |
| [config](cli-ref-config.md) | 全部 | 全部 | 获取或设置 NuGet 配置值。 |
| [help or ?](cli-ref-help.md) | 全部 | 全部 | 显示帮助信息或命令的帮助。 |
| [locals](cli-ref-locals.md) | 使用 | 3.3+ | 列出的位置*全局包*， *http 缓存*，并*temp*文件夹和清除这些文件夹的内容。 |
| [restore](cli-ref-restore.md) | 使用 | 2.7+ | 还原引用使用的包管理格式的所有包。 Mono 上运行时，不支持还原使用 PackageReference 格式的包。 |
| [setapikey](cli-ref-setapikey.md) | 发布消耗 | 全部 | 该程序包源需要访问密钥时，将保存给定的包源的 API 密钥。 |
| [spec](cli-ref-spec.md) | 创建 | 全部 | 生成`.nuspec`文件，请使用令牌，如果从 Visual Studio 项目生成文件。 |

| 辅助命令 | 适用角色 | NuGet 版本 | 描述 |
| --- | --- | --- | --- |
| [add](cli-ref-add.md) | 发布 | 3.3+ | 将包添加到使用层次结构布局的非 HTTP 包源。 对于 HTTP 源，使用*推送*。 |
| [delete](cli-ref-delete.md) | 发布 | 全部 | 删除或取消列出包从包源。 |
| [init](cli-ref-init.md) | 创建 | 3.3+ | 将包从文件夹添加到使用层次结构布局的包源。 |
| [install](cli-ref-install.md) | 使用 | 全部 | 安装到当前的包的项目，但不修改的项目或引用文件。 |
| [list](cli-ref-list.md) | 使用情况，可能发布 | 全部 | 显示从给定源的包。 |
| [mirror](cli-ref-mirror.md) | 发布 | 3\.2 + 中不推荐使用 | 镜像包和来自源到目标存储库及其依赖项。 |
| [sources](cli-ref-sources.md) | 消耗发布 | 全部 | 管理配置文件中的包源。 |
| [update](cli-ref-update.md) | 使用 | 全部 | 更新到最新版本的项目的包。 不支持在 Mono 上运行时。 |

不同的命令进行使用的各种[环境变量](cli-ref-environment-variables.md)。

适用角色通过 NuGet CLI 命令：

| 角色 | 命令 |
| --- | --- |
| 使用 | `config`、`help`、`install`、`list`、`locals`、`restore`、`setapikey`、`sources`、`update` |
| 创建 | `config`, `help`, `init`, `pack`, `spec` |
| 发布 | `add`, `config`, `delete`, `help`, `list`, `push`, `setapikey`, `sources` |

例如，开发人员仅与使用包，只需理解该子集 NuGet 命令。

> [!Note]
> 命令选项名称不区分大小写。 不推荐使用的选项中不包括此引用，如`NoPrompt`(替换为`NonInteractive`) 和`Verbose`(替换为`Verbosity`)。
