---
title: NuGet CLI 删除命令 |Microsoft 文档
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 01/18/2018
ms.topic: reference
ms.prod: nuget
ms.technology: ''
description: Nuget.exe delete 命令的引用
keywords: nuget 删除引用，则删除包命令
ms.reviewer:
- karann-msft
- unniravindranathan
ms.workload:
- dotnet
- aspnet
ms.openlocfilehash: 9445042c46ef41721def1fbbb8dcebf4afc14d1b
ms.sourcegitcommit: beb229893559824e8abd6ab16707fd5fe1c6ac26
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/28/2018
---
# <a name="delete-command-nuget-cli"></a>删除命令 (NuGet CLI)

**适用于：**包发布&bullet;**受支持的版本：**所有

删除或 unlists 从包源的包。 有关 nuget.org，delete 命令[unlists 包](../policies/deleting-packages.md)。

## <a name="usage"></a>用法

```cli
nuget delete <packageID> <packageVersion> [options]
```

其中`<packageID>`和`<packageVersion>`标识要删除或不列出的确切包。 具体的行为取决于源。 对于本地文件夹，例如，则删除此包;未列出 nuget.org 包为。

## <a name="options"></a>选项

| 选项 | 描述 |
| --- | --- |
| ApiKey | 目标存储库的 API 密钥。 如果不存在，则使用在配置文件中指定。 |
| ConfigFile | 要应用的 NuGet 配置文件。 如果未指定， `%AppData%\NuGet\NuGet.Config` (Windows) 或`~/.nuget/NuGet/NuGet.Config`使用 (Mac/Linux)。|
| ForceEnglishOutput | *（3.5 +)*强制 nuget.exe 运行使用固定的、 基于英语的区域性。 |
| 帮助 | 显示的帮助命令的信息。 |
| NonInteractive | 取消显示提示用户输入或确认。 |
| 源 | 指定服务器 URL。 Nuget.org 的 URL 是`https://api.nuget.org/v3/index.json`。 对于专用源，用替换主机名，例如， *%hostname%/api/v3*。 |
| 详细级别 | 指定的输出中显示的详细信息量：*正常*， *quiet*，*详细*。 |

另请参阅[环境变量](cli-ref-environment-variables.md)

## <a name="examples"></a>示例

```cli
nuget delete MyPackage 1.0

nuget delete MyPackage 1.0 -Source http://package.contoso.com/source -apikey A1B2C3
```
