---
title: NuGet CLI push 命令
description: nuget.exe push 命令的参考
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: d53a2e7f41219e68e59b195d1d5a9d1f62ad7c63
ms.sourcegitcommit: cbc87fe51330cdd3eacaad3e8656eb4258882fc7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/19/2020
ms.locfileid: "88622840"
---
# <a name="push-command-nuget-cli"></a> (NuGet CLI 的推送命令) 

**适用于：** 包发布 &bullet; **支持的版本：** 全部; 4.1.0 + 必需的 nuget.org

> [!Important]
> 若要将包推送到 nuget.org，必须使用 nuget.exe v 4.1.0 + 来实现所需的 [nuget 协议](../../api/nuget-protocols.md)。

将包推送到包源并发布包。

通过加载 `%AppData%\NuGet\NuGet.Config` (Windows) 或 `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) ，然后加载 `Nuget.Config` `.nuget\Nuget.Config` 从驱动器的根目录开始并在当前目录中结束的任何或文件，将获取 NuGet 的默认配置 (参见 [常见 NuGet 配置](../../consume-packages/configuring-nuget-behavior.md)) 

## <a name="usage"></a>使用情况

```cli
nuget push <packagePath> [options]
```

其中 `<packagePath>` 标识要推送到服务器的包。

## <a name="options"></a>选项

- **`-ApiKey`**

  目标存储库的 API 密钥。 如果不存在，则使用配置文件中指定的一个。

- **`-ConfigFile`**

  要应用的 NuGet 配置文件。 如果未指定，则 `%AppData%\NuGet\NuGet.Config` 使用 (Windows) `~/.nuget/NuGet/NuGet.Config` 或 `~/.config/NuGet/NuGet.Config` (Mac/Linux) 。

- **`-DisableBuffering`**

  当推送到 HTTP (s) 服务器来减少内存使用情况时，将禁用缓冲。 注意：使用此选项时，集成的 Windows 身份验证可能不起作用。

- **`-ForceEnglishOutput`**

  * (3.5 +) * 使用固定的、基于英语的区域性强制运行 nuget.exe。

- **`-?|-help`**

  显示命令的帮助信息。

- **`-NonInteractive`**

  禁止提示用户输入或确认。

- **`-NoServiceEndpoint`**

  不追加 `api/v2/packages` 到源 URL。

- **`-NoSymbols`**

  * (3.5 +) * 如果符号包存在，则不会将其推送到符号服务器。

- **`-src|-Source`**

  指定服务器 URL。 NuGet 标识 UNC 或本地文件夹源，只是复制该文件，而不是使用 HTTP 推送它。  此外，从 NuGet 3.4.2 开始，这是必需的参数，除非该 `NuGet.Config` 文件指定了 *DefaultPushSource* 值 (请参阅 [配置 NuGet 行为](../../consume-packages/configuring-nuget-behavior.md)) 。

- **`-SkipDuplicate`**

  * (5.1 +) * 如果包和版本已存在，则跳过它，并继续执行推送中的下一个包（如果有）。

- **`-SymbolSource`**

  * (3.5 +) * 指定符号服务器 URL;推送到 nuget.org 时使用 nuget.smbsrc.net

- **`-SymbolApiKey`**

  * (3.5 +) * 为中指定的 URL 指定 API 密钥 `-SymbolSource` 。

- **`-Timeout`**

  指定推送到服务器的超时值（以秒为单位）。 默认值为 300 秒（5 分钟）。

- **`-Verbosity [normal|quiet|detailed]`**

  指定在输出中显示的详细信息的数量： `normal` (默认) 、 `quiet` 或 `detailed` 。


另请参阅 [环境变量](cli-ref-environment-variables.md)

## <a name="examples"></a>示例

```cli
nuget push foo.nupkg

nuget push foo.symbols.nupkg

nuget push foo.nupkg -Timeout 360

nuget push *.nupkg

nuget.exe push -source \\mycompany\repo\ mypackage.1.0.0.nupkg

nuget push foo.nupkg 4003d786-cc37-4004-bfdf-c4f3e8ef9b3a -Source https://api.nuget.org/v3/index.json

nuget push foo.nupkg 4003d786-cc37-4004-bfdf-c4f3e8ef9b3a

nuget push foo.nupkg 4003d786-cc37-4004-bfdf-c4f3e8ef9b3a -src https://customsource/

:: In the example below -SkipDuplicate will skip pushing the package if package "Foo" version "5.0.2" already exists on NuGet.org
nuget push Foo.5.0.2.nupkg 4003d786-cc37-4004-bfdf-c4f3e8ef9b3a -src https://api.nuget.org/v3/index.json -SkipDuplicate
```
