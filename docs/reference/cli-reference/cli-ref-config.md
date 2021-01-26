---
title: NuGet CLI config 命令
description: nuget.exe config 命令的参考
author: JonDouglas
ms.author: jodou
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 3d50c12e34f71d7a62fe177da1dbb33eb702347a
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/26/2021
ms.locfileid: "98775959"
---
# <a name="config-command-nuget-cli"></a>配置命令 (NuGet CLI) 

**适用于：** 所有 &bullet; **受支持的版本**：全部

获取或设置 NuGet 配置值。 有关其他用法，请参阅 [常见 NuGet 配置](../../consume-packages/configuring-nuget-behavior.md)。 有关允许的密钥名称的详细信息，请参阅 [NuGet 配置文件参考](../nuget-config-file.md)。

## <a name="usage"></a>使用情况

```cli
nuget config -Set <name>=[<value>] [<name>=<value> ...] [options]
nuget config -AsPath <name> [options]
```

其中 `<name>` ，并 `<value>` 指定要在配置中设置的键值对。 您可以根据需要指定任意数量对。 若要删除值，请指定名称和 `=` 符号但不指定值。

有关允许的密钥名称，请参阅 [NuGet 配置文件参考](../nuget-config-file.md)。

在 NuGet 3.4 + 中， `<value>` 可以使用 [环境变量](cli-ref-environment-variables.md)。

## <a name="options"></a>选项


- **`AsPath`**

  将配置值作为路径返回，使用时将忽略此值 `-Set` 。

- **`-ConfigFile`**

  要应用的 NuGet 配置文件。 如果未指定，则 `%AppData%\NuGet\NuGet.Config` 使用 (Windows) `~/.nuget/NuGet/NuGet.Config` 或 `~/.config/NuGet/NuGet.Config` (Mac/Linux) 。

- **`-ForceEnglishOutput`**

  *(3.5 +)* 使用固定的、基于英语的区域性强制运行 nuget.exe。

- **`-?|-help`**

  显示命令的帮助信息。

- **`-NonInteractive`**

  禁止提示用户输入或确认。

- **`-Set`**

  要在配置中设置的键/值对的一个。

- **`-Verbosity [normal|quiet|detailed]`**

  指定在输出中显示的详细信息的数量： `normal` (默认) 、 `quiet` 或 `detailed` 。

另请参阅 [环境变量](cli-ref-environment-variables.md)

### <a name="examples"></a>示例

```cli
nuget config -Set repositoryPath=c:\packages -configfile c:\my.config

nuget config -Set repositoryPath=

nuget config -Set repositoryPath=%PACKAGE_REPO% -configfile %ProgramData%\NuGet\NuGetDefaults.Config

nuget config -Set HTTP_PROXY=http://127.0.0.1 -set HTTP_PROXY.USER=domain\user
```
