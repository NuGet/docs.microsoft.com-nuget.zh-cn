---
title: NuGet CLI 局部变量命令 |Microsoft 文档
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 03/19/2018
ms.topic: reference
ms.prod: nuget
ms.technology: ''
description: Nuget.exe 局部变量命令参考
keywords: nuget 局部变量引用，局部变量命令
ms.reviewer:
- karann-msft
- unniravindranathan
ms.workload:
- dotnet
- aspnet
ms.openlocfilehash: 0122c79e55b12838bd123cf91bfcbc5dbbd2a65c
ms.sourcegitcommit: beb229893559824e8abd6ab16707fd5fe1c6ac26
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/28/2018
---
# <a name="locals-command-nuget-cli"></a>局部变量命令 (NuGet CLI)

**适用于：**打包消耗&bullet;**受支持的版本：** 3.3 +

清除或列出本地 NuGet 资源例如*http 缓存*，*全局包*文件夹和临时文件夹。 `locals`命令还可以用于显示这些位置的列表。 有关详细信息，请参阅[管理全局包和缓存文件夹](../consume-packages/managing-the-global-packages-and-cache-folders.md)。

## <a name="usage"></a>用法

```cli
nuget locals <folder> [options]
```

其中`<folder>`是之一`all`， `http-cache`， `packages-cache` *（3.5 及更早版本）*， `global-packages`，和`temp` *（3.4 +）*。

## <a name="options"></a>选项

| 选项 | 描述 |
| --- | --- |
| 清除 | 清除指定的文件夹。 |
| ConfigFile | 要应用的 NuGet 配置文件。 如果未指定， `%AppData%\NuGet\NuGet.Config` (Windows) 或`~/.nuget/NuGet/NuGet.Config`使用 (Mac/Linux)。|
| ForceEnglishOutput | *（3.5 +)*强制 nuget.exe 运行使用固定的、 基于英语的区域性。 |
| 帮助 | 显示的帮助命令的信息。 |
| 列表 | 列出指定的文件夹的位置或一起使用时的所有文件夹的位置*所有*。 |
| NonInteractive | 取消显示提示用户输入或确认。 |
| 详细级别 | 指定的输出中显示的详细信息量：*正常*， *quiet*，*详细*。 |

另请参阅[环境变量](cli-ref-environment-variables.md)

## <a name="examples"></a>示例

```cli
nuget locals all -list
nuget locals http-cache -clear
```

有关其他示例，请参阅[管理全局包和缓存文件夹](../consume-packages/managing-the-global-packages-and-cache-folders.md)。
