---
title: NuGet CLI 局部变量命令
description: nuget.exe 局部变量命令的参考
author: karann-msft
ms.author: karann
ms.date: 03/19/2018
ms.topic: reference
ms.openlocfilehash: cdc2b760021ffc4a9e02edacb45beac01cc99bf1
ms.sourcegitcommit: cbc87fe51330cdd3eacaad3e8656eb4258882fc7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/19/2020
ms.locfileid: "88623053"
---
# <a name="locals-command-nuget-cli"></a> (NuGet CLI 的局部变量命令) 

**适用于：** 包使用 &bullet; **受支持的版本：** 3.3 +

清除或列出本地 NuGet 资源，例如 *http 缓存*、 *全局包* 文件夹和临时文件夹。 `locals`命令也可用于显示这些位置的列表。 有关详细信息，请参阅 [管理全局包和缓存文件夹](../../consume-packages/managing-the-global-packages-and-cache-folders.md)。

## <a name="usage"></a>使用情况

```cli
nuget locals <folder> [options]
```

其中 `<folder>` `all` ，是、 `http-cache` 、 `packages-cache` * (3.5 及更低版本) *、 `global-packages` `temp` * (3.4 +) *和 `plugins-cache` * (4.8 +) *。

## <a name="options"></a>选项

- **`-Clear`**

  清除指定的文件夹。

- **`-ConfigFile`**

  要应用的 NuGet 配置文件。 如果未指定，则 `%AppData%\NuGet\NuGet.Config` 使用 (Windows) `~/.nuget/NuGet/NuGet.Config` 或 `~/.config/NuGet/NuGet.Config` (Mac/Linux) 。

- **`-ForceEnglishOutput`**

  * (3.5 +) * 使用固定的、基于英语的区域性强制运行 nuget.exe。

- **`-?|-help`**

  显示命令的帮助信息。

- **`-List`**

  列出指定文件夹的位置或所有文件夹在与 *all*一起使用时的位置。

- **`-NonInteractive`**

  禁止提示用户输入或确认。

- **`-Verbosity [normal|quiet|detailed]`**

  指定在输出中显示的详细信息的数量： `normal` (默认) 、 `quiet` 或 `detailed` 。

另请参阅 [环境变量](cli-ref-environment-variables.md)

## <a name="examples"></a>示例

```cli
nuget locals all -list
nuget locals http-cache -clear
```

有关其他示例，请参阅 [管理全局包和缓存文件夹](../../consume-packages/managing-the-global-packages-and-cache-folders.md)。
