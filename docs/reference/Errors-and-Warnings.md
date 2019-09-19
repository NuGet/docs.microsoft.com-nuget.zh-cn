---
title: NuGet 错误和警告参考
description: 在各种 NuGet 操作过程中，完整引用 NuGet 发出的警告和错误。
author: karann-msft
ms.author: karann
ms.date: 05/18/2018
ms.topic: reference
ms.reviewer: anangaur
ms.openlocfilehash: 66bfe3cbc55f68947e85af5384c37092889c5169
ms.sourcegitcommit: 1eda83ab537c86cc27316e7bc67f95a358766e63
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/18/2019
ms.locfileid: "71094062"
---
# <a name="errors-and-warnings"></a>错误和警告

在 NuGet 4.3.0 + 中，错误和警告按照本主题中的说明进行编号，并提供详细信息来帮助解决所涉及的问题。

此处列出的错误和警告仅适用于[基于 PackageReference 的](../consume-packages/package-references-in-project-files.md)项目和 NuGet 4.3.0 +。 NuGet 还遵循 MSBuild 属性来禁止显示警告或将警告提升为错误。 有关更多信息，请参见[如何：在 Visual Studio](/visualstudio/ide/how-to-suppress-compiler-warnings)文档中取消显示编译器警告。

## <a name="errors"></a>错误

| Group | 错误号 |
| --- | --- |
| 输入错误无效 | [NU1001](./errors-and-warnings/NU1001.md)、 [NU1002](./errors-and-warnings/NU1002.md)、 [NU1003](./errors-and-warnings/NU1003.md) |
| 缺少包和项目错误 | [NU1100](./errors-and-warnings/NU1100.md)、 [NU1101](./errors-and-warnings/NU1101.md)、 [NU1102](./errors-and-warnings/NU1102.md)、 [NU1103](./errors-and-warnings/NU1103.md)、 [NU1104](./errors-and-warnings/NU1104.md)、 [NU1105](./errors-and-warnings/NU1105.md)、 [NU1106](./errors-and-warnings/NU1106.md)、 [NU1107](./errors-and-warnings/NU1107.md)、 [NU1108](./errors-and-warnings/NU1108.md) |
| 兼容性错误 | [NU1201](./errors-and-warnings/NU1201.md)、 [NU1202](./errors-and-warnings/NU1202.md)、 [NU1203](./errors-and-warnings/NU1203.md)、 [NU1401](./errors-and-warnings/NU1401.md) |
| NuGet 内部错误 | [NU1000](./errors-and-warnings/NU1000.md) |
| 签名包错误（创建和验证） | [NU3001](./errors-and-warnings/NU3001.md)、 [NU3004](./errors-and-warnings/NU3004.md)、 [NU3005](./errors-and-warnings/NU3005.md)、 [NU3008](./errors-and-warnings/NU3008.md)、 [NU3034](./errors-and-warnings/NU3034.md)|
| 包错误 | [NU5000](./errors-and-warnings/NU5000.md)、 [NU5001](./errors-and-warnings/NU5001.md)、 [NU5002](./errors-and-warnings/NU5002.md)、 [NU5003](./errors-and-warnings/NU5003.md)、 [NU5004](./errors-and-warnings/NU5004.md)、 [NU5005](./errors-and-warnings/NU5005.md)、 [NU5007](./errors-and-warnings/NU5007.md)、 [NU5008](./errors-and-warnings/NU5008.md)、 [NU5009](./errors-and-warnings/NU5009.md)、 [NU5010](./errors-and-warnings/NU5010.md)、 [NU5011](./errors-and-warnings/NU5011.md)、 [NU5012](./errors-and-warnings/NU5012.md)、 [NU5013](./errors-and-warnings/NU5013.md)、 [NU5014](./errors-and-warnings/NU5014.md)、 [NU5015](./errors-and-warnings/NU5015.md)、 [NU5016](./errors-and-warnings/NU5016.md)、 [NU5017](./errors-and-warnings/NU5017.md)、 [NU5018](./errors-and-warnings/NU5018.md)、 [NU5019](./errors-and-warnings/NU5019.md)、 [NU5020](./errors-and-warnings/NU5020.md)、 [NU5021](./errors-and-warnings/NU5021.md)、 [NU5022](./errors-and-warnings/NU5022.md)、 [NU5023](./errors-and-warnings/NU5023.md)、 [NU5024](./errors-and-warnings/NU5024.md)、 [NU5025](./errors-and-warnings/NU5025.md)、 [NU5026](./errors-and-warnings/NU5026.md)、[NU5027](./errors-and-warnings/NU5027.md)、 [NU5028](./errors-and-warnings/NU5028.md)、 [NU5029](./errors-and-warnings/NU5029.md)、 [NU5036](./errors-and-warnings/NU5036.md)
| 许可证特定的包错误 | [NU5030](./errors-and-warnings/NU5030.md)、 [NU5031](./errors-and-warnings/NU5031.md)、 [NU5032](./errors-and-warnings/NU5032.md)、 [NU5033](./errors-and-warnings/NU5033.md)、 [NU5034](./errors-and-warnings/NU5034.md)、 [NU5035](./errors-and-warnings/NU5035.md)

## <a name="warnings"></a>警告

