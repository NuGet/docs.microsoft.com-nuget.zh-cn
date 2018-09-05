---
title: NuGet 3.4.3 发行说明
description: NuGet 3.4.3 包括的发行说明的已知问题、 bug 修复、 新增的功能和 Dcr。
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 6ee4ecc06eb5119e24108d1cd6d2050254c45817
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/04/2018
ms.locfileid: "43549160"
---
# <a name="nuget-343-release-notes"></a>NuGet 3.4.3 发行说明

[NuGet 3.4.2 发行说明](../release-notes/nuget-3.4.2.md) | [NuGet 3.4.4 发行说明](../release-notes/nuget-3.4.4.md)

NuGet 3.4.3 发布于 2016 年 4 月 22，若要解决在 3.4 及后续版本中已发现的几个问题。

您可以下载的 VSIX 和 nuget.exe[此处](https://dist.nuget.org/index.html)。

## <a name="updates-and-improvements"></a>更新和改进

* 改进了 Visual Studio 可靠性。 我们已在 Visual Studio 中导致崩溃的 NuGet 中解决一些问题。

## <a name="fixes"></a>修补程序

* 修复一些授权问题与受密码保护私有 nuget 源。
* 修复了围绕无法还原 PCL 从`project.json`与指定的运行时。
* 安装包时，某些客户已遇到间歇性故障。 此问题现在已在此版本中修复。
* 修复了导致还原失败，在 C + + /cli 项目与`project.json`。
* 在其中不解压缩正确在 mono 中使用 nuget 时某些包 (例如 ModernHttpClient)。 此问题现在已在此版本中修复。

有关此版本中的修补程序和改进的完整列表，请参阅问题列表[此处](https://github.com/NuGet/Home/issues?q=is%3Aissue+milestone%3A3.4.3+is%3Aclosed)。