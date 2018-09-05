---
title: NuGet CLI 局部变量命令
description: Nuget.exe 局部变量命令参考
author: karann-msft
ms.author: karann
ms.date: 03/19/2018
ms.topic: reference
ms.openlocfilehash: ea216c4651ba9619bc3b6a7ab52546fd299b0bb6
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/04/2018
ms.locfileid: "43545023"
---
# <a name="locals-command-nuget-cli"></a>locals 命令 (NuGet CLI)

**适用于：** 打包消耗&bullet;**支持的版本：** 3.3 +

清除或列出本地 NuGet 资源，例如*http 缓存*，*全局包*文件夹和临时文件夹。 `locals`命令还可用于显示这些位置的列表。 有关详细信息，请参阅[管理全局包和缓存文件夹](../consume-packages/managing-the-global-packages-and-cache-folders.md)。

## <a name="usage"></a>用法

```cli
nuget locals <folder> [options]
```

其中`<folder>`是之一`all`， `http-cache`， `packages-cache` *（3.5 及更早版本）*， `global-packages`， `temp` *（3.4 +）*，和`plugins-cache` *（4.8 +）*。

## <a name="options"></a>选项

| 选项 | 描述 |
| --- | --- |
| 清除 | 清除指定的文件夹。 |
| ConfigFile | 要应用的 NuGet 配置文件。 如果未指定，否则`%AppData%\NuGet\NuGet.Config`(Windows) 或`~/.nuget/NuGet/NuGet.Config`(Mac/Linux) 使用。|
| ForceEnglishOutput | *（3.5 +)* 强制 nuget.exe 以运行使用固定的、 基于英语的区域性。 |
| 帮助 | 显示的帮助命令的信息。 |
| 列表 | 列出在指定的文件夹的位置或与一起使用时的所有文件夹的位置*所有*。 |
| NonInteractive | 取消显示提示用户输入或确认。 |
| 详细级别 | 指定的输出中显示的详细信息：*正常*，*静默*，*详细*。 |

另请参阅[环境变量](cli-ref-environment-variables.md)

## <a name="examples"></a>示例

```cli
nuget locals all -list
nuget locals http-cache -clear
```

有关其他示例，请参阅[管理全局包和缓存文件夹](../consume-packages/managing-the-global-packages-and-cache-folders.md)。