| Group | 警告编号 |
| --- | --- |
| 输入警告无效 | [NU1501](./errors-and-warnings/NU1501.md)、 [NU1502](./errors-and-warnings/NU1502.md)、 [NU1503](./errors-and-warnings/NU1503.md) |
| 意外的包版本警告 | [NU1601](./errors-and-warnings/NU1601.md)、 [NU1602](./errors-and-warnings/NU1602.md)、 [NU1603](./errors-and-warnings/NU1603.md)、 [NU1604](./errors-and-warnings/NU1604.md)、 [NU1605](./errors-and-warnings/NU1605.md)、 [NU1606](./errors-and-warnings/NU1108.md)、 [NU1607](./errors-and-warnings/NU1107.md) |
| 冲突解决程序冲突警告 | [NU1608](./errors-and-warnings/NU1608.md) |
| 包回退警告 | [NU1701](./errors-and-warnings/NU1701.md) |
| 源警告 | [NU1801](./errors-and-warnings/NU1801.md) |
| NuGet 内部警告 | [NU1500](./errors-and-warnings/NU1500.md) |
| 签名包警告（创建和验证） | [NU3000](./errors-and-warnings/NU3000.md)、 [NU3002](./errors-and-warnings/NU3002.md)、 [NU3003](./errors-and-warnings/NU3003.md)、 [NU3006](./errors-and-warnings/NU3006.md)、 [NU3007](./errors-and-warnings/NU3007.md)、 [NU3009](./errors-and-warnings/NU3009.md)、 [NU3010](./errors-and-warnings/NU3010.md)、 [NU3011](./errors-and-warnings/NU3011.md)、 [NU3012](./errors-and-warnings/NU3012.md)、 [NU3013](./errors-and-warnings/NU3013.md)、 [NU3014](./errors-and-warnings/NU3014.md)、 [NU3015](./errors-and-warnings/NU3015.md)、 [NU3016](./errors-and-warnings/NU3016.md)、 [NU3017](./errors-and-warnings/NU3017.md)、 [NU3018](./errors-and-warnings/NU3018.md)、 [NU3019](./errors-and-warnings/NU3019.md)、 [NU3020](./errors-and-warnings/NU3020.md)、 [NU3021](./errors-and-warnings/NU3021.md)、 [NU3022](./errors-and-warnings/NU3022.md)、 [NU3023](./errors-and-warnings/NU3023.md)、 [NU3024](./errors-and-warnings/NU3024.md)、 [NU3025](./errors-and-warnings/NU3025.md)、 [NU3026](./errors-and-warnings/NU3026.md)、 [NU3027](./errors-and-warnings/NU3027.md)、 [NU3028](./errors-and-warnings/NU3028.md)、 [NU3029](./errors-and-warnings/NU3029.md)、[NU3030](./errors-and-warnings/NU3030.md)、 [NU3031](./errors-and-warnings/NU3031.md)、 [NU3032](./errors-and-warnings/NU3032.md)、 [NU3033](./errors-and-warnings/NU3033.md)、 [NU3035](./errors-and-warnings/NU3035.md)、 [NU3036](./errors-and-warnings/NU3036.md)、 [NU3037](./errors-and-warnings/NU3037.md)、 [NU3038](./errors-and-warnings/NU3038.md)、 [NU3040](./errors-and-warnings/NU3040.md) |
| 包警告 | [NU5100](./errors-and-warnings/NU5100.md)、 [NU5101](./errors-and-warnings/NU5101.md)、 [NU5102](./errors-and-warnings/NU5102.md)、 [NU5103](./errors-and-warnings/NU5103.md)、 [NU5104](./errors-and-warnings/NU5104.md)、 [NU5105](./errors-and-warnings/NU5105.md)、 [NU5106](./errors-and-warnings/NU5106.md)、 [NU5107](./errors-and-warnings/NU5107.md)、 [NU5108](./errors-and-warnings/NU5108.md)、 [NU5109](./errors-and-warnings/NU5109.md)、 [NU5110](./errors-and-warnings/NU5110.md)、 [NU5111](./errors-and-warnings/NU5111.md)、 [NU5112](./errors-and-warnings/NU5112.md)、 [NU5114](./errors-and-warnings/NU5114.md)、 [NU5115](./errors-and-warnings/NU5115.md)、 [NU5116](./errors-and-warnings/NU5116.md)、 [NU5117](./errors-and-warnings/NU5117.md)、 [NU5118](./errors-and-warnings/NU5118.md)、 [NU5119](./errors-and-warnings/NU5119.md)、 [NU5120](./errors-and-warnings/NU5120.md)、 [NU5121](./errors-and-warnings/NU5121.md)、 [NU5122](./errors-and-warnings/NU5122.md)、 [NU5123](./errors-and-warnings/NU5123.md)、 [NU5128](./errors-and-warnings/NU5128.md)、 [NU5500](./errors-and-warnings/NU5500.md)
| 许可证特定包警告 | [NU5124](./errors-and-warnings/NU5124.md)、 [NU5125](./errors-and-warnings/NU5125.md)
| 图标特定包警告 | [NU5046](./errors-and-warnings/NU5046.md)、 [NU5047](./errors-and-warnings/NU5047.md)、 [NU5048](./errors-and-warnings/NU5048.md)
