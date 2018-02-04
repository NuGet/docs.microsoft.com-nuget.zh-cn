---
title: "NuGet 2.8.6 发行说明 |Microsoft 文档"
author: karann-msft
ms.author: karann-msft
manager: ghogen
ms.date: 11/11/2016
ms.topic: article
ms.prod: nuget
ms.technology: 
ms.assetid: 920c551c-18a7-40f4-a32b-ce84de6ea766
description: "发行说明，了解 NuGet 2.8.6 包括已知问题、 bug 修复、 增加的功能，以及 DCRs。"
keywords: "NuGet 2.8.6 发行说明，bug 修复的已知问题，添加了一些功能，DCRs"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 4dfd0a76967280cc6a16b37fe2b2a3362231fce5
ms.sourcegitcommit: 4651b16a3a08f6711669fc4577f5d63b600f8f58
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/02/2018
---
# <a name="nuget-286-release-notes"></a>NuGet 2.8.6 发行说明

[NuGet 2.8.5 发行说明](../release-notes/nuget-2.8.5.md) | [NuGet 2.8.7 发行说明](../release-notes/nuget-2.8.7.md)

发布 NuGet 2.8.6 2015 年 7 月 20 日作为一项次要更新到我们 2.8.5 VSIX 一些针对修补程序和改进，可使用支持 Windows 10 UWP 开发模型支持可能会发送的包。

此版本的 NuGet 包管理器扩展提供仅支持 32 位 Visual Studio 2013。

在此版本中，NuGet 包管理器对话框必须添加对支持：

* 引入了 UAP 目标框架名字对象以支持 Windows 10 应用程序开发。
* NuGet 协议版本 3 终结点
* 支持[Nuget.Config](../consume-packages/configuring-nuget-behavior.md) protocolVersion 属性存储库源。 默认值为"2"
* 回退到远程存储库如果所需的程序包版本在本地缓存中不可用