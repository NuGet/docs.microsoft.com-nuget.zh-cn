---
title: NuGet CLI 搜索命令
description: nuget.exe 搜索命令的参考
author: JonDouglas
ms.author: jodou
ms.date: 08/17/2020
ms.topic: reference
ms.openlocfilehash: 6f4adcdf3981e5ec0e5e88337a8c3bcdd9158ca3
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/26/2021
ms.locfileid: "98779159"
---
# <a name="search-command-nuget-cli"></a> (NuGet CLI) 搜索命令

**适用于：** 包使用 &bullet; **受支持的版本：** 5.8 +

使用提供的查询字符串搜索给定的源。 如果未指定任何源，将使用% AppData% \NuGet\NuGet.config 中定义的所有源。

## <a name="usage"></a>使用情况

```cli
nuget search [search terms] [options]
```

其中，搜索词应用于包、标记和包说明的名称，就像在 nuget.org 上使用时一样。

## <a name="options"></a>选项

| 名称 | 说明 | 使用情况 |
| ---  |     ---     |  :-:  |
| 早期 | 默认情况下不包括预发行包，但可以通过使用此参数包含这些包 | -预发行版 |
| Source | 要搜索的特定包源 () ，而不是查询中的默认源 __nuget.config__ | -源 `<Source URL>`|
| Take | 要返回的结果数。 默认值为 20。 | -Take `<positive integer>` |
| 详细程度 | 要在输出中显示的详细信息的级别。 默认值为 " _正常_"。  (参见下面的注释)   | -详细级别 `<quiet|normal|detailed>` |
| 帮助 | 显示命令的帮助信息 | -Help |

另请参阅 [环境变量](cli-ref-environment-variables.md)

> [!NOTE] 
> 详细级别：
> * _quiet_ -程序包 ID，版本
> * _标准_ 包 ID、版本、下载、说明预览
> * _详细_ -包 ID、版本、下载、完整说明、其他信息，如查询 URL

## <a name="examples"></a>示例

从默认源搜索与 *日志记录* 相关的包：
```
nuget search logging
```
搜索与 *日志记录* 相关的包，详细详细说明：
```
nuget search logging -Verbosity detailed
```
搜索与 *日志记录* 相关的包，只显示前5个结果：
```
nuget search logging -Take 5
```
从指定的源/源搜索与 *JSON* 相关的包，包括预发布版本：
```
nuget search JSON -PreRelease -Source "https://api.nuget.org/v3/index.json"
```
从多个源/源搜索 *JSON* 相关的包：
```
nuget search JSON -Source "https://api.nuget.org/v3/index.json" -Source "https://other-feed-url-goes-here"
```
