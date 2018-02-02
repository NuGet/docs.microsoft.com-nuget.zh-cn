---
title: "NuGet CLI 局部变量命令 |Microsoft 文档"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 01/18/2018
ms.topic: reference
ms.prod: nuget
ms.technology: 
description: "Nuget.exe 局部变量命令参考"
keywords: "nuget 局部变量引用，局部变量命令"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: b2f62a9ab5699bfb486eee146ab7046f5240aa50
ms.sourcegitcommit: 262d026beeffd4f3b6fc47d780a2f701451663a8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/25/2018
---
# <a name="locals-command-nuget-cli"></a>局部变量命令 (NuGet CLI)

**适用于：**打包消耗&bullet;**受支持的版本：** 3.3 +

清除或列出本地 NuGet 资源，如 http 请求缓存、 包缓存和计算机范围全局包文件夹。 `locals`命令还可以用于显示这些位置的列表。 有关详细信息，请参阅[管理 NuGet 缓存](../consume-packages/managing-the-nuget-cache.md)。

## <a name="usage"></a>用法

```cli
nuget locals <cache> [options]
```

其中`<cache>`是之一`all`， `http-cache`， `packages-cache`， `global-packages`，和`temp` *（3.4 +）*。

## <a name="options"></a>选项

| 选项 | 描述 |
| --- | --- |
| 清除 | 清除指定的缓存。 |
| ConfigFile | 要应用的 NuGet 配置文件。 如果未指定， *%AppData%\NuGet\NuGet.Config*使用。 |
| ForceEnglishOutput | *（3.5 +)*强制 nuget.exe 运行使用固定的、 基于英语的区域性。 |
| 帮助 | 显示的帮助命令的信息。 |
| 列表 | 列出指定的缓存的位置或一起使用时的所有缓存的位置*所有*。 |
| NonInteractive | 取消显示提示用户输入或确认。 |
| 详细级别 | 指定的输出中显示的详细信息量：*正常*， *quiet*，*详细*。 |

另请参阅[环境变量](cli-ref-environment-variables.md)

## <a name="examples"></a>示例

```cli
nuget locals all -list
nuget locals http-cache -clear
```
