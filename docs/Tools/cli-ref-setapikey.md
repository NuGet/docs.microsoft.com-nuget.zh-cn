---
title: "NuGet CLI setapikey 命令 |Microsoft 文档"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 10/24/2017
ms.topic: reference
ms.prod: nuget
ms.technology: 
ms.assetid: a64c0462-973d-4100-ba3f-8902a2b127f7
description: "Nuget.exe setapikey 命令参考"
keywords: "nuget setapikey 引用，setapikey 命令"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: a07c35b8bdd57157391e391e04a90204342b1d5c
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/14/2017
---
## <a name="setapikey-command-nuget-cli"></a>setapikey 命令 (NuGet CLI)

**适用于：**包消耗、 发布&bullet;**受支持的版本：**所有

将 API 密钥保存到给定的服务器 url `NuGet.Config` ，以便它不需要的后续命令输入。

## <a name="usage"></a>用法

```
nuget setapikey <key> -Source <url> [options]
```

其中`<source>`标识的服务器和`<key>`是密钥或密码才能保存。 如果`<source>`是省略，则假定 nuget.org。

## <a name="options"></a>选项

| 选项 | 描述 |
| --- | --- |
| ConfigFile | *（2.5 +)* NuGet 要修改的配置文件。 如果未指定， *%AppData%\NuGet\NuGet.Config*使用。 |
| ForceEnglishOutput | *（3.5 +)*强制 nuget.exe 运行使用固定的、 基于英语的区域性。 |
| 帮助 | 显示的帮助命令的信息。 |
| 非交互式 | 取消显示提示用户输入或确认。 |
| 详细级别 | 指定的输出中显示的详细信息量：*正常*， *quiet*，*详细 （2.5 +）*。 |

另请参阅[环境变量](cli-ref-environment-variables.md)

## <a name="examples"></a>示例

```
nuget setapikey 4003d786-cc37-4004-bfdf-c4f3e8ef9b3a

nuget setapikey 4003d786-cc37-4004-bfdf-c4f3e8ef9b3a -source https://example.com/nugetfeed
```
