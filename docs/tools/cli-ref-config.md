---
title: NuGet CLI config 命令
description: Nuget.exe config 命令参考
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 376b69186ad22d4d94a1df51146b833a1f6f9bd9
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/04/2018
ms.locfileid: "43546473"
---
# <a name="config-command-nuget-cli"></a>配置命令 (NuGet CLI)

**适用于：** 所有&bullet;**支持的版本**： 所有

获取或设置 NuGet 配置值。 有关其他用法，请参阅[配置 NuGet 行为](../consume-packages/configuring-nuget-behavior.md)。 有关允许的密钥名称的详细信息，请参阅[NuGet 配置文件引用](../reference/nuget-config-file.md)。

## <a name="usage"></a>用法

```cli
nuget config -Set <name>=[<value>] [<name>=<value> ...] [options]
nuget config -AsPath <name> [options]
```

其中`<name>`和`<value>`指定要在配置中设置的键-值对。 您可以根据需要指定任意多个对。 若要删除一个值，指定名称和`=`登录而没有值。

有关允许的密钥名称，请参阅[NuGet 配置文件引用](../reference/nuget-config-file.md)。

在 NuGet 3.4 + 中，`<value>`可以使用[环境变量](cli-ref-environment-variables.md)。

## <a name="options"></a>选项

| 选项 | 描述 |
| --- | --- |
| AsPath | 返回配置值作为路径，忽略时`-Set`使用。 |
| ConfigFile | 要修改的 NuGet 配置文件。 如果未指定，否则`%AppData%\NuGet\NuGet.Config`(Windows) 或`~/.nuget/NuGet/NuGet.Config`(Mac/Linux) 使用。|
| ForceEnglishOutput | *（3.5 +)* 强制 nuget.exe 以运行使用固定的、 基于英语的区域性。 |
| Help | 显示的帮助命令的信息。 |
| NonInteractive | 取消显示提示用户输入或确认。 |
| Verbosity | 指定的输出中显示的详细信息：*正常*，*静默*，*详细*。 |

另请参阅[环境变量](cli-ref-environment-variables.md)

### <a name="examples"></a>示例

```cli
nuget config -Set repositoryPath=c:\packages -configfile c:\my.config

nuget config -Set repositoryPath=

nuget config -Set repositoryPath=%PACKAGE_REPO% -configfile %ProgramData%\NuGet\NuGetDefaults.Config

nuget config -Set HTTP_PROXY=http://127.0.0.1 -set HTTP_PROXY.USER=domain\user
```
