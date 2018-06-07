---
title: NuGet CLI setapikey 命令
description: Nuget.exe setapikey 命令参考
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 66fc62074b4e7c39ff2ed6b515eee9f821530536
ms.sourcegitcommit: 2a6d200012cdb4cbf5ab1264f12fecf9ae12d769
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/06/2018
ms.locfileid: "34817679"
---
# <a name="setapikey-command-nuget-cli"></a>setapikey 命令 (NuGet CLI)

**适用于：** 包消耗、 发布&bullet;**受支持的版本：** 所有

将 API 密钥保存到给定的服务器 url `NuGet.Config` ，以便它不需要的后续命令输入。

## <a name="usage"></a>用法

```cli
nuget setapikey <key> -Source <url> [options]
```

其中`<source>`标识的服务器和`<key>`是密钥或密码才能保存。 如果`<source>`是省略，则假定 nuget.org。

## <a name="options"></a>选项

| 选项 | 描述 |
| --- | --- |
| ConfigFile | 要应用的 NuGet 配置文件。 如果未指定， `%AppData%\NuGet\NuGet.Config` (Windows) 或`~/.nuget/NuGet/NuGet.Config`使用 (Mac/Linux)。|
| ForceEnglishOutput | *（3.5 +)* 强制 nuget.exe 运行使用固定的、 基于英语的区域性。 |
| 帮助 | 显示的帮助命令的信息。 |
| NonInteractive | 取消显示提示用户输入或确认。 |
| 详细级别 | 指定的输出中显示的详细信息量：*正常*， *quiet*，*详细*。 |

另请参阅[环境变量](cli-ref-environment-variables.md)

## <a name="examples"></a>示例

```cli
nuget setapikey 4003d786-cc37-4004-bfdf-c4f3e8ef9b3a

nuget setapikey 4003d786-cc37-4004-bfdf-c4f3e8ef9b3a -source https://example.com/nugetfeed
```
