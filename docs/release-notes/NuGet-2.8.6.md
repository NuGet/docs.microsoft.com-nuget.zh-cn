---
title: NuGet 2.8.6 发行说明
description: 发行说明，了解 NuGet 2.8.6 包括已知问题、 bug 修复、 增加的功能，以及 DCRs。
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: ee801a0edfe22888d65506cea557fd9c79dcf7bd
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/26/2018
ms.locfileid: "31819713"
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