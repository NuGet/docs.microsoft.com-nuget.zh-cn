---
title: NuGet CLI config 命令
description: 针对 nuget.exe config 命令的参考
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 384e708187a747221de103720cc51af07acf713e
ms.sourcegitcommit: f9e39ff9ca19ba4a26e52b8a5e01e18eb0de5387
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/24/2019
ms.locfileid: "68433321"
---
# <a name="config-command-nuget-cli"></a>config 命令 (NuGet CLI)

**适用于:** 所有&bullet; **受支持的版本**: 全部

获取或设置 NuGet 配置值。 有关其他用法, 请参阅[常见 NuGet 配置](../../consume-packages/configuring-nuget-behavior.md)。 有关允许的密钥名称的详细信息, 请参阅[NuGet 配置文件参考](../nuget-config-file.md)。

## <a name="usage"></a>用法

```cli
nuget config -Set <name>=[<value>] [<name>=<value> ...] [options]
nuget config -AsPath <name> [options]
```

其中`<name>` , `<value>`并指定要在配置中设置的键值对。 您可以根据需要指定任意数量对。 若要删除值, 请指定名称和`=`符号但不指定值。

有关允许的密钥名称, 请参阅[NuGet 配置文件参考](../nuget-config-file.md)。

在 NuGet 3.4 + 中`<value>` , 可以使用[环境变量](cli-ref-environment-variables.md)。

## <a name="options"></a>选项

| 选项 | 描述 |
| --- | --- |
| AsPath | 将配置值作为路径返回, 使用时`-Set`将忽略此值。 |
| ConfigFile | 要修改的 NuGet 配置文件。 如果未指定, 则使用默认文件-`%AppData%\NuGet\NuGet.Config` (Windows) 或`~/.config/NuGet/NuGet.Config` (Mac/Linux) 或`~/.nuget/NuGet/NuGet.Config` (因 OS 分发而异)。|
| ForceEnglishOutput | *(3.5 +)* 使用固定的、基于英语的区域性强制执行 nuget.exe。 |
| Help | 显示命令的帮助信息。 |
| NonInteractive | 取消显示提示用户输入或确认。 |
| Verbosity | 指定在输出中显示的详细信息量: "*正常*"、"*静默*"、"*详细*"。 |

另请参阅[环境变量](cli-ref-environment-variables.md)

### <a name="examples"></a>示例

```cli
nuget config -Set repositoryPath=c:\packages -configfile c:\my.config

nuget config -Set repositoryPath=

nuget config -Set repositoryPath=%PACKAGE_REPO% -configfile %ProgramData%\NuGet\NuGetDefaults.Config

nuget config -Set HTTP_PROXY=http://127.0.0.1 -set HTTP_PROXY.USER=domain\user
```
