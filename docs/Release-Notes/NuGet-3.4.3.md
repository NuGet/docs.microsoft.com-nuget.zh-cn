---
title: "NuGet 3.4.3 发行说明 |Microsoft 文档"
author: karann-msft
ms.author: karann-msft
manager: ghogen
ms.date: 11/11/2016
ms.topic: article
ms.prod: nuget
ms.technology: 
ms.assetid: 60af25ad-e899-43ac-9236-8b8cb167bcde
description: "发行说明，了解 NuGet 3.4.3 包括已知问题、 bug 修复、 增加的功能，以及 DCRs。"
keywords: "NuGet 3.4.3 发行说明，bug 修复的已知问题，添加了一些功能，DCRs"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 6138d939136595d2d6dbff0dca9c88b09e70b43d
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/14/2017
---
# <a name="nuget-343-release-notes"></a>NuGet 3.4.3 发行说明

[NuGet 上面 3.4.2 发行说明](../release-notes/nuget-3.4.2.md) | [NuGet 3.4.4 发行说明](../release-notes/nuget-3.4.4.md)

NuGet 3.4.3 发布于 2016 年 4 月 22，为了解决发现 3.4 及后续版本中的几个问题。

你可以下载 VSIX 和 nuget.exe[此处](https://dist.nuget.org/index.html)。

## <a name="updates-and-improvements"></a>更新和改进

* 改进了 Visual Studio 可靠性。 在 Visual Studio 中导致崩溃的 NuGet 中，我们已解决的一些问题。

## <a name="fixes"></a>修补程序

* 使用密码保护私有 nuget 源固定一些授权问题。
* 修复了问题解决时无法进行还原 PCL 从`project.json`与指定的运行时。
* 某些客户安装程序包时遇到了出现间歇性故障。 此问题现在已在此版本中修复。
* 修复了问题导致还原故障，在 C + + /cli 项目与`project.json`。
* 其中不解压缩正确 mono 中使用 nuget 时某些包 (例如 ModernHttpClient)。 此问题现在已在此版本中修复。

有关此版本中的修补程序和改进的完整列表，请参阅的问题列表[此处](https://github.com/NuGet/Home/issues?q=is%3Aissue+milestone%3A3.4.3+is%3Aclosed)。