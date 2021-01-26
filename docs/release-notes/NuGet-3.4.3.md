---
title: NuGet 3.4.3 发行说明
description: NuGet 3.4.3 的发行说明，包括已知问题、bug 修复、新增功能和 Dcr。
author: JonDouglas
ms.author: jodou
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: f0d9740aaf0a82b9e4023b5e4990c8f4adbea63c
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/26/2021
ms.locfileid: "98776464"
---
# <a name="nuget-343-release-notes"></a>NuGet 3.4.3 发行说明

[NuGet 3.4.2 发行说明](../release-notes/nuget-3.4.2.md)  | [NuGet 3.4.4 发行说明](../release-notes/nuget-3.4.4.md)

NuGet 3.4.3 于2016年4月22日发布，以解决3.4 和后续版本中标识的几个问题。

可在 [此处](https://dist.nuget.org/index.html)下载 VSIX 和 nuget.exe。

## <a name="updates-and-improvements"></a>更新和改进

* 改进了 Visual Studio 的可靠性。 我们已修复了 NuGet 中导致 Visual Studio 崩溃的一些问题。

## <a name="fixes"></a>修复项

* 解决了密码保护的专用 nuget 源的一些授权问题。
* 解决了无法从 `project.json` 指定的运行时中还原 PCL 的问题。
* 有些客户在安装包时遇到间歇性故障。 此版本中现已修复此项。
* 修复了在 c + +/CLI 项目中导致还原失败的问题 `project.json` 。
* 某些包 (例如，当你在 mono 中使用 nuget 时，ModernHttpClient) 未正确进行解压缩。 此版本中现已修复此项。

有关此版本中的修复和改进的完整列表，请查看 [此处](https://github.com/NuGet/Home/issues?q=is%3Aissue+milestone%3A3.4.3+is%3Aclosed)的问题列表。