---
title: NuGet CLI 规范命令
description: Nuget.exe spec 命令参考
author: kraigb
ms.author: kraigb
manager: douge
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 68d661030ce7bcff7d7a3a1c96c07e149ad4ffea
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/26/2018
---
# <a name="spec-command-nuget-cli"></a>spec 命令 (NuGet CLI)

**适用于：** ，创建包&bullet;**受支持的版本：**所有

生成`.nuspec`新包的文件。 如果在项目文件所在的文件夹中运行 (`.csproj`， `.vbproj`， `.fsproj`)，`spec`创建标记`.nuspec`文件。 有关其他信息，请参阅[创建包](../create-packages/creating-a-package.md)。

## <a name="usage"></a>用法

```cli
nuget spec [<packageID>] [options]
```

其中`<packageID>`是一个可选软件包的标识符以保存`.nuspec`文件。

## <a name="options"></a>选项

| 选项 | 描述 |
| --- | --- |
| AssemblyPath | 指定要对元数据使用的程序集的路径。 |
| 强制 | 将覆盖任何现有`.nuspec`文件。 |
| ForceEnglishOutput | *（3.5 +)* 强制 nuget.exe 运行使用固定的、 基于英语的区域性。 |
| 帮助 | 显示的帮助命令的信息。 |
| 非交互式 | 取消显示提示用户输入或确认。 |
| 详细级别 | 指定的输出中显示的详细信息量：*正常*， *quiet*，*详细*。 |

另请参阅[环境变量](cli-ref-environment-variables.md)

## <a name="examples"></a>示例

```cli
nuget spec

nuget spec MyPackage

nuget spec -a MyAssembly.dll
```
