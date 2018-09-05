---
title: NuGet CLI 推送命令
description: Nuget.exe push 命令参考
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 125671ca3f695f82bd74f8097e590c3972003e22
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/04/2018
ms.locfileid: "43548338"
---
# <a name="push-command-nuget-cli"></a>push 命令 (NuGet CLI)

**适用于：** 包发布&bullet;**支持的版本：** 所有; 所需的 nuget.org 4.1.0 +

> [!Important]
> 若要将包推送到 nuget.org，必须使用 nuget.exe v4.1.0 +，该实现所需[NuGet 协议](../api/nuget-protocols.md)。

将包推送到包源并将其发布。

NuGet 的默认配置通过加载`%AppData%\NuGet\NuGet.Config`(Windows) 或`~/.nuget/NuGet/NuGet.Config`(Mac/Linux)，然后加载任何`Nuget.Config`或`.nuget\Nuget.Config`文件从驱动器的根目录开始和结束当前目录中 (请参阅[配置NuGet 行为](../consume-packages/configuring-nuget-behavior.md))

## <a name="usage"></a>用法

```cli
nuget push <packagePath> [options]
```

其中`<packagePath>`标识要推送到服务器的包。

## <a name="options"></a>选项

| 选项 | 描述 |
| --- | --- |
| ApiKey | 目标存储库 API 密钥。 如果不存在，则使用配置文件中指定的一个。 |
| ConfigFile | 要应用的 NuGet 配置文件。 如果未指定，否则`%AppData%\NuGet\NuGet.Config`(Windows) 或`~/.nuget/NuGet/NuGet.Config`(Mac/Linux) 使用。|
| DisableBuffering | 禁用缓冲时推送到 http （s） 服务器以减少内存使用情况。 注意： 使用此选项时，集成的 Windows 身份验证可能无法工作。 |
| ForceEnglishOutput | *（3.5 +)* 强制 nuget.exe 以运行使用固定的、 基于英语的区域性。 |
| 帮助 | 显示的帮助命令的信息。 |
| NonInteractive | 取消显示提示用户输入或确认。 |
| NoSymbols | *（3.5 +)* 如果符号包存在，它将不会推送到符号服务器。 |
| 源 | 指定服务器 URL。 NuGet 标识的 UNC 或本地文件夹源，并只需将复制的文件而非推送它使用 HTTP。  此外，从 NuGet 3.4.2 开始，这是一个必需参数除非`NuGet.Config`文件指定*DefaultPushSource*值 (请参阅[配置 NuGet 行为](../consume-packages/configuring-nuget-behavior.md))。 |
| SymbolSource | *（3.5 +)* Nuget.smbsrc.net 使用推送到 nuget.org 时; 指定符号服务器 URL |
| SymbolApiKey | *（3.5 +)* 为 URL 指定在指定的 API 密钥`-SymbolSource`。 |
| 超时 | 指定的超时，以秒为单位，以便将推送到服务器。 默认值为 300 秒 （5 分钟）。 |
| 详细级别 | 指定的输出中显示的详细信息：*正常*，*静默*，*详细*。 |

另请参阅[环境变量](cli-ref-environment-variables.md)

## <a name="examples"></a>示例

```cli
nuget push foo.nupkg

nuget push foo.symbols.nupkg

nuget push foo.nupkg -Timeout 360

nuget push *.nupkg

nuget.exe push -source \\mycompany\repo\ mypackage.1.0.0.nupkg

nuget push foo.nupkg 4003d786-cc37-4004-bfdf-c4f3e8ef9b3a -Source https://api.nuget.org/v3/index.json

nuget push foo.nupkg 4003d786-cc37-4004-bfdf-c4f3e8ef9b3a

nuget push foo.nupkg 4003d786-cc37-4004-bfdf-c4f3e8ef9b3a -s https://customsource/
```
