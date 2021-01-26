---
title: NuGet CLI 源命令
description: nuget.exe 源命令的参考
author: JonDouglas
ms.author: jodou
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 0e9cbdd089c5c0f66d25e7588ece504feae63f2f
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/26/2021
ms.locfileid: "98780000"
---
# <a name="sources-command-nuget-cli"></a>源命令 (NuGet CLI) 

**适用于：** 包消耗，发布 &bullet; **支持的版本：** 全部

管理位于用户范围配置文件或指定配置文件中的源的列表。 用户范围配置文件位于 `%appdata%\NuGet\NuGet.Config` (Windows) 和 `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) 。

请注意，nuget.org 的源 URL 是 `https://api.nuget.org/v3/index.json`。

## <a name="usage"></a>使用情况

```cli
nuget sources <operation> -Name <name> -Source <source>
```

其中 `<operation>` 是 *List、Add、Remove、Enable、Disable* 或 *Update* 中的一个， `<name>` 是源的名称， `<source>` 是源的 URL。 一次只能在一个源上操作。

## <a name="options"></a>选项

- **`-ConfigFile`**

  要应用的 NuGet 配置文件。 如果未指定，则 `%AppData%\NuGet\NuGet.Config` 使用 (Windows) `~/.nuget/NuGet/NuGet.Config` 或 `~/.config/NuGet/NuGet.Config` (Mac/Linux) 。

- **`-ForceEnglishOutput`**

  *(3.5 +)* 使用固定的、基于英语的区域性强制运行 nuget.exe。

- **`-Format`**

  适用于 `list` 操作，可以 `Detailed` (默认) 或 `Short` 。

- **`-?|-help`**

  显示命令的帮助信息。

- **`-Name`**

  源的名称。

- **`-NonInteractive`**

  禁止提示用户输入或确认。

- **`-Password`**

  指定用于对源进行身份验证的密码。

- **`-src|-Source`**

   (s) 源的包的路径。

- **`-StorePasswordInClearText`**

  指示以未加密的文本而不是存储加密的窗体的默认行为来存储密码。

- **`-UserName`**

  指定用于对源进行身份验证的用户名。

- **`-ValidAuthenticationTypes`**

  此源的有效身份验证类型的逗号分隔列表。 默认情况下，所有身份验证类型都是有效的。 示例：`basic,negotiate`。

- **`-Verbosity [normal|quiet|detailed]`**

  指定在输出中显示的详细信息的数量： `normal` (默认) 、 `quiet` 或 `detailed` 。

> [!Note]
> 请确保在与 nuget.exe 稍后用于访问包源的用户上下文中添加源密码。 密码将以加密形式存储在配置文件中，并且只能在对其进行加密的用户上下文中解密。 例如，在使用生成服务器还原 NuGet 包时，必须使用运行生成服务器任务的相同 Windows 用户对密码进行加密。

另请参阅 [环境变量](cli-ref-environment-variables.md)

## <a name="examples"></a>示例

```cli
nuget sources Add -Name "MyServer" -Source \\myserver\packages

nuget sources Disable -Name "MyServer"

nuget sources Enable -Name "nuget.org"

nuget sources add -name foo.bar -source C:\NuGet\local -username foo -password bar -StorePasswordInClearText -configfile %AppData%\NuGet\my.config
```
