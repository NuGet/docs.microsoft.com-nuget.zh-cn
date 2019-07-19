---
title: NuGet CLI delete 命令
description: Nuget.exe delete 命令的参考
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 5185bc8b89f645a0a0f4d3241b5fa04e09560ede
ms.sourcegitcommit: efc18d484fdf0c7a8979b564dcb191c030601bb4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/18/2019
ms.locfileid: "68327834"
---
# <a name="delete-command-nuget-cli"></a>delete 命令 (NuGet CLI)

**适用于:** 包发布&bullet; **支持的版本:** 全部

从包源中删除或取消列出包。 对于 nuget.org, delete 命令[取消列出包](../../nuget-org/policies/deleting-packages.md)。

## <a name="usage"></a>用法

```cli
nuget delete <packageID> <packageVersion> [options]
```

where `<packageID>` 和`<packageVersion>`确定要删除或取消列出的确切包。 具体的行为取决于源。 例如, 对于本地文件夹, 将删除包;对于 nuget.org, 包未列出。

## <a name="options"></a>选项

| 选项 | 描述 |
| --- | --- |
| ApiKey | 目标存储库的 API 密钥。 如果不存在, 则使用配置文件中指定的一个。 |
| ConfigFile | 要应用的 NuGet 配置文件。 如果未指定, `%AppData%\NuGet\NuGet.Config`则使用 (Windows `~/.nuget/NuGet/NuGet.Config` ) 或 (Mac/Linux)。|
| ForceEnglishOutput | *(3.5 +)* 使用固定的、基于英语的区域性强制执行 nuget.exe。 |
| Help | 显示命令的帮助信息。 |
| NonInteractive | 取消显示提示用户输入或确认。 |
| Source | 指定服务器 URL。 Nuget.org 的 URL 是`https://api.nuget.org/v3/index.json`。 对于专用源, 请替换主机名, 例如, *% hostname%/api/v3*。 |
| Verbosity | 指定在输出中显示的详细信息量: "*正常*"、"*静默*"、"*详细*"。 |

另请参阅[环境变量](cli-ref-environment-variables.md)

## <a name="examples"></a>示例

```cli
nuget delete MyPackage 1.0

nuget delete MyPackage 1.0 -Source http://package.contoso.com/source -apikey A1B2C3
```
