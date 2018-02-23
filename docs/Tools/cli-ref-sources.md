---
title: "NuGet CLI 源命令 |Microsoft 文档"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 01/18/2018
ms.topic: reference
ms.prod: nuget
ms.technology: 
description: "参考 nuget.exe 源命令"
keywords: "nuget 源引用，源命令"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 1e8204f5e1bf712f65d8efb14ca2a4bd802e3f90
ms.sourcegitcommit: 7969f6cd94eccfee5b62031bb404422139ccc383
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/20/2018
---
# <a name="sources-command-nuget-cli"></a>源命令 (NuGet CLI)

**适用于：**包消耗、 发布&bullet;**受支持的版本：**所有

管理位于用户作用域配置文件或指定的配置文件的源的列表。 用户作用域配置文件位于`%APPDATA%\NuGet\NuGet.Config`在 Windows 和`~/.nuget/NuGet.Config`Mac/Linux 中。


请注意，nuget.org 的源 URL 是 `https://api.nuget.org/v3/index.json`。

## <a name="usage"></a>用法

```cli
nuget sources <operation> -Name <name> -Source <source>
```

其中`<operation>`是之一*列表、 添加、 删除、 启用、 禁用*或*更新*，`<name>`是源，名称和`<source>`是源的 URL。

## <a name="options"></a>选项

| 选项 | 描述 |
| --- | --- |
| ConfigFile | 要应用的 NuGet 配置文件。 如果未指定， *%AppData%\NuGet\NuGet.Config*使用。 |
| ForceEnglishOutput | *（3.5 +)*强制 nuget.exe 运行使用固定的、 基于英语的区域性。 |
| 格式 | 适用于`list`操作并可以是`Detailed`（默认值） 或`Short`。 |
| 帮助 | 显示的帮助命令的信息。 |
| NonInteractive | 取消显示提示用户输入或确认。 |
| Password | 指定与源进行身份验证的密码。 |
| StorePasswordInClearText | 指示要将密码存储在未加密的文本，而不是存储以加密的形式的默认行为。 |
| UserName | 指定与源进行身份验证的用户名。 |
| 详细级别 | 指定的输出中显示的详细信息量：*正常*， *quiet*，*详细*。 |

> [!Note]
> 请确保添加在相同的用户上下文的源的密码，如 nuget.exe 更高版本用于访问包源。 密码将以加密形式存储在配置文件中，因为它已加密仅可以在相同的用户上下文中解密。 因此，例如当你使用的生成服务器具有相同的生成服务器任务将在其下运行的 Windows 用户还原 NuGet 程序包必须加密密码。

另请参阅[环境变量](cli-ref-environment-variables.md)

## <a name="examples"></a>示例

```cli
nuget sources Add -Name "MyServer" -Source \\myserver\packages

nuget sources Disable -Name "MyServer"

nuget source Enable -Source "nuget.org"

nuget sources add -name foo.bar -source C:\NuGet\local -username foo -password bar -StorePasswordInClearText -configfile %AppData%\NuGet\my.config
```
