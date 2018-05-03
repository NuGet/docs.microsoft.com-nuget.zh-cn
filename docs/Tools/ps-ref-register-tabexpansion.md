---
title: NuGet 注册 TabExpansion PowerShell 参考
description: Visual Studio 中的 NuGet 包管理器控制台中注册 TabExpansion PowerShell 命令参考。
author: kraigb
ms.author: kraigb
manager: douge
ms.date: 12/07/2017
ms.topic: reference
ms.openlocfilehash: 02f6d4ecd246b7ce5425cf56ade10789cf03113c
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/26/2018
---
# <a name="register-tabexpansion-package-manager-console-in-visual-studio"></a>注册 TabExpansion （Visual Studio 中的包管理器控制台）

*仅在内可用[NuGet 程序包管理器控制台](package-manager-console.md)Windows 上的 Visual Studio 中。*

注册指定的命令的参数选项卡扩展，以便使用时选项卡上，输入命令时，扩展的值显示为相关参数的可用选项。 将覆盖任何以前扩展命令。

## <a name="syntax"></a>语法

```ps
Register-TabExpansion [-Name] <String> [-Definition] <Object> [<CommonParameters>]
```

## <a name="parameters"></a>参数

| 参数 | 描述 |
| --- | --- |
| 名称 | （必需）要注册扩展到该命令。 -Name 是可选的交换机本身。 |
| 定义 | （必需）描述在语法中的自变量的对象`@{'<parameter>' = {'<value1>', '<value2>', ...}}`其中`<parameter>`是要修改的参数和每个名称`<value>`提供特定的扩展。 接受单引号和双引号。 |

任何这些参数接受管道输入或通配符字符。

## <a name="common-parameters"></a>通用参数

`Register-TabExpansion` 支持以下[常见的 PowerShell 参数](http://go.microsoft.com/fwlink/?LinkID=113216)： 调试、 错误操作、 ErrorVariable、 OutBuffer、 OutVariable、 PipelineVariable、 Verbose、 WarningAction 和 WarningVariable。

## <a name="examples"></a>示例

请考虑一个包含三个项目名称 EventManager、 实用程序和 SpecialParser 解决方案。 开发人员经常使用`Update-Package`命令在不同时间与每个这些项目。 她发现方便具有`Update-Package`命令提供的自动完成扩展`-ProjectName`自变量，因此她不需要键入项目名称出每个时间。 

以下命令，然后，将这些三个项目名称注册为扩展的`-ProjectName`参数：

```ps
Register-TabExpansion Update-Package @{'ProjectName' = {'EventManager', 'Utilities', 'SpecialParser'}}    
```

开发人员然后可以键入`Update-Package -ProjectName `、 按 tab 键，以及查看作为自动完成选项提供的扩展：

![使用注册 TabExpansion 的示例](media/Register-TabExpansion-Example.png)
