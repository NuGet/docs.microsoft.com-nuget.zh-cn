---
title: "NuGet CLI 规范命令 |Microsoft 文档"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 10/24/2017
ms.topic: reference
ms.prod: nuget
ms.technology: 
ms.assetid: 85611449-87e6-489b-8c6c-fe1d7be76c13
description: "Nuget.exe spec 命令参考"
keywords: "nuget 规范引用、 spec 命令"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: c32b23e66c8eb4db1c8fa6dc615589219c00239f
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/14/2017
---
# <a name="spec-command-nuget-cli"></a>spec 命令 (NuGet CLI)

**适用于：** ，创建包&bullet;**受支持的版本：**所有

生成`.nuspec`新包的文件。 如果在项目文件所在的文件夹中运行 (`.csproj`， `.vbproj`， `.fsproj`)，`spec`创建标记`.nuspec`文件。 有关其他信息，请参阅[创建包](../create-packages/creating-a-package.md)。

## <a name="usage"></a>用法

```
nuget spec [<packageID>] [options]
```

其中`<packageID>`是一个可选软件包的标识符以保存`.nuspec`文件。

## <a name="options"></a>选项

| 选项 | 描述 |
| --- | --- |
| AssemblyPath | 指定要对元数据使用的程序集的路径。 |
| 强制 | 将覆盖任何现有`.nuspec`文件。 |
| ForceEnglishOutput | *（3.5 +)*强制 nuget.exe 运行使用固定的、 基于英语的区域性。 |
| 帮助 | 显示的帮助命令的信息。 |
| 非交互式 | 取消显示提示用户输入或确认。 |
| 详细级别 | 指定的输出中显示的详细信息量：*正常*， *quiet*，*详细 （2.5 +）*。 |

另请参阅[环境变量](cli-ref-environment-variables.md)

## <a name="examples"></a>示例

```
nuget spec

nuget spec MyPackage

nuget spec -a MyAssembly.dll
```
