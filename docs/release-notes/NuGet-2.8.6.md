---
title: NuGet 2.8.6 发行说明
description: NuGet 2.8.6 的发行说明，包括已知问题、bug 修复、新增功能和 Dcr。
author: JonDouglas
ms.author: jodou
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: ea291bdf7a5b6cc3ac3bde526030e517db4632d7
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/26/2021
ms.locfileid: "98776702"
---
# <a name="nuget-286-release-notes"></a>NuGet 2.8.6 发行说明

[NuGet 2.8.5 发行说明](../release-notes/nuget-2.8.5.md)  | [NuGet 2.8.7 发行说明](../release-notes/nuget-2.8.7.md)

NuGet 2.8.6 发布于2015年7月20日，作为对我们的 2.8.5 VSIX 的次要更新，其中包含一些目标修补程序和改进功能，可通过支持 Windows 10 UWP 开发模型提供支持。

此版本的 NuGet 包管理器扩展仅为 Visual Studio 2013 提供支持。

在此版本中，NuGet 包管理器对话框为添加了支持：

* 引入了 UAP 目标框架名字对象，以支持 Windows 10 应用程序开发。
* NuGet 协议版本3终结点
* 支持存储库源上 [Nuget.Config](../consume-packages/configuring-nuget-behavior.md) protocolVersion 属性。 默认值为 "2"
* 如果本地缓存中不提供所需的包版本，则回退到远程存储库