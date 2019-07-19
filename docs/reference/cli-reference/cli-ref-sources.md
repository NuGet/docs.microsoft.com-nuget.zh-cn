---
title: NuGet CLI 源命令
description: 针对 nuget.exe 源命令的参考
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 94134b87f83e057d5d11a2722d9067fb76cc8e21
ms.sourcegitcommit: efc18d484fdf0c7a8979b564dcb191c030601bb4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/18/2019
ms.locfileid: "68327594"
---
# <a name="sources-command-nuget-cli"></a>sources 命令 (NuGet CLI)

**适用于:** 包消耗, 发布&bullet; **支持的版本:** 全部

管理位于用户范围配置文件或指定配置文件中的源的列表。 用户范围配置文件位于`%appdata%\NuGet\NuGet.Config` (Windows) 和`~/.nuget/NuGet/NuGet.Config` (Mac/Linux)。

请注意，nuget.org 的源 URL 是 `https://api.nuget.org/v3/index.json`。

## <a name="usage"></a>用法

```cli
nuget sources <operation> -Name <name> -Source <source>
```

其中`<operation>`是*List、Add、Remove、Enable、Disable*或*Update* `<name>`中的一个, 是源的名称, `<source>`是源的 URL。 一次只能在一个源上操作。

## <a name="options"></a>选项

| 选项 | 描述 |
| --- | --- |
| ConfigFile | 要应用的 NuGet 配置文件。 如果未指定, `%AppData%\NuGet\NuGet.Config`则使用 (Windows `~/.nuget/NuGet/NuGet.Config` ) 或 (Mac/Linux)。|
| ForceEnglishOutput | *(3.5 +)* 使用固定的、基于英语的区域性强制执行 nuget.exe。 |
| 格式 | 适用于`Detailed` `Short`操作, 可以为 (默认值) 或。 `list` |
| Help | 显示命令的帮助信息。 |
| NonInteractive | 取消显示提示用户输入或确认。 |
| Password | 指定用于对源进行身份验证的密码。 |
| StorePasswordInClearText | 指示以未加密的文本而不是存储加密的窗体的默认行为来存储密码。 |
| UserName | 指定用于对源进行身份验证的用户名。 |
| Verbosity | 指定在输出中显示的详细信息量: "*正常*"、"*静默*"、"*详细*"。 |

> [!Note]
> 请确保在与 nuget.exe 一起用于访问包源的用户上下文中添加源密码。 密码将以加密形式存储在配置文件中, 并且只能在对其进行加密的用户上下文中解密。 例如, 在使用生成服务器还原 NuGet 包时, 必须使用运行生成服务器任务的相同 Windows 用户对密码进行加密。

另请参阅[环境变量](cli-ref-environment-variables.md)

## <a name="examples"></a>示例

```cli
nuget sources Add -Name "MyServer" -Source \\myserver\packages

nuget sources Disable -Name "MyServer"

nuget sources Enable -Name "nuget.org"

nuget sources add -name foo.bar -source C:\NuGet\local -username foo -password bar -StorePasswordInClearText -configfile %AppData%\NuGet\my.config
```
