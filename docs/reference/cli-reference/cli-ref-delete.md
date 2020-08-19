---
title: NuGet CLI delete 命令
description: nuget.exe delete 命令的参考
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: bec1a778d4986a4cb7ee87e1ef8a98550c96ed57
ms.sourcegitcommit: cbc87fe51330cdd3eacaad3e8656eb4258882fc7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/19/2020
ms.locfileid: "88622858"
---
# <a name="delete-command-nuget-cli"></a> (NuGet CLI) 删除命令

**适用于：** 包发布 &bullet; **支持的版本：** 全部

从包源中删除或取消列出包。 对于 nuget.org，delete 命令 [取消列出包](../../nuget-org/policies/deleting-packages.md)。

## <a name="usage"></a>使用情况

```cli
nuget delete <packageID> <packageVersion> [options]
```

where `<packageID>` 和 `<packageVersion>` 确定要删除或取消列出的确切包。 具体的行为取决于源。 例如，对于本地文件夹，将删除包;对于 nuget.org，包未列出。

## <a name="options"></a>选项

- **`-ApiKey`**

  目标存储库的 API 密钥。 如果不存在，则使用配置文件中指定的一个。

- **`-ConfigFile`**

  要应用的 NuGet 配置文件。 如果未指定，则 `%AppData%\NuGet\NuGet.Config` 使用 (Windows) `~/.nuget/NuGet/NuGet.Config` 或 `~/.config/NuGet/NuGet.Config` (Mac/Linux) 。

- **`-ForceEnglishOutput`**

  * (3.5 +) * 使用固定的、基于英语的区域性强制运行 nuget.exe。

- **`-?|-help`**

  显示命令的帮助信息。

- **`-NonInteractive`**

  禁止提示用户输入或确认。

 - **`-np|-NoPrompt`**

   删除时不提示。

 - **`-NoServiceEndpoint`** 不会将 "api/v2/包" 追加到源 URL。

- **`-src|-Source`**

  指定服务器 URL。 Nuget.org 的 URL 是 `https://api.nuget.org/v3/index.json` 。 对于专用源，请替换主机名，例如， *% hostname%/api/v3*。

- **`-Verbosity [normal|quiet|detailed]`**

  指定在输出中显示的详细信息的数量： `normal` (默认) 、 `quiet` 或 `detailed` 。

另请参阅 [环境变量](cli-ref-environment-variables.md)

## <a name="examples"></a>示例

```cli
nuget delete MyPackage 1.0

nuget delete MyPackage 1.0 -Source http://package.contoso.com/source -apikey A1B2C3
```
