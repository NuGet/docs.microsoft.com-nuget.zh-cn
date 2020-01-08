---
title: NuGet CLI setapikey 命令
description: Nuget.exe setapikey 命令的参考
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 0e2119953e6d07cd3571f156fa0b2665de49f963
ms.sourcegitcommit: 26a8eae00af2d4be581171e7a73009f94534c336
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/25/2019
ms.locfileid: "75383964"
---
# <a name="setapikey-command-nuget-cli"></a>setapikey 命令（NuGet CLI）

**适用于：** 包使用情况、发布 &bullet;**支持的版本：** 全部

将给定服务器 URL 的 API 密钥保存到 `NuGet.Config`，以便不需要为后续命令输入该 URL。

## <a name="usage"></a>用量

```cli
nuget setapikey <key> -Source <url> [options]
```

其中 `<source>` 标识服务器，`<key>` 是要保存的密钥或密码。 如果省略 `<source>`，则采用 nuget.org。

> [!NOTE]
> API 密钥不用于通过专用源进行身份验证。 请参阅[`nuget sources` 命令](../cli-reference/cli-ref-sources.md)，管理凭据以便通过源进行身份验证。

## <a name="options"></a>选项

| 选项 | 描述 |
| --- | --- |
| ConfigFile | 要应用的 NuGet 配置文件。 如果未指定，则使用 `%AppData%\NuGet\NuGet.Config` （Windows）或 `~/.nuget/NuGet/NuGet.Config` （Mac/Linux）。|
| ForceEnglishOutput | *（3.5 +）* 使用固定的、基于英语的区域性强制执行 nuget.exe。 |
| 帮助 | 显示命令的帮助信息。 |
| NonInteractive | 取消显示提示用户输入或确认。 |
| 详细级别 | 指定在输出中显示的详细信息量： "*正常*"、"*静默*"、"*详细*"。 |

另请参阅[环境变量](cli-ref-environment-variables.md)

## <a name="examples"></a>示例

```cli
nuget setapikey 4003d786-cc37-4004-bfdf-c4f3e8ef9b3a

nuget setapikey 4003d786-cc37-4004-bfdf-c4f3e8ef9b3a -source https://example.com/nugetfeed
```
