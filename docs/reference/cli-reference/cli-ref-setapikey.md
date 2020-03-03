---
title: NuGet CLI setapikey 命令
description: Nuget.exe setapikey 命令的参考
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: e06cfb5b355dfae8104090db7babdecdf9e9fec1
ms.sourcegitcommit: c81561e93a7be467c1983d639158d4e3dc25b93a
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/02/2020
ms.locfileid: "78231222"
---
# <a name="setapikey-command-nuget-cli"></a>setapikey 命令（NuGet CLI）

**适用于：** 包使用情况、发布 &bullet;**支持的版本：** 全部

将给定服务器 URL 的 API 密钥保存到 `NuGet.Config`，以便不需要为后续命令输入该 URL。

## <a name="usage"></a>使用情况

```cli
nuget setapikey <key> -Source <url> [options]
```

其中 `<source>` 标识服务器，`<key>` 是要保存的密钥。 如果省略 `<source>`，则采用 nuget.org。 

> [!NOTE]
> API 密钥不用于通过专用源进行身份验证。 请参阅[`nuget sources` 命令](../cli-reference/cli-ref-sources.md)，管理凭据以便通过源进行身份验证。
> 可以从单个 NuGet 服务器获取 API 密钥。 若要创建和管理 nuget.org 的 APIKeys，请参阅[发布 api 密钥](../../quickstart/includes/publish-api-key.md)

## <a name="options"></a>选项

| 选项 | 说明 |
| --- | --- |
| ConfigFile | 要应用的 NuGet 配置文件。 如果未指定，则使用 `%AppData%\NuGet\NuGet.Config` （Windows）或 `~/.nuget/NuGet/NuGet.Config` （Mac/Linux）。|
| ForceEnglishOutput | *（3.5 +）* 使用固定的、基于英语的区域性强制执行 nuget.exe。 |
| 帮助 | 显示命令的帮助信息。 |
| NonInteractive | 取消显示提示用户输入或确认。 |
| 详细程度 | 指定在输出中显示的详细信息量： "*正常*"、"*静默*"、"*详细*"。 |

另请参阅[环境变量](cli-ref-environment-variables.md)

## <a name="examples"></a>示例

```cli
nuget setapikey 4003d786-cc37-4004-bfdf-c4f3e8ef9b3a

nuget setapikey 4003d786-cc37-4004-bfdf-c4f3e8ef9b3a -source https://example.com/nugetfeed
```
