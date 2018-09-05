---
title: NuGet CLI 删除命令
description: Nuget.exe delete 命令参考
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 11eea6e806d7bfe364587db9c7ef8374da1819f9
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/04/2018
ms.locfileid: "43548505"
---
# <a name="delete-command-nuget-cli"></a>delete 命令 (NuGet CLI)

**适用于：** 包发布&bullet;**支持的版本：** 所有

删除或取消列出包从包源。 对于 nuget.org，删除命令[取消列出包](../policies/deleting-packages.md)。

## <a name="usage"></a>用法

```cli
nuget delete <packageID> <packageVersion> [options]
```

其中`<packageID>`和`<packageVersion>`标识要删除或取消列出的确切包。 确切行为取决于源。 对于本地文件夹，例如，删除的包;对于 nuget.org 包是未列出。

## <a name="options"></a>选项

| 选项 | 描述 |
| --- | --- |
| ApiKey | 目标存储库 API 密钥。 如果不存在，则使用配置文件中指定的一个。 |
| ConfigFile | 要应用的 NuGet 配置文件。 如果未指定，否则`%AppData%\NuGet\NuGet.Config`(Windows) 或`~/.nuget/NuGet/NuGet.Config`(Mac/Linux) 使用。|
| ForceEnglishOutput | *（3.5 +)* 强制 nuget.exe 以运行使用固定的、 基于英语的区域性。 |
| 帮助 | 显示的帮助命令的信息。 |
| NonInteractive | 取消显示提示用户输入或确认。 |
| 源 | 指定服务器 URL。 Nuget.org 的 URL 是`https://api.nuget.org/v3/index.json`。 对于专用源，例如，替换主机名 *%hostname%/api/v3*。 |
| 详细级别 | 指定的输出中显示的详细信息：*正常*，*静默*，*详细*。 |

另请参阅[环境变量](cli-ref-environment-variables.md)

## <a name="examples"></a>示例

```cli
nuget delete MyPackage 1.0

nuget delete MyPackage 1.0 -Source http://package.contoso.com/source -apikey A1B2C3
```
