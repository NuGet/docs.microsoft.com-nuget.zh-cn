---
title: NuGet 5.4 发行说明
description: NuGet 5.4 的发行说明，包括新功能、bug 修复和 Dcr。
author: karann-msft
ms.author: karann
ms.date: 09/06/2019
ms.topic: conceptual
ms.openlocfilehash: c7fb9c1e587b6603abe63581c662571abfd4506b
ms.sourcegitcommit: 26a8eae00af2d4be581171e7a73009f94534c336
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/25/2019
ms.locfileid: "75384106"
---
# <a name="nuget-54-release-notes"></a>NuGet 5.4 发行说明

NuGet 分发车辆：

| NuGet 版本 | 适用于 Visual Studio 版本| 适用于 .NET SDK|
|:---|:---|:---|
| [**5.4.0**](https://nuget.org/downloads) | [Visual Studio 2019 版本16。4](https://visualstudio.microsoft.com/downloads/) | [3.1.100](https://dotnet.microsoft.com/download/dotnet-core/3.1)<sup>1</sup> |

<sup>1</sup>随 Visual Studio 2019 with .NET Core 工作负载一起安装

## <a name="summary-whats-new-in-54"></a>摘要：5.4 中的新增功能

* 更快的解决方案加载时间-在第一个解决方案加载过程中，运行 NuGet 代码的开销已通过部分 ngen 降低，以减少 JIT 成本[#6007](https://github.com/NuGet/Home/issues/6007)

* 新建帮助程序函数-给定包 id 和版本的列表，获取可能的顶级包。 - [#8316](https://github.com/NuGet/Home/issues/8316)

* 新[`nuget/setup-nuget`](https://github.com/marketplace/actions/setup-nuget-exe-for-use-with-actions)操作，用于在[GitHub 操作](https://github.com/features/actions)上安装和配置 nuget.exe。 - [#8818](https://github.com/NuGet/Home/issues/8818)

### <a name="issues-fixed-in-this-release"></a>此版本中已修复的问题

**Bug**

* 插件： linux/Mac 上的日志记录时间准确性已关闭- [#8747](https://github.com/NuGet/Home/issues/8747)

* 释放插件有时会引发并使整个操作失败。 - [#8732](https://github.com/NuGet/Home/issues/8732)

* 停止在 PMUI 中的允许和阻止版本列表中显示版本重复项- [#8679](https://github.com/NuGet/Home/issues/8679)

* 锁定文件未正确生成-框架排序不应影响 restore with lockedmode- [#8645](https://github.com/NuGet/Home/issues/8645)

* <RuntimeIdentifiers> SDK 3.0.100 中设置的项目的 LockFile 验证失败- [#8639](https://github.com/NuGet/Home/issues/8639)

* 签名验证现在会正确拒绝带有时间戳的签名，该时间戳在同一 OID [#8629](https://github.com/NuGet/Home/issues/8629)下具有2个值

* 更新许可证列表- [#8544](https://github.com/NuGet/Home/issues/8544)

**Dcr**

* 将诊断文件载入 IFeedbackDiagnosticFileProvider- [#8535](https://github.com/NuGet/Home/issues/8535)

**[此版本中已修复的所有问题的列表-5。4](https://github.com/nuget/home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%225.4")**
