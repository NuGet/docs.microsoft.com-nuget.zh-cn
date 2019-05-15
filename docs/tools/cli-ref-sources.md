---
title: NuGet CLI 源命令
description: Nuget.exe 的参考源命令
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 94134b87f83e057d5d11a2722d9067fb76cc8e21
ms.sourcegitcommit: 4ea46498aee386b4f592b5ebba4af7f9092ac607
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/14/2019
ms.locfileid: "65610618"
---
# <a name="sources-command-nuget-cli"></a>sources 命令 (NuGet CLI)

**适用于：** 包使用、 发布&bullet;**支持的版本：** 所有

管理用户作用域配置文件或指定的配置文件中的源的列表。 用户作用域配置文件位于`%appdata%\NuGet\NuGet.Config`(Windows) 和`~/.nuget/NuGet/NuGet.Config`(Mac/Linux)。

请注意，nuget.org 的源 URL 是 `https://api.nuget.org/v3/index.json`。

## <a name="usage"></a>用法

```cli
nuget sources <operation> -Name <name> -Source <source>
```

其中`<operation>`是之一*列表中，添加、 删除、 启用、 禁用*或*更新*，`<name>`是源的名称和`<source>`是源的 URL。 您可以一次操作上只有一个源。

## <a name="options"></a>选项

| 选项 | 描述 |
| --- | --- |
| ConfigFile | 要应用的 NuGet 配置文件。 如果未指定，否则`%AppData%\NuGet\NuGet.Config`(Windows) 或`~/.nuget/NuGet/NuGet.Config`(Mac/Linux) 使用。|
| ForceEnglishOutput | *（3.5 +)* 强制 nuget.exe 以运行使用固定的、 基于英语的区域性。 |
| 格式 | 适用于`list`操作可以是`Detailed`（默认值） 或`Short`。 |
| Help | 显示的帮助命令的信息。 |
| NonInteractive | 取消显示提示用户输入或确认。 |
| Password | 指定与源进行身份验证的密码。 |
| StorePasswordInClearText | 指示要将密码存储在未加密的文本，而不是存储以加密的形式的默认行为。 |
| UserName | 指定与源进行身份验证的用户名。 |
| Verbosity | 指定的输出中显示的详细信息：*正常*，*静默*，*详细*。 |

> [!Note]
> 请务必添加相同的用户上下文的源的密码，如 nuget.exe 更高版本用于访问包源。 密码将以加密形式存储在配置文件中，因为它已加密仅可以在相同的用户上下文解密。 因此，例如当您使用的生成服务器具有相同的 Windows 用户，其下运行生成服务器任务会还原 NuGet 包必须加密密码。

另请参阅[环境变量](cli-ref-environment-variables.md)

## <a name="examples"></a>示例

```cli
nuget sources Add -Name "MyServer" -Source \\myserver\packages

nuget sources Disable -Name "MyServer"

nuget sources Enable -Name "nuget.org"

nuget sources add -name foo.bar -source C:\NuGet\local -username foo -password bar -StorePasswordInClearText -configfile %AppData%\NuGet\my.config
```
