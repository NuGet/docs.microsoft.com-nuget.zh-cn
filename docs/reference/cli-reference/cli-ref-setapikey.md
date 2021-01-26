---
title: NuGet CLI setapikey 命令
description: nuget.exe setapikey 命令的参考
author: JonDouglas
ms.author: jodou
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 3e0c2f84e336e0a642b1b5e815e74a1fb0878467
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/26/2021
ms.locfileid: "98780020"
---
# <a name="setapikey-command-nuget-cli"></a> (NuGet CLI) 的 setapikey 命令

**适用于：** 包消耗，发布 &bullet; **支持的版本：** 全部

将给定服务器 URL 的 API 密钥保存到 `NuGet.Config` ，以便不需要为后续命令输入该 URL。

## <a name="usage"></a>使用情况

```cli
nuget setapikey <key> -Source <url> [options]
```

其中 `<source>` 标识服务器， `<key>` 是要保存的密钥。 如果 `<source>` 省略，则假定为 nuget.org。 

> [!NOTE]
> API 密钥不用于向专用源进行身份验证。 请参考 [`nuget sources` 命令](../cli-reference/cli-ref-sources.md)来管理用于向源进行身份验证的凭据。
> API 密钥可以从单个 NuGet 服务器获取。 若要创建和管理 nuget.org 的 APIKeys，请参阅 [获取 api 密钥](../../nuget-org/scoped-api-keys.md#acquire-an-api-key)

## <a name="options"></a>选项

- **`-ConfigFile`**

  要应用的 NuGet 配置文件。 如果未指定，则 `%AppData%\NuGet\NuGet.Config` 使用 (Windows) `~/.nuget/NuGet/NuGet.Config` 或 `~/.config/NuGet/NuGet.Config` (Mac/Linux) 。

- **`-ForceEnglishOutput`**

  *(3.5 +)* 使用固定的、基于英语的区域性强制运行 nuget.exe。

- **`-?|-help`**

  显示命令的帮助信息。

- **`-NonInteractive`**

  禁止提示用户输入或确认。

- **`-src|-Source`**

  API 密钥有效的服务器 URL。

- **`-Verbosity [normal|quiet|detailed]`**

  指定在输出中显示的详细信息的数量： `normal` (默认) 、 `quiet` 或 `detailed` 。

另请参阅 [环境变量](cli-ref-environment-variables.md)

## <a name="examples"></a>示例

```cli
nuget setapikey 4003d786-cc37-4004-bfdf-c4f3e8ef9b3a

nuget setapikey 4003d786-cc37-4004-bfdf-c4f3e8ef9b3a -source https://example.com/nugetfeed
```
