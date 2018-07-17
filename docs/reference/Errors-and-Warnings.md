---
title: NuGet 错误和警告参考
description: 警告和错误在各种 NuGet 操作期间从 NuGet 颁发的完整参考。
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 05/18/2018
ms.topic: reference
ms.reviewer: anangaur
ms.openlocfilehash: a787d036f7682b54adb30140152655fe165ee161
ms.sourcegitcommit: a76ecc58f41c2c5b3536ff4a3f3fcbdf5258177c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/17/2018
ms.locfileid: "39069656"
---
# <a name="errors-and-warnings"></a>错误和警告

在 NuGet 4.3.0 错误和警告本主题中所述进行编号，并提供详细的信息来帮助你解决所涉及的问题。

错误和警告在此处列出并仅提供[基于 PackageReference 的](../consume-packages/package-references-in-project-files.md)项目和 NuGet 4.3.0。 NuGet 还支持 MSBuild 属性禁止显示警告或将其提升至错误。 有关详细信息，请参阅[如何： 禁止显示编译器警告](/visualstudio/ide/how-to-suppress-compiler-warnings)Visual Studio 文档中。

**错误**

| Group | 错误号 |
| --- | --- |
| 无效输入的错误 | [NU1001](./errors-and-warnings/NU1001.md)， [NU1002](./errors-and-warnings/NU1002.md)， [NU1003](./errors-and-warnings/NU1003.md) |
| 缺少的包和项目错误 | [NU1100](./errors-and-warnings/NU1100.md)， [NU1101](./errors-and-warnings/NU1101.md)， [NU1102](./errors-and-warnings/NU1102.md)， [NU1103](./errors-and-warnings/NU1103.md)， [NU1104](./errors-and-warnings/NU1104.md)， [NU1105](./errors-and-warnings/NU1105.md)， [NU1106](./errors-and-warnings/NU1106.md)， [NU1107](./errors-and-warnings/NU1107.md)， [NU1108](./errors-and-warnings/NU1108.md) |
| 兼容性错误 | [NU1201](./errors-and-warnings/NU1201.md)， [NU1202](./errors-and-warnings/NU1202.md)， [NU1203](./errors-and-warnings/NU1203.md)， [NU1401](./errors-and-warnings/NU1401.md) |
| NuGet 的内部错误 | [NU1000](./errors-and-warnings/NU1000.md) |
| 已签名的包错误 （创建和验证） | [NU3000](./errors-and-warnings/NU3000.md)， [NU3001](./errors-and-warnings/NU3001.md)， [NU3004](./errors-and-warnings/NU3004.md)， [NU3008](./errors-and-warnings/NU3008.md) |

**警告**

| Group | 警告编号 |
| --- | --- |
| 无效输入的警告 | [NU1501](./errors-and-warnings/NU1501.md)， [NU1502](./errors-and-warnings/NU1502.md)， [NU1503](./errors-and-warnings/NU1503.md) |
| 意外的包版本警告 | [NU1601](./errors-and-warnings/NU1601.md)， [NU1602](./errors-and-warnings/NU1602.md)， [NU1603](./errors-and-warnings/NU1603.md)， [NU1604](./errors-and-warnings/NU1604.md)， [NU1605](./errors-and-warnings/NU1605.md)， [NU1606](./errors-and-warnings/NU1108.md)， [NU1607](./errors-and-warnings/NU1107.md) |
| 冲突解决程序冲突警告 | [NU1608](./errors-and-warnings/NU1608.md) |
| 包回退警告 | [NU1701](./errors-and-warnings/NU1701.md) |
| 源警告 | [NU1801](./errors-and-warnings/NU1801.md) |
| NuGet 内部警告 | [NU1500](./errors-and-warnings/NU1500.md) |
| 已签名的包警告 （创建和验证） | [NU3002](./errors-and-warnings/NU3002.md)， [NU3018](./errors-and-warnings/NU3018.md)， [NU3028](./errors-and-warnings/NU3028.md) |
