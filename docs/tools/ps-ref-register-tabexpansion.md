---
title: NuGet 注册 TabExpansion PowerShell 参考
description: 在 Visual Studio 中的 NuGet 包管理器控制台中的注册 TabExpansion PowerShell 命令参考。
author: karann-msft
ms.author: karann
ms.date: 12/07/2017
ms.topic: reference
ms.openlocfilehash: 8adb80af85e2e32fa8c35e5272cf90ff0c0ddcbb
ms.sourcegitcommit: 0dea3b153ef823230a9d5f38351b7cef057cb299
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/12/2019
ms.locfileid: "67842485"
---
# <a name="register-tabexpansion-package-manager-console-in-visual-studio"></a>注册 TabExpansion （在 Visual Studio 中的包管理器控制台）

*仅在内可用[程序包管理器控制台](package-manager-console.md)在 Windows 上的 Visual Studio 中。*

注册指定的命令的参数的选项卡扩展，以便使用选项卡时输入命令时，扩展的值显示为相关参数的可用选项。 将覆盖任何以前的命令扩展。

## <a name="syntax"></a>语法

```ps
Register-TabExpansion [-Name] <String> [-Definition] <Object> [<CommonParameters>]
```

## <a name="parameters"></a>参数

| 参数 | 描述 |
| --- | --- |
| name | （必需）将注册扩展到命令。 -名称本身的开关是可选的。 |
| 定义 | （必需）描述在语法中的参数的对象`@{'<parameter>' = {'<value1>', '<value2>', ...}}`其中`<parameter>`是要修改的参数和每个名称`<value>`提供特定的扩展。 接受的单引号和双引号。 |

任何这些参数接受管道输入或通配符字符。

## <a name="common-parameters"></a>通用参数

`Register-TabExpansion` 支持以下[常见的 PowerShell 参数](http://go.microsoft.com/fwlink/?LinkID=113216):调试、 错误操作、 ErrorVariable、 OutBuffer、 OutVariable、 PipelineVariable，详细、 WarningAction 和 WarningVariable。

## <a name="examples"></a>示例

请考虑包含三个项目名称 EventManager、 实用工具和 SpecialParser 的解决方案。 开发人员经常使用`Update-Package`命令在与这些项目中的每个不同的时间。 她发现方便`Update-Package`命令提供的自动完成功能扩展`-ProjectName`参数，因此她不需要每次键入项目名称。 

以下命令，然后，将这些这三个项目名称注册为扩展`-ProjectName`参数：

```ps
Register-TabExpansion Update-Package @{'ProjectName' = {'EventManager', 'Utilities', 'SpecialParser'}}    
```

开发人员然后可以键入`Update-Package -ProjectName `、 按选项卡上，并请参阅作为自动完成选项提供的扩展：

![使用注册 TabExpansion 的示例](media/Register-TabExpansion-Example.png)
