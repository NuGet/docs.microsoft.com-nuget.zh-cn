---
title: "NuGet CLI 将命令添加 |Microsoft 文档"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 10/24/2017
ms.topic: reference
ms.prod: nuget
ms.technology: 
ms.assetid: 4f68a016-ad4e-41fc-b869-88910fc5121e
description: "Nuget.exe 的引用添加命令"
keywords: "nuget 添加引用，添加包命令"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: bf9a6e51dfbf1716ba40273487b76ae04c18e948
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/14/2017
---
# <a name="add-command-nuget-cli"></a>添加命令 (NuGet CLI)

**适用于**： 包发布&bullet;**受支持的版本**: 3.3 +

将指定的包添加到其中的包 ID 和版本号创建文件夹层次结构布局中的非 HTTP 包源 （文件夹或 UNC 路径）。 例如: 

    \\myserver\packages
      └─<packageID>
        └─<version>
          ├─<packageID>.<version>.nupkg
          ├─<packageID>.<version>.nupkg.sha512
          └─<packageID>.nuspec

还原或更新时对包源，则层次结构布局提供显著提高性能。

若要对目标包源扩展包中的所有文件，使用`-Expand`切换。 这通常会出现在该目标，如其他子文件夹中`tools`和`lib`。

## <a name="usage"></a>用法

```
nuget add <packagePath> -Source <sourcePath> [options]
```

其中`<packagePath>`到包后，若要添加，路径名和`<sourcePath>`指定包将添加到基于文件夹的包源。 不支持 HTTP 源。

## <a name="options"></a>选项

| 选项 | 描述 |
| --- | --- |
| ConfigFile | 要应用的 NuGet 配置文件。 如果未指定， *%AppData%\NuGet\NuGet.Config*使用。| 
| Expand | 将包中的所有文件都添加到包源。 |
| ForceEnglishOutput | *（3.5 +)*强制 nuget.exe 运行使用固定的、 基于英语的区域性。 |
| 帮助 | 显示的帮助命令的信息。 |
| 非交互式 | 取消显示提示用户输入或确认。 |
| 详细级别 | 指定的输出中显示的详细信息量：*正常*， *quiet*，*详细*。 |

另请参阅[环境变量](cli-ref-environment-variables.md)

## <a name="examples"></a>示例

```
nuget add foo.nupkg -Source c:\bar\

nuget add foo.nupkg -Source \\bar\packages\
```
