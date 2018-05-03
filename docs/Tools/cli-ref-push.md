---
title: NuGet CLI 推送命令
description: Nuget.exe 推送命令参考
author: kraigb
ms.author: kraigb
manager: douge
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 959b539fc20bc47f38946cb660375a6652582a0d
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/26/2018
---
# <a name="push-command-nuget-cli"></a>推送命令 (NuGet CLI)

**适用于：**包发布&bullet;**受支持的版本：**所有; 4.1.0+ nuget.org 的必要条件

> [!Important]
> 若要将包推送到 nuget.org 必须使用 nuget.exe v4.1.0 +，并实现所需[NuGet 协议](../api/nuget-protocols.md)。

推送到包源的包，将其发布。

NuGet 的默认配置通过加载获取`%AppData%\NuGet\NuGet.Config`(Windows) 或`~/.nuget/NuGet/NuGet.Config`(Mac/Linux)，然后加载任何`Nuget.Config`或`.nuget\Nuget.Config`文件从驱动器的根目录开始和结束当前目录中 (请参阅[配置NuGet 行为](../consume-packages/configuring-nuget-behavior.md))

## <a name="usage"></a>用法

```cli
nuget push <packagePath> [options]
```

其中`<packagePath>`标识要将推送到服务器的包。

## <a name="options"></a>选项

| 选项 | 描述 |
| --- | --- |
| ApiKey | 目标存储库的 API 密钥。 如果不存在，则使用在配置文件中指定。 |
| ConfigFile | 要应用的 NuGet 配置文件。 如果未指定， `%AppData%\NuGet\NuGet.Config` (Windows) 或`~/.nuget/NuGet/NuGet.Config`使用 (Mac/Linux)。|
| DisableBuffering | 禁用时将推送到的 http （s） 服务器以减少内存使用情况进行缓冲。 注意： 当使用此选项时，集成的 Windows 身份验证可能无法工作。 |
| ForceEnglishOutput | *（3.5 +)* 强制 nuget.exe 运行使用固定的、 基于英语的区域性。 |
| 帮助 | 显示的帮助命令的信息。 |
| 非交互式 | 取消显示提示用户输入或确认。 |
| NoSymbols | *（3.5 +)* 如果符号包存在，它将不会推送到符号服务器。 |
| 源 | 指定服务器 URL。 NuGet 标识的 UNC 或本地文件夹源，并只需将复制文件而不是将它使用 HTTP 推送。  此外，从开始 NuGet 上面 3.4.2，这是强制参数除非`NuGet.Config`文件指定*DefaultPushSource*值 (请参阅[配置 NuGet 行为](../consume-packages/configuring-nuget-behavior.md))。 |
| SymbolSource | *（3.5 +)* 指定符号服务器 URL; 推送到 nuget.org 时使用 nuget.smbsrc.net |
| SymbolApiKey | *（3.5 +)* 中指定的 URL 指定的 API 密钥`-SymbolSource`。 |
| 超时 | 指定超时，以秒为单位，以便将推送到服务器。 默认值为 300 秒 （5 分钟）。 |
| 详细级别 | 指定的输出中显示的详细信息量：*正常*， *quiet*，*详细*。 |

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
