---
title: NuGet 2.8.6 发行说明
description: NuGet 2.8.6 包括的发行说明的已知问题、 bug 修复、 新增的功能和 Dcr。
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: d57c658999ed3c79b962de84fd973276833ef3fd
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/04/2018
ms.locfileid: "43546486"
---
# <a name="nuget-286-release-notes"></a>NuGet 2.8.6 发行说明

[NuGet 2.8.5 发行说明](../release-notes/nuget-2.8.5.md) | [NuGet 2.8.7 发行说明](../release-notes/nuget-2.8.7.md)

发布 NuGet 2.8.6 2015 年 7 月 20 日作为一项次要更新到我们 2.8.5 VSIX 某些目标修复和改进功能以支持具有支持的 Windows 10 UWP 开发模型可能会发送的包。

此版本的 NuGet 包管理器扩展提供仅支持 Visual Studio 2013。

此版本中，在 NuGet 包管理器对话框中必须添加对的支持：

* 引入了 UAP 目标框架名字对象以支持 Windows 10 应用程序开发。
* NuGet 的协议版本 3 终结点
* 为支持[Nuget.Config](../consume-packages/configuring-nuget-behavior.md) protocolVersion 属性存储库源。 默认值为"2"
* 回退到远程存储库如果所需的包版本在本地缓存中不可用